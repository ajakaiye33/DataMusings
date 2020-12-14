---
toc: true
layout: post
description: The Magic of Generative Expression Function.
categories: [markdown]
title: Wrangling Data With Pythons Generative Expressions
---




![](/images/clean_data.jpg)

### Introduction
In recent times we have heard it in different quarters that *data is the new oil*
You will agree that this is a lofty designation that would elicit if anything
some eye-rolling episodes :smirk:

However I must point out as an aspiring Data Scientist & Wrangler,  I believe
the assertion. The importance of data especially in the 21st century can not be
overemphasize. Nevertheless, if you aren't convinced just yet, I suggest you read
**Yuval Noah Harari**'s *Homo Deus* :closed_book:

To continue with the above analogy, it's evident that oil goes through various
processes and transformation before it's certified useful in the multiple ways that
we currently oil.

Similarly, Data is basically
useless in its crude form until it is transformed. The process of transforming Data
has been dubbed as *Data Cleaning* or *Data Scrubbing* or *Data Wrangling*. The python
language has a lot of tools that make this cleaning process easy. I thought I'm
versed in the available data wrangling tools until when I discovered **Generative Expressions**
Therefore this post will be about How  efficient and elegant is python's Generative Expressions especially  when compared to other methods like *for loop*, list comprehension etc.in the art and craft of Data Wrangling!

### Efficiency & Effectiveness
According to  Peter Drucker, the father of management, effectiveness is doing
the right things, efficiency is doing things rightly. This definition may sound
confusing at first, but on deeper reflection, it actually hit the nail on the head.
You can be effective without necessarily be efficient. To demonstrate this concept.
I will use a real-life code examples.
Firstly, I will need to import an essential function from the sys python package.

`# from sys import getsizeof`


Extract odd number with for loop
```python
odd_num_with_FL = []
for i in range(100000):
  if i % 2 != 0:
      odd_num_with_FL.append(i)
```

Extract odd number with List Comprehension

```python
# get odd number
odd_num_with_LC = [x for x in range(100000) if x % 2 !=0]
```

Extract odd number with generative expressions

```python
# get odd number using generative expressions
odd_num_with_GE = (y for y in range(100000) if y % 2 !=0)
```

The above three different ways we extracted the odd numbers are correct and effective but are all three examples efficient?

One way to measure code efficiency is the number of bytes an operation occupies in the computer memory. Without further ado, we can know the size our above code occupies in our system's memory with the aid of `getsizeof` function from the `sys` package.

Let us see the bytes that each operation takes:

```python
print(getsizeof(odd_num_with_FL))
```
406496 `bytes`

```python
print(getsizeof(odd_num_with_LC))
```
406496 `#bytes`

```python
print(getsizeof(odd_num_with_GE))
```
120 `#bytes`

Wow! isn't this amazing! Look at the difference in bytes. I understand. You aren't alone. I was blown away when I encounter the power of the generative expression.

However, the magic behind this apparent efficiency lies in the concept of *lazing rendering or evaluation* as the generative expression saves little or nothing in the memory. You don't believe me ... let us see the code.

```python
print(odd_num_with_GE)
```
<generator object <genexpr> at 0x10453a840>

Unlike the output of the above code, the other code examples would print out the actual odd numbers, you can go ahead and print them out. Knock yourself out! :smile:


### Elegance and Simplicity
Efficiency, which we have tried to illustrate in the preceding session, could also be defined in the light of simplicity. Not for nothing did Austin Freeman, said *Simplicity is the Soul of efficiency*. Similarly, according to Leonardo Da Vinci, *Simplicity is the ultimate sophistication* and I make bold to say you don't understand a concept or a phenomenon until you can render it as simple as possible. The same simplicity informs the  Zen of python.

We don't need to complicate the already complicated process of Data Wrangling and Data Cleaning, to this end you can not but agree that any procedure or tool seeking to reduce the observed complexity would be welcome and embraced by all and sundry. The generative expression makes life easy, even in the thick and thin of the dirtiest of data.
Let illustrate this with the following
code:

```python
# Clean the following List of words
words = ['Hello\n', 'My name', 'is\n','Bob','How are', 'doing\n']
```

Using the normal for loop to clean the above list of words

```python
clean_words = []
for word in words:
    for w in word.split(' '):
        clean_words.append(w.strip().lower())
```
```python
print(clean_words)
['hello', 'my', 'name','is','bob','how','are','you', 'doing']
```
Without the risk of sounding immodest, the above path would be the route taken by the majority of python newbies in solving this problem. This approach may be very much useful but appears ponderous. Just look at the number of lines of code written and the complex nested for loop. Can the above code be improved on with generative expression?

Here is the code:

```python
clean_words_with_GE = (word.strip().lower() for word in words for w in word.split(' '))
```
The same result was achieved with just a line and also little, or no memory is utilized by lazy evaluation.

### Brevity Vs Readability

There is no doubt that the generative expression approach not only engenders efficiency, it also ensures simplicity. Like every other approach, it has its own drawbacks and limitations. And chief amongst the limitations is Readability. Our code may not pass the 7th Zen of Python's rule, which admonished:'Readability Counts'. Therefore as you enjoy the new powers of generative expression equally ensures that your code is clear and readable.

I hope you enjoy this post. Till we meet again, happy coding:hammer:
