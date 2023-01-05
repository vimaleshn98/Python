# CHAPTER 12.1
# String Encodings and Functions

  Strings hold onto characters and those characters don't need to be alphanumeric. Depending on how a string is encoded, some characters might not be valid. Before we can dig into string encodings, we need to take a look at some of the functions that allow us to interact with Unicode code points (the numbers behind characters). In this video, we'll delve into the ord and chr functions.

  What are Unicode Code Points?
  In Python 3, strings are Unicode by default (specifically UTF-8 encoded). Behind the scenes, each character is stored as its Unicode code point, but what does that mean? Unicode is an encoding standard that allows all sorts of unique characters across different languages to have consistent, unique numeric values. For instance, the code point for the letter a is 97, but the character that isn't commonly typed out like the trademark symbol ™ has a code point of 8482. Unicode is a standard, but there are different encodings, one of the most commonly used being UTF-8. UTF-8 stands for "Unicode Transformation Format," with the "8" meaning that values are 8-bits in length. 1,112,064 valid Unicode code points can be encoded with UTF-8.

  Up to this point, we've been working with strings that use standard ASCII characters (letters, numbers, and common punctuation). ASCII is an older specification with 256 named characters. Their corresponding code points and the first 128 are also valid UTF-8 values. The trademark symbol is in the ASCII specification under the extended characters table, so it has an ASCII numeric value between 128 - 255, but a completely different Unicode code point.

  To make things even more confusing, Unicode code points are sometimes represented in decimal form and other times by using a 'U+' with the hexadecimal form of the same number. So '™' is 8482, but if you search the internet, you'll usually see it written as U+2122.

  Going from Code Point to String and Vice Versa
  Now that we have an idea of what code points are and how encodings work let's see how we can work with them in Python. If we want to see the code point for a character that we know how to type, then we can use the ord function. This function takes a single character and will return the decimal code point. Let's see what this looks like for the letter l:

   
  ```
  >>> ord('l')
  108 
  ```
  

  If we try to use ord with more than one character, then it will raise an error:

   
  ```
  >>> ord('la')
  Traceback (most recent call last):
    File "<input>", line 1, in <module>
      ord('la')
  TypeError: ord() expected a character, but string of length 2 found 
  ```
  

  If we already know the Unicode code point for a character that is more difficult to type, like the trademark symbol, then we can type it out using the hexadecimal notation if we prefix the number with \u:

   
  ```
  >>> ord('\u2122')
  8482 
  ```
  

  Notice that ord took a single character as the argument, but didn't give us an error when we escaped the Unicode code point by using the \u. This is because a Python string is UTF-8 encoded by default, and although it looks like more than one character to us, that is a single character in UTF-8.

  It's also worth noting that when the string \u2122 is evaluated in Python, it will print the character that we're expecting:

   
  ```
  >>> '\u2122'
  '™'
  >>> '\u2124'
  '?' 
  ```
  

  Say we want to take a decimal code point and convert it back into a string. To do that we'll need to use the chr function:

   
  ```
  >>> chr(8482)
  '™' 
  ```
  

  Because we can write integers in hexadecimal notation using the 0x prefix, and those numbers then get converted into the decimal value, we are also able to use that form with the chr function:

   
  ```
  >>> chr(0x2122)
  '™' 
  ```
# CHAPTER 12.2
# Useful String Methods, Part 1

  As strings are one of the most important and common types that we work with, we're going to dive into some different
  sets of methods that we have at our disposal when working with strings. In this lesson, we'll take a look at some capitalization methods and how to evaluate the contents of a string against common patterns.

  Changing String Capitalization
  When working with strings, it's not uncommon for us to want to change the capitalization of the string. We can make comparisons easier or to improve the way that we display the value. Thankfully, Python provides us with simple methods on the str class for just these purposes.

   
  ```
  >>> my_str = 'tEsTinG'
  >>> my_str.lower()
  'testing'
  >>> my_str.upper()
  'TESTING'
  >>> my_str.capitalize()
  'Testing' 
  ```
  

  The lower and upper methods are great for changing all of the characters in a string to either lowercase or uppercase. This is handy to do when capitalization doesn't matter and we want to compare against a value that we already know. For all intents and purposes, an email address: Kevin@example.com is the same as kevin@example.com. If we want to compare a user-provided value that could have odd capitalization with a known email address, then we could call lower before comparing the two values.

   
  ```
  email = input("Your Email: ")
  print("Email is test@example.com:", email.lower() == 'test@example.com') 
  ```
  

  The capitalize method is a little different, as it will lowercase every character besides the first one. It doesn't take into consideration if that's the right thing to do for the words within the string. Because of this, you might not find yourself using capitalize all that often, but in many cases, it will work for single-word strings.

  Checking String Patterns with .is___ Methods
  Since strings are collections of characters, they can hold onto an incredible variety of information. But that doesn't mean that there aren't different patterns that the information could fall into. For instance, the string '12' is completely numeric. For these types of patterns, the str class provides a whole family of methods that start with is, such as isnumeric:

   
  ```
  >>> "12".isnumeric()
  True 
  ```
  

  There are quite a few of these methods. Here's a list:

   
  ```
  isascii - Return True if all characters in the string are ASCII, False otherwise.
  islower - Return True if the string is a lowercase string, False otherwise.
  isupper - Return True if the string is an uppercase string, False otherwise.
  istitle - Return True if the string is a title-cased string (all words capitalized), False otherwise.
  isspace - Return True if the string is a whitespace string, False otherwise.
  isdecimal - Return True if the string is a decimal string (whole number), False otherwise.
  isdigit - Return True if the string is a digit string (whole number), False otherwise.
  isnumeric - Return True if the string is a numeric string (whole number), False otherwise.
  isalpha - Return True if the string is an alphabetic string, False otherwise.
  isalnum - Return True if the string is an alphanumeric string, False otherwise.
  isidentifier - Return True if the string is a valid Python identifier, False otherwise. String could be used as a variable, function, or class name.
  isprintable - Return True if the string is printable, False otherwise. Meaning that if the character can't be printed as-is, then it's not printable. So escape characters like \n are considered not printable even though they change how the string is printed.\ 
  ```
# CHAPTER 12.3
# Useful String Methods, Part 2

  As strings are one of the most important and common data types that we work with, we're going to dive into some different
  sets of methods that we have at our disposal when working with strings. In this lesson, we'll take a look at how to split strings apart, build them up from a list, and substitute information into a string using the format method.

  Splitting and Joining Strings
  Sometimes we have strings that we want to break into smaller pieces to work with. If we have a delimiter that we'd like to use to separate the string into smaller strings, then we're able to use the split method to get a list of substrings. A simple example of this would be getting the individual words in a string by splitting on a single space (the default separator):

   
  ```
  >>> phrase = "This is a simple phrase"
  >>> words = phrase.split()
  >>> words
  ['This', 'is', 'a', 'simple', 'phrase'] 
  ```
  

  Another way I've personally used this is to get the final segment of a URL by splitting on slashes and then selecting the last item in the list:

   
  ```
  >>> url = 'https://example.com/users/jimmy
  >>> user = url.split('/')[-1]
  >>> user
  'jimmy' 
  ```
  

  Being able to split a string is useful, but we might also want to create a single string from a list of strings that we already have. To do this we can use the join method. It's interesting because the string we start with will be the separator that we want inserted between the strings in the list. Let's take our words list and insert commas between the words instead of spaces:

   
  ```
  >>> phrase = "This is a simple phrase"
  >>> words = phrase.split()
  >>> ", ".join(words)
  'This, is, a, simple, phrase' 
  ```
  

  A common way that join is used is by taking a list of lines forming them into a single string with new lines between the lines:

   
  ```
  >>> lines = ['First line', 'Second line', 'Third line']
  >>> output = '\n'.join(lines)
  >>> print(output)
  First line
  Second line
  Third line 
  ```
  

  Formatting Strings with format
  The last method that we're going to talk about is the format method. We often have a good idea of what a message needs to look like, but we want to have some dynamic information inserted into the middle of a string. Up to this point, we've been using the multiple arguments available to the print function, but sometimes we don't want to print the formatted string out.

  The format method allows us to place {} segments into a string and then have values added into those positions:

   
  ```
  >>> "Hello, my name is {}, and I really enjoy {}. Have a nice day!".format('Keith', 'Python')
  'Hello, my name is Keith, and I really enjoy Python. Have a nice day!' 
  ```
  

  If we want to use the same value multiple times within the string, then we can place the item index within the {} values:

   
  ```
  >>> "Hello, my name is {0}, and I really enjoy {1}. Have a nice day! - {0}".format('Keith', 'Python')
  'Hello, my name is Keith, and I really enjoy Python. Have a nice day! - Keith' 
  ```
  

  It's worth noting that these two approaches can't be mixed. There's a lot more that we can do with the format method, and reading the Format String Syntax documentation can help.
