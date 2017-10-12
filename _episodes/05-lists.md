---
title: "Lists"
teaching: 10
exercises: 10
questions:
- "How can I store multiple values?"
objectives:
- "Explain why programs need collections of values."
- "Write programs that create flat lists, index them, slice them, and modify them through assignment and method calls."
keypoints:
- "A list stores many values in a single structure."
- "Use an item's index to fetch it from a list."
- "Lists' values can be replaced by assigning to them."
- "Appending items to a list lengthens it."
- "Use `del` to remove items from a list entirely."
- "The empty list contains no values."
- "Lists may contain values of different types."
- "Character strings can be indexed like lists."
- "Character strings are immutable."
- "Indexing beyond the end of the collection is an error."
---
## A list stores many values in a single structure.

*   Dealing with a hundred variables called `subject_001`, `subject_002`, etc.,
    would be a wildly inefficient classification system
*   Use a *list* to store many values together.
    *   Contained within square brackets `[...]`.
    *   Values separated by commas `,`.
*   Use `len` to find out how many values are in a list.

~~~
subjects = [dogs, cats, hampsters, pets, fauna]
print('subjects:', subjects)
print('length:', len(subjects))
~~~
{: .python}
~~~
subjects: [dogs, cats, hampsters, pets, fauna]
length: 5
~~~
{: .output}

## Use an item's index to fetch it from a list.

*   Just like strings.

~~~
print('zeroth item of subjects:', subjects[0])
print('fourth item of subjects:', subjects[4])
~~~
{: .python}
~~~
zeroth item of subjects: dogs
fourth item of subjects: fauna
~~~
{: .output}

## Lists' values can be replaced by assigning to them.

*   Use an index expression on the left of assignment to replace a value.

~~~
subjects[0] = snakes
print('subjects is now:', subjects)
~~~
{: .python}
~~~
subjects is now: [snakes, cats, hampsters, pets, fauna]
~~~
{: .output}

## Appending items to a list lengthens it.

*   Use `list_name.append` to add items to the end of a list.

~~~
cities = ['Vancouver', 'Ontario', 'Montreal']
print('cities is initially:', cities)
cities.append('Saskatoon')
cities.append('Halifax')
print('cities has become:', cities)
~~~
{: .python}

~~~
cities is initially: ['Vancouver', 'Ontario', 'Montreal']
cities has become: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Halifax']
~~~
{: .output}

*   `append` is a *method* of lists.
    *   Like a function, but tied to a particular object.
*   Use `object_name.method_name` to call methods.
    *   Deliberately resembles the way we refer to things in a library.
*   We will meet other methods of lists as we go along.
    *   Use `help(list)` for a preview.
*   `extend` is similar to `append`, but it allows you to combine two lists.  For example:

~~~
australian_cities = ['Sydney', 'Brisbane', 'Darwin', 'Adelaide', 'Hobart']
french_cities = ['Paris', 'Marseille', 'Strasbourg', 'Nice']
print('cities is currently:', cities)
cities.extend(australian_cities)
print('cities has now become:', cities)
cities.append(french_cities)
print('cities has finally become:', cities)
~~~
{: .python}

~~~
cities is currently: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Halifax']
cities has now become: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Halifax', 'Sydney', 'Brisbane', 'Darwin', 'Adelaide', 'Hobart']
cities has finally become: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Halifax', 'Sydney', 'Brisbane', 'Darwin', 'Adelaide', 'Hobart', ['Paris', 'Marseille', 'Strasbourg', 'Nice']]
~~~
{: .output}

Note that while `extend` maintains the "flat" structure of the list, appending a list to a list makes the result two-dimensional.

## Use `del` to remove items from a list entirely.

*   `del list_name[index]` removes an item from a list and shortens the list.
*   Not a function or a method, but a statement in the language.

~~~
print('cities before removing the fifth item:', cities)
del cities[4]
print('cities after removing the fifth item:', cities)
~~~
{: .python}
~~~
cities before removing last item: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Halifax', 'Sydney', 'Brisbane', 'Darwin', 'Adelaide', 'Hobart', ['Paris', 'Marseille', 'Strasbourg', 'Nice']]
cities after removing last item: ['Vancouver', 'Ontario', 'Montreal', 'Saskatoon', 'Sydney', 'Brisbane', 'Darwin', 'Adelaide', 'Hobart', ['Paris', 'Marseille', 'Strasbourg', 'Nice']]
~~~
{: .output}

## The empty list contains no values.

*   Use `[]` on its own to represent a list that doesn't contain any values.
    *   "The zero of lists."
*   Helpful as a starting point for collecting values
    (which we will see in the [next episode]({{page.root}}/12-for-loops/)).

## Lists may contain values of different types.

*   A single list may contain numbers, strings, and anything else.

~~~
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
~~~
{: .python}

## Character strings can be indexed like lists.

*   Get single characters from a character string using indexes in square brackets.

~~~
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
~~~
{: .python}
~~~
zeroth character: c
third character: b
~~~
{: .output}

## Character strings are immutable.

*   Cannot change the characters in a string after it has been created.
    *   *Immutable*: cannot be changed after creation.
    *   In contrast, lists are *mutable*: they can be modified in place.
*   Python considers the string to be a single value with parts,
    not a collection of values.

~~~
element[0] = 'C'
~~~
{: .python}
~~~
TypeError: 'str' object does not support item assignment
~~~
{: .error}

*   Lists and character strings are both *collections*.

## Indexing beyond the end of the collection is an error.

*   Python reports an `IndexError` if we attempt to access a value that doesn't exist.
    *   This is a kind of runtime error.
    *   Cannot be detected as the code is parsed
        because the index might be calculated based on data.

~~~
print('99th element of element is:', element[99])
~~~
{: .python}
~~~
IndexError: string index out of range
~~~
{: .output}

> ## Fill in the Blanks
>
> Fill in the blanks so that the program below produces the output shown.
>
> ~~~
> values = ____
> values.____(1)
> values.____(3)
> values.____(5)
> print('first time:', values)
> values = values[____]
> print('second time:', values)
> ~~~
> {: .python}
>
> ~~~
> first time: [1, 3, 5]
> second time: [3, 5]
> ~~~
> {: .output}
{: .challenge}

> ## How Large is a Slice?
>
> If 'low' and 'high' are both non-negative integers,
> how long is the list `values[low:high]`?
{: .challenge}

> ## From Strings to Lists and Back
>
> Given this:
>
> ~~~
> print('string to list:', list('tin'))
> print('list to string:', ''.join(['g', 'o', 'l', 'd']))
> ~~~
> {: .python}
> ~~~
> ['t', 'i', 'n']
> 'gold'
> ~~~
> {: .output}
>
> 1.  Explain in simple terms what `list('some string')` does.
> 2.  What does `'-'.join(['x', 'y'])` generate?
{: .challenge}

> ## Working With the End
>
> What does the following program print?
>
> ~~~
> element = 'helium'
> print(element[-1])
> ~~~
> {: .python}
>
> 1.  How does Python interpret a negative index?
> 2.  If a list or string has N elements,
>     what is the most negative index that can safely be used with it,
>     and what location does that index represent?
> 3.  If `values` is a list, what does `del values[-1]` do?
> 4.  How can you display all elements but the last one without changing `values`?
>     (Hint: you will need to combine slicing and negative indexing.)
{: .challenge}

> ## Stepping Through a List
>
> What does the following program print?
>
> ~~~
> element = 'fluorine'
> print(element[::2])
> print(element[::-1])
> ~~~
> {: .python}
>
> 1.  If we write a slice as `low:high:stride`, what does `stride` do?
> 2.  What expression would select all of the even-numbered items from a collection?
{: .challenge}

> ## Slice Bounds
>
> What does the following program print?
>
> ~~~
> element = 'lithium'
> print(element[0:20])
> print(element[-1:3])
> ~~~
> {: .python}
{: .challenge}

> ## Sort and Sorted
>
> What do these two programs print?
> In simple terms, explain the difference between `sorted(letters)` and `letters.sort()`.
>
> ~~~
> # Program A
> letters = list('gold')
> result = sorted(letters)
> print('letters is', letters, 'and result is', result)
> ~~~
> {: .python}
>
> ~~~
> # Program B
> letters = list('gold')
> result = letters.sort()
> print('letters is', letters, 'and result is', result)
> ~~~
> {: .python}
{: .challenge}

> ## Copying (or Not)
>
> What do these two programs print?
> In simple terms, explain the difference between `new = old` and `new = old[:]`.
>
> ~~~
> # Program A
> old = list('gold')
> new = old      # simple assignment
> new[0] = 'D'
> print('new is', new, 'and old is', old)
> ~~~
> {: .python}
>
> ~~~
> # Program B
> old = list('gold')
> new = old[:]   # assigning a slice
> new[0] = 'D'
> print('new is', new, 'and old is', old)
> ~~~
> {: .python}
{: .challenge}
