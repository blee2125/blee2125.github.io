---
layout: post
title:      "My Sinatra Recipe App"
date:       2020-05-12 10:26:41 -0400
permalink:  my_sinatra_recipe_app
---


For my Sinatra project, I decided to do an app that would keep track of a user’s recipes. There are several recipe apps out there, but I wanted to make my own. I find it can be difficult to keep track of recipes. I get some recipes online and many from cookbooks. With some of my cookbooks being several decades old, a digital version of a recipe can help me continue to make that recipe and reduce wear and tear on my cookbook.

## Models

For this app, I currently only have two models, the user and the recipe. 

The recipe model belongs_to the user. The user model has_many recipes, has_secure_password, and validates the username for uniqueness. To validate the username, I used Active Record’s built-in validation helpers. Active Record checks the username, first for it being present, second, that it is unique. This is important because we only want valid data in the database and we can’t have multiple users using the same username. Below is the code used. 

```
    class User < ActiveRecord::Base
        validates :username, :presence => true,
        :uniqueness => true
```

## Views

Originally, I was going to use sinatra-flash to display messages to the user. I changed my mind after making a couple of messages because they felt more annoying than helpful. When the user creates a new recipe, the controller redirects them to the recipe just created. This would display a message “Recipe created”. They don’t need a message telling them the recipe is saved when it’s right there. I wanted a different form of feedback because feedback is important, so I instead added “required” to my erb forms to have a popup that says “Please fill out this field.”. It’s useful because it also doesn’t let you submit the form unless everything is filled in.

![](https://imgur.com/btItsaT.png)

## Controller

When creating a new recipe, the recipe_controller also checks the required fields for data. If there is any missing, it will redirect you to '/recipes/new' and have you fill out the form again. This doesn't trigger because the form "required" the fields be filled before you can click submit. Below is the code used.

```
if params[:recipe_name] == "" || params[:ingredients] == "" || params[:directions] == ""
    redirect to '/recipes/new'
else
    @recipe= current_user.recipes.create(name: params[:recipe_name],
        ingredients: params[:ingredients],
        directions: params[:directions])
        redirect to '/recipes'
end
```

One last thing I wanted to do is allow a user to view recipes created by other users. On the index page, it lists every recipe in the database. People typically share their recipes and this makes that easier.
