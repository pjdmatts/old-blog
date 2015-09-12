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
GET /tourists/22
```

The routes.rb file defined the *routes*. If the first match to the pattern is

```
get '/toursits/:id', to: 'tourists#show'
```

the request is sent to the tourists controller's show action with { id: '22' } stored in the applications params hash.

*Routes get requests to where they need to go, which is the correct Controller and Action.*

###How to make a Route###



###What is a Controller?###



###How to make a Controller###



###What is an Action?###



###How to make an Action###









