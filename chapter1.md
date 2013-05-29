## Variables

**Local Variables:** Local variables are the variables that are defined in a method. Local variables are not available outside the method. You will see more detail about method in subsequent chapter. Local variables begin with a lowercase letter or _.

**Instance Variables:** Instance variables are available across methods for any particular instance or object. That means that instance variables change from object to object. Instance variables are preceded by the at sign (@) followed by the variable name.

**Class Variables:** Class variables are available across different objects. A class variable belongs to the class and is a characteristic of a class. They are preceded by the sign @@ and are followed by the variable name.

**Global Variables:** Class variables are not available across classes. If you want to have a single variable, which is available across classes, you need to define a global variable. The global variables are always preceded by the dollar sign ($).


## Class Vs. Instanace Methods

### Generally speaking:

- ````Class Methods```` can only be called on a class itself without creating an instance of the class (i.e. an object)
- ````Instance Methods```` are only available to an instance of the class (i.e. an object)


### Examples

````ruby
Class Example
	def self.bar
		puts "Class Method"
	end

	def baz
		puts "Instance Method"
	end
end

# Exmaples:
# 1. Calling Methods directly on the Class
# Calling the Class Method
# Works! You're calling directly on the class (not an instance aka object of the class)
Example.bar # => Class Method

# Calling the Instance Method
# Fail! Not allowed to call Instance Method directly from the class 
Example.baz # => NoMethodError: undefined method ‘baz’ for Example:Class

# 2. Calling Methods on an instance/object of the Class
# Create/Instantiate a new Example Class (i.e. create an "Example object")
exampleObject = Example.new

# Calling the Class Method
# Fail! You can't do this on an object...only directly on a class itself
exampleObject.bar # => NoMethodError: undefined method ‘bar’ for #<Example:0x1e820>

# Calling the Instance Method
# Works! You're allowed to call this on an object (i.e. an instance of a class)
exampleOjbect.baz # => Instance Method

````

## More Examples and getting deeper into ````Class```` and ````Instance```` Methods

Since ````Class Methods```` are only callable/invoked/used directly on a class - we can take advantage of this inside of the class or when extending from another class.

### Examples
````ruby
# create a class called Example1
class Example1
	# create a Class Method called 'bar'.  
	# What makes it a Class Method is by appending 'self' and a '.' to the method name
	def self.bar
		puts "Hello"
	end
end

# create another class called Example2 that extends from Example1
class Example2 < Example
	# Call the bar method that was orginally written in the Example1 class inside of the new Example2 class
	bar
end

# Call Example2 class
Example2 # => Hello
````

In the above example, "````Hello````" is printed/outputed because the method ````bar```` was called inside the ````Example2 class````.  

In essence you are calling the ````Example2 class```` as if it were a function (you're not really but use this as an anology).  Following this anology/idea, ````Example2```` is internally calling a function called ````bar```` (which we inherited from the first ````Example1 class````).  As a result ````bar```` has only one purpose - to print/output the word "````Hello````".

This only works because the ````bar```` method was originally written as a ````Class Method````.  In other words it was written like ````self.methodName````, and in our case specifically ````self.bar````.  

All together a ````Class Method```` gernerically looks like this:

````ruby
# Generic Example
class SomeClass
	# Creating a class method => similar to writing a 'normal' method but prepending 'self.'
	def self.someMethod
		# do something awesome here
	end
end
````

This means it can just be called directly on the class name/type itself directly without creating/instantiating an instance of that class.  So again to drill the idea home, in our case we could call 'bar' on either the ````Exmaple1```` or ````Example2```` class directly.

````ruby
Example1.bar # => 'Hello'
Example2.bar # => 'Hello' because we've inherited the 'bar' method from 'Example1' 
````

Contrast this to an ````Instance Method````.

````ruby
# create a third class called Example3
class Example3
	# create an Instance Method called jaz
	# remember that we're *NOT* appending 'self' and a '.' to the method name
	def jaz
		puts "Goodbye"
	end
end

# create a fourth class called Example4 that extends from Example3
class Example4 < Example3
	# call 'jaz' that we've inherited from Example3
	jaz
end

#call Example4 class directly
Example4 # => You get an error message instead of seeing 'Goodbye'
````

So...what just happend?

## Public vs. Protected vs. Private

