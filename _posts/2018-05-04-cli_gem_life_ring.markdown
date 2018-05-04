---
layout: post
title:      "CLI Gem: Life Ring"
date:       2018-05-04 15:10:17 -0400
permalink:  cli_gem_life_ring
---


I started out really pumped! I'd been to several study groups, I understood the basics of scraping(or so I thought), and I had my website picked out weeks in advance. Whoo! Let's do this! ... Or not.

The initial idea for Life Ring was to have an instant database of US-based [hotlines](http://www.pleaselive.org/hotlines/) at your fingertips. Abortion, Depression, Domestic Violence, Abuse... you name it, it would have a hotline listed. I stubbed out my program with little to no problems following [Avi's video](https://www.youtube.com/watch?v=_lDExWIhYKI). Then I built my scraper and used binding.pry to ensure I was grabbing the correct data. I was! But there was a huge problem. The page for Please Live isn't set up to properly scrape. The categories are not divided into divs; instead, it's all in one big list. My program was returning all of the category titles as one entry. The organization names? One big list. And the numbers themselves? You betcha. All smooshed together in one big block. Ugh.

I spent too much time trying to figure out what I was doing wrong. When I finally asked for help with a 1:1, I was told that my suspicions that I'd have to find a different website to use were correct. My heart dropped like lead. I had been so excited about this project! I was going to create something that would make a difference, gosh darnit! But it wasn't meant to be. Instead, after an intense googling session, my 1:1 mentor said that the [Suicide LIfeline](https://suicidepreventionlifeline.org/) was probably my best bet. I grudgingly agreed, knowing it was either this site or starting completely over from scratch.

I was able to plug in the new site pretty easily, and used pry to once again grab the data I needed. But there was another problem. How would I scrape the details off of a second page? How do you chase the information through the tubes?

```
class LifeRing::Scraper
  attr_accessor :name, :url, :topic, :section, :contact


  def self.grab_page
    @doc = Nokogiri::HTML(open("https://suicidepreventionlifeline.org/"))
    @doc
  end

  def self.main_menu_info
      grab_page.css("div.im-struggling-grid a.button--struggle").each do |info|
        @topic = LifeRing::Topic.new(info.attr("href"))
        @topic.name = info.css("span.button--struggle__text").text
      end
    end

  def self.page_menu(topic)
        @details = Nokogiri::HTML(open(topic.url))
        @details.css("main.main").each do |info|
          topic.summary = info.css("div.intro").text
          topic.contact = info.css("div.contact-box a").first.text
        end
      end
    end
```

I half-figured out **.page_menu** on my own and then had more help in figuring out why it wasn't working.  I had started out with **.page_menu**'s topic.summary and topic.contact as instance variables, but this confused the program and kept breaking it. Then I turned them into local variables for this method alone and it worked. I use **.grab_page** to scour the Lifeline's web page and then use **.main_menu_info** to grab the items to create the menu. Lastly, **.page_menu(topic)** is used to provide the user with the details of each topic.

The CLI class was pretty easy except for the menu. I wrote most of it in one go; the **#menu** method was of course the most difficult. If you don't set up your if/else statements properly your program can and will tie itself in knots. I tried if/else, then I tried case, then I went back to if/else... Using a mixture of pry, google, and Flatiron videos I managed to bang out a lot of the dents. For those things that I couldn't I used the 1:1 option. Here is my CLI class in full:

```
class LifeRing::CLI
  attr_accessor :topic, :name, :url, :section


  def call
    opening
    LifeRing::Scraper.main_menu_info
    hotline
    menu
  end

  def opening
    puts " "
    puts " #       #####   #####   #####"
    puts " #         #     #       #    "
    puts " #         #     ####    #### "
    puts " #         #     #       #    "
    puts " ######  #####   #       #####"
    puts " "
    puts " ####    #####  ##   #  #### "
    puts " #   #     #    # #  #  #    "
    puts " ####      #    #  # #  #  ##"
    puts " #   #     #    #   ##  #   #"
    puts " #    #  #####  #    #  #####"
    puts " "
    puts " "
    puts "The National Suicide Prevention Lifeline is a national network of local crisis centers that provides free and confidential emotional support to people in suicidal crisis or emotional distress 24 hours a day, 7 days a week. We're committed to improving crisis services and advancing suicide prevention by empowering individuals, advancing professional best practices, and building awareness."
    puts " "
  end

  def hotline
    puts " "
    puts "We can all help prevent suicide. The Lifeline provides 24/7, free and confidential support for people in distress, prevention and crisis resources for you or your loved ones, and best practices for professionals."
    puts " "
    puts "For help, call 1(800)273-8255"
    puts " "
  end

  def list_topics
    LifeRing::Topic.all.collect.with_index(1) do |topic, index|
      puts "#{index}. #{topic.name}"
    end
    puts ""
  end

  def topic_sections(topic)
    LifeRing::Scraper.page_menu(topic)
    puts "#{topic.name}"
    puts ""
    puts "#{topic.summary}"
    puts ""
    puts "Please call #{topic.contact}"
    puts ""
  end

  def  menu
    input = nil
    list_topics
    puts "Enter a number to see more information, or type 'menu' to see the menu or 'exit' to leave."
    input = gets.strip.downcase
    if input == "exit"
      goodbye
    else
      topic = LifeRing::Topic.all[input.to_i - 1]
      selection = input.to_i
      if selection.between?(1, 9)
        user_input = LifeRing::Topic.find(input)
        topic_sections(topic)
        puts "Would you like to learn more about another topic? Y/N"
        again = gets.strip.downcase
        if again == "y" || again == "yes"
          menu
        else
          goodbye
        end
      else
        puts "Please try again."
        puts ""
        menu
      end
    end
  end

  def goodbye
    puts " "
    puts "Thank you for using Life Ring. We wish you a happy and healthy future!"
    puts " "
  end
```

I put my opening before the scraper so that the user has something to look at for the milisecond that it takes to scrape the data. Then I list the Lifeline's number so that it's right up front in case the user needs it right away. Next the menu runs most of the program, and finally everything ends with the **#goodbye** method. If you follow through the menu, you can see that each round starts with a list of the topics. The user follows directions and enters a menu selection, which uses **LifeRing::Topic.find(input)** to match up the selection with the correct details page. **#topic_sections(topic)** then prints out all of the details for the user to read through, including the relevant phone number to call for help. The user is then asked if they'd like to view another topic, and the program reacts accordingly.

I will most definitely not be publishing this gem. It's not because I don't think it works well. It's because it isn't a sliver of the gem I originally had in mind; I just don't like it. I don't think it was a waste of time as I've learned quite a lot. Maybe some day I'll make something worth publishing but this just isn't it, and I'm perfectly okay with that. I've built my first fully-functioning program from scratch, and that's definitely something to be proud of.

# My Take-Aways
* Is your data properly div'ed out on the web page? Does each category or section have it's own div? If not, it may be too difficult. Even if you've picked a page, know that you may not be able to stick with that page.
* You know more than you think you do. When you don't, use pry! Binding.pry is a great way to view the values of different variables and methods, target the data you wish to scrape, and experiement with code. I've solved a lot of issues with pry alone.
* When you get discouraged, ask for help. It doesn't matter how much you tell yourself you just aren't smart enough, how you'll never get it, or even how dumb and worthless you feel. More than likely the problem isn't because you're dumb. It's because it's something you just haven't become familair enough with yet or it's something that can't be done(or can't be done easily).
* **You can do this! Good luck!**


### *My repository: [Life Ring](https://github.com/z00kie/life_ring)*
