---
title: "Built-in Functions and Help"
teaching: 10
exercises: 5
questions:
- "How can I use built-in functions?"
- "How can I find out what they do?"
- "What kind of errors can occur in programs?"
objectives:
- "Explain the purpose of functions."
- "Correctly call built-in Python functions."
- "Correctly nest calls to built-in functions."
- "Use help to display documentation for built-in functions."
- "Correctly describe situations in which SyntaxError and NameError occur."
keypoints:
- "Use comments to add documentation to programs."
- "A function may take zero or more arguments."
- "Commonly-used built-in functions include `max`, `min`, and `round`."
- "Functions may only work for certain (combinations of) arguments."
- "Functions may have default values for some arguments."
- "Use the built-in function `help` to get help for a function."
- "Every function returns something."
- "Python reports a syntax error when it can't understand the source of a program."
- "Python reports a runtime error when something goes wrong while a program is executing."
- "Fix syntax errors by reading the source code, and runtime errors by tracing the program's execution."
---
## Use comments to add documentation to programs.

~~~
# This sentence isn't executed by Python.
name = 'Library Carpentry'   # Neither is this comment - anything after '#' is ignored.
~~~
{: .python}

## A function may take zero or more arguments.

*   We have seen some functions already --- now let's take a closer look.
*   An *argument* is a value passed into a function.
*   Any arguments you want to pass into a function must go into the `()`
    * `print("I am an argument and must go here.")`
*   You must always use parentheses, because this is how Python knows you are calling a function.
    * You leave them empty if you don't want or need to pass any arguments in.
*   `len` takes exactly one.
*   `int`, `str`, and `float` create a new value from an existing one.
*   `print` takes zero or more.
    *   `print()` prints a blank line.

~~~
print('before')
print()
print('after')
~~~
{: .python}
~~~
before

after
~~~
{: .output}


## Use the built-in function `len` to find the length of a string.

~~~
print(len('helium'))
~~~
{: .python}
~~~
6
~~~
{: .output}

*   Nested functions are evaluated from the inside out,
    just like in mathematics.


## Use the built-in function `help` to get help for a function.

*   Every built-in function has online documentation.

~~~
help(len)
~~~
{: .python}
~~~
Help on built-in function len in module builtins:

len(obj, /)
    Return the number of items in a container.
~~~
{: .output}

## Python reports a syntax error when grammar rules (that's Python grammar, not English grammar) have been violated.

*   You've seen errors when you try to use a function incorrectly.
    * Can also have errors when you use punctuation incorrectly.
*   Python will run the program up until that point, but if the grammar of that line
    of code has produced an error, then the program will shut down with an error.

~~~
# Forgot to close the quotation marks around the string.
name = 'Feng
~~~
{: .python}
~~~
SyntaxError: EOL while scanning string literal
~~~
{: .error}

~~~
# An extra '=' in the assignment.
age = = 52
~~~
{: .python}
~~~
SyntaxError: invalid syntax
~~~
{: .error}

*   Look more closely at the error message:

~~~
print("hello world"
~~~
{: .python}
~~~
  File "<ipython-input-6-d1cc229bf815>", line 1
    print ("hello world"
                        ^
SyntaxError: unexpected EOF while parsing
~~~
{: .error}

*   The message indicates a problem on first line of the input ("line 1").
    *   In this case the "ipython-input" section of the file name tells us that
        we are working with input into IPython.
*   The `-6-` part of the filename indicates that
    the error occurred in cell 6 of our Notebook.
*   Next is the problematic line of code,
    indicating the problem with a `^` pointer.

## Python reports a runtime error when something goes wrong while a program is executing.

~~~
age = 53
remaining = 100 - aege # mis-spelled 'age'
~~~
{: .python}
~~~
NameError: name 'aege' is not defined
~~~
{: .error}

*   Fix syntax errors by reading the source and runtime errors by tracing execution.

## Every function returns something.

*   Every function call produces some result.
*   If the function doesn't have a useful result to return,
    it usually returns the special value `None`.

~~~
result = print('example')
print('result of print is', result)
~~~
{: .python}
~~~
example
result of print is None
~~~
{: .output}


> ## Last Character of a String
>
> If Python starts counting from zero,
> and `len` returns the number of characters in a string,
> what index expression will get the last character in the string `name`?
> (Note: we will see a simpler way to do this in a later episode.)
>
> > ## Solution
> >
> > `name[len(name) - 1]`
> {: .solution}
{: .challenge}
