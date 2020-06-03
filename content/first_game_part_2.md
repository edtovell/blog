Title: More Things I Learned While Trying to Learn Game Development
Date: 2020-June-3
Modified: 2020-June-3
Category: dev-stuff
Slug: first_game_2
Authors: Ed
Summary:

> __WHOOPS__ I wrote this in like April and forgot to upload it.

You know what, there's nothing like a killer virus to free up some spare time.

Here are some things I think I learned now that I finally "finished" the game.


# haha "finished"
I didn't put absolutely everything I wanted into it, so it's not finished. It's never finished. There's always more. I had to keep reminding myself that this whole game is just for me to learn how to make a game, and not a badass triple-A title that will make me rich. I kept imagining other cool bits I could put into it, moving the goalposts a bit further away. It was a sort of masochistic self-imposed feature creep.

In the end I set a strict end-of-day deadline for myself, finished up, and closed the laptop. There are all sorts of bugs and obvious space for improvement, but they will never be addressed because I want to stop practicing and start actually doing. In future I'm going to try to stick to the to-do list.


# Javascript is a bananas hot mess
I come from python, which is a good language to pick up and run with and is generally awesome. But under the hood it's - and I don't normally like using terms like this because of mental health stigma and whatnot, but I can't think of a better way of putting it - absolutely batshit bonkers. It is full of weird vestigial features and band-aids over broken bits. For just one example, the very existence of the [integer cache](https://wsvincent.com/python-wat-integer-cache/) perplexes me profoundly.

So Javascript then. It's a right barrel of laughs, it is.

 - Everything is a function, to an overwhelming degree. I feel like a core language developer must have smoked some stuff and then got overexcited and fanatical about passing functions as arguments to other functions, because it's everywhere. It feels shoehorned in. A stack overflow post told me to prefer `.forEach` over a for-loop when iterating through arrays - why? For-loops are readable and sense-making to humans. Not everything has to be a function.
 - I suppose as a sort of corollary of the previous, there are about a billion different ways to declare functions. I do quite like the `()=>{}` thing, but is it really necessary?
 - Tracing bugs is a damn chore. I'm not sure how much of this is JS and how much is the Phaser framework, but it's bloody annoying either way. Every level of anonymous-function-as-argument and callback within callback seems to totally obfuscate the stack trace to the point where you might as well just get "Error: It Broke".
 - Is `this` a reserved term? Is that built in? I find the number of `this.something`s in my code mildly upsetting. It seems sort of redundant. Is there some other way to keep track of common variables between object methods that I don't know about? Maybe I'm just confused about how scope works.
 - Can you import a script from another file? Because I couldn't figure out how to do it, other than in the root html file. And then weird things start happening with scope and you can directly reference variables from other scripts, which I strongly dislike.
 - On the plus side, I do like the semicolons and the {curly bois};


# The simplest things are way more complicated than you would expect
The hardest bits of the whole process were:

 - getting the guy to move fixed to a grid (like Pokemon) instead of floating freely in whichever direction (like Zelda).
 - reading a keyboard tap as one event, instead of seeing the key in the down position at the start of each frame and reading it as a new event, meaning you immediately skip and then exit dialogue every time you enter it. I've since found out that there is a built-in way of doing this, but I never found it because I came via the "hold left to go left" sphere of influence.
 - Everything to do with displaying text. I naively thought I wouldn't need to treat the menus as full-blown state machines, I would just sort of wing it, and like almost every other time I made that assumption I came to regret it down the line. It's such a simple part of every game that I totally overlooked how complex it would get. Meet NPC, press button, read dialog text, choose response, press button to skip ahead, etc. And as soon as I tried to formalise a structure with some good old family-style JSON, I made it so that every interaction had to follow the same highly restrictive format (text, followed by a response menu, followed by text). In future I'll probably just use an existing plugin for this kind of thing.


# There is great shame in doing it wrong, but do it anyway
I am so humble, I think I am literally the most humble person I know. Humility is my actual literal figurative breakfast. I'm really really good at it. Nevertheless, throughout my learning odyssey I tried very hard to do things the "right way" to the best of my knowledge, and I quickly came to appreciate that the best of my knowledge was zero knowledge. So I did it the wrong way, because it was a choice between that and doing nothing. There is no shame in this, by which I mean, there is great shame in this. But you can wriggle out of it. It's like starting a job or something: you can make as many mistakes as you want on the first day. And if you subscribe to a lifelong-learning-type philosophy then it's always your first day and you can never be held responsible for anything ever.

If you were for some reason to look at the source code and commit history for _Get The Hat_, you would see that for ages I didn't know that Phaser could run two scenes at the same time. And that's _literally the point_ of Phaser 3 - you can have a main game scene, and an overlay scene with things like health bars and radars and whatnot, and another overlay scene for text boxes and what-have-you. But I didn't know that, so all the dialog and interaction texts are actual game objects in the main scene. What that means is that, if there were a bug that caused the game to remain active during a dialog, then the dialog box would sit in the game world like a rock or a wall or something. Insanity. There might be an idea for a game there actually. A bit like [Baba Is You](https://hempuli.com/baba/), but with dialog. See, fringe benefit!

And that's about all I have to say about that. Play my game [Get The Hat](http://edtovell.com/get_the_hat/).
