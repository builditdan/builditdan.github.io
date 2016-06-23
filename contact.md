---
layout: page
title: Contact Me
feature-img: "img/bannera.jpg"
---

<!-- CSS -->
<link rel="stylesheet" href="/css/contact.css">

<script>
function validateForm( form )
{

  if (form.elements['Message'].value && form.elements['Name'].value && form.elements['Email'].value)
      return true;
  else
      swal({   title: "Stop!",   text: "Please provide your name, email, and a message first!",   type: "error",   confirmButtonText: "Ok" });
      return false;
  end

}
</script>

<form action="https://getsimpleform.com/messages?form_api_token=a40fe9a3a332c4ccb89ae70732486336" method="post" onSubmit="return validateForm( this );">
  <!-- use this one for testing <input type='hidden' name='redirect_to' value='http://localhost:4000/thank-you.html' /> -->
  <input type='hidden' name='redirect_to' value='http://builditdan.github.io/thank-you.html' />


  <div id="page-wrap">

		<h2>Contact Form</h2>
		<p>I am looking forward to hearing from you. You have some fields and button below so you know what to do!</p>

		<div id="contact-area">

			<form method="post" >
      <!-- <form method="post" action="contactengine.php"> -->
				<label for="Name">Name:</label>
				<input type="text" name="Name" id="Name" />

				<label for="Email">Email:</label>
				<input type="text" name="Email" id="Email" />

				<label for="Message">Message:</label><br />
				<textarea name="Message" rows="20" cols="20" id="Message"></textarea>

				<input type="submit" name="submit" value="Submit" class="submit-button" />
			</form>

			<div style="clear: both;"></div>

		</div>

	</div>


</form>