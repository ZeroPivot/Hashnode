## Update: Notes On How to use WSL-remote with WSL2, and Ruby 3.0.0

 [Previous Notes Were Here](https://zeropivot.xyz/notes-on-a-ruby-30-development-environment-for-vscode-linterintellisense-on-windows-10) 



I discovered a way of using VScode "natively" with WSL, in the sense that everything is done in WSL and VScode does that while working with windows.

With VScode installed, search for the  ["Remote - WSL"](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) , and install that.

Hit `Ctrl+Shift+P` and search for remote, you can create a new WSL remote session based on the distribution, like, ubuntu, etc.

Upon getting that setup, and you're up and running with WSL-remote, there are more things to do to get ruby up and running.

You use `Ctrl+Shift+P` whenever you want to interact with WSL-remote

In the bash console for WSL-remote, install Ruby with RVM:

Install a couple rubygems, assuming you have  [RVM installed alongside ruby](https://zeropivot.xyz/setting-up-ruby-300-on-windows-10-or-wsl2-ubuntu-updated) 

Always done in new Ruby installations; updates system gems: 
`gem update --system`
Formats code on save:
`gem install rufo`

This also installs Rubocop
`gem install solargraph` 

`rubocop -A` in any given directory will lint/format your code.

For extensions to install on VScode... When running in WSL-remote, you can choose

![Code_2021-01-23_03-50-00.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1611402629479/pBD8P2lHM.png)

Be sure to install these extensions into your WSL remote distro in question:

VSCode Ruby](https://marketplace.visualstudio.com/items?itemName=wingrunr21.vscode-ruby) 
 [WSL - Remote](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)  (Work natively with WSL1/2)
 [Ruby Solargraph](https://marketplace.visualstudio.com/items?itemName=castwide.solargraph)  (intellisense)
 [rufo (Ruby formatter)](https://marketplace.visualstudio.com/items?itemName=mbessey.vscode-rufo) 

Restart VScode if you haven't already, and you should have a development environment for Ruby and WSL2

Also, remember: When working inside WSL, like in /home/aritywolf, you get a speed boost and file monitoring if and only if you work IN WSL, not say, /mnt/c -- a real gotcha for me.