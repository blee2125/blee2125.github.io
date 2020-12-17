---
layout: post
title:      "My Javascript Project"
date:       2020-12-17 13:22:25 +0000
permalink:  my_javascript_project
---


For my single page javascript project with a ruby on rails backend, I decided to do a weather app where the user could save previous locations and settings.

When I first started the project, I had several features I wanted to put in but that would take forever because there is always some new feature that can be added after that one. So, I tried my best to stick with MVP(minimum viable product) principles. This will help to avoid getting side tracked. Some of the basic features of my app are…

* User can sign up, log in, and log out

* User can save settings, just dark mode at the moment

* User can save locations

* Look up weather by zipcode


Some features I would like to add...

* Hourly forecast

* 10day forecast

* Maps/ radar

* Let user delete locations

* Option to choose fahrenheit or celsius

* Look up locations by city name, then autocomplete as you type


For the weather, I needed to find an external api. Many of them cost money, but there are a few with free/limited services. The weather api I chose was openweathermaps.com. They limit you to 60 calls per minute and 1,000,000 calls per month. So for a personal project, this will be viable.

Dark mode is probably the most demanded feature at the current time. It is currently the only setting I have in my application is dark mode. When the user toggles dark mode, dark mode is saved server side to the user’s account. Below I used fetch which sends a PATCH request to the backend where rails will update the settings.

```
fetch(`http://${BACKEND_URL}/update`, {
	method: "PATCH",
	headers: {
		"Content-Type": "application/json",
		"Accept": "application/json",
	},
	body: JSON.stringify({username: currentUser.name, settings: settingsArray})
})
```
	

When the user logs in, the application will load there saved preference. It checks the user's saved settings and then applies them to the page.

```
if (currentUser.settings[0] === "dark") {
  document.body.classList.value === "dark-mode"
}
```



I enjoyed building this project and plan to add a few of the features listed above sometime in the near future. The thing I liked most about this project was using the external api to bring in real-time data. Of course it can be a little depressing when I look up the weather and it says cold and snowy.
