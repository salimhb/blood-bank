---
title: ! 'JavaScript: parseXMLString() - a reminder to myself... '
slug: javascript-parsexmlstring-a-reminder-to-myself
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 42
wordpress_url: http://blog.railslove.com/?p=42
published_at: 2008-09-27 16:04:51.000000000 +02:00
categories:
- javascript
tags:
  keyword:
  - javascript
  - xml
  - dom
  - parse
---
If you have a string containing a XML-document you need to tell the browser to parse the the DOM. Otherwise you can not access the nodes and work with it. Makes sense you say?!

yeah... but I've wasted far to much time on that. 

<strong>So remember: If you have a XML in a string convert it to a DOM-object to work with it otherwise you will see very strange results.</strong>

Here is a sample function: 

<pre lang="Javascript">

function parseXMLString(xmlString) {
  //for IE
  if (window.ActiveXObject) {
    var xml_tree = new ActiveXObject("Microsoft.XMLDOM");
    xml_tree.async = "false";
    xml_tree.loadXML(xmlString);
  }
  //for Mozilla, Firefox, Opera, etc.
 else if (document.implementation && document.implementation.createDocument) {
    var parser = new DOMParser();
    var xml_tree = parser.parseFromString(xmlString,"text/xml");
  }
  return xml_tree;
}
</pre>
 
This function accepts a string as parameter and uses ActiveXObject("Microsoft.XMLDOM") [IE] or DOMParser() [the rest of the gang] to parse it.
