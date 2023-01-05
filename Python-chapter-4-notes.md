# CHAPTER 4.1 c
  # Comments

  When writing scripts, we often want to leave ourselves notes or explanations. Python (along with most scripting languages) uses the # character to signify that the line should be ignored and not executed.

  Single Line Comment
  We can comment out a whole line:

  ```# This is a full line comment```


  or we can comment at the end of a line:

  2 + 2 # This will add the numbers


  What About Block Comments?
  Python does not have the concept of block commenting that you may have encountered in other languages.
  Many people mistake a triple quoted string as being a comment, but it is not. It's a multi-line string.
  That being said, multi-line strings can functionally work like comments, but they will still be allocated
  into memory.
  ```
  """
  This is not a block comment,
  but it will still work when you need
  for some lines of code to not execute.
  """ 
  ```
  
# CHAPTER 4.2
# Variables and the Assignment Operator
  Almost any script that we write will need to provide a way for us to hold onto information for use later on. That's where variables come into play.

  Working with Variables
  We can assign a value to a variable by using a single = and we don't need to (nor can we) specify the type of the variable.
  ```
  >>> my_str = "This is a simple string"
  ```

  Now we can print the value of that string by using my_var later on:
  ```
  >>> print(my_str)
  This is a simple string
  ```

  We can also change the value that is assigned to a variable later on, either by using the standard assignment operator = or by using some of the short-hand operators that we'll learn about as we continue.
  ```
  >>> my_str += " testing"
  >>> my_str
  'This is a simple string testing'
  ```

  An important thing to realize is that the contents of a variable can be changed and we don't need to maintain the same type:
  ```
  >>> my_str = 1
  >>> print(my_str)
  1
  ```


  Ideally, we wouldn't change the contents of a variable called my_str to be an interger, but it is something that Python will allow us do.

  One last thing to remember is that, if we assign a variable with another variable, it will be assigned to the initial result of the variable and not whatever that variable points to later.
  ```
  >>> my_str = 1
  >>> my_int = my_str
  >>> my_str = "testing"
  >>> print(my_int)
  1
  >>> print(my_str)
  testing
  ```

  Short-Hand Assignment Operators
  There are numerous shorthand assignment operators we can use that allow us to perform operations and also assign back to variables in the way that we did with the += operator. The form for these shorthand assignment operations always follows the same pattern. We'll take the operator that we want to use, say +, and create a new operator by adding = to the right-hand side of it. So, for the subtraction operation, we could subtract from the current value and assign the new value to a variable using the -= operator.

  As we learn about more and more operators we'll be able to follow this pattern if we want to reassess our current variable based on an operation.

# CHAPTER 4.3
# Strings and String Operators


  Let's learn about one of the core data types in Python: the str type.

  Python Documentation For This Video

  strings (the str type) (https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str)


  Strings
  Open a REPL to start exploring Python strings:

  $ python3.7


  We've already worked with a string when we created our "Hello, World!" program. We create strings using either single quotes ('), double quotes ("), or triple-single (''')or double quotes for a multi-line string.
  ```
  >>> 'single quoted string'
  'single quoted string'
  >>> "double quoted string"
  'double quoted string'
  >>> '''
  ... this is a triple
  ... quoted string
  ... '''
  '\nthis is a triple\nquoted string\n'

  ```

  Strings also work with some arithmetic operators.

  We can combine strings using the + operator and multiply a string by a number using the * operator:
  ```
  >>> "pass" + "word"
  'password'
  >>> "Ha" * 4
  'HaHaHaHa'
  ```


  A string is a sequence of grouped characters. We do need to cover the concept of an "Object" in object-oriented programming before moving on. An "object" encapsulates two things: state and behavior. For the built-in types, the state makes sense because it's the entire contents of the object. The behavior aspect means that there are functions that we can call on the instances of the objects that we have. A function bound to an object is called a method. Here are some example methods that we can call on strings:

  find locates the first instance of a character (or string) in a string.
  This function returns the index of the character or string.
  ```
  >>> "double".find('s')
  -1
  >>> "double".find('u')
  2
  >>> "double".find('bl')
  3
  ```


  lower converts all of the characters in a string to their lowercase versions (if they have one).
  This function returns a new string without changing the original, and this becomes important later.
  ```
  >>> "TeStInG".lower() # "testing"
  'testing'
  >>> "another".lower()
  'another'
  >>> "PassWord123".lower()
  'password123'
  ```

  Lastly, if we need to use quotes or special characters in a string, we can do that using the backslash character \:

  ```
  >>> print("Tab\tDelimited")
  Tab     Delimited
  >>> print("New\nLine")
  New
  Line
  >>> print("Slash\\Character")
  Slash\Character
  >>> print("'Single' in Double")
  'Single' in Double
  >>> print('"Double" in Single')
  "Double" in Single
  >>> print("\"Double\" in Double")
  "Double" in Double
  ```
# CHAPTER 4.5
# Numbers: Integers, Floats, and Scientific Notation

  Let's learn about some of the core data types in Python: the number types int and float.

  Documentation For This Video
  numeric types (the int and float types) (https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)


  Numbers
  There are two main types of numbers that we'll use in Python, int and float. The big difference between an int and a float being that the float class handles decimal point information.

  If either of the numbers in a mathematical operation in Python is a float, then the other will be converted before carrying out the operation and the result will always be a float.

  Scientific notation
  If we happen to be working with really large numbers, and it's easier to use scientific notation, then Python can help us. For the equivalent of a float times 10 to a specified power we're able to use e or E when specifying the number:
  ```
  >>> 4.5e9
  4500000000.0
  >>> 4.5e9 == 4.5 * (10 ** 9) == 4.5E9 == 4.5E+9
  True
  ```
