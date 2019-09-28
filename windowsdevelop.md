# My Windows development environment

This page contains mostly notes on how my Windows development environment is setup.

## Tools

The following list shows the tools I use most for development, explanations are not really necessary:

- Visual Studio
- Git (Git Bash)
- Visual Studio Code (mostly for frontend development)

Some other tool I use regularly are:

- Putty
- VirtualBox
- WSL

## Visual Studio

Within Visual Studio I use the following plugins:

- Productivity Power Tools (Actually, I am not using everything so specify the once I use...)
- RegionExpander
- SonarLint

## Vim and config in Git

*This is no longer necessary, since the company made some changes. Besides that, it did seem to break certain applications...*

In order to have the same configuration of Vim on several machines, I store my configuration on [GitHub](https://github.com/dnperfors/vimrc/). To be able to use the config in Windows on my work laptop, I need to change the location of my home directory. Otherwise my home directory will be a network drive when I am logged in at work, and to a local directory (c:\users\\\<username>) when I use the laptop outside the corparate network. In order to achive this, I will do the following:

- Create a custom home folder where the config can be stored (I use c:\home)
- Add a new environment variable, called 'HOME' and give it the value of the directory just created (c:\home)
- Checkout the vimrc repository to c:\home\vimfiles

After this VIM will use the correct configuration. Note that Git Bash will also use this directory as it's home directory.
