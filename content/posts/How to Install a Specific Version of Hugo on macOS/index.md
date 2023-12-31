---
title: "How to Install a Specific Version of Hugo on macOS"
date: 2023-11-02
draft: false
description: "How to Install a Specific Version of Hugo on macOS"
slug: "install specific hugo version"
tags: ["tutorial", "hugo", "blog"]
categories: ["Tech"]
---
To demo how to build a blog for beginners, I created a new user on my macOS and reinstalled Hugo in the new environment. However, the latest Hugo version, 0.120.3, unfortunately has some compatibility issues with the installed Blowfish module. For example, certain configuration parameters such as `showDate`, `showView`, `showLikes` cannot be rendered correctly on my site. 

While this issue may be resolved in future version updates, I would like to **revert to my previous Hugo version**, 0.119.0, for the time being. `brew install hugo@0.119.0` was my initial thought, but it didn't work as expected. After some research, I found that [Manuel Martinez's method](https://datacenterjourney.com/2021/install-specific-version-hugo-macos/) worked best for me. Below are the exact procedures with a few adjustments.
## Procedures
### 1.  Download a Specific Hugo Version
- Visit [Hugo releases on GitHub](https://github.com/gohugoio/hugo/releases) and search for the version that you want to install
- Click on the specific version number link and scroll down to the `Assets` section
- Choose the package that matches your operating system. The one I downloaded is `hugo_extended_0.119.0_darwin-universal.tar.gz`
- Verify the package's contents before extracting it using the command:
``` 
tar tvf ~/Downloads/hugo_extended_0.119.0_darwin-universal.tar.gz
```
### 2. Edit the Shell Profile
- Run `echo $PATH` to see the order of directories in your `PATH`. By default, you may see the result starts with `/opt/homebrew/bin/hugo`
- Run the following command to determine whether your default shell is bash or zsh
```
echo $SHELL
```
- Depending on the type of the shell, edit the profile using one of the commands below
```
nano ~/.bash_profile
#or
nano ~/.zprofile
```
- Add `export PATH="$HOME/bin:$PATH"` to the beginning of the file 
- Press `Ctrl + O` to save the changes and exit by pressing `Ctrl + X`
- Run one of the following commands to apply the changes to the current session
```
source ~/.bash_profile
#or
source ~/.zprofile
```
### 3. Install Hugo in the Local Bin Directory
- Check whether you already have a bin directory in the home directory; if not, create one
```
ls ~/bin
#or
mkdir ~/bin
```
- Move to the bin directory and extract the tarball
```
cd ~/bin
tar -xvzf ~/Downloads/hugo_extended_0.119.0_darwin-universal.tar.gz
```
### 4. Verify the Installation
- Run `which hugo` to confirm Hugo is in the local bin directory
- Re-run `echo $PATH`. It should now begin with the path `/Users/<your-user-name>/bin`
- Run `hugo version` to display the Hugo version your system is using
## Reference
- [Install Specific Version Hugo MacOS](https://datacenterjourney.com/2021/install-specific-version-hugo-macos/)

