---
layout: post
title:  "Tic Tac Toe Game Status(Part 2)"
date:   2017-09-08 10:05:58 -0400
---


Alright! New day! Fresh start! Whoo! I was working on the #won? method, so let's take a look at the code and then the error:
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
```
1) ./lib/game_status.rb #won? returns an array of matching indexes for a top row win
     Failure/Error: expect(won?(board)).to match_array([0,1,2])
       expected a collection that can be converted to an array with `#to_ary` or `#to_a`, but got nil
     # ./spec/game_status_spec.rb:35:in `block (3 levels) in <top (required)>'
```

After about twenty minutes of flipping through pages and staring at code, I've managed to get my brain back on track. For awhile there I was worried I had gotten completely lost. This is one of the dangers of pausing in the middle of a lab. The text for this lab has a very good example of how to set up the #won? method. YAY. I love getting help without having to ask for it, don't you? I set up my method like so:
```
def won?(board)
  WIN_COMBINATIONS.each do |win_combination|
    win_index_1 = win_combinations[0]
    win_index_2 = win_combinations[1]
    win_index_3 = win_combinations[2]
    win_index_4 = win_combinations[3]
    win_index_5 = win_combinations[4]
    win_index_6 = win_combinations[5]
    win_index_7 = win_combinations[6]
    win_index_8 = win_combinations[7]

    position_1 = board[win_index_1]
    position_2 = board[win_index_2]
    position_3 = board[win_index_3]
    position_4 = board[win_index_4]
    position_5 = board[win_index_5]
    position_6 = board[win_index_6]
    position_7 = board[win_index_7]
    position_8 = board[win_index_8]

    if position_1 == "X" && position_2 == "X" && position_3 == "X"
      return win_combinations
    else
      false
    end
  end

  end

end
```

And just as I hit enter to start the test I realized I have a syntax error- too many ends. Once I take one out, I get the following error message:
```
1) ./lib/game_status.rb #won? returns false for an empty board
     Failure/Error: expect(won?(board)).to be_falsey
     NameError:
       undefined local variable or method `win_combinations' for #<RSpec::ExampleGroups::LibGameStatusRb::Won:0x000000021a77f8>
```
Once again I forgot to capitalize WIN_COMBINATIONS. So I have to fix all those tags. You can bet from now on I'm going to be much more careful about everything matching up! Now the error message is:
```
 1) ./lib/game_status.rb #won? returns false for an empty board
     Failure/Error: expect(won?(board)).to be_falsey
     TypeError:
       no implicit conversion of Array into Integer
	```
	Something isn't matching up. Let's compare the code(top) to the error message. Seeing them next to each other makes it easier for me to figure out what's going on:
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
  WIN_COMBINATIONS.each do |win_combination|
    win_index_1 = win_combination[0]
    win_index_2 = win_combination[1]
    win_index_3 = win_combination[2]

    position_1 = board[win_index_1]
    position_2 = board[win_index_2]
    position_3 = board[win_index_3]

    if position_1 == "X" && position_2 == "X" && position_3 == "X"
      return win_combination
    else
      false
    end

  end

end
```

```
1) ./lib/game_status.rb #won? returns false for an empty board
     Failure/Error: expect(won?(board)).to be_falsey
       expected: falsey value
            got: [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 4, 8], [2, 4, 6], [0, 3, 6], [1, 4, 7], [2, 5, 8]]
```

I had been trying to make things overcomplicated- I didn't understand how this method was functioning and so assumed that I needed an entry for each individual win combination. After realizing that it seemed to have too many parts, I deleted all the extra lines. Bam! Now we're on to a different error! I can see that this part of the method seems to have a couple of layers. There's the position_# layer which picks out each box and then the win_index_# which seems to put them together into a win_combination. Cool! Now let's take a look at this new error mressage. It's not returning false if there isn't a win combo. Hmm... 

I searched through the text for help, but couldn't find it. Next I read through all the open questions, hoping that someone is having a similar issue and I can learn from their discussion. I found one! The instructor, one Mr. Michael Djurdjevic, pointed out that he had his else inside the loop. This means that every single time the program loops it will return on a win_comination or not at all. So we need to slide our else/false lines down and out of the loop somewhere.
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
  WIN_COMBINATIONS.each do |win_combination|
    win_index_1 = win_combination[0]
    win_index_2 = win_combination[1]
    win_index_3 = win_combination[2]

    position_1 = board[win_index_1]
    position_2 = board[win_index_2]
    position_3 = board[win_index_3]

    if position_1 == "X" && position_2 == "X" && position_3 == "X"
      return win_combination
    end

  end
else
  false
end
```
Let's see if that works!
```
 1) ./lib/game_status.rb #won? returns an array of matching indexes for a left column win
     Failure/Error: expect(won?(board)).to match_array([0,3,6])
       expected a collection that can be converted to an array with `#to_ary` or `#to_a`, but got false
			 # ./spec/game_status_spec.rb:53:in `block (3 levels) in <top (required)>'
```
Mostly green! Except the last part. Drat! Not wanting to cheat, I decide to check out the spec file. According to the error message, I need to see line 53. It's linked to an example of the O's winning, and I immediately realize where my mistake is. I have an if statement that talks about the X's winning but I neglected to add the O's. Whoops! After a quick edit of "|| position_1 == "O" && position_2 == "O" && position_3 == "O"' to the X line, I see:
```
1) ./lib/game_status.rb #full? returns true for a draw
     Failure/Error: expect(full?(board)).to be_truthy
     NoMethodError:
       undefined method `full?' for #<RSpec::ExampleGroups::LibGameStatusRb::Full:0x00000001e70698>
     # ./spec/game_status_spec.rb:85:in `block (3 levels) in <top (required)>'
```
YAY. I MADE IT THROUGH THE FIRST METHOD. And bonus! I understand all of the working parts now! I did my trademark WHOO! dance as soon as I realized. Maybe y'all will get lucky one day and I'll do it for you. Maybe. In the meantime, I need to read through the #full? section and see what's going on.

It's like an hour later and I'm still staring at a blank #full? method. I did have about a 15 minute break in there, so that's 45 minutes of wandering around in circles. I googled Ruby iterators and different keywords and came across different search/select iterators. None of them worked, however. Next I go back to the student "Ask a Question" section and found the same student as before chatting about the #full? method. He had used the iterator #all?, which I promptly googled:
> Passes each element of the collection to the given block. The method returns true if the block never returns false or nil. 
> -- apidock.com


Awesome! So now I have an easy way to check if all the boxes are full at once! I love easy! My code now looks like:

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
  WIN_COMBINATIONS.each do |win_combination|
    win_index_1 = win_combination[0]
    win_index_2 = win_combination[1]
    win_index_3 = win_combination[2]

    position_1 = board[win_index_1]
    position_2 = board[win_index_2]
    position_3 = board[win_index_3]

    if position_1 == "X" && position_2 == "X" && position_3 == "X" || position_1 =="O" && position_2 == "O" && position_3 == "O"
      return win_combination
    end

  end
else
  false
end


def full?(board)
  board.all? do |box|
    if box == "X" || box == "Y"
      return true
    end
  end
else
  return false
end
```

The next error message says:
```
1) ./lib/game_status.rb #full? returns false for an in-progress game
     Failure/Error: expect(full?(board)).to be_falsey
       expected: falsey value
            got: true
     # ./spec/game_status_spec.rb:91:in `block (3 levels) in <top (required)>
```

So this means my return false is in the wrong spot. Or not. I played around with this method, moved some parts, made it worse, panicked, fixed it back up, and was still stuck. Round and round she goes! If she'll get it, no one knows! Actually I did get it, finally! There doesn't need to be an if statement:
```
def full?(board)
  board.all? do |box|
    box == "X" || box == "O"
  end
end
```
I suppose it's implied? Not too sure about that, but for now that's what I'll go with. Now I'm on the #draw? method. 

--- (@) ---

So once I hit this point I was starting to get tired, which meant my anxiety was intensifying. I read through the #draft section several times while trying to code it out. I ended up being totally lost, confusing myself, and then feeling ashamed that I needed to ask -*again*- for help. That's three Ask a Questions in three days! Come on! I should be getting this!!! Unlike 'normal' people, if you have anxiety issues the thought of asking for help is overwhelming. Suffocating depression swelled over me once again, all because I wasn't understanding how to build the #draw method and felt like I was asking too many questions. I ended up shutting down my laptop and walking away because I was too mentally stressed- it was so bad that it seeped into the physical realm. Super nauseous, fatigued, having chills, migraine... Yummy fun stuff!

Yesterday morning in my shower time I meditated over what had happened and almost immediately felt ashamed. If I were to get a new job in this field and didn't understand something, would I shut down like this? I'd be fired! Bossman don't care about anxiety! He ultimately only cares about my ability to get the job done. After the shower I had two meetings- the first was with Miss(Mrs?) Christina Cole and the second with Mr. Ian Candy. Just listening to Christina mention her own difficulties and experiences were very soothing to my bruised psyche. She got stuck, too! Whoa! (Haha! It's okay to laugh!) She informed me that it was not only okay to ask questions, but it was okay and expected that I ask *lots* of questions. Ian restated and enforced this. By the time i was done I felt exhausted and head-achey from speaking to 'new' people, but was bouyed spiritually knowing A)I'm not alone in my struggles and B)there's really not a question cap(unless you expect people to do it for you, obviously). Sweet!

It took me all of yesterday afternoon to unwind and heal through the impact of being so wound up, but this morning I feel so very positive about moving forward. I have a new plan set in place to enhance my learning experience and pace and I can already feel my momentum strengthening. Huzzah! As Artemis Gordon says: Avanti!
