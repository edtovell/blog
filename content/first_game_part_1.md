Title: Things I Learned While Trying to Learn Game Development
Date: 2020-March-01
Modified: 2020-Jan-01
Category: dev-stuff
Slug: first_game_1
Authors: Ed
Summary:

I am very bad at doing things in my spare time, but I have been trying to do this for about two years and finally have some embarassingly small first steps to show for it.


# Pick a free technology and a free tutorial
You can't just "learn game development", that's like saying you want to "learn books". I knew I had to narrow it down a bit, so I decided to learn Unity because I see it everywhere and it was free (my personal motto is basically **never ever pay for anything, ever**). I found what looked like a good (free) tutorial where you [make a 2D roguelike](https://learn.unity.com/project/2d-roguelike-tutorial).


# Admit when you're wrong, and then pick again
I finished every video in the tutorial and got the game working perfectly and I have no idea how I did it. The tutorial was fine, but I didn't actually learn anything - I just followed the instructions and wrote the code they told me to write. Looking back now I could probably just about tell you what a given individual function does, but I have no idea how the thing is structured, and if it broke I wouldn't have any idea how to fix it.

That was very sad and quite discouraging, because I'm quite clever and good at computers and stuff, and frustration and non-understanding are feelings I associate more with my social life. This is supposed to be fun. Unity is just way too much for a first try - I wanted something less GUI-y and more codey, and ideally much smaller and in a language I already know a bit about, but also well-documented and with a large enough community that there would be some tutorials and also free. So I settled on [phaser](http://www.phaser.io/), partly because I've seen HTML and JavaScript before and I'd been meaning to bone up on my JS for a while, but also mostly because I saw [Pippin Barr](pippinbarr.com) used it a couple of times and everything he does is great (I like [this](http://www.pippinbarr.com/games/getxavoidy) for example).


# Having a highly depth-first-biased sense of priorities is sometimes OK
by which I mean, the tendency to want to finish task X before starting task Y, even if X takes ages and spins off into something else entirely. I do it a lot. I have heard this called "rabbitholing" and "yak shaving", which is fine except that the catchy nicknames make it easy to dismiss as a bad thing. This old [blog](https://mariapacana.tumblr.com/post/78260425415/the-never-ending-patch) I found is really interesting because it acknowledges both sides: yes, focussing too hard on one issue can reduce your "productivity", but you also learn a lot when you absolutely must understand everything before you proceed.

In this case, I had finished this [2D Platformer tutorial](https://phaser.io/news/2018/04/phaser-3-platformer-tutorial) and found myself deeply unsatisfied with the character's jump physics. You tap the spacebar and the guy zooms up into the air, then floats down and bounces unconvincingly. I couldn't get it right just fiddling with the parameters, so I saw an opportunity to branch off and go beyond the lesson: try to implement a more responsive and satisfying jump. Thus begun several days of googling and reading and trial-and-error testing of all the various methods and schools of thought on 2D platformer jumping.

That's why I put "productivity" in scare quotes before; if I had been at work and I had a ticket on for "getting the guy to jump", I should/would probably have left the crappy jump in place and moved on to the next thing. But since this is my free time and I have no stated goal or motivation other than to learn stuff, indulging my inner cattle barber and spending a week reading tangentially related blogs and stack exchange posts is a perfectly reasonable option.

I didn't get a game out of it, but I know lots of other stuff now, and not just to do with jumping! I know a little bit about how and where to represent other kinds of physical effects, like collision and friction; I know how to represent a player as an object and as a state machine, and why you might want to do that; and I know a bunch of ways to get a sprite to go up and then down again in a way that satisfies the fingers. So the rabbit hole isn't good or bad in itself, but it's good to bear context in mind and know what you want to achieve. 


# Embrace the fear and panic of not knowing how anything works
I took French classes at uni many years ago, and I did German A Level at school many years before that. I loved German when I started because learning a language was new to me. By the time I got to A Level I could throw out all kinds of sentences off the cuff, like "this wine displeases me as it stinks of pretention" and "so what's your opinion on the state of the arms trade?" (I can't do it any more, it's been too long, but I'm still pretty confident I knew how to say those things before). Then when I started French I found myself getting very upset that I was reduced to basics like "My name is Ed and I live in London", when what I really wanted to say was "this band is blandly derivative of Neutral Milk Hotel and the bassist's moustache makes him look like a sex offender". I totally sucked at French and I still do. It was a difficult time.

Anyhow, even though I'm still a relative newbie to the "computers-and-stuff" scene, what I know best is Python and web service development. So it comes as a bit of an ego-fart when I feel like I could code up a kickass REST API with a bunch of nifty custom request headers and paginated rate-limited responses, and now I'm reduced to "make the man go up and down". It's a little bit demeaning.

But that ***is*** where I'm at, and I have to accept and embrace that. I have to somehow take pride in the small achievements, knowing they're small in the grander scheme of things, but still holding on to the fact that they're big for me at this stage. I still don't know how I'm going to do it, but I hope I get better at it. Maybe that's a skill to be learned in itself.


# My game sucks (so far)
So here's my game so far. It's called "Get The Hat" and it currently has the following glaring errors:

 * There is no menu or HUD of any sort
 * No music or SFX
 * No stated goal
 * No adverse conditions (moving platforms, enemies, spikes, etc)
 * No hat

And also these minor things that I want to learn how to fix

 * Pixel bleed in between the tiles
 * Deciding a way to handle diagonal movement, or what happens when you press left and right at the same time
 * I'd like to give the player sprite an idle animation, just for fun
 * I'd like to figure out friendly NPCs and dialogue
 * I'd also like some combat, and presumably some enemies too

But I like how the guy waddles.
<div>
	<iframe src="http://edtovell.com/get-the-hat-v1/" height=600 width=800 style="transform: scale(0.75);"></iframe>
</div>
(Note: this might change or move or something as I build on it, but you can always see the work in progress version in the history at github dot com slash ed tovell)
