Title: Walrus Abuse
Date: 2021-June-24
Modified: 2021-June-24
Category: dev-stuff
Slug: walrus
Authors: Ed
Summary:

At work I've been upgrading a lot of my python projects to 3.8 for a good few months now, and I've taken the opportunity to wantonly overuse the new-as-of-3.8 walrus operator. Now that it's been long enough for me to have cause to go and _again_ revisit those scripts, I can confidently say this: the walrus feels _so good_ to write, and it feels _so bad_ to read.

Just look at this bastard
```python
:=
```

The whole entire point of the thing - as I understand it, at least - is to reduce repetition in your list comprehensions. I didn't really mean to do yet another tutorial here, I was just trying to get my thoughts in order and it kinda turned into it, but I guess it also counts as background for making my point.

List comprehensions are themselves a nice way of building lists without having to think very hard about loops. Let's say you've got a bunch of these `Animal` objects:
```python
>>> animals = [Dog, Cat, Walrus, Parakeet, Esquilax]
```

Let's say - just like in every OOP tutorial - you want to get the noise each animal makes, in a list. Without list comprehension syntax you might write this loop:
```python
>>> noises = []
>>> for a in animals:
>>>    noises.append(a.noise)
```

This will give you the correct answer, `["woof", "meow", "arf", "caw", "reeee"]`, but wouldn't it be nicer to just do
```python
noises = [a.noise for a in animals]
```
Yep yep yep yep yep, good good good. List comprehension syntax also lets you do this cool filtering trick where you can add a condition, and it reads almost just like a sentence of English, which is super nifty:
```python
>>> [a.is_a_mammal() for a in animals]
[True, True, True, False, NaN]
>>> [a for a in animals if a.is_a_mammal()]
[Dog, Cat, Walrus, Esquilax]
```
I'm sure there's a good reason why `NaN` evaluates `True` but I don't know what it is, I don't like it, and I don't trust it.

ANYWAY AS I WAS SAYING BEFORE the entire justification for this walrus thingy - again, as far as I can tell, at least - is to ease the situation where you're cramming way too much logic into one line already and ending up repeating yourself. Wouldn't this
```python
>>> [tuple(a, DogCatcher.daily_capture_quota(a)) for a in animals if DogCatcher.daily_capture_quota(a)]
[(Dog, 500), (Walrus, 2), (Esquilax, NaN)]

```
be so much more readable as this:
```python
>>> [tuple(a, quota) for a in animals if (quota:=DogCatcher.daily_capture_quota(a))]
[(Dog, 500), (Walrus, 2), (Esquilax, NaN)]
```
More readable, right? Right? Eh, sorta, at least? And I think it only executes the repeated part once instead of twice too, which is nice I guess...? I think?

Maybe this is just me but I love list comprehensions beyond what is reasonable, so I've been abusing the walrus to fuck. And the resulting code is just not legible. I am unwilling to show it to you for business secrets and embarassment reasons, but honestly just picture spaghetti with tangled earbuds in it.

I saw this Fibonacci implementation in a tweet when walrus was first released and it took me honestly like 15 to 20 minutes of staring right at it before I knew what was happening. And honestly I'm not sure if 15 to 20 minutes is like above average or what
```python
>>> [x:=[1,1]] + [x := [x[1], sum(x)] for i in range(10)]
```
(I found it again on <a href=https://news.ycombinator.com/item?id=21862671>Hacker News</a>)

The other peeve I have about this thing is that every time I think about it I get _I Am The Walrus_ in my head and it's a cracking tune but ... it's a lot, you know? Custard dripping from a dead dog's eye? Too much to be dealing with when I'm struggling to concentrate on these TPS reports as it is.

Damn.

Like, I'm not saying we shouldn't have it, but just do it in moderation. Not too many walri, please.