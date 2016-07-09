---
layout: post
title: Alexa Skill Number 3
---
I submitted my final skill called [Fridge Storage Times Helper](https://github.com/dale3h/alexa-skills-list/tree/master/skills/B01HQW7016) last week.  This skill provides recommended fridge storage times for various meats, fruits, and vegetables. The information was sourced from [Foodsafety.gov](https://www.foodsafety.gov/keep/foodkeeperapp/index.html) and covers most common meats, fruits, and vegetables. To invoke the skill, you would just ask Alexa: "Alexa ask fridge storage times" or "Alexa ask fridge storage times how long can I keep leftovers".

I pattered the skill after [Mine Craft Helper](https://github.com/amzn/alexa-skills-kit-js/tree/master/samples/minecraftHelper) with some minor adjustments to the slots, sample utterances, and added all the food storage time recommendations into the existing JSON hash.

Again, testing focused on making sure Alexa pronounced the words correctly and that the sample utterances were abundant. They need to match the natural way people speak, that is in all there various forms. This is critical so that the skill actually gets invoked on the first try. Nothing more frustrating than having to change the way you say something, just so Alexa will perform the action. Further improvement of this skill would be to use a NOSQL database for storing answers instead of using a hardcoded JSON hash. I think having Alexa tell users how long they can keep food in the fridge with a power loss or breakdown would be a good feature to add.

Finally, in regards to my skill and safety, I added these comments below.

  These are just guidelines and common sense should be followed when handling all food items including following the use-by-date provider by the retailer or manufacturer.

  Disclaimer: Refrigeration guidelines were collected from FoodSafety.gov. In no event will I be liable for any food-born illness, death, or damage including without limitation, indirect or consequential loss or damage, or any loss or damage whatsoever in connection with, the use of this Amazon Alexa Skill.

-Dan
