---
layout: post
title: "A Quick Guide to Aliasing Terminal Commands"
date: 2015-05-19 02:34:25 +0800
---
This guide will probably only be useful to you if you find yourself using the **Terminal** a lot whether on Linux/OS X. Here, I'll be talking about aliases and how you could use them in your daily work to maximize your productivity and, to an extent, maintain your sanity while working with a mountain of commands.

## What is Aliasing?
Aliasing a command is rather self explanatory - it's the act of defining a nickname or alias to a certain set of commands via the Terminal. For instance, take a look at the following command I've been using frequently these past few days:

```
g++ -std=c++11 *.cpp -o output
```

As someone who started compiling C++ with `make` and only recently moved on to `g++` to handle multiple files, the additional `std=c++11` parameter was simply too tedious for me to type every time I wanted to compile a project on a new Terminal window. Call me lazy, but I've been spoiled with the likes of `javac`, `ruby` and `python` for a couple of years now, and would like to have a similarly short compile command for C++. Luckily, a Terminal command actually exists to cure my predicament:

```
alias g++11="g++ -std=c++11"
```

The `alias` command is pretty straightforward - it aliases the text `g++ -std=c++11` into an alias `g++11`. From now on, as long as I remain in the same Terminal window, I can compile files in C++ with the following command:

```
g++11 *.cpp -o output
```

It's important to know that these `alias` commands will only remain in effect while the terminal windows they've been typed in remain open. This probably wouldn't bother you if you don't plan on using the defined aliases beyond the timeline of a short project - if you find yourself needing to use multiple commands on a daily basis, however, you'll be glad to know there's a way to permanently retain these aliases.

## For Linux
To make aliases permanent in Linux or any of its distros, just append the `alias` commands to the end of your `.bashrc` file. To do this, open a Terminal window, type `nano ~/.bashrc` and append your `alias` commands to the end of the file. You can add multiple aliases, though you'd probably want to leave comments for each of them to avoid getting them mixed up.

```
~/.bashrc
# This is a comment, by the way. You can use it to label your aliases.
...

# This alias is for compiling C++ files.
alias g++11="g++ -std=c++11"
```

When you're done, save the file using `Ctrl+X`, `Y`, and `Enter`. Restart your Terminal or your machine, and you'll find that `g++11` or whatever aliases you've declared are now permanently recognized by the system. To remove an alias, open the `.bashrc` file again and delete any alias entries you no longer want to keep.

## For OS X
The procedure retain aliases in OS X is similar to that of Linux; however, the `alias` commands need to be entered in the `.bash_profile` file instead ` .bashrc`. To do this, open terminal and type `nano ~/.bash_profile` and append your `alias` commands to the end of the file. Like Linux, you can add comments as well as multiple aliases to the `.bash_profile` file.

```
~/.bash_profile
...
# The process is exactly the same!
alias g++11="g++ -std=c++11"
```

When you're done, save the file using `Ctrl+X`, `Y`, and `Return`. Afterwards, restart your Terminal or machine, and you're done! The removal process is also the same as that of Linux. As a final note, be careful not to alias your commands with the names of existing commands.

Thanks for reading my guide!