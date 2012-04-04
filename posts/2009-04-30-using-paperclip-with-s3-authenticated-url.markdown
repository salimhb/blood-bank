---
title: Using Paperclip with S3 authenticated url
slug: using-paperclip-with-s3-authenticated-url
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 188
wordpress_url: http://blog.railslove.com/?p=188
published_at: 2009-04-30 15:13:29.000000000 +02:00
categories:
- rails
- plugins
- channelthing
- app-in-7-days
- yai7d
- s3
- security
- attachments
---
Für <a href="http://channelthing.com/landing.html">Channelthing</a> ist es besonders wichtig, dass die hochgeladenen Dokumente, die wir bei <a href="http://aws.amazon.com/s3/">S3</a> ablegen, nur durch authentifizierte Benutzer abgerufen werden können. Daher haben wir uns eine kleine Extension zu <a href="http://thoughtbot.com/projects/paperclip">Paperclip</a> gebaut, die solch eine verschlüsselte URL von S3 erhält, sobald ein Dokument, etc. angezeigt werden soll. 

Dazu muss man zum einen den Bucket erstmal "sicher" machen. Mit der kleinen Firefox-Extension <a href="http://www.s3fox.net/Features.aspx?isnew=true&from=addon">S3Fox Organizer</a>. Man erlaubt nur dem Owner auf das Bucket zuzugreifen.

Unsere Extension erhält nur die Methode <em>authenticated_s3_url</em> die über die <em>get_link</em> Methode von dem s3-Objekt unsere URL mit einem Hash zurückgibt der nur über eine bestimmte Zeit aufgerufen werden kann. Die <em>url</em>-Methode von Paperclip überscheiben wir anschliessend.

<pre lang="ruby">
module Railslove
  module Paperclip
    module SecureS3
      
      def authenticated_s3_url(style = nil, include_updated_timestamp = true, time_limit = 15.minutes)
        url = original_filename.nil? ? interpolate(@default_url, style) : self.s3.interface.get_link(self.s3_bucket.to_s, self.path(style), time_limit) 
        include_updated_timestamp && updated_at ? [url, updated_at].compact.join(url.include?("?") ? "&" : "?") : url
      end
      
    end
  end
end

Paperclip::Attachment.send(:include, Railslove::Paperclip::SecureS3)
Paperclip::Attachment.class_eval("alias :url :authenticated_s3_url")
</pre>

Man sollte daran denken auch die entsprechenden Rechte, jedem hochgeladenem Dokument zu setzen. Die können über den Parameter <em>s3_permissions</em> gesetzt werden:

<pre lang="ruby">
paperclip:
    storage: "s3"
    s3_credentials: <%= "#{RAILS_ROOT}/config/s3.yml" %>
    path: ":attachment/:id/:style.:extension"
    bucket: "RailsloveLovesS3"
    s3_permssions: "authenticated-read"
</pre>

Nun haben wir unser gewünschtes Ziel erreicht.
