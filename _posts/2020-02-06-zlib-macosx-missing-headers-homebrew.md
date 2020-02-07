---
layout: post
title: Homebrew and Compiling errors with zlib not found for OSX Mojave 10.14
---

Starting in Mojave, the Command Line Tools no longer installed headers needed for compiling C code. The most noticeable problem is when installing applications from source in Homebrew, and a report of no zlib found.

Apple stated they were no longer going to install the headers with the Command Line Tools, but for version 10.x of Xcode, an additional package was provided that would install the headers. Apple made good on its threat with version 11 of Xcode. XCode 11 does not install the headers, nor does it supply the package to add the headers.

If you have not upgraded to Catalina yet due to other problems (no 32-bit support), your XCode may have updated to version 11, which brings with it the header mentioned above problem. The way to fix this if you are still on 10.14 (Mojave) is to delete the command line tools and reinstall them with `xcode-select`

To do so is easy:
```
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install
```
After install go look for the headers installation package which will be in `/Library/Developer/CommandLineTools/Packages/`

Then install the pkg file like so (substitute the correct pkg file):
```
sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
```