--- 
title: Payment processing mit Rails, Activemerchant (PayPal) und Finite State Machine
slug: payment-processing-mit-rails-activemerchant-paypal-und-finite-state-machine
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
excerpt: |
  Wer schon &Atilde;&frac14;berlegt hat <a href="https://www.paypal.com/">PayPal</a> als Bezahlungsm&Atilde;&para;glichkeit auf seiner Rails-Platform zu integrieren, st&Atilde;&para;&Atilde;?t schnell auf die aufschlu&Atilde;?reiche Lekt&Atilde;&frac14;re der <a href="http://www.pragprog.com/">Pragmatic Programmers</a>: <a href="http://www.pragprog.com/titles/jfpaypal/payment-processing-with-paypal-and-ruby">Payment Processing with Paypal and Ruby</a>. Dieses Buch legt einen sehr guten Grundstein f&Atilde;&frac14;r weitere Ideen wie sich eine Bezahlung via PayPal in einer RubyOnRails Anwendung realisieren l&Atilde;&curren;sst.
  In diesem Blog-Post soll eine weitere Alternative vorgestellt werden, wie durch den Einsatz von <a href="http://www.activemerchant.org/">Active Merchant</a> und des <a href="http://agilewebdevelopment.com/plugins/acts_as_state_machine">Finite State Machine-Plugins</a> eine einfache PayPal Express Bezahlung in Rails realisiert werden kann. Basierend auf dem  Blogeintrag von Cody Fauser <a href="http://www.codyfauser.com/2008/1/17/paypal-express-payments-with-activemerchant">PayPal Express Payments with ActiveMerchant</a> und, ebenso von Cody Fauster ver&Atilde;&para;ffentlichtem eBook <a href="https://peepcode.com/products/activemerchant-pdf">Active Merchant; Show me the money!</a> m&Atilde;&para;chte ich den Paymentprozess mit Paypal um das FSM-Plugin erweitern.

wordpress_id: 34
wordpress_url: http://blog.railslove.com/?p=34
published_at: 2008-09-16 12:54:59 +02:00
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
Wer schon &Atilde;&frac14;berlegt hat <a href="https://www.paypal.com/">PayPal</a> als Bezahlungsm&Atilde;&para;glichkeit auf seiner Rails-Platform zu integrieren, st&Atilde;&para;&Atilde;?t schnell auf die aufschlu&Atilde;?reiche Lekt&Atilde;&frac14;re der <a href="http://www.pragprog.com/">Pragmatic Programmers</a>: <a href="http://www.pragprog.com/titles/jfpaypal/payment-processing-with-paypal-and-ruby">Payment Processing with Paypal and Ruby</a>. Dieses Buch legt einen sehr guten Grundstein f&Atilde;&frac14;r weitere Ideen wie sich eine Bezahlung via PayPal in einer RubyOnRails Anwendung realisieren l&Atilde;&curren;sst.
In diesem Blog-Post soll eine weitere Alternative vorgestellt werden, wie durch den Einsatz von <a href="http://www.activemerchant.org/">Active Merchant</a> und des <a href="http://agilewebdevelopment.com/plugins/acts_as_state_machine">Finite State Machine-Plugins</a> eine einfache PayPal Express Bezahlung in Rails realisiert werden kann. Basierend auf dem  Blogeintrag von Cody Fauser <a href="http://www.codyfauser.com/2008/1/17/paypal-express-payments-with-activemerchant">PayPal Express Payments with ActiveMerchant</a> und, ebenso von Cody Fauster ver&Atilde;&para;ffentlichtem eBook <a href="https://peepcode.com/products/activemerchant-pdf">Active Merchant; Show me the money!</a> m&Atilde;&para;chte ich den Paymentprozess mit Paypal um das FSM-Plugin erweitern.
<a id="more"></a><a id="more-34"></a>
Zun&Atilde;&curren;chst einmal muss man &Atilde;&frac14;ber ein PayPal-Developer-Account verf&Atilde;&frac14;gen. In den oben genannten Lekt&Atilde;&frac14;ren von den Pragmatic Programmers und Cody Fauser ist das PayPal-Setup genau beschrieben. Auch unter <a href="https://developer.paypal.com/">https://developer.paypal.com/</a> finden sich genaue Anweisungen wie man ein Developer-Account anlegt. Jetzt brauchen wir zwei Sandbox-Accounts: einen Business-Account und ein Persona-Account (Seller & Buyer). Mit diesem Setup k&Atilde;&para;nnen wir uns an die Entwicklung unserer PayPal-Rails-App begeben.

Zun&Atilde;&curren;chst legen wir die Rails-Applikation an:
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

Wir m&Atilde;&frac14;ssen uns jetzt &Atilde;&frac14;berlegen, wie unser Payment-Model aussehen soll, um sp&Atilde;&curren;ter Attribute des einkaufenden Users in unserer Datenbank abzulegen. Legen wir unser Model an:

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

Die Attribute <em>state, confirmed_at, completed_at</em> brauchen wir f&Atilde;&frac14;r unser FSM-Plugin. Der Rest wird mit den R&Atilde;&frac14;ckgabeparametern von PayPal gef&Atilde;&frac14;llt.
Nachfolgende Abbildung stellt unsere Finite State Machine dar, die wir implementieren wollen. 

<a href="http://www.ipernity.com/doc/66233/2943504"><img src="http://u1.ipernity.com/8/35/04/2943504.2f4523ae.240.jpg" width="240" height="136" alt="Payment processing mit Rails, Activemerchant (PayPal) und Finite State Machine" border="0"/></a>

Das Payment-Objekt wird default als <em>pending</em> Markiert. Sprich: der Benutzer hat den Paymentprozess eingeleitet. Nachdem der User auf PayPal die Bezahlung best&Atilde;&curren;tigt hat, f&Atilde;&curren;llt er in den Zustand <em>confirmed</em>. Nach einer letzten Best&Atilde;&curren;tigung in unserer Applikation und einer erfolgreichen &Atilde;?berweisung des Geldes f&Atilde;&curren;llt er in den Zustand <em>completed</em>. Dementsprechend erg&Atilde;&curren;nzen wir unser Model mit folgendem Code:

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

und wir erg&Atilde;&curren;nzen das Model mit den Methoden <em>do_confirm</em> und <em>do_complete</em> die den Zeitstempel setzen, indem der Zustand gesetzt wurde:

<pre lang="ruby">
  # app/models/payment.rb
  def do_complete
    self.completed_at = Time.now
  end

  def do_confirm
    self.confirmed_at = Time.now
  end
</pre>

Wir werden unser Model noch gleich erg&Atilde;&curren;nzen. Kommen wir zu unserem Payment-Controller. Wir generieren ihn ohne die <em>create</em> Methode, da wir daf&Atilde;&frac14;r keinen View brauchen:

<pre lang="ruby">
! script/generate controller Payments new confirm complete
</pre>

Als n&Atilde;&curren;chstes binden wir das ActiveMerchant-Plugin ein:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  include ActiveMerchant::Billing
</pre>

Wir m&Atilde;&frac14;ssen ActiveMerchant noch in den Test-Modus zwingen, da die Default-Einstellung den Production-Modus von PayPal nutzt, somit w&Atilde;&frac14;rde PayPal mit unseren Sandbox-Keys nicht akzeptieren w&Atilde;&frac14;rde. Dies machen wir indem wir die <em>config/environments/development.rb</em> um folgende Zeilen erg&Atilde;&curren;nzen:

<pre lang="ruby">
  # config/environments/development.rb
  config.after_initialize do
    ActiveMerchant::Billing::Base.mode = :test
  end
</pre>

Weiterhin erg&Atilde;&curren;nzen wir unsere <em>new</em> Methode, und erstellen ein neues Payment-Objekt:

<pre lang="ruby">
  # app/controller/payments_controller.rb
  def new
    @payment = Payment.new
    respond_to do |format|
      format.html
    end
  end
</pre>

Als n&Atilde;&curren;chstes brauchen wir noch die <em>create</em> Methode, die unser Objekt abspeichert und uns zu PayPal weiterleitet:

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


An dieser Stelle, brauchen wir ein <em>gateway-Objekt</em>, dass f&Atilde;&frac14;r uns den Paymentprozess handelt. Wir erg&Atilde;&curren;nzen unseren Controller um folgende Zeilen (alle Informationen zur API-Signatur von PayPal gibt es im <a href="https://www.paypal.com/IntegrationCenter/ic_api-signature.html">IntegrationCenter von PayPal</a>:

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

Das <em>gateway-Objekt</em> handelt f&Atilde;&frac14;r uns die Return-Parameter, die Paypal mitgeteilt werden und den Preis, der f&Atilde;&frac14;r den gew&Atilde;&frac14;nschten Order verlangt wird.
Als n&Atilde;&curren;chstes f&Atilde;&frac14;llen wir den View, indem der User seine E-Mail-Adresse angibt und somit den Payment-Prozess anst&Atilde;&para;sst:

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

Nun sind wir mit dem ersten Schritt soweit: wir speichern einen User im Pending-Zustand ab, leiten einen PayPal-Payment-Prozess ein und mit einem vorher generiertem Token leiten wir den User zur PayPalseite. Zuvor wurden Return-Urls gesetzt, zu die PayPal zur&Atilde;&frac14;ckleitet.
Wenn wir unsere App starten, werden wir nach Eingabe unserer E-Mail-Adresse zu PayPal weitergeleitet um die Bezahlung zu best&Atilde;&curren;tigen. Hier loggen wir uns mit unserem, zuvor angeletem, <em>buyer</em>-Sandbox-Account ein (bitte zuvor generell in die Sandbox einloggen). Auf der PayPal-Seite best&Atilde;&curren;tigen wir unsere Bezahlung und werden auf die Best&Atilde;&curren;tigungsseite unserer Applikation zur&Atilde;&frac14;ckgeleitet. Die wir als n&Atilde;&curren;chstes implementieren:

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

Wir suchen uns als n&Atilde;&curren;chstes unser Paymentobjetk heraus und pr&Atilde;&frac14;fen ob ein Token von Paypal gesetzt worden ist - nur so werden wir den Einkaufsprozess erlauben. Als n&Atilde;&curren;chstes fragen wir PayPal nach den Details des PayPal-Prozesses an. Leider sind die R&Atilde;&frac14;ckgabeparameter von <em>details_response</em> in der <a href="http://activemerchant.rubyforge.org/">ActiveMerchant-Dokumentation</a> nicht beschrieben, daher m&Atilde;&para;chte ich diese hier noch mal auflisten:

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

Weiterhin bietet ActiveMerchant ein <a href="http://activemerchant.rubyforge.org/classes/ActiveMerchant/Billing/PaypalExpressResponse.html">PaypalExpressResponse-Objekt</a> an, das meiner Meinung nach etwas ungl&Atilde;&frac14;cklich implementiert worden ist, denn es verarbeitet nicht alle Parameter und definiert Wrappermethoden f&Atilde;&frac14;r einzelne Parameter. Daher habe ich die Methode <em>map_paypal_response(details_response)</em> in unserem Payment-Model definiert, die beispielhaft die ersten zehn, der oben genannten Parameter von PaPal auf unser, vorhin angelegtes Model mappt:

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

Weiterhin brauchen wir noch einen <em>error</em>-View, der uns bei Fehlern entsprechende Statusmessages von PayPal zur&Atilde;&frac14;ckgibt:

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

An dieser Stelle best&Atilde;&curren;tigt der User das letzte mal die Bezahlung, die dann im Controller in der <em>complete</em>-Definition eingeleitet wird:

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

Und somit haben wir den Payment-Prozess abgeschlossen. Der Payment-Zustand wird auf <em>complete</em> gesetzt, wenn die Bezahlung gelungen ist. Falls ein Fehler auftritt, wird die <em>error.html.erb</em> mit einer entsprechenden Fehlermeldung aufgerufen. Nat&Atilde;&frac14;rlich kann man an dieser Stelle die Antwort von PayPal (<em>purchase</em>) weiterverarbeiten um komplexere oder genauere Operationen bei Fehlschlagen (oder gelingen) eines Payments vorzunehmen.
