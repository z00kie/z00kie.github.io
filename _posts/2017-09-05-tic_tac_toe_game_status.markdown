---
layout: post
title:  "Tic Tac Toe Game Status"
date:   2017-09-05 17:50:16 +0000
---


Until now I've written after I've finished a lab or been walked through a syntax I didn't understand... i thought it might be fun to write as I go this time. I'll be quoting the lesson, sharing my code, and of course giving commentary to the difficulties I encounter. As I want to remain on a somewhat professional level, all profanity will be replaced with cleaner phrases. Come on, I know you curse, too. ;D

So I just opened the lesson page for Tic Tac Toe Game Status and my heart trembled a little: a lab. Great. Then I read the overview:
> We'll be building helper methods that introspect and report on the various game states in Tic Tac Toe, including if the game has been #won?, if the game board is #full?, if the game has been a #draw?, if the game is #over?, and finally who the #winner is.
*Really?!* Solving one or two problems at a time isn't enough for you people anymore?! But *five*? 

I grudgingly start to read through the lesson. I usually try to read through the lesson at least once before starting the lab, though if there seem to be a lot of parts I tend to build the lesson as I go. Scanning through this one I can tell I'll be reading and coding one step at a time. The first is the #win_combinations method and it doesn't look too scary! Yay! I quickly build the code:
```
win_combinations =[
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 4, 8],
  [2, 4, 6],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8]
]
```
Aaaaand I failed the test. 
```
1) ./lib/game_status.rb WIN_COMBINATIONS defines a constant WIN_COMBINATIONS with arrays for each win combination
     Failure/Error: expect(WIN_COMBINATIONS.size).to eq(8)
     NameError:
       uninitialized constant WIN_COMBINATIONS
```
I can see from the error message that for some reason it doesn't see 8 elements in my win_combinations array. Hmm... Do you see it there? At the top? The equals sign is right up against the bracket. If there's one thing I've learned about coding, it's that the individual syntax really like their space. I can relate, but I can't sympathize- just because I have a clingy four-year-old and a huge list of chores to do one right after the other and growing anxiety and panic doesn't mean I break dow- well. Fine. I *can* sympathize. This single space alone, however, does not fix the problem. 

```
1) ./lib/game_status.rb WIN_COMBINATIONS defines a constant WIN_COMBINATIONS with arrays for each win combination
     Failure/Error: expect(WIN_COMBINATIONS.size).to eq(8)
     NameError:
       uninitialized constant WIN_COMBINATIONS
```
Looking at the message closer I see there's a name error. I forgot to put it in all caps. After muttering under my breath I fix this... YES. IT WORKED! *-Ahem-* I mean of course it worked. Right! 

On to the next error message:
```
 1) ./lib/game_status.rb #won? returns false for an empty board
     Failure/Error: expect(won?(board)).to be_falsey
     NoMethodError:
       undefined method `won?' for #<RSpec::ExampleGroups::LibGameStatusRb::Won:0x000000023e6a50>
```
This error is simple! Once I define the #won? method I read:
```
1) ./lib/game_status.rb #won? returns false for an empty board
     Failure/Error: expect(won?(board)).to be_falsey
     ArgumentError:
       wrong number of arguments (given 1, expected 0)
```
So there is an extra argument somewhere? What? Let's read through the lesson; I'm obviously missing something. Oh. I didn't read far enough along in the text. It appears that #won is supposed to accept the board as an argument and return true or false based on the game's status. After another quick fix:
```def won?(board)

end
```
the error says:
```
1) ./lib/game_status.rb #won? returns an array of matching indexes for a top row win
     Failure/Error: expect(won?(board)).to match_array([0,1,2])
       expected a collection that can be converted to an array with `#to_ary` or `#to_a`, but got nil
```

I realize that this entry is getting quite long, so let's do a quick code recap. This is the code I have so far:
```
WIN_COMBINATIONS = [
  [0, 1, 2],
  [3, 4, 5],
  [6, 7, 8],
  [0, 4, 8],
  [2, 4, 6],
  [0, 3, 6],
  [1, 4, 7],
  [2, 5, 8]
]

def won?(board)

end
```
and the error seems to say it expects me to convert my array but I didn't. Time to read further along in the text... 

After reading through the rest of the #won? section, my brain feels sufficiently beaten to mush. I've now been working for almost 6 hours straight(not on this lab alone, mind you) on schoolwork and the words seem to hit my eyeballs and bounce off. I think it's time for a break! My daughter will be home from school soon anyway, so I'm going to grab that as an excuse to set things aside 'til tomorrow. 

Sometimes you just have to know when to set things down...

