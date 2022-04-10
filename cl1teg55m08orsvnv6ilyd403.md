## Creating a Ruby (3.0+) development environment with VScode

Ruby is a fun and elegant programming language! 

Even moreso when you have more "*things*" to accompany it, such as a linter and debugger. Both of which works directly in VScode when setup correctly. 

The debugger is integrated with VScode and you should be able to direct the debugger towards a certain ruby file, after clicking on the debug icon at the upper left hand side of VScode

The linter in question will also show you API documentation, but is full-functioning as any other is.

The debugger works with line breaks without any issue, but still, once again, has to be setup correctly

Ordinarily, it's pretty easy to get Ruby working, given that you use something like the Ruby Version Manager (RVM), but I will go step by step and outline all the possibilities.

First off, the easiest thing to do is to download [VScode](https://code.visualstudio.com/), and install it.

If you are using windows, enable the Windows Subsystem For Linux (WSL2).

On Windows 11, it is a download from the store.

Windows 10 (or 11): `Control Panel > Add/Remove Programs > Turn Windows features on or off` -> `Check in 'Windows Subsystem for Linux'` -> `OK > reboot`

("Windows Subsystem ... ") in the windows store if you want to install through the store)

Install Ubuntu for WSL2: In the store. Say, v20.04

You can access Ubuntu by searching for it in the search menu, running the `wsl` or `ubuntu` command in the command prompt or powershell.

The same things apply in setting up ubuntu, including `sudo apt update && sudo apt upgrade

What I am getting at is you can program almost freely in Ruby in windows as if you were on desktop GNU/Linux.

I have had problems getting local server hosting to work, but that is about it.

Now we go for installing RVM (ruby version manager)

1) Install [RVM](https://rvm.io/) - (their instructions in link)
2) `source /.../rvm` -- the file rvm tells you to at the end of its installation
3) `rvm install 3.0` -- installs ruby 3.0, accessible as `ruby`

Run the general thing to get Ruby up to speed:
1) `gem update --system && gem update`

Remember one thing: VScode seems to make workflow as same-y as possible no matter what platform you are using, so you can setup all of this via Remote-SSL as well, but this assumes you are either using WSL2/Ubuntu or some GNU/Linux distribution that can run RVM.

Now, we need the extensions for VScode

(At the end of the article I will provide a Gemfile containing all the extensions I work with)

In no specific order, when searching for extensions:

1) `Settings Sync`: allows you to save what extensions you have on your VScode box (upload [update]/download [restore)


Linter set:
* "`Rubocop Quick Fix`" (allows you to disable rubocop warnings)

* "`ruby-rubocop`" (gem: `rubocop`)

* "`Ruby Solargraph`" (linter) (gem: `solargraph`)


"`Ruby`"

"`Ruby extension pack`"

"`Ruby language Colorization`"

"`ruby-symbols`"

"`TODO Highlight`"

"`VSCode Ruby`"

Setting up a development environment

There is a gemfile at the end, but the only two extensions you have to install are: `rubocop` and `solargraph`

With rubocop, you may have to go to settings.json and add the lines:

```
"ruby.rubocop.useBundler": true,
"ruby.rubocop.executePath": "/home/aritywolf/.rvm/gems/ruby-3.0.0/bin/",
"ruby.rubocop.suppressRubocopWarnings": true,
```
For `"ruby.rubocop.executePath"`, set it to the location or rubocop (`whereis rubocop`)

Provided is `.rubocop.yml` for use in the root folder of your Ruby project: [.rubocop.yml](https://gist.github.com/ZeroPivot/15b03e03d45d5a33e51ae764cb52fb8a)

Then, in the root directory of your project, `solargraph config .`, which should get the linter going.

If you have any questions or want to address anything I missed, please do contact me:

My telegram is [@ArityWolf](https://t.me/aritywolf)

And my hashnode is @ZeroPivot

**Note: Hitting F1 will allow you to choose Remote-WSL, and this is what is used with WSL2
You can also access Remote-SSH, and all of the same steps apply!**




