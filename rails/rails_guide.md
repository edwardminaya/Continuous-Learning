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

Next, create your database. Without this the server will not run. 
```
rails db:create
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

In your terminal start the server in your directory
```
$ rails server
```
Now you can go into a web browser and see your hello, rails message with the following address: http://localhost:3000/articles

## 3. Models
Model (Ruby Class): used to represent data. Models can interact with the application's database through a feature of rails called active record. Models can create, read, update and destroy records (CRUD). 

In your terminal run the following command. This will create several files
```
$ rails generate model Article title:string body:text
```
IMPORTANT: Model names are singular, because an instantiated model represents a single data record. 

title and string are attributes and you are setting the class type (string, integer, boolean, text, etc.)

Migrations are used to alter the structure of an application's database. Go into your db/migrate folder and you'll find the new migration file. The code inside should look like this
```
class CreateArticles < ActiveRecord::Migration[7.0]
  def change
    create_table :articles do |t|
      t.string :title
      t.text :body

      t.timestamps
    end
  end
end
```

create_table: specifies how the articles table should be constructed. By default this method adds an id column as an auto-incrementing primary key. Inside the block two columns are defined: title and body, which were created with the terminal command to generate the model and attributes. The last line of the block is called t.timestamps. By default two additional columns named created_at and updated_at were created. Rails manages these for us. 

The table structure was defined but not created. To create the table run the following command line in your terminal
```
$ rails db:migrate
```

## 4. Using a Model to Interact with the Database (Terminal)
Similar to irb, rails uses the console. To launch the console run the following code in your terminal
```
$ rails console
```
Here we can initiate a new Article object. Run the following code in your terminal
```
article = Article.new(title: "Hello Rails", body: "I am on rails!")
```
This is essentially assigning the variable, article, to a new instance of the class Article that requires two attributes we initiated when we created the model (title and body). 

Also note that this created an instance but did not save it. To save the object in the database run the following command in your terminal
```
article.save
```
The object, article, has now been saved and inserted to our table. Like we mentioned before it will get an id and since this is the first object inserted it will have an id of 1. To see the table you can run either of the following commands in your terminal
```
article
```
```
Article.all
```
## 5. Views
In your directory app/controller/articles_controllers.rb update the action index with the following code
```
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
end
```
Then in your app/views/articles/index.html.erb file replace the content with the following code.
```
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>
```
This files is a mixture of HTML and ERB. ERB is a templating system that evaluates Ruby code embedded in a document. 

<% %> This tag means 'evaluate the enclosed Ruby code.

<%= %> This tag means 'evaluate the enclosed Ruby code and out put the value it returns

## Conclusion
This does not include the jbuillder and the tutorial continues through each CRUD (Create, Read, Update, Destroy) action by updating the routs, controllers and views. This was a great way to learn about how to start a new rails application. 
