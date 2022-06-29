# Introduction
This document is intended to detail what I've learned in the process of contributing code to iSH.  It is not meant to be a guide to coding style.  The only goal is to detail the process of creating a clean Pull Request (PR) that can be submitted for consideration by the lead developers.

The bulk of this document came from a discussion on the iSH #dev forum where @saagarjha walked me through the process, which was a huge help.  I never would have figured this stuff out on my own.

This document assumes that you have a fork of iSH hosted on GitHub

## What you want at the end

At the end of this process you should have a published PR with exactly one commit.  The PR should apply cleanly to the current iSH master branch and should include only the bare minimum number of files needed.  In particular it should NOT include files such as...

```
.gitignore
app/FileProvider/iSHFileProvider.entitlements
app/iSH.entitlements
app/iSH.xcconfig                                       # More on avoiding this one below
iSH.xcodeproj/project.pbxproj
```

## Cloning and preparation

First of all, you will need a valid paid or free Apple developer account.  

Next you will need to follow the instructions on the main iSH page (https://github.com/ish-app/ish), specifically the 'Hacking' section.

If you do not already have a .gitignore file in your home directory I recommend the following.  You'll need to be in the Terminal program. 

```
user@my-mac ~> curl  https://raw.githubusercontent.com/github/gitignore/main/Global/macOS.gitignore > ~/.gitignore # Get a reasonable set of defaults
user@my-mac ~> git config --global core.excludesFile '~/.gitignore'                                                # Make sure git actually pays attention

```
Now clone the iSH repository.  If you don't have a preference then I'd recommend putting it in ~/git.

```
user@my-mac ~> git clone https://github.com/ish-app/ish.git
user@my-mac ~> cd ish
user@my-mac ~> git submodule update --init deps/libapps
user@my-mac ~> git remote set-url upstream https://github.com/ish-app/ish.git
```

You should now have a working copy of the iSH repo.  You'll need to make some modifications to get Xcode to work cleanly with git.

Make sure you edit 

```
app/iSH.xcconfig
```

to reflect your own Developers ID and bundle identifier.  Then run the following command so that git will ignore future changes...

```
user@my-mac ~> git update-index --assume-unchanged app/iSH.xcconfig           # Make git ignore this file
```

## Creating your PR
First of all, you should never alter your master branch.  It should always track the upstream/mainline iSH master branch.  I recommend creating an alternate branch if you want to make your own changes.  For instance...

user@my-mac ~> git branch myiSH

You would of course have to switch into that branch when you wanted to make changes.  You would do this by issuing the following command.

```
user@my-mac ~> git switch myiSH
```

### The PR
Once you are confident that your change does what you want create a clean new branch off of your master branch.  In theory this should match the upstream Master, but we'll make sure this isn't an issue below.

```
user@my-mac ~> git switch master
user@my-mac ~> git checkout -b my_proposed_pr   # The branch should be named something descriptive like 'add_proc_cpuinfo'
user@my-mac ~> git fetch upstream               # Keep things up to date
user@my-mac ~> git reset --hard upstream/master # Make really sure that we are in sync with the upstream master
```

Now incorporate your changes into this new branch, verify they work and then do the following...

```
user@my-mac ~> git commit -a                                    # Log a meaningful message
user@my-mac ~> git push --set-upstream origin my_proposed_pr    # Push to your GitHub repo
```

Assuming your are logged in, if you go to the main GitHub iSH page you should see an option near the top of the page to submit a PR based on your newly pushed branch.  Click that and follow the instructions.

As mentioned at the start, be sure that only one commit appears in your Pull request and that only the files that are needed by your change are included.

Do not delete your PR branch yet. 

### Dealing with requests for modifications
If changes are requested you will make them in your local branch and issue the following commands

```
user@my-mac ~> git switch my_proposed_pr
user@my-mac ~> # Make modifications, test
user@my-mac ~> git commit --amend
user@my-mac ~> git push
```

This will automatically update the PR request, no further action is required, though you may need to iterate depending on the feedback you get.
