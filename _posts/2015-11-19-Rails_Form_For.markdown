---
layout: post
title:  "Rails: Form-For"
date:   2015-11-18 15:33:00
categories: coding
---

Rails ships with some handy form helpers: form_for and form_tag. The form_for method is intended for when you are building a form for a model object, whereas the form form_tag method is for a situation where you don’t need to update the database (sometimes referred to as an ‘unbounded form’ because the form is not bound to a model object: A good example might be a search).

To use the form_for tag you pass in the model object (the table you want to access) and create a set of labels and fields for each column in your table:

{% highlight ruby %}
<%= form_for(@product) do |f| %>
    <%= f.label :name %>
    <%= f.text_field :name %>

    <%= f.label :price %>
    <%= f.number_field :price %>

    <%= f.submit “Create” %>
<% end %>
{% endhighlight %}

Working with the form_tag method is a bit more involved, because you need to specify the path that you will be working with and the method to use.

I have not figured out a good example for form_tag yet - more on this later.
