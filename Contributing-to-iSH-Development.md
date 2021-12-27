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
user@my-mac ~> git remote set-url upstream https://github.com/ish-app/ish.git
```

You should now have a working copy of the iSH repo.

## Creating your PR
First of all, you should never alter your master branch.  It should always track the upstream/mainline iSHE master branch.  I recommend creating an alternate branch if you want to make your own changes.  For instance...

user@my-mac ~> git branch myiSH

You would of course have to switch into that branch when you wanted to make changes.  Rather than get into a detailed conversation on iSH I'll stop there and get to the main point.

### The PR
Once you are confident that your change does what you want create a clean new branch off of your master branch

```
user@my-mac ~> git switch master
user@my-mac ~> git checkout -b my_proposed_pr   # The branch should be named something descriptive like 'add_proc_cpuinfo'
user@my-mac ~> git fetch upstream               # Keep things 
git submodule update --init deps/libapps
git fetch upstream
git reset --hard upstream/master
git cherry-pick 4fa0397613434742f53038219ae0e243b9b23137

git update-index --assume-unchanged app/iSH.xcconfig

# To make changes to a PR

git commit --amend

git switch enhance_stub_syscall_dmesg
git status
git reset --hard 585cf94
vi kernel/calls.c
git commit --amend
git status
git diff
git add kernel/calls.c
git status
git commit --amend
git push
git push --force

git pull --no-ff https://github.com/nimelehin/ish procfs








