This week we dived into rails and was able to do a lot of cool stuff but I'm still a little iffy on some things. 

I decided to created this step by step cheatsheet to help me learn and lay it all out on one place for references. I'm going to follow the rails guid link: 
https://guides.rubyonrails.org/getting_started.html

Assumption: Already have rails and ruby installed on your machine

## 1. Creating A New Application

The first step is to create a rails application with the following command in your terminal.
Name will be the actual name of your application

```
$ rails new name
```
This will create a directory and install the gem dependencies.

Navigate into your new directory with the followign command

```
cd name
```

At this point you should create a GitHub repository and push changes to your GitHub.

## 2. Routes & Controllers
Route (Rules written in a Ruby DSL): maps a request to a controller action
Controller (Ruby Classes): performs the necessary work to handle the request, and prepares any data for the view
View (Templates written in HTML and Ruby): displays data in a desired format

To understand the connections let's start by saying hello.
In your directory go to config/routes.rb inside you'll find
```
Rails.application.routes.draw do
  # Define your application routes per the DSL in https://guides.rubyonrails.org/routing.html

  # Defines the root path route ("/")
  # root "articles#index"
end
```

Inside the block add a route. Your code should look like this (You can delete the comments if you want). The route delcares that GET /articles requests are mapped to the index action of ArticlesController. 
```
Rails.application.routes.draw do
  get "/articles", to: "articles#index"
end
```

As of now there is no ArticlesController. To create it we'll run the generator in your terminal.
```
$ rails generate controller Articles
```

Rails will create several files for you. Go into your app/controllers/articles_controllers.rb
```
class ArticlesController < ApplicationController
end
```

You will need to create the index action (or method)
```
class ArticlesController < ApplicationController
  def index
  end
end
```

Now go to app/views/articles/index.html.erb and replace its content with:
```
<h1>Hello, Rails</h1>
```

