---
layout: page
title: BlocItOff
hide: true
feature-img: "/img/bannera.jpg"

---

### URL
[http://blocitoffa.herokuapp.com/welcome/index](http://blocitoffa.herokuapp.com/welcome/index)

### Github URL
[https://github.com/builditdan/blocitoff](https://github.com/builditdan/blocitoff)

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
This sample application uses Ruby on Rails.

It is a website where you can enter tasks and they will automatically self-destruct in 7 days. By automatically deleting the tasks it provides you that motivation to get your tasks done before they expire.

<iframe src="//giphy.com/embed/8p8E1sylIARDW" width="480" height="204" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="http://giphy.com/gifs/excited-8p8E1sylIARDW"></a></p>

### Design Information
I used [bootstrap](http://getbootstrap.com/) to aide in design and layout. I leveraged gems [devise](https://github.com/plataformatec/devise) and [pundit](https://github.com/elabs/pundit) for account management. Gained more hands-on experience using [partials](http://guides.rubyonrails.org/layouts_and_rendering.html#using-partials) to keep my code dry.

To create a more dynamic feel to the task list I used [Ajax](http://guides.rubyonrails.org/working_with_javascript_in_rails.html) to add and mark tasks complete without having to do a page refresh. To keep those tasks expiring - I created a custom [Rake](http://guides.rubyonrails.org/command_line.html#rake) job that would purge tasks after seven days.

### Highlights on Gem's used
* [`rspec`](https://github.com/rspec/rspec-rails) for testing
* [`postgres`](http://www.postgresql.org/) for my production database, mysql for development
* [`devise`](https://github.com/plataformatec/devise) to aide in account management
* [`pundit`](https://github.com/elabs/pundit) to aide in security policies
* [`redcarpet`](https://github.com/vmg/redcarpet) for handling markdown
* [`byebug`](https://github.com/deivid-rodriguez/byebug) debugging helper
* [`better_errors`](https://github.com/charliesome/better_errors) better error messages
* [`binding_of_caller`](https://github.com/banister/binding_of_caller) better debug messages
* [`faker`](https://github.com/stympy/faker) handy gem for generating fake data

### Additional comments
It is NOT a responsive site so additional work would be needed in that area.

The Rake task that purges expired tasks only runs manually. A future enhancement would be to add it to scheduler like [Cron](https://en.wikipedia.org/wiki/Cron).

### Disclaimer
I provide this Web site as an example of my work. It is **not a production site** and subject to **removal** along with any content that you may have created. If you are interested in using this site or the code - feel free to download or contact me with your questions.
