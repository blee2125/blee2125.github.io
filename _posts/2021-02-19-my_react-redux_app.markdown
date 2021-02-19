---
layout: post
title:      "My React-Redux App"
date:       2021-02-19 11:12:55 -0500
permalink:  my_react-redux_app
---


For my React-Redux app, I decided to make an app that would manage storage units. I made my decision because I know someone who is thinking about building storage units to rent, so this could have potential real-world uses. The program is intended for just owner/landlord of the storage units to be able to view the app. Currently, the owner can add new storage units and they can also delete existing units. In the future, I would like to give more attributes the units and  add a way to modify the units. The last thing they can do is rent the units via a form and then it displays the rental forms below the form.

One requirement of this project is to have multiply routes rendered by the browser instead of the server. To do this, I needed to import a few functions from "react-router-dom". In index.js, I had to import "BrowserRouter as Router" from "react-router-dom". This sets up the <Router /> parent element for the the routes. Each route is then declared with the <Route /> element which are  children elements to <Switch />. Below is the code from my project showing the switch setup.

```
          <Switch>
                <Route path='/rentalunits' render={() => <RentalUnits data={this.props} />} />
                <Route path='/addrentalunit' component={NewRentalUnit} />
                <Route path='/rentalform' render={() => <RentalFormsContainer data={this.props} />}/>                    
          </Switch>
```

Switch looks through the <Route /> elements and matches it with the current url. After a match, each route renders as the appropriate component or container. NavBar.js imports the <Link /> element which will "link" to the given route. Client-side routing helps speed up page load time because it doesn't require us to contact the external server every time. We only need to contact the server to first load the application and the second reason to contact the server is to relay changes to data.
