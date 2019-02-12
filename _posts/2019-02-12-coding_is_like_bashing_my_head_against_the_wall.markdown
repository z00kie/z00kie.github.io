---
layout: post
title:      "Coding is like bashing my head against the wall... "
date:       2019-02-12 15:10:26 -0500
permalink:  coding_is_like_bashing_my_head_against_the_wall
---


### Eventually, if I just keep at it, I might break through and have a working app!

#### (*AKA My Sinatra App*)

I don't know how lucky or smart you are, but there are times I feel like everyone is smarter or luckier than me when it comes to coding. Those moments are slowly becoming fewer and farther between but when they hit it's still soul-crushing. The inevitable cycle of "Why the [expletive] am I doing this, anyway?" and "I'm the opposite of Midas when it comes to coding- everything I touch crumbles!" begins and I'm forced to grit my teeth and drag my ragged carcass through the minefield even as the arrows begin to fall. Anyone else? Maybe it's just me. 

This portfolio project was no different. At first I was doing great! I had a repository set up on github, the file tree was filled out, I was cruising through the Sinatra section lesson by lesson and slowly building it up... and then the errors started. At first they made sense, but soon all logic and reasoning was lost as the browser told me quite plainly that I needed to add the 'sqlite3' gem despite all my attempts to tell it that it was wrong and my gem 'sqlite3' was actually right there in the gem file why can't you see it oh god... ! So I started over, built it from scratch again, got even farther, and then had a different but equally puzzling error that somehow resulted in me tying my project up in knots. How in the world do you accidentally get an exit error??? What in the world did I do?! It was so bad I had to delete my entire github repo and start over from scratch. 

The next day's attempt had me starting completely over. I built it much faster this time because I was typing out a working copy from the fwitter lab. I molded it as I typed to fit my Author's Sketchbook. It should have worked, but did not. Once again I tried everything to debug. I googled and googled and got one issue fixed after another until... the exit error. No amount of googling would produce an answer. The only clue I had is if you use the command 'exit' syntax and nowhere in my program had I done that. It was an issue with the Ruby language itself, and one I had no idea how to begin fixing. So I started over *again.* And *again*. ... And *again.*

Finally, I was so desparate that I cloned my Fwitter lab and just started changing variables. I dug through line by line and switched it all over and it worked and it was beautiful! So then the next step was the CSS to make it look not so ugly. Again I tried and tried and everyone was saying the same thing, to use the same link syntax to attach your stylesheet(s) to your erb page. But mine. Wouldn't. Work. ALDJFOAUF. So I googled. And googled. And googled. And finally after two hours worth of googling I dug up the most beautiful thing EVER. At least for now. 
``` <link rel="stylesheet" type="text/css" href="<%= url("/style.css")%>"> ```
Thank you LORD. This is an easy way to ensure your erb page finds your stylesheet.

So I *finally* got everything working and tried commiting the final changes to github when I realized in horror that I'd been pushing to the wrong repository. *-facepalm-* What! So I tried pushing my finished app to the correct one but it was too different and said I needed to pull then push. I tried and it failed. I tried everything they said to do and nothing. Then I decided to just create a new repository and push it there and be done. So I did! Yay! Time to record! ... Except it wasn't. It suddenly didn't work.

... 

I went from a functioning, decent little web app back to square one. Back to... you guessed it. Errors. My files had somehow gotten corrupted in trying to pull and push and save my app. I went through and deleted the odd >>>>>>>>HEAD lines, hoping with each refresh the browser would show me a happy teal site. But... !!! Like Satan rearing up to poke you with his pitchfork, up popped my *best* friend the exit error. I broke. My mouse went flying, I'm pretty surprised my desk didn't crack in two from the pounding it took, and I went outside and I *raged* ladies and gentleman. I ugly cried so hard I gave Sloth from the Goonies a run for his money. Ten minutes later when I was stable but shaking like a leaf I walked right back to my desk and started over. I found the last working repository save and I deleted my newest repository on github and I started over from where I began this morning. Fresh repository, working web app, just plain and ugly. Then I went through and added my css changes using the new sparkly link helper I found and I finished the tar out of my project. It's new and it's shiny and it's all done. 

At least half of my commits were lost in the purges. But it's done. My github repositories are currently a mess. But it's done.  I made so many bleeping mistakes. But. It's. Done. 

#### And I learned so much!

I learned 1000 things what *not* to do with git and github. I learned the very very hard way why and how to check to see what repository you are currently hooked up to and how to change it if you're in the wrong one. I learned a fancy pants way of linking your stylesheet so that your web app can find it easily. And I learned that in learning how to do new things you get very, very messy. But that doesn't mean you can't do it. It just means you're giving it your all and will figure it out soon. 

In the end my app doesn't have the features I originally planned but I am still every bit of proud of it. It took way more effort than it looks for me to complete, and I perservered and learned and I did it. And I will continue to learn and grow and get it done because that's what true success is. It's getting messy and discouraged but pushing through and thriving. I'm thankful for this opportunity to learn and look forward to the future.


-------------------

Notes: *I am going to link the horrid evidence here because I'm confident in my failures. Browse my steaming, post-apocalyptic mess of repositories in all their glory. However do not weep for me, friends. Know that I am in a much stronger, better place because of the beautiful destruction you see before you.*

[authors_sketchbook repo](https://github.com/z00kie/authors_sketchbook)

[fwitter lab cum authors_sketchbook repo](https://github.com/z00kie/sinatra-fwitter-group-project-v-000)

[final authors_sketchbook2 repo](https://github.com/z00kie/authors_sketchbook2)
