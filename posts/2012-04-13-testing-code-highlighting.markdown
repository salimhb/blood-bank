---
title: Testing Code Highlighting
slug: testing-code-highlighting
author: salim_hbeiliny
published: true
published_at: 2012-04-13
categories:
- railslove
---
<pre class="hs_js">
  $(document).bind("showoff:loaded", function (event) {
    $('.content').each( function(index){
      $(this).parents('.slide').addClass($(this)[0].className).removeClass('content');
    });
  });
</pre>