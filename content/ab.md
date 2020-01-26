Title: A Sensible Naming Convention for A/B Deployment
Date: 2020-Jan-26
Modified: 2020-Jan-26
Category: dev stuff
Slug: ab_naming
Authors: Ed
Summary:

# What is A/B Deployment?

***Obviously skip this bit if you know what it is, it gets more interesting afterwards***

It's a low-risk way of updating your web app when you need to maintain uptime. The technique is explained in the movie *Fight Club* ([video NSFW](https://youtu.be/wS_pYyWp6I8?t=41)).

Before cinemas went digital, projectors came in pairs. The film would come on several reels, so you need to do some manoeuvring to get a movie to play straight through with no interruption. You set up your first projector with the first reel and press play, and you rig up the other projector with the second reel. Just before the first reel comes to an end, you press play on the second projector and switch them. The audience sees one continuous movie, but it's being projected from the second machine now. Now you can take the first reel down and wind it back and put it away, then set up your first projector with the _third_ reel and do the whole thing again. And again and again until the film ends.

You can pull the same trick with web services. Once you've built an app and put it on a running server and people are using it, you might not be able risk any downtime. So instead of restarting the server every time you need to deploy changes to your code, you can use a second server and pull the old switcheroo. With two servers, you can keep your service live and ready on server A, while you deploy and restart and test and whatnot on server B. When you're sure it's ready, you swap the DNS CNAMEs and everybody's using the updated service, none the wiser.

# So what's the problem?

It's a good system. Swapping CNAMEs is very easy and fast, so nobody will notice the switch. You get an extra server to tinker and play around with while your service stays live, and if you *do* deploy some bad code by accident and you catch it straight away, then you can just swap CNAMEs again and roll back to the previous version. No harm done. It's a good system.

The main source of trouble in this otherwise good system is that either one of your servers could be the live one. It's a good system as long as you keep track of which server is the live one. Don't touch the live one while it's live. It's important that you be able to tell at a glance which server is the live one. They need names so you can tell them apart, but either one could be live at any time.

So for the love of all that is holy...

# DON'T CALL YOUR SERVERS "A" and "B"

If you're new to the code base because you just started a new job or joined a project, or if you had a rough night last night and you're a bit hungover, or for any silly human reason you aren't 100% on board with what's going on, your brain might look at this setup and go

*"**A** is the main one, so I can deploy to **B** and swap them..."*

... which 50% of the time will RUIN EVERYTHING. If Server B is live, then you just took down a live server to deploy code to it, then rolled back your service to whatever was running on Server A. "A" and "B" are names from a well-known series called the Latin Alphabet, where "A" is the *first* letter and "B" is the *second*. So everyone assumes that "A" is the **main one**.

To make things worse, I once inherited a stack where the servers were called "A" and "B", but also the CNAMEs were called `...service/api/whatever...` and `...service-b/api/whatever...`, so half the time "B" would be live while "A" is serving **service-b**. It takes a little bit of brainwork to figure out what's happening, and if you have to think about it then you can make mistakes.

So you shouldn't call your servers anything from a series. Don't call them "1 and 2" or "Alpha and Beta" or "Batman and Robin" or anything like that. Don't.

It is for precisely this reason that the A/B Deployment pattern is sometimes also known as **Green/Blue Deployment**, which surely fixes everything right?

# DON'T CALL YOUR SERVERS "GREEN" AND "BLUE"

Colours don't normally come "in order" like letters or numbers or superheroes, but they do have unhelpful connotations that confuse things. The colour green, for example, is generally associated with "good" or "health" or "go" or "safe", that sort of thing, which is ironic in this case because it's a problem.

I use AWS a lot (obviously because I love Bezos and I don't think he has enough money), and this is what the Elastic Beanstalk dashboard looks like from a search I did:

![The servers, they are both green]({static}/images/eb-dash.png)

Leaving aside that this person has called their servers "primary" and "secondary" (grr), the dashboard is helpfully telling us that both servers are healthy by colour-coding them as green. When they start getting overloaded they turn yellow, and if they fail they turn red. Handy, good, useful, etc...

UNTIL you come to deployment time, and let's say you followed convention and called your servers "GREEN" and "BLUE". If you're tired or drunk or new (or **green**?) or out of sorts for whatever reason, you might look at the dashboard and conclude that "GREEN" is the live one. And 50% of the time, that conclusion is wrong.

Even if you're the kind of person who knows the difference between names for colours and actual colours, and who prefers skimming command line text output to relying on web interfaces, Elastic Beanstalk provides a helpful command line tool that includes a status monitor, which outputs something like this (again, I found it from a quick search):

!["Health: Green"]({static}/images/eb-status.png)

And even though it clearly only says "Green" under "Health" and not "Application Name" or "Environment ID" or any other heading, *the fact that is says "Green" at all* is probably enough to mislead somebody just skimming for keywords.

Luckily, there is a solution. You may also have heard that the A/B or Green/Blue Deployment pattern is also commonly known as **Red/Black Deployment**, which ...

# DON'T CALL YOUR SERVERS "RED" AND "BLACK"

"RED" is no better a name than "GREEN" for precisely the same reason.

However, the Red/Black naming convention does provide a clue to an *actual* solution here. It's only unhelpful because "red" and "black" imply a good/bad binarity (think "in the ..."), which will lead to wrong conclusions half the time. But whoever came up with it was probably thinking about a deck of cards. Half the cards are red and half are black, and neither is *better* or *worth more* (in most games at least). It's an entirely neutral pairing, and a common enough cultural reference point that you can expect your whole team to understand it * if it weren't overshadowed by the seperate and unrelated "black=good/red=bad" thing.

So the best thing to do would be to name your servers after a common, sentiment-neutral pairing that is unlikely to be confused with some other naming convention, and doesn't imply anything about the seniority or status of the instances. So I suggest we all

# CALL YOUR SERVERS "PINK" AND "BLUE"

Allow me to make the case thusly:

 * Pink and blue are the colours that are traditionally assigned to girls and boys, which is a common two-way distinction.
 * The binary is neutral in terms of seniority * neither girls or boys are better or more important, so either one could be in charge at a given time.
 * They aren't conventionally associated with health (barring the little-used phrase "in the pink", which makes no sense in this context if you consider that the hypothetical counterpart "in the blue" means nothing).
 * The words "pink" and "blue" each contain the same number of letters, which is mildly aesthetically pleasing.
 * Pink and blue are (along with white) the colours of the [Transgender Pride flag](https://en.wikipedia.org/wiki/Transgender_flags#/media/File:Transgender_Pride_flag.svg), which hopefully should spark a productive conversation about inclusivity in your workplace.
 * As for any developer who subconsciously assumes that boys are better, and who concludes therefore that the Blue server is the live one, and who deploys new code to the *actually* live Pink server, and who accidentally causes a small amount of downtime and rolls back the service to an old version; they deserve to learn the lesson that they would undoubtedly be taught in that situation.

 The only downsides I can think of are:

 * Gender is a spectrum and this naming convention directly reinforces harmful assumptions about socially assigned gender roles
 * This is entirely too hard to be thinking about such a mild problem

See, it's a practically flawless system!

Other acceptable naming conventions for the Pink/Blue Deployment (hey, it's catching on!) include:

 * Square/Circle
 * Laurel/Hardy
 * Jessie/James
 * Wilbur/Orville (because nobody remembers which one did the flying anyway)
 
 Suggestions welcome!



