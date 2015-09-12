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

And Presto! You have succesfully created a Route, Controller and Action! Head over to the browser and take a look at the marvel that you have wrought with your fingertips.

End of tutorial!





