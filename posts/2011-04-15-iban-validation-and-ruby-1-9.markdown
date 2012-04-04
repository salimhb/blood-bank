---
title: IBAN Validation and Ruby 1.9
slug: iban-validation-and-ruby-1-9
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 934
wordpress_url: http://blog.railslove.com/?p=934
published_at: 2011-04-15 15:52:30.000000000 +02:00
categories:
- rails
tags:
  keyword:
  - ruby
  - iban
  - bic
  - bank
  - data
  - account
---
In one of our projects <a href="http://9flats.com">9flats.com</a> we're using a short IBAN and SWIFT Validation rule to be sure the user entered valid bank account information.
To know how to validate an IBAN account number, just have a look at <a href="http://en.wikipedia.org/wiki/IBAN#Calculating_and_Validating_IBAN_checksums">this article on wikipedia</a>. Therefore you have to do a few steps to be sure get the right format of an IBAN number:

<blockquote>
<strong>Validating the IBAN</strong>
The basis of the IBAN validation is to convert the IBAN into a number and to perform a basic Mod-97 calculation (as described in ISO 7064) on it. If the IBAN is valid, then the remainder equals 1. Rule process of IBAN validation is:
<ul>
<li>Check that the total IBAN length is correct as per the country. If not, the IBAN is invalid.</li>
<li>Move the four initial characters to the end of the string.</li>
<li>Replace each letter in the string with two digits, thereby expanding the string, where A=10, B=11, ..., Z=35.</li>
<li>Interpret the string as a decimal integer and compute the remainder of that number on division by 97.</li>
</ul>
If the remainder is 1, the checks digits test is passed and the IBAN may be valid.
</blockquote>

I found a <a href="http://www.locknet.ro/article/iban-validation-and-beast">short (and also funny) blogpost</a> about a validation script in ruby. Unfortunely the expression
<code>
iban = value.gsub(/[A-Z]/) { | p | p[0]-55 }
</code>
does'n work anymore, because Ruby 1.9 doesn't return the integer ordinal of a one-character string using p[0]. Instead of that just use the .ord method on a string. So our Ruby 1.9 compatible code will looks like this:
<code>
iban = value.gsub(/[A-Z]/) { | p | p.ord-55 }
</code>
If you're using two or more environments (e.g.: Ruby 1.8 and Ruby 1.9) on your production or development machine (I know thats not the way to go, but it could happen for a little time) just ask if Ruby respond to the .ord method.
<code>
iban = value.gsub(/[A-Z]/) { |p| (p.respond_to?(:ord) ? p.ord : p[0]) - 55 }
</code>

The final code from the blogpost mentioned before will be looks like this:

<script src="https://gist.github.com/921728.js?file=gistfile1.rb"></script>

Small things can be very helpful!
