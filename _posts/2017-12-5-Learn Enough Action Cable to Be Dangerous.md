---
layout: post
title: "Learn Enought Action Cable to Be Dangerous"
date: 2017-12-5
tags:
  Learn_Enough
  教材
  Ruby_On_Rails
---
![cover](https://ws1.sinaimg.cn/large/006tKfTcgy1fm7383so9sj30fg0namyj.jpg)
# Learn Enough Action Cable to Be Dangerous

**Michael Hartl**

An introduction to real-time apps with Rails 5

*Learn Enough Action Cable to Be Dangerous* is an introduction to Action Cable, a WebSockets interface for Rails (available as of Rails 5.0) that combines ultra-responsive real-time applications with the power and convenience of Rails. Its main prerequisites are a knowledge of Rails at the level of the [*Ruby on Rails Tutorial*](http://railstutorial.org/book) and technical sophistication at the level of [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial). A working knowledge of JavaScript is also recommended, but is not strictly necessary.[1](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-1)

We’ll start in [Section 1](https://www.learnenough.com/action-cable-tutorial#sec-websockets_and_action_cable) by giving a brief overview of Action Cable, including a discussion of what WebSockets are and what they can do. In [Section 2](https://www.learnenough.com/action-cable-tutorial#sec-base_app), we’ll introduce the base application, which is a pre-existing Rails chat app made using the standard [REST architecture](https://www.railstutorial.org/book/toy_app#aside-REST). In [Section 3](https://www.learnenough.com/action-cable-tutorial#sec-javascript_nanoslices), we’ll mention some aspects of JavaScript and related technologies needed to build real-time apps. Then in [Section 4](https://www.learnenough.com/action-cable-tutorial#sec-upgrading_to_action_cable) we’ll upgrade the application to use Action Cable. We’ll add some basic enhancements in [Section 5](https://www.learnenough.com/action-cable-tutorial#sec-basic_enhancements) and some more advanced enhancements in [Section 6](https://www.learnenough.com/action-cable-tutorial#sec-advanced_enhancements), and then in [Section 7](https://www.learnenough.com/action-cable-tutorial#sec-deploying_to_production) we’ll deploy the application to production.

*Note*: This tutorial is available for free online and available for purchase as an ebook and video [here](https://www.learnenough.com/buy/232).

## [1WebSockets and Action Cable](https://www.learnenough.com/action-cable-tutorial#sec-websockets_and_action_cable)

The *WebSocket Protocol* is a complement to the standard HyperText Transfer Protocol (HTTP) that creates a persistent connection between servers and clients, allowing two-way communication between them. The result is that WebSockets allow developers to create real-time applications such as chat apps and game servers that are far more interactive than ordinary web pages.

In HTTP, the standard request–response cycle ([Figure 1](https://www.learnenough.com/action-cable-tutorial#fig-http_protocol))[2](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-2) allows for a huge variety of apps—including nearly all of the web apps currently in existence—but it isn’t well-suited to real-time apps that require the server and client to be in constant communication.HTTP’s design is what’s known as “half-duplex”, which means that only one half of the client/server system can be “talking” at a given time. This design is simple and efficient, and shows up in situations such as [CB radios](https://en.wikipedia.org/wiki/Citizens_band_radio) and [walkie-talkies](https://en.wikipedia.org/wiki/Walkie-talkie) ([Figure 2](https://www.learnenough.com/action-cable-tutorial#fig-walkie_talkie)).[3](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-3) When using such devices, users are restricted to a single communication band, requiring the use of a standard word or phrase to indicate the end of a one-way message (such as “[Over](https://youtu.be/fVq4_HhBK8Y)”) to let the other person know they can begin talking. In the context of HTTP responses, these messages take the form of standard [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes), such as 200 OK and 301 Moved Permanently (known colloquially as a “301 redirect”).[4](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-4)

![images/figures/http_protocol](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v3pj9v8j31fk10sjrq.jpg)

Figure 1: The request–response cycle of the HyperText Transfer Protocol.

![images/figures/walkie_talkie](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v3u8c9ij308m0dwwlj.jpg)

Figure 2: An early walkie-talkie.

In contrast to HTTP’s half-duplex communication, the WebSocket Protocol allows *full-duplex* communication between client and server (after an intial one-way request using a [header](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) called “[Upgrade](https://en.wikipedia.org/wiki/HTTP/1.1_Upgrade_header)”), as shown in [Figure 3](https://www.learnenough.com/action-cable-tutorial#fig-websocket_protocol). This connection allows the client and server to communicate simultaneously and persistently—i.e., instead of a walkie-talkie, we have a mobile phone.

![images/figures/websocket_protocol](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v3w3s5nj31fk10sab3.jpg)

Figure 3: The WebSocket procotol’s full-duplex communication.

For example, consider a chat app written using HTTP. Alice ([Figure 4](https://www.learnenough.com/action-cable-tutorial#fig-alice))[5](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-5) and Bob ([Figure 5](https://www.learnenough.com/action-cable-tutorial#fig-bob))[6](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-6) each types in their respective chat boxes ([Figure 6](https://www.learnenough.com/action-cable-tutorial#fig-chat_box)). When Alice submits a message, there’s no way for Bob to get it without refreshing his browser. As a result, the traditional solution for HTTP chat is to use *polling*, whereby the client runs a program (typically in JavaScript) to pull in any changes every few seconds.

Polling is sufficient in situations where a short delay is acceptable, but it’s inefficient because the polling happens regardless of whether there’s a new message or not, and it scales horribly as clients are added, because each client has to hit the server every time it polls. It’s not a disaster, and the chat app for [Basecamp](http://basecamp.com/) (the original Rails app) used polling for years. But, as Rails creator David Heinemeier Hansson (DHH) has [noted](https://www.youtube.com/watch?v=KJVTM7mE1Cc), using WebSockets is even better, as long as it’s not too hard.

Making WebSockets not too hard is the purpose of Action Cable.

![images/figures/alice](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v3xe8f8j306o050jrq.jpg)

Figure 4: Alice.

![images/figures/bob](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v3yoyrtj304c06oq2z.jpg)

Figure 5: Bob.

![images/figures/chat_box](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v4089noj30vi0ntwfq.jpg)

Figure 6: A chat box.

The reason using WebSockets is better than polling is because there is a bi-directional connection between the server and each client, so Alice’s submitted message gets pushed to Bob immediately after being received by the server. Moreover, because the connection is persistent, Alice and Bob can submit their messages at the same time and still see their respective messages appear immediately. Finally, the WebSocket protocol scales much better with multiple users, with the server simply maintaining one WebSocket per client, updating only as necessary.

When using WebSockets, it’s nice to be able to have users log in, store their attributes in a database, render templates back to the browser, etc. In other words, it’s nice to have the full power of Ruby on Rails behind us. This is where Action Cable comes in. Using Action Cable gives us the best of both worlds: real-time, full-duplex communications with WebSockets combined with all the convenience and flexibility of Rails.

To show off power of WebSockets, the rest of this tutorial develops a simple real-time chat app with Action Cable. The final design combines aspects of “[Rails 5: Action Cable Demo](https://medium.com/@dhh/rails-5-action-cable-demo-8bba4ccfc55e)” by DHH and “[Real-Time Rails](https://blog.heroku.com/real_time_rails_implementing_websockets_in_rails_5_with_action_cable)” by [Sophie DeBenedetto](http://sophiedebenedetto.nyc/). In particular, although we’ll be using some of the more advanced techniques introduced by DHH, we’ll be sure to ground our app in the kind of standard REST design used for non-WebSocket apps.

We’ll start by giving a high-level overview of the *base app* ([Section 2](https://www.learnenough.com/action-cable-tutorial#sec-base_app)), which implements a basic chat app. We’ll then take a brief detour for a crash course on the aspects of JavaScript (including CoffeeScript) needed to make our chat app ([Section 3](https://www.learnenough.com/action-cable-tutorial#sec-javascript_nanoslices)). We’ll then build the core WebSocket-enabled chat app ([Section 4](https://www.learnenough.com/action-cable-tutorial#sec-upgrading_to_action_cable)), and then add some polish in [Section 5](https://www.learnenough.com/action-cable-tutorial#sec-basic_enhancements). Finally, we’ll conclude by adding a couple of more advanced extensions, Markdown support and @mention alerts ([Section 6](https://www.learnenough.com/action-cable-tutorial#sec-advanced_enhancements)), and then deploy the application to production ([Section 7](https://www.learnenough.com/action-cable-tutorial#sec-deploying_to_production)).

## [2Base app](https://www.learnenough.com/action-cable-tutorial#sec-base_app)

We’ll begin with a base app that implements the basic functionality of a chat app but without Action Cable (or even polling). The purpose is to start with an app design that is familiar from other REST-style applications, thus helping to bridge the gap to the Action Cable style used starting in [Section 4](https://www.learnenough.com/action-cable-tutorial#sec-upgrading_to_action_cable).

The base app works as a chat app, but it’s intentionally impractical. In particular, chat participants have to manually refresh their browsers to see messages from other users.This cumbersome design provides ample motivation to implement an Action Cable solution. (The base app also has no mechanism for letting new users register for the site, but such straightforward extensions should be within your capabilities if you’re reading this tutorial, or can be found in the [*Ruby on Rails Tutorial*](http://railstutorial.org/book).)

Rather than build the base app from scratch, we’ll instead *fork* and *clone* the app from a reference repository, and then go over its most important parts.

### [2.1Application setup](https://www.learnenough.com/action-cable-tutorial#sec-application_setup)

The base app’s source is hosted at [github.com/mhartl/action_cable_chat_app](https://github.com/mhartl/action_cable_chat_app). You should make your own copy of the repository so that you can push your own changes, and the way to do this in Git is to fork the repository, as shown in [Figure 7](https://www.learnenough.com/action-cable-tutorial#fig-fork).

![images/figures/fork](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v429du7j30vi0nt78i.jpg)

Figure 7: Forking the chat app repo.

![images/figures/clone](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v4593trj30vi0ntjvo.jpg)

Figure 8: Getting the chat app clone URL.

Once you’ve forked the repo, you should grab the clone URL ([Figure 8](https://www.learnenough.com/action-cable-tutorial#fig-clone)) and then clone it at the command line as follows:

```
$ git clone https://github.com/<username>/action_cable_chat_app.git

```

(For reference, this repo has an `action-cable-reference` branch with the state of the app at the end of this tutorial.) Then `cd` into it as follows:

```
$ cd action_cable_chat_app/

```

Then install any necessary gems and prepare the database and seed data:

```
$ bundle install
$ rails db:migrate
$ rails db:seed

```

Finally, run the test suite to make sure the app is working:

```
$ rails test

```

If the tests fail, use your technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)) to debug the issue.

> Box 1. Technical sophistication.
>
> One of the principal themes developed by [Learn Enough to Be Dangerous](http://learnenough.com/) is *technical sophistication*, the knowledge and attitude needed to solve technical problems. It’s likely that you will have ample opportunity to exercise your technical sophistication when following *Learn Enough Action Cable to Be Dangerous*. If you’re not fluent in JavaScript or CoffeeScript, you’ll discover that it’s challenging but entirely possible to program in a language you hardly know.You’ll also likely have opportunities to experience the joys of debugging JavaScript in a browser. (*Hint*: The web inspector, `console.log`, and `alert` are your friends.) Whatever comes your way, remember: we all run into brick walls all the time. The difference is that, with the power of technical sophistication, you’ll have what it takes to break through them.

### [2.2User and Message models](https://www.learnenough.com/action-cable-tutorial#sec-user_and_message_models)

We’ll start our investigation of the base app by looking at the data model, which is generally a good route into an app you haven’t seen before. Rails stores the data model in the file `db/schema.rb`, as shown in [Listing 1](https://www.learnenough.com/action-cable-tutorial#code-schema).

Listing 1: The database schema.`db/schema.rb`

```
ActiveRecord::Schema.define(version: 20160719235623) do

  create_table "messages", force: :cascade do |t|
    t.text     "content"
    t.integer  "user_id"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["user_id"], name: "index_messages_on_user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string   "username"
    t.string   "password_digest"
    t.datetime "created_at",      null: false
    t.datetime "updated_at",      null: false
    t.index ["username"], name: "index_users_on_username", unique: true
  end

end

```

We see from [Listing 1](https://www.learnenough.com/action-cable-tutorial#code-schema) that there are two tables, `users` and `messages`, implementing the data models shown in [Figure 9](https://www.learnenough.com/action-cable-tutorial#fig-user_model) and [Figure 10](https://www.learnenough.com/action-cable-tutorial#fig-message_model).

![images/figures/user_model](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v46sa1dj3080049jrg.jpg)

Figure 9: The `users` table for the User model.

![images/figures/message_model](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v4810l0j30720493yk.jpg)

Figure 10: The `messages` table for the Message model.

The corresponding Active Record models are User and Message, located as usual in the `app/models/` directory. The User model ([Listing 2](https://www.learnenough.com/action-cable-tutorial#code-user_model)) includes a username validated for presence, case-insensitive uniqueness, format, and length. It also implements a secure password using `has_secure_password`, with separate validations for password presence and length.

Listing 2: The User model.`app/models/user.rb`

```
class User < ApplicationRecord
  has_many :messages
  NAME_REGEX = /\w+/
  validates :username, presence: true, uniqueness: { case_sensitive: false },
                       format: { with: /\A#{NAME_REGEX}\z/i },
                       length: { maximum: 15 }
  validates :password, presence: true, length: { minimum: 6 }
  has_secure_password
end

```

The Message model ([Listing 3](https://www.learnenough.com/action-cable-tutorial#code-message_model)) includes a text field called `content` with a presence validation, as well as a named scope to ensure that the messages for display appear with most-recent last (at the bottom of the chat) and a maximum of 50.

Listing 3: The Message model.`app/models/message.rb`

```
class Message < ApplicationRecord
  belongs_to :user
  validates :content, presence: true
  scope :for_display, -> { order(:created_at).last(50) }
end

```

Finally, [Listing 2](https://www.learnenough.com/action-cable-tutorial#code-user_model) and [Listing 3](https://www.learnenough.com/action-cable-tutorial#code-message_model) set up a `has_many`/`belongs_to` association, as shown in [Figure 11](https://www.learnenough.com/action-cable-tutorial#fig-user_message_association). This association gives rise in the usual way to an array-like attribute `user.messages` for each user’s messages and a `message.user` attribute for each message’s user.

![images/figures/user_message_association](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v493axtj30et050q3a.jpg)

Figure 11: The association between users and messages.

### [2.3Messages resource](https://www.learnenough.com/action-cable-tutorial#sec-messages_resource)

In keeping with the usual [REST architecture](https://www.railstutorial.org/book/toy_app#aside-REST) favored by Rails, we treat messages as a *resource* that can be created, updated, and destroyed. We’ve already seen the Message model ([Listing 3](https://www.learnenough.com/action-cable-tutorial#code-message_model)), and for a full resource we need the corresponding Messages controller, as shown in [Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller).

We see from [Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller) that we’ll need only the `index` and `create` actions in this tutorial, but a more full-featured chat app would probably add the other REST actions as well (`show`, `edit`, `update`, and `destroy`).

Listing 4: The Messages controller.`app/controllers/messages_controller.rb`

```
class MessagesController < ApplicationController
  before_action :logged_in_user
  before_action :get_messages

  def index
  end

  def create
    message = current_user.messages.build(message_params)
    if message.save
      redirect_to messages_url
    else
      render 'index'
    end
  end

  private

    def get_messages
      @messages = Message.for_display
      @message  = current_user.messages.build
    end

    def message_params
      params.require(:message).permit(:content)
    end
end

```

The highlighted line in [Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller) shows that there is a `current_user` variable representing the currently logged-in user, which in this case uses the `build` action through the association ([Figure 11](https://www.learnenough.com/action-cable-tutorial#fig-user_message_association)) to make a new message.

To display and create the messages, we define a messages index, as shown in [Listing 5](https://www.learnenough.com/action-cable-tutorial#code-messages_index), which defers the hard work to a message form partial ([Listing 6](https://www.learnenough.com/action-cable-tutorial#code-message_form)) and a messages partial ([Listing 7](https://www.learnenough.com/action-cable-tutorial#code-messages_partial)).

Listing 5: The messages index.`app/views/messages/index.html.erb`

```
<div class="message-wr">
  <%= render 'messages' %>
  <%= render 'message_form' %>
</div>

```

Listing 6: The message form partial.`app/views/messages/_message_form.html.erb`

```
<div class="message-input">
  <%= form_for(@message) do |f| %>
    <%= f.text_area :content %>
    <%= f.submit "Send" %>
  <% end %>
</div>

```

The messages partial in turn delegates the rendering of individual messages to a message partial ([Listing 8](https://www.learnenough.com/action-cable-tutorial#code-message_partial)).

Listing 7: The messages partial.`app/views/messages/_messages.html.erb`

```
<div id="messages" class="messages">
  <div id="messages-table" class="messages-table">
    <% if @messages.any? %>
      <%= render @messages %>
    <% end %>
  </div>
</div>

```

Note in [Listing 7](https://www.learnenough.com/action-cable-tutorial#code-messages_partial) that we include both CSS ids and CSS classes. The classes are used mainly for styling, while the ids are included mainly to manipulate the Document Object Model (DOM) with JavaScript starting in [Section 3](https://www.learnenough.com/action-cable-tutorial#sec-javascript_nanoslices).

Listing 8: The message partial.`app/views/messages/_message.html.erb`

```
<div class="message">
  <div class="message-user">
    <%= message.user.username %>:
  </div>
  <div class="message-content">
    <%= message.content %>
  </div>
</div>

```

### [2.4Creating messages](https://www.learnenough.com/action-cable-tutorial#sec-using_for_messaging)

To verify that everything is working, let’s fire up a Rails server and log in as one of the sample users. We’ll start with `rails server` as usual:

```
$ rails server

```

*Note*: If you’re using the cloud IDE as described in the [*Ruby on Rails Tutorial*](http://railstutorial.org/book), recall that you’ll need to include the binding IP and port number as well:

```
$ rails server -b $IP -p $PORT

```

With the server running, we can now take a look at the locally running app, which is initially just a login window, as shown in [Figure 12](https://www.learnenough.com/action-cable-tutorial#fig-locally_running). We can log in as one of the users created by `rails db:seed` in [Section 2.1](https://www.learnenough.com/action-cable-tutorial#sec-application_setup) by entering the username “alice” and password “wonderland”, with the result shown in [Figure 13](https://www.learnenough.com/action-cable-tutorial#fig-initial_chat_window).

![images/figures/locally_running](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v4akjs2j30vi0nt0tx.jpg)

Figure 12: The locally running app.

![images/figures/initial_chat_window](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v4by5kij30vi0nt3zk.jpg)

Figure 13: The initial chat window.

We can submit a first chat message as Alice, as shown in [Figure 14](https://www.learnenough.com/action-cable-tutorial#fig-first_message). If we then use a different browser to log in as a second user (username “bob”, password “asdfasdf”), the first message will be displayed in the main box, as seen in [Figure 15](https://www.learnenough.com/action-cable-tutorial#fig-first_message_displayed).

![images/figures/first_message](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v4dd5l3j30vi0ntt9u.jpg)

Figure 14: Alice’s first message.

![images/figures/first_message_displayed](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v4eybxsj30vl0nt0tz.jpg)

Figure 15: The first message displayed for a second user.

If Bob then adds a message, it appears for him instantly because the HTTP response redirects him back to the same page ([Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller)), but it doesn’t refresh Alice’s window, so Bob’s message doesn’t appear ([Figure 16](https://www.learnenough.com/action-cable-tutorial#fig-alice_no_refresh)). Instead, Alice has to refresh her browser manually to get Bob’s message ([Figure 17](https://www.learnenough.com/action-cable-tutorial#fig-manual_refresh)).

![images/figures/alice_no_refresh](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v4gwlavj311i0kndhm.jpg)

Figure 16: The new message doesn’t appear for other users.

![images/figures/manual_refresh](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v4x00rcj30vi0ntgms.jpg)

Figure 17: The first user’s refreshed display.

Although this base app “works” (for certain values of “work”), it’s obviously inadequate for a real chat app, even a super-minimalist one. In particular, requiring users to refresh their browsers to get new messages is totally unacceptable.

As mentioned in the introduction, the standard solution in HTTP-land is periodic polling to pull in changes, but with the release of Action Cable we now have a much better option. The rest of this tutorial is dedicated to implementing it.

## [3JavaScript nanoslices](https://www.learnenough.com/action-cable-tutorial#sec-javascript_nanoslices)

Because the WebSocket Protocol involves establishing persistent connections between client and server, Action Cable relies on having code running in both places. On the server, we can use Rails and hence Ruby, but on the client we need to use the language of browsers, i.e., JavaScript.[7](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-7) As a result, in order to upgrade the base app from [Section 2](https://www.learnenough.com/action-cable-tutorial#sec-base_app)to use Action Cable, we need to take a moment to discuss JavaScript and related technologies.

By default, Action Cable uses a language called *CoffeeScript* that gets converted to JavaScript before being sent to the browser. In addition, for manipulating the Document Object Model, or DOM ([Box 2](https://www.learnenough.com/action-cable-tutorial#aside-DOM)),[8](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-8) the JavaScript library *jQuery* is practically essential.

This section thus contains tiny introductions (or *nanoslices*) to the aspects of JavaScript, CoffeeScript, and jQuery needed for this tutorial. The resulting presentation barely even scratches the surface, though, and pointers to further reading are included for reference.

> Box 2. The DOM.
>
> The Document Object Model, or DOM (“rhymes with Mom”) for short, refers to the structured tree-like representation of HTML documents. In this context, a picture is worth the proverbial thousand words:
>
> ![DOM-model](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v54i3hdj30bw0cbmxx.jpg)
>
> We see here that the DOM is ordered as a hierarchical structure, with elements and sub-elements all the way down to the plain text that makes up most of the web.
>
> There are many programs available for manipulating the DOM, but perhaps the most common is jQuery, a pure JavaScript library that makes accessing and modifying DOM elements a breeze. We’ll start learning about this powerful library in [Section 3.2](https://www.learnenough.com/action-cable-tutorial#sec-a_nanoslice_of_jquery).

Because we’ll be making changes in the chat app that won’t be used later on, I suggest making a separate Git branch for this section:

```
$ git checkout -b javascript-nanoslices

```

### [3.1A nanoslice of JavaScript](https://www.learnenough.com/action-cable-tutorial#sec-a_nanoslice_of_javascript)

In this section we’ll introduce three essential aspects of JavaScript needed in our chat app: including JavaScript in our Rails app and function definition.

For convenience, we’ll work directly with the main JavaScript file used by Rails apps, `application.js`, which is located in the `app/assets/javascripts` directory. (In larger Rails apps, the usual practice is to use separate JavaScript files and then let the [Asset Pipeline](https://www.railstutorial.org/book/filling_in_the_layout#sec-the_asset_pipeline) combine them in production, but for our purposes using `application.js` is fine.)

We’ll start with a simple “hello, world” program just to make sure things are basically working.[9](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-9) The method is to use the JavaScript `alert` method with the string `’hello, world!’` as an argument, as shown in [Listing 9](https://www.learnenough.com/action-cable-tutorial#code-hello_world). (The vertical dots represent boilerplate comments and code generated by Rails, which should remain unmodified throughout this tutorial.)

Listing 9: A “hello, world” article in JavaScript.`app/assets/javascripts/application.js`

```
// This is a manifest file that'll be compiled into application.js...
.
.
.
alert('hello, world!');

```

If you’re new to JavaScript, note that method calls (also called function calls) are the same as in many other languages, with the name of the method followed by the argument(s) in parentheses, followed by a semicolon. (Only this last element won’t be familiar from a language like Ruby.)

We can see the result of [Listing 9](https://www.learnenough.com/action-cable-tutorial#code-hello_world) by refreshing the browser, which causes the `alert` to fire and displays its argument in a modal box, as shown in [Figure 18](https://www.learnenough.com/action-cable-tutorial#fig-hello_world).

![images/figures/hello_world](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v5dw7zgj30vi0nt75k.jpg)

Figure 18: The result of “hello, world” in JavaScript.

Our next task is to define a function in JavaScript, which we can do by assigning a name to a `function` as follows:[10](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-10)

```
greeting_doubler = function(phrase) {
  alert(phrase + " " + phrase);
};

```

This function serves as a “greeting doubler” by displaying the given `phrase` twice, separated by a space `" "`. Note the presence of curly braces to define the body of the function, a practice common in languages [influenced by Algol and C](http://programmers.stackexchange.com/questions/188455/why-do-programming-languages-especially-c-use-curly-braces-and-not-square-ones).

We can put the greeting doubler to work by replacing the alert in [Listing 9](https://www.learnenough.com/action-cable-tutorial#code-hello_world) with the code shown in [Listing 10](https://www.learnenough.com/action-cable-tutorial#code-greeting_doubler), which includes the function definition followed the call to `greeting_doubler` on the string `’hello, world!’`.

Listing 10: Defining a greeting double.`app/assets/javascripts/application.js`

```
.
.
.
greeting_doubler = function(phrase) {
  alert(phrase + " " + phrase);
};

greeting_doubler('hello, world!');

```

The result of refreshing the browser after including [Listing 10](https://www.learnenough.com/action-cable-tutorial#code-greeting_doubler) is shown in [Figure 19](https://www.learnenough.com/action-cable-tutorial#fig-greeting_doubler).

![images/figures/greeting_doubler](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v5fyvngj30vi0ntgmx.jpg)

Figure 19: A doubled greeting.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_a_nanoslice_of_javascript)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Does the code in [Listing 10](https://www.learnenough.com/action-cable-tutorial#code-greeting_doubler) still work if you swap the order of the function call and its definition?
2. What happens if you replace `’hello, world!’` in [Listing 10](https://www.learnenough.com/action-cable-tutorial#code-greeting_doubler) with `’¡Hola, mundo!’`?

### [3.2A nanoslice of jQuery](https://www.learnenough.com/action-cable-tutorial#sec-a_nanoslice_of_jquery)

In order to complete our chat app, we’ll need to append messages to the site’s messages div so that logged-in users see new messages as soon as they’re ready to be displayed.While it is possible to do this in raw JavaScript, it’s much easier to use jQuery, a pure JavaScript library for manipulating the DOM and performing other common JavaScript tasks. The jQuery library is included automatically with every new Rails application.

The specific task we’ll need is appending the HTML for new messages at the end of the `div` with CSS id `messages-table`, which is defined in the messages partial from [Listing 7](https://www.learnenough.com/action-cable-tutorial#code-messages_partial):

```
<div id="messages-table" class="messages-table">

```

This will involve selecting the DOM element with this id,[11](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-11) which we can do in jQuery using the dollar-sign operator `$`:

```
$('#messages-table')

```

Using a syntax borrowed from CSS, this jQuery selects the DOM element with id `messages-table`.

To append to the messages table, we can use the jQuery `append` method, which lets us append a string to the end of the table. A first guess at how this might work is shown in [Listing 11](https://www.learnenough.com/action-cable-tutorial#code-message_append_first_guess).

Listing 11: A first guess at message appending.`app/assets/javascripts/application.js`

```
.
.
.
$('#messages-table').append('hello, world!');

```

The code in [Listing 11](https://www.learnenough.com/action-cable-tutorial#code-message_append_first_guess) attempts to append the string `’hello, world!’` to the end of the messages table, but unfortunately it doesn’t work, as you can verify by refreshing the browser ([Figure 20](https://www.learnenough.com/action-cable-tutorial#fig-message_append_first_guess)).

![images/figures/message_append_first_guess](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v5m2lsoj30vi0ntgms.jpg)

Figure 20: A failed attempt at message appending.

The reason the code in [Listing 11](https://www.learnenough.com/action-cable-tutorial#code-message_append_first_guess) doesn’t work is related to the order of events when a web page loads. At the time `application.js` loads, the DOM hasn’t yet been defined, so there’s no element available to append to. The solution is is to use the `on` method to run the code in [Listing 11](https://www.learnenough.com/action-cable-tutorial#code-message_append_first_guess) on document load—or, more specifically, on loading the Rails *Turbolinks* library:

```
$(document).on('turbolinks:load', function() {
  $('#messages-table').append('hello, world!');
});

```

This code is syntactically complex, and I recommend copying it exactly rather than trying to figure out exactly how it works. What’s important to know is that the code inside the curly braces executes after the DOM has been defined. Putting this code in `application.js` gives the result shown in [Listing 12](https://www.learnenough.com/action-cable-tutorial#code-message_append).

Listing 12: Working code to append a message.`app/assets/javascripts/application.js`

```
.
.
.
$(document).on('turbolinks:load', function() {
  $('#messages-table').append('hello, world!');
});

```

The result appears in [Figure 21](https://www.learnenough.com/action-cable-tutorial#fig-message_append). Of course, this is just a proof-of-concept, so we haven’t worried about the exact formatting, but starting in [Section 4](https://www.learnenough.com/action-cable-tutorial#sec-upgrading_to_action_cable) we’ll take care to append nice-looking HTML.

![images/figures/message_append](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v5utfc2j30vi0ntq4h.jpg)

Figure 21: Successfully appending text in the DOM.

As a final step, we’ll factor our message appender into a function, as shown in [Listing 13](https://www.learnenough.com/action-cable-tutorial#code-message_appender_function).Here the `message_appender` function is called on Turbolinks load, appending its `content` argument to the `#messages-table` element in the DOM.

Listing 13: Defining a message appender function.`app/assets/javascripts/application.js`

```
.
.
.
message_appender = function(content) {
  $('#messages-table').append(content);
}

$(document).on('turbolinks:load', function() {
  message_appender('hello, world!');
});

```

Upon refreshing the browser, the result should appear exactly as in [Figure 21](https://www.learnenough.com/action-cable-tutorial#fig-message_append).

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_a_nanoslice_of_jquery)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Can you guess the jQuery syntax to select elements with a particular CSS class?Google it only if necessary.
2. What happens if you reverse the order of the appender and document on load in [Listing 13](https://www.learnenough.com/action-cable-tutorial#code-message_appender_function)?

### [3.3A nanoslice of CoffeeScript](https://www.learnenough.com/action-cable-tutorial#sec-a_nanoslice_of_coffeescript)

By its own [description](http://coffeescript.org/), “CoffeeScript is a little language that compiles [is transformed] into JavaScript.” It’s designed to be a cleaner, more user-friendly version of JavaScript.

Writing CoffeeScript is an excellent exercise in technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)), and you can often guess the right syntax using a combination of JavaScript and Ruby. For example, in [Section 4.2](https://www.learnenough.com/action-cable-tutorial#sec-appending_messages) we’ll use the code

```
data.content.blank?

```

to check if a `data` object is blank, which is exactly the same syntax as Ruby.[12](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-12)

As an additional aid, Rails generates a template CoffeeScript files in some contexts, including when generating Action Cable *channels*, which will be enough to get us started when we start using CoffeeScript in [Section 4.1](https://www.learnenough.com/action-cable-tutorial#sec-the_room_channel). In fact, I hardly know CoffeeScript at all, but between the generated code and some judicious guessing we’ll be able to get surprisingly far.

For the purposes of this tutorial, the main thing we need to know about CoffeeScript is how to define functions, and the best way to do this is to translate one of our previous examples from JavaScript to CoffeeScript. Consider, for example, the message appender function defined in [Listing 13](https://www.learnenough.com/action-cable-tutorial#code-message_appender_function):

```
message_appender = function(content) {
  $('#messages-table').append(content);
}

```

The CoffeeScript version looks like this:

```
message_appender = (content) ->
  $('#messages-table').append content

```

The main differences compared to JavaScript are as follows:

1. CoffeeScript uses the compact arrow notation `->` for functions.
2. Parentheses are usually optional.
3. CoffeeScript uses much less punctuation (fewer parentheses, no curly braces, no semicolons).

CoffeeScript comes installed automatically in every new Rails app, and a CoffeeScript file gets generated with every new controller. In the case of the Messages controller, this means there’s a `messages.coffee` file in the `app/assets/javascripts` directory that we can use for a CoffeeScript version of [Listing 13](https://www.learnenough.com/action-cable-tutorial#code-message_appender_function).

First we’ll move the contents of [Listing 13](https://www.learnenough.com/action-cable-tutorial#code-message_appender_function) to the CoffeeScript file, as shown in [Listing 14](https://www.learnenough.com/action-cable-tutorial#code-no_message_appender)and [Listing 15](https://www.learnenough.com/action-cable-tutorial#code-message_appender_js_coffeescript).

Listing 14: The application JavaScript file restored to its original condition.`app/assets/javascripts/application.js`

```
// This is a manifest file that'll be compiled into application.js...
.
.
.

```

Listing 15: The message appender JavaScript moved to a CoffeeScript file.`app/assets/javascripts/messages.coffee`

```
# Place all the behaviors and hooks related to the matching controller here.
# All this logic will automatically be available in application.js.
# You can use CoffeeScript in this file: http://coffeescript.org/

message_appender = function(content) {
  $('#messages-table').append(content);
}

$(document).on('turbolinks:load', function() {
  message_appender('hello, world!');
});

```

JavaScript code isn’t allowed in CoffeeScript files, so the code in [Listing 15](https://www.learnenough.com/action-cable-tutorial#code-message_appender_js_coffeescript) doesn’t work, but we copied it in because converting it to CoffeeScript by hand is an instructive exercise. The result is shown in [Listing 16](https://www.learnenough.com/action-cable-tutorial#code-message_appender_coffeescript).

Listing 16: The message appender converted to CoffeeScript.`app/assets/javascripts/messages.coffee`

```
# Place all the behaviors and hooks related to the matching controller here.
# All this logic will automatically be available in application.js.
# You can use CoffeeScript in this file: http://coffeescript.org/

message_appender = (content) ->
  $('#messages-table').append content

$(document).on 'turbolinks:load', ->
  message_appender('hello, world!')

```

![images/figures/message_append_coffeescript](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v637rqyj30vi0nt403.jpg)

Figure 22: Appending text with CoffeeScript.

Although the final chat app will use several other aspects of JavaScript and CoffeeScript, at this point we’ve got enough foundation to start updating our application to use Action Cable. For more information, see the [resources at javascript.com](https://www.javascript.com/resources), and watch for the release of [*Learn Enough JavaScript to Be Dangerous*](http://learnenough.com/javascript-tutorial). Also consider taking a look at [CoffeeLint](http://www.coffeelint.org/), a style checker that helps catch formatting and other common errors in CoffeeScript code.

As a final step, I recommend committing the JavaScript branch in case you want to review it, and then check out the `master` branch as preparation for the Action Cable upgrade:

```
$ git commit -am "Finish JS, etc."
$ git checkout master

```

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_a_nanoslice_of_coffeescript)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What happens if you remove the parentheses in the call to `message_appender`in [Listing 16](https://www.learnenough.com/action-cable-tutorial#code-message_appender_coffeescript)?

## [4Upgrading to Action Cable](https://www.learnenough.com/action-cable-tutorial#sec-upgrading_to_action_cable)

In this section, we’ll modify the base app described in [Section 2](https://www.learnenough.com/action-cable-tutorial#sec-base_app) to use Action Cable.Instead of using the request–response cycle with HTTP ([Figure 1](https://www.learnenough.com/action-cable-tutorial#fig-http_protocol)), we’ll use persistent connections with WebSockets ([Figure 3](https://www.learnenough.com/action-cable-tutorial#fig-websocket_protocol)).

There are only three main steps needed to convert the base app to a working Action Cable chat app:

1. Make a *channel* to handle WebSocket connections on the server side (local server in development, Heroku in production).
2. Make a CoffeeScript program (`room.coffee`) for the chat room on the client side (web browser).
3. Update the Messages controller `create` action to *broadcast* changes to the channel instead of redirecting or rendering.

It’s convenient to keep the base app around for reference, so we’ll do our work on (and even deploy from) an `action-cable` topic branch:

```
$ git checkout -b action-cable

```

I’ll assume anyone reading this is advanced enough to handle their own Git tasks, so [make commits](https://www.learnenough.com/git-tutorial#aside-commitment_issues) as you see necessary throughout the rest of the tutorial. (For more on Git, see [*Learn Enough Git to Be Dangerous*](http://learnenough.com/git-tutorial).)

### [4.1The Room channel](https://www.learnenough.com/action-cable-tutorial#sec-the_room_channel)

The `rails` command, which is commonly used to generate models and controllers, can generate Action Cable channels as well. We’ll name ours “Room”:

```
$ rails generate channel Room
      create  app/channels/room_channel.rb
   identical  app/assets/javascripts/cable.js
      create  app/assets/javascripts/channels/room.coffee

```

If you like, you can also reset and reseed the database at this time:

```
$ rails db:migrate:reset && rails db:seed

```

This gets us back to a blank slate for now, but developing our chat app involves submitting lots of test messages, and in subsequent screenshots no attempt will be made to maintain continuity.

Let’s take a look at the Room channel generated by Rails, which appears as shown in [Listing 17](https://www.learnenough.com/action-cable-tutorial#code-generated_channel).

Listing 17: The generated channel.`app/channels/room_channel.rb`

```
# Be sure to restart your server when you modify this file.
# Action Cable runs in a loop that does not support auto reloading.
class RoomChannel < ApplicationCable::Channel
  def subscribed
    # stream_from "some_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end

```

Here we see two methods by default, `subscribed` and `unsubscribed`. Action Cable works by *subscribing* a user to a particular channel, which allows that user’s browser to be updated via a WebSocket. The `subscribed` and `unsubscribed` methods are [callbacks](https://en.wikipedia.org/wiki/Callback_(computer_programming)) that allow us to take action when either of these two events takes place. We’ll need only the `subscribed` method in our chat application, but the references at the end of the tutorial include pointers to apps that use `unsubscribe` as well ([Section 8](https://www.learnenough.com/action-cable-tutorial#sec-conclusion)).

Also note the comment at the top of [Listing 17](https://www.learnenough.com/action-cable-tutorial#code-generated_channel), indicating that the Rails server needs to be restarted to reload the Action Cable functionality. This is slated to change in a future Rails update, but for now you should restart the server when necessary. This tutorial won’t call out each such necessary restart, as figuring out things like this is a valuable exercise in technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)).

We’ll name our initial stream `"room_channel"`, which will be global to all users. (We’ll see an example of user-specific streams in [Section 6.2](https://www.learnenough.com/action-cable-tutorial#sec-at_mention_notifications).) The result appears in [Listing 18](https://www.learnenough.com/action-cable-tutorial#code-room_channel).

Listing 18: The updated Room channel.`app/channels/room_channel.rb`

```
class RoomChannel < ApplicationCable::Channel
  def subscribed
    stream_from "room_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end

```

The way to send data to the subscribers of a channel is to use the server’s `broadast`method in the controller:

```
ActionCable.server.broadcast 'room_channel', <data hash>

```

Here the data hash consists of the data being passed to the client. In the case of our chat app, it will be the content of the message and the username of the message’s user.

To use the `broadcast` method, we’ll update the Messages controller’s `create` action from [Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller) to replace the redirect/render with an Action Cable server broadcast, as shown in [Listing 19](https://www.learnenough.com/action-cable-tutorial#code-messages_controller_broadcast). (This handles only valid submissions; invalid (blank) submissions will simply be ignored.)

Listing 19: Broadcasting in the Messages controller.`app/controllers/messages_controller.rb`

```
class MessagesController < ApplicationController
  .
  .
  .
  def create
    message = current_user.messages.build(message_params)
    if message.save
      ActionCable.server.broadcast 'room_channel',
                                   content:  message.content,
                                   username: message.user.username
    end
  end
  .
  .
  .
end

```

With the design in [Listing 19](https://www.learnenough.com/action-cable-tutorial#code-messages_controller_broadcast), Action Cable will send a broadcast to all users subscribed to the `"room_channel"` stream, which will be received by the third piece of the puzzle, the client-side Room subscription, which in this case is the file `room.coffee`. The generated version of this file appears in [Listing 20](https://www.learnenough.com/action-cable-tutorial#code-generated_room_subscription).

Listing 20: The generated channel subscription.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    # Called when there's incoming data on the websocket for this channel

```

We see in the highlighted line that the `received` method has a `data` object, which automatically contains the data hash broadcast in [Listing 19](https://www.learnenough.com/action-cable-tutorial#code-messages_controller_broadcast). (We won’t need `connected` or `disconnected` in this tutorial.)

In order to see how everything fits together, let’s put in an alert in the `received`method. The message content is available via the attribute `data.content`, as shown in [Listing 21](https://www.learnenough.com/action-cable-tutorial#code-room_subscription_alert)

Listing 21: The Room subscription with an alert.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    alert data.content

```

To get this to work, we need one final bit of configuration, which is to tell our app about the [Action Cable server](https://github.com/rails/rails/tree/master/actioncable#running-the-cable-server), which is responsible for transmitting information between the local system and the main Rails server. By default, it runs at the URL /cable, and the way to link it to the main server is using the `mount` method, as shown in [Listing 22](https://www.learnenough.com/action-cable-tutorial#code-mount_action_cable).

Listing 22: Mounting the Action Cable server.`config/routes.rb`

```
Rails.application.routes.draw do
  root 'messages#index'
  resources :users
  resources :messages
  get    '/login',   to: 'sessions#new'
  post   '/login',   to: 'sessions#create'
  delete '/logout',  to: 'sessions#destroy'

  mount ActionCable.server, at: '/cable'
end

```

By the way, if you’re using a cloud IDE you will probably have to add an “allowed request origin” to the development environment. For example, on my Rails Tutorial workspace at Cloud9, my development configuration looks like [Listing 23](https://www.learnenough.com/action-cable-tutorial#code-action_cable_cloud_ide).

Listing 23: Action Cable configuration at Cloud9.`config/environments/development.rb`

```
Rails.application.configure do
  .
  .
  .
  # Add Cloud9 origin for Action Cable requests.
  config.action_cable.allowed_request_origins = [
    'https://rails-tutorial-mhartl.c9users.io' ]
end

```

By following this template and applying your technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)), you should be able to get things to work on your system.

At this point, entering some text into the chat box and clicking “Send” should raise an alert with the contents of the message, as shown in [Figure 23](https://www.learnenough.com/action-cable-tutorial#fig-hello_world_action_cable).

![images/figures/hello_world_action_cable](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v6bzqzqj30vi0nt75h.jpg)

Figure 23: Saying “hello, world!” using Action Cable.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_the_room_channel)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Replace on `data.content` with `data.username` in [Listing 21](https://www.learnenough.com/action-cable-tutorial#code-room_subscription_alert). Do you get the correct value?
2. Replace the `alert` in [Listing 21](https://www.learnenough.com/action-cable-tutorial#code-room_subscription_alert) with a call to `console.log`. Use your browser’s web inspector to confirm that the correct value appears in the console (`data.username` if you completed the previous exercise, `data.content`otherwise). If you don’t have any experience with web inspectors or consoles, use your technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)) to figure it out.

### [4.2Appending messages](https://www.learnenough.com/action-cable-tutorial#sec-appending_messages)

Now that we’ve got a proof-of-concept working, we’ll add the code necessary to append a message to the messages table. A first attempt appears in [Listing 24](https://www.learnenough.com/action-cable-tutorial#code-room_append).

Listing 24: Appending a message to the chat.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    unless data.content.blank?
      $('#messages-table').append '<div class="message">' +
        '<div class="message-user">' + data.username + ":" + '</div>' +
        '<div class="message-content">' + data.content + '</div>' + '</div>'

```

As we’ll see, the appended HTML in [Listing 24](https://www.learnenough.com/action-cable-tutorial#code-room_append) will work fine, but it’s effectively a duplicate of the message partial from [Listing 8](https://www.learnenough.com/action-cable-tutorial#code-message_partial). We’ll eliminate this duplication in [Section 5.3](https://www.learnenough.com/action-cable-tutorial#sec-message_rendering).

You can verify by submitting a message that it appears as desired, but in fact this is a cheat because the form from [Listing 6](https://www.learnenough.com/action-cable-tutorial#code-message_form) is currently submitting an ordinary HTTP POST request, which causes the page to refresh. In order to use Action Cable, we need to change the form to submit a *remote* request that submits an Ajax request without refreshing the page. As you may [recall](https://www.railstutorial.org/book/following_users#sec-a_working_follow_button_with_ajax) from the [Ruby on Rails Tutorial](http://railstutorial.org/), we can do this by including the `remote: true` option in the call to `form_for`. The result appears in [Listing 25](https://www.learnenough.com/action-cable-tutorial#code-message_form_remote).

Listing 25: Submitting the data remotely.`app/views/messages/_message_form.html.erb`

```
<div class="message-input">
  <%= form_for(@message, remote: true) do |f| %>
    <%= f.text_area :content %>
    <%= f.submit "Send" %>
  <% end %>
</div>

```

At this point, the basic Action Cable infrastructure is working: new messages appear not only for the submitting user ([Figure 24](https://www.learnenough.com/action-cable-tutorial#fig-message_appears)), but also across clients when, e.g., when Bob sends Alice a message ([Figure 25](https://www.learnenough.com/action-cable-tutorial#fig-instant_appearance)):

1. (client) Bob submits a new message using a remote form ([Listing 25](https://www.learnenough.com/action-cable-tutorial#code-message_form_remote)).
2. (server) The Messages controller ([Listing 19](https://www.learnenough.com/action-cable-tutorial#code-messages_controller_broadcast)) receives the submission, saves the message to the database, and broadcasts the result.
3. (client) Because every user is subscribed to the Room channel ([Listing 18](https://www.learnenough.com/action-cable-tutorial#code-room_channel)), each client receives the broadcast and executes the `received` method ([Listing 24](https://www.learnenough.com/action-cable-tutorial#code-room_append)), which appends the message HTML to the messages table for both Alice and Bob.

![images/figures/message_appears](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v6efsfvj30vi0nt40d.jpg)

Figure 24: The new message appears.

![images/figures/instant_appearance](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v6fpzi3j30q904ymxt.jpg)

Figure 25: Each new message appears instantly for other users.

The full flow of information is illustrated in [Figure 26](https://www.learnenough.com/action-cable-tutorial#fig-redis_messages). The middle layer is *Redis*, an in-memory data store that is important for scaling in production. We’ll discuss this issue in more detail in [Section 7](https://www.learnenough.com/action-cable-tutorial#sec-deploying_to_production).

![images/figures/redis_messages](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v6h69h7j31fk10smy2.jpg)

Figure 26: The flow of data when a message is created.

Unfortunately, the ordinary form submission method also leaves the contents of the message in the text box, as noted in [Figure 24](https://www.learnenough.com/action-cable-tutorial#fig-message_appears). In addition, chat programs usually let you submit messages just by hitting the Enter key. We’ll solve both of these issues in [Section 4.3](https://www.learnenough.com/action-cable-tutorial#sec-submitting_with_javascript) by handling form submission with JavaScript instead of Ruby.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_appending_messages)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Describe the steps taken when Alice sends a message to Bob.

### [4.3Submitting with JavaScript](https://www.learnenough.com/action-cable-tutorial#sec-submitting_with_javascript)

In order to handle chat message submissions with JavaScript, we’ll add some code to `room.coffee` to monitor the client’s browser for submissions.[13](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-13) Our method will be to define a `submit_message` function that will monitor the client’s browser and wait for the user to press the Enter key in the chat box.

By inspecting the chat app’s HTML with a web inspector, we find that the CSS id for the chat box textarea has CSS id `"message_content"`, as seen in [Figure 27](https://www.learnenough.com/action-cable-tutorial#fig-message_content_id).

![images/figures/message_content_id](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v6klzc4j30pw04rdh1.jpg)

Figure 27: The message content CSS id.

By monitoring the textarea for a so-called “keydown” event, we can arrange to perform particular actions when the user presses the Enter key. Each keydown corresponds to a numerical code, and the Enter code happens to be 13, so as a proof-of-concept we can output the event to the console log when this key is pressed:

```
submit_message = () ->
  $('#message_content').on 'keydown', (event) ->
    if event.keyCode is 13
      console.log(event)

```

If you feel like you wouldn’t been able to guess how to do this, it’s worth emphasizing that *I* didn’t know how to do it when I started making this tutorial. The code above is *exactly*the kind of thing you can just grab from a tutorial like this one, and in fact I grabbed it from a [writeup of DHH’s tutorial](https://hectorperezarenas.com/2015/12/26/rails-5-tutorial-how-to-create-a-chat-with-action-cable/).

In order to use the `submit_message` function, we have to call it after the DOM has loaded, and we saw in [Listing 12](https://www.learnenough.com/action-cable-tutorial#code-message_append) and [Listing 16](https://www.learnenough.com/action-cable-tutorial#code-message_appender_coffeescript) how to do this using `$(document).on ’turbolinks:load’`:

```
$(document).on 'turbolinks:load', ->
  submit_message()

```

Putting things together gives the code in [Listing 26](https://www.learnenough.com/action-cable-tutorial#code-submit_message_function).

Listing 26: Add a function to submit messages.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    $('#messages-table').append '<div class="message">' +
        '<div class="message-user">' + data.username + ":" + '</div>' +
        '<div class="message-content">' + data.content + '</div>' + '</div>'

$(document).on 'turbolinks:load', ->
  submit_message()

submit_message = () ->
  $('#message_content').on 'keydown', (event) ->
    if event.keyCode is 13
      console.log(event)

```

After including the code in [Listing 26](https://www.learnenough.com/action-cable-tutorial#code-submit_message_function), pressing Enter will display the `event` object in the browser’s console log. At this point, you should type in some text, press the Enter key (*not* the Send button), and then fire up the console inspector. Details will vary by browser, but you should be able to pick out most of the major elements, as shown in [Figure 28](https://www.learnenough.com/action-cable-tutorial#fig-console_log) (for Safari).

![images/figures/console_log](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v6uehdsj30rm07hmz4.jpg)

Figure 28: The console log after pressing Enter.

Now that we’ve verified our JavaScript is executing on the client, we can modify our `submit_message` function to actually submit the message. There are three steps:

1. Click to submit the form.
2. Clear the box after submission.
3. Ignore the Enter character.

Each of these has a one-line CoffeeScript translation. First, the way to click on the form is to select the input field with jQuery and then use the `click` method:

```
$('input').click()

```

We can clear the value of the box by setting the value of the event target to the empty string `""` as follows:

```
event.target.value = ""

```

Finally, in order to leave the box in its original state, we need to prevent the default behavior of adding a newline using the `preventDefault` method:

```
event.preventDefault()

```

This is a bit advanced, and you wouldn’t necessarily have been able to guess it, which is OK. In addition, clarifying the meaning of “default behavior” is included in the exercise ([Section 4.3.1](https://www.learnenough.com/action-cable-tutorial#sec-exercises_submitting_with_javascript)).

Putting everything together gives the `submit_message` method shown in [Listing 27](https://www.learnenough.com/action-cable-tutorial#code-working_submit_message).

Listing 27: A working message submission method.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
.
.
.
submit_message = () ->
  $('#message_content').on 'keydown', (event) ->
    if event.keyCode is 13
      $('input').click()
      event.target.value = ""
      event.preventDefault()

```

You should be able to verify that it’s working by entering some text in the chat box and hitting Enter. The result on my system appears in [Figure 29](https://www.learnenough.com/action-cable-tutorial#fig-submit_with_enter).

![images/figures/submit_with_enter](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v73b0p7j30vi0ntac0.jpg)

Figure 29: Submitting with the Enter key.

The chat is now working, but, as suggested in [Figure 29](https://www.learnenough.com/action-cable-tutorial#fig-submit_with_enter), for a fully chat-like design we should remove the Send button as well. (Indeed, because of the remote form the text remains in the box if we submit using the button, as seen in [Figure 24](https://www.learnenough.com/action-cable-tutorial#fig-message_appears).) It’s tempting to remove the `submit` tag (via `f.submit`) in [Listing 25](https://www.learnenough.com/action-cable-tutorial#code-message_form_remote), but this doesn’t work because the `click()` method needs something to click on. Instead, we can simply hide the button with CSS while extending the chat box textarea across the full width of the window.

The base app comes with a stylesheet written in [Sass](http://sass-lang.com/), which gets converted to CSS before being sent to the browser. The relevant portion of `main.sass` appears as in [Listing 28](https://www.learnenough.com/action-cable-tutorial#code-main_sass).[14](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-14)

Listing 28: The main Sass for message input.`app/assets/stylesheets/main.sass`

```
.
.
.
.message-input
  background-color: rgba(0,0,0,0.03)
  box-sizing: border-box
  height: 13%
  padding: 0 5px 5px
  form
    height: 100%
  textarea
    height: 100%
    width: 84.5%
  input
    float: right
    height: 100%
    vertical-align: top
    width: 14.5%

```

To extend the chat box and hide the Send button, we just need to change the textarea width to 100% and change the `input` rule to `display: none`, as shown in [Listing 29](https://www.learnenough.com/action-cable-tutorial#code-main_sass_display_none).The svelte new chat app appears as in [Figure 30](https://www.learnenough.com/action-cable-tutorial#fig-chat_app_no_send).

Listing 29: Extending the chat box and hiding the Send button.`app/assets/stylesheets/main.sass`

```
.
.
.
.message-input
  background-color: rgba(0,0,0,0.03)
  box-sizing: border-box
  height: 13%
  padding: 0 5px 5px
  form
    height: 100%
  textarea
    height: 100%
    width: 100%
  input
    display: none

```

![images/figures/chat_app_no_send](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v75n29pj30vi0nt3zx.jpg)

Figure 30: The chat app with hidden Send button.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_submitting_with_javascript)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. What happens if you remove the `preventDefault` line in [Listing 27](https://www.learnenough.com/action-cable-tutorial#code-working_submit_message)?
2. Remove the call to `f.submit` in [Listing 25](https://www.learnenough.com/action-cable-tutorial#code-message_form_remote) to see if `$(’input’).click()` still works.

### [4.4Updating the tests](https://www.learnenough.com/action-cable-tutorial#sec-updating_the_tests)

At this point, we have a functional chat app, but if you run the test suite you should find that it’s currently **red**:

Listing 30: **red**

```
$ rails test

```

This is because the test expects a `:redirect` status code, but the Ajax XHR request returns a `:success` status code instead.[15](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-15)

Updating the test with the right status code gives the result shown in [Listing 31](https://www.learnenough.com/action-cable-tutorial#code-test_xhr). Note that we’ve also taken this opportunity to add `xhr: true` to the form submission.Although the tests pass anyway, this setting better simulates the remote form defined in [Listing 25](https://www.learnenough.com/action-cable-tutorial#code-message_form_remote), which submits an XHR request instead of a normal `POST` request.

Listing 31: Getting the tests to **green**.`test/controllers/messages_controller_test.rb`

```
require 'test_helper'

class MessagesControllerTest < ActionDispatch::IntegrationTest

  def setup
    @user = users(:example)
  end

  test "index should require login" do
    get messages_url
    assert_redirected_to login_url
  end

  test "index" do
    login_as @user
    get messages_url
    assert_response :success
  end

  test "should handle invalid message" do
    login_as @user
    post messages_url, params: { message: { content: "" } }, xhr: true
    assert_response :success
  end

  test "should create valid message" do
    login_as @user
    post messages_url, params: { message: { content: "Lorem" } }, xhr: true
    assert_response :success
  end
end

```

At this point, the tests should be **green**:

Listing 32: **green**

```
$ rails test

```

## [5Basic enhancements](https://www.learnenough.com/action-cable-tutorial#sec-basic_enhancements)

Although the chat app is now working, there are a few basic enhancements we should add for convenience and security. These include rejecting unauthorized connections ([Section 5.1](https://www.learnenough.com/action-cable-tutorial#sec-login_protection)), auto-scrolling to the bottom of the message list ([Section 5.2](https://www.learnenough.com/action-cable-tutorial#sec-auto_scroll)), and eliminating duplication by reusing the message partial ([Section 5.3](https://www.learnenough.com/action-cable-tutorial#sec-message_rendering)).

### [5.1Login protection](https://www.learnenough.com/action-cable-tutorial#sec-login_protection)

We’re currently handling authorization in our chat application using a standard Rails-style before filter ([Listing 4](https://www.learnenough.com/action-cable-tutorial#code-messages_controller)), but there’s a way to require a valid user login at the Action Cable connection level as well. In addition to giving us an additional layer of security, this will create a `message_user` variable that we’ll put to use in [Section 6.2](https://www.learnenough.com/action-cable-tutorial#sec-at_mention_notifications).

The relevant file is `connection.rb` in the `app/channels/application_cable`directory. It defines a `Connection` class that gets defined when a new connection is made. By default, the file contains only an `ApplicationCable` module and the `Connection` class, but we can add in the necessary code to identify the user using the `identified_by` accessor (supplied by Action Cable) and by defining a `connect`method that gets called when the connection is made:

```
identified_by :message_user

def connect
  self.message_user = find_verified_user
end

```

We’ll also define a `find_verified_user` method that either returns the current logged-in user or rejects the connection:

```
def find_verified_user
  if logged_in?
    current_user
  else
    reject_unauthorized_connection
  end
end

```

Here the `reject_unauthorized_connection` method is supplied by Action Cable.

The full code appears as in [Listing 33](https://www.learnenough.com/action-cable-tutorial#code-reject_unauthorized_connection). [Listing 33](https://www.learnenough.com/action-cable-tutorial#code-reject_unauthorized_connection) is only a slight modification of the code in the [Action Cable documentation](http://edgeguides.rubyonrails.org/action_cable_overview.html), so don’t worry too much about understanding it in full. Its main purpose is to let us use `message_user` in places where `current_user`isn’t available, but as seen in the exercises ([Section 5.1.1](https://www.learnenough.com/action-cable-tutorial#sec-exercises_login_protection)) it also protects against unauthorized connections.

Listing 33: Rejecting unauthorized connections.`app/channels/application_cable/connection.rb`

```
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    include SessionsHelper

    identified_by :message_user

    def connect
      self.message_user = find_verified_user
    end

    private

      def find_verified_user
        if logged_in?
          current_user
        else
          reject_unauthorized_connection
        end
      end
  end
end

```

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_login_protection)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Because of the authorization before filter in [Listing 35](https://www.learnenough.com/action-cable-tutorial#code-render_message), it’s a little tricky to test that the system is really rejecting unauthorized connections. One way is to comment out the logged-in user filter and then change `logged_in?` to `false` in [Listing 33](https://www.learnenough.com/action-cable-tutorial#code-reject_unauthorized_connection). This forces the system to execute the `reject_unauthorized_connection` branch of the `if` statement in `find_verified_user`. Can you tell by looking at the Rails server log if it worked?

### [5.2Auto-scroll](https://www.learnenough.com/action-cable-tutorial#sec-auto_scroll)

A second enhancement is to add auto-scroll when loading the page or after submitting a message. One blemish in our application is that some messages are hidden when enough of them have been submitted to fill up the chat window. At that point, it becomes clear that we have a UI problem: users have to scroll to the bottom of the window by hand to see the latest message; otherwise, the full message list doesn’t show, as seen in [Figure 31](https://www.learnenough.com/action-cable-tutorial#fig-message_list_too_long).

![images/figures/message_list_too_long](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v7dkhjqj30vi0nttb0.jpg)

Figure 31: You currently have to scroll by hand.

The solution presented here might seem a little magical, but in fact it’s just the result of Googling around with Learn Enough cofounder Lee Donahoe until we cobbled together enough Stack Overflow hints to get it to work ([Figure 32](https://www.learnenough.com/action-cable-tutorial#fig-essential_stack_overflow)).[16](https://www.learnenough.com/action-cable-tutorial#cha-0_footnote-16) Bear that in mind if you get discouraged that you wouldn’t have been able to guess these yourself; neither could we.

![images/figures/essential_stack_overflow](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v7hjzepj30al0dwdk5.jpg)

Figure 32: Sometimes it’s the only way.

The technique we’ll use is called `scrollTop`, which forces the browser to scroll to a particular location:

```
$('#messages').scrollTop(...)

```

The location itself will be the height of the `#messages` div defined in [Listing 7](https://www.learnenough.com/action-cable-tutorial#code-messages_partial), which we can extract with jQuery as follows:

```
$('#messages')[0]

```

In other words, the div is the zeroth element of the object returned by the jQuery `$`operator applied to the `messages` id. To get this div’s height, we then call the `scrollHeight` method, like this:

```
$('#messages')[0].scrollHeight

```

Rolling everything together gives us the following `scroll_bottom` function:

```
scroll_bottom = () ->
  $('#messages').scrollTop($('#messages')[0].scrollHeight)

```

Our plan is to call this function on Turbolinks load so that the page scrolls to the latest message. We’ll add a second call to `scroll_bottom` to the end of the `received`callback so that each user ends up in the right place after someone submits a new message. The result appears in [Listing 34](https://www.learnenough.com/action-cable-tutorial#code-scroll_bottom).

Listing 34: Adding scrolling to the app.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    unless data.content.blank?
      $('#messages-table').append '<div class="message">' +
          '<div class="message-user">' + data.username + ":" + '</div>' +
          '<div class="message-content">' + data.content + '</div>' + '</div>'
      scroll_bottom()

$(document).on 'turbolinks:load', ->
  submit_message()
  scroll_bottom()

submit_message = () ->
  $('#message_content').on 'keydown', (event) ->
    if event.keyCode is 13
      $('input').click()
      event.target.value = ""
      event.preventDefault()

scroll_bottom = () ->
  $('#messages').scrollTop($('#messages')[0].scrollHeight)

```

With the code in [Listing 34](https://www.learnenough.com/action-cable-tutorial#code-scroll_bottom), the app should now scroll to the most recent chat message, both on load and after each message, as shown in [Figure 33](https://www.learnenough.com/action-cable-tutorial#fig-scroll_bottom).

![images/figures/scroll_bottom](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v7kokjdj30vi0nttak.jpg)

Figure 33: Auto-scrolling to the latest message.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_auto_scroll)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Use `console.log` to determine the value of the `scrollHeight` in your current application. *Hint*: In most browsers, you can use `console.log` and jQuery directly in the web inspector console.

### [5.3Message rendering](https://www.learnenough.com/action-cable-tutorial#sec-message_rendering)

Our final basic enhancement involves removing the redundancy that currently exists between the message partial in [Listing 8](https://www.learnenough.com/action-cable-tutorial#code-message_partial) and the message append in [Listing 24](https://www.learnenough.com/action-cable-tutorial#code-room_append). Such duplication is brittle and error-prone, requiring us to keep the two renderings in sync by hand. Instead, we’ll render the message in the Messages controller and pass the entire message HTML to `room.coffee` for display. This approach will also pay immediate dividends in [Section 6.1](https://www.learnenough.com/action-cable-tutorial#sec-markdown_support) when we add Markdown support to our application.

On the server side, our method will be to write a `render_message` function in the Messages controller to render the message with the existing template. We’ll then broadcast the entire rendered message to every user in the chat room. The rendering code just calls the `render` method, which can take a template as an argument

```
render(partial: 'message', locals: { message: message })

```

Then the broadcast will send the rendered message as follows:

```
ActionCable.server.broadcast 'room_channel',
                             message: render_message(message)

```

Putting these together gives the updated Messages controller shown in [Listing 35](https://www.learnenough.com/action-cable-tutorial#code-render_message).

Listing 35: Rendering the message in the controller.`app/controllers/messages_controller.rb`

```
class MessagesController < ApplicationController
  before_action :logged_in_user
  before_action :get_messages

  def index
  end

  def create
    message = current_user.messages.build(message_params)
    if message.save
      ActionCable.server.broadcast 'room_channel',
                                   message: render_message(message)
    end
  end

  private

    def get_messages
      @messages = Message.for_display
      @message  = current_user.messages.build
    end

    def message_params
      params.require(:message).permit(:content)
    end

    def render_message(message)
      render(partial: 'message', locals: { message: message })
    end
end

```

On the client side, now all we need to do is check if the `message` is blank (instead of checking the `content` as in [Listing 24](https://www.learnenough.com/action-cable-tutorial#code-room_append)) and, if not, append the full rendered message, as shown in [Listing 36](https://www.learnenough.com/action-cable-tutorial#code-room_append_message).

Listing 36: Rendering the full message HTML.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
  connected: ->
    # Called when the subscription is ready for use on the server

  disconnected: ->
    # Called when the subscription has been terminated by the server

  received: (data) ->
    unless data.message.blank?
      $('#messages-table').append data.message
      scroll_bottom()
.
.
.

```

At this point, the app should be working exactly as before ([Figure 34](https://www.learnenough.com/action-cable-tutorial#fig-same_rendering)).

![images/figures/same_rendering](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v7wcttlj30vi0nttak.jpg)

Figure 34: Rendering in the controller should work the same in the browser.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_message_rendering)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Make a gratuitous change to the message partial, such as adding a random word.Does the change appear for messages created using JavaScript?

## [6Advanced enhancements](https://www.learnenough.com/action-cable-tutorial#sec-advanced_enhancements)

Even though it’s simple, the app as it currently stands is a functional and scalable chat program, a perfectly reasonable minimum viable product. In this section, we’ll add just a couple of the many enhancements that are possible to build on this solid foundation.

### [6.1Markdown support](https://www.learnenough.com/action-cable-tutorial#sec-markdown_support)

Our first extension to the core chat app is support for *Markdown*, a lightweight and human-readable format that’s easy to convert to HTML. We’ll start by adding a Markdown converter called kramdown to our `Gemfile` ([Listing 37](https://www.learnenough.com/action-cable-tutorial#code-kramdown)).

Listing 37: Adding the `kramdown` gem.`Gemfile`

```
source 'https://rubygems.org'
.
.
.
gem 'jbuilder',                '2.4.1'
gem 'kramdown',                '1.12.0'
.
.
.

```

Then install as usual:

```
$ bundle install

```

By consulting the [kramdown documentation](http://kramdown.gettalong.org/documentation.html), we can learn how to use it to convert Markdown to HTML using `Kramdown::Document.new(...).to_html`:

```
$ rails console
>> text = "*emphasis*"
>> Kramdown::Document.new(text, input: 'GFM').to_html
=> "<p><em>emphasis</em></p>\n"

```

Here we’ve used an input option to use GitHub-flavored Markdown (GFM) instead of the kramdown default, mainly because GFM better handles the “fenced code” examples we’ll see in a moment.

For convenience, we’ll define a `markdown_to_html` converter in the Messages helper, as shown in [Listing 38](https://www.learnenough.com/action-cable-tutorial#code-markdown_to_html).

Listing 38: Defining a Markdown-to-HTML helper.`app/helpers/messages_helper.rb`

```
module MessagesHelper

  # Returns HTML from input text using GitHub-flavored Markdown.
  def markdown_to_html(text)
    Kramdown::Document.new(text, input: 'GFM').to_html
  end
end

```

Because we eliminated the HTML duplication in [Section 5.3](https://www.learnenough.com/action-cable-tutorial#sec-message_rendering), we need only one call to `markdown_to_html`, in the message partial. The result appears in [Listing 39](https://www.learnenough.com/action-cable-tutorial#code-markdown_partial).

Listing 39: Converting Markdown to HTML in the message partial.`app/views/messages/_message.html.erb`

```
<div class="message">
  <div class="message-user">
    <%= message.user.username %>:
  </div>
  <div class="message-content">
    <%= sanitize markdown_to_html(message.content) %>
  </div>
</div>

```

Note that [Listing 39](https://www.learnenough.com/action-cable-tutorial#code-markdown_partial) uses the `sanitize` method to deactivate potentially dangerous code, such as user-supplied JavaScript:

```
>> helper.sanitize "<script>dangerous code</script>"
=> "dangerous code"

```

The results for a simple Markdown line are shown in [Figure 35](https://www.learnenough.com/action-cable-tutorial#fig-markdown_text) and [Figure 36](https://www.learnenough.com/action-cable-tutorial#fig-markdown_result).

![images/figures/markdown_text](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v80fveuj30vi0ntq44.jpg)

Figure 35: Entering Markdown text.

![images/figures/markdown_result](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v8568s2j30vi0nt3zp.jpg)

Figure 36: The Markdown rendered as HTML.

One of the most useful applications of Markdown is formatting code, and in this context it’s useful to be able to enter multiple lines, like this:

```
​```
def greeting
  puts "hello, world!"
end
​```

```

Our app as currently designed allows such code to be pasted in, but we don’t have any way to enter it directly—as soon as the user hits the Enter key, the line gets submitted and rendered.

One common way to support multi-line entry, while also preserving the convenience of submitting new messages using the Enter key, is to use Shift-Enter to enter new lines. In other words, hitting Enter inputs the line, unless the user also holds down the Shift key.

Figuring out how to do this is an excellent exercise in technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)), so if you’d like to try your hand at it, you can Google around now. I personally had no idea how to do it when I decided to add this feature, but a little searching quickly turned up the answer.

The solution is to modify the `if` statement in [Listing 27](https://www.learnenough.com/action-cable-tutorial#code-working_submit_message) to input the textarea data if the event keycode is `13` (Enter) and is *not* the Shift key, which we can do as follows:

```
if event.keyCode is 13 && !event.shiftKey

```

Putting this into the Room CoffeeScript gives the code in [Listing 40](https://www.learnenough.com/action-cable-tutorial#code-not_shiftkey).

Listing 40: Using Shift-Enter to enter new lines.`app/assets/javascripts/channels/room.coffee`

```
App.room = App.cable.subscriptions.create "RoomChannel",
.
.
.
submit_message = () ->
  $('#message_content').on 'keydown', (event) ->
    if event.keyCode is 13 && !event.shiftKey
      $('input').click()
      event.target.value = ""
      event.preventDefault()

scroll_bottom = () ->
  $('#messages').scrollTop($('#messages')[0].scrollHeight)

```

In order to get the code to display nicely, we also need to make a minor update to the site CSS, as shown in [Listing 41](https://www.learnenough.com/action-cable-tutorial#code-code_css).

Listing 41: Adding some CSS (Sass) for code.`app/assets/stylesheets/main.sass`

```
.
.
.
.message-user
  color: #666
  font-size: 13px
  margin-right: 10px
  vertical-align: top

code
  font-family: monospace
  white-space: pre-wrap
  padding: 9px 15px
  display: inline-block
  background-color: #eee
.
.
.

```

With the code in [Listing 40](https://www.learnenough.com/action-cable-tutorial#code-not_shiftkey) and [Listing 41](https://www.learnenough.com/action-cable-tutorial#code-code_css), we can now use Shift-Enter to input the code for a friendly greeting, as shown in [Figure 37](https://www.learnenough.com/action-cable-tutorial#fig-markdown_greeting) and [Figure 38](https://www.learnenough.com/action-cable-tutorial#fig-html_greeting).

![images/figures/markdown_greeting](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v87regtj30vi0nt75l.jpg)

Figure 37: The Markdown with code for a greeting.

![images/figures/html_greeting](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v8c8l6wj30vi0nt0u6.jpg)

Figure 38: The rendered greeting.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_markdown_support)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Using blockquote syntax for Markdown, enter a multi-line quote into the chat using Shift-Enter. Does the display look good? Improve the display by appending the Sass in [Listing 42](https://www.learnenough.com/action-cable-tutorial#code-blockquote_sass) to the end of `main.sass`.
2. Confirm that you can include links in your chat messages. How would you make the link [*Learn Enough to Be Dangerous*](http://learnenough.com/) (including italics), linked to learnenough.com?
3. Use the Markdown image syntax to include the image at http://cdn.learnenough.com/archer_ants.jpg. Are you able to get a result that looks something like [Figure 39](https://www.learnenough.com/action-cable-tutorial#fig-archer_ants)?

Listing 42: Sass to improve blockquote styling.`app/assets/stylesheets/main.sass`

```
.
.
.
blockquote
  display: block
  margin-top: 1em
  margin-bottom: 1em
  margin-left: 40px
  margin-right: 40px
  background: #eee
  padding: 0.5em
  font-style: italic

```

![images/figures/archer_ants](https://ws2.sinaimg.cn/large/006tNc79gy1fm6v8mf7evj31190jpqga.jpg)

Figure 39: Alice and Bob discuss you get ants.

### [6.2At-mention notifications](https://www.learnenough.com/action-cable-tutorial#sec-at_mention_notifications)

Our second advanced enhancement is @mention notifications. As we’ll see, this is a highly instructive example, as it will require creating a stream on a per-user basis, which will help deepen our understanding of how Action Cable works.

The idea behind @mention notifications is to give users a way to grab the attention of other users in the chat. For example, if Bob types a message mentioning Alice by username, as in “@alice Good morning!” or “Good morning, @alice!”, then Alice should be alerted about being mentioned. Indeed, for simplicity our plan will be to use literal alerts, as in the JavaScript `alert` method we met in [Section 3](https://www.learnenough.com/action-cable-tutorial#sec-javascript_nanoslices).

Because the Room channel defined in [Listing 18](https://www.learnenough.com/action-cable-tutorial#code-room_channel) includes only a single global stream, currently any alerts will be sent to *all* users. In order to allow more targeted alerts, in this section we’ll create a separate stream for each Room channel user, and then send @mention notifications only to the channels of users who were mentioned.

The easiest way to create per-user streams is to scope them by the user id, as in

```
stream_from "room_channel_user_#{message_user.id}"

```

Here we’ve applied the `message_user` variable created when we protected the connection in [Listing 33](https://www.learnenough.com/action-cable-tutorial#code-reject_unauthorized_connection).

Applying this idea to the Room channel gives [Listing 43](https://www.learnenough.com/action-cable-tutorial#code-user_specific_room).

Listing 43: Subscribing to a user-specific room.`app/channels/room_channel.rb`

```
class RoomChannel < ApplicationCable::Channel
  def subscribed
    stream_from "room_channel"
    stream_from "room_channel_user_#{message_user.id}"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end
end

```

Our method for creating @mentions involves defining a `mentions` attribute on the Message model that returns a list of all the users mentioned in the message. We can build it up in the Rails console as follows:

```
$ rails console
>> content = "This mentions @alice and @bob, and also @nonexistent"

```

We can now scan the message content for mentions, using the username regex defined in the User model ([Listing 2](https://www.learnenough.com/action-cable-tutorial#code-user_model)):

```
>> content.scan(/@(#{User::NAME_REGEX})/)
=> [["alice"], ["bob"], ["nonexistent"]]

```

Note the use of parentheses in the `scan` regex, which captures just the username (without the `@`).

Next we flatten the nested array to get just an array of usernames:

```
>> content.scan(/@(#{User::NAME_REGEX})/).flatten
=> ["alice", "bob", "nonexistent"]

```

Then we map over the list to find by username:

```
>> content.scan(/@(#{User::NAME_REGEX})/).flatten.map do |username|
?>   User.find_by(username: username)
>> end
=> [#<User id: 1, username: "alice"...>, #<User id: 2, username: "bob"...>, nil]

```

The final element in the list is `nil`, indicating that there is no user with the username “nonexistent”. We can eliminate any such `nil` values using the `compact` method:

```
>> content.scan(/@(#{User::NAME_REGEX})/).flatten.map do |username|
?>   User.find_by(username: username)
>> end.compact
=> [#<User id: 1, username: "alice"...>, #<User id: 2, username: "bob"]

```

At this point we’re ready to define the `mentions` method, as shown in [Listing 44](https://www.learnenough.com/action-cable-tutorial#code-message_mentions).

Listing 44: Defining a `mentions` method.`app/models/message.rb`

```
class Message < ApplicationRecord
  belongs_to :user
  validates :content, presence: true
  scope :for_display, -> { order(:created_at).last(50) }

  # Returns a list of users @mentioned in message content.
  def mentions
    content.scan(/@(#{User::NAME_REGEX})/).flatten.map do |username|
      User.find_by(username: username)
    end.compact
  end
end

```

We can put the `mentions` method to work in the Messages controller by iterating through the mentions and broadcasting to the corresponding user’s personal stream, as shown in [Listing 45](https://www.learnenough.com/action-cable-tutorial#code-broadcast_mentions).

Listing 45: Broadcasting mentions.`app/controllers/messages_controller.rb`

```
class MessagesController < ApplicationController
  .
  .
  .
  def create
    message = current_user.messages.build(message_params)
    if message.save
      ActionCable.server.broadcast 'room_channel',
                                   message: render_message(message)
      message.mentions.each do |mention|
        ActionCable.server.broadcast "room_channel_user_#{mention.id}",
                                     mention: true
      end
    end
  end
  .
  .
  .
end

```

Note in [Listing 45](https://www.learnenough.com/action-cable-tutorial#code-broadcast_mentions) that we pass `mention: true` to indicate that the given user has an @mention, and should therefore receive an alert to that effect.

The alert itself is located on the client side in `room.coffee`, where we can use CoffeeScript to display an alert if `data.mention` is `true`:

```
alert("You have a new mention") if data.mention

```

This is pure CoffeeScript, by the way; the Ruby-like syntax (with the `if` statement after the main statement) isn’t supported by JavaScript.

Putting this alert in `room.coffee` gives the code in [Listing 46](https://www.learnenough.com/action-cable-tutorial#code-room_alert), which also takes care to test that `data.message` exists before calling the `blank?` method on it. (Figuring out exactly why this is necessary is left as an exercise ([Section 6.2.1](https://www.learnenough.com/action-cable-tutorial#sec-exercises_at_mention_notifications)).)

Listing 46: Add an @mention alert.`app/assets/javascripts/channels/room.coffee`

```
 1 App.room = App.cable.subscriptions.create "RoomChannel",
 2   connected: ->
 3     # Called when the subscription is ready for use on the server
 4
 5   disconnected: ->
 6     # Called when the subscription has been terminated by the server
 7
 8   received: (data) ->
 9     alert("You have a new mention") if data.mention
10     if (data.message && !data.message.blank?)
11       $('#messages-table').append data.message
12       scroll_bottom()
13   .
14   .
15   .

```

Including an @mention from Alice to Bob confirms that it’s working, as shown in [Figure 40](https://www.learnenough.com/action-cable-tutorial#fig-at_mention).

![images/figures/at_mention](https://ws3.sinaimg.cn/large/006tNc79gy1fm6v8qjccrj310b0i20u6.jpg)

Figure 40: Bob gets an alert from Alice’s @mention.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_at_mention_notifications)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Include the `SessionsHelper` (as in [Listing 33](https://www.learnenough.com/action-cable-tutorial#code-reject_unauthorized_connection)) and then try using `current_user` in [Listing 43](https://www.learnenough.com/action-cable-tutorial#code-user_specific_room). What error do you get?
2. Write some Message model tests for the `mentions` method.
3. Why can’t you use the original `unless` from [Listing 36](https://www.learnenough.com/action-cable-tutorial#code-room_append_message) in Line 10 of [Listing 46](https://www.learnenough.com/action-cable-tutorial#code-room_alert)?
4. Extend the @mention functionality to include the mentioning user in the alert, as in “You have a new message from @bob”.

## [7Deploying to production](https://www.learnenough.com/action-cable-tutorial#sec-deploying_to_production)

As a final step, we’ll deploy the chat app to production with Heroku. The only mildly tricky part is that we need to configure Redis.

As noted in [Section 4.2](https://www.learnenough.com/action-cable-tutorial#sec-appending_messages) and illustrated in [Figure 26](https://www.learnenough.com/action-cable-tutorial#fig-redis_messages), Redis is an in-memory data store used in production to facilitate scaling. The issue in the case of WebSockets is that a large number of clients could all connect to the same server, causing a problem with [load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)). By running all messages through Redis, we arrange to pool the outgoing data, alleviating the load on any given connection.

A detailed understanding of Redis is *not* necessary to use Action Cable, but many of the other resources out there will assume you’ve heard of it and know some basic vocabulary.In particular, some Action Cable resources refer to the “Redis Pub/Sub”, which is simply the publish (Pub)/subscribe (Sub) model that Redis uses. I don’t really understand how Pub/Sub works exactly, and both the [Redis docs](http://redis.io/topics/pubsub) and the [Wikipedia page](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) are rather obscure on the subject. Rather than study up on the subject just so I can explain it here, I’ll tell you the truth, which is that it doesn’t matter for our purposes. What does matter is that the app won’t run in production unless we include Redis.

Speaking of which, the way to use Redis in production is via the `redis` gem, which we’ll now add to the `Gemfile` ([Listing 47](https://www.learnenough.com/action-cable-tutorial#code-redis_gemfile)).

Listing 47: Adding the `redis` gem.`Gemfile`

```
source 'https://rubygems.org'
.
.
.
gem 'kramdown',                '1.10.0'
gem 'redis',                   '3.3.1'
.
.
.

```

Then install as usual:

```
$ bundle install

```

If you don’t already have a Heroku account, you can follow the [Heroku setup section](https://www.railstutorial.org/book/beginning#sec-heroku_setup) in the [*Ruby on Rails Tutorial*](http://railstutorial.org/book). Then create a new Heroku app at the command line using `heroku create`:

```
$ heroku create

```

To confugure Heroku to use Redis, all we need to do is include the `redistogo` addon:

```
$ heroku addons:create redistogo
Creating redistogo-clear-66322... done, (free)
Adding redistogo-clear-66322 to peaceful-basin-31856... done
Setting REDISTOGO_URL and restarting peaceful-basin-31856... done, v6

```

Next, we need to update our `cable.yml` configuration file with the right Redis URL. In other words, we need to update the production URL in the default config file ([Listing 48](https://www.learnenough.com/action-cable-tutorial#code-default_cable_yml)) with the Redis URL at Heroku.

Listing 48: The default Action Cable configuration file.`config/cable.yml`

```
development:
  adapter: async

test:
  adapter: async

production:
  adapter: redis
  url: redis://localhost:6379/1

```

We can get the production Redis URL from the Heroku configuration by [piping](https://www.learnenough.com/command-line-tutorial#sec-wordcount_and_pipes) the result of `heroku config` to `grep`:

```
$ heroku config | grep REDISTOGO_URL
REDISTOGO_URL: redis://redistogo:c9e21735e8cde14a6fe72@sculpin.redistogo.com:9426/

```

(Your URL will of course differ.) Then all we need to do is update the production URL in the config file, as shown in [Listing 49](https://www.learnenough.com/action-cable-tutorial#code-redis_cable_yml).

Listing 49: The default Action Cable configuration file.`config/cable.yml`

```
development:
  adapter: async

test:
  adapter: async

production:
  adapter: redis
  url: redis://redistogo:c9e21735e8cde14a6fe72@sculpin.redistogo.com:9426/

```

Finally, we need to configure the production environment with the proper Action Cable URL and allowed request origins, as shown in [Listing 50](https://www.learnenough.com/action-cable-tutorial#code-production_action_cable). (If you have trouble finding the right location in the file, just search for “action_cable” using your text editor.)

Listing 50: Configuring the production environment for Action Cable.`config/environments/production.rb`

```
Rails.application.configure do
  .
  .
  .
  config.action_cable.url = 'wss://peaceful-basin-31856.herokuapp.com/cable'
  config.action_cable.allowed_request_origins = [
    'https://peaceful-basin-31856.herokuapp.com' ]
  .
  .
  .
end

```

In [Listing 50](https://www.learnenough.com/action-cable-tutorial#code-production_action_cable), take care to use the Heroku URL for your app, not the one for mine.

At this point, we’re ready to deploy, so we’ll make a final commit to prepare for launch:

```
$ git add -A
$ git commit -m "Prep for launch"

```

In case you want to keep the `master` branch around for reference, we’ll deploy directly from the `action-cable` branch as follows:

```
$ git push heroku action-cable:master

```

You might notice some warnings during the deployment, which are safe to ignore. See [Professional-grade deployment](https://www.railstutorial.org/book/sign_up#sec-professional_grade_deployment) in the [*Ruby on Rails Tutorial*](http://railstutorial.org/book) if you want to address them.

At this point, all we need to do is migrate and seed the database:

```
$ heroku run rails db:migrate
$ heroku run rails db:seed

```

With that, our chat app should be running successfully in production! If you run into trouble (I certainly did), use your technical sophistication ([Box 1](https://www.learnenough.com/action-cable-tutorial#aside-technical_sophistication)) to resolve any issues.Once you’re done, your result should look something like [Figure 41](https://www.learnenough.com/action-cable-tutorial#fig-alice_production) and [Figure 42](https://www.learnenough.com/action-cable-tutorial#fig-bob_production).

![images/figures/alice_production](https://ws4.sinaimg.cn/large/006tNc79gy1fm6v8wz7gej311v0ik408.jpg)

Figure 41: A message to Alice in production.

![images/figures/bob_production](https://ws1.sinaimg.cn/large/006tNc79gy1fm6v90kg3gj311y0jq406.jpg)

Figure 42: A message back to Alice.

#### [Exercises](https://www.learnenough.com/action-cable-tutorial#sec-exercises_deploying_to_production)

Solutions to exercises are available for free at [learnenough.com/solutions](http://www.learnenough.com/solutions) with any Learn Enough purchase. To see other people’s answers and to record your own, join the [Learn Enough Society](http://learnenough.com/society) at [learnenough.com/society](http://learnenough.com/society).

1. Confirm that your production app can replicate the behavior shown in [Figure 41](https://www.learnenough.com/action-cable-tutorial#fig-alice_production)and [Figure 42](https://www.learnenough.com/action-cable-tutorial#fig-bob_production).
2. Using the Heroku console, add a third sample user named “Charlie”, and confirm using a third web browser that all three users can chat simultaneously.

## [8Conclusion](https://www.learnenough.com/action-cable-tutorial#sec-conclusion)

Congratulations! You now know enough Action Cable to be *dangerous*. You should now be ready for some of the other resources on the web:

- DHH’s intro to Action Cable ([video](https://www.youtube.com/watch?v=KJVTM7mE1Cc) and [writeup](https://hectorperezarenas.com/2015/12/26/rails-5-tutorial-how-to-create-a-chat-with-action-cable/))
- [Real-Time Rails](https://blog.heroku.com/real_time_rails_implementing_websockets_in_rails_5_with_action_cable) by Sophie DeBenedetto
- [Action Cable Overview](http://edgeguides.rubyonrails.org/action_cable_overview.html) from the Rails Guides
- The [Action Cable source](https://github.com/rails/rails/tree/master/actioncable)
- **(recommended)** [Building a chess server](http://jargon.io/joeyschoblaska/rails-5-chess-with-action-cable-websockets) by Joey Schoblaska

Action Cable is a new and fast-moving subject, so it’s also probably not a bad idea to Google around from time to time to see what’s new.

I wish you good luck using Action Cable to make real-time apps with Rails. I’m excited to see what you’ll build!
