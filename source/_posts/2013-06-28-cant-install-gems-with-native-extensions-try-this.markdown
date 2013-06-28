---
layout: post
title: "Can't install gems with native extensions? Try this"
date: 2013-06-28 15:10
comments: true
categories: 
---
Yesterday, I re-installed my homebrew install because it was corrupted. That led to a huge headache where I couldn't install any gems with native extensions. It took forever for me to find the issue, so I thought I'd write this in the hopes it helps anyone googling around.

My issue was that I'd installed gcc-4.2 using homebrew. Re-installing homebrew broke that install.

##Solution:

First, try ```brew install apple-gcc42```. If you're lucky, it'll work, and you're set.

If not, you need to tap ```homebrew/dupes```. A tap is just homebrew speak for another git repository with extra formulae. Try 
``` bash 
brew tap homebrew/dupes
brew update
brew install apple-gcc42
```

It might fail on the ```brew update``` step. This is a super old bug that's been fixed, but you need to do the following:
``` bash
cd $(brew --repository)
git reset --hard FETCH_HEAD
```

If that doesn't work:

``` bash
cd $(brew --repository)/Library
git clean -fd
```

Now that almost fixed it for me, but when I ran brew update it was complaining about overwritten files in ```homebrew/dupes```. I couldn't find the solution for this anywhere, so I kept poking around and trying different things. Here's what worked:

``` bash
cd $(brew --repository)/Library/Taps/homebrew-dupes
git reset --hard FETCH_HEAD
brew update
brew tap --repair homebrew/dupes
```

And now, you should be able to ```brew install apple-gcc42``` and your native extensions should install. It's worth noting that you *need* gcc-4.2 for the native extensions. Using another version of gcc (4.3 - 4.8) won't work.

Happy hacking!

