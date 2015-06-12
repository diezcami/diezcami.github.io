---
layout: post
title: "Setting up Go on your OS X Machine"
date: 2015-06-12 23:00:10 +0800
--- 
Go is easily one of my favorite proramming languages due to its features and performance for web based projects. Installing it is relatively simple and should take about 5-10 minutes tops.

## Installing Go
I used [Homebrew](http://brew.sh) to install Go. If you haven't heard of it, it's a package manager for OS X similar to the built-in `apt-get` of Linux. To install Homebrew, paste this at a Terminal prompt:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

If you already have Homebrew in your system, paste this to install Go:

```
brew install go
```
At this point, you should be able to write and compile Go files with `go run`, as well as check your environment variables with `go env`.

## Handling Imports
`$GOPATH` is not set by default, which poses a problem when installing custom packages with `go get`. To set the path permanently for succeeding Terminal sessions, type `nano ~/.bash_profile` onto your Terminal prompt, and paste the following:

```
export GOPATH=$HOME 
export PATH=$PATH:$GOPATH/bin
```

Save the file with `Ctrl+X`, `Y` and `Enter`. After restarting Terminal (no need to reboot your machine), you should be able to import custom packages with no compile errors.