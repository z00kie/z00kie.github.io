---
layout: post
title:      "Yield - It's Like a Sandwich"
date:       2017-11-17 16:06:12 +0000
permalink:  yield_-_its_like_a_sandwich
---

Okay, so my last attempt at writing a technical entry SUCKED. It was awful. I was writing as I coded and it was completely messy and horrendous and just gross. I've actually been afraid to write anything else because I made such a mess. While the title of this post may be a bit confusing it will be much clearer, I promise you. 

If you are a visual person like me, learning to code is super hard. Your brain is constantly trying to figure out what line of code makes what piece of your current build. Your project is(usually) super complex with many parts working together, and not all of those parts translate into a single piece by themselves. This makes for many a migraines as I try to smash a round lesson-peg into a giraffe-shaped hole. It's just not going to go! I have to then tear away all my expectations and try to find a working analogy that will help me finally understand what it is the lesson is talking about.

This morning I stared at the [Yield and Blocks](https://learn.co/tracks/full-stack-web-development-v3/procedural-ruby/iteration/yield-and-blocks?batch_id=306&track_id=28005) reading for like ten minutes as I read and reread and tried to get what exactly was happening. Then I clicked on and scanned over all four of the extra resources at the bottom. Then I reread and reworked the lesson again, this time paying extra attention to what I was typing as I was reading and copying. I still didn't get it, so I returned to the very simple example given at the beginning of this lesson:

```
def yielding
  puts "the program is executing the code inside the method"
  yield
  puts "now we are back in the method"
end

yielding { puts "the method has yielded to the block!" }
```

Something tickled at the back of my brain. I was starting to comprehend. It was there, knocking at the door... but... 

**OH. IT'S LIKE A SANDWICH. OKAY. YEAH!**

So here is what my brain finally put together:
![](https://imgur.com/jWA3Cqg)

![](https://imgur.com/qB1dpcB)

Ohhhhh! Right! So the first method is like the bun and the yielding method is like the meat. #yielding starts to run, but then pauses to grab the second block of code down there before continuing to the bottom of the sandwich. I know my brain is weird and needs some sort of visual reference to learn. Sometimes it's decorated boxes or bulletin boards(HTML and CSS) and sometimes it's sandwiches. What sorts of weird things does your mind come up with? I know I can't be the only one. Happy learning!

