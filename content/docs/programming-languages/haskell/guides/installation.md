---
title : 'Installation'
date : 2023-09-06T23:37:53+02:00
tags: ["howto"]
author: "Leon"
---

### Installation of GHCI [^1]

[ghcup website](https://www.haskell.org/ghcup/)

Before installing ghci, install the following requirements:

`sudo apt install build-essential curl libffi-dev libffi8ubuntu1 libgmp-dev libgmp10 libncurses-dev libncurses5 libtinfo5`

`sudo apt install libghc-zlib-dev libghc-zlib-bindings-dev`

Simple execute the following command in a linux or wsl 2 terminal.

`curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh`

Note during installation
> ghcup installs only into the following directory,
which can be removed anytime:
/home/leon/.ghcup

### After Installation

To start a simple repl, run:
`ghci`

To start a new haskell project in the current directory, run:
`cabal init --interactive`

To install other GHC versions and tools, run:
`ghcup tui`

If you are new to Haskell, check out [haskell.org/ghcup/steps](https://www.haskell.org/ghcup/steps/)
 
[^1]: Glasgow Haskell Compiler