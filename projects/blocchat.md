---
layout: page
title: Bloc Chat
hide: true
---
### URL
[https://blocchat1.herokuapp.com/](https://apomodoro.herokuapp.com/)

### Github URL
[https://github.com/builditdan/bloc-chat](https://github.com/builditdan/bloc-chat)

### Getting Started

**Clone the Github application**<br>
```
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
```

**Install grunt**<br>
[http://gruntjs.com/getting-started](http://gruntjs.com/getting-started)

Run the application using the Gruntfile's `default` task:

```
$ grunt
```

The default task runs a simple server on port 3000. To view it in a any browser, go to [http://localhost:3000](http://localhost:3000).

>Note that unless the application is run [via Live Preview in Brackets](#use-in-brackets-live-preview), the browser will need to be refreshed to view the most recent changes.

### Background and General Information
I built this Angular JavaScript site during my front-end training with [bloc.io](https://bloc.io).

It is a single page website where you can create conversations and chat with other users. No login is required but you are requested to enter your username each time you visit the website.

### Design Information
This project uses AngularJS and Google's [Firebase](https://firebase.google.com/) for it's database.

My biggest challenge in this project was getting a better understanding how to use a [NoSQL](https://en.wikipedia.org/wiki/NoSQL) database system like Firebase. This project required me to store not only my conversations but also the chats associated with them. I needed a relationship (foreign key) between those two tables. NoSQL is not a relational database so the whole concept of tables, fields, relationships, schemas, and indexes is different. Once my mind embraced the core concept that the document store (the database in a sense) is really just a series of [JSON](https://en.wikipedia.org/wiki/JSON) objects with children and nodes it started to make since. Not all NoSQL databases you JSON - others include [XML](https://en.wikipedia.org/wiki/XML), [YAML](https://en.wikipedia.org/wiki/YAML), etc.

### Highlights on scripts included
* [Angular](http://angular-ui.github.io/) for development
* [Firebase](https://firebase.google.com/docs/) for storing tasks
* [UI Router](https://github.com/angular-ui/ui-router) for angular routing
* [Bootbox](https://github.com/makeusabrew/bootbox) for showing nice popup boxes
* [Datejs](https://github.com/datejs/Datejs) date library
* [Angular Cookie helper](https://docs.angularjs.org/api/ngCookies) cookie helper for storing username


### Additional comments

I worked on making the site responsive but could most likely benefit from some more work in that area.

You get prompted each time you hit the page to enter your username even though it is stored in your local hash. I need to add a button for that in the future and improve the overall username setting experience.

### Disclaimer
I provide this Web site as an example of my work. It is **not a production site** and subject to **removal** along with any content that you may have created. If you are interested in using this site or the code - feel free to download or contact me with your questions.
