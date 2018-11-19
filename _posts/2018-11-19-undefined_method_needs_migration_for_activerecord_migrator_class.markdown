---
layout: post
title:      "Undefined method `needs_migration?' for ActiveRecord::Migrator:Class"
date:       2018-11-19 17:19:08 +0000
permalink:  undefined_method_needs_migration_for_activerecord_migrator_class
---


This little error was giving me a HUGE complex. I thought I had done everything correctly; I went through and deleted my Gemfile.lock so that I could bundle install a fresh set... and quickly found out that deleting your Gemfile.lock can actually be a *horrible* idea. Like letting your mothball-reeking great aunt May get a better lookatchu. Just. Don't. Do it.

I have been stuck on this very same lab for almost a week now. First I couldn't get the tests to run because I deleted my Gemfile.lock and it screwed up how my program processes things

```
undefined method `needs_migration?' for ActiveRecord::Migrator:Class
```

Basically doing that created an error because the method that worked for one version did not for the newest. So I deleted the entire lab including all of my work to start over. It's just more practice, right? Great!

This time I tried bundle installing straight away, figuring it would work itself out. I made it as far as about 80% through the project and then couldn't move forward because shotgun wasn't working. So I tried uninstalling and reinstalling the gems using my good ol' process of deleting my Gemfile.lock. I had to start over *again*. Okaaay. Fine. More practice will help me remember things better. By this time I had been working on it for a whole day and a half and figured I'd just ask for help in the morning. 

Whelp. Flatiron's Ask a Question did help! ... sort of. After taking a look at things we couldn't figure out what was going wrong and I was advised to delete the entire repo, refork the lesson, and start over. *Again*. Alright! I can whip through it this time! I worked diligently as I built up all the parts of my app. Once again I got stuck with three errors left, and once again shotgun failed. 

```
Gem::LoadError: You have already activated rack 2.0.6, but your Gemfile requires rack 2.0.4. Prepending `bundle exec` to your command may solve this.
```

Rawr! Again? This time I spent a bit more time searching and reading other experiences and found something called 'bundle update' which updates the Gemfile.lock instead of deleting things and replacing them. Maybe it would work better than my previous method! Yes! ... Nope. Now I am back to the brick-wall error I had before:

```
undefined method `needs_migration?' for ActiveRecord::Migrator:Class
```

 Really? ... You know, I should probably just google that error message. I did so, *finally*, and found that I simply(*simply*) had to change my config.ru file to read:
 
 ```
 if ActiveRecord::Base.connection.migration_context.needs_migration?
  raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end
```

instead of this:

```
if ActiveRecord::Migrator.needs_migration?
  raise 'Migrations are pending. Run `rake db:migrate` to resolve the issue.'
end
```

And voila! Now shotgun works and I can work through the issues! Yeah!

The real lesson is that I need to continue working on how to not assume it's my fault that something isn't working and let guilt and anxiety cloud my mind. Having general anxiety disorder and trying to do *anything* is hard, but having it while coding can really cause me to get stuck sometimes. Luckily I am a very persistant person who keeps trying no matter what. You can't tell me it's impossible! 

So be like me and just google your errors right away as they pop up. But don't be like me and assume the issue is something unfixable. We are coders. Our job is constantly fixing things that shouldn't be fixable. Much love! <3
