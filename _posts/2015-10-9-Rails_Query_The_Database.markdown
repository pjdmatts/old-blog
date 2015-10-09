---
layout: post
title:  "Rails: Query The Database"
date:   2015-10-09 12:24:00
categories: coding
---

The controllers job is to go fetch data to ‘give’ to the view.

If the process of getting the data is not complicated (it can be done with built in Rails query methods) then this is done in the controller by calling methods on Model objects

(If the process is more complicated this can be done with scopes - which basically expand the built in query methods into something more complicated over in the model, and then this modified query method can be called from the controller. But this is a bit beyond the scope of these notes at the moment.)

Active Record is the part of Rails that is used to ‘talk to’ the database. Active Record uses something called an Object Relational Mapper (ORM) that takes the entries in the database tables and matches them up (maps them) to Objects in the Model. Having things in the database represented as objects allows our code makes it a lot easier to talk to the database.  Queries start in the controller and go through the classes set up in the Model. Active Record handles the actual database transactions for us.

Say we needed an array containing the titles of all the blog posts, we can simply type Post.all and Active Record gets us an array of Post objects.

Here are some more examples of queries that start in the controller. These ones are taken from my ‘Pinteresting’ [repo](https://github.com/pjdmatts/pinteresting) (I recently completed the One Month Rails course and this is what Mattan has you build).

In the first example the Index action in the Pins Controller is going and getting all of the pins for us (thats the Pin.all part. Additional methods are called to set the order in which the results are returned and to paginate the results):

```
def index

    @pins = Pin.all.order("created_at DESC").paginate(:page => params[:page], :per_page => 8)
    
end
```

```

In the second example a private method called set_pin is searching for one specific pin (identified by the parameters set in the url):

```
def set_pin

      @pin = Pin.find_by(id: params[:id])

end
```

In short, here is how to query the database:

1, Make a controller
2, Make an action inside that controller
3, Within the action call query methods on the objects in the Model.
4, If things get complicated move the logic into the Model (e.g. by using scopes).

