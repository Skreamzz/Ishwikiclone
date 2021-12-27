# Introduction
This document is intended to detail what I've learned in the process of contributing code to iSH.  It is not meant to be a guide to coding style.  The only goal is to detail the process of creating a clean Pull Request (PR) that can be submitted for consideration by the lead developers.

The bulk of this document came from a discussion on the iSH #dev forum where @saagarjha walked me through the process which was a huge help.  I honestly never would have figured this stuff out on my own.

## What you want at the end

At the end of this process you should have a published PR with exactly one commit.  The PR should apply cleanly to the current iSH master branch and should include only the bare minimum number of files needed.  In particular it should NOT include files such as...

```
.gitignore
app/FileProvider/iSHFileProvider.entitlements
app/iSH.entitlements
app/iSH.xcconfig
iSH.xcodeproj/project.pbxproj
```

## Cloning and preparation

First of all, you will need a valid paid or free Apple developer account.  

Next you will need to follow the instructions on the main iSH page (https://github.com/ish-app/ish), specifically the 'Hacking' section.

If you do not already have a .gitignore file in you home directory I recommend doing the following in your home directory.  You'll need to be in the Terminal program. 

```
user@my-mac ~> curl  https://raw.githubusercontent.com/github/gitignore/main/Global/macOS.gitignore > .gitignore # Get a reasonable set of defaults
user@my-mac ~> git config --global core.excludesFile '~/.gitignore                                              # Make sure git actually pays attention`

```
Now you can clone the iSH repository.  If you don't have a preference then I'd recommend ~/git.

```
user@my-mac ~> git clone https://github.com/ish-app/ish.git
user@my-mac ~> cd ish
user@my-mac ~> git submodule update --init deps/libapps
```

You should now have a working copy of the iSH repo.





