# My Windows development environment

This page contains mostly notes on how my Windows development environment is setup.

## Tools

The following list shows the tools I use most for development, explanations are not really necessary:

- Visual Studio
- GVim
- Git (Git Bash and Tortoise Git)
- WebStorm (mostly for frontend development)
- SQL Server Developer edition

Some other tool I use regularly are:

- Remote Desktop Connection Manager
- Putty

## Visual Studio

Within Visual Studio I use the following plugins:

- EditorConfig (not needed in VS2017)
- VsVim
- Microsoft CodeLens Code Health Indicator
- Productivity Power Tools
- Refactoring Essentials
- Trevor
- I hate #regions
- GitDiffMargin

## Vim and config in Git

In order to have the same configuration of Vim on several machines, I store my configuration on [GitHub](https://github.com/dnperfors/vimrc/). To be able to use the config in Windows on my work laptop, I need to change the location of my home directory. Otherwise my home directory will be a network drive when I am logged in at work, and to a local directory (c:\users\\\<username>) when I use the laptop outside the corparate network. In order to achive this, I will do the following:

- Create a custom home folder where the config can be stored (I use c:\home)
- Add a new environment variable, called 'HOME' and give it the value of the directory just created (c:\home)
- Checkout the vimrc repository to c:\home\vimfiles

After this VIM will use the correct configuration. Note that Git Bash will also use this directory as it's home directory.
