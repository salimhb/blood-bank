---
title: Payment processing mit Rails, Activemerchant (PayPal) und Finite State Machine
slug: payment-processing-mit-rails-activemerchant-paypal-und-finite-state-machine
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
excerpt: ! "Wer schon überlegt hat <a href=\"https://www.paypal.com/\">PayPal</a>
  als Bezahlungsmöglichkeit auf seiner Rails-Platform zu integrieren, stößt schnell
  auf die aufschlußreiche Lektüre der <a href=\"http://www.pragprog.com/\">Pragmatic
  Programmers</a>: <a href=\"http://www.pragprog.com/titles/jfpaypal/payment-processing-with-paypal-and-ruby\">Payment
  Processing with Paypal and Ruby</a>. Dieses Buch legt einen sehr guten Grundstein
  für weitere Ideen wie sich eine Bezahlung via PayPal in einer RubyOnRails Anwendung
  realisieren lässt.\r\nIn diesem Blog-Post soll eine weitere Alternative vorgestellt
  werden, wie durch den Einsatz von <a href=\"http://www.activemerchant.org/\">Active
  Merchant</a> und des <a href=\"http://agilewebdevelopment.com/plugins/acts_as_state_machine\">Finite
  State Machine-Plugins</a> eine einfache PayPal Express Bezahlung in Rails realisiert
  werden kann. Basierend auf dem  Blogeintrag von Cody Fauser <a href=\"http://www.codyfauser.com/2008/1/17/paypal-express-payments-with-activemerchant\">PayPal
  Express Payments with ActiveMerchant</a> und, ebenso von Cody Fauster veröffentlichtem
  eBook <a href=\"https://peepcode.com/products/activemerchant-pdf\">Active Merchant;
  Show me the money!</a> möchte ich den Paymentprozess mit Paypal um das FSM-Plugin
  erweitern.\r\n"
wordpress_id: 34
wordpress_url: http://blog.railslove.com/?p=34
published_at: 2008-09-16 12:54:59.000000000 +02:00
categories:
- railslove
- rails
- plugins
tags:
  keyword:
  - activemerchant
  - paypal
  - finale-state-machine
  - process
  - fsm
  - checkout
---
Wer schon überlegt hat <a href="https://www.paypal.com/">PayPal</a> als Bezahlungsmöglichkeit auf seiner Rails-Platform zu integrieren, stößt schnell auf die aufschlußreiche Lektüre der <a href="http://www.pragprog.com/">Pragmatic Programmers</a>: <a href="http://www.pragprog.com/titles/jfpaypal/payment-processing-with-paypal-and-ruby">Payment Processing with Paypal and Ruby</a>. Dieses Buch legt einen sehr guten Grundstein für weitere Ideen wie sich eine Bezahlung via PayPal in einer RubyOnRails Anwendung realisieren lässt.
In diesem Blog-Post soll eine weitere Alternative vorgestellt werden, wie durch den Einsatz von <a href="http://www.activemerchant.org/">Active Merchant</a> und des <a href="http://agilewebdevelopment.com/plugins/acts_as_state_machine">Finite State Machine-Plugins</a> eine einfache PayPal Express Bezahlung in Rails realisiert werden kann. Basierend auf dem  Blogeintrag von Cody Fauser <a href="http://www.codyfauser.com/2008/1/17/paypal-express-payments-with-activemerchant">PayPal Express Payments with ActiveMerchant</a> und, ebenso von Cody Fauster veröffentlichtem eBook <a href="https://peepcode.com/products/activemerchant-pdf">Active Merchant; Show me the money!</a> möchte ich den Paymentprozess mit Paypal um das FSM-Plugin erweitern.
<a id="more"></a><a id="more-34"></a>
Zunächst einmal muss man über ein PayPal-Developer-Account verfügen. In den oben genannten Lektüren von den Pragmatic Programmers und Cody Fauser ist das PayPal-Setup genau beschrieben. Auch unter <a href="https://developer.paypal.com/">https://developer.paypal.com/</a> finden sich genaue Anweisungen wie man ein Developer-Account anlegt. Jetzt brauchen wir zwei Sandbox-Accounts: einen Business-Account und ein Persona-Account (Seller & Buyer). Mit diesem Setup können wir uns an die Entwicklung unserer PayPal-Rails-App begeben.

Zunächst legen wir die Rails-Applikation an:
<pre lang="ruby">
! rails paypalcheckout
</pre>

Weiterhin brauchen wir das FSM-Plugin:

<pre lang="ruby">
! script/plugin install \
http://elitists.textdriven.com/svn/plugins/acts_as_state_machine/trunk
</pre>

Und das ActiveMerchant-Plugin:

<pre lang="ruby">
! script/plugin install \
git://github.com/Shopify/active_merchant.git
</pre>

Wir müssen uns jetzt überlegen, wie unser Payment-Model aussehen soll, um später Attribute des einkaufenden Users in unserer Datenbank abzulegen. Legen wir unser Model an:

<pre lang="ruby">
! script/generate model payment price:integer initial_mail:string \
payer_id:string firstname:string \
middelname:string, lastname:string \
email:string payer_country:string \
company:string address1:string \
address2:string city:string \
state:string confirmed_at:datetime \
completed_at:datetime token:string
</pre>

Die Attribute <em>state, confirmed_at, completed_at</em> brauchen wir für unser FSM-Plugin. Der Rest wird mit den Rückgabeparametern von PayPal gefüllt.
Nachfolgende Abbildung stellt unsere Finite State Machine dar, die wir implementieren wollen. 

<a href="http://www.ipernity.com/doc/66233/2943504"><img src="http://u1.ipernity.com/8/35/04/2943504.2f4523ae.240.jpg" width="240" height="136" alt="Payment processing mit Rails, Activemerchant (PayPal) und Finite State Machine" border="0"/></a>

Das Payment-Objekt wird default als <em>pending</em> Markiert. Sprich: der Benutzer hat den Paymentprozess eingeleitet. Nachdem der User auf PayPal die Bezahlung bestätigt hat, fällt er in den Zustand <em>confirmed</em>. Nach einer letzten Bestätigung in unserer Applikation und einer erfolgreichen Überweisung des Geldes fällt er in den Zustand <em>completed</em>. Dementsprechend ergänzen wir unser Model mit folgendem Code:

<pre lang="ruby">
  # app/models/payment.rb
  acts_as_state_machine :initial => :pending

  state :pending,
  state :confirmed, :enter => :do_confirm
  state :completed, :enter => :do_complete

  event :confirm do
    transitions :to => :confirmed, :from => :pending
  end

  event :complete do
    transitions :to => :completed, :from => :confirmed
  end

</pre>

und wir ergänzen das Model mit den Methoden <em>do_confirm</em> und <em>do_complete</em> die den Zeitstempel setzen, indem der Zustand gesetzt wurde:

<pre lang="ruby">
  # app/models/payment.rb
  def do_complete
    self.completed_at = Time.now
  end

  def do_confirm
    self.confirmed_at = Time.now
  end
</pre>

Wir werden unser Model noch gleich ergänzen. Kommen wir zu unserem Payment-Controller. Wir generieren ihn ohne die <em>create</em> Methode, da wir dafür keinen View brauchen:

<pre lang="ruby">
! script/generate controller Payments new confirm complete
</pre>

Als nächstes binden wir das ActiveMerchant-Plugin ein:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  include ActiveMerchant::Billing
</pre>

Wir müssen ActiveMerchant noch in den Test-Modus zwingen, da die Default-Einstellung den Production-Modus von PayPal nutzt, somit würde PayPal mit unseren Sandbox-Keys nicht akzeptieren würde. Dies machen wir indem wir die <em>config/environments/development.rb</em> um folgende Zeilen ergänzen:

<pre lang="ruby">
  # config/environments/development.rb
  config.after_initialize do
    ActiveMerchant::Billing::Base.mode = :test
  end
</pre>

Weiterhin ergänzen wir unsere <em>new</em> Methode, und erstellen ein neues Payment-Objekt:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  def new
    @payment = Payment.new
    respond_to do |format|
      format.html
    end
  end
</pre>

Als nächstes brauchen wir noch die <em>create</em> Methode, die unser Objekt abspeichert und uns zu PayPal weiterleitet:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  def create
    @payment = Payment.create(params[:payment])

    respond_to do |format|
      if @payment.save
        flash[:notice] = 'Payment was successfully created.'
        setup_response = gateway.setup_purchase(@payment.price,
        :ip                      => request.remote_ip,
        :return_url           => confirm_payment_url(@payment),
        :cancel_return_url => root_url
        )
        format.html { 
          redirect_to gateway.redirect_url_for(setup_response.token) 
          }
      else
        format.html { 
          render :action => "new" 
          }
      end
    end
  end
</pre>


An dieser Stelle, brauchen wir ein <em>gateway-Objekt</em>, dass für uns den Paymentprozess handelt. Wir ergänzen unseren Controller um folgende Zeilen (alle Informationen zur API-Signatur von PayPal gibt es im <a href="https://www.paypal.com/IntegrationCenter/ic_api-signature.html">IntegrationCenter von PayPal</a>:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  private

  def gateway
    @gateway ||= PaypalExpressGateway.new(
    :login => 'PAPAL_LOGIN',
    :password => 'PAYPAL_PASSWORD',
    :signature => 'PAYPAL_API_SIGNATURE'
    )
  end
</pre>

Das <em>gateway-Objekt</em> handelt für uns die Return-Parameter, die Paypal mitgeteilt werden und den Preis, der für den gewünschten Order verlangt wird.
Als nächstes füllen wir den View, indem der User seine E-Mail-Adresse angibt und somit den Payment-Prozess anstösst:

<pre lang="ruby">
# app/views/payments/new.html.erb
<h1>New payment</h1>

<% form_for(@payment) do |f| %>
  <%= f.error_messages %>
  <p>
    <%= f.label :initial_mail, "Your Email" %>
    <%= f.text_field :initial_mail %>
  </p>
  <p>
    <%= f.label :price, "How much?" %>
    <%= f.text_field :price %>
  </p>
  <p>
    <%= f.submit "Create" %>
  </p>
<% end %>
</pre>

Nun sind wir mit dem ersten Schritt soweit: wir speichern einen User im Pending-Zustand ab, leiten einen PayPal-Payment-Prozess ein und mit einem vorher generiertem Token leiten wir den User zur PayPalseite. Zuvor wurden Return-Urls gesetzt, zu die PayPal zurückleitet.
Wenn wir unsere App starten, werden wir nach Eingabe unserer E-Mail-Adresse zu PayPal weitergeleitet um die Bezahlung zu bestätigen. Hier loggen wir uns mit unserem, zuvor angeletem, <em>buyer</em>-Sandbox-Account ein (bitte zuvor generell in die Sandbox einloggen). Auf der PayPal-Seite bestätigen wir unsere Bezahlung und werden auf die Bestätigungsseite unserer Applikation zurückgeleitet. Die wir als nächstes implementieren:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  def confirm
    @payment = Payment.find(params[:id])
    redirect_to(root_url) and return unless params[:token]     
    details_response = gateway.details_for(params[:token])
    
    if !details_response.success?
      @message = details_response.message
      render :action => 'error'
      return
    end
    
    @payment.map_paypal_response(details_response)
    @payment.confirm!
    
  end
</pre>

Wir suchen uns als nächstes unser Paymentobjetk heraus und prüfen ob ein Token von Paypal gesetzt worden ist - nur so werden wir den Einkaufsprozess erlauben. Als nächstes fragen wir PayPal nach den Details des PayPal-Prozesses an. Leider sind die Rückgabeparameter von <em>details_response</em> in der <a href="http://activemerchant.rubyforge.org/">ActiveMerchant-Dokumentation</a> nicht beschrieben, daher möchte ich diese hier noch mal auflisten:

<pre lang="ruby">
    # "payer_id"=>"AAAAAASME9AEGQ", 
    # "first_name"=>"Test", 
    # "last_name"=>"User", 
    # "middle_name"=>nil,
    # "payer"=>"team_12234567888_per@railslabs.com", 
    # "payer_country"=>"US", 
    # "payer_business"=>nil, 
    # "street1"=>"1 Main St", 
    # "street2"=>nil, 
    # "city_name"=>"San Jose", 
    # "token"=>"EC-12345641FA574341C", 

    # "postal_code"=>"95131", 
    # "country_name"=>"United States", 
    # "state_or_province"=>"CA", 
    # "name"=>"Test User", 
    # "address_owner"=>"PayPal", 
    # "timestamp"=>"2008-09-06T10:12:01Z", 
    # "correlation_id"=>"558cdcfa7777b1", 
    # "country"=>"US", 
    # "salutation"=>nil, 
    # "build"=>"671339", 
    # "version"=>"52.0", 
    # "address_status"=>"Confirmed", 
    # "payer_status"=>"verified", 
    # "suffix"=>nil, 
    # "ack"=>"Success", 
</pre>

Weiterhin bietet ActiveMerchant ein <a href="http://activemerchant.rubyforge.org/classes/ActiveMerchant/Billing/PaypalExpressResponse.html">PaypalExpressResponse-Objekt</a> an, das meiner Meinung nach etwas unglücklich implementiert worden ist, denn es verarbeitet nicht alle Parameter und definiert Wrappermethoden für einzelne Parameter. Daher habe ich die Methode <em>map_paypal_response(details_response)</em> in unserem Payment-Model definiert, die beispielhaft die ersten zehn, der oben genannten Parameter von PaPal auf unser, vorhin angelegtes Model mappt:

<pre lang="ruby">
  # app/models/payment.rb
  def map_paypal_response(details_response)
    self.attributes = {
      :payer_id => details_response.params['payer_id'],
      :firstname => details_response.params['first_name'], 
      :lastname => details_response.params['last_name'], 
      :middelname => details_response.params['middle_name'], 
      :email => details_response.params['payer'],
      :payer_country => details_response.params['payer_country'],
      :company => details_response.params['payer_business'],
      :address1 => details_response.params['street1'],
      :address2 => details_response.params['street2'],
      :city => details_response.params['city_name'],
      :token => details_response.params['token']
    }
  end
</pre>

Weiterhin brauchen wir noch einen <em>error</em>-View, der uns bei Fehlern entsprechende Statusmessages von PayPal zurückgibt:

<pre lang="ruby">
  # app/views/payments/error.html.erb
  <h1>Error</h1>
  <p>Unfortunately an error occurred: <%= @message %></p>
</pre>

Zu guter letzt speichern wir das Objekt mit der <em>confirm!</em> Methode und setzen es in den Zustand <em>confirmed</em>. Nun legen wir unseren <em>confirm.html.erb</em>-View an:

<pre lang="ruby">
# app/views/payments/confirm.html.erb
<h1>Please Confirm Your Payment Details</h1>

<p><strong>Name</strong>: 
  <%= @payment.firstname%>
  <%= @payment.lastname%>
  <%= @payment.middelname%><br />
<strong>Company</strong>: <%= @payment.company%><br />
<strong>Address 1</strong>: <%= @payment.address1%><br />
<strong>Address 2</strong>: <%= @payment.address2%><br />
<strong>City</strong>: <%= @payment.city%><br />
<strong>Email</strong>: <%= @payment.email%><br />

<% form_tag complete_payment_url(@payment), :method => :put do %>
  <%= submit_tag 'Complete Payment' %>
<% end %>
</pre>

An dieser Stelle bestätigt der User das letzte mal die Bezahlung, die dann im Controller in der <em>complete</em>-Definition eingeleitet wird:

<pre lang="ruby">
  def complete
    @payment = Payment.find(params[:id])
    purchase = gateway.purchase(@payment.price,
    :ip       => request.remote_ip,
    :payer_id => @payment.payer_id,
    :token    => @payment.token
    )
    unless purchase.success?
      @message = purchase.message
      render :action => 'error'
      return
    end

    @payment.complete!
  end
</pre>

Und somit haben wir den Payment-Prozess abgeschlossen. Der Payment-Zustand wird auf <em>complete</em> gesetzt, wenn die Bezahlung gelungen ist. Falls ein Fehler auftritt, wird die <em>error.html.erb</em> mit einer entsprechenden Fehlermeldung aufgerufen. Natürlich kann man an dieser Stelle die Antwort von PayPal (<em>purchase</em>) weiterverarbeiten um komplexere oder genauere Operationen bei Fehlschlagen (oder gelingen) eines Payments vorzunehmen.
