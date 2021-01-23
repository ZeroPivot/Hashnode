## Notes On Debugging Ruby's Sinatra Server in VScode, using WSL-remote

This assumes that one knows how to use WSL-remote in VScode (see previous posts for more information: https://zeropivot.xyz/update-notes-on-how-to-use-wsl-remote-with-wsl2-and-ruby-300)

https://github.com/microsoft/vscode-recipes/blob/master/debugging-Ruby-on-Rails/README.md

Based on the link posted, one is able to get Sinatra + Puma Server working with VScode + WSL remote

I pieced together some notes that will attempt to clarify the process of setting up the debugger.

I am using in WSL2:

- Ruby 3.0.0
- Sinatra web framework gem
- Puma server gem

First, install the appropriate gems for debugging:

```
gem install debase
gem install ruby-debug-ide # vscode has settings for this by default
```

With that out of the way, we can get onto configuring VScode

![Code_-_Insiders_2021-01-23_12-20-52.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611433295743/_arYMercd.png)

You will see a little wheel gear, and most likely Listen for rdebug-ide, and there you can edit launch.json. Go ahead and edit it.

The code to add to launch.json:

```
 {
            "name": "Debug Sinatra Puma Server",
            "type": "Ruby",
            "request": "launch",
            "cwd": "${workspaceRoot}",
            "useBundler": true,
            "pathToBundler": "/home/<username>/.rvm/rubies/ruby-3.0.0/bin/bundler",
            "pathToRDebugIDE": "/home/<username>/.rvm/gems/ruby-3.0.0/bin/rdebug-ide",
            "program": "/home/<username>/.rvm/gems/ruby-3.0.0/bin/puma",
            "args": [
                "-C",
                "config/puma-local.rb",
            
            ]
        },

```

Full launch.json:  [here](https://gist.github.com/ZeroPivot/3664269c159a9f5e749541f802bc186f) 

Assuming you're using RVM for Ruby, the paths should lie there.

If you're not sure, you can always use something like `whereis bundler`

Ultimately, with using puma and sinatra with bundler in tandem, you also may need a Gemfile file for your sinatra app

***

With all that being said, you should be able to run the debug server and set breakpoints.


![Code_-_Insiders_2021-01-23_12-31-44.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611433920470/l_UlwaxV4.png)

You can run it by going to the debug window and clicking the little green arrow, then a breakpoint  menu appears near the code, where you can go to the next breakpoint or close the server altogether. 

If you need any help, please let me know. These notes are mostly for me referencing things in the future, since there isn't a lot of help on the internet when it comes to these ideas.

Example Gemfile:

```
# frozen_string_literal: true

source 'http://rubygems.org'
gem "ruby-debug-ide"
gem "debase"
gem 'aasm'
gem 'andand'
gem 'cloudinary', git: 'https://github.com/cloudinary/cloudinary_gem'
gem 'free-image'
gem 'mechanize'
gem 'mongo'
gem 'puma'
gem 'rack-ssl', git: 'https://github.com/josh/rack-ssl'
gem 'rails'
gem 'rerun', git: 'https://github.com/alexch/rerun'
gem 'rmagick'
gem 'roda', git: 'https://github.com/jeremyevans/roda' # alternative to sinatra; look into
gem 'ruby-vips'
gem 'sequel' # database that has the same author as roda
gem 'shotgun'
gem 'sinatra'
gem 'sinatra-contrib'
gem 'statemachine'
gem 'time_difference', git: 'https://github.com/ZeroPivot/time_difference' # time difference algorithm (https://github.com/tmlee/time_difference)
gem 'twitter'
gem 'tzinfo'
gem 'webrick'
```
The way the server is configured in this case, bundler is automatically initialized.