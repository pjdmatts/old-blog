---
layout: post
title:  "Rails: Create a route, controller, and action"
date:   2015-09-12 12:00:00
categories: coding
---

I had been looking at the [Thoughtbot Rails Trail Map](https://github.com/thoughtbot/trail-map/blob/master/rails.md) and thought it would be useful to dig into each step in some detail.

First we will *do* some creating, and then we can step back and think about what we *did*.

Go to a safe place in the terminal, a folder where you don't mind making a mess or leaving half built starter projects laying around, and do this:

```
$ rails new create_route_controller_action
```

```
$ cd create_route_controller_action
```

```
$ bin/rails generate controller middleman index
```

In your newly created app navigate to config/routes.rb and replace

```
get 'middleman/index'
```

with

```
root ‘middleman#index'
```

Back in the comman line run

```
$ bin/rails s
```

And Presto! You have succesfully created a Route, Controller and Action! 

Head over to ```localhost``` in the browser and take a look at the marvel that you have wrought with your fingertips. End of tutorial.

But what did we actually *do*?

##About Routes, Controllers and Actions##

###What is a Route?###

The router acts as a signpost telling HTTP requests coming from the users browser where to go in the application. Just like arriving in a new country: Citizens should go to this desk, non-citizens should go to another one. 

HTTP requests come in the form of the stantdard HTTP *verbs* (POST, GET, PUT, DELETE etc) and the router matches the request to a pattern so see where to send it. For example if the request is in the form 

```
GET /travellers/22
```

and if the first match to the pattern in routes.rb is

```
get '/travellers/:id', to: 'travellers#show'
```

the request is sent to the travellers *controller's* show *action* with { id: '22' } stored in the applications params hash.

*Routes get requests to where they need to go, which is the correct Controller and Action.*

###How to make a Route###

We did it above with ```root ‘middleman#index'``` in the routes.rb file. In that case we set the *root route*, a default route that handles requests for the main page of the application (e.g. www.stunningawesomeness.com). This route sends requests to the ```index``` action inside the ```middleman``` controller.

Then there are other routes for other parts of your application. One approach to making a route is to specify a route directly. For example 

```
get '/travellers/:id', to: 'travellers#show'
```

The other (usually preferred) approach is to create what are referred to as RESTful routes.

REST is an acronym for Representational State Transfer. It's an idea in software architecture that talks about where to put things in a networked system (like the web) and how to talk to them. Something is RESTful if it arranges the different URI's (e.g. http://example.com/frequentFlyers/) and HTTP methods (or verbs) in a certain way. You can learn more by starting with [this section](http://guides.rubyonrails.org/routing.html#resource-routing-the-rails-default) of the Rails Guides, but the main points to grasp center around *resources* and the things you can do with them.

Your application has objects (usually things in the database, but not always) that you want to let users get to and *do things to*. These objects are your Resources. (e.g. users, posts). 

The things users do to them usually fall into the categories of Create, Read, Update and Delete (or CRUD) in database speak, or the HTTP methods (verbs) in web speak.

A RESTful route in a rails app maps the HTTP verb, CRUD operations and URL representation of resources in a pre-defined way.

For example.

```
resources :travellers
```

in the routes.rb file creates seven different RESTful routes in the application, all mapping to actions in the travellers controller:

HTTP Verb| Path       | Controller#Action| Used for (CRUD operation) |
:------- | :--------- | :--------------- | :------------------------ |
GET      | /travellers| travellers#index | display a list of all travellers (Read)
GET | /travellers/new | travellers#new | return an HTML form for creating new travellers (Create)
POST | /travellers | travellers#create | create a new traveller (Create)
GET | /travellers/:id | travellers#show | display a specific traveller (Read)
GET | /travellers/:id/edit | travellers#edit | return an HTML form for editing a traveller (Update)
PATCH/PUT  | /travellers/:id | travellers#update | update a specific traveller (Update)
DELETE | /travellers/:id  | travellers#destroy | delete a specific traveller (Delete)
 | | |

This single entry in the routing file takes care of the majority of the routes you would want to associate with the travellers controller.


###What is a Controller?###

In an earlier analogy the route is a map telling arriving travellers which immigration desk to go to. Extending the analogy we can think of the Controller as the officer at the desk that greats each traveller (browser request) after the map (the router) has sent them there. The Officer takes the travellers credentials (the parameters, if any, in the URL) and can look things up (by asking questions of the Model). 

The Controller understands what the router has sent it and knows how to look things up in the Model (but the Model does the application logic 'work' behind the scenes). Depending on what the Model responds with the Controller knows with Views to render (but the Views does the HTML 'work' behind the scenes). 

Hopefully if the request and the parameters check out the Controller stamps the passport and the nervous traveller gets to go on their way...


###How to make a Controller###

To create a new controller, you need to run the "controller" generator and tell it you want a controller called "travellers" with an action named "index", like so:

```
$ bin/rails generate controller travellers index
```

Names matter in Rails, which makes certain assumptions about what you are going to do in order to help get things running. In this instance Rails assumes that you are going to give controllers and actions the same names you do in the routing file.


###What is an Action?###

An Action is a method inside a controller - Actions are the parts of the controller that 'do' things. For example there might be a 'stamp_passport' Action and a 'pull_to_one_side_for_search' Action, but usually you will see Actions that correspond to CRUD operations such as 'index' and 'destroy'. 

###How to make an Action###

In the step where we called generate to create our controller we also specify which action(s) we want to be created. Actions start out simple after running generate:

{% highlight ruby %}
class TravellersController < ApplicationController
  def index
  end
end
{% endhighlight %}

And we can add additional functionality to them:

{% highlight ruby %}
class TravellersController < ApplicationController
  def index
    @travellers = Traveller.all
  end
end
{% endhighlight %}

In this example we have found all of the travellers in the database (with Traveller.all) and assigned them to the *instance variable* @travellers.

###Wrapping Up###

Routes, Controllers and Actions are key building blocks in a Rails application. This short introduction has only just scratched the surface. Now that you have some of the concepts aligned a good place to go next is to read the specific sections for these aspects of Rails in the Rails Guides:

[Routing](http://guides.rubyonrails.org/routing.html)

[Controllers and Actions](http://guides.rubyonrails.org/action_controller_overview.html)