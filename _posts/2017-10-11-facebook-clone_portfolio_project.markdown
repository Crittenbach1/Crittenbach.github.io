---
layout: post
title:      "How to set up a Sinatra app"
date:       2017-10-11 10:13:06 -0400
permalink:  facebook-clone_portfolio_project
---


Step 1. Create a folder for your Sinatra app.  I will be calling mine "teach".

     You should create the following files and folders:
```
> teach
				v app 
					 > controllers 
					 > models
					 > views
				v config
					environment.rb
				v db
		config.ru
		Gemfile
		Rakefile
```

Step 2. Add this to your config/environment.rb file:

```
ENV['SINATRA_ENV'] ||= "development"

require 'bundler/setup'
Bundler.require(:default, ENV['SINATRA_ENV'])

ActiveRecord::Base.establish_connection(
  :adapter => "sqlite3",
  :database => "db/#{ENV['SINATRA_ENV']}.sqlite"
)

require_all 'app'
```

Step 3. Add this to your config.ru file:
 
```
require './config/environment'

if ActiveRecord::Migrator.needs_migration?
  raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end

use Rack::MethodOverride
run ApplicationController

```

Step 4. Add these to your gemfile: 

```
source 'https://rubygems.org'

gem 'sinatra'
gem 'activerecord', :require => 'active_record'
gem 'sinatra-activerecord', :require => 'sinatra/activerecord'
gem 'rake'
gem 'require_all'
gem 'sqlite3'
gem 'thin'
gem 'shotgun'
gem 'pry'
gem 'bcrypt'

group :test do
  gem 'rspec'
  gem 'capybara'
  gem 'rack-test'
  gem 'database_cleaner', git: 'https://github.com/bmabey/database_cleaner.git'
end

```

Step 5. Run bundle install to install your gemfiles.  A file called Gemfile.lock should appear.

Step 6. Lastly, add this to your rake file:

```
ENV["SINATRA_ENV"] ||= "development"

require_relative './config/environment'
require 'sinatra/activerecord/rake'

```
