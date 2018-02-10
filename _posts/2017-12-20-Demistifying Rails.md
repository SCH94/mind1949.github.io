# Demystifying Rails

by Launch School

This book doesn't teach how to use Rails to build prototypes. Instead, this book dives one layer below the surface to expose how Rails is pieced together. We'll take common Rails conventions apart and study each component from the perspective of web development fundamentals. Significant programming, web development, and even basic Rails knowledge will be helpful prior to starting this book. This book also supplements the material in our course, [Rapid Prototyping with Ruby on Rails](https://launchschool.com/courses/b5a135ab/home)

# 1. GETTING STARTED

# 1.1 Introduction

As a web application development framework, Ruby on Rails is tremendously helpful for building web applications, but only if you understand the problems it solves and how it solves them.

Sadly, most guides dive right in with Rails, showing *what* it does, rather than *why*or *how* it does it. This is helpful if you're only ever going to do *exactly* what you see in the book, but falls pitifully short if you want to apply these tools to whatever problem you come across.

So our reason for writing this book is different than that of other guides. This is not a manual to show every last thing you can do with Rails, but instead a journey behind the scenes to see what life in a web application is like without Rails, a journey to understand why web application frameworks exist. You'll see the pains that arise when building a web application without a framework, so that when the conventions *are* introduced, they make sense, because you can now see them in context.

In short, we wrote this book because we believe that before you do it with Rails, you need to understand how to do it without.

## [Prerequisites](https://launchschool.com/books/demystifying_rails/read/introduction#prerequisites)

If you've been interested in Rails or even played with it a bit, but don't quite feel like you "get it", then this book is for you. This book also works well as review material, so even if you are familiar with Rails, there is still some benefit to gain from reading this book; it does expect that you have a basic understanding of the following:

- [The Command Line](https://launchschool.com/books/command_line)
- [Ruby](https://launchschool.com/books/ruby)
- [OO Ruby](https://launchschool.com/books/oo_ruby)
- [HTTP](https://launchschool.com/books/http)
- [SQL](https://launchschool.com/books/sql)
- Basic HTML

Each of the concepts listed above are crucial for understanding the content of this book. Please make sure that you thoroughly understand those concepts before moving onto the main content of this book. If you feel that you do know the material above, but that you're somewhat rusty on that material, then it may be a good idea to review things first.

## [How To Read This Guide](https://launchschool.com/books/demystifying_rails/read/introduction#howtoreadthisguide)

The book is divided into two parts:

1. No Magic Rails
2. Rails Core Conventions

In "No Magic Rails" we aim to use very little in the way of Rails conveniences. We'll start with some web application basics, then move to writing a simple blogging application.

The goal in this first section is to painstakingly build a web application without using any conventions or conveniences provided by Rails. This process exposes fundamental web development concepts, revealing many of the pains that Rails seeks to alleviate.

And as we write our blog app, we'll see all of the pieces. What's more, we'll start to notice some duplication and a few different patterns, and refactor accordingly as we go.

Then in the second half, "Rails Core Conventions", we'll go back through our complete blog application, armed with the knowledge of those patterns. This time through, we'll better understand the problems they relate to, and rewrite our app using everything Rails has to offer.

But Rails is more than just the tools it provides; its conventions give us a way of thinking about web applications and an organizational structure for implementing them. The real power here comes from understanding the reasons for and the mechanisms of the framework, so that you're able not only to use it, but also adapt it to fit your needs.

By the time you're done reading this book, you'll understand the most important conventions in Rails, but more importantly, you'll understand why they exist. If this sounds good to you, then it's time to head to the next section, where we'll do a quick review of HTTP before we get underway!

# 1.2 HTTP and Web Development Review

## [HTTP and Web Apps](https://launchschool.com/books/demystifying_rails/read/http_and_web_development_review#httpandwebapps)

In a lot of ways, building a web application is all about HTTP. This fact ends up getting obscured quickly as we dive into writing our application with a framework such as Ruby on Rails, but as you read, please try to keep in mind that the fundamental paradigm of a web application is to react to an HTTP request and to create an appropriate HTTP response. Much of what we'll see in Rails exists solely to make this easier.

Before we dive into building our application and learning about Rails, let's take a moment to review what we know about HTTP already, and begin to think about it in the context of developing a web application.

We expect you have read our [Introduction to HTTP](http://www.launchschool.com/books/http) book at this point. If you haven't, you should take the time to go through it. It's a short read and provides the necessary background for this book.

### The Client-Server Model

HTTP makes use of the client-server model. In the context of Rails web applications, the client is a web browser and the Rails app runs on the server.

Any interaction begins with the client (web browser) sending an HTTP request to the server (Rails app). The Rails app will then:

1. figure out where to direct the request to be processed
2. process the request with pre-defined logic
3. construct a response

When this is finished, the app sends an HTTP response back to the browser. The browser then displays the response to the user.

### Every Client-Server Interaction Begins with an HTTP Request

An HTTP request has three parts:

1. request line
2. request headers
3. request message body

For this book, we'll only be concerned with the request line, and with two pieces of it in particular:

1. the **request verb** (a.k.a. **request method**)
2. the **request path**

`GET` and `POST` are common HTTP verbs, and `/hello_world` and `/create_post` are examples of paths.

The path is the part of the URL beginning with `/` that occurs *after* the domain. So for the URL `http://www.launchschool.com/books`, `/books` is the path.

Requests like the following will arrive in our web app:

```
GET /hello_world
POST /create_post

```

And based on the verb and path combination, we'll decide what what to do with them.

### Every Client-Server Interaction Ends with a HTTP Response

HTTP Responses have three parts:

1. status code
2. headers
3. body

The status code tells the clients the general result of how the server processed the result. Some possible values are `200 (OK)`, `404 (Resource Not Found)`and `500 (Server Side Error)`.

The body section of the response can be empty, but most of the time, there is a HTML document carried in the body section as "payload". This will be the primary HTTP response pattern we see in this book.

### The Web Application in the Middle

Between the Request and Response is the actual web application that interprets the incoming requests, pulls the necessary data from the database, follows pre-defined business rules, and generates the responses that carry the HTML document to be displayed in the user's browser. Although it's possible to implement web applications from scratch without any frameworks, most modern web apps are built with frameworks like Ruby on Rails to make development easier.

We will learn the In's and Out's of how to build web applications with Rails in this book.

Let's get to it.

# 1.3 Outlining Our First App

## [Set Up Starter App](https://launchschool.com/books/demystifying_rails/read/outlining_our_first_app#setupstarterapp)

For the first two sections of this book, we'll ask you to build up a blog app to learn Ruby on Rails. To get this started, follow the commands below to clone a starter app:

```
# make sure to use ruby version 2.2

$ git clone https://github.com/launchschool/demystifying_rails_app_template
$ cd demystifying_rails_app_template
$ bundle exec bundle install
$ bundle exec rails server

```

Once `$ bundle exec rails server` is running, just point your browser to[`http://localhost:3000/`](http://localhost:3000/) to use the app.

## [Outlining Our First App](https://launchschool.com/books/demystifying_rails/read/outlining_our_first_app#outliningourfirstapp)

So now that we have a fresh Rails app up and running, let's make it respond to an HTTP request.

Specifically, let's say that we want a request from our browser to `/hello_world`to result in the text `Hello, world!` being displayed in the browser.

In Rails, this is essentially a two step process:

1. define where the request should go
2. define the code to handle a request of this kind

The first of these is accomplished by declaring a **route**.

The second, by defining a method on a **controller**. This type of method on a controller containing logic for handling a request is called an **action**.

In the next several chapters, we'll go through those steps to build up our first Rails app.

# 2. NO MAGIC RAILS

# 2.1 Sending Requests And Responses

## [Defining A Route](https://launchschool.com/books/demystifying_rails/read/sending_requests_and_responses#definingaroute)

The "entrance" of a Rails app is a "route", which tells the Rails app where to find the code to handle the incoming requests. To prove our need for a route, let's try to hit our path first. Visit [`http://localhost:3000/hello_world`](http://localhost:3000/hello_world) and see what happens.

```
Routing Error
No route matches [GET] "/hello_world"

```

We haven't defined any route yet, hence the error. We can fix this by defining a route that points these kinds of requests to our new action. To do this, we need three bits of information:

The Rails route file contains a list of routes for the app. Each route is a combination of a HTTP verb (GET, POST etc) and a URL pattern, mapping to a combination of a controller and an action.

The error told us we don't have a route for the combination of a GET request with URL pattern `/hello_world`.

Let's define a route then, in the `routes.rb` file in the `config` directory.

`config/routes.rb`

```
Rails.application.routes.draw do
  get '/hello_world' => 'application#hello_world'
end

```

Inside the block in our `routes.rb`, we can use methods named after each of the HTTP verbs, e.g. `get`, `post`. We then define the URL pattern, then the combination of the controller and the action where the handling code for this type of requests lives.

In our case, we are defining that the code to process this request lives in the `ApplicationController`'s `hello_world` action. We haven't defined them yet, and we'll do that next.

Now, if you refresh the page `http://localhost:3000/hello_world`, you will get the following error:

```
Unknown action
The action 'hello_world' could not be found for ApplicationController

```

We'll tackle this issue in the next section by defining an action for this route in our `ApplicationController`.

### Ruby Tips

This line that we have in the route file may not look familiar:

```
get '/hello_world' => 'application#hello_world'

```

But it is essentially just a method call. It calls the `get` method passing in a hash as a parameter.

```
get({'/hello_world' => 'application#hello_world'})

```

If a hash is the last argument in a method call, Ruby allows you to drop the braces to make the line read better.

## [Defining An Action](https://launchschool.com/books/demystifying_rails/read/sending_requests_and_responses#defininganaction)

Now it's time to define the `hello_world` action in the `ApplicationController`, as our first route specified:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base
  def hello_world
    render plain: 'Hello, World!'
  end
end

```

The purpose of a controller action is to respond to an HTTP request and build an appropriate HTTP response. For this action, we're completely unconcerned with the details of the request, and simply build our `Hello, World!` message no matter what. Here we see that accomplished with a call to `render`, which is used to set the HTTP response. In the call to `render` above, we've passed in `plain: 'Hello, World!'`, so the generated response will have a content type of `text/plain` and a body of `Hello, World!`. Here is what the response will look like:

```
Cache-Control:max-age=0, private, must-revalidate
Connection:Keep-Alive
Date:Tue, 23 Feb 2016 01:21:23 GMT
Etag:W/"65a8e27d8879283831b664bd8b7f0ad4"
Server:WEBrick/1.3.1 (Ruby/2.3.0/2015-12-25)
X-Content-Type-Options:nosniff
X-Frame-Options:SAMEORIGIN
X-Request-Id:24c23eec-8a37-49d9-bcaf-4f5b3f18aaaa
X-Runtime:0.021203
X-Xss-Protection:1; mode=block

Hello, World!

```

We can even look at our response from within Rails, let's drop a debugger and inspect the response.

```
render plain: 'Hello, World!'
binding.pry

### in Pry's console ###
response.body         # => "Hello, World!"
response.content_type # => "text/plain"
response.status       # => 200

```

We'll see varied uses of `render` in a bit, but for now, it's enough to recognize that `render`'s job is to accomplish one of the core responsibilities of a controller action: building the HTTP response.

Additionally, notice that our `ApplicationController` class above inherits from `ActionController::Base`. The `render` method (and much more) is made available to us thanks to this inheritance.

### Ruby Tips

It's also worth noting that the `plain: 'Hello, World!'` above is simply a hash argument being passed into `render`:

```
render({:plain => 'Hello, World!'})

```

or,

```
render({plain: 'Hello, World!'})

```

Passing hashes this way (especially hashes with symbol keys) is incredibly common in Rails, but it's important to notice that there's no magic here, just standard Ruby syntax.

# 2.2 Rendering HTML with Views

## [Rendering HTML](https://launchschool.com/books/demystifying_rails/read/rendering_html_with_views#renderinghtml)

With our route properly handling requests to the action `/hello_world`, let's change our action to render some HTML instead:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base
  def hello_world
    render inline: '<em>Hello, World!</em>'
  end
end

```

Here we use `inline:` instead of `plain:` to pass the response body string to `render`, which sets the content type of the response to HTML. Here is what our response will look like:

```
HTTP/1.1 200 OK
Cache-Control: max-age=0, private, must-revalidate
Connection: Keep-Alive
Content-Length: 22
Content-Type: text/html; charset=utf-8
Date: Tue, 23 Feb 2016 02:44:36 GMT
Etag: W/"1e401bc81108cb3e3dba191111bf9059"
Server: WEBrick/1.3.1 (Ruby/2.3.0/2015-12-25)
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
X-Request-Id: a2eac900-60da-460d-9757-94d8c41c4624
X-Runtime: 0.252767
X-Xss-Protection: 1; mode=block

<em>Hello, World!</em>

```

Most of the above is very similar to our last HTTP response for the hello world action. Notice, that there are a few differences, and one of those differences is that the response body now has `em` tags wrapped around it.

Let's inspect our `response` object within Rails as well:

```
# assuming we're inside the hello_world action above...

render inline: '<em>Hello, World!</em>'
binding.pry
### inside Pry ###
response.body         # => "<em>Hello, World!</em>"
response.content_type # => "text/html"
response.status       # => 200

```

Here we see the content type set appropriately to `text/html`, thanks to using `inline:` instead of `plain:`. The status code here also defaults to `200` (`OK`), which is fine, but if we wanted to change it, we could do so in a `render` call simply by passing e.g. `status: 404` along as well.

Now if you refresh the page, you'll see our `Hello, World!` message displayed in italics in your browser, thanks to the `text/html` content type and the `<em>`tags in the HTML response body string.

## [Content Using Views](https://launchschool.com/books/demystifying_rails/read/rendering_html_with_views#contentusingviews)

We've got requests being processed by an action now, but there's something amiss: there's content in our action.

The problem here is that a controller's job is not to hold content, it's to… well, *control* things. A cleanly written controller action won't *do* much of anything itself, other than orchestrate the calling of other parts of the application and, when needed, put those results together.

A controller action is merely the director of the request handling, it should delegate other responsibilities to other parts of the application. But already, ours is doing something it shouldn't have to: it's holding our content, the HTML message.

To fix this, let's move that HTML out of our action.

### Creating a Simple View

HTML content belongs in a **View**, so let's create one to hold it:

```
<!-- app/views/application/hello_world.html -->

<html>
  <body>
    <p>Hello, World!</p>
  </body>
</html>

```

This is the same HTML as before, but now stored in its own view file. And notice where we placed it, because this is important:

```
app/views/application/hello_world.html

```

All views live in the `app/views` directory. From there, they are placed in a directory that corresponds to the controller and action that uses them. Here, this leaves us with an `app/views/application/hello_world.html` file.

With our view defined, let's make use of it in our controller:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base
  def hello_world
    render 'application/hello_world'
  end
end

```

NOTE: Make sure to restart your Rails server with `bundle exec rails server`before reloading the page

Now, we've used `render` a couple times already, but here we're doing something different because we're simply passing it a string. Furthermore, you'll note that this string matches the path of the view that we just created. As a result, our `hello_world` action will now render our HTML response body using our freshly defined `application/hello_world` view.

Effectively, using `render` this way is the equivalent of doing:

```
render inline: File.read('app/views/application/hello_world.html')

```

Whether we're pointing it to a view or setting the response body in the action itself, keep in mind that it's always the job of `render` to set the HTTP response body. Though, as we pointed out above, it's typically bad practice to leave content sitting in your controller, so quite commonly you'll see `render` calls rendering views, like the one above.

# 2.3 Making Our App Dynamic

## [Dynamic Server Responses](https://launchschool.com/books/demystifying_rails/read/making_our_app_dynamic#dynamicserverresponses)

Now we've got a route sending requests to our action and we have our action rendering a view, but so far all of our content has been **static**. Our Rails application now is essentially a file server that fetches a HTML document, wraps it in an HTTP response and returns it to the client.

This **was** the main paradigm of the Web in its early days, where web servers respond to requests and send back static documents. The modern web, however, gave rise to web "applications" that can assemble responses on the fly to respond to requests.

The dynamic nature of web apps come mainly from the following two sources:

- The client embeds a piece of data inside the URL for the server to respond to. For example, when we type in the browser "<https://www.google.com/search?q=robots>" we are asking Google to dynamically assemble a web page containing only search results for "robots".
- The server responds with data based on some internal state of the data in the server's database. For example, when you visit a blog, the server would retrieve the blog posts stored in the database, and dynamically assemble a web page based on this data.

We'll look at those two scenarios more closely in the upcoming topics.

## [Dynamic Documents With Embedded Ruby](https://launchschool.com/books/demystifying_rails/read/making_our_app_dynamic#dynamicdocuments)

ERB stands for "embedded Ruby". It's a templating engine that allows us to embed Ruby code in a text document to have dynamic documents.

In an ERB template, the Ruby code has to be put inside `<%... %>` tags for it be evaluated. Moreover, we can use the `<%= ruby_expression %>` syntax to put the evaluated value of the ruby expression into the HTML document.

When we "render" a template into a HTML document, it means we are going to run the template through a "rendering engine" (in this case, the ERB rendering engine), then execute the Ruby code embedded and output the resultant document.

For example, this ERB template

```
<html>
  <body>
    <% name = "John" %>
    <p>Hello, <%= name %>!</p>
  </body>
</html>

```

will be rendered into

```
<html>
  <body>
    <p>Hello, John!</p>
  </body>
</html>

```

In this example, we assigned value `"John"` to the variable `name` inside of the ERB template, then used it to render the HTML document. This works, though, it's not really interesting, because the template would always render into the same result.

We can also simply leave the template as

```
<html>
  <body>
    <p>Hello, <%= name %>!</p>
  </body>
</html>

```

and pass in the value of the variable `name` from outside of the template. If the value of variable `name` is also `"John"`, this template will be rendered to the same result.

## [Responses With Query Parameters](https://launchschool.com/books/demystifying_rails/read/making_our_app_dynamic#responseswithqueryparameters)

Now that we know how to use ERB templates to render dynamic documents, we are going to pass a name in the request URL and have the server respond with a custom greeting, for example, "Hello, John!"

To be able to do this, we'll rename our HTML document to `hello_world.html.erb`. In Rails, this convention means that this is an ERB template that will eventually be rendered into a HTML document.

The ERB template should look familiar:

`app/views/application/hello_world.html.erb`

```
<html>
  <body>
    <p>Hello, <%= name %>!</p>
  </body>
</html>

```

We have a number of ways of passing values from the client to the server, and the most basic is to use **query parameters** in the URL, for example, `http://localhost:3000/hello_world?name=John`. The part following the `?`in the path, `name=John`, is the query string that can be interpreted by the server

Let's see how we can access these parameters in our action:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base
  def hello_world
    name = params['name']
    render 'application/hello_world', locals: { name: name }
  end
end

```

Rails parses the query parameters into a hash called `params`. In our action, we take the value of the `name` query parameter and pass it to the ERB rendering engine to render the `hello_world.html.erb` template.

If the previous line of code looks a bit confusing, it can also be written as this below:

```
render('application/hello_world', { locals: { name: name } })

```

You can see this is really a method call with two arguments, and the second argument is a hash with a key/value pair -- the key is `:locals` and the value is another hash. When the ERB engine sees the `:locals` key in the hash, it will use the value of that key to render the template.

Now if you type into your browser `http://localhost:3000/hello_world?name=John` you will see "Hello, John!".

This works great, but we've also introduced a bit of a problem: when we hit `/hello_world` all by itself now, we get this:

```
Hello, !

```

The reason being, `name` here is `nil`. There's no query parameter passed in with key `name`; this results in our strangely punctuated message above when the template is rendered.

We could go about fixing this in a number of ways, but let's just give `name` a default value inside our action:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base
  def hello_world
    name = params['name'] || "World"
    render 'application/hello_world', locals: { name: name }
  end
end

```

Now we see `Hello, World!` again if we don't pass along a `name` in the query string.

With the `params['name'] || 'World'` line above, the `||` (logical OR) works as a check to see if anything is in `params['name']` or not. If its value is truthy (any value other than `false` or `nil`), it simply returns the value. Otherwise ("OR"), it returns `'World'`.

## [Responses With URL Capture Pattern](https://launchschool.com/books/demystifying_rails/read/making_our_app_dynamic#responseswithurlcapturepattern)

Query parameters are useful to pass data to the server, however, it is not the only way. We can also specify URL matching patterns for routing and capture data.

For example, we are going to add a new line in our `routes.rb` file:

`config/routes.rb`

```
Rails.application.routes.draw do
  get '/hello_world/' => 'application#hello_world'
  get '/hello/:name'  => 'application#hello_world'
end

```

Now hitting `/hello/John` will also display `Hello, John!`

The pattern `/hello/:name` tells Rails to route any request with URL like `/hello/John` to the `hello_world` action in the `ApplicationController`. The value that matches the `name` placeholder, in this case, `John` is going to be accessible in the controller with `params['name']`.

And one last thing to notice about our routes above: we have *two* routes pointing at the same action. There's nothing wrong with this, Rails will simply use the first route that matchesdiidci the URL pattern.

# 2.4 Persisting Data In Our App

## [Database Backed Applications](https://launchschool.com/books/demystifying_rails/read/persisting_data_in_our_app#databasebackedapplications)

Passing data through the URL is one way to make the web application respond with dynamic content, but the most common paradigm for the dynamic web is "database backed applications", where the server queries the backend database and uses the result of that query to assemble a response to return to the client.

With this use case, the dynamic nature of the response is not coming from the data in the request, but from the "state" of the backend database.

This is a big topic, and we'll use several sections to cover it. We'll be working on creating a real web app, a blog, to walk through interactions with this paradigm.

## [Prepare The Database](https://launchschool.com/books/demystifying_rails/read/persisting_data_in_our_app#preparethedatabase)

To begin, let's give ourselves a database of blog posts to work with. We are going to use SQLite3, a lightweight database that Rails has built-in support for.

In dealing with posts in our database, we'll need to think about:

1. the structure of the database (a table and its columns)
2. the data itself (the rows representing individual posts)

As for the structure, we'll want a `posts` table to hold the details of each post. Each post will have the following attributes:

- `id` (integer)
- `title` (string)
- `body` (text)
- `author` (string)
- `created_at` (datetime)

Each of these will become a column for our `posts` table in our database.

To create this table, we'll be using the following SQL file:

`db/posts.sql`

```
CREATE TABLE "posts" (
  "id"         INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
  "title"      varchar,
  "body"       text,
  "author"     varchar,
  "created_at" datetime NOT NULL);

```

We'll then populate the resulting `posts` table with some dummy posts, using the following CSV (Comma-Separated Value) file:

`db/posts.csv`

```
1,Blog 1,Lorem ipsum dolor sit amet.,Brad,2014-12-07
2,Blog 2,Lorem ipsum dolor sit amet.,Chris,2014-12-08
3,Blog 3,Lorem ipsum dolor sit amet.,Kevin,2014-12-09

```

So, to create our database, execute our SQL against it and create a `posts` table inside it, we just run the following from the "Rails root directory", that is, the top-level directory in our Rails app that contains directories like `app` and `db`:

```
$ sqlite3 db/development.sqlite3 < db/posts.sql
```

For this project we'll be using SQLite3 as our DBMS (Database Management System). There are other much more powerful DBMS's out there, but we'll go with SQLite3 because it's the default development database for Rails and because it just works.

This command results in the file `db/development.sqlite3` being created, which contains our SQLite3 database. And, since we executed our `posts.sql` file against it, it will have a `posts` table.

Let's run the SQLite3 console to take a look:

```
$ sqlite3 db/development.sqlite3

sqlite> .tables
posts

sqlite> SELECT * FROM posts;
sqlite>

```

Our `posts` table is there, but, as we can see from our blank return from that `SELECT`, there aren't any post rows in the table yet.

We can fix this by importing our CSV file of posts. We first have to tell SQLite3 that we're importing a CSV file, then we can perform the import like this:

```
sqlite> .mode csv
sqlite> .import db/posts.csv posts

```

Now let's check to see what we have:

```
sqlite> SELECT * FROM posts;
1,"Blog 1","Lorem ipsum dolor sit amet.",Brad,2014-12-07
2,"Blog 2","Lorem ipsum dolor sit amet.",Chris,2014-12-08
3,"Blog 3","Lorem ipsum dolor sit amet.",Kevin,2014-12-09

sqlite> SELECT title FROM posts;
"Blog 1"
"Blog 2"
"Blog 3"

sqlite> SELECT created_at FROM posts WHERE id=1;
2014-12-07

```

You can use the command `.quit` to exit the sqlite REPL. There we go, we have some posts in our DB to play with now!

## [Interacting With The Database](https://launchschool.com/books/demystifying_rails/read/persisting_data_in_our_app#interactwiththedatabase)

Before talking about how to work with this database in Rails, let's see how to interact with it with pure Ruby.

We'll need a way of connecting to our SQLite3 database from Ruby, and fortunately for us, there's a Ruby library named `sqlite3` that lets us do just that.

```
$ irb

> require 'sqlite3'
=> true

# setup db connection
> connection = SQLite3::Database.new 'db/development.sqlite3'
=> #<SQLite3::Database:0x000000039ff288 ... >

```

Here we `require` the library to make it available to us, then we instantiate a `SQLite3::Database` object that will allow us to query our `db/development.sqlite3` database.

So now we're all set to run SQL against our database, using Ruby:

```
> post_arrays = connection.execute 'SELECT * FROM posts'
=> [
     [1, "Blog 1", "Lorem ipsum dolor sit amet.", "Brad", "2014-12-07"],
     [2, "Blog 2", "Lorem ipsum dolor sit amet.", "Chris", "2014-12-08"],
     [3, "Blog 3", "Lorem ipsum dolor sit amet.", "Kevin", "2014-12-09"]
   ]

```

We pass an SQL string to `connection.execute` to have it run against our database. The return from this `connection.execute` call is an array of arrays, with each representing a table row.

The arrays representing the post rows hold values in the following format:

```
[id, title, body, author, created_at]
```

Which makes sense, because that's the order that we declared the columns for the tables, but it's not particularly convenient. For example, if we want a post's title, we'd have to know that titles are at index `1`in these arrays, then use `post[1]` to grab the title string. Instead, it'd be nice to have these posts returned to us as hashes, so that if we want a post's title, we could simply use `post['title']` to get it.

Conveniently enough, we can tell our connection to return these rows to us as hashes:

```
> connection.results_as_hash = true
=> true

> connection.execute('SELECT * FROM posts').first
=> {
     "id"         => 1,
     "title"      => "Blog 1",
     "body"       => "Lorem ipsum dolor sit amet.",
     "author"     => "Brad",
     "created_at" => "2014-12-07",
     0 => 1,
     1 => "Blog 1",
     2 => "Lorem ipsum dolor sit amet.",
     3 => "Brad",
     4 => "2014-12-07"
   }

```

Now if we look at the `first` element in the array returned from the `SELECT` from before, we see that we get back a hash that'll let us get to a post title with `post['title']`.

Incidentally, we can still find the title with `post[1]`, because the title is also stored in the hash with the integer key `1`. These keys allow the hashes to *act* exactly like the arrays from before (in regard to value access using `[]` at least), even though they're not arrays anymore. Clever!

So now that we have some posts in a database and can get at them with Ruby, it's time to start building our web app.

# 2.5 List and Show Records

## [Listing Our Posts](https://launchschool.com/books/demystifying_rails/read/list_and_show_records#listposts)

For our blog app, we want to first display a list of all post titles. And now that we have a database with a few posts in it, we'll actually have something to display here!

So to get started, we'll recall that with our `hello_world` action we needed three things:

1. a route
2. an action
3. a view

We'll need each of those here as well, so let's kick things off by defining a route for `/list_posts`:

`config/routes.rb`

```
Rails.application.routes.draw do
  get '/list_posts' => 'application#list_posts'
end
```

the `application#list_posts` action points to:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base
  def list_posts
    connection = SQLite3::Database.new 'db/development.sqlite3'
    connection.results_as_hash = true

    posts = connection.execute("SELECT * FROM posts")

    render 'application/list_posts', locals: { posts: posts }
  end
end

```

Inside our `list_posts` action we see our DB initialization logic from before, followed by the `SELECT`query to grab all of our posts as hashes. After that, we're just passing those along as `locals` to the view.

A view which isn't defined yet, so let's do that next:

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <% posts.each do |post| %>
        <div class="post">

          <h2 class="title">
            <%= post['title'] %>
          </h2>

          <small class="meta">
            <span class="author">by <%= post['author'] %> -</span>
            <em class="created_at"><%= post['created_at'] %></em>
          </small>

        </div>
        <hr />
      <% end %>
    </div>

  </body>
</html>

```

There's quite a bit of markup here, but most of it should be familiar, with the exception of this:

```
<% posts.each do |post| %>
  <!-- ... -->
<% end %>

```

Here we see how we're able to iterate over an array inside of an ERB view. Above we loop over `posts` with `posts.each`, building a `<div>` for each `post`. (This `post` variable is available anywhere before the `<% end %>` for the block.)

An important thing to note here is the use of `<% %>` (without an `=`) as opposed to `<%= %>`. This allows us to execute Ruby *without* placing the return value into the page.

Besides that, you can see that we simply place the proper `post` values into different locations in the post `<div>` with lines like `<%= post['title'] %>`.

And with that, if you visit `/list_posts`, you'll see the titles of our three posts, along with their respective authors' names and dates of creation.

## [Show A Post To The User](https://launchschool.com/books/demystifying_rails/read/list_and_show_records#showapost)

Now that we have `/list_posts` working, let's implement something for `/show_post/:id`, which is where users will go to read a given post.

First, we'll need a route:

```
### config/routes.rb ###

Rails.application.routes.draw do
  get '/list_posts'    => 'application#list_posts'
  get '/show_post/:id' => 'application#show_post'
end

```

You can see here we set up a URL pattern to capture `id` as a parameter that we'll use in our controller action.

Then we'll need a `show_post` action:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def show_post
    connection = SQLite3::Database.new 'db/development.sqlite3'
    connection.results_as_hash = true

    post = connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", params['id']).first

    render 'application/show_post', locals: { post: post }
  end
end

```

In this `show_post` action, we first need to get a post from the database by a particular ID. We again run some SQL against the DB with `connection.execute`, but this time we call `.first` on the result. The reason here is that `connection.execute` is always going to return an array, even if it's only ever going to contain a single element, as is the case here with the `LIMIT 1`.

The way we use this with the database is interesting though, so let's take a look:

```
connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", params['id'])
```

For our purposes, this line has the same effect as:

```
connection.execute("SELECT * FROM posts WHERE posts.id = #{params['id']} LIMIT 1")

```

The `?` character in the original statement is a placeholder that will be replaced by the value of the second parameter, which is `params['id']`. This is a safer way to include user's input (in this case, from the URL) in a SQL statement. Rails makes sure that the statement is safe. The second statement is not safe because we included user's input directly in the statement. This technique is called protection against SQL Injection Attacks. We'll get to this topic later in the book.

But getting back to the last line of our action, we see that we simply pass our `post` along to our `show_post` view. Speaking of, let's define that now:

```
<!-- app/views/application/show_post.html.erb -->

<html>
  <body>

    <div class="post">
      <h2 class="title">
        <%= post['title'] %>
      </h2>

      <small class="meta">
        <span class="author">by <%= post['author'] %> -</span>
        <em class="created_at"><%= post['created_at'] %></em>
      </small>

      <p class="body"><%= post['body'] %></p>
    </div>

    <br />

  </body>
</html>

```

This view is basically the same as our `list_posts` view, except that it *doesn't* have a loop and *does* render the post body.

Hit `/show_post/1` and you'll see the post details from before, plus the post body.

### Links

Finally, let's make some links between these two pages:

```
<!-- app/views/application/show_post.html.erb -->

<html>
  <body>

    <!-- link to list of posts -->
    <a href="/list_posts">Back to Posts</a>

    <div class="post">
      <!-- ... -->
    </div>

    <br />

  </body>
</html>

```

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <% posts.each do |post| %>
        <div class="post">

          <h2 class="title">
            <!-- link to post -->
            <a href="/show_post/<%= post['id'] %>"><%= post['title'] %></a>
          </h2>

          <!-- ... -->

        </div>
        <hr />
      <% end %>
    </div>

  </body>
</html>

```

The link from the show view to the list view is a simple, static link:

```
<a href="/list_posts">Back to Posts</a>

```

While the one in the loop in the list view is more involved:

```
<a href="/show_post/<%= post['id'] %>"><%= post['title'] %></a>

```

Here we dynamically build the `href` using the post ID and then set the link text to the post title for each post.

## [Extract Shared Logic for DB Connection](https://launchschool.com/books/demystifying_rails/read/list_and_show_records#extractsharedlogic)

You might have noticed in `show_post` that we repeated the same two lines to connect to the database that we used in `list_posts`. let's move this logic to its own `connection` method in the controller and adjust both actions to make use of it:

```
class ApplicationController < ActionController::Base
  def list_posts
    posts = connection.execute("SELECT * FROM posts")

    render 'application/list_posts', locals: { posts: posts }
  end

  def show_post
    post = connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", params['id']).first

    render 'application/show_post', locals: { post: post }
  end

  private

  def connection
    db_connection = SQLite3::Database.new 'db/development.sqlite3'
    db_connection.results_as_hash = true
    db_connection
  end
end

```

This is great because if we need to change things about our database connection later, we can just make the change in a single place. Additionally, if any other actions need to make use of a database connection (they will), then they'll be able to make use of `connection` too.

# 2.6 Create a New Record Using a Form

## [Displaying A Form](https://launchschool.com/books/demystifying_rails/read/create_a_record_using_a_form#displayaform)

Now that we can see a list of posts and read a specific post, let's give the user a means to create a new post.

This will involve two parts:

1. provide the user with a form to collect the details of the new post
2. receive that submitted form data and add it as a new post to our collection of posts

Let's first look at how to display a form that we can use to collect user input. We'll start by defining a route, action, and view to serve the new post form to the client:

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  get '/new_post' => 'application#new_post'
end

```

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base
  # ...

  def new_post
    render 'application/new_post'
  end
end

```

```
<!-- app/views/application/new_post.html.erb -->

<html>
  <body>

    <form method="post" action="/create_post">

      <label>Title</label>
      <input name="title" type="text" />
      <br /> <br />

      <label>Body</label>
      <textarea name="body"></textarea>
      <br /> <br />

      <label>Author</label>
      <input name="author" type="text" />
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

  </body>
</html>

```

We add another route to send `GET` requests for the `/new_post` path to the `application#new_post`action.

Then we define that `new_post` action, which then renders the `new_post` view.

And finally we define a `new_post` view, which has a few new pieces. Namely:

1. a `<form>` with `method` and `action` attributes
2. `<input>`s with `name` attributes

The `<form>` attributes are hugely important to us because `method` determines the HTTP request method (a.k.a. verb) used for form submission and `action` determines the request path.

```
<form method="post" action="/create_post">

```

Does this pair sound familiar?

These two pieces of information are what we use to define a route. So here in the `<form>` we decide where to submit to, i.e. send a request. Then in our `routes.rb` we'll route requests of that type to a post action, which we'll define next.

So what kind of route will we need to respond to this request?

If you peek ahead, you'd see that in the next step we end up with:

```
post '/create_post' => 'application#create_post'

```

But coming back to our view, you'll also see a handful of `<input>`s inside the `<form>` that look something like this:

```
<input name="title" type="text" />

```

The `type` attribute is used to determine the kind of `<input>` (here, `text` results in a single-line text input), but `name` has a special purpose.

When a form like this is submitted with a `POST` request, it sends the form data to the server in the body of the HTTP request as **POST data**. Much like query string parameters, POST data is essentially just a collection of key-value pairs. The values here are obvious: string values for the post title, body, and so on.

But what determines the keys for the POST data?

The `name` attribute on an `<input>`.

This is a crucial detail to understand, because Rails will place these POST data pairs into `params` for us, and we'll need to know which keys to look for.

So in the next step, when we go looking for a post's title on a request resulting from this form submit, we'll find it in `params['title']`, because inside the `<form>` we have an `<input>` for it with `name="title"`.

Speaking of the next step, we're actually done with our form for now! Hit `/new_post` and you'll see our new post form.

## [Creating A Post](https://launchschool.com/books/demystifying_rails/read/create_a_record_using_a_form#creatingapost)

Now that we have a form for a new post, let's define the route and the action it submits to:

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  post '/create_post' => 'application#create_post'
end

```

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def create_post
    insert_query = <<-SQL
      INSERT INTO posts (title, body, author, created_at)
      VALUES (?, ?, ?, ?)
    SQL

    connection.execute insert_query,
      params['title'],
      params['body'],
      params['author'],
      Date.current.to_s

    redirect_to '/list_posts'
  end
end

```

We start implementing post creation by defining a route for our form to be submitted to. This route is quite similar to those before it, except that it uses the `post` method, as it's looking to match on `POST` requests.

Next we have our `create_post` action.

- The first thing we do in `create_post` is execute some SQL to `INSERT` the new post into the `posts`table. Since our SQL query string is multiline, we define it using a [heredoc](http://ruby-doc.org/core-2.0/doc/syntax/literals_rdoc.html#label-Here+Documents) (the `<<-SQL ... SQL` syntax above), and inside we see four `?`s for the values of our four post attributes.
- Then we see those four values passed in as arguments to `connection.execute`, following the query argument. We also see that we get these values out of `params`, as in `params['title']`. These values make their way into `params` based on the `name` attributes of the `<input>`s in our `new_post` `<form>`.
- And SQLite3 handles our `id`s automatically, so we don't need to worry about setting those.

Then, with our new post successfully added to the database, we simply respond to the client by redirecting them back to the list of posts. Since the new post is now a row in the `posts` table, `list_posts` will include its title when it renders.

Redirecting is accomplished with the Rails-provided `redirect_to` method. We have this available to us for the same reason we have `render`: `ApplicationController` inherits from `ActionController::Base`.

To see what goes on for a redirect, let's look again at our `response` object, but this time, after our `redirect_to` call:

```
# assuming we're inside the create_post action above...

redirect_to '/list_posts'
require 'pry'; binding.pry;

response.body
# => "<html><body>You are being <a href=\"http://localhost:3000/list_posts\">redirected</a>.</body></html>"

response.content_type # => nil

response.status #  => 302

response.headers
# => {
#      # ...
#      "Location"=>"http://localhost:3000/list_posts"
#    }

response.headers['Location']
# => "http://localhost:3000/list_posts"

```

Here the response body is set to a message about redirection and the content type is `nil`, but because this is a redirect, we really don't care about these values.

Instead, the two key parts are:

1. the `302` status code
2. the `Location` header

These two values are what make the redirect happen. The reason is that the `302` status code means `Found`, as in "we found the thing you requested, but it's somewhere else", and the value found in the `Location` header is used to explain where.

So the `302` tells the browser that it needs to redirect, and the `Location` header explains where it should redirect to. By passing a path string to `redirect_to` in our action above, we set both of these values to tell the user's browser to go to `/list_posts`.

It's also interesting to note that issuing a redirect causes the browser to make a total of two requests when the user submits the new post `<form>`:

1. ```
   POST /create_post
   ```

   - creates post in DB
   - HTTP response: `302` `Location: /list_posts`

2. `GET /list_posts`

And speaking of submitting the form, we're now able to create a new post from `/new_post`, thanks to the route and action above!

### Linking to Our New Post Page

Now that we can create posts from `/new_post`, let's link to it from `/list_posts`:

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <!-- ... -->
    </div>

    <!-- link to new post -->
    <a href="/new_post">New Post</a>

  </body>
</html>

```

And back to `/list_posts` from `/new_post` :

```
<!-- app/views/application/new_post.html.erb -->

<html>
  <body>

    <form method="post" action="/create_post">
      <!-- ... -->
    </form>

    <br />
    <!-- link back to the list of post -->
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

### Finishing Our Form

Before we move on, there are a couple attributes we should add to the fields in our `<form>`:

```
<html>
  <body>

    <form method="post" action="/create_post">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" />
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" />
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

As you can see above, each `<input>` and `<textarea>` gets an `id`, and their corresponding `<label>`gets a `for` attribute set to the value of the `id`. This is how we associate a `<label>` with its input field.

This has two primary benefits:

1. when you click the label in the browser, the focus will go to the input field
2. visually impaired users that depend on screen reading software will be able to use your form, since screen readers depend on these attributes to associate form inputs with their labels

# 2.7 Edit a Record

## [Editing and Updating a Post](https://launchschool.com/books/demystifying_rails/read/edit_a_record#editupdate)

We can now view a list of all of our posts, read an individual post, and create new ones. Next, it would be nice to be able to make changes to an existing post.

Much like creating a new post, this process will involve two parts:

1. provide the user with a form to allow editing of the existing post
2. receive that submitted form data and update the appropriate post in the database

So first let's define a route to show a form so that we can edit the post:

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  get  '/edit_post/:id' => 'application#edit_post'
end

```

An action to render our edit form:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def edit_post
    post = connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", params['id']).first

    render 'application/edit_post', locals: { post: post }
  end

  # ...
end

```

And a view for our edit form:

```
<!-- app/views/application/edit_post.html.erb -->

<html>
  <body>

    <form method="post" action="/update_post/<%= post['id'] %>">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" value="<%= post['title'] %>"/>
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"><%= post['body'] %></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" value="<%= post['author'] %>"/>
      <br /> <br />

      <input type="submit" value="Update Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

Our route simply sends requests in the format of `/edit_post/:id` to `application#edit_post`, capturing the post ID just like we did in the `show_post` route.

Inside the `edit_post` action, we find the post to edit using the same call to the database as we used in `show_post`, and then pass it into the `application/edit_post` view.

This `edit_post` view is identical to the `new_post` with three exceptions:

1. our submit button reads `Update Post`
2. all of the `<form>` fields are populated with the values of the post
3. the `<form>` `action` attribute points to our new route (using the proper post ID)

### Updating a Post

With our edit form now in place, we'll need to define the route and action to actually update the post in the database.

The `<form>` `action` above points to a path of the format `/update_post/:id`, so we'll need to define that route:

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  post '/update_post/:id' => 'application#update_post'
end

```

And then we'll define this `update_post` action:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def update_post
    update_query = <<-SQL
      UPDATE posts
      SET title      = ?,
          body       = ?,
          author     = ?
      WHERE posts.id = ?
    SQL
    connection.execute update_query, params['title'], params['body'], params['author'], params['id']

    redirect_to '/list_posts'
  end
end

```

The `<form>` above will make a `POST` request to `/update_post/:id`, so we define our route with `post`and direct requests of that format to a new action, `application#update_post`.

Inside this new action, we execute a SQL statement to `UPDATE` the post by its ID, using the new values submitted by the `application/edit_post` `<form>`.

Remember, the `name` attributes on our `<input>`s in the `application/edit_post` view determine what these values are called in `params` when they arrive in our controller action.

After the post is updated in the database, then we `redirect_to '/list_posts'`.

So try it out! If you visit `/edit_post/1`, change something, and submit the form, you'll be able to make changes to that post.

### Link to Edit Post from List Posts

Editing posts works now, but we don't have any links to get to the edit post page yet. Let's change that by adding an `Edit` link next to each post title in `list_posts`:

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <% posts.each do |post| %>
        <div class="post">

          <h2 class="title"> <!-- ... --> </h2>

          <small class="meta">

            <!-- ... -->

          </small>
          <!-- link to edit post -->
          <a href="/edit_post/<%= post['id'] %>">Edit</a>
        </div>
        <hr />
      <% end %>
    </div>

    <!-- ... -->

  </body>
</html>

```

This whole post editing process is analogous to the post creation process. That is, `edit_post` behaves very similarly to `new_post` (provides the user with a `<form>`), and `update_post` behaves very similarly to `create_post` (executes SQL and redirects). The key differences are that the `edit_post` route requires a post ID (since editing, unlike creating a post, is in reference to an existing database row) and the `edit_post` view needs to populate its `<form>` with the values of the post it represents.

**\*Redirect vs. Render***
You probably have seen a bit of a pattern here: whenever we do HTTP `POST`, we redirect instead of `render`. This is because of HTTP semantics. That is, the *meaning* of a `POST` request is different from that of a `GET` request.
When we `POST`, we're requesting for the server to *do something* e.g. change something in the database. With a `GET` request, we're asking the server to *give us something*. So the point of a `POST`request is not to *get* something, but to have the server *do* something. But, even though the `POST`request itself is *not* a request for a document (e.g. HTML), we're still making these `POST` requests from a browser, so we have to show the user *something*. And so, once our action is done successfully processing a `POST` request, it delegates responsibility for displaying something to the user on to another action, by redirecting. Another reason for redirecting instead of rendering is that if we render after a POST request, we may run into errors when trying to refresh the page as the URL from the POST request will not be changed even though a new has rendered.

# 2.8 Find and Delete a Post(Record)

## [Extract Finding A Post](https://launchschool.com/books/demystifying_rails/read/find_and_delete_a_record#extractfindingapost)

Now, post editing works, but if you were to look at the beginning of our `show_post` and `edit_post`actions, you'd notice that the logic to look up a post in the database is the same in each. So before we move on, let's take a moment to refactor this logic into its own method to make it more reusable.

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def show_post
    post = find_post_by_id(params['id'])

    render 'application/show_post', locals: { post: post }
  end

  # ...

  def edit_post
    post = find_post_by_id(params['id'])

    render 'application/edit_post', locals: { post: post }
  end

  # ...

  def find_post_by_id(id)
    connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", id).first
  end
end

```

Here we simply move the line we've been using to look up individual posts into its own method, named `find_post_by_id`. Then we use it in both `show_post` and `edit_post` like so:

```
post = find_post_by_id(params['id'])

```

Again, refactoring our logic into one place like this makes it:

1. easy to change later, because now we'll only need to make a change in one place
2. easy to use elsewhere if needed

## [Delete a Post](https://launchschool.com/books/demystifying_rails/read/find_and_delete_a_record#deleteapost)

NOTE: Make sure **not to delete** the three original posts, or you may run into errors later in the book.

At this point we can view posts, create them, edit them, but we can't yet delete them, so that'll be our next step.

To do this, we'll just need something a user can click to send a request that deletes a post. But since deleting a post is destructive, we won't want to use a `GET` request for this. Instead, we'll use a `POST` request, and to perform this `POST`, we'll need to create a `<form>` to submit.

This `<form>` will be incredibly simple though, because it will have no `<input>`s, except for a submit button. All it needs to do is `POST` to the path for destroying the post.

Here's what it looks like:

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <% posts.each do |post| %>
        <div class="post">
          <h2 class="title"> <!-- ... --> </h2>

          <small class="meta">

            <!-- ... -->

          </small>
          <!-- ... -->
          <form method="post" action="/delete_post/<%= post['id'] %>" style='display: inline'>
            <input type="submit" value="Delete" />
          </form>
        </div>
        <hr />
      <% end %>
    </div>

    <!-- ... -->

  </body>
</html>

```

Then the route our new `<form>` points to:

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  post '/delete_post/:id' => 'application#delete_post'
end

```

And the action that routes to:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def delete_post
    connection.execute("DELETE FROM posts WHERE posts.id = ?", params['id'])

    redirect_to '/list_posts'
  end
end

```

We start off in `application/list_posts` by giving each of our posts a `<form>`:

```
<form method="post" action="/delete_post/<%= post['id'] %>" style='display: inline'>
  <input type="submit" value="Delete" />
</form>

```

This will result in a `Delete` button for each post.

The `<form>` `action` has the format `/delete_post/:id`, so we route those requests to `application#delete_post`.

Inside `application#delete_post`, we see the familiar pattern we noticed in `create_post` and `update_post` (the other actions that receive `POST` requests):

1. make a change to the database
2. redirect

Now is a good time to go and try out some of the functionalities we've built into our app. We should now be able to create, edit, and delete posts.

# 2.9 Controller Patterns and CRUD

## [Controller Patterns in a Datacentric App](https://launchschool.com/books/demystifying_rails/read/controller_patterns_and_crud#controllerpatterns)

So far we've seen each action in our controller doing the following two things:

1. Interacting with the database, either read data from the database (with a `SELECT` SQL statement) or write data to the database (with `INSERT`, `UPDATE` or `DELETE` SQL statements)
2. Use the retrieved data to render a view template (in case a "read"), or redirect to a different page (in case of a "write")

If the request wants a HTML document back (in case of HTTP GET), it retrieves the data from the database then uses it to render a dynamic view template into a HTML document, which it then uses to set up the HTTP response; if the request wants to update data in the database, it collects the user's input, prepares the data, uses it to compose a SQL statement to change the database, then setup the HTTP response.

The controller stands between the data (in the database) and the presentation (the view templates) to coordinate the flow. This is a fundamental pattern of controllers that we'll see repeatedly in Rails applications.

## [CRUD](https://launchschool.com/books/demystifying_rails/read/controller_patterns_and_crud#crud)

Before we move on, there's one more interesting thing to note: at this point, we've built out what is known as **CRUD** functionality for our simple blog application

CRUD stands for:

- C - create
- R - read
- U - update
- D - delete

CRUD represents four basic actions to interact with data. The four resource actions here map directly to SQL's four core commands: `INSERT`, `SELECT`, `UPDATE` and `DELETE`. In fact, our current Rails application is essentially a web front that collect user's input and delegates the data manipulation to the underlying database. Sometimes people call these type of apps "CRUDy" apps or "data centric" apps, where the web application's concerns are centered around interacting with the database.

# 2.10 Data Encapsulation With Models

## [Creating a New Post](https://launchschool.com/books/demystifying_rails/read/data_encapsulation_with_models#newpostwithmodel)

Our application works now with data access patterns that directly embed SQL statements in the application code (the controller actions). This works, and in fact, this is how many applications were built about 20 years ago before the emergence of modern web development frameworks. The problem is as the application grows bigger, the SQL statements get scattered all around the application, then for simple data related changes (such as changing the table name of the `posts` to `blog_posts` in the database) you'd have to scan the entire application code base to to make changes on all SQL statements that touch that data.

The answer to this problem is encapsulation, to move all SQL commands about a piece of data into a single place, so they can be easily updated when necessary.

Let's do this now with a `Post` model.

`app/models/post.rb`

```
class Post
  attr_reader :id, :title, :body, :author, :created_at

  def initialize(attributes={})
    @id = attributes['id']
    @title = attributes['title']
    @body = attributes['body']
    @author = attributes['author']
    @created_at = attributes['created_at']
  end
end

```

Be sure to notice that a model is *just a Ruby class*, and in Rails these model classes live in the `app/models`directory. Thus, we create our `Post` class in `app/models/post.rb`.

This is a very simple class - in fact it is nothing more than a container for a bunch of attributes (such as `title`, `body` etc) at this point. With the `initialize` method, we allow data to be passed in as a hash with `Post.new` when a `Post` object is instantiated and then assign the values to the instance variables.

You'll notice that we have a default value of an empty hash for our `attributes` parameter:

```
def initialize(attributes={})
```

This is so that we can instantiate an empty `Post`, without passing any arguments to it. So now:

```
post = Post.new

```

is equivalent to

```
post = Post.new({})

```

Then later in the class, we define reader methods to get to each of these attributes by using `attr_reader`.

And remember:

```
attr_reader :title

```

is just a shorthand for defining a method like this

```
def title
  @title
end

```

Now we're ready to start moving our database calls out of `ApplicationController` and into our `Post`model.

We're going to first move the SQL commands from `create_post` in our controller to the `Post` class. We are going to wrap the database access steps in a `save` method.

### app/models/post.rb

```
class Post
  attr_reader :id, :title, :body, :author, :created_at
  # ...

  def save
    insert_query = <<-SQL
      INSERT INTO posts (title, body, author, created_at)
      VALUES (?, ?, ?, ?)
    SQL

    connection.execute insert_query,
      title,
      body,
      author,
      Date.current.to_s
  end

  # ...

  private

  # ...

  def connection
    db_connection = SQLite3::Database.new('db/development.sqlite3')
    db_connection.results_as_hash = true
    db_connection
  end
end

```

Then our controller action for `create_post` becomes:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base

  # ...

  def create_post
    post = Post.new('title' => params['title'],
                    'body' => params['body'],
                    'author' => params['author'])
    post.save
    redirect_to '/list_posts'
  end
end

```

The logic in the controller action is much simpler now - we are just going to instantiate a post object from the params, which has all of the user's inputs, and tell the post object to save itself into the database.

## [Find and Show a Post](https://launchschool.com/books/demystifying_rails/read/data_encapsulation_with_models#findshowpost)

Next, let's move our logic for looking up a post to a `Post.find` method. This is not an operation that we do on an instance of a Post (we don't have one yet, we are finding one!) so we'll put it as a class method.

`app/models/post.rb`

```
class Post
  attr_reader :id, :title, :body, :author, :created_at

  # ...

  def self.find(id)
    post_hash = connection.execute("SELECT * FROM posts WHERE posts.id = ? LIMIT 1", id).first
    Post.new(post_hash)
  end

  # ...

end

```

Also because the `connection` method needs to be accessed from a class method `find`, we'll move it to be a class method as well.

```
class Post
  attr_reader :id, :title, :body, :author, :created_at


  # ...

  def self.connection
    db_connection = SQLite3::Database.new 'db/development.sqlite3'
    db_connection.results_as_hash = true
    db_connection
  end

  def connection
    self.class.connection
  end

  # ...

```

We can now change the `show` controller action accordingly:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base

  # ...

  def show_post
    post = Post.find(params['id'])

    render 'application/show_post', locals: { post: post }
  end
end

```

Here again, we just move our database logic out of our controller and into a method in our model, making sure that this new `Post.find` method returns a `Post` object.

And after using `Post.find` in the `show_post` action, we're also able to get rid of our `find_post_by_id`method from the controller entirely, since we're now exclusively using our new `Post.find` method for this purpose.

We have refactored the code to the model and changed the controller actions, but if we visit `/show_post/1` now, we'll find ourselves staring at an error page. The reason for this is that we changed the type of objects that are passed into the view as `posts`. Before they were `Hash` objects, and now they're `Post` objects.

Let's change our `show_post` view to use the Post object instead. Since we have defined `attr_reader` for the Post class, accessing its attributes is now easier:

```
<!-- app/views/application/show_post.html.erb -->

<html>
  <body>

    <div class="post">
      <h2 class="title">
        <%= post.title %>
      </h2>

      <small class="meta">
        <span class="author">by <%= post.author %> -</span>
        <em class="created_at"><%= post.created_at %></em>
      </small>

      <p class="body"><%= post.body %></p>
    </div>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

And with that, the `show_post` action and view are successfully using our new `Post` model. Next, let's do the same thing for our `edit_post` action and view. It will be a very similar process.

## [Edit a Post](https://launchschool.com/books/demystifying_rails/read/data_encapsulation_with_models#editwithmodel)

After we're done altering the `edit_post` action and view, we should be able to visit `/edit_post/1` and see a form filled with the current values of that post.

```
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base

  # ...

  def edit_post
    post = Post.find(params['id'])

    render 'application/edit_post', locals: { post: post }
  end

  # ...
end

<!-- app/views/application/edit_post.html.erb -->

<html>
  <body>

    <form method="post" action="/update_post/<%= post.id %>">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" value="<%= post.title %>"/>
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"><%= post.body %></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" value="<%= post.author %>"/>
      <br /> <br />

      <input type="submit" value="Update Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

Make sure to try out the code above yourself.
In the next chapter, we'll deal with altering our action for `update_post` so that it utilizes the new `Post`model we've been working with.

# 2.11 Expanded Encapsulation Through Our Models

## [Update a Record](https://launchschool.com/books/demystifying_rails/read/expanded_encapsulation_through_our_models#updatearecord)

Let's first look at the current controller code for updating a post:

```
class ApplicationController < ActionController::Base

  # ...

  def update_post
    update_query = <<-SQL
      UPDATE posts
      SET title      = ?,
          body       = ?,
          author     = ?
      WHERE posts.id = ?
    SQL
    connection.execute(update_query, params['title'], params['body'], params['author'], params['id'])

    redirect_to '/list_posts'
  end
end

```

Updating an existing post is essentially saving it back to the database with new values. So ideally, we'd like to be able to do the following:

```
# ...
def update_post
  post = Post.find(params['id'])
  post.set_attributes('title' => params['title'], 'body' => params['body'], 'author' => params['author'])
  post.save

  redirect_to '/list_posts'
end

# ...

```

We first retrieve the post from the database with its `id` passed through the URL, then set its attribute values with user inputs, and in the end save the post back to the database with updated values.

However, if we call `save` on an existing `Post`, it will create a new post in the database… with the `INSERT`SQL command. This is not what we want. When we update a record, it's always an existing record already in the database. When we try to update the record in the database, we should use the `UPDATE` SQL command instead of `INSERT`.

The way to tell if a record is a new record or not is to check its `id` column - if it's `nil` then it's a new record that has never been saved into the database; if it's not `nil` then it's an existing record since the `id`column is automatically generated by the database.

We'll adjust our model code to either `INSERT` or `UPDATE` records based on whether the post is a new or existing one.

```
### app/models/post.rb ###

class Post
  attr_reader :id, :title, :body, :author, :created_at

  # ...

  def new_record?
    id.nil?
  end

  def save
    if new_record?
      insert
    else
      update
    end
  end

  def insert
    insert_query = <<-SQL
      INSERT INTO posts (title, body, author, created_at)
      VALUES (?, ?, ?, ?)
    SQL

    connection.execute insert_query,
      title,
      body,
      author,
      Date.current.to_s
  end

  def update
    update_query = <<-SQL
      UPDATE posts
      SET title      = ?,
          body       = ?,
          author     = ?
      WHERE posts.id = ?
    SQL

    connection.execute update_query,
      title,
      body,
      author,
      id
  end

  # ...

end

```

First, we change `Post#save` to react conditionally, based on whether or not it's a `new_record?`. If it is, it calls `insert`, if not, `update`.

We also need to implement the `set_attributes` method for the `Post` class, and it's pretty straightforward. We can even refactor the the `initialize` method to call `set_attributes` method to remove some duplication.

`app/models/post.rb`

```
class Post
  attr_reader :id, :title, :body, :author, :created_at

  def initialize(attributes={})
    set_attributes(attributes)
  end

  def set_attributes(attributes)
    @id = attributes['id'] if new_record?
    @title = attributes['title']
    @body = attributes['body']
    @author = attributes['author']
    @created_at ||= attributes['created_at']
  end

  # ...

end

```

Note that we have made some changes within `set_attributes`. The `id` is only set if this `Post` is a new record. We always set the attributes for `title`, `body` and `author`, but we only conditionally set `created_at`. We do this because we only want to set `created_at` once: when the `Post` object is first created.

## [Delete a Post Model](https://launchschool.com/books/demystifying_rails/read/expanded_encapsulation_through_our_models#deleteapostmodel)

The rest of this chapter will comprise of code related to deleting and listing posts. We want to write code that allows us to delete and list records using our models. The business logic and interactions with the database should be done through our model. The workflow will be similar to code we previously worked on in this chapter.

First we'll write the code for deleting a post. Remember, we want to have database logic inside our model; this applies to deleting a post as well.

```
# app/models/post.rb

class Post
  attr_reader :id, :title, :body, :author, :created_at

  # ...

  # used in application#delete_post
  def destroy
    connection.execute "DELETE FROM posts WHERE posts.id = ?", id
  end
end

```

Finally, we'll use that code and our `Post` model in the `delete_post` action.

```
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base

  # ...

  def delete_post
    post = Post.find(params['id'])
    post.destroy

    redirect_to '/list_posts'
  end

  # ...

end

```

## [List Posts](https://launchschool.com/books/demystifying_rails/read/expanded_encapsulation_through_our_models#listposts)

Now that we have updated our code for deleting a post, lets update our for listing all posts. The various methods we'll need for grabbing those records from the DB (through our model) should also be implemented here.

To accomplish this task, we'll define a class method in the `Post` class that executes the SQL command to return all the posts in a hash, then we'll use `map` to create an array of `Post` objects from that.

```
# app/models/post.rb

class Post
  attr_reader :id, :title, :body, :author, :created_at

  # ...

  def self.all
    post_hashes = connection.execute("SELECT * FROM posts")
    post_hashes.map do |post_hash|
      Post.new(post_hash)
    end
  end

  # ...
end

```

```
# app/controllers/application_controller.rb

class ApplicationController < ActionController::Base
  def list_posts
    posts = Post.all

    render 'application/list_posts', locals: { posts: posts }
  end
end

```

Remember, we'll now want to use our Post model methods this view. That includes the getters for the various states of a Post model.

```
<!-- app/views/application/list_posts.html.erb -->

<html>
  <body>

    <div class="posts">
      <% posts.each do |post| %>
        <div class="post">
          <h2 class="title">
            <a href="/show_post/<%= post.id %>">
              <%= post.title %>
            </a>
          </h2>

          <small class="meta">
            <span class="author">by <%= post.author %> -</span>
            <em class="created_at"><%= post.created_at %></em>

            <a href="/edit_post/<%= post.id %>">Edit</a>

            <form method="post" action="/delete_post/<%= post.id %>" style='display: inline'>
              <input type="submit" value="Delete" />
            </form>
          </small>
        </div>
        <hr />
      <% end %>
    </div>

    <a href="/new_post">New Post</a>

  </body>
</html>

```

Now that we've done all that, our blog app has all the conveniences that a model gives us, at least for our posts. In the next chapter, we'll add in some validations, and we'll show how they work in the process.

# 2.12 Model Validations

## [How to Write a Model Validation](https://launchschool.com/books/demystifying_rails/read/model_validations#writeamodelvalidation)

At the moment, we simply save records into the database without checking if the data is valid or not. However, our application is built with the assumption that a post should always have a title, a body and an author. If we allow posts without a title, body or an author to be saved into the database, repercussions will surface in many places and cause bugs in our code. This would occur because of the mismatch of the integrity of data and the assumption of the application code.

As a general guideline, whenever an application allows user's input, we want to validate the data as early as possible. Let's look at how we can do that with our `Post` model before the records are saved into the database.

```
### app/models/post.rb ###

class Post

  # ...

  def valid?
    title.present? && body.present? && author.present?
  end

  # ...

end

```

We are adopting the validation rule that a post is only valid when `title`, `body` and `author` fields are all present.

And notice when we check for the presence of each of the attributes, we're using the `present?` method, which is a method that Rails provides:

```
> ''.present?
=> false

> nil.present?
=> false

> 'something'.present?
=> true

```

As you can see above, this `present?` method returns `false` if it's called on `nil` or an empty string. Just what we're looking for to test if a title, body, or author is present.

And now that we have a way to check if a post is valid or not, let's make sure we do that before saving a post, and react appropriately:

```
### app/models/post.rb ###

class Post

  # ...

  def save
    return false unless valid?

    if new_record?
      insert
    else
      update
    end

    true
  end

  # ...

end

```

Here we use what's called a *guard clause*:

```
return false unless valid?
```

We use this guard clause here to "guard" against execution further into `Post#save` unless the post is valid. This prevents invalid posts from being saved to the database.

So now when we call `Post#save`, we'll return `true` if validation passes and the post is saved to the DB. Otherwise, if the validation fails and the post is *not* saved, we'll return `false`.

We'll see how to integrate this model validation with the form submission workflow next.

## [Integrate Validations With Forms](https://launchschool.com/books/demystifying_rails/read/model_validations#integratevalidationswithforms)

Let's now look at how we can integrate the validation logic to the form submission process.

From a user experience point of view, when the user provides invalid inputs, we want to:

1. instead of taking the user to the listing posts page, we would "bounce back" to the page with the input form
2. preserve the user's input so they don't have to fill the form from scratch
3. show the user what input field(s) are not valid

Let's see how to do this with the "create a post" workflow:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...


  def create_post
    post = Post.new('title' => params['title'], 'body' => params['body'],
      'author' => params['author'])
    if post.save
      redirect_to '/list_posts'
    else
      render 'application/new_post', locals: { post: post }
    end
  end

  # ...

end

```

From this code you can see if `save` returns `false`, in the case of validation failure, we will render the `new_post` template again with the post object that contains all the user's inputs.

We `render` the `new_post` view here because we need to provide the user with a form to keep editing the post.

We also have to change the `new_post` view so that it would render with a `post` object passed into it.

`app/views/application/new_post.html.erb`

```
<html>
  <body>
    <form method="post" action="/create_post">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" value="<%= post.title %>"/>
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"><%= post.body %></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" value="<%= post.author %>"/>
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

With our view ready, we'll just need to adjust the `new` controller action to pass in an instantiated "empty" post object.

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def new_post
    post = Post.new

    render 'application/new_post', locals: { post: post }
  end

  # ...

end

```

While we're at it, let's also alter our code for updating a post, as we'll want to include validations for that workflow as well.

```
class ApplicationController < ActionController::Base

  # ...

  def update_post
    post = Post.find(params['id'])
    post.set_attributes('title' => params['title'], 'body' => params['body'],
      'author' => params['author'])
    if post.save
      redirect_to '/list_posts'
    else
      render 'application/edit_post', locals: { post: post }
    end
  end

  # ...
end

```

```
<!-- app/views/application/edit_post.html.erb -->

<html>
  <body>
    <form method="post" action="/update_post/<%= post.id %>">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" value="<%= post.title %>"/>
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"><%= post.body %></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" value="<%= post.author %>"/>
      <br /> <br />

      <input type="submit" value="Update Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

Now we have implemented 1) and 2) from the three requirements we listed before. We are going to tackle the displaying errors requirement in the next lesson.

==NOTE==: When you reload a page with a browser, it asks the browser to replay the last HTTP request. In the case of a form submission with errors, the last request will be a `POST` request because the behavior on the server side is to render the form and not redirect to another path.

## [Display Validations](https://launchschool.com/books/demystifying_rails/read/model_validations#displayvalidations)

The last piece we need to do to ensure a good user experience, is to show the validation errors so the user knows what went wrong with their inputs.

Those messages should be created while we validate the user inputs, which currently happens in the `Post`model. We could just store an array of error messages in the model. Since the model will be passed into the view template when it's rendered, the view template can then pull the error messages out of the model to display on the screen.

Here's what we'll do:

```
### app/models/post.rb ###

class Post
  attr_reader :id, :title, :body, :author, :created_at, :errors
  # ...

  def initialize(attributes={})
    # ...

    @errors = {}
  end


  def valid?
    @errors['title']  = "can't be blank" if title.blank?
    @errors['body']   = "can't be blank" if body.blank?
    @errors['author'] = "can't be blank" if author.blank?
    @errors.empty?
  end

  # ...

end

```

The `blank?` method is defined by Rails to work on `nil` and strings with the following behavior:

```
> ''.blank?
=> true

> nil.blank?
=> true

> 'something'.blank?
=> false

```

As you probably have guessed, `blank?` is the opposite of `present?`

Now that we know an invalid post created from user input would always have errors set in the object, we can adjust our view to show the error messages:

`app/views/application/new_post.html.erb`

```
<html>
  <body>

    <div class="errors">
      <% post.errors.each do |attribute, error| %>
        <p class="error" style="color: orange">
          <%= attribute %>: <%= error %>
        </p>
      <% end%>
    </div>

    <form method="post" action="/create_post">

      <label for="title"> Title</label>
      <input id="title" name="title" type="text" value="<%= post.title %>"/>
      <br /> <br />

      <label for="body"> Body</label>
      <textarea id="body" name="body"><%= post.body %></textarea>
      <br /> <br />

      <label for="author"> Author</label>
      <input id="author" name="author" type="text" value="<%= post.author %>"/>
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

Make sure to include the changes we've made above in your `edit_post.html.erb` file as well. Now is a good time to run through our app and test the code that we have just added in. Try making a post with invalid inputs; the new post view should render and the application should display a list of errors.

# 2.13 A Second Resource

## [Adding Comments to Our App](https://launchschool.com/books/demystifying_rails/read/a_second_resource#addingcomments)

Now that we have all the CRUD actions working for posts *and* we have a `Post` model, let's add on to our web app's functionality by adding post comments.

Each post will be able to have many comments, so let's start off by giving ourselves some comments in our DB to play with. This process will be the same as it was with posts, we'll:

1. create a new table (define a structure)
2. populate that table with rows (place data in that structure)

Our comments will also have `id`, `body`, `author`, and `created_at` columns, just like our posts. But there's another thing we'll have to keep track of for each comment: what post does the comment belong to?

In relational databases, we keep track of this using a **foreign key**.

For both tables, our `id` column holds the *primary key* for each row, that is, a value that uniquely identifies that row within that table. A *foreign key* is called "foreign" because it references a row in a different ("foreign") table.

Since our comments belong to a post, we'll follow Rails' convention and name this foreign key column `post_id`. The integer held in this column will be the ID of the post row that a given comment row belongs to.

But our process for creating the table and populating it with data remains the same as it was with posts. First we have some SQL to create the table:

```
-- db/comments.sql --

CREATE TABLE "comments" (
  "id" INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
  "body" text,
  "author" varchar,
  "post_id" integer,
  "created_at" datetime NOT NULL);

```

And some CSV we'll import to create some comments, three for each post:

`db/comments.csv`

```
1,Lorem ipsum dolor sit amet.,Matz,1,2014-12-09
2,Lorem ipsum dolor sit amet.,DHH,1,2014-12-09
3,Lorem ipsum dolor sit amet.,tenderlove,1,2014-12-09
4,Lorem ipsum dolor sit amet.,Matz,2,2014-12-09
5,Lorem ipsum dolor sit amet.,DHH,2,2014-12-09
6,Lorem ipsum dolor sit amet.,tenderlove,2,2014-12-09
7,Lorem ipsum dolor sit amet.,Matz,3,2014-12-09
8,Lorem ipsum dolor sit amet.,DHH,3,2014-12-09
9,Lorem ipsum dolor sit amet.,tenderlove,3,2014-12-09

```

Notice the `post_id` values for each comment. These are after the author name and before the date.

First we run the SQL against our `db/development.sqlite3` database:

```
$ sqlite3 db/development.sqlite3 < db/comments.sql

```

Then we can use the `sqlite3` console to see that we have a `comments` table now, but no rows within:

```
$ sqlite3 db/development.sqlite3

sqlite> .tables
comments posts

sqlite> SELECT * FROM comments;
sqlite>

```

And lastly, we'll import our comments CSV:

```
sqlite> .mode csv
sqlite> .import db/comments.csv comments

sqlite> SELECT * FROM comments;
8,"Lorem ipsum dolor sit amet.",DHH,3,2014-12-09
7,"Lorem ipsum dolor sit amet.",Matz,3,2014-12-09
6,"Lorem ipsum dolor sit amet.",tenderlove,2,2014-12-09
5,"Lorem ipsum dolor sit amet.",DHH,2,2014-12-09
4,"Lorem ipsum dolor sit amet.",Matz,2,2014-12-09
3,"Lorem ipsum dolor sit amet.",tenderlove,1,2014-12-09
2,"Lorem ipsum dolor sit amet.",DHH,1,2014-12-09
1,"Lorem ipsum dolor sit amet.",Matz,1,2014-12-09

```

And now we have comments in our database!

## [Displaying Comments](https://launchschool.com/books/demystifying_rails/read/a_second_resource#displayingcomments)

Now that we have rows of comments in a `comments` table in our database, let's show the comments that belong to a post in our `show_post` view.

We'll do this in two steps:

1. collect the comments from the DB for a post inside the controller action and pass them to the view
2. display the comments in the view

Let's start with the `show_post` action changes:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base

  # ...

  def show_post
    post     = Post.find(params['id'])
    comments = connection.execute('SELECT * FROM comments WHERE comments.post_id = ?', params['id'])

    render 'application/show_post', locals: { post: post, comments: comments }
  end

  # ...

end

```

Here we simply find our comments by specifying in our query:

```
WHERE comments.post_id = ?

```

Where `params['id']` (the post's ID) is substituted for the `?`. This where clause is how we only pull comments that are "associated" to a post.

Then we pass the resulting hash along into our view using `locals`, so let's now make use of `comments` in our `show_post` view:

`app/views/application/show_post.html.erb`

```
<html>
  <body>
    <div class="post">
      <!-- post title, meta data, and body displayed here -->
      <br /><br />
      <div class="comments">
        <h3>Comments:</h3>
        <hr />
        <% comments.each_with_index do |comment, index| %>
          <div class="comment">
            <small class="comment_meta">
              <span class="comment_author">#<%= index+1 %> by <%= comment['author'] %> -</span>
              <em class="comment_created_at"><%= comment['created_at'] %></em>
            </small>
            <p class="comment_body"><%= comment['body'] %></p>
          </div>
          <hr />
        <% end %>
      </div>
    </div>
    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

Here we loop again, using `<% %>` instead of `<%= %>`, just like we did with our post titles in `list_posts`, but this time we use `each_with_index` so that we can number our comments. Just as a quick Ruby-only illustration of how this works, here's what `each_with_index` can do:

```
['a','b','c'].each_with_index do |char, idx|
  puts "##{idx+1}: #{char}"  
end  

# prints:
#
# #1: a
# #2: b
# #3: c

```

So now if we visit `/show_post/1`, we'll see the comments for the post as well.

NOTE: As a reminder, if you ended up deleting any of the three original posts in a previous assignment, you will not be able to see the comments associated with the deleted post(s).

## [A Comment Model](https://launchschool.com/books/demystifying_rails/read/a_second_resource#acommentmodel)

Just like the way we have a `Post` model for the posts, let's create a `Comment` model for the comments:

`app/models/comment.rb`

```
class Comment
  attr_reader :id, :body, :author, :post_id, :created_at

  def initialize(attributes={})
    @id = attributes['id'] if new_record?
    @body = attributes['body']
    @author = attributes['author']
    @post_id = attributes['post_id']
    @created_at ||= attributes['created_at']
  end

  def new_record?
    @id.nil?
  end
end

```

Now we have the beginning of a `Comment` model. The file `app/models/comment.rb` contains an `initialize` and `new_record?` method similar to those found in `Post`.

# 2.14 Working With Model Associations

## [Association Between Models](https://launchschool.com/books/demystifying_rails/read/working_with_model_associations#associationbetweenmodels)

Currently in the `ApplicationController`, we first find a post from the database, then we need to get a collection of comments that are associated with the post. We're getting that from directly executing SQL in the controller action, which is not the ideal solution.

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base

  # ...

  def show_post
    post     = Post.find(params['id'])
    comments = connection.execute('SELECT * FROM comments WHERE comments.post_id = ?', params['id'])

    render 'application/show_post', locals: { post: post, comments: comments }
  end

  # ...

end

```

Since the SQL command needs a post id to find the comments, we'll move the command to the `Post`model.

`app/models/post.rb`

```
class Post

  # ...

  def comments
    comment_hashes = connection.execute 'SELECT * FROM comments WHERE comments.post_id = ?', id
    comment_hashes.map do |comment_hash|
      Comment.new(comment_hash)
    end
  end

  # ...

end

```

Now we can change the code in the controller:

`app/controllers/application_controller.rb`

```
class ApplicationController < ActionController::Base

  # ...

  def show_post
    post = Post.find(params['id'])

    render 'application/show_post', locals: { post: post }
  end

  # ...

end

```

And make adjustments on the view:

`app/views/application/show_post.html.erb`

```
<html>
  <body>

    <div class="post">

      <!-- display post -->
      <br /> <br />
      <div class="comments">
        <h3>Comments:</h3>
        <% post.comments.each_with_index do |comment, index| %>
          <p class="comment">
            <small class="comment_meta">
              <span class="comment_author">#<%= index %> by <%= comment.author %> -</span>
              <em class="comment_created_at"><%= comment.created_at %></em>
            </small>

            <p class="comment_body"><%= comment.body %></p>
          </p>
          <hr />
        <% end %>
      </div>
    </div>

    <!-- ... -->

  </body>
</html>

```

## [Creation Through Association](https://launchschool.com/books/demystifying_rails/read/working_with_model_associations#createthroughassociation)

Moving on, we'll provide users with a way of adding a comment to a post.

And because it's a [CRUD](https://launchschool.com/books/demystifying_rails/read/%22://a_database_backed_application#crud%22) action, creating a comment will very much resemble creating a post. Below you'll find a `<form>` to create a new comment placed in `show_post`, the route it submits to, and the `create_comment` action that route points to:

```
<!-- app/views/application/show_post.html.erb -->

<html>
  <body>

    <div class="post">

      <div class="comments">
        <hr />
        <% comments.each do |comment| %>
          <!-- display each comment -->
        <% end %>

        <!-- new comment form -->
        <form method="post" action="/create_comment_for_post/<%= post.id %>">

          <label for="body">Comment</label>
          <textarea id="body" name="body"></textarea>
          <br /> <br />

          <label for="author">Name</label>
          <input id="author" name="author" type="text" />
          <br /> <br />

          <input type="submit" value="Add Comment" />
        </form>
        <hr />

      </div>
    </div>

    <br />
    <a href="/list_posts">Back to Posts</a>

  </body>
</html>

```

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  post '/create_comment_for_post/:post_id' => 'application#create_comment'
end

```

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def create_comment

    insert_comment_query = <<-SQL
      INSERT INTO comments (body, author, post_id, created_at)
      VALUES (?, ?, ?, ?)
    SQL

    connection.execute insert_comment_query,
      params['body'],
      params['author'],
      params['post_id'],
      Date.current.to_s

      redirect_to "/show_post/#{params['post_id']}"
  end
  # ...

end

```

The primary difference in creating a comment, as opposed to creating a post, is our concern for `post_id`. When creating a comment, we'll need to be sure to associate it with the right post. This is essentially done in three steps.

First, we point the `<form>` `action` to a path that includes `post.id`:

```
<form method="post" action="/create_comment_for_post/<%= post.id %>">

```

Then we capture this `post_id` in the route:

```
post '/create_comment_for_post/:post_id' => 'application#create_comment'

```

And finally, we make sure to set the `post_id` for the row in the `comments` table:

```
connection.execute insert_comment_query,
  params['body'],
  params['author'],
  params['post_id'],
  Date.current.to_s

```

This way, when a comment is created through this process, it is always associated with the post identified by the ID in the URL. At the end of `create_comment`, we just redirect back to `show_post`, which will end up rendering the post again, now with a new comment.

Similar to how we moved the SQL command to retrieve comments associated to a post to the `Post` model, we'll do the same to the SQL command to create a comment associated to a post.

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def create_comment
    post = Post.find(params['post_id'])
    post.create_comment('body' => params['body'], 'author' => params['author'])
    redirect_to "/show_post/#{params['post_id']}"
  end
  # ...

end

```

Now the `Post` model will look like:

```
class Post

  # ...

  def create_comment(attributes)
    comment = Comment.new(attributes.merge!('post_id' => id))
    comment.save
  end

  # ...

end

```

Then the `Comment` model:

`app/models/comment.rb`

```
class Comment

  # ...

  def initialize(attributes={})
    @id = attributes['id'] if new_record?
    @body = attributes['body']
    @author = attributes['author']
    @post_id = attributes['post_id']
    @created_at ||= attributes['created_at']
  end

  def save
    if new_record?
      insert
    else
      # update # ...not yet defined
    end
  end

  def insert
    insert_comment_query = <<-SQL
      INSERT INTO comments (body, author, post_id, created_at)
      VALUES (?, ?, ?, ?)
    SQL

    connection.execute insert_comment_query,
      @body,
      @author,
      @post_id,
      Date.current.to_s
  end

  private

  def self.connection
    db_connection = SQLite3::Database.new 'db/development.sqlite3'
    db_connection.results_as_hash = true
    db_connection
  end

  def connection
    self.class.connection
  end
end

```

Notice that we have nearly identical database connections in Comment as we do in Post. We'll be extracting these commonalities later on.

# 2.15 Cleaning Up Our App

## [Validation for Creating a Comment](https://launchschool.com/books/demystifying_rails/read/cleaning_up_our_app#validationforcomments)

Following the way we created validation for posts, let's create validation for comments:

- The body and author field both have to be present.
- If validation fails, the user should be brought back to the create comment page with the fields of the comment form populated.

```
### app/models/comment.rb ###

class Comment
  attr_reader :id, :body, :author, :post_id, :created_at, :errors
  # ...

  def initialize(attributes={})
    # ...

    @errors = {}
  end

  def valid?
    @errors['body']   = "can't be blank" if body.blank?
    @errors['author'] = "can't be blank" if author.blank?
    @errors.empty?
  end

  def new_record?
    @id.nil?
  end

  def save
    return false unless valid?

    if new_record?
      insert
    else
      # update # ...not defined
    end

    true
  end

  # ...

end

```

```
### app/models/post.rb ###

class Post

  # ...

  def build_comment(attributes)
    Comment.new( attributes.merge!('post_id' => id) )
  end

  def create_comment(attributes)
    comment = build_comment(attributes)
    comment.save
  end

  # ...

end

```

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def create_comment
    post     = Post.find(params['post_id'])
    comments = post.comments
    # post.build_comment to set the post_id
    comment  = post.build_comment('body' => params['body'], 'author' => params['author'])
    if comment.save
      # redirect for success
      redirect_to "/show_post/#{params['post_id']}"
    else
      # render form again with errors for failure
      render 'application/show_post',
        locals: { post: post, comment: comment, comments: comments }
    end
  end

  # ...

end

```

```
<!-- app/views/application/show_post.html.erb -->

<html>
  <body>
    <div class="post">
      <!-- ... -->

      <div class="comments">
        <!-- ... -->

        <!-- display errors -->
        <div class="errors">
          <% comment.errors.each do |attribute, error| %>
            <p class="error" style="color: orange">
              <%= attribute %>: <%= error %>
            </p>
          <% end%>
        </div>

        <!-- populate comment <form> with values -->
        <form method="post" action="/create_comment_for_post/<%= post.id %>">

          <label for="body">Comment</label>
          <textarea id="body" name="body"><%= comment.body %></textarea>
          <br /> <br />

          <label for="author">Name</label>
          <input id="author" name="author" type="text" value="<%= comment.author %>"/>
          <br /> <br />

          <input type="submit" value="Add Comment" />

        </form>
        <hr />
      </div>
    </div>

    <!-- ... -->

  </body>
</html>

```

But now we need to consider a normal request to `show_post`, one that isn't a result of failed comment validation. In this case, we need to provide the view with a `Comment` object, because we're now calling `comment.errors` each time we render it. To set things straight, we'll simply instantiate an empty `Comment`in `show_post` and pass it into the view:

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def show_post
    post    = Post.find(params['id'])
    comment = Comment.new
    comments = post.comments
    render "application/show_post",
      locals: { post: post, comment: comment, comments: comments }
  end

  # ...

end

```

And with that, comment validation is complete!

## [Delete a Comment](https://launchschool.com/books/demystifying_rails/read/cleaning_up_our_app#deleteacomment)

Now that we have our `Comment` validation, lets move on to adding some more `Comment` related functionality. We're going to make it so we can delete a comment from a `Post` page.

First let's set up the route necessary to accomplish this.

```
### config/routes.rb

# ...

post '/list_posts/:post_id/delete_comment/:comment_id' => 'application#delete_comment'

```

Next, we'll add in a form that lets us delete a comment from a `Post`.

```
<!-- app/views/application/show_post.html.erb -->
<html>
  <body>
    <!-- display errors -->
    <div class="post">
      <!-- ... -->

      <div class="comments">
        <% comments.each do |comment| %>
          <!-- display each comment -->

          <form method="post" action="/list_posts/<%= post.id %>/delete_comment/<%=
          comment.id %>">
            <input type="submit" value="Delete Comment" />
          </form>
          <hr />
        <% end %>

        <!-- populate comment <form> with values -->

      </div>
    </div>

    <!-- ... -->

  </body>
</html>

```

For the time being, we'll use the `POST` action to do this. We'll show a way to simulate `PATCH`/`PUT` and `DELETE` actions later in this book.

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  # ...

  def delete_comment
    post = Post.find(params['post_id'])
    post.delete_comment(params['comment_id'])
    redirect_to "/show_post/#{params['post_id']}"
  end

  # ...

end

```

```
### app/models/post.rb ###

class Post

  # ...

  def build_comment(attributes)
    Comment.new(attributes.merge!('post_id' => id)
  end

  def create_comment(attributes)
    comment = build_comment(attributes)
    comment.save
  end

  def delete_comment(comment_id)
    Comment.find(comment_id).destroy
  end

  # ...

end

```

```
### app/models/comment.rb
  class Comment
    # ...
    def self.find(id)
      comment_hash = connection.execute("SELECT * FROM comments WHERE comments.id = ? LIMIT 1", id).first
      Comment.new(comment_hash)
    end

    def destroy
      connection.execute "DELETE FROM comments WHERE id = ?", id
    end

    # ...

    private

    def self.connection
      db_connection = SQLite3::Database.new 'db/development.sqlite3'
      db_connection.results_as_hash = true
      db_connection
    end

    def connection
      self.class.connection
    end
  end

```

Notice the order in which we wrote our code. It was a very top down approach. We start with our route and move onto the view. From the view we went to the controller and wrote an action for deleting a comment. And based on what model related methods we needed, we then proceeded to the `Comment` model and set up those methods. We're writing the code we want to see and then implementing that code when it is needed. With the code listed above, we can now delete comments!

## [List Comments](https://launchschool.com/books/demystifying_rails/read/cleaning_up_our_app#listcommentspage)

We would also like to have a page that shows all the comments that have been made in our Blog app. Lets do that now. Let's start with the view template.

```
<!-- app/views/application/list_comments.html.erb -->

<html>
  <body>

    <div class="comments">
      <% comments.each do |comment| %>

        <div class="comment">
          <small class="comment_meta">
            <span class="comment_post_title">
              Comment on
              <strong><%= comment.post.title %></strong>
            </span>

            <span class="comment_author">by <%= comment.author %> -</span>
            <em class="comment_created_at"><%= comment.created_at %></em>
          </small>

          <p class="comment_body"><%= comment.body %></p>
        </div>

        <hr />
      <% end %>
    </div>

  </body>
</html>

```

```
### config/routes.rb ###

Rails.application.routes.draw do
  # ...
  get  '/list_comments' => 'application#list_comments'
end

```

```
### app/controllers/application_controller.rb ###

class ApplicationController < ActionController::Base

  def list_comments
    comments = Comment.all

    render 'application/list_comments', locals: { comments: comments }
  end

  # ...

end

```

Note, that in our view, `list_comments.html.erb` we are using the method `comment.post`. This is one of the methods we need to build in the Comment model.

```
### app/models/comment.rb ###

class Comment

  # ...

  def self.all
    comment_row_hashes = connection.execute("SELECT * FROM comments")
    comment_row_hashes.map do |comment_row_hash|
      Comment.new(comment_row_hash)
    end
  end

  def post
    Post.find(post_id) # This can be accomplished using an existing method
  end
end

```

Now we also have a nice view for seeing all comments made in our app. In the next chapter, we'll be cleaning up and consolidating the code we currently have in our application.

NOTE: if you previously deleted any posts that had comments, you may run into errors since we are not yet handling the deletion comments when a post is deleted.

# 2.16 A Base Model

## [Inheriting From a Base Model](https://launchschool.com/books/demystifying_rails/read/a_base_model#abasemodel)

Now that we've completed work on our `Comment` model, we've seen tons of duplication between it and our `Post` model. In particular, there are several methods that are *identical* between the two models, such as:

- `#new_record?`
- `#save`
- `.connection` and `#connection`

So let's pull these methods out of these two models and place them inside a new model:

```
### app/models/base_model.rb ###

class BaseModel
  attr_reader :errors

  def new_record?
    @id.blank?
  end

  def save
    return false unless valid?
    if new_record?
      insert
    else
      update
    end
    true
  end

  private

  def self.connection
    db_connection = SQLite3::Database.new 'db/development.sqlite3'
    db_connection.results_as_hash = true
    db_connection
  end

  def connection
    self.class.connection
  end
end

```

This `BaseModel` model class holds the shared functionality of both of our prior models, so we can now completely remove those methods from `Post` and `Comment`, *if* we change both of them to inherit from `BaseModel`:)

```
### app/models/post.rb ###

class Post < BaseModel
  # ...
end

```

```
### app/models/comment.rb ###
class Comment < BaseModel
  # ...
end

```

`BaseModel` nicely consolidates a fair amount of common logic for us, but there a few methods that are *almost* the same in both classes: `.all`, `.find` and `#destroy`

They're not *exactly* the same. Let's take a look at `.all`:

```
### app/models/post.rb ###

class Post

  # ...

  def self.all
    post_hashes = connection.execute("SELECT * FROM posts")
    post_hashes.map do |post_hash|
      Post.new(post_hash)
    end
  end

  # ...

end


```

```
### app/models/comment.rb ###

class Comment

  # ...

  def self.all
    comment_hashes = connection.execute("SELECT * FROM comments")
    comment_hashes.map do |comment_hash|
      Comment.new(comment_hash)
    end
  end

  # ...

end

```

Notice that what these methods are doing is the same, but things are named differently. In particular, the naming differences are as follows:

1. variable names e.g. `post_hash`
2. class names e.g. `Post` in `Post.new`
3. table name strings e.g. `posts` in `SELECT * FROM posts`

We'll address each of these, as we work to move this method into `BaseModel` to be shared by `Post` and `Comment`.

The issue of the variable names is simple: we'll pick something appropriate, but more generic. Taking `post_hashes` as an example, we could instead call the variable `record_hashes`.

```
### app/models/base_model.rb ###

class BaseModel

  # ...

  def self.all
    # rename all the variables...
    record_hashes = connection.execute("SELECT * FROM posts")
    record_hashes.map do |record_hash|
      Post.new(record_hash)
    end
  end

  # ...

end

```

Next, the use of class names with the `Post.new` and `Comment.new` calls are actually syntactically unnecessary. We can omit the classes and call `new` all by itself. The reason for this is that `.all` is a class method. So if we call `new` inside of this *class* method, it will be called on the *class* it lives in.

```
### app/models/base_model.rb ###

class BaseModel

  # ...

  def self.all
    record_hashes = connection.execute("SELECT * FROM posts")
    record_hashes.map do |record_hash|
      new record_hash
    end
  end

  # ...

end

```

And lastly there's the matter of the table names. Inside `Comment`, a query should be made to the `comments`table, and in `Post`, `posts`.

Notice the transformation there?

`Post` goes to `posts` and `Comment` goes to `comments`. It would be nice if our `.all` method could look at the class it lives in and figure out what to do based on the name of that class. Fortunately for us, this is not only common, but also easy in Ruby.

Let's see how we can get from a class (a constant) to the string we want:

```
Post
# => Post

Post.to_s
# => "Post"

Post.to_s.pluralize
# => "Posts"

Post.to_s.pluralize.downcase
# => "posts"

```

Let's give our classes a `.table_name` method to figure out the appropriate table name string and then make use of it inside of `.all`:

```
### app/models/base_model.rb ###

class BaseModel

  # ...

  # a way get the right table name string
  def self.table_name
    to_s.pluralize.downcase
  end

  def self.all
    # use it in our SQL
    record_hashes = connection.execute("SELECT * FROM #{table_name}")
    record_hashes.map do |record_hash|
      new record_hash
    end
  end

  # ...

end

```

It's worth noting that our call got shortened to `to_s.pluralize.downcase` inside of `.table_name`. The reason for this is the same as our shortened call to `new` earlier: inside of a class method `self` is the class.

Based on what we've done with our `.all` class method, we can also extract `.find`, and `#destroy` to the base model as well.

```
class BaseModel

  # ...

  def destroy
    query_string = "DELETE FROM #{self.class.table_name} WHERE #{self.class.table_name}.id = ?"
    connection.execute query_string, id
  end

  def self.find(id)		
    query_string = "SELECT * FROM #{table_name} WHERE #{table_name}.id = ? LIMIT 1"		
    record_hash = connection.execute(query_string, id).first		
    new(record_hash)		
  end

  # ...

end

```

And with that, we can remove `.all`,`#destroy`, `.find` from the `Comment` and `Post` models. Since both classes inherit from `BaseModel`, they will now each make use of this new implementation.

This process of having an object look at itself is called *introspection*. You will see it and its effects littered all throughout Rails.

We've come a long ways, soon it will be time to start implementing Rails conventions in our app. In the next section, we will slowly introduce Rails conventions (magic) that can help make the work we've been doing simpler, easier to read, and more efficient.

# 3. RAILS CORE CONVENTIONS

# 3.1 Overview

Now that we've gone through the process of building our blog app with minimum Rails conventions, we're ready to go back through, make more use of Rails, and understand what it's doing and why.

From here, we'll start to focus more on how different parts of our application are the same, and understand how Rails conventions help simplify application development. It will be much more clear why these conventions exist, as well as why and how Rails helps us address them in the way that it does.

Just about every part of our app will change in this process, but we'll be refactoring our application from the outside in, which means that we'll kick things off with routes.

# 3.2 Routes and Resources

## [Basic Routing Conventions](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#routing_conventions)

Let's take a look at our routes as they are now, using `rake routes`:

```
$ rake routes

       Prefix Verb URI Pattern                                               Controller#Action
   list_posts GET  /list_posts(.:format)                                     application#list_posts
              GET  /show_post/:id(.:format)                                  application#show_post
     new_post GET  /new_post(.:format)                                       application#new_post
  create_post POST /create_post(.:format)                                    application#create_post
              GET  /edit_post/:id(.:format)                                  application#edit_post
              POST /update_post/:id(.:format)                                application#update_post
              POST /delete_post/:id(.:format)                                application#delete_post
              POST /create_comment_for_post/:post_id(.:format)               application#create_comment
              POST /list_posts/:post_id/delete_comment/:comment_id(.:format) application#delete_comment
list_comments GET  /list_comments(.:format)                                  application#list_comments

```

One of the key insights for Rails conventions is that data-centric apps (or CRUDy apps) tend to have very similar ways for letting users interact with the application, which are:

- a page to view a list of something
- view something
- show a form to create a new instance of something
- actually create something
- show a form to edit an instance of something
- actually update something
- delete something

Those seven "interaction patterns" are so common, that Rails provides a strong set of conventions from routing to controllers, views and forms to help make those workflows simpler. We're going to focus on the routing part now.

For routing, the convention is that instead of us having to come up with the URL patterns, Rails recommends that we structure the URLs and corresponding controller actions in the following way:

| Workflow                     | HTTP VERB | PATH            | Controller Action |
| ---------------------------- | --------- | --------------- | ----------------- |
| Show a list of posts         | GET       | /posts          | posts#index       |
| Show a post                  | GET       | /posts/:id      | posts#show        |
| Show the page to create post | GET       | /posts/new      | posts#new         |
| Create a post                | POST      | /posts          | posts#create      |
| Show the page to edit a post | GET       | /posts/:id/edit | posts#edit        |
| Update a post                | PUT/PATCH | /posts/:id      | posts#update      |
| Delete a post                | DELETE    | /posts/:id      | posts#destroy     |

We can change the `post` part of our current routing to follow this convention:

```
# posts
GET  /list_posts        ->   GET       /posts           posts#index
GET  /show_post/:id     ->   GET       /posts/:id       posts#show
GET  /new_post          ->   GET       /posts/new       posts#new
POST /create_post       ->   POST      /posts           posts#create
GET  /edit_post/:id     ->   GET       /posts/:id/edit  posts#edit
POST /update_post/:id   ->   PUT/PATCH /posts/:id       posts#update
POST /delete_post/:id   ->   DELETE    /posts/:id       posts#destroy


```

And in the `routes.rb` file,

```
Rails.application.routes.draw do

  ### posts ###

  get    '/posts'          => 'posts#index'
  get    '/posts/:id'      => 'posts#show'

  get    '/posts/new'      => 'posts#new'
  post   '/posts'   => 'posts#create'

  get    '/posts/:id/edit' => 'posts#edit'
  patch  '/posts/:id'      => 'posts#update'
  put    '/posts/:id'      => 'posts#update'

  delete '/posts/:id'      => 'posts#destroy'

  # comments later..
  ...

end

```

Notice that with this new pattern, there's a lot less verbs in the URL itself, but we're relying on the HTTP verbs (`GET`/`POST`/`PUT`/`PATCH`/`DELETE`) to supply the semantics for otherwise same URL pattern, for example `/posts/:id`.

Note that `PUT` had been used for updating resources until recently, when `PATCH` was determined to be a better semantic match for this action. Since then, Rails has moved to preferring `PATCH`, but allowing both verbs for updates.

Another change we'll see later on is that we will be routing all URLs related to posts to a `PostsController`instead of handling everything in `ApplicationController`. The `PostController`'s action names

- new
- index
- show
- create
- edit
- update
- destroy

are also conventions corresponding to the 7 interaction patterns.

This is the strongest set of conventions that Rails imposes on you as an application developer. We'll ask you to make an effort to memorize it. We'll revisit this plenty of times throughout the book to help you do that as well.

## [Routing For Multiple Resources](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#routingformultipleresources)

Oftentimes we need to have multiple resources present in the URL. For example for our blog app whenever we need to have a route to create a comment, it's very important that we know which post this comment is created on.

We're currently doing this:

```
post 'create_comment_for_post/:post_id' => 'application#create_comment'

```

The Rails convention of a URL with multiple associated resources is to start with the "containing" resource all the way to the "innermost" resource. For example, our routes for comments would change to:

```
post   '/posts/:id/comments' => 'comments#create'
delete '/posts/:post_id/comments/:id' => 'comments#destroy'

get    '/comments'                => 'comments#index'

```

The semantics of those URLs represent: "Create a comment under a specific post" and "delete a comment under a specific post". The last route, "show all comments in the system", doesn't need to be "scoped" under a post, so the URL doesn't have to lead with "/posts".

If we need to have multiple resources in the URL with their IDs, the convention is such that the last resource will use the placeholder `:id` and all the rest will be `:resource_id` such as `:post_id`.

## [Restful](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#restful)

REST stands for "Representational State Transfer". It's a software architecture style and guideline to create scalable web services. REST, as a way to structure web applications, has many facets to it, but let's just look at how it applies to the interface that we use to interact with web apps, the URLs.

To see how REST simplifies the semantics of URLs, let's walk through an example. Let's say we're building an online pizza ordering service. A naïve implementation of the interfaces of the service (URLs) would be:

```
/check_order?order_id=2
/place_new_order
/pizza_details?type=1
/pay_for_my_order?order_id=12
/cancel_order?order_id=3
/expedite_order?order_id=13

```

A RESTful interface design would look like this:

```
GET       /orders/2
POST      /orders
GET       /pizzas/1
POST      /orders/12/payments
DELETE    /orders/3
POST      /orders/13/expeditions
```

You can see, RESTful interfaces center around "nouns" or "resources", removing "verbs" from the interfaces but instead relying on the standardized HTTP verbs (`GET`/`POST`/`PUT`/`DELETE`) to supply CRUD semantics for the actions. Verbs such as `check`, `place`, `cancel` are mapped directly to HTTP verbs of `GET` to retrieve, `POST` to create, and `DELETE` to destroy resource `order`. `pay` and `expedite` are structured as creation (HTTP POST) of sub resources of `payments` and `expeditions` under resource `orders`.

RESTful interfaces standardized web application interaction patterns to make them easier to understand and program against. Because the interfaces are centered around manipulating resources, the responses are much more predictable. An analogy of how the RESTful architecture pattern simplifies interaction with web services would be how the Relational Database and SQL language simplifies data storage. Before Relational Database and SQL, data was typically stored in proprietary systems with specific logic to interact with them, which means, on every project you'd have to learn a different set of instructions to interact with data. Relational Databases and SQL gave a common data structure (data records as rows and columns stored in tables) and a set of common interfaces - four simple verbs of `SELECT`, `INSERT`, `UPDATE` and `DELETE` that can support all types of applications.

Adopting a RESTful interface for your web app will also streamline your application to align with how the backend data is stored in databases, and makes development easier. We'll see that in the following chapters.

## [Resource Notation](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#resourcenotation)

We have talked about Rails' routing conventions, and RESTful URL patterns. Now our `routes.rb` file would look like the following:

```
### config/routes.rb ###

Rails.application.routes.draw do
  ### posts ###

  get    '/posts'          => 'posts#index'
  get    '/posts/:id'      => 'posts#show'
  get    '/posts/new'      => 'posts#new'
  post   '/posts'   => 'posts#create'
  get    '/posts/:id/edit' => 'posts#edit'

  patch  '/posts/:id'      => 'posts#update'
  put    '/posts/:id'      => 'posts#update'

  delete '/posts/:id'      => 'posts#destroy'


  ### comments ###

  get    '/comments'                    => 'comments#index'
  post   '/posts/:post_id/comments'     => 'comments#create'
  delete '/posts/:post_id/comments/:id' => 'comments#destroy'

end

```

In fact, the routes like what we have in the `posts` section are very common, so that Rails provides a special `resources` notation that help generate those for you.

We can simply do:

```
resources :posts

```

This line will automatically generate the 8 lines we had before. Note that for the `update` action, Rails allows both `PUT` and `PATCH` verb, for compatibility reasons.

You can run `bundle exec rake routes` in your command line environment to verify that it generates exactly the same set of routes.

Note that this single line will generate 8 routes. In our case we happen to need all the routes here, but if you only need a subset of the routes, you can define them more explicitly as:

```
resources :posts, only: [:new, :create, :index]

```

This line above would only generate 3 routes for you - type `bundle exec rake routes` to check it out.

## [Nested Resources](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#nestedresources)

Rails also allows us to nest resources to create URL patterns with multiple resources, see below:

```
### config/routes.rb ###

Rails.application.routes.draw do
  resources :posts do
    resources :comments, only: [:create, :destroy]
  end

  resources :comments, only: :index
end

```

Run `bundle exec rake routes` and see the output - it should be the same as what we had before.

## [Path Helpers](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#pathhelpers)

When you run `bundle exec rake routes`, notice the `Prefix` column for some of these routes. These are here to help us know how to use Rails' provided *path helpers* for our routes. We can use these prefixes followed by `_path` in our controllers and views to easily build paths.

For example:

```
posts_path # => '/posts'

post_id = 123
post_comments_path(post_id)
# => '/posts/123/comments'

```

What's the advantage of using URL helpers, rather than hard coding the paths such as `/posts/123/comments` directly in your code? (for example, in your controller action?) The reason you want to use path helpers is that if you want to change the URL patterns in your app, it's a lot easier to use the URL helpers to return a different path - let's look at an example:

```
get '/register', to: 'users#new', as: 'register'

```

When we add the "as" clause to this route, if you run `bundle exec rake routes`, you'll see the `Prefix`column with `register`, and you can use `register_path` to get `/register` the path. Now, if we want to change the path to `/login`, all we have to do is just to:

```
get '/login', to: 'users#new', as: 'register'

```

Now our `register_path` gives us `/login`. We don't have to change our code in the Rails app at all.

## [More Routing Conventions](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#moreroutingconventions)

Before we move on, let's take a quick look at a couple variations of what we've already seen, as well as some other features available to us in Rails routing:

```
### config/routes.rb ###

Rails.application.routes.draw do

  # pointing our homepage (root path) to posts#index
  root to: 'posts#index'

  # `match` & `via:` allow us to define one route and use several HTTP verbs
  # `as:` lets us define the name of the route prefix

  match '/authors/:id' => 'authors#update',
    via: [:put, :patch],
    as:   :update_author
  # update_author  PUT|PATCH /authors/:id(.:format)  authors#update

  resources :posts do
    # define extra params to pass for requests to a route
    get 'popular', on: :collection, action: :index, popular: true
    # popular_posts  GET /posts/popular(.:format)  posts#index {:popular=>true}

    get 'preview', on: :member

    # ...
  end

  # we can even use routes to redirect
  get '/home', to: redirect('/')
end

```

Let's break down all the features listed above one at a time.

- **root:** `root` is used to specify what action maps to "/"(the top-level URL of our site which has no path). The root URL of your website/app is the most commonly used, because of this `root` should be specified at the top of the routes file.

- **match + via:** `match` is used to match URL patterns to one or more routes. We can also specify which HTTP verb may be used for matching to a URL with this pattern. We do this by passing in a hash to the `match` method. The key for this hash is `via`, and the value is an array of HTTP verbs. `match` is a more general purpose form of some more commonly used HTTP routing methods, such as `get`, `post`, and `delete`. It may take all of the same options as those methods, but, compared to those methods, it gives a bit more flexibility.
  For instance, by using `match` we may specify a URL that matches for two different routes, each corresponding to two different HTTP verbs. Normally, doing this would require two commands, instead of one. We can see this from our example above, where we match the URL pattern `'/authors/:id'` to the action `'authors#update'`. We then specify what HTTP verbs may be used to issue the request for that URL with `via: [:put, :patch]`. Always specify an HTTP method when using `match`, not doing so may have negative implications on your application's security.
  `match` presents another option for routing to certain actions in Rails. In general, it is best to stick with the more commonly used `HttpHelpers` methods, such as `get` and `post`.

- **as:** We mentioned a bit earlier that the option `as:` may be used with our route declaration to change the prefix for our URL helpers. This can be used in various ways. We can us `as:` to make our URL helpers better match custom URLs. Another use is to change the current URL path helper to something more intuitive or something that matches up better with the resources within an application.

- **collection route:** See how above we nest our `/popular` route under the `posts` resource. We then use `on: :collection` to specify what part of a resource we are nesting this route under. We have many posts so that is considered a collection. By specifying `on: :collection` we are saying, "Match a URL with path `/posts/popular`." If we didn't add `on: :collection`, Rails will assume that this route corresponds to another resource associated with a single member of our posts collection. In that case our route would become `/posts/:post_id/popular`. We can also specify multiple collection routes by using a block format.

  ```
  collection do
    get 'popular'
  end

  ```

- **passing an extra parameter:** We can specify a default parameter that always gets passed in with our `params` hash when we are matched with certain URLs. There are two ways to specify this; one way is the same way we do above:

  ```
  get 'popular', on: :collection, action: :index, popular: true

  ```

  `popular: true` will be passed to our action that the popular route matches with via the `params` hash. It will have a key of `:popular` and a value of `true`. We can also use more explicit syntax by passing a hash to our route method `get`, where the key is `defaults:` and the value is another hash containing the name of the parameter we want to pass to our action.

  ```
  get 'popular', on: :collection, action: :index, default: { popular: true}

  ```

- **member route:** We can use `on: member` to specify that our route matches a member of a collection. If we use this the dynamic segment will show up as `:id`. A URL helper will also be created as `preview_post`. By specifying this route with `on: member`, we are telling Rails that this is a member of this particular resource. That it isn't just another resource nested under posts, but more closely linked or related to our posts in this application. Multiple member routes may be defined using a block format; this format uses the same syntax as the block format for defining multiple collection routes, just replace `collection` with `member`.

- **redirect:** There is one other concept to talk about that is displayed in our example above, and that is redirection. Rails gives us the capability to redirect from one path to another by using a redirect helper in conjunction with a route. `get '/home', to: redirect('/')`. If someone tries to access the path `/home`, they will immediately be redirected to the root path `/`. This isn't restricted to just one URL path of course; we could also have something like this: `get '/home', to: redirect('/travel')`.

## [Review](https://launchschool.com/books/demystifying_rails/read/routes_and_resources#routingreview)

Rails routes stand in the front of an application. A route interprets an incoming HTTP request and:

- matches a request to a controller action based on the combination of a HTTP verb and the request URL pattern
- captures data in the URL to be available in `params` in controller actions
- Rails encourages developers to use RESTful URL patterns when setting up routes, with conceptualization of manipulating resources with HTTP verbs.
- You can use the `resources` macro to generate RESTful routes very quickly.



# 3.3 Conventional Views and Controller Actions

## [Restful Controller Conventions](https://launchschool.com/books/demystifying_rails/read/conventional_views_and_actions#restfulconventions)

In Rails the RESTful conventions based on resources don't stop with routes. Let's look at how this applies to our controllers.

Following what we specified in the routes, we'll create a `PostsController` and a `CommentsController`, moving the appropriate actions into them, and matching the action names to our new routes. The goal is to organize all the actions related to the `posts` resource in the `PostsController` and all the actions related to the `comments` resource in the `CommentsController`.

In Rails, the controllers are named with the plural form of the resources that they handle along with the name `Controller`, therefore `PostsController` and `CommentsController`. They are stored in the `app/controllers` directory, and the file names should be "snake cased" as `posts_controller.rb` and `comments_controller.rb`.

A typical Rails controller will have a subset of RESTful actions of `index`, `show`, `new`, `edit`, `create`, `update`, and `destroy`. However, you may need non-RESTful actions, for example, you may need a way to publish a post. To do this you can also create a `publish` action in your `PostsController` and route to it manually. However, if you find yourself adding actions such as `create_draft`, `delete_draft`, `update_draft` etc. to the `PostsController`, it's a sign that you should think about having a `DraftsController` instead, with `create`, `delete` and `update` actions.

After this, `ApplicationController` will be empty, but that's actually how it would look in a typical Rails app. These two new controllers will inherit from it and thus from `ActionController::Base`, which is where they get all their Rails magic.

Here is an example of a controller action after this step:

```
class PostsController < ApplicationController
  def show # <- used to be: show_post
    post    = Post.find(params['id'])
    comment = Comment.new

    render 'application/show_post', locals: { post: post, comment: comment }
  end
end

```

## [Rendering Views With Instance Variables](https://launchschool.com/books/demystifying_rails/read/conventional_views_and_actions#renderwithinstancevariables)

If you look at what we have in the controller actions, you can see there's a pattern. We would create a model and use it to render the view templates - for example below:

```
class PostsController < ApplicationController
  def show
    post    = Post.find(params['id'])
    comment = Comment.new

    render 'application/show_post', locals: { post: post, comment: comment }
  end
end

```

This happens so much that Rails allows you to simplify this step with instance variables.

```
class PostsController < ApplicationController
  def show
    @post    = Post.find(params['id'])
    @comment = Comment.new

    render 'application/show_post'
  end
end

```

You have to update the `post` and `comment` variables in the view templates to `@post` and `@comment` as well.

Instance variables are automatically available in view templates, bound to the value that they are assigned to in the controller actions.

This doesn't mean you have to make all the variables in your controller actions instance variables, but for the ones you need in the view templates, make them instance variables and you won't have to manually pass them in anymore.

## [Controller Action and View File Structure](https://launchschool.com/books/demystifying_rails/read/conventional_views_and_actions#actionsandviews)

Currently, our view templates are still located in the `app/views/application` directory, and when we render view templates, we have to explicitly specify where the template is:

```
class PostsController < ApplicationController
  def show
    @post    = Post.find(params['id'])
    @comment = Comment.new

    render 'application/show_post'
  end
end

```

If we move the `show_post.html.erb` view templates to a directory with the same name of the resource - `app/views/posts`, we can change the `render` line to:

```
render 'show_post'

```

Rails will automatically search the `app/views/posts` directory for views related to actions in the `PostsController`.

What we want to do is use the RESTful conventions mentioned earlier. And if we name our view template as `show.html.erb`, we can simplify our controller action further:

```
def show
  @post    = Post.find params['id']
  @comment = Comment.new
end

```

That is, if we don't specify otherwise, Rails will automatically look for a view template in directory `app/views/posts` (matches the controller resource's name) with the name that matches the controller action's name (in this case, `show`). You can still, of course, explicitly tell Rails what view template to render, or set the response header with a redirect.

Let's make it so the rest of our actions in `PostsController` follow RESTful conventions:

```
### app/controllers/posts_controller.rb ###

class PostsController < ApplicationController

  # list_posts -> list -> index
  def index
    @posts = Post.all
  end

  # show_post -> show
  def show
    @post    = Post.find(params['id'])
    @comment = Comment.new
  end

  # new_post -> new
  def new
    @post = Post.new
  end

  # create_post -> create
  def create
    @post = Post.new('author' => params['author'], 'title' => params['title'], 'body' => params['body'])

    if @post.save
      redirect_to posts_path
    else
      render 'new'
    end
  end

  # edit_post -> edit
  def edit
    @post = Post.find(params['id'])
  end

  # update_post -> update
  def update
    @post = Post.find(params['id'])
    @post.set_attributes('author' => params['author'],
                         'title' => params['title'],
                         'body' => params['body'])
    if @post.save
      redirect_to posts_path
    else
      render 'edit'
    end
  end

  # delete_post -> delete -> destroy
  def destroy
    post = Post.find(params['id'])
    post.destroy

    redirect_to posts_path
  end

end

```

Notice now we are also using path helpers to define the redirection paths in the actions.

Next up, our Comments controller:

```
### app/controllers/comments_controller.rb ###

class CommentsController < ApplicationController
  # def list_comments -> list -> index
  def index
    @comments = Comment.all
  end

  # def create_comment -> create
  def create
    @post    = Post.find params['post_id']
    @comment = @post.build_comment('author' => params['author'],
                                   'body' => params['body'])

    if @comment.save
      redirect_to post_path(@post.id)
    else
      render 'posts/show'
    end
  end

  # def delete_comment -> delete -> destroy
  def destroy
    post = Post.find(params['post_id'])
    post.delete_comment(params['id'])

    redirect_to post_path(post.id)
  end
end

```

Once again, it is important to remember to update any views that rely on these newly changed actions. For `CommentsController`, that means we need to jump into our view template, `views/comments/index.html.erb`, and update it so that the `@comments` instance variable is used instead of the local `comments`. This isn't too big of a change, so let's take care of it real quick.

```
<!-- OLD app/views/application/list_comments.html.erb -->

<!-- app/views/comments/index.html.erb -->

<div class="comments">
  <% @comments.each do |comment| %>
  <!-- ^ use `@comments` instead of `comments` -->
    <div class="comment">
      <small class="comment_meta">
        <span class="comment_post_title">
          Comment on
          <strong><%= comment.post.title %></strong>
        </span>

        <span class="comment_author">by <%= comment.author %> -</span>
        <em class="comment_created_at"><%= comment.created_at %></em>
      </small>

      <p class="comment_body"><%= comment.body %></p>
    </div>
    <hr />
  <% end %>
</div>

```

We've covered some important Rails conventions in this chapter related to directory structure and our app's views. These conventions will be used going forward, so be sure to keep them in mind.

# 4. CONTROLLER VERSATILITY

# 4.1 Filters and Indifferent Access

## [Filters](https://launchschool.com/books/demystifying_rails/read/filters_indifferent_access#filters)

Our controllers are quite cleaned up now, but there's still a line that repeats in several actions:

```
@post = Post.find() ...

```

We can instead move this post lookup to filter method and call it before each action that needs it using `before_action`:

```
### app/controllers/posts_controller.rb ###

class PostsController < ApplicationController
  before_action :find_post, only: [:show, :edit, :update, :destroy]

  # ...

  def show
    @comment = Comment.new
  end

  def edit
  end

  def update
    if @post.update_attributes('title' => params['title'], 'author' => params['author'], 'body' => params['body'])
      redirect_to posts_path
    else
      render 'edit'
    end
  end

  def destroy
    @post.destroy
    redirect_to posts_path
  end

  private

  def find_post
    @post = Post.find(params['id'])
  end
end

```

```
### app/controllers/comments_controller.rb ###

class CommentsController < ApplicationController
  before_action :find_post, only: [:create, :destroy]

  # ...

  def create
    @comment = @post.build_comment(
      'body' => params['body'], 'author' => params['author']
    )

    if @comment.save
      redirect_to post_path(@post.id)
    else
      render 'posts/show'
    end
  end

  def destroy
    @post.delete_comment(params['id'])

    redirect_to post_path(@post.id)
  end

  private

  def find_post
    @post = Post.find(params['post_id'])
  end
end

```

If we don't tell it otherwise, `before_action` will call the specified method before *every* action. We don't want to do that, so we specify just the actions we want by passing in an extra argument which is a hash: `{only: [:show, :edit, :update, :destroy]}` so it'll be applied only to those actions. If this filter only applies to one action then we can exclude the array and only pass in a single symbol (e.g `{only: :show}`). We can also pass in the hash with the `except` key with an array of actions to exclude, and apply to all other actions.

You'll also notice that `find_post` is private in both controllers. In Rails, a controller action that's a private method will never be routed to, which is exactly what we want.

Other than `before_action`, Rails also allows you to define `after_action` and `around_action`. They are similar to `before_action` filters. `after_action` will execute code after the specified actions and `around_action` will execute code before and after the specified actions -- a typical use case for it is logging, where you can write to the log when the code execution starts and when it finishes.

## [Indifferent Access](https://launchschool.com/books/demystifying_rails/read/filters_indifferent_access#indifferentaccess)

Notice, that as our app has progressed we have accessed values in our `params` hash in two different ways: with symbols, and strings. Let's take a closer look at this rails feature:

```
# First we'll place a debugger in our index action in the comments controller
class CommentsController < ApplicationController

  # ...

  def index
    binding.pry
    @comments = Comment.all
  end

  # ...
end

```

Next, let's navigate to the comments page. From there we can look around using pry in the terminal.

```
4: def index
=> 5:   binding.pry
6:   @comments = Comment.all
7: end

[1] pry(#<CommentsController>)> params
=> {"controller"=>"comments", "action"=>"index"}
# Since we are accessing a collection, the only parameters by default are the controller name and action name.
# Let's try accessing the action name using our params hash.
[2] pry(#<CommentsController>)> params['action']
=> "index"
[3] pry(#<CommentsController>)> params[:action]
=> "index"

```

Rails gives us the option to access params using either a Symbol or a String. If we check the class of our hash, we'll see what type of data structure gives us this flexibility.

```
[4] pry(#<CommentsController>)> params.class
=> ActionController::Parameters

```

If we go a bit further and check the documentation, we'll see that this class inherits from `ActiveSupport::HashWithIndifferentAccess`. It's that parent class that allows us to access the values in our params hash with either a `String` or a `Symbol`.
Now would be a good time to explain why we've been slowly changing out code to use symbols. Symbols are unique identifiers, they also take up less memory, and are a bit easier to type.
Overall, using symbols to access our params is the preferred method. So, from now on that is what we'll be using. One last thing to do then, would be to go through our comments and posts controllers, and change the `params` access from string to symbol.

```
### app/controllers/posts_controller.rb ###

# ...

private

def find_post
  @post = Post.find(params[:id]) #used to be params['id']
end

### app/controllers/comments_controller.rb ###

def destroy
  @post.delete_comment(params[:id])

  redirect_to post_path(@post.id)
end

```

With that we're done investigating controller filters and parameters. In the next chapter, we'll cover more useful conventions that Rails provides for us. We'll also give a short review of what we've gone over thus far.

# 4.2 More Controller Options

## [Status Codes and Request Formats](https://launchschool.com/books/demystifying_rails/read/more_controller_options#statuscoderequestformats)

Before we move on to changing our views to be used by these new controllers, let's take a look at a couple more things we'll commonly see inside Rails actions:

### Set explicit response header status code

```
def four_oh_four
  # specific HTTP status code for the response
  render plain: '404 Not Found', status: :not_found
  # Fixnums also work:
  # render plain: '404 Not Found', status: 404
end

```

### Respond to multiple request formats

```
def greeting
  # respond differently to different formats...
  respond_to do |format|
    # render one response for HTML requests
    format.html { render inline: "<p>Hi!</p>" }
    # render another for JSON requests
    format.json { render json: {greeting: 'Hi!'} }
  end
end

```

Given a `/greeting` route to this action:

```
$ curl localhost:3000/greeting    
<p>Hi!</p>
$ curl localhost:3000/greeting.html
<p>Hi!</p>
$ curl localhost:3000/greeting.json
{"greeting":"Hi!"}

```

`.html` is assumed, but if the format is `.json` we receive the JSON response defined above; also notice that we define a Ruby hash, but Rails converts this into a JSON string for us.

## [Review](https://launchschool.com/books/demystifying_rails/read/more_controller_options#reviewrailscontrollers)

The job of a controller action is to react to a specific kind of HTTP request, gather the appropriate data, and assemble an appropriate HTTP response. For our application this process has mostly involved fetching DB data and using that data in our ERB view templates to create HTML response bodies.

As far as inspecting incoming requests goes, we mostly made use of `params`, but we actually have access to the entirety of the HTTP request in the `request` object.

And when it comes to setting the response, we've mostly relied on `render` to accomplish this, but we also have a `response` object to more directly interact with the HTTP response we're building to send back to the client.

The reason `render`, `params`, and the rest of these methods are available to us is because our Rails controllers inherit from `ActionController::Base`.

The 7 standard action names for a resource controller are:

- `index`
- `show`
- `new`
- `create`
- `edit`
- `update`
- `destroy`

Following this naming convention allows `resources` calls in your `config/routes.rb` to neatly match up to your controller actions.

And last but not least, don't forget that instance variables (e.g. `@posts`) defined in your action will also be available for use inside the view that the action renders.

If we adhere to some conventions pertaining to directory, filename, and naming, Rails will take care of a lot of things for us automatically.

For more resources on Rails controllers, check out:

- [the Ruby on Rails Guide on controllers](http://guides.rubyonrails.org/action_controller_overview.html)
- [the API documentation for ActionController::Base](http://api.rubyonrails.org/classes/ActionController/Base.html)

# 5. HELPERS AND FORMS

# 5.1 The link_to Helper

## [link_to](https://launchschool.com/books/demystifying_rails/read/link_to#link_to)

Let's now make adjustments for the `index` view template for posts.

```
<!-- app/views/posts/index.html.erb -->

<html>
  <body>
    <div class="posts">
      <% @posts.each do |post| %>
      <!-- use `@posts` instead of `posts` -->
        <div class="post">
          <h2 class="title">

            <%= link_to post.title, post_path(post.id) %>
          </h2>

          <small class="meta">
            <span class="author">by <%= post.author %> -</span>
            <em class="created_at"><%= post.created_at %></em>

            <%= link_to 'Edit', edit_post_path(post.id) %>

            <form method="post" action="/posts/<%= post.id %>" style='display: inline'>
              <input type="submit" value="Delete" />
            </form>

          </small>
        </div>
        <hr />
      <% end %>
    </div>

    <%= link_to 'New Post', new_post_path %>
  </body>
</html>

```

We have moved the view template to its conventional location,changed its name, utilized our instance variables from the controller, and we have also used the link helper `link_to`.

`link_to` works like this:

```
<%= link_to 'Link Text', url_or_path %>

```

We're also making use of our route-defined path helper methods in combination with `link_to`. For example, here we make the link to `posts/show` with:

```
<%= link_to post.title, post_path(post.id) %>

```

## [More About Helpers](https://launchschool.com/books/demystifying_rails/read/moreabouthelpers)

`link_to` is a Rails built in helper that helps generate an anchor tag. To understand what it does and how it actually works, let's build a similar helper ourselves.

Helpers, or more specifically, view helpers are methods that generate HTML snippets to be placed in a view. To get a feel for what this means, let's take a look at a Rails-provided helper we've already seen:

```
<%= link_to 'Back to Posts', posts_path %>

<!-- this generates the HTML... -->

<a href="/posts">Back to Posts</a>

```

`link_to` is a helper method provided by Rails, but we can easily define a simple version of this helper ourselves. We'll name it `my_link_to` and place it in `app/helpers/application_helper.rb` - methods defined here will automatically become helpers and can be used in views.

```
### app/helpers/application_helper.rb ###

module ApplicationHelper
  def my_link_to(text, href)
    "<a href='#{href}'>#{text}</a>".html_safe
  end
end

```

Our `my_link_to` method is incredibly simple. It returns an `<a>` tag string, with the `href` and element contents (link text) set by the parameters. We also call `html_safe` on the string to prevent Rails from escaping this string.

So let's try using our `my_link_to` method in our `posts/show` view now:

```
<!-- app/views/posts/show.html.erb -->

<!-- ... -->

<div class="post">
  <!-- ... -->
</div>

<%= my_link_to 'Back to Posts', posts_path %>
<!-- generates... -->
<!-- <a href="/posts">Back to Posts</a> -->

```

This was a pretty simple helper method to start with, but through it we can clearly see the purpose of helpers are to build HTML strings.

# 5.2 Nonstandard HTTP Verbs

Let's look at how we delete a post. Currently we have:

```
<form method="post" action="/posts/<%= post.id %>" style='display: inline'>
  <input type="submit" value="Delete" />
</form>

```

This issues an HTTP `POST`. Since we changed to RESTful routes, we need to trigger a `DELETE` HTTP verb here. However, since browsers natively only support HTTP `GET` and `POST` methods, we have to do something a bit tricky to use HTTP `POST` to fake `PUT`/`PATCH`/`DELETE` methods.

```
<form method="post" action="/posts/<%= post.id %>" style='display: inline'>
  <input name= "_method" type="hidden" value="delete">
  <input type="submit" value="Delete" />
</form>

```

On the server side, Rails is able to examine the "_method" value in the `params`to restore the semantics of the HTTP request.

Take a look at your server log to make sure Rails interprets this as an HTTP `DELETE` and also use a debugger to see it's routed to the `destroy` action of the PostsController.

# 5.3 Form Helpers

## [CSRF](https://launchschool.com/books/demystifying_rails/read/form_helpers#csrf)

In this chapter we'll be talking about forms and form helpers. The first one we'll be introducing is `form_tag`, but before we talk about the `form_tag` helper, let's first talk about the various reasons to use this helper.

CSRF or Cross-Site Request Forgery is a type of attack on an application. CSRF utilizes malicious code hidden in one application to affect the data in another application. For instance, consider a link written by a hacker, and in that link some sort of call to our application API is hidden within. Malicious code like this can sometimes be found within the attributes of image or link tags.

Here's an example what was mentioned above:

```
<a href="http://example.com" name="example" onclick="www.our_app/posts/1/delete">...</a>

```

If such a link was clicked, that html event of `onclick` would fire off. The value in `onclick` would get added to our cookies. If we were still logged into our app when we clicked the above link, then that cookie would be sent to our application, and verified with our current session id. Clicking the link above could then delete a post on our application without the user even realizing it.

### Preventing CSRF

So, how do we prevent such an attack on our application. Rails does this with the use of an `authenticity_token`. This token is a random string stored in our session. Every time a javascript or html based request is made, it is checked for an authenticity token. If the token sent with the request from a form does not match the one stored in our application's session, then an exception will be thrown.

We can add this authenticity token to our session with one simple line, added to our application controller.

```
protect_from_forgery with: :exception

```

Let's start by enabling CSRF protection. We'll add the line of ruby code listed above to our Application Controller.

```
class ApplicationController < ActionController::Base
  # Prevent CSRF attacks by raising an exception.
  # For APIs, you may want to use :null_session instead.
  protect_from_forgery with: :exception

  # ...
end

```

To test out this CSRF protection, we'll use our form for creating a new post. If this works as expected then we shouldn't be able to make a new post without that authenticity token within our form. First we'll need to make a new RESTful view for creating a new post; we can move the code from our `new_post` view to this file. Don't forget to change the local variable `post` to the instance variable that we are passing in from our `PostsController`, `@post`.

```
<!-- app/views/posts/new.html.erb -->
<html>
  <body>
    <!-- ... -->

    <form method="post" action="/posts">

      <label for="title">Title</label>
      <input id="title" name="title" type="text" value="<%= @post.title %>"/>
      <br /> <br />

      <label for="body">Body</label>
      <textarea id="body" name="body"><%= @post.body %></textarea>
      <br /> <br />

      <label for="author">Author</label>
      <input id="author" name="author" type="text" value="<%= @post.author %>"/>
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

    <!-- ... -->
  </body>
</html>

```

Let's see what happens when we try to create a post:

```
Started POST "/posts" for ::1 at 2016-04-13 15:13:37 -0700
Processing by PostsController#create as HTML
  Parameters: {"title"=>"Another Post", "body"=>"Test", "author"=>"Missy"}
Can't verify CSRF token authenticity
Completed 422 Unprocessable Entity in 1ms (ActiveRecord: 0.0ms)

```

This occurs because we've turned on checks for CSRF authenticity tokens, but we haven't included one in our form. Let's do that now:

```
<!-- app/views/posts/new.html.erb -->

<html>
  <body>
    <!-- ... -->

    <form method="post" action="/posts">

      <label for="title">Title</label>
      <input name="authenticity_token" type="hidden" value="<%= form_authenticity_token %>">
      <input id="title" name="title" type="text" value="<%= @post.title %>"/>
      <br /> <br />

      <label for="body">Body</label>
      <textarea id="body" name="body"><%= @post.body %></textarea>
      <br /> <br />

      <label for="author">Author</label>
      <input id="author" name="author" type="text" value="<%= @post.author %>"/>
      <br /> <br />

      <input type="submit" value="Create Post" />

    </form>

    <!-- ... -->
  </body>
</html>

```

We set a hidden input element with a name of `authenticity_token` and a value that is set by the `form_authenticity_token` method. This method looks at the token saved in our session and returns it for use here.
With the code above, our form works, and this part of our code is now protected from a CSRF attack.

## [form_tag](https://launchschool.com/books/demystifying_rails/read/form_helpers#formtag)

One problem with our method above is that we'll have to remember to include this hidden input tag in all of our forms. Rails provides a form helper that gives us a bit of a shortcut. The form helper, `form_tag` generates an HTML form for us. If CSRF protection is enabled, then that hidden input is automatically added to our form. `form_tag` helper also gives us a few options for customizing our form in an effective and intuitive way.

Here is the code we would need to make the form used above with a `form_tag`helper:

```
<html>
  <body>
    <!-- ... -->

    <%= form_tag url_for(action: 'create'), method: "post" do %>

      <%= label_tag 'Title' %>
      <%= text_field_tag 'title', @post.title %>
      <br /> <br />

      <%= label_tag 'Body' %>
      <%= text_area_tag 'body', @post.body %>
      <br /> <br />

      <%= label_tag 'Author' %>
      <%= text_field_tag 'author', @post.author %>
      <br /> <br />

      <%= submit_tag "Create Post" %>

    <% end %>

    <!-- ... -->
  </body>
</html>

```

### Options for form_tag

There are a lot of changes here, so let's go through them one by one. First, notice that we start with the syntax:

`<%= form_tag url_for(action: 'create'), method: "post" do %>`

We have `form_tag`, this is a form helper method that creates a form tag for us and allows us to specify various options for our form. To make sure that our form is submitted to the correct action, we can specify a url and the HTTP method(verb) used to submit this form.

We're using a Rails method to build up the URL we want the form to submit to. This method is `url_for`. It gives us several options to create a URL. One option is to specify only the action, as we do above: by doing so any other missing values from our URL are filled in with values from the current request.
The current request for making a new post would have a URL of `/posts`. This lets Rails know which controller this URL will be for. From there, specifying the action in `url_for` let's us further refine the URL based on our routes.

In this case, `url_for(action: 'create') #=> '/posts'`. This URL is pretty short, we could write it manually. But you could imagine that using `url_for`would be necessary for submitting forms to resources nested deep within our application.

We've previously also used URL path helpers to generate URLs. We'll be using these for our forms going forward, along with `url_for`.

The next part of our `form_tag` utilizes the option `method`. This option shows us one other situation where using `form_tag` versus writing out a form manually can be quite helpful. HTML forms can only use the `GET` and `POST`HTTP verbs. For some actions, we don't want to use `GET or POST`. If we want to delete a post we would want to use the `DELETE` HTTP verb.

Recall, that to do this we used a Rails convention where we had to set a hidden input field in our form. Then, we made sure to have a `method` attribute for that input tag of `"delete"`; this allowed us to submit a form with the `DELETE` HTTP verb. The `method` option does just that for us, depending on what value we set for the `method` option. If we use `method="delete"` in the `form_tag` above, then a hidden input field with method attribute `delete` will be automatically added to our form.

### form_tag Helpers

Let's continue examining what makes up our `form_tag` and its helpers. For each tag we want to create, we have a helper method to dynamically make it.

- `label_tag` → `<label></label>`
- `text_field_tag` → `<input type='text'>`
- `submit_tag` → `<input type='submit'>`

Here is a list of the arguments we've used with these helpers and what each argument is used for:

- The first argument of the text field and text area helpers sets the `name` and `id` attributes for the tag we are creating. The second argument sets what the content/value that will be used for that tag.
- `label_tag` takes one argument that sets the `for` attribute, as well as the content for that label.
- `submit_tag` takes one argument that sets the value of the submit tag.

All of the form helpers listed above as well as many other form helpers can also be passed a list of options. We don't need those options at the moment though, so if you're curious about that information, you can find more on it in the [relevant documentation](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html).

## [Using form_tag for the Rest of Our Forms](https://launchschool.com/books/demystifying_rails/read/form_helpers#usingformtag)

We've gotten a look at `form_tag` and its field helper methods as well, the `tag`methods. Let's put that knowledge to good use. In this section, we'll convert the rest of our views that use plain HTML forms to use Rails `form_tag`. Here are some things to keep in mind when making the conversion.

Make sure that views:

- are moved to their conventional directory locations
- are renamed to their conventional names
- links and forms are fixed to fit the new routes
- forms use a hidden input with `name="_method"` to specify the correct HTTP verb when necessary

Recall that so far we have adjusted the view templates for:

- posts: index and new
- comments: index

```
<!-- app/views/posts/index.html.erb -->

<%= form_tag post_path(post.id), method: "delete" , style: "display: inline" do %>
  <%= submit_tag "Delete" %>
<% end %>

```

```
<!-- app/views/posts/show.html.erb -->

<%= form_tag post_comment_path(@post.id, comment.id), method: "delete" do %>
  <%= submit_tag "Delete Comment" %>
<% end %>

<%= form_tag post_comments_path(@post.id) do %>

  <%= label_tag 'Comment' %>
  <%= text_area_tag 'body', @comment.body %>
  <br /> <br />

  <%= label_tag 'Name' %>
  <%= text_field_tag 'author', @comment.author %>
  <br /> <br />

  <%= submit_tag "Add Comment" %>
<% end %>

```

```
<!-- app/views/posts/edit.html.erb -->

<%= form_tag url_for(action: 'update'), method: "patch" do %>

  <%= label_tag 'Title' %>
  <%= text_field_tag 'title', @post.title %>
  <br /> <br />

  <%= label_tag 'Body' %>
  <%= text_area_tag 'body', @post.body %>
  <br /> <br />

  <% label_tag 'Author' %>
  <%= text_field_tag 'author', @post.author %>
  <br /> <br />

  <%= submit_tag 'Update Post' %>

<% end %>

```

## [Parameter Naming Conventions and Mass Assignment](https://launchschool.com/books/demystifying_rails/read/form_helpers#namingmassassignment)

Lets go over what parameters from our form look like when we receive them in the controller. For this step, we'll put a `binding.pry` in our `create` action for the `PostsController`.

```
def create
  binding.pry
  @post = Post.new('author' => params[:author],
                   'title' => params[:title],
                   'body' => params[:body])

  if @post.save
    redirect_to posts_path
  else
    render 'new'
  end
end

```

Next, we'll fill out our new post form and submit it. If we look at our `params`hash, we'll see that author, title, and body each show up as individual keys at the highest level of this hash, along with the controller and action keys.

```
[1] pry(#<PostsController>)> params
=> {"utf8"=>"✓",
 "authenticity_token"=>"wYCWFeQFIDOLk4tkFd+gHUhLHlw5od3UL+RKcjKrXInSNDPZ+SfzYQrO3KW6TU0zwGuh36q4db1rfJzu+k/Kuw==",
 "title"=>"A New Post",
 "body"=>"Hello World",
 "author"=>"Alice Cooper",
 "commit"=>"Create Post",
 "controller"=>"posts",
 "action"=>"create"}

```

This may be fine with our current application. But if our form was more complicated or if we were passing more information to our controller, then we would maybe want further organization of the data related to our new post. Rails provides a way to organize related parameters into a sub-hash. To do this we need to change the name attribute for the form data that we want grouped together.

Here is what our form currently looks like:

```
<!-- app/views/posts/new.html.erb -->

<html>
  <body>
    <!-- ... -->

    <%= form_tag url_for(action: 'create'), method: "post"  do %>
      <%= label_tag 'Title' %>
      <%= text_field_tag 'title', @post.title %>

      <br /> <br />

      <%= label_tag 'Body' %>
      <%= text_area_tag 'body', @post.body %>

      <br /> <br />

      <%= label_tag 'Author' %>

      <%= text_field_tag 'author', @post.author %>

      <br /> <br />

      <%= submit_tag "Create Post" %>
    <% end %>

    <!-- ... -->
  </body>
</html>

```

Now, let's change the form so that parameters related to our post are grouped together in our params hash.

```
<!-- app/views/posts/new.html.erb -->

<html>
  <body>
    <!-- ... -->

    <%= form_tag url_for(action: 'create'), method: "post"  do %>
      <%= label_tag 'Title' %>   
      <%= text_field_tag 'post[title]', @post.title %>

      <br /> <br />

      <%= label_tag 'Body' %>
      <%= text_area_tag 'post[body]', @post.body %>

      <br /> <br />

      <%= label_tag 'Author' %>

      <%= text_field_tag 'post[author]', @post.author %>

      <br /> <br />

      <%= submit_tag "Create Post" %>
    <% end %>

    <!-- ... -->
  </body>
</html>

```

Our params hash now looks like:

```
[1] pry(#<PostsController>)> params
=> {"utf8"=>"✓",
 "authenticity_token"=>"PSdbhGz0Cb2ic0PO2GwmNs9+3rSxLp0wNAVR6OHvGdIuk/5Icdba7yMuFA93/ssYR15hNyI3NVlwnYd0KQuP4A==",
 "post"=>{"title"=>"A New Post", "body"=>"Hello World", "author"=>"Alice Cooper"},
 "commit"=>"Create Post",
 "controller"=>"posts",
 "action"=>"create"}

```

Notice that everything is a bit easier to read. Any fields related to our post are in a nested hash. While we're at it, lets also make this change to our form used to create a new comment. Make sure that the file for showing a post and creating a comment follow Rails conventions.

- `views/application/show_post.html.erb` -> `views/posts/show.html.erb`
- `comment` -> `@comment`
- `post` -> `@post`
- `comments` -> `@post.commments`

```
<!-- app/views/posts/show.html.erb -->

<html>
  <body>
    <!-- ... -->
    <!-- We're using a url helper to post data to the correct action. -->

    <%= form_tag post_comments_path(@post.id) do %>
      <%= label_tag 'Comment' %>
      <%= text_area_tag 'comment[body]', @comment.body %>
      <br /> <br />

      <%= label_tag 'Author' %>
      <%= text_field_tag 'comment[author]', @comment.author %>
      <br /> <br />

      <%= submit_tag 'Add Comment' %>
    <% end %>

    <!-- ... -->
  </body>
</html>

```

Here is what our params hash looks like when we apply this rails parameter convention for creating a new comment:

```
[1] pry(#<CommentsController>)> params
=> {"utf8"=>"✓",
 "authenticity_token"=>"cz2+kiA91zb8sEdxotc6U7JCPTQ40ITM2M26oRQ2TYlgiRtePR8EZH3tELANRdd9OmKCt6vJLKWcVWw93NLbuw==",
 "comment"=>{"body"=>"New Comment", "author"=>"Number 5"},
 "commit"=>"Add Comment",
 "controller"=>"comments",
 "action"=>"create",
 "post_id"=>"23"}
 
```

If you are following along, there is something that you should have noticed after these changes. Our create actions don't seem to work. If we take a closer look at our actions we may notice the issue:

```
# /app/controllers/posts_controller.rb

# ...

def create
  @post = Post.new('author' => params[:author],
                   'title' => params[:title],
                   'body' => params[:body])

  if @post.save
    redirect_to posts_path
  else
    render 'new'
  end
end

# ...

```

```
# /app/controllers/comments_controller.rb

# ...

def create
  @comment = @post.build_comment(
    'body' => params[:body], 'author' => params[:author]
  )

  if comment.save
    # redirect for success
    redirect_to posts_path(@post.id)
  else
    # render form again with errors for failure
    render 'posts/show'
  end
end

```

Recall, that by changing the `name` attributes in our forms, we changed the structure of our parameters hash. So, if we want to access values related to a post, we use `params[:post]`, and if we want to access values related to a comment, we'll have to use `params[:comment]`.

Using the examples above we have:

```
params[:post] #=> {"title"=>"A New Post", "body"=>"Hello World", "author"=>"Alice Cooper"}

```

```
params[:comment] #=> {"body"=>"New Comment", "author"=>"Number 5"}

```

This structure for our parameters gives us a shorter, more concise syntax for object creation. Let's fix those create actions by using the correct calls to `params`.

```
# /app/controllers/posts_controller.rb

# ...

def create
  @post = Post.new(params[:post])

  if @post.save
    redirect_to posts_path
  else
    render 'new'
  end
end

# ...

```

```
# /app/controllers/comments_controller.rb

# ...

def create
  @comment = @post.build_comment(params[:comment])

  if comment.save
    # redirect for success
    redirect_to posts_path(@post.id)
  else
    # render form again with errors for failure
    render 'posts/show'
  end
end

```

Make sure to also apply these changes to the forms we've been using in our app. Also, make sure you update their corresponding controller actions as well.

There is a name for when we use a group of values to update an object. It's called *mass assignment* . By accessing a single k-v pair from our `params` hash, we're able to assign many attributes at once. While convenient, mass assignment also opens up our application to a security risk. How do we know that only the parameters we want assigned are updated for our object.
By using mass assignment, we're blindly allowing any number of parameters for assignment, as long as they are included in our form. Rails does give us a way to safeguard our data when using mass assignment, which we'll learn about later on in this book.

# 6. CUSTOM FORMS

# 6.1 Building Our Own Form Helpers

## [my_form_tag](https://launchschool.com/books/demystifying_rails/read/building_our_own_form_helpers#myformtag)

We'll build our own form helpers to better understand what the form helpers do. We'll start with our own version of `form_tag` - we'll call it `my_form_tag`instead.

To build a `my_form_tag` helper, we'll need to be aware of a number of different things:

1. the path the `<form>` should submit to
2. the HTTP verb the `<form>` uses
3. the `name` attribute of each field in the `<form>`
4. populating each field with a value, if needed

The first two have to do with the `<form>` itself, and the last two have to do with the fields. We'll define a `my_form_tag` helper to build the `<form>`, and then define helpers like `my_text_area_tag` to build the fields.

But before we define the helpers, let's see what we want our view to look like. For this exercise, we'll replace the new comment `<form>` in `posts/show` with a call to our yet-undefined `my_form_tag` method.

```
<!-- app/views/posts/show.html.erb -->
<html>
  <body>
    <!-- ... -->

    <div class="post">

      <!-- ... -->

      <div class="comments">

        <!-- ... -->

        <%= my_form_tag post_comments_path(@post.id) do %>

          <% unless @comment.new_record? %>
            <%= my_hidden_field_tag '_method', 'patch' %>
          <% end %>

          <%= my_label_tag 'Comment' %>
          <%= my_text_area_tag 'comment[body]', @comment.body %>
          <br /><br />

          <%= my_label_tag 'Author' %>
          <%= my_text_field_tag 'comment[author]', @comment.author %>
          <br /><br />

          <%= my_submit_tag %>
        <% end %>

      </div>
    </div>

    <!-- ... -->
  </body>
</html>

```

We must define the fields inside the `<form>` using a block, because this is the way we're able to nest HTML using ERB and helper methods. That is, this block allows us to nest the fields inside of the `<form>` element, which really just means placing the HTML strings for the fields before the closing `</form>` tag. We'll see how we accomplish that in just a minute.

Inside the block, we conditionally create a hidden field to set the HTTP method for the form to `PATCH` if we're updating the record:

```
<% unless @comment.new_record? %>
  <%= my_hidden_field_tag '_method', 'patch' %>
<% end %>

```

Our versions of input, textarea, and label helpers are all functionally the same as the ones that come with Rails. Notice, that it also reads in almost an identical manner as if we were using the form helpers provided by Rails.
Now that we know what helpers we'll be using, let's implement them:

```
### app/helpers/application_helper.rb ###

module ApplicationHelper

  # ...

  def my_hidden_field_tag(name, value)
    "<input name='#{name}' value='#{value}' type='hidden' />".html_safe
  end

  def my_label_tag(txt)
    "<label>#{txt}</label>".html_safe
  end

  def my_text_field_tag(name, value)
    "<input name='#{name}' value='#{value}' type='text' />".html_safe
  end

  def my_text_area_tag(name, value)
    "<textarea name='#{name}' value='#{value}'></textarea>".html_safe
  end

  def my_submit_tag(txt="Submit")
    "<input type='submit' value='#{txt}'>".html_safe
  end

  def my_form_tag(path, &block)
    attrs  = "method='post' action='#{path}'"
    fields = capture(&block)
    "<form #{attrs}> #{my_authenticity_token_field} #{fields} </form>".html_safe
  end

  def my_authenticity_token_field
    my_hidden_field_tag('authenticity_token', form_authenticity_token)
  end
end

```

We see all of our `_tag` helpers for our labels and fields, which each return the proper HTML element with their attributes and contents set by the parameters. And then there's `my_form_tag`:

```
def my_form_tag(path, &block)
  attrs  = "method='post' action='#{path}'"
  fields = capture(&block)
    "<form #{attrs}> #{my_authenticity_token_field} #{fields} </form>".html_safe
end

```

There's also attribute setting being done here, but it's worth noting how the block is handled here.

The `&` in front of `&block` is used to capture a block as a named parameter. This is syntactically necessary, because if we didn't include the `&` in front of the parameter, Ruby would think this was another non-block parameter.

Blocks are usually called with `yield` or `block.call`, but there's something a little different about this block: it's ERB. Because it's ERB, we have to handle it a little differently, executing it instead with the Rails-provided `capture` method. `capture` allows us to execute the ERB block, assign the HTML string returned to a variable, and place that where we want it inside of our `<form>` string.

If we were to execute the block normally, like this:

```
def my_form_tag(path, &block)
  attrs  = "method='post' action='#{path}'"
  fields = block.call # <- calling the block normally
  "<form #{attrs}> #{my_authenticity_token_field} #{fields} </form>".html_safe
end

```

We end up with something like this:

```
<!-- ... -->

<label>Comment:</label>
<textarea name='comment[body]' value=''></textarea>

<label>Your Name:</label>
<input name='comment[author]' value='' type='text' />

<input type='submit' value='Submit'>

<!-- ^ Only the authenticity token field makes it into the <form>! -->

<form method='post' action='/posts/1/comments'>
  <input name="authenticity_token" value="" type="hidden">
</form>

<!-- ... -->

```

This happens because executing the ERB block results in its return being placed immediately into the output HTML when the call occurs. In our helper above, this call occurs before our `my_form_tag` return, so the fields are output before the `<form>`. Not what we want! So we instead use `capture` to trap the block's return value in a variable, and then place it in the `<form>` string where it belongs.

So the `capture` implementation will give us a working `<form>`, just like we had before, but we've actually reinvented the wheel a bit here, since Rails already provides all of these methods, and they take the exact same parameters.

Our own helper now works just like Rails' `form_tag` helper.

This all reads pretty nice, but we're still working a little too hard. For instance, we're stuck calculating: the path for the `<form>`, the `name` attribute values for the fields, and whether or not we need a hidden field to make a `PATCH` request for an update. And this is all taking place in our view. It would be nice to push this logic somewhere else. But, for now we'll hold off on doing that, as it will require the use of `ActiveRecord` objects.

# 6.2 Unobtrusive Scripting

## [Write a Dynamic Form With link_to](https://launchschool.com/books/demystifying_rails/read/unobtrusive_scripting#dynamicform)

Deleting a post or a comment currently needs a form so that we can use the `_method` trick to trigger a `DELETE` action. Rails provides a way that we can do this simply with the `link_to` helper.

For example:

```
<%= link_to 'Delete', post_path(post.id), method: :delete, data: { confirm: "Are you sure want to delete '#{post.title}'?"} %>

```

This will render into:

```
<a data-confirm="Are you sure want to delete 'post_title_here'?" rel="nofollow" data-method="delete" href="..." >Delete</a>

```

Rails monitors the `data-method` and `data-confirm` data attributes for special processing with a Javascript library that it ships with, the `jquery-rails` library. This behavior is called "unobtrusive scripting". It is named "unobtrusive scripting" because the Javascript code that facilitates this is not intertwined with the markup.

In this case, it'll trigger a HTTP `DELETE` after the user confirms a dialog box on the UI.

For more about Unobtrusive Scripting behaviors, see:

<https://github.com/rails/jquery-ujs/wiki/Unobtrusive-scripting-support-for-jQuery>

## [Javascript Include Tag and CSRF meta tags](https://launchschool.com/books/demystifying_rails/read/unobtrusive_scripting#javascriptincludetag)

If we want our `link_to` to work as a dynamic form, we need to enable Javascript on our page. To do that we'll need a `<script>` tag for our application's main Javascript page. Rails gives us a useful helper for creating this script tag when we need it.

```
<head>
  <title>Blog App</title>
  <%= javascript_include_tag 'application' %>
  <%= csrf_meta_tags %>
</head>

```

Notice that we also have `csrf_meta_tags` . This dynamically creates a csrf token for our dynamic form to use. Our `link_to` dynamic form is using Javascript, and when using Javascript to send a form, we will need to include this csrf meta token. Rails requires it by default.

# 7. MORE VIEW CONVIENS

# 7.1 Render Responsive Views

## [Layouts](https://launchschool.com/books/demystifying_rails/read/render_responsive_views#href)

So far, each of our views has had an `<html>` tag and a `<body>` tag. By using a "layout", we can extract common code that is used for several view templates to one location. We do this by creating an `application.html.erb` file.

```
<!-- app/views/layouts/application.html.erb -->

<!DOCTYPE html>
<html>
  <head>
    <title>BlogApp</title>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
    <%= csrf_meta_tags %>
  </head>

  <body>

    <%= yield %>

  </body>
</html>

```

"Common code" usually includes the `<html>`, `<head>`, and `<body>` tags.

Notice that we also have HTML tag helpers from the chapter on unobtrusive scripting. We make sure to include those in our layout as well. These should be included so any additions or changes to CSS and Javascript will be included in our application.

You can define and use other layouts, but `layouts/application.html.erb` is the default, so that's what we create here. Rails will actually generate a layout similar to the one above whenever you run `$ rails new` to generate a new app.

`yield` identifies where content from our view should be inserted into the enclosing layout. Typically, you'll have a layout for most view templates, so as to cut out code duplication.

## [Partials](https://launchschool.com/books/demystifying_rails/read/render_responsive_views#partials)

We've shown that it is possible to insert code from a view template into a layout, and then render that layout and view together to the user. We can even go a step further, it is possible to move certain HTML/ERB code that is reused in various view templates to one location. This is called a partial view template or just "partial". Let's move some redundant HTML/ERB code to a partial. The convention we want to follow is to create a partial in the same view folder as the resource it is used for. So, if this is a partial for posts, then we'll save the partial view template file under the `views/posts` folder. One other convention that is important to remember is that partial view templates start with an underscore. We do this to help differentiate partials from other view templates. First, let's first take a look at the two view templates we are working with, `posts/edit.html.erb` and `posts/new.html.erb`.

```
<!-- app/views/posts/new.html.erb -->

<div class="errors">
  <% @post.errors.each do |attribute, error| %>
    <p class="error" style="color: orange">
      <%= attribute %>: <%= error %>
    </p>
  <% end%>
</div>


<%= form_tag posts_path, method: "post" do %>
  <%= label_tag 'title' %>
  <%= text_field_tag 'post[title]', @post.title %>

  <br /> <br />

  <%= label_tag 'body' %>
  <%= text_area_tag 'post[body]', @post.body %>

  <br /> <br />

  <%= label_tag 'author' %>
  <%= text_field_tag 'post[author]', @post.author %>

  <br /> <br />

  <%= submit_tag "Create Post" %>
<% end %>

```

```
<!-- app/views/posts/edit.html.erb -->

<div class="errors">
  <% @post.errors.each do |attribute, error| %>
    <p class="error" style="color: orange">
      <%= attribute %>: <%= error %>
    </p>
  <% end%>
</div>


<%= form_tag url_for(action: 'update'), method: "patch" do %>

  <%= label_tag 'Title' %>
  <%= text_field_tag 'post[title]', @post.title %>

  <br /> <br />

  <%= label_tag 'Body' %>
  <%= text_area_tag 'post[body]', @post.body %>

  <br /> <br />

  <% label_tag 'Author' %>
  <%= text_field_tag 'post[author]', @post.author %>

  <br /> <br />

  <%= submit_tag 'Update Post' %>

<% end %>

<br />
<%= my_link_to 'Back to Post', posts_path %>

```

Let's look at what similarities these two views contain:

1. They both have the same error messages
2. They both use fields for their form that are *nearly* the same.

We can address each of these commonalities by extracting them to their own partial views. Let's tackle the one for error messages first.

```
<!-- app/views/posts/edit.html.erb -->

<%= render "errors" %>

<!-- ... -->

```

```
<!-- app/views/posts/new.html.erb -->

<%= render "errors" %>

<!-- ... -->

```

```
<!-- app/views/posts/_errors.html.erb -->

<div class="errors">
  <% @post.errors.each do |attribute, error| %>
    <p class="error" style="color: orange">
      <%= attribute %>: <%= error %>
    </p>
  <% end%>
</div>

```

By using the code above, we're able to move any error related code to one place. Then, we can use that code in any view template within the same directory as `_errors` by calling `render "errors"`. Now, if we wanted to make our error partial usable for multiple resources, we could store it in a separate directory. Let's say we do that, and now `_errors.html.erb` is now in a directory called `shared`. If we want to still use that partial in `new` and `edit` view template for posts, then we'll have to provide the relative path to that file, starting from the `views` directory: `<%= render "shared/errors" %>`.

The above partial would then look like this:

```
<!-- app/views/shared/_errors.html.erb -->

<div class="errors">
  <% obj.errors.each do |attribute, error| %>
    <p class="error" style="color: orange">
      <%= attribute %>: <%= error %>
    </p>
  <% end%>
</div>

```

And when we call `render` for that errors partial, we'll have to specify what the local `obj` is:

```
<!-- For Posts -->

<%= render 'shared/errors', obj: @post %>

<!-- For Comments -->

<%= render 'shared/errors', obj: @comment %>

```

Next, let's work on view template similarity number 2, the fields for our two forms. Note, that our two forms for `edit.html.erb` and `new.html.erb` go to different paths. For the time being we'll only extract the fields for these forms to a partial. But, later on we'll be able to extract the entire form.

```
<!-- app/views/posts/new.html.erb -->

<%= render "shared/errors", obj: @post %>

<%= form_tag posts_path, method: "post" do %>
  <%= render "form_fields" %>
<% end %>
<br />
<%= link_to "Back to Posts", posts_path %>

```

```
<!-- app/views/posts/edit.html.erb -->

<%= render "shared/errors", obj: @post %>

<%= form_tag url_for(action: 'update'), method: "patch" do %>
  <%= render "form_fields" %>
<% end %>
<br />
<%= my_link_to 'Back to Post', posts_path %>

```

```
<!-- app/views/posts/_form_fields.html.erb -->

<%= label_tag 'Title' %>
<%= text_field_tag 'post[title]', @post.title %>
<br /> <br />

<%= label_tag 'Body' %>
<%= text_area_tag 'post[body]', @post.body %>
<br /> <br />

<%= label_tag 'Author' %>
<%= text_field_tag 'post[author]', @post.author %>
<br /> <br />

<%= submit_tag "#{@post.new_record? ? 'Create' : 'Update'} Post" %>

```

So far we have seen that we can render partials by calling `<%= render "path/to/partial" %>`. There is actually one other way to call `render`, and that is by passing a hash to `render`.

```
<%= render { partial: 'shared/errors' } %>

```

The code above would give us the same result as calling: `<%= render 'shared/errors' %>`

## [Options for using layout method](https://launchschool.com/books/demystifying_rails/read/optionsforlayout)

In the controller, we may specify a different layout (instead of the default one, `application.html.erb`) for our views. It's also possible to set a specific layout for all actions in a controller. We do this by using the layout macro:

```
layout 'layout_file_name', options

```

As an example, what if we wanted to use a different layout for all actions in our`PostsController`. First, we would have to create a new layout file and store it under the `views/layouts` folder. Then, all that needs to be done is to specify that file in `PostsController`.

```
class PostsController < ApplicationController
  # ...
  layout 'file_name'


  # ...
end

```

Pretty useful. But we may want to only use this new layout file in certain actions, not all of them. We have two ways to go about that. One way would be to specify which actions to apply the layout to via our options hash. Code such as the following is perfectly valid:

```
layout 'file_name', only: :index

```

Or, if we want specify more than one action:

```
layout 'file_name' only: [:index, :new]

```

If we don't want to specify which actions for this layout but which ones we don't want, we may use `except:` instead of `only:`:

```
layout 'file_name' except: [:edit, :create, :update, :destroy]

```

Finally, we may also specify the layout in the action itself. Recall that in these actions we have been specifying which view template to render, e.g. `render :edit`. `render` can take a layout key as part of its options hash.

```
render :edit, layout: 'file_name'

```

## [Flash Messages](https://launchschool.com/books/demystifying_rails/read/render_responsive_views#flashmessages)

In Rails, the flash message is a convenient way to show messages on a page, typically as confirmation or error message after user actions.

Let's add flash messages to our app for the `create` action of the `CommentsController`:

```
def create
  @comment = @post.build_comment(params[:comment])

  if @comment.save
    redirect_to post_path(@post.id)
  else
    render 'posts/show'
  end
end

```

Becomes:

```
def create
  @comment = @post.build_comment(params[:comment])

  if @comment.save
    flash[:success] = "You have successfully created the comment."
    redirect_to post_path(@post.id)
  else
    flash.now[:error] = "Comment couldn't be created. Please check the errors."
    render 'posts/show'
  end
end

```

You can consider flash as a hash that can store messages which can then be pulled out in the next HTTP request. This is why we added `flash[:success]`before the redirection. Flash messages are automatically deleted after the next request.

If we want the messages to be available to the **current** request, we can use the `flash.now` hash instead, like we did for the error path.

We'll also need to put the flash messages in the view. In fact we're going to put the snippet to handle flash messages in a partial and render it from the `application` layout.

Let's do that now.

```
<!-- app/views/layouts/application.html.erb -->

<!DOCTYPE html>
<html>
  <head>
    <title>BlogApp</title>
    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track' => true %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
    <%= csrf_meta_tags %>
  </head>
  <body>
    <%= render 'layouts/messages' %>
    <%= yield %>

  </body>
</html>

<!-- app/views/layouts/_messages.html.erb -->

<% flash.each do |name, message| %>
  <% if message.is_a? String %>
    <p style="color: <%= name == 'success' ? 'green' : 'red' %>">
      <%= message %>
    </p>
  <% end %>
<% end %>

```

There, now we may include a flash message in our view templates. This is a feature that is available throughout our entire app. That call to `<%= render 'layouts/messages' %>` makes it all possible.

# 8. ACTIVE RECORE MODELS AND DATABASE MANAGEMENT

# 8.1 Active Record Models

## [Models](https://launchschool.com/books/demystifying_rails/read/models#models)

With our routes, controllers, and views all converted to use Rails' conventions and conveniences, we have one last big piece to change: our models.

What we're going to do next feels like a bit of magic - we're just going to let our models `Post` and `Comment` inherit from `ActiveRecord::Base` and remove all the code:

```
### app/models/comment.rb ###

class Comment < ActiveRecord::Base
end

```

```
### app/models/post.rb ###

class Post < ActiveRecord::Base
end

```

That's right, we can get rid of the entirety of the content of our classes now that we're inheriting from `ActiveRecord::Base`. Remember how we were sharing some functionality between our models using `BaseModel` earlier? Well, `ActiveRecord::Base` provides *all* of the functionality we've been using thus far, using (mostly) the same method names.

We went through this process mostly to show you what `ActiveRecord::Base`actually does under the hood - you can always check your original models to understand what Rails provides to you as a framework that you don't have to implement yourself.

When we use Active Record based models, and we follow the convention like below:

| Model Name  | File Location and Name      | Database Table Name |
| ----------- | --------------------------- | ------------------- |
| Post        | app/models/post.rb          | posts               |
| MoutainBike | app/models/mountain_bike.rb | mountain_bikes      |

Rails will automatically map a model to a database table if you follow this naming convention. Inheriting from `ActiveRecord::Base` will allow you to access data records in the database directly through your models:

```
### find a post, read its attributes ###

post = Post.find 1
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT 1  [["id", 1]]
#=> #<Post:0x00000007360e78
# id: 1,
# title: "Blog 1",
# body: "Lorem ipsum dolor sit amet.",
# author: "Brad",
# created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

post.title
# => "Blog 1"
post.body
# => "Lorem ipsum dolor sit amet."
post.created_at
# => Sun, 07 Dec 2014 00:00:00 UTC +00:00
post.title="My Blog"
# => "My Blog"
post.save
# => true

```

## [Validations](https://launchschool.com/books/demystifying_rails/read/models#validations)

We have our Active Record based models set up, but they don't have validations ready yet:

```
### check validity of empty post ###

post = Post.new
# => #<Post:0x0000000252fbc8
#  id: nil,
#  title: nil,
#  body: nil,
#  author: nil,
#  created_at: nil>
post.valid?
# => true
post.errors
# => #<ActiveModel::Errors:0x00000003664bc8
#  @base=
#   #<Post:0x0000000252fbc8
#    id: nil,
#    title: nil,
#    body: nil,
#    author: nil,
#    created_at: nil>,
#  @messages={}>

```

Rails allows you to define validations in a very easy way:

```
### app/models/post.rb ###

class Post < ActiveRecord::Base
  validates_presence_of :title, :body, :author
end

```

```
### app/models/comment.rb ###

class Comment < ActiveRecord::Base
  validates_presence_of :body, :author
end

```

Let's take a look how this works:

```
### Post validation ###

post = Post.new
# => #<Post:0x000000074be7e8
#  id: nil,
#  title: nil,
#  body: nil,
#  author: nil,
#  created_at: nil>

post.valid?
# => false

post.errors.messages
# => {:title=>["can't be blank"],
#  :body=>["can't be blank"],
#  :author=>["can't be blank"]}


### Comment validation ###

comment = Comment.new
# => #<Comment:0x00000007676dd8
#  id: nil,
#  body: nil,
#  author: nil,
#  post_id: nil,
#  created_at: nil>

comment.valid?
# => false

comment.errors.messages
# => {:body=>["can't be blank"], :author=>["can't be blank"]}

```

Validation impacts on a record's persistence:

```
post = Post.new
# => #<Post:0x00000005aaece0
#  id: nil,
#  title: nil,
#  body: nil,
#  author: nil,
#  created_at: nil,
#  updated_at: nil>

post.valid?
# => false

# as expected, this invalid instance returns false here
post.save
#    (0.3ms)  begin transaction
#    (0.0ms)  rollback transaction
# => false

# but if we call the "bang" (!) version of the method...
post.save!
#    (0.2ms)  begin transaction
#    (0.0ms)  rollback transaction
# ActiveRecord::RecordInvalid: Validation failed: Title can't be blank, Body can't be blank, Author can't be blank

# it throws an error. this convention repeats throughout Rails.

# with `.create` for example...
Post.create({title:'foo', body:'bar', author:'baz'})
#    (0.1ms)  begin transaction
#   SQL (0.2ms)  INSERT INTO "posts" ("title", "body", "author", "created_at", "updated_at") VALUES (?, ?, ?, ?, ?)  [["title", "foo"], ["body", "bar"], ["author", "baz"], ["created_at", "2015-01-31 10:59:33.931414"], ["updated_at", "2015-01-31 10:59:33.931414"]]
#    (13.1ms)  commit transaction
# => #<Post:0x0000000537a870 id: 4, title: "foo", body: "bar", author: "baz", ...>

Post.create({})
#   (0.1ms)  begin transaction
#   (0.1ms)  rollback transaction
#=> #<Post:0x0000000553c820
# id: nil,
# title: nil,
# body: nil,
# author: nil,
# created_at: nil,
# updated_at: nil>

# with create, we always get back a `Post` object

# but with invalid attributes sent to `.create!`
Post.create!({})
#    (0.1ms)  begin transaction
#    (0.1ms)  rollback transaction
# ActiveRecord::RecordInvalid: Validation failed: Title can't be blank, Body can't be blank, Author can't be blank

# we get an error instead

```

Other than `validate_presence_of`, there are other validations that you can use with Rails. Here are some other validations that you may often use:

- validates_uniqueness_of
- validates_numericality_of
- validates_length_of

There other way of defining validations as well. We may use the `validates`method, and with that method we can specify which attributes to validates and what to validate. For instance,

```
validates :name, presence: true

```

validates the name attribute by checking that it is present before saving. When using validations in this form, we pass the types of validation as k-v pairs of a hash.

```
validates :name, presence: true, uniqueness: true

```

By adding `uniqueness: true`, we may also check that a name is unique along with checking that it is present in our model.
There's even more to learn about validations, but we won't be covering it here. For more information on validations, check out the Rails documentation and the [Rails guides page](http://guides.rubyonrails.org/active_record_validations.html).

## [Callbacks](https://launchschool.com/books/demystifying_rails/read/models#callbacks)

Callbacks are methods that "hook" into the lifecycle of an Active Record object. They may be used to run logic whenever a object is created, saved, updated, deleted, validated, or loaded from the database. Here is a list of available callbacks that may be used in Rails:

- `after_initialize`
- `after_find`
- `after_touch`
- `before_validation`, `after_validation`
- `before_save`, `around_save`, `after_save`
- `before_create`, `around_create`, `after_create`
- `before_update`, `around_update`, `after_update`,
- `before_destroy`, `around_destroy`, `after_destroy`
- `after_commit`
- `after_rollback`

For more information on Active Record callbacks, you may refer to the [Ruby on Rails API page](http://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html) or the Rails guide on [Active Record Callbacks](http://guides.rubyonrails.org/active_record_callbacks.html).

# 8.2 Active Recored Associations

## [Defining Associations](https://launchschool.com/books/demystifying_rails/read/associations#definingassociations)

Let's see if our associations are still there?

```
post = Post.find 1
#   Post Load (0.4ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
# => #<Post:0x00000003e1b470
#  id: 1,
#  title: "Blog 1",
#  body: "Lorem ipsum dolor sit amet.",
#  author: "Brad",
#  created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

post.comments
# NoMethodError: undefined method `comments' for #<Post:0x00000003e1b470>

```

In Rails, defining associations is quite simple:

```
### app/models/post.rb ###

class Post < ActiveRecord::Base
  ....

  has_many :comments
end

```

```
### app/models/comment.rb ###

class Comment < ActiveRecord::Base
  ....

  belongs_to :post
end

```

These `has_many` and `belong_to` calls work just as expected, and return us to the functionality we had before:

```
### post comments ###

post = Post.find 1
#   Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT 1  [["id", 1]]
# => #<Post:0x000000085a9e68
#  id: 1,
#  title: "Blog 1",
#  body: "Lorem ipsum dolor sit amet.",
#  author: "Brad",
#  created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

post.comments
  Comment Load (0.1ms)  SELECT "comments".* FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 1]]
# => [#<Comment:0x00000004865b88
#   id: 1,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "Matz",
#   post_id: 1,
#   created_at: Tue, 09 Dec 2014 00:00:00 UTC +00:00>,
#  #<Comment:0x00000004865318
#   id: 2,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "DHH",
#   post_id: 1,
#   created_at: Tue, 09 Dec 2014 00:00:00 UTC +00:00>,
#  #<Comment:0x00000004864b20
#   id: 3,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "tenderlove",
#   post_id: 1,
#   created_at: Tue, 09 Dec 2014 00:00:00 UTC +00:00>]

### post for a comment ###

comment = Comment.find 1
#  Comment Load (0.2ms)  SELECT  "comments".* FROM "comments" WHERE "comments"."id" = ? LIMIT 1  [["id", 1]]
#=> #<Comment:0x0000000513fd30
# id: 1,
# body: "Lorem ipsum dolor sit amet.",
# author: "Matz",
# post_id: 1,
# created_at: Tue, 09 Dec 2014 00:00:00 UTC +00:00>

comment.post
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT 1  [["id", 1]]
#=> #<Post:0x000000052ab7c8
# id: 1,
# title: "Blog 1",
# body: "Lorem ipsum dolor sit amet.",
# author: "Brad",
# created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

```

So again, ActiveRecord will handle our associations for us, but we have to define how our models are related.

How did this happen?

- When you have a `has_many :comments` line in your model, Rails will define a method `comments` for you, very similar to the `comments` method we had before, to retrieve all the comments related to the post.
- Similarly when you have a `belongs_to :post` line in your `Comment` model, Rails will define the method `post` to fetch you the post related to that comment.

More about Active Record Associations:

- Associations may be separated into three main types. One-to-One(1:1), One-To-Many(1:M), and Many-to-Many(M:M). In this book, we have mainly dealt with a One-To-Many association. In a blog that has posts and comments, a post may have many comments, but a comment cannot have many posts. So, that is a one(post) to many(comments) association.
  If we could write the same comment on multiple posts at once, then we would have many to many association. And if we could only post at most a single comment on a single post, then we would be dealing with a one to one association.
- After you define the associations, Rails defines for you many convenient methods that you can use. See here: <http://api.rubyonrails.org/classes/ActiveRecord/Associations/ClassMethods.html>

Here are some more examples with associations:

```
post = Post.first
#   Post Load (0.3ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
# => #<Post:0x00000004cbefe0 ...>

post.comments.count
#    (0.5ms)  SELECT COUNT(*) FROM "comments" WHERE "comments"."post_id" = ?  [["post_id", 1]]
# => 3

post.comments.exists?
#   Comment Exists (0.4ms)  SELECT  1 AS one FROM "comments" WHERE "comments"."post_id" = ? LIMIT 1  [["post_id", 1]]
# => true

Post.last.comments.exists?
#   Post Load (0.4ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" DESC LIMIT 1
#   Comment Exists (0.2ms)  SELECT  1 AS one FROM "comments" WHERE "comments"."post_id" = ? LIMIT 1  [["post_id", 5]]
# => false

# and for posts, we can instantiate new comments like so:
comment = post.comments.build
# => #<Comment:0x0000000483f730
#  id: nil,
#  body: nil,
#  author: nil,
#  post_id: 1,
#  created_at: nil,
#  updated_at: nil>

# notice that the `post_id` was properly set
comment.post_id
# => 1

# and we can reference back from the post
comment.post
# => #<Post:0x00000004cbefe0
#  id: 1,
#  title: "Blog 1",
#  body: "Lorem ipsum dolor sit amet.",
#  author: "Kevin",
#  created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00,
#  updated_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

# and just as there is `.build`, there is also
# `.create` and `.create!` methods for associations
post.comments.create!({})
#    (0.1ms)  begin transaction
#    (0.0ms)  rollback transaction
# ActiveRecord::RecordInvalid: Validation failed: Body can't be blank, Author can't be blank

```

## [Associations in Controllers](https://launchschool.com/books/demystifying_rails/read/associations#associationscontrollers)

Now, let's use Active Record association methods in the two controllers we've been working with, `PostsController` and `CommentsController`. We'll want to use these methods going forward instead of the custom ones that we have made so far.

Listed below are the actions we need to change so that our code works with Active Record.

```
# app/controllers/posts_controller OLD

def update
  @post.set_attributes(params[:post])
  if @post.save
    redirect_to posts_path
  else
    render 'edit'
  end
end

# app/controllers/posts_controller NEW

def update
  if @post.update_attributes(params[:post])
    redirect_to posts_path
  else
    render 'edit'
  end
end

```

There aren't too many changes needed in the `PostsController`.`set_attributes` becomes the Active Record method, `update_attributes`. This method works in the same manner, taking a hash of attributes we wish to change, and updating the current object accordingly. The difference is that a call to `save` isn't needed. `update_attributes` sets the attributes and saves the changes to the database all in one command.

```
# app/controllers/comments_controller OLD

def create
  @comment = @post.build_comment(params[:comment])
  if @comment.save
    # redirect for success
    flash[:success] = "You have successfully created the comment."
    redirect_to post_path(@post.id)
  else
    # render form again with errors for failure
    flash.now[:error] = "Comment couldn't be created. Please check the errors."
    render 'posts/show'
  end
end

def destroy
  @post.delete_comment(params[:id])

  redirect_to post_path(@post.id)
end

# app/controllers/comments_controller NEW

def create
  @comment = @post.comments.build(params[:comment])
  if @comment.save
    # redirect for success
    flash[:success] = "You have successfully created the comment."
    redirect_to post_path(@post)
  else
    # render form again with errors for failure
    flash.now[:error] = "Comment couldn't be created. Please check the errors."
    render 'posts/show'
  end
end

def destroy
  @post.comments.delete(params[:id])

  redirect_to post_path(@post)
end

```

There's a bit more work to be done on the `CommentsController`. For the `create` action we have to change `@post.build_comment` to `@post.comments.build`. They both take the same argument, but `build_comment` isn't a method that exists in Rails. What we use above is the Active Record associations method, `build`, which allows us to create a new Active Record object of the same type as the collection it is called on(`Comment`in this case).

We perform a similar change in the `destroy` action. The Active Record method, `delete` takes the same arguments as our `delete_comment` method. The difference between the two is that we have to call `delete` on a collection of `comments`, and then supply the id(s) for the comment(s) we wish to delete from the database.

One final thing to notice is that we're now only passing in the model object `@post`, we're not passing in its id to our path helpers. Rails allows us to write this shorter code. If we only pass in the Active Record model, then Rails will inspect it, determine its id and add that to the URL we wish to navigate to. This allows our path helper to accurately navigate to the correct post page when after we create and destroy a comment.

# 8.3Strong Parameters

Our new Active Record models behave *mostly* the same as before, but with a couple of exceptions.

## [Handling params](https://launchschool.com/books/demystifying_rails/read/strong_parameters#handlingparams)

One glaring issue is that if we try to create a post right now, we get this:

```
ActiveModel::ForbiddenAttributesError in PostsController#create

```

This is because Active Record models distrust `params` by default. There are security reasons for this, but we obviously want to allow some `params` to be used, so we'll have to specify which ones to permit in our post controller:

```
### app/controllers/posts_controller.rb ###

class PostsController < ApplicationController

  # ...

  def create
    @post = Post.new(post_params)

    # ...
  end

  def update
    if @post.update_attributes(post_params)
      # ...
    end
  end

private

  # ...

  def post_params
    params.require(:post).permit(:title, :body, :author)
  end
end

```

Here we just create a `post_params` private helper method and use it to grab the params we want. We then use it in the calls to our `Post` model in the `create` and `update` actions.

The `params.require(:post)` call makes sure that there is something at `params[:post]`. Subsequently, `.permit(...)` grabs the pairs out of that `params[:post]` hash that we want and allows them to be passed to `Post`.

A similar `params` method will be needed in the comments controller. Be sure to add that in as well so that your app works as intended. Additionally, you will need to change your create action for `comments_controller.rb`

```
def create
  @comment = @post.comments.build(comment_params)
  if @comment.save
    # ...
  else
    @post.reload.comments
    # ...
  end
end

```

When comment validation fails, even though the comment is not saved in the database, it is still being associated with the current post in memory. This will raise an exception when rendering the `show.html.erb` because of its dependency on `comment.id` where our invalid comment will have an id of `nil`. Because of the way we wrote our code, we are grabbing all the comments associated with the current post in memory rather than directly from the database. To solve this, we need to add `@post.reload.comments` during comment validation failures to make sure our current post is synced with the database.

## [More Resources](https://launchschool.com/books/demystifying_rails/read/strong_parameters#moreresources)

For more on these topics, check out:

- [The Ruby on Rails Guide on Strong Parameters](http://guides.rubyonrails.org/action_controller_overview.html#strong-parameters)
- [The Ruby on Rails Guide on Active Record associations](http://guides.rubyonrails.org/association_basics.html#detailed-association-reference)

# 8.4 Querying the Database

Let's dive a little deeper into ActiveRecord and see how we can find and search for records:

```
### Lookups ###

# find the "first" `Post`
# notice the ORDER BY and LIMIT in the generated SQL
Post.first
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1
#=> #<Post:0x000000059f3378
# id: 1,
# title: "Blog 1",
# body: "Lorem ipsum dolor sit amet.",
# author: "Kevin",
# created_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00,
# updated_at: Sun, 07 Dec 2014 00:00:00 UTC +00:00>

# some similar methods...

Post.second
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" ASC LIMIT 1 OFFSET 1
#=> #<Post:0x00000005a8b100 id: 2, ...

Post.last
#  Post Load (0.4ms)  SELECT  "posts".* FROM "posts"  ORDER BY "posts"."id" DESC LIMIT 1
#=> #<Post:0x00000005ae99f8 id: 3, ...

# we can even get counts
Post.count
#  (0.1ms)  SELECT COUNT(*) FROM "posts"
# => 3


# at this point we're familiar with the idea of `.find`
Post.find 1
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT 1  [["id", 1]]
#=> #<Post:0x00000005b86f50 id: 1, ...

# but with Active Record, we can also look up by several ids at once
Post.find [1,2]
#  Post Load (0.4ms)  SELECT "posts".* FROM "posts" WHERE "posts"."id" IN (1, 2)
#=> [#<Post:0x00000005bd8558 id: 1, ...>,
# #<Post:0x00000005bd83f0 id: 2, ...>]


# we're also familiar with `.where`
Post.where(author: 'Brad')
#  Post Load (0.3ms)  SELECT "posts".* FROM "posts" WHERE "posts"."author" = ?  [["author", "Brad"]]
#=> [#<Post:0x0000000207b528 ... author: "Brad", ...

# but we can also use special finders like this
Post.find_by_author 'Brad'
#  Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."author" = ? LIMIT 1  [["author", "Brad"]]
#=> #<Post:0x00000005c6ee68 ... author: "Brad", ...

### ActiveRecord_Relation ###

# it's important to note what `.where` really gives us
Post.where(author: 'Brad').class
# => Post::ActiveRecord_Relation

# this ActiveRecord_Relation lets us chain calls together

# for example, if we wanted, for some reason,
# the first three comments ordered by author,
# we could chain `.author` and `.limit` calls
Comment.order(:author).limit(3)
#  Comment Load (0.2ms)  SELECT  "comments".* FROM "comments"  ORDER BY "comments"."author" ASC LIMIT 3
# => [#<Comment:0x00000005f84f58
#   id: 2,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "DHH",
#   post_id: 1,
#   created_at: Thu, 11 Dec 2014 00:00:00 UTC +00:00,
#   updated_at: Thu, 11 Dec 2014 00:00:00 UTC +00:00>,
#  #<Comment:0x00000005f84df0
#   id: 5,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "DHH",
#   post_id: 2,
#   created_at: Sun, 14 Dec 2014 00:00:00 UTC +00:00,
#   updated_at: Sun, 14 Dec 2014 00:00:00 UTC +00:00>,
#  #<Comment:0x00000005f84c88
#   id: 7,
#   body: "Lorem ipsum dolor sit amet.",
#   author: "DHH",
#   post_id: 3,
#   created_at: Tue, 16 Dec 2014 00:00:00 UTC +00:00,
#   updated_at: Tue, 16 Dec 2014 00:00:00 UTC +00:00>]

# this is possible because each of these methods is...
Comment.order(:author).limit(3).class
# => Comment::ActiveRecord_Relation

# but when we also iterate over these objects as if they were arrays
Comment.order(:author).limit(3).map {|comment|
  [comment.author, comment.created_at]
}
#  Comment Load (0.9ms)  SELECT  "comments".* FROM "comments"  ORDER BY "comments"."author" ASC LIMIT 3
#=> [["DHH", Thu, 11 Dec 2014 00:00:00 UTC +00:00],
# ["DHH", Sun, 14 Dec 2014 00:00:00 UTC +00:00],
# ["DHH", Tue, 16 Dec 2014 00:00:00 UTC +00:00]]

# the chaining of these calls basically builds up a query
# and the SQL is generated and executed upon something like
# one of the following methods being called on the object:
#
# .first
# .last
# .all
# .each
#
# which is why our `.map` above works as we'd expect it to

```

For more resources on `ActiveRecord` models, validations, associations, and more:

- [the Ruby on Rails Guide on ActiveRecord basics](http://guides.rubyonrails.org/active_record_basics.html)
- [the Ruby on Rails Guide on ActiveRecord querying](http://guides.rubyonrails.org/active_record_querying.html)
- [the Ruby on Rails Guide on ActiveRecord validations](http://guides.rubyonrails.org/active_record_validations.html)
- [the Ruby on Rails Guide on ActiveRecord associations](http://guides.rubyonrails.org/association_basics.html)
- [the API documentation for ActiveRecord::Base](http://api.rubyonrails.org/classes/ActiveRecord/Base.html)

[NEXT:  THE FORM_FOR HELPER ](https://launchschool.com/books/demystifying_rails/read/form_for_helper)

# 8.5 The form_for Helper

## [Patterns in Forms](https://launchschool.com/books/demystifying_rails/read/form_for_helper#repeatedpatterns)

Rails forms follow very specific conventions. If we reexamine the resources that we've been working with so far, we'll see a repeated pattern.

Whenever we use a form to `POST` new data to the DB, our URL is of the form `/resources`. That means that if we want to use a form to create a new resource, we would `POST` to a URL like: `/comments`.

If we need to update a resource, we have to specify which type of resource we wish to update (e.g. comments or posts). And we also have to specify which item out of this collection of resources we want to update via the id number.

An example of a URL for `PATCH`ing our data (updating it), would then look like: `/comments/1`. Keep this in mind while we move forward.

So far we've been working with `form_tag` to dynamically create our HTML forms used in our Rails app. There is another type of form helper that can be quite useful when working with Active Record model resources in our application. This form helper is called `form_for`.

## [form_for](https://launchschool.com/books/demystifying_rails/read/form_for_helper#formfor)

The form helper `form_for` is very similar to `form_tag`. The difference here is that the method signature doesn't require a URL. When we use `form_tag`, we need to specify which action we want to submit data to, and to do that we specify a URL string with `url_for`. `form_for` does this for us, all we need to do is pass a certain type of model, and `form_for` generates the correct URL for us by using `url_for` behind the scenes. Let's convert our new post form to use `form_for` instead of `form_tag`:

```
<!-- views/posts/new.html.erb -->

<!-- ... -->

<%= render 'form' %>

<!-- ... -->

```

There are definitely some differences in the code above when compared to what we currently have set up. We'll have to update the form fields partial to get all of this to work. Before, we only included our `form_fields` in that partial, this was because we were using `form_tag`, with `form_for` we may include the entire form. We'll be renaming our partial to `_form.html.erb`.

```
<!-- views/posts/_form.html.erb -->

<%= form_for @post do |f| %>

  <%= f.label 'Title' %>
  <%= f.text_field :title %>
  <br /> <br />

  <%= f.label 'Body' %>
  <%= f.text_area :body %>
  <br /> <br />

  <%= f.label 'Author' %>
  <%= f.text_field :author %>
  <br /> <br />

  <%= submit_tag "#{@post.new_record? ? 'Create' : 'Update'} Post" %>

<% end %>

```

Notice how there is now a block parameter `f`. That is a `FormBuilder` object. It allows us to specify form helpers in a more condensed manner. `form_for`knows that we are using the `Post` Active Record object stored in `@post`. All we need to do for each form helper is specify the method we wish to call on `@post`. For instance, let's consider the code, `<%= f.text_field :title %>`. This gets turned into the HTML code:

```
<input type="text" name="post[title]" id="post_title">

```

And if `post.title` does contain a value, then that will show up as well in the `value` attribute, the above code would become:

```
<input type="text" name="post[title]" id="post_title" value="text value here">

```

This feature is especially useful when certain validations fail and the page gets re-rendered. In that case the value will remain filled in, just as if value had been set to `@post.title` directly.

### url_for and form_for

We've mentioned that `form_for` uses `url_for` behind the scenes to determine which action to route to. Rails can do this when supplied with an Active Record object in conjunction with `url_for`. Let's take a deeper look at how this really works using the rails console.

```
$ bundle exec rails c

```

```
# include the helpers in order to have access to `url_for`
include Rails.application.routes.url_helpers

# set host in default_url_options:
default_url_options[:host] = "localhost:3000"

# A new Post record
post = Post.new
url_for(post)
# => "http://localhost/posts"

# An existing Post record
post = Post.first
url_for(post)
# => "http://localhost/posts/1"

# A new comment on an existing Post
post = Post.first
comment = Comment.new
url_for([post,comment])
# => http://localhost/posts/1/comments


# An existing comment on a Post
post = Post.first
comment = post.comments.second
url_for([post,comment])
#=> "http://localhost/posts/1/comments/2"

```

`form_for` takes the same type of arguments as `url_for`. If we want a form related to a new `Post` or an existing one. We directly pass in a `Post` object as the first argument to `form_for`. That will get passed to `url_for` behind the scenes and a valid URL to the correct action will get generated for our form.

### Moving pages with form_tag to form_for

Now that we've shown what `form_for` can do, the next logical step would be to update all our `form_tag`s to `form_for`. As long as we have an Active Record model to work with, using `form_for` makes a bit more sense than `form_tag`. It does more for us with less code. Below are the remaining forms that we can now move to `form_for`.

```
<!-- app/views/posts/show.html.erb -->


<!-- form used to delete a comment -->
<%= form_for [@post, comment], method: "delete" do %>
  <%= submit_tag "Delete Comment" %>
<% end %>

<!-- form used to create a comment -->
<%= form_for [@post, @comment] do |f| %>
  <%= f.label 'Comment' %>
  <%= f.text_area :body %>
  <br /><br />
  <%= f.label :author %>
  <%= f.text_field :author %>
  <br /><br />
  <%= f.submit %>
<% end %>

```

```
<!-- app/views/posts/edit.html.erb -->

<%= render "shared/errors", obj: @post %>

<%= render 'form' %>

<br />
<%= my_link_to 'Back to Post', posts_path %>

```

See how we're using the form partial now? Rails does a bit of work for us in that we may use the same partial for both new posts and existing posts. If `@post` is a new `Post` object, then the HTTP verb is set appropriately to `POST`. If `@post`is an existing object, then Rails injects a hidden input tag with a method attribute into the form, and that input tag will have a method of `update`. That will let Rails know to set the HTTP verb to `PATCH`. Setting the HTTP verb correctly is key to sending the form data to the correct URL.

## [Our Own form_for](https://launchschool.com/books/demystifying_rails/read/form_for_helper#ourownformfor)

Similar to how we created a `my_form_tag` method, let's now make a `my_form_for` method. Putting this together will help us understand how form helpers really work. We really only need to convert one of our forms to see how these form helpers are working. The comments creation form seems like a good choice, so let's go with that one.

```
<!-- app/views/posts/show.html.erb -->

<%= my_form_for [@post, @comment] do |f| %>
  <%= f.my_label 'Comment' %>
  <%= f.my_text_area :body %>

  <%= f.my_label 'Your Name' %>
  <%= f.my_text_field :author %>

  <%= f.my_submit %>
<% end %>

```

Here, we don't figure out a path and pass it in to the form helper, we pass the array of objects instead. Remember that when we have nested routes, we have to pass in two models. In this case, the first model object helps us identify which post we want. The second model object helps us identify which comment out of all the comments is related to that one post. The ids of each model are inserted into the URL so that we can navigate to the correct page.

Next, let's create those custom form helpers we use above. This can be done by defining them in the `ApplicationHelper` file.

```
### app/helpers/application_helper.rb ###

module ApplicationHelper

  # ...

  def my_form_for(records, &block)
    # grab the record we're building the form for
    # either the lone record OR last record of the array
    @record = records.is_a?(Array) ? records.last : records
    # it's critically important that this is set as an
    # instance variable, as this is how we get at the record
    # later for e.g. the field values

    # here we use `capture` again, this time passing `self`
    # as the context for the block to be executed in. this
    # `self` will be the view, and is necessary so that the
    # @record will be accessible for the later calls
    fields = capture(self, &block)

    # tack on the hidden `_method` field if needed
    unless @record.new_record?
      fields += my_hidden_field_tag('_method', 'patch')
    end

    # build the path string, then the <form>
    path  = url_for(records)
    attrs = "method='post' action='#{path}'"
    "<form #{attrs}> #{my_authenticity_token_field} #{fields} </form>".html_safe
  end

  def my_label(text)
    my_label_tag(text)
  end

  # method to build name attr values
  # w/ format: "record_class_name[attr_name]"
  def name_for(record, attr_name)
    record_class_name = record.class.to_s.underscore
    "#{record_class_name}[#{attr_name}]"
  end

  def my_text_area(attr_name)
    # build the name string
    name  = name_for(@record, attr_name)
    # dynamically grab the attr value off of the @record
    value = @record.read_attribute(attr_name)
    # create and return the HTML string for the tag
    # using our tag helper from before
    my_text_area_tag(name, value)
  end

  # very similar to `my_text_area`
  def my_text_field(attr_name)
    name  = name_for(@record, attr_name)
    value = @record.read_attribute(attr_name)
    my_text_field_tag(name, value)
  end

  def my_submit
    # decide what the submit text should be
    text = if @record.new_record?
            "Create #{@record.class}"
          else
            "Update #{@record.class}"
          end

    # build and return the tag string
    my_submit_tag(text)
  end
end

```

Keeping track of the object we're building the form for in `@record`, we're able to push a lot of the logic to our helper methods and keep our view nice and clean.

And, as you might guess, Rails provides these helper methods like these to us, just as it did with the `_tag` helpers earlier.

Our own `my_form_for` form helper works very similar to Rails' built in `form_for` helper! Here is how the Rails form helper would look like:

```
<!-- app/views/posts/show.html.erb -->

<%= form_for [@post, @comment] do |f| %>
  <%= f.label :body, 'Comment:' %>
  <%= f.text_area :body %>

  <%= f.label :author, 'Your Name:' %>
  <%= f.text_field :author %>

  <%= f.submit %>
<% end %>

```

The label field implementation is a bit different. Here it takes two arguments and the first is the attribute `name` the label corresponds to and the second is the text we want displayed for the label. We want to pass the attribute name here because `f.label` will build an appropriate `for` attribute to match its field's `id`. For example, this results in author label and field HTML like this:

```
<label for="comment_author">Your Name:</label>
<input id="comment_author" type="text" name="comment[author]" />
<!-- the matching `for` and `id` values -->

```

In this chapter we've covered quite a bit. We've slowly added in more functionality to our forms with `form_for`, and we've even made our own `form_for` as `my_form_for`. Hopefully you're starting to see what's behind all the magic of our Rails form helpers.

# 8.6 Active Record Migrations

We currently have used direct SQL to change our database structure. This is fine if we were developing alone but wouldn't work in a team environment because the database change on our machine is not tracked anywhere, so our teammates won't be able to pick it up.

Sharing database state among members of a team can quickly become a nightmare, unless you have a strategy. Fortunately, there's an easy way of dealing with this in Rails, because Active Record provides us with the ability to create, run, and track database **migrations**. This makes database changes much, much more manageable by isolating each change in its own file, conveniently written in Ruby.

## [Migration Fundamentals](https://launchschool.com/books/demystifying_rails/read/active_record_migrations#migrationsfundamentals)

Let's imagine we don't have our database from before, and write a couple migrations to create our `posts` and `comments` tables:

```
### db/migrate/20150127114820_create_posts.rb ###

class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts do |t|
      t.string :title
      t.text   :body
      t.string :author

      t.timestamps null: false
    end
  end
end

```

```
### db/migrate/20150127115017_create_comments.rb ###

class CreateComments < ActiveRecord::Migration
  def change
    create_table :comments do |t|
      t.text    :body
      t.string  :author
      t.integer :post_id

      t.timestamps null: false
    end
  end
end

```

Here we see `create_table` calls used to name both tables. Then, inside the passed block, we see various calls of the format `t.data_type :column_name` to define the columns. And the `t.timestamps` at the bottom is responsible for creating `created_at` and `updated_at` columns, which are `DateTime`columns that are automatically set by Active Record as changes are made to the records.

As far as naming goes, there are a couple important things to note:

1. table names should be the lowercase, plural, underscored-separated class name e.g. `ModelName` would have a `model_names` table
2. column names for foreign keys should be the lowercase, singular, underscored-separated class name followed by `_id` e.g. the column to reference a post is `post_id`

It's critical to get the naming for these values right if you want to utilize all the conveniences that Rails can provide for your models.

Notice also that the file contains a class that inherits from `ActiveRecord::Migration`. Because of this the `change` method defined within has special meaning. Using the tools we're about to see, it can be run *up*or *down*. The `create_table` call does what it claims when run up, and drops the table when run down.

And finally, the filenames of these migrations is important:

```
db/migrate/20150127114820_create_posts.rb
db/migrate/20150127115017_create_comments.rb

```

Rails will run migrations in alphanumeric order by their filenames, so migration filenames are traditionally prefixed with a timestamp to maintain this order. Because of the naming above, the `create_posts` migration will be run first.

Also, notice that the filenames contain `create_posts` and `create_comments`. The filename for a migration should be descriptive of what it does, and this is the traditional way of creating a migration for creating a new table. Along the same line, if you wanted to, say, add a `user_id` column to the `posts` table, you'd create a migration that ended in `add_user_id_to_posts.rb`.

## [Running Migrations](https://launchschool.com/books/demystifying_rails/read/active_record_migrations#runningmigrations)

So let's see these migrations in action. First, we'll use a `rake` command to drop the DB we presently have (this works because Rails expects our DB to be at `db/development.sqlite3`, and it is). Then we'll run the migrations.

```
$ bundle exec rake db:drop

$ bundle exec rake db:migrate
== 20150127114820 CreatePosts: migrating ======================================
-- create_table(:posts)
  -> 0.0008s
== 20150127114820 CreatePosts: migrated (0.0009s) =============================

== 20150127115017 CreateComments: migrating ===================================
-- create_table(:comments)
  -> 0.0004s
-- add_index(:comments, :post_id)
  -> 0.0004s
== 20150127115017 CreateComments: migrated (0.0009s) ==========================

```

This creates the tables, but it also generates a `db/schema.rb` file. No need to read the whole thing, but it looks like this:

```
### db/schema.rb ###

# encoding: UTF-8
# This file is auto-generated from the current state of the database. Instead
# of editing this file, please use the migrations feature of Active Record to
# incrementally modify your database, and then regenerate this schema definition.
#
# Note that this schema.rb definition is the authoritative source for your
# database schema. If you need to create the application database on another
# system, you should be using db:schema:load, not running all the migrations
# from scratch. The latter is a flawed and unsustainable approach (the more migrations
# you'll amass, the slower it'll run and the greater likelihood for issues).
#
# It's strongly recommended that you check this file into your version control system.

ActiveRecord::Schema.define(version: 20150127115017) do

  create_table "comments", force: true do |t|
    t.text     "body"
    t.string   "author"
    t.integer  "post_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

  create_table "posts", force: true do |t|
    t.string   "title"
    t.text     "body"
    t.string   "author"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

end

```

As the comment says, this schema file is the authoritative source for your database schema. If you ever forget your DB structure, you can consult this file. But never change it manually, as it's only intended to be changed by Rails.

## [More on Active Record Migrations](https://launchschool.com/books/demystifying_rails/read/active_record_migrations#moreonmigrations)

Let's look at some more information regarding Active Record Migrations:

```
# in our `create_table :comments` above, we could
# have defined our `post_id` column instead with:
create_table :comments do |t|
  t.references :post, index: true
  # `.references :post` makes an integer `post_id`
  # column, and we also specify that we want this
  # column to be indexed with `index: true`
end

# we can also make changes to existing tables
# assuming we already had a `users` table...
class AddAdminToUsers < ActiveRecord::Migration
  def change
    #           table   column  type
    add_column :users, :admin, :boolean, null: false, default: false
    # we also pass options to disallow, on the DBMS level,
    # `NULL` values, and default this column to `false`
  end
end

```

And migrations go both up and down. We already know that `$ bundle exec rake db:migrate` runs them up, but let's take a look at how to roll them back, and also how to see what's been run:

```
$ bundle exec rake db:rollback

== 20150127115017 CreateComments: reverting ===================================
-- remove_index(:comments, {:column=>:post_id})
   -> 0.0006s
-- drop_table(:comments)
   -> 0.0002s
== 20150127115017 CreateComments: reverted (0.0026s) ==========================

$ bundle exec rake db:migrate:status

database: .../blog-app/db/development.sqlite3

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20150127114820  Create posts
  down    20150127115017  Create comments

$ bundle exec rake db:migrate

== 20150127115017 CreateComments: migrating ===================================
-- create_table(:comments)
   -> 0.0010s
-- add_index(:comments, :post_id)
   -> 0.0005s
== 20150127115017 CreateComments: migrated (0.0016s) ==========================

$ bundle exec rake db:migrate:status

database: .../blog-app/db/development.sqlite3

 Status   Migration ID    Migration Name
--------------------------------------------------
   up     20150127114820  Create posts
   up     20150127115017  Create comments

```

And it's also worth noting that Active Record automatically handles the setting of the `timestamps` columns (`created_at` and `updated_at`) for us:

```
post = Post.last
post.updated_at
# => Sat, 31 Jan 2015 10:59:33 UTC +00:00

post.body = 'foobar'
# => "foobar"
post.save
# => true

post.updated_at
# => Sat, 31 Jan 2015 11:49:38 UTC +00:00

```

### Reversible and Irreversible Migrations

So far we've been using the `change` method in our migrations. This is a very useful method that allows us to include code that changes the database when a migration is run. And depending on the code we use, it may also be reversed when we rollback a migration. But, not all actions in a database migration can be reversed automatically. Rails uses `ActiveRecord::Migration::CommandRecorder` for recording commands used in migration, it also knows how to reverse them. Refer to this [list](http://api.rubyonrails.org/classes/ActiveRecord/Migration/CommandRecorder.html) of possible actions to take in a migration file. These are all the actions that are reversible. If a common Rails database command you use isn't in this list, then it cannot be automatically reversed. In that case, you'll have to use `up` and `down` methods to write what happens when we run a migration(up) and when we roll it back(down).

## [Add last_commented_on to Posts](https://launchschool.com/books/demystifying_rails/read/active_record_migrations#lastcommentedon)

So far we've seen various operations that can be performed through Active Record migrations. We've seen how to add a column to a table, migrate those changes, and how to roll them back if necessary. Let's practice some of what we've learned thus far. We want to add a new column to the posts table. This column will be called `last_commented_on`, we'll use an Active Record callback to update this column whenever a new comment is created on a `Post` object. The column should be of type `DateTime` and have a value of the time of the last created comment for that post.

First, let's generate our migration file with the following command:

```
rails g migration add_last_commented_on_to_posts

```

```
class AddLastCommentedOnToPosts < ActiveRecord::Migration[5.0]
  def change
    add_column :posts, :last_commented_on, :datetime
  end
end

```

Next execute the migration we just created:

```
bundle exec rake db:migrate

```

The next step is to set up a callback in the Comment model to handle the updates necessary for the Post column, `last_commented_on`.

```
class Comment < ActiveRecord::Base
  # ...

  after_save :update_last_commented_on

  private

  def update_last_commented_on
    self.post.last_commented_on = self.created_at
  end
end

```

See how we're using `after_save` method. We use `after_save` because the Comment `created_at` column only gets populated after a save. Once that column has been set, we can then assign it to `last_commented_on` field for the Post related to this `Comment`. So, using `after_save` allows us to specify a callback method to run after a Comment is saved to the db. To be extra safe, we could add the option `on: :create` to our `after_save` callback. But, this extra safeguard isn't really necessary, since `created_at` is only set on `Comment`creation.

Now, let's test out our new Active Record callback in the rails console.

```
irb(main):001:0> post = Post.first
  Post Load (0.2ms)  SELECT  "posts".* FROM "posts" ORDER BY "posts"."id" ASC LIMIT ?  [["LIMIT", 1]]
=> #<Post id: 1, title: "Blog 1", body: "Lorem ipsum dolor sit amet.", author: "Kevin", created_at: "2016-05-07 00:00:00", updated_at: "2016-05-07 00:00:00", last_commented_on: nil>
irb(main):002:0> comment = post.comments.create body: 'hello', author: 'jaba'
   (0.0ms)  begin transaction
  SQL (0.5ms)  INSERT INTO "comments" ("body", "author", "post_id", "created_at", "updated_at")
  VALUES (?, ?, ?, ?, ?)  [["body", "hello"], ["author", "jaba"], ["post_id", 1], ["created_at",
  2016-08-09 18:58:36 UTC], ["updated_at", 2016-08-09 18:58:36 UTC]]
   (3.7ms)  commit transaction
=> #<Comment id: 10, body: "hello", author: "jaba", post_id: 1, created_at: "2016-08-09 18:58:36", updated_at: "2016-08-09 18:58:36">
irb(main):003:0> post.last_commented_on == comment.updated_at
=> true

```

That seems like some good practice for using migrations and callbacks.

For more resources on Active Record migrations:

- [the Ruby on Rails Guide on Active Record migrations](http://guides.rubyonrails.org/active_record_migrations.html)
- [the API documentation for ActiveRecord::Migration](http://api.rubyonrails.org/classes/ActiveRecord/Migration.html)

# 8.7 Seeding the Database

## [seeds.rb](https://launchschool.com/books/demystifying_rails/read/seeding_the_database#seedsfile)

So now we've used Rails' conveniences to recreate our database tables, but they're empty again. We could use the CSV files from before to repopulate them, but instead let's define a `db/seeds.rb` file to demonstrate how we can seed our database with test data programmatically using Ruby and our models:

```
### db/seeds.rb ###

puts "Seeding"

print "  posts "

posts = [
  {
    title:     'Blog 1',
    body:      'Lorem ipsum dolor sit amet.',
    author:    'Kevin',
  },
  {
    title:     'Blog 2',
    body:      'Lorem ipsum dolor sit amet.',
    author:    'Chris',
  },
  {
    title:     'Blog 3',
    body:      'Lorem ipsum dolor sit amet.',
    author:    'Brad',
  }
]

time = DateTime.parse '2016-5-07'

posts.each do |post_hash|
  Post.create post_hash.merge(created_at: time, updated_at: time)

  time += 1.day

  print '.'
end


print "\n  comments "

comment_authors = %w[Matz DHH tenderlove]

Post.all.each do |post|
  3.times do
    post.comments.create \
      body:      'Lorem ipsum dolor sit amet.',
      author:     comment_authors.sample,
      created_at: time,
      updated_at: time

    time += 1.day

    print '.'
  end
end
puts

```

This creates our three posts from before and then creates three comments per post by a random author.

Now, if you have actual data you want to use, a CSV may be a good choice, but in the case that you just want to generate some data to play with, seeding this way may be a better option.

You can use this file to seed your DB with the following command:

```
$ bundle exec rake db:seed
Seeding
  posts ...
  comments .........

```

Let's hop into Rails console real quick to make sure that the seeding process worked as intended.

```
$ bundle exec rails c

```

```
irb(main):001:0> Post.all
  Post Load (4.2ms)  SELECT "posts".* FROM "posts"
=> #<ActiveRecord::Relation [#<Post id: 1, title: "Blog 1", body: "Lorem ipsum dolor sit amet.", author: "Kevin", created_at: "2016-05-07 00:00:00", updated_at: "2016-05-07 00:00:00">,
#<Post id: 2, title: "Blog 2", body: "Lorem ipsum dolor sit amet.", author: "Chris", created_at: "2016-05-08 00:00:00", updated_at: "2016-05-08 00:00:00">,
#<Post id: 3, title: "Blog 3", body: "Lorem ipsum dolor sit amet.", author: "R2D2", created_at: "2016-05-09 00:00:00", updated_at: "2016-05-09 00:00:00">]>

irb(main):002:0> Comment.all
  Comment Load (1.3ms)  SELECT "comments".* FROM "comments"
=> #<ActiveRecord::Relation [#<Comment id: 1, body: "Lorem ipsum dolor sit amet.", author: "DHH", post_id: 1, created_at: "2016-05-10 00:00:00", updated_at: "2016-05-10 00:00:00">,
#<Comment id: 2, body: "Lorem ipsum dolor sit amet.", author: "Matz", post_id: 1, created_at: "2016-05-11 00:00:00", updated_at: "2016-05-11 00:00:00">,
#<Comment id: 3, body: "Lorem ipsum dolor sit amet.", author: "Matz", post_id: 1, created_at: "2016-05-12 00:00:00", updated_at: "2016-05-12 00:00:00">,
#<Comment id: 4, body: "Lorem ipsum dolor sit amet.", author: "DHH", post_id: 2, created_at: "2016-05-13 00:00:00", updated_at: "2016-05-13 00:00:00">,
#<Comment id: 5, body: "Lorem ipsum dolor sit amet.", author: "tenderlove", post_id: 2, created_at: "2016-05-14 00:00:00", updated_at: "2016-05-14 00:00:00">,
#<Comment id: 6, body: "Lorem ipsum dolor sit amet.", author: "tenderlove", post_id: 2, created_at: "2016-05-15 00:00:00", updated_at: "2016-05-15 00:00:00">,
#<Comment id: 7, body: "Lorem ipsum dolor sit amet.", author: "Matz", post_id: 3, created_at: "2016-05-16 00:00:00", updated_at: "2016-05-16 00:00:00">,
#<Comment id: 8, body: "Lorem ipsum dolor sit amet.", author: "DHH", post_id: 3, created_at: "2016-05-17 00:00:00", updated_at: "2016-05-17 00:00:00">,
#<Comment id: 9, body: "Lorem ipsum dolor sit amet.", author: "Matz", post_id: 3, created_at: "2016-05-18 00:00:00", updated_at: "2016-05-18 00:00:00">]>
```

Great, it seems we have 3 posts, and 3 comments for each of those posts, just as we specified in our `seeds.rb` file.

# 9. Conclusion

Throughout this book we built a blog application, which served as the basis for revealing the magic behind the web development framework Ruby on Rails. We first built this app without any Rails conventions to focus on the core fundamental web development tasks and completely bypassed the Rails magic. By building features from scratch, we were forced to understand the *problems*that these conventions solve.

From there, we slowly added in Rails conventions. By utilizing Rails conventions and libraries, we were able to streamline development and build out features faster. By showing what problems these conventions address, we were able to see their power and experience their utility.

This book is here to show what happens behind the scenes when using Ruby on Rails. It's one thing to use a technology, and it is another thing to understand it. So many people stop at being content with merely using Rails to sling together simple CRUD applications. But having a deeper understanding will help when you have to customize and configure Rails, and when you have to utilize it to ends outside of a textbook example. We certainly didn't show everything there is to know about Ruby on Rails, but our hope is that we have given you enough of a start to begin an earnest journey into truly *understanding* this powerful framework.