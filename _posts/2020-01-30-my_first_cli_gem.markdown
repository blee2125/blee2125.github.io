---
layout: post
title:      "My first CLI Gem"
date:       2020-01-30 19:45:13 +0000
permalink:  my_first_cli_gem
---

For my CLI Gem project, I will be scraping the Top Companies List - 2019 from Y Combinator. I chose this website because they have some interesting information on different tech companies. For example, they have a brief description of the companies along with a link to apply for a jobs at any listed. 

When the user starts the program, it will list all of the companies and ask for input. The input is then processed by an if statement. If you type “exit”, you will end the program. If you type something not recognized, then it will say “Try again!” and ask for input again. Lastly, if you type a number within the given range, it will display that company. Below is an example of how a companies information would be displayed.

![image](https://github.com/blee2125/top-companies-y-combinator-cli-gem/blob/master/print%20company%20screenshot.png?raw=true)

I used Bundler to start my project because Bundler creates the environment for my code, saving me work.

```
bundle gem top_yc_companies
```
 After Bundler completes, I had to add cli.rb, company.rb and scraper.rb to the /lib directory. Next, I added top-yc-companies to /bin. This file tells the computer to use ruby to interpret the code, requires the environment file(/lib/top_yc_companies), and starts the program.


To find each element that I wanted to scrape, I used binding.pry and the inspect selector in Chrome. First, I had to make a method(list_page) to retrieve the website using Nokogiri, then, I added a method which would parse it into more useful data. Below is the scrape_page method. To find “tbody#main-companies tr”, I first used inspect in Chrome to get a general idea of where I wanted start. Then, I put binding.pry into scrape_page and began experimenting until I found something that worked. The <tr> elements are nested inside the <tbody> element that has an id of “main-companies"

```
  def scrape_page
    self.list_page.css("tbody#main-companies tr")
  end
```

Next, the program needs to iterate through the data and organize each company as individual objects. This is done by parsing the data again and passing it through initialize. Initialize then saves each company to the @@all array.

Below you can see the six different elements that are scraped and passed to initialize.

```
  def self.new_company(c)
    self.new(
      c.css("b.h4").text,		#=>name
      c.css("td.hq").text,		#=>hq
      c.css("a").attribute("href").text,	#=>website
      c.css("td.sectors").text,		#=>sector
      c.css("td.td-description p.margin-bottom-22").text,	#=>overview
      c.css("td.apply a").attribute("href")	#=>jobs_url
      )
  end
```

Below is initialize. It is triggered by self.new which passes each element as an argument with a default value of nil, just in case some information is unavailable.

```
  def initialize(name=nil, hq=nil, website=nil, sector=nil, overview=nil, jobs_url=nil)
    @name= name
    @hq= hq
    @website= website
    @sector= sector
    @overview= overview
    @jobs_url= jobs_url
    @@all << self
  end
```

Now that each company is saved as an object. We can use this program to experiment with the data and call on different companies to receive results like the first picture in this post.


