---
layout: post
title:      "Variables in Ruby"
date:       2020-02-05 14:04:32 +0000
permalink:  variables_in_ruby
---


There are four different variables. They are Local, Instance, Class and Global. I will cover the first three below.

A local variable is only available to the method it exists in. An example of a local variable would be: 

```
def print_year
	year = 2020
	puts year
end
#=> 2020
```

An instance variable starts with a single “@“. An instance variable’s value is unique to an object and is available across methods. Instance variables operate within the scope of self.

```
@name= “Joe”
def print_name
	puts “Hello #{@name}!”
end
#=> Hello Joe!
```

A class variable starts with “@@“. Unlike instance variables, a class variable is available across different objects. A class variable must be initialized.

```
class Dog
  @@dogs= []
  def initialize(name)
    @name= name
    @@dogs << self
  end
  def self.all
    @@dogs
  end
end
```
