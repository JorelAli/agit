# agit

A simple git wrapper

## Inspiration

This project is heavily inspired by [SiliconSloth's Metro](https://github.com/SiliconSloth/Metro) project, which is a simple version control and file syncing system that is written in C++. The _Metro_ project aims to reduce common pitfalls that occur when using `git`, such as messing up a repository to a state where it is easier to just re-clone the repository from a remote.

![git](https://imgs.xkcd.com/comics/git.png)

## Design choices

Since _agit_ is just a wrapper for git (in the sense that it doesn't do the fancy file synchronization that _Metro_ does), I chose to write it as a shell script for the _Bourne Shell_ (`#!/bin/sh`), as opposed to the _Bourne Again Shell_, for various reasons:

- NixOS does not inherently include the file `/bin/bash` at that location. This is primarily due to how NixOS works (in short, bash on NixOS is actually located at `/run/current-system/sw/bin/bash`). Despite that, NixOS does include `/bin/sh`.
- A shell script is super lightweight. It doesn't require any compilation to be run and can literally be copied from a webpage (you don't even have to download it!)
- It is compatible with all operating systems. Since `sh` is available on MacOS and Linux, it can be run on those operating systems. It is also compatible with Windows by using `git bash`, which isn't really a problem since that's how you'd usually use git on Windows anyway.

## Etymology

_Agit_ was originally named _bGit_, standing for "better git". After working on it, I found it a little awkward to type and wanted a name that was easier to type as it's the sort of thing you'd type frequently. Hence, _agit_.

Also, it sounds funny. "How do I push this branch?" "Just use a git!"

## Upcoming features

[ ] Project branches. A project branch is a special branch that cannot be merged and always begins with no files in it. The idea for this is to simplify project management. This situation is basically ideal for a project that has one section solely for code, one section solely for documentation, one section solely for testing and prototyping, and so on. This is heavily inspired by my frustration to have "repository grouping", which lets you link repositories that are similar in function, but have different codebases. For example, this can be useful for a project that is written multiple times in different languages (e.g. an iOS app and an Android app). _In addition_, this is sort of what GitHub Pages does - it requires a branch called `gh-pages`, but surely you'd want this branch to be separate and non-mergeable? 

[ ] The _agit helper_. The concept is simple: You should never be at a point in time in your repository where you don't know what to do. For example, if a merge conflict has arisen*, you should know how to easily resolve it without having to look it up online. The _agit helper_ is designed to analyze the current state of the repository and inform the user of what should be done next. 

[ ] Emergency saving (`agit save`). Instead of doing the infamous `git add`, `git commit`, `git push` (`git out of the building`) in the event of an emergency, `agit save` will save the current state of the repository by making a temporary commit. This is then automatically pushed to the remote (thus, saving a copy of the code in the remote as well). When the user comes back to their code, they can delete the temporary commit, but still retain the current state of where they were. (Basically, it's a temporary commit that, once resolved, doesn't consume a commit message in the final commit tree).

*That is, assuming _agit_ will have merge conflicts.
