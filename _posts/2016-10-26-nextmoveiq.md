---
layout: post
title: NextMoveIQ.com is live!
---

I changed a few things on my capstone project including it’s name. It is now called NextMoveIQ located at [http://www.nextmoveiq.com/](http://www.nextmoveiq.com/). I did this based on some great feedback I received from the [Bloc Hacker Club](https://www.facebook.com/groups/blocalumni/) on Facebook.

I redesigned the way the questions are presented. I condensed all the questions into a single page that leads the user through each question. It does this by first disabling all but the first question on state. It then enables the next question as each answer is provided. I used Javascript/jQuery in Rails to accomplish this. It required allot of event detection. Including handling if the user switches the state or city then other fields would have to respond or reset appropriately.

I added two new questions. Does an area have big mountains and how much snow. I believe those questions are better indicators of the type of weather and seasons a state may offer. I removed the question on budget as it applies to home prices which can vary widely in some neighborhoods.

I changed the way the results are presented. Showing a simple list of cities that a user could browse along with their respective neighborhoods. I felt this flow was better than showing states and cities then on another page showing the neighborhoods. This created that SPA(Single Page Application) approach that is so popular now. Again,  I am using Javascript with Rails code to create that in page updating experience.

I hope you enjoy the site. Be sure to like and share the page and please send me your comments and feedback!  

Dan

Feel free to [contact me](http://builditdan.github.io/contact.html) with any questions you may have
