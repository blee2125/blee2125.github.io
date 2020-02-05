---
layout: post
title:      "Return Values"
date:       2020-02-05 13:58:19 +0000
permalink:  return_values
---


This is a brief blog post on return values in Ruby. Every method in Ruby returns a value by default.

A string will return a string

```
“String” #=> “String”
```

An equation will return the calculated results

```
2 + 2 #=> 4
```

A variable will return it’s value

```
Weather = “sunny” #=> “sunny”
```

A puts statement returns nil.

```
puts “The weather is sunny” #=> nil
```


By default, every method returns a value. The following method will return the last statement.

```
def laptop
	brand = “Apple”
	model = “Macbook Pro”
	screen_size = 13.3
end
#=> 13.3
```

Using the return keyword, you can choose what to return. This method will return brand. Because brand is a variable, it will return the value “Apple”.

```
def laptop
	brand = “Apple” 
	return brand
	model = “Macbook Pro”
	screen_size = 13.3
end
#=> “Apple”
```
