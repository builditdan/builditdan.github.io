---
layout: page
title: Contact Me
hide: true
feature-img: "img/bannera.jpg"
---

<script>
$(document).ready(function() {

  $("#quote-it").effect('fade', 3000);


});
$.getJSON("http://quotesondesign.com/wp-json/posts?filter[orderby]=rand&filter[posts_per_page]=1&callback=", function(a) {
  $("#quote-it").append(a[0].content + "<p>— " + a[0].title + "</p>")
});
</script>

<h4 class="thank-you">Your question has been submitted.</h4>

<blockquote id="quote-it"></blockquote>

<br>
Thank you,<br>
Dan
