---
layout: post
title:      "Dinosaur_directory.rb - Class Variables and Methods Lab"
date:       2017-12-13 12:41:17 -0500
permalink:  dinosaur_directory_rb_-_class_variables_and_methods_lab
---


So I don't know about you, but sometimes after I've managed to complete a lab things still seem a bit foggy. When this happens, I tend to rebuild the lesson or lab using themes that I am more interested in. Recently I've been stuck on dinosaurs because you can classify them in so many different ways. They work excellent for nested hashes and more complex programs as well- you can make them roar, classify them by different traits, etc. They work really well for a learning clone of the [Class Variables and Methods Lab](https://learn.co/tracks/full-stack-web-development-v3/object-oriented-ruby/class-variables-and-methods/class-variables-and-methods-lab?batch_id=306&track_id=28005), as well.

There are a lot of things this lab is looking for, and I had to use "learn --f-f" instead of "learn test" in order to sort through everything; if a lab has a lot of tests with it I tend to get overwhelmed. For all of these tests to pass, we need a properly defined class that initializes with a song name, artist, and genre. It needs to keep a count of all the songs passed in as well as print off a list of the genres and artists that have been submitted. Lastly it needs to give a hash with the genres and their amounts and do the same for the artists. Let's see if we can do that with dinosaurs instead!

The first step is defining your class and setting up the initialize method- the framework of the class method we're building. We need to think about what our class method will be doing- it will be storing and working with our dinosaurs' traits as well as keeping a count on everything going on. For that we will need some (attr_accessor)'s for the constants: name, color, and type. We also need to set up the base of our counter as well as our color and species database, in this case a couple of arrays. After we have our arrays and counter set up we can fill in our #initialize method.

```
class Dinosaur
  attr_accessor :name, :color, :species
	
	@@amount = 0
	@@colors = []
	@@species = []
	
	def initialize(name, color, type)
    @name = name
	  @color = color
		@species = type
		  @@amount += 1
			@@colors << color
			@@species << type
	end
	
end
```

We want to save the colors and species each and every time we create a new dinosaur as well as count each incoming entry every time a new dinosaur is introduced. That is why we've placed the shoveling(saving) action and counter @@amount increments in our #initialize method.

This lab is asking for a way to count all the entries; in our case we need to be able to count all the dinosaurs. It's really as simple as returning your @@amount counter. After that, we need a way to print off a list of all the colors and species if anyone asks for them. But how do we do this without having duplicates? If there are five T-Rexes we don't want it listed five times. This took me a bit to figure out, but I stumbled across the method .uniq. I was googling 'ruby pick unique elements from array' and found it. Thus I was able to easily set up the next two methods: #self.colors and #self.species.

```
def self.count
    @@amount
  end

  def self.colors
    @@colors.uniq
  end

  def self.species
    @@species.uniq
  end
```

The last two methods were the hardest. I honestly had no idea where to even start at first, but then I broke it down. For a #self.color_count and #self.species_count(in the lab's case genre and artist counts), we would need to set up an empty hash to put our new keys and values into. Then we would need to iterate through the proper array and create those keys and counts. Finally we need to print the hash to the screen. 

> A quick aside: my biggest problem is not being able to easily turn word problems into code. If you're like me, hang in there and keep trying! Redoing labs like this one using terms you're familiar with or interested in seems to help a lot! Your brain is able to latch on to something familiar and go from there.

I was mostly confused with how to get the info into the key => value format. After a lot of searching and many edits I figured out that all I had to do was format it to get the correct amount of each key and Ruby would do the rest. So here is our code for #self.color_count and #self.species_count:

```
def self.color_count
    dino_colors = {}
    @@colors.each do |color|
      if dino_colors[color]
        dino_colors[color] += 1
      else
        dino_colors[color] = 1
      end
    end
    dino_colors
  end

  def self.species_count
    dino_species = {}
    @@species.each do |type|
      if dino_species[type]
        dino_species[type] += 1
      else
        dino_species[type] =1
      end
    end
    dino_species
  end
```

That is the last of it. We now have a fully-functioning dinosaur database that can keep track of two aspects(color and species) as well as give an accurate count of pretty much anything you ask for(color, species, Dinosaurs). For fun I've added a few extra functions as well. Here is my final program:

```
class Dinosaur
attr_accessor :name, :color, :species

@@amount = 0
@@colors = []
@@species = []

def initialize(name, color, type)
	@name = name
	@color = color
	@species = type
		@@amount += 1
	@@colors << color
	@@species << type
end

def self.count
	@@amount
end

def self.colors
	@@colors.uniq
end

def self.species
	@@species.uniq
end

def self.color_count
	dino_colors = {}
	@@colors.each do |color|
		if dino_colors[color]
			dino_colors[color] += 1
		else
			dino_colors[color] = 1
		end
	end
	dino_colors
end

def self.species_count
	dino_species = {}
	@@species.each do |type|
		if dino_species[type]
			dino_species[type] += 1
		else
			dino_species[type] =1
		end
	end
	dino_species
end

def roar
	puts "#{@name} rears its head back and lets out a soul-shattering roar."
	puts "Your pants are wet."
end

def eat(food)
	puts "#{@name} gobbles the #{food} up hungrily."
end

def dance
	["#{@name} does the Cotton Eye Joe rather well. You are impressed.", "#{@name} trips over themselves trying to do an Irish jig.", "With a flourish, #{@name} spins around and moonwalks away."].sample
end

end
```

Here is a short list of dinos to use if/when you play with it in irb:

```
yen = Dinosaur.new("Yen", "Black", "Pterodactyl")
tina = Dinosaur.new("Tina", "Pink", "Brontosaurus")
rex = Dinosaur.new("Rex", "Brown", "T-Rex")
shir = Dinosaur.new("Shirley", "Orange", "Brontosaurus")
tuli = Dinosaur.new("Tuli", "Black", "Tortoise")
frank = Dinosaur.new("Frank", "Brown", "T-Rex")
opka = Dinosaur.new("Opkar", "Orange", "Tortoise")
rosk = Dinosaur.new("Roski", "Pink", "T-Rex")
```

For the #dance method, I wanted to make it have random returns. Using the .sample method on an array was the only thing I could find. I have no idea if there's a better way or not, but for now it works just fine. Enjoy!
