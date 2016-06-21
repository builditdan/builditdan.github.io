---
layout: page
title: Wiki Pad
hide: true
feature-img: "/img/bannera.jpg"
---

### URL
[https://wikipad1.herokuapp.com/](https://wikipad1.herokuapp.com/)

### Github URL
[https://github.com/builditdan/wikipad](https://github.com/builditdan/wikipad)

### Getting Started

**Clone the Github application**

```
$ git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY
```

**Create the database**

```
rake db:create
```

**Migrating and seeding the database**

```
rake db:migrate
rake db:seed
```

**Starting the local server**

```
rails s

```

### Background and General Information
I built this application during my Ruby on Rails training with [bloc.io](https://bloc.io).

It is a website that will allow users to be authenticated and create public and private Wikis. You can add collaborators so others can update your wiki and use markdown for creating the content.

### Design Information
I used [bootstrap](http://getbootstrap.com/) to aide in design and layout. It is a responsive site and should work on mobile devices as well as computer screens.

The big new concept with this project was adding the ability for a user to upgrade to a premium account and charge them. I used the [Stripe](https://stripe.com/) gem which made handling credit card transactions much easier. See the screenshot below.

[<img src="/img/payforit.png">](http://wikipad1.herokuapp.com/)<br>

### Highlights on Gem's used
* [`rspec`](https://github.com/rspec/rspec-rails) for testing
* [`postgres`](http://www.postgresql.org/) for my production database, mysql for development
* [`devise`](https://github.com/plataformatec/devise) to aide in account management
* [`pundit`](https://github.com/elabs/pundit) to aide in security policies
* [`stripe`](https://github.com/stripe/stripe-ruby) for handling credit card transactions
* [`redcarpet`](https://github.com/vmg/redcarpet) for handling markdown
* [`money-rails`](https://github.com/RubyMoney/money-rails) helper when dealing with currency
* [`byebug`](https://github.com/deivid-rodriguez/byebug) debugging helper
* [`better_errors`](https://github.com/charliesome/better_errors) better error messages
* [`binding_of_caller`](https://github.com/banister/binding_of_caller) better debug messages
* [`faker`](https://github.com/stympy/faker) handy gem for generating fake data

### Additional comments
This site does not actually process real credit card transactions. It uses a [test credit card](https://stripe.com/docs/testing) number provided by Stripe. You can just user credit card number '4242424242424242' and CVC code '9999'. If it does not work, I just need to set my test publisher keys for stripe as the Dyno has been bounced.  

### Disclaimer
I provide this Web site as an example of my work. It is **not a production site** and subject to **removal** along with any content that you may have created. If you are interested in using this site or the code - feel free to download or contact me with your questions.
