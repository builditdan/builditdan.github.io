---
layout: post
title: Alexa Skills (Wordsmith Trivia & Political Geek)
---

As part of my full stack training with [bloc.io](bloc.io), I completed two Alexa skills. Both have been accepted by Amazon. The first one is called [Wordsmith Trivia](https://github.com/dale3h/alexa-skills-list/tree/master/skills/B01G91DCFI) and the other is [Political Geek](https://github.com/builditdan/politicalgeek). For both of these, I followed the Amazon provided templates on [Github](https://github.com/amzn/alexa-skills-kit-js). I used [Space Geek](https://github.com/amzn/alexa-skills-kit-js/tree/master/samples/spaceGeek) for Political Geek and explained in a [previous post](http://builditdan.github.io/2016/05/27/alexa-development-platform.html) want I did for Wordsmith Trivia.

The process was pretty straight forward and well documented regarding how to get these skills live. The instructions were listed so nicely in the Github readme.md file for that project and all others.

One snag I hit, was properly understanding the invocation name. It is how a users interacts with your skill. For example, "Alexa, ask Political Geek for a government fact". I had initially included the word "start" in my documentation and sample phrases. The 'start' word is a reserved launched word and can not be used. Once I fixed that issue, my skill was approved quickly.

Most of my testing time was spent making sure Alexa properly pronounced words by using the simulator in the test area of the [developer console](https://developer.amazon.com/home.html).

Finally, I hit a snag one night while testing. I was getting the following error... `The remote endpoint could not be called, or the response it returned was invalid'. This was a pretty generic error message it got me looking at how to debug this stuff. I stumbled upon using Lambda's test function following this [guide](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/developing-an-alexa-skill-as-a-lambda-function#Testing a Lambda Function in the Console) and reviewing the [CloudWatch logs](http://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions-logs.html). For my error, the best I could I figure out was that there must have been a service interruption as all was working in the morning. Just goes to show you, when following a tutorial, and it goes south, you can learn so much more researching your problem.

My last skill is going to be a guide that will provide durations regarding how long you can safely keep foods under refrigeration. I will talk about that in my next post once it is approved.


-Dan
