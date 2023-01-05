# CHAPTER 17.1
# Python Scopes

  We've lightly touched on this already, but when working with any programming language, the variables and objects that we're working with are only accessible within certain scopes. In this lesson, we'll take a closer look at how scopes work and when our variables might not be what we expect them to be.

  What is a Scope?
  When we say that we're working in a different "scope" in Python, we mean that we're within the boundaries of a function or a class. This is important because while within the body of a function or class, the variables that we create are not automatically accessible outside of that context. Let's create a new file called scopes.py so that we can experiment with how scopes work. To start, let's see how variables work when dealing with conditionals and loops.

   
  ```
  scopes.py

  if 1 < 2:
      x = 5

  while x < 6:
      print(x)
      x += 1

  print(x) 
  ```
  

  Here we're creating a variable (x=5) within the body of a conditional (if 1 < 2:1). Afterward, we attempt to access that variable within the context of a loop (while x < 6:) and at the highest level of our script. Will this work? Let's find out by running this through the interpreter:

   
  ```
  $ python3.7 scopes.py
  5
  6
  $ 
  ```
  

  We didn't run into an error because conditionals and loops do not create scopes. Now, let's change our conditional to be a function instead.

   
  ```
  scopes.py

  def set_x():
      x = 5

  set_x()

  while x < 6:
      print(x)
      x += 1

  print(x) 
  ```
  

  Now if we run this we'll see the following:

   
  ```
  $ python3.7 scopes.py
  Traceback (most recent call last):
    File "scopes.py", line 7, in <module>
      while x < 6:
  NameError: name 'x' is not defined
  $ 
  ```
  

  We see this error because x is defined within the set_x function and only exists during the execution of the function.
  
# CHAPTER 17.2
# Name Hiding (Shadowing)

  Now that we've looked at how scopes work initially, we're ready to look at what happens when we have a function
  parameter that is the same as a variable that exists at a higher level. This is sometimes called shadowing or name hiding.

  Name Hiding in Action
  We know that functions create scopes. But, what happens when a parameter name is the same as a variable that has already been defined? Let's continue using scopes.py to see what happens when we set y before we define the set_x function, and then change our function to have a y parameter:

   
  ```
  scopes.py

  y = 5

  def set_x(y):
      print("Inner y:", y)
      x = y
      y = x

  set_x(10)
  print("Outer y:", y) 
  ```
  

  Now if we run this, we'll see the following:

   
  ```
  $ python3.7 scopes.py
  Inner y: 10
  Outer y: 5 
  ```
  

  Since our function defines the y parameter, it's as though the outer y variable doesn't exist within the set_x function. Name hiding makes it possible for us to be confident that our parameters won't be affected by values at a higher scope. That doesn't mean that name hiding is something that we should always use though because it can make our code a little harder for people to understand.
  
  
# CHAPTER 17.3
# The `global` Keyword

  Occasionally, we want to be able to modify a global variable from within a more specific context. In this situation, Python provides us with the global keyword. In this lesson, we'll learn how to use the global keyword.

  Modifying the Global State from a Nested Scope
  If we would like one of our functions to have the side effect of changing or creating a global variable, we can utilize the global statement. This isn't something that we'll use all that often since it is better to keep global state to a minimum as we start working on larger and more complex programs. But it is useful now and then. Let's modify scopes.py so that we can change the global y variable from within our set_x function:

   
  ```
  scopes.py

  y = 5

  def set_x(y):
      print("Inner y:", y)
      x = y
      global y
      y = x


  set_x(10)
  print("Outer y:", y) 
  ```
  

  If we run this, we should see the following:

   
  ```
  python3.7 scopes.py
    File "scopes.py", line 7
      global y
      ^
  SyntaxError: name 'y' is parameter and global 
  ```
  

  It's important to know that we can't utilize the global statement if we have a parameter with the same name. Let's change our parameter to be z before running this again:

   
  ```
  scopes.py

  y = 5

  def set_x(z):
      x = z
      global y
      global a
      y = x
      a = 7

  print("y Before set_x:", y)
  set_x(10)
  print("y After set_x:", y)
  print("a After set_x:", a) 
  ```
  

  We've also created a global variable from within our set_x function called a. This variable won't be available before the first time that set_x is called, but we should be able to print it after we've called our function for the first time. Let's run scopes.py again:

   
  ```
  $ python3.7 scopes.py
  y Before set_x: 5
  y After set_x: 10
  a After set_x: 7 
  ```
  

  This example shows how potentially confusing using global can be. We have a function called set_x that will change the global state for the variable y. Someone who didn't write this code could be completely confused as to why the value of the variable y that they've been working with was changed right out from under them. Keep this in mind when considering whether or not it's a good idea to use the global statement.

