## Setting up Ruby 3.0.0 on Windows 10 or WSL2 Ubuntu

***Update***: You can now just do `gem update --system` and be just fine, but the steps are still there for installing RVM.

***

 [Ruby 3.0 was released recently](https://www.ruby-lang.org/en/news/2020/12/25/ruby-3-0-0-released/) and seems to be fully backwards compatible with Ruby < 3.0 (2.7, etc). 

I need a dual setup, as I use a linter and intellisense highlighter in VScode, and the Gem (rubocop and solargraph) won't pick up from WS2L (and I don't think it was designed to, either...).

You can get the installer for Windows [here](https://rubyinstaller.org/downloads/); Just follow the directions in the console and you're good to go. But how about on WSL2/Ubuntu? 

(Also, the bundler/RubyGems steps below, and installing net-http-persistent apply to the Windows version of Ruby 3.0.0 as well!)
 
https://rvm.io/ Is the answer.

First, head to https://rvm.io/

On Ubuntu, install `gnupg2`:

`sudo apt install gnupg2`

Then, as of this writing from https://rvm.io:

`gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`

To receive the keys needed.

Then:

`\curl -sSL https://get.rvm.io | bash -s stable`

To get the current stable version of RVM.

Once RVM is installed, don't forget to follow the `source` directions; it is something like:

``` * To start using RVM you need to run `source /home/aritywolf/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.```

Now that we've got a stable version of RVM installed, it's time to install Ruby 3.0.0:

`rvm install ruby-3.0.0`

Now we have Ruby 3.0 installed with RVM managing the Ruby.

However, there is a slight problem; we receive a RubyGem related error:

```Error running 'run_gem_wrappers regenerate',
please read /home/aritywolf/.rvm/log/1609499010_ruby-3.0.0/gemset.wrappers.default.log```

***

To work around this, use:

`gem update --system 3.1.4`

Then, install Bundler to manage RubyGems:

`gem install bundler`

Then, a workaround to be able to work with `bundler` in Ruby-3.0.0, for **Windows OR Linux**:

`gem install net-http-persistent -v 2.9.4`

In your directory if you're working on a project, you should be able to do

`bundle install`

I had some problems with setting up my sinatra and puma server environment, but Ruby 3.0.0 works as if it were < 3.0.0 otherwise!

Enjoy Your Speed Boost!


Happy New Year!





