---
layout: post
title:      "Rails Portfolio Project - Beer Review"
date:       2020-08-06 21:28:13 +0000
permalink:  rails_portfolio_project_-_beer_review
---


This is my first project called Beer Review. It is basically a database of different beers and their attributes. The users can leave a recommendation and a comment for each beer. The idea behind this app, is that the users will be able to browse the list of beers and discover new beers based on input from other users.



##Uploading pictures with Active Storage

One feature that I was excited to include in my project was pictures uploaded by the user using Active Storage. Active Storage is a gem that is built in to Rails. Many of the breweries go above and beyond with artwork on the labels and including a way to upload and display a picture would be needed.

Setup is simple.

```
rails active_storage:install
#then
rails db:migrate
```

This will create a migration file with two table, active_storage_blobs and active_storage_attachments. Then in the config files you can choose where to store file(locally or in the cloud). By default, it is setup for local storage. The next step is to add a picture to the model. In this case, the following code will be added to the Beer model.

```
has_one_attached :beer_picture
```
If you wanted multiple photos, change one to many.

To upload a photo, all I had to do is add the following code to views/beers/_form.html.erb which allows you to upload when creating a new beer or editing an existing beer.

```
<%= f.label :beer_picture, "Upload a Picture" %>
<%= f.file_field :beer_picture %>
```

Below is the results.

![](https://imgur.com/ChwoX5q.png)

##Displaying the uploaded picture

```
<% if beer.beer_picture.attached? %>
    <img src="<%= url_for(beer.beer_picture) %>" id="beerpicindex">
<% end %>
```

The above code, on the first line, first checks if the picture is attached. If it is, then the picture is displayed. If the beer doesn't have a picture, then nothing is displayed. This is important that nothing is displayed because if there is no picture, the broken photo link is unnecessary. Attached? is a built in method included with Active Storage.

