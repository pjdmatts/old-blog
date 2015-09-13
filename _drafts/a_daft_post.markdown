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

HTTP Verb  | Path| Controller#Action| Used for (CRUD operation)
:---| :---- | :---- | :----
GET  | /travellers| travellers#index | display a list of all travellers (Read)
GET | /travellers/new | travellers#new | return an HTML form for creating new travellers (Create)
POST | /travellers | travellers#create | create a new traveller (Create)
GET | /travellers/:id | travellers#show | display a specific traveller (Read)
GET | /travellers/:id/edit | travellers#edit | return an HTML form for editing a traveller (Update)
PATCH/PUT  | /travellers/:id | travellers#update | update a specific traveller (Update)
DELETE | /travellers/:id  | travellers#destroy | delete a specific traveller (Delete)
 | | |

This single entry in the routing file takes care of the majority of the routes you would want to associate with the travellers controller.


###What is a Controller?###



###How to make a Controller###



###What is an Action?###



###How to make an Action###









