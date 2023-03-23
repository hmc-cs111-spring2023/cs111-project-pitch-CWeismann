# Project proposal

## The user and a language

This section describes who the project would serve and why a language might be 
a good way to meet their needs.

### What's the need?

_What need is met by your idea? Who are you helping? What is that person's
experience like now? What would their experience be like if you could help
them?_

The process of designing a board game can be very difficult- there is the need 
to build physical prototypes in order to develop the game further, the need 
for copious amounts of playtesting, and the difficulty of distributing 
prototypes to playtesters. A DSL representing the various components and 
actions that can undertaken in a game would significantly impact the ease of 
development, as (a), digital implementations could be quickly developed and 
iterated on, without the need to build a full GUI interface, and (b), AI could 
be trained to play the game without a full digital adaptation, making 
playtesting a much less people-intensive process.

### Why a language?

_Why is a DSL appropriate for your user(s)? How does it address the need?_

Board games most often have a turn-by-turn structure, so a DSL that represents 
various actions that can be taken works much better than say, a DSL that 
represents controller input in a game of Smash Bros. By removing the need to 
create fully-functioning physical prototypes and even the need to gather 
dozens of playtesters for hundereds of hours, board game designers will be 
able to focus much more on the actual design and development, and less on the 
logistics.

### Why you?

_What excites you about this idea? How did you come up with it?_

I'm a huge board game fan, and I aspire to one day be able to develop one 
myself. After doing a lot of reading about what it takes to design, develop, 
test, publish, and distribute a game, however, I've begun to feel like the 
entire process is terribly unoptimized. It's like if musicians had to build 
their instruments before playing them, or painters had to make their own 
canvases, pigments, and brushes before getting down to work. I feel like 
applying the power of computing to board game creation, without losing track 
of the fact that they are analog, not digital games, is something that could 
make a huge difference for the hobby.

### Domain

_Describe the project's domain in five words._

Developing and playtesting board games!

### Interface (syntax)

_How might the user interact with the language? What does programming look
like? Why is this the right way to interact with the problem domain?_

The user will interact with the language by setting up the various componenta 
and rules of the game in a file, then playing the game through the command 
prompt (although it certainly would be doable to adapt a GUI on top of this). 
This allows for a clean workflow: the playtesters can boot up the file, then 
play the game through their terminal, without necessarily needing to know how 
the game works. The designer can create a file for each game, then customize 
its features for the specific quirks of the game. By providing a list of 
allowable commands to an ML model, the game could also be tested through the 
prompt by a computer, eliminating some of the need for human playtesters. As 
Chris pointed out in my feedback for HW3, this is somewhat similar to how 
Prolog works: a rules file and a REPL.

### Operation (semantics)

_What might happen when a program runs? How does a program interact with the
user? What kinds of errors might occur, and how might they be communicated to
the user?_

When a program runs, all of the various component "piles", decks of cards, 
board positions, etc., will be set up, then a command prompt will open. The 
user will then be able to interact with the program through a finite list of 
commands, e.g., draw card from deck, place token on card, etc. The program 
might have fully programmed actions that do multiple commands at once, e.g., 
draw card, place face down, then place token on that card. For some games, it 
might be helpful to show the user the list of actions available to them, so 
that will be an option that the programmer can include for games with a more 
complex decision space. Errors might involve commands that aren't allowed, 
like drawing from an empty deck, or mistyped commands, like "drawc ard". This 
would probably just alert the user "illegal command: [reason]".

### Expressiveness

_What should be easy to do in this language? What should be possible, but
difficult? What should be impossible or very difficult?_

It will be pretty easy to implement games with a limited amount of visible 
information, like Werewolf, Hearts, Poker, etc. It will be tougher to 
implement games with a significant visible presence, like Chess, where 
visualizing the position of pieces is extremely necessary, or Agricola, where 
a significant amount of card text needs to be visible at once. Features that 
allow more visible information to be printed, like viewing the board after 
each turn, will be implementable, but quite a bit more work. Interestingly 
enough, however, it will actually be easier to design games so that an AI can 
play them rather than a human, as an AI can just take in a list of values 
representing the game state, while a human requires a more visual output. 
Games with significant real-time components will be very difficult to make 
work well, as there is a fundamental disconnect between playing on the screen 
and playing in real life; for a similar reason, any dexterity games, like 
Jenga or Flick 'Em Up, will be basically completely impossible to implement in 
a satisfying way.

### Related work

_Are there any other DSLs in this domain? If not, describe how you know there
aren't and conjecture why not. If so, describe them and provide links. How well
do they address the need? Are there any particularly admirable qualities of the
language? Are there parts of the language you think could be improved?_

https://boardgame-dsl.github.io/haskell/
https://essay.utwente.nl/79157/1/Schroten_BA_ewi.pdf
https://github.com/gergelyszaz/board-game-language

All three of these address my basic goal pretty well- they provide a fair 
mechanic to create games and engage with them. However, I think there are 
aspects of them that some do better than others, and I think I can improve on 
them all with my implemenation.

The first of these is written in Haskell, and allows the games to easily be 
plugged into a web interface which is pretty nice. While I myself am a big 
Haskell fan, the very Haskell-like syntax is not very forgiving for people 
with less of a CS background.

The second is much more readable, although still a bit more obtuse than I 
would like. It's also much more academic than the other two projects, and 
seems to have both the best planning and execution. However, it could use some 
sort of graphical output to make the game more playable.

The third has the most readable syntax, although the language might be too 
simple, and many of the features remain incomplete.

I expect to reference these a bit for high-level concepts, mostly when I get 
significantly stuck on a design aspect.

## The Project

This section examines whether the idea makes for a good CS 111 project.

### Suitability

_If someone were to work on this project, what percentage of their time would be
spent directly engaging in the **language** aspects of this project (e.g.,
making language design decisions), as opposed to "systems" aspects of the
project (e.g., implementing a complicated semantics that doesn't require a lot
of language design)?_

It seems unlikely that an complex semantics system is at all necessary for 
this project. The vast majority of the programmer's time should be able to be 
spent on language design systems. Most of the actual "gameplay" is just 
manipulating items in nested lists and sets, but the design isn't necessarily 
so clear-cut. I expect to have a loop of about 70% design, 30% implementation, 
then test and repeat. My plan is to write an internal DSL in Scala, which 
should reduce implementation time somewhat, leaving me more space for design.

### Scope

_How big an idea is this? How ambitious is this project?_

I think this project is highly scalable: a small version, that could, for 
example, play games that use a 52-card deck, could probably be completed in as 
little as a few days, but with the amount of time we're given to work on this 
project, it could be highly refined, improving usability and power. With even 
more time, it could be developed even  further, with full graphics support and 
some way to play over the internet. The ambition level is whatever you make 
it: it can be as simple as a playing-card game engine or as complex as 
something like BoardGameArena. While I'm not certain exactly how much time the 
design and implementation will take, I suspect that I will be able to 
implement enough to play a fairly complex game.

### Benefits and drawbacks

_Why might this be a good idea for a project? Why might this not be a good idea
project?_

Benefits:
- flexible: a lot of depth that can be explored to whatever degree the programmer wishes 
- should be fairly fun to implement and play around with when completed
- the domain is fairly accessible, as most people have played a board game before

Drawbacks:
- lots of ways to get sidetracked during implementation, leading to feature creep
- implementations already exist
- getting it to be "board game turing-complete" will be a lot of work