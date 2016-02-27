---
layout: post
comments: true
title:  "Ruby Based Scripts"
date:   2016-02-27 01:15:00
categories: Ruby, Scripting, Design Patterns, Startup
---

<b> <a href='https://github.com/pramod-sharma/ruby-script'> Ruby Scripts Bootstrap </a> </b>

If you are using Ruby beyond Rails as scripting language, you might have got yourself strucked with long running single file scripts with thousand of LOCs and hundreds of require statements with no way to properly synchronize Gems among other team members
and in production environment.

Thats when I thought of bootstraping my own Ruby Scripts directory structure for own use. Hopefully it will help you for better scaling your Ruby Scripts

You may found the repository <a href='https://github.com/pramod-sharma/ruby-script'> here </a>.In case you wants to extend it for your own use, its free to fork

Now going on with Directory Structure :-

* <b> config/ </b> - It includes config yml files, boot.rb and initializers, which will further include scripts to be called at the time of initialisation. boot file is the position where one must require one's initalizer scripts, ruby libraries and constants as well for script which includes Logger constant whose position you can alter.

* <b> data/ </b> - My ruby script is one for analytics hence I to work on lots of data processing thats the reason I opted for a data folder to include all data files at one place and work on it from my scripts

* <b> lib/ </b> - It is the folder where one must keep one's own libraries directly related to script and call them from main script

* <b> log/ </b> - It includes log files created during the script execution phase.

* <b> utils/ </b> - It includes the file not directly related to script but can act as a utility for your script. For example in my case I have an S3 utility to recursively download the S3 folder

* <b> Gemfile and Gemfile.lock </b> This file servers the same purpose for maintaining Ruby gems

* <b> .ruby-version </b> - To follow the same ruby version in production and across team as well

* <b> main.rb </b> - This is the root file of whole script which one must call directly or in cron it must use all above mentioned libraries for achieving the functionality.

In case you find any issue or improvement or just loved it please drop a comment in comment box.

<b>Note to self </b> :- I will surely add a better readme in the github repository itself once enough space.  