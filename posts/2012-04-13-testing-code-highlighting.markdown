---
title: Testing Code Highlighting
slug: testing-code-highlighting
author: salim_hbeiliny
published: false
published_at: 2012-04-13
categories:
- railslove
---
<pre class="sh_javascript">
$(document).bind("showoff:loaded", function (event) {
  $('.content').each( function(index){
    $(this).parents('.slide').addClass($(this)[0].className).removeClass('content');
  });
});
</pre>