---
layout: post
title:      "How to set up a Rails API for React "
date:       2018-12-19 19:25:04 -0500
permalink:  how_to_set_up_a_rails_api_for_react
---

**Step 1. Create a new rails App: **
```
$ rails new railsAPI
```


**Step  2. Set up the controllers for the API: **

```
Api/v1/articles_controller.rb 

class Api::V1::ArticlesController < Api::V1::BaseController
  def index
    respond_with Article.all
  end

  def create
    respond_with :api, :v1, Article.create(article_params)
  end

  def destroy
    respond_with Article.destroy(params[:id])
  end

  def update
    article = Article.find(params["id"])
    article.update_attributes(article_params)
    respond_with article, json: article
  end

  private

  def article_params
    params.require(:article).permit(:id, :title, :url, :description, :author)
  end
end
```

——

```
Api/v1/base_controller.rb 

class Api::V1::BaseController < ApplicationController
  respond_to :json
end

application_controller.rb 

class ApplicationController < ActionController::Base
  protect_from_forgery with: :null_session
end
```


**Step 3. Create models:** 

```
 Models/article.rb
 
class Article < ActiveRecord::Base
 
end
```


**Step 4. Create serializers: 
**

```
class ArticleSerializer < ActiveModel::Serializer
  attributes :title, :url, :description, :author

end
```

**Step 5:  Create routes at config/routes.rb: 
**

```
Rails.application.routes.draw do
    root to: 'site#index'

    namespace :api do
      namespace :v1 do
        resources :articles, only: [:index, :show, :create, :destroy, :update]
      end
    end
  end
```



**Step 6. Add tables to database: 
**

```
$ rails g migration create_articles_table 
```

```
 \db/migrate/20181016003008_create_articles_table.rb

class CreateArticlesTable < ActiveRecord::Migration[5.2]
  def change
    create_table :articles do |t|
      t.string :title
      t.string :url
      t.string :description
      t.string :author
    end
  end
end
```

```
$  rake db:migrate
```



**Step 7: Add some seeds:***

```
Seeds.rb 

 Article.create(title: ‘My Article’, url: "MyArticle.com", description: “content”, author: “CR”)
```

```
$ rake db:seed
```
 

**Step 8: Create a new react app inside your rails app with the name client:**

```
$ npx create-react-app client
```


**Step 9: Add a file named Procfile to your rails app with this code inside:**

```
web: cd client && npm start
api: bundle exec rails s -p 3001
```

This will start 2 servers at the same time.


**Step 10: In the lib/tasks folder, add a file start.rake with this code:**

```
task :start do
  exec 'foreman start -p 3000'
end
```

This will allow you to start the servers with ‘rake start’

**Step 11:**
1. Add foreman, responders, react-rails and Thor gems to your gemfile  and run bundle install.
2. Update your rails package.json file:   

```
{
  "name": "railsAPI",
  "private": true,
  "dependencies": {
    "react": "^16.5.2",
    "react-dom": "^16.5.2"
  }
}
```

And your react app package.json: 
```

{
  "name": "client",
  "version": "0.1.0",
  "private": true,
  "proxy": "http://localhost:3001/",
  "dependencies": {
    "es6-promise": "^4.2.4",
    "isomorphic-fetch": "^2.2.1",
    "jquery": "^3.3.1",
    "popper.js": "^1.14.3",
    "react": "^16.4.1",
    "react-dom": "^16.4.1",
    "react-redux": "^5.0.7",
    "react-router-dom": "^4.3.1",
    "react-scripts": "^1.1.4",
    "redux": "^4.0.0",
    "redux-thunk": "^2.3.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  },
  "devDependencies": {
    "popper": "^1.0.1"
  }
}
```


**Step 11:**  You should now be able to run rake start in the terminal.  http://localhost:3000/ should first load in the browser but you can also view your rails app at http://localhost:3001 and reach your api at  http://localhost:3001/api/v1/articles.json

```
[{"id":1,"title”:”My Article”,”url”:”MyArticle.com","description”:”content”,”author”:”CR”}]
```


