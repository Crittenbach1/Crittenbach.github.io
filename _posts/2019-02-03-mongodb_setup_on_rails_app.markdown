---
layout: post
title:      "Mongodb Setup on Rails app"
date:       2019-02-03 02:31:11 -0500
permalink:  mongodb_setup_on_rails_app
---


**Step 1**

Install mongodb in terminal:

```
brew install mongodb
```

**Step 2**

Start the mongodb server with: 

```
mongod --config /usr/local/etc/mongod.conf
```

**Step 3**

Create a new rails app with a name 

```
 rails new [app name] --skip-active-record
```

**Step 4**

Add the Mongodb gem to your rails gemfile 

```
gem 'mongoid', '>= 3.0.2'
```

**Step 5**

```
bundle install
```

**Step 6**

Create a mongoid.yml file in your config folder

```
rails g mongoid:config
```

**Step 7**

Create contoller, model, view, route files

ex: 

```
rails g scaffold product name price:big_decimal
```





