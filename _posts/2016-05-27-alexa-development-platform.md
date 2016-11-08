---
layout: post
title: Alexa development platform
---

 I started playing around with the Alexa platform to develop what they call a skill for the echo device. Kevin Utter posted a very easy  [walk-thru](https://developer.amazon.com/public/community/post/TxDJWS16KUPVKO/New-Alexa-Skills-Kit-Template-Build-a-Trivia-Skill-in-under-an-Hour) which I followed and completed in about an hour or so. You will need a AWS and Developer account but if you already have a Amazon login then you are good. Kevin's steps were easy to follow and I simply pasted in the sample index.js in the Github [Reindeer Games](https://github.com/amzn/alexa-skills-kit-js/tree/master/samples/reindeerGames/src) project and modified it as needed. My changes focused on just the questions and answers in the JSON object. I also tweaked the introduction.


I named my skill **Wordsmith Trivia** and spent additional time just creating all the definitions. I did take care that Alexa was able to properly pronounce all the words. Sometimes just adding a space in the middle of the word did the trick. Periods are important to slow her down. You can use the [Speech Synthesis Markup Language (SSML)](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/speech-synthesis-markup-language-ssml-reference) to tweak her speech and even have her use a phonemic/phonetic pronunciation. I ended up adding 50 questions and will expand them if I see the skill getting used. I believe you have analytics as well. I tested my skill thru the developer console using the voice and interaction tool. Once I get an echo myself, I will enjoy playing my trivia game. :)

I did some thinking about what else I could develop. So in the spirit of sharing - below is a few use cases I was thinking of developing as time permits.

![Remind me skill for Alexa](/img/alexa_skills_001.jpeg)
![Message journal skill for Alexa](/img/alexa_skills_002.jpeg)
![Food substitution skill for Alexa](/img/alexa_skills_003.jpeg)

This [site](http://lovemyecho.com/2016/03/04/complete-listing-of-alexa-skills-as-of-3416/) was helpful as I found it hard to get a complete listing of existing echo skills. Take care and hope you give Kevin's tutorial a try.

-Dan
