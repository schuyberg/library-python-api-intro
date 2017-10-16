---
title: "Dictionaries"
teaching: 10
exercises: 5
questions:
- "How can I represent more complex datasets?"
objectives:
- "Use a dictionary to represent complex, nested datasets"
- "Retrieve data from a dictionary at any level of its hierarchy"
keypoints:
- "Every item in a dictionary has its own unique key"
- "Dictionaries can hold any kind of item, including lists and other dictionaries"
- "Data in a dictionary can be accessed by referencing its keys"
---

## A dictionary stores many values in a single structure, and each value has a 'key'.

*   Dictionaries are similar to lists, but instead of just an order (and numerical index), each item has a key string associated with it
*   Use a *dictionary* to store values under a specific name or 'key':
    *   Contained within curly brackets `{...}`.
    *   Values separated by commas `,`.
    *   Key / value pairs separated by colons`:`'
* The values of a dictionary can be accessed by their keys.
* Dictionaries can be used to represent more sophisticated data structures and classification systems
* They are analogous to 'associative arrays' or to some extent 'objects' in other programming languages


~~~
metadata = { 'title' : 'Guards! Guards!', 'author' : 'Terry Pratchett'}
print('metadata:', metadata)
print('title:', metadata['title'])
~~~
{: .python}
~~~
metadata: {'title': 'Guards! Guards!', 'author': 'Terry Pratchett'}
title: Guards! Guards!
~~~
{: .output}


## New dictionaries can be created by with the `dict()` constructor function and a sequence of key-value pairs.

*   Pairs with simple keys can be in created using the `key=value` format

~~~
publisher = dict(name='HarperTorch', place='New York', year=2001)
print('publisher:', publisher)
~~~
{: .python}
~~~
publisher: {'name': 'HarperTorch', 'place': 'New York', 'year': 2001}
~~~
{: .output}


##  Add or replace items in a dictionary by accessing them by key. Dictionaries can store any type of item, even lists or other dictionaries.

*   Nested values can be accessed by using multiple key selectors in a row

~~~
metadata = { 'title' : 'Guards! Guards!', 'author' : 'Terry Pratchett' }
metadata['publisher'] = publisher
metadata['format'] = 'Print book'
metadata['subjects'] = [ 'crime', 'mystery', 'plots', 'dragons', 'dwarves']
print('metadata:', metadata)
~~~
{: .python}
~~~
metadata: {'title': 'Guards! Guards!', 'author': 'Terry Pratchett', 'publisher': {'name': 'HarperTorch', 'place': 'New York', 'year': 2001}, 'format': 'Print book', 'subjects': ['crime', 'mystery', 'plots', 'dragons', 'dwarves']}
~~~
{: .output}


## Use multiple key selectors in a row to get at nested dictionaries and lists

*   Selectors can be chained together using multiple sets of square brackets to access items deep inside a dictionary

~~~
print('place of publication: ', metadata['publisher']['place'])
print('second subject: ', metadata['subjects'][1])
~~~
{: .python}
~~~
place of publication:  New York
second subject:  mystery
~~~
{: .output}



> ## You have been told you need at least 7 subjects in your metadata for this book.
>
> How many subjects do you have now?
> Add a few more.
> 
> > ## Solution
> >
> > `print(len(metadata['subjects']))`
> > `metadata['subjects'].extend(['swords', 'royalty'])`
> > `print('metadata: ', metadata)`
> {: .solution}
{: .challenge}


> ## You're actually looking for the original UK edition, update the publisher info accordingly
>
> Change the publication date to 1998.
> Change the publisher to 'Corgi'
> Change the publication place to 'London'
> 
> > ## Solution
> >
> > `metadata['publisher'] = dict(name='Corgi', place='London', year=1998)`
> > `print('metadata: ', metadata)`
> {: .solution}
{: .challenge}


