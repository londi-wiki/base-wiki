---
weight: 999
title: "Tmux"
description: ""
icon: "article"
date: "2024-01-04T11:24:37+01:00"
lastmod: "2024-01-04T11:24:37+01:00"
draft: false
toc: true
---

# tmux — terminal multiplexer

> man page:  tmux is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a
single screen.  tmux may be detached from a screen and continue running in the background, then later reat‐
tached.

The following commands are the most useful commands (at least for me). If something is missing, send a feedback :-). 

## Commands

### tmux commands

| Command                  | Description                                 |
|--------------------------|---------------------------------------------|
| tmux                     | Simply create a new session                 |
| tmux ls                  | List existing sessions                      |
| tmux a                   | Attach to most recent session               |
| tmux new -s bob          | Create and attach to new session called bob |
| tmux a -t bob            | Attach to session bob                       |
| tmux kill-session        | Kill most recent session                    |      
| tmux kill-session -t bob | Kill session called bob                     |      
| tmux kill-server         | Kill all tmux sessions                      |      


### tmux session commands

"C" stands for Ctrl.

Remember to press first "Ctrl + B" then release these key and press immediately the next key e.g. D (for detaching).

| Command            | Description                                       |
|--------------------|---------------------------------------------------|
| C-B + D            | Detach from session                               |
| C-B + "            | Split the current pane into two, top and bottom.  |
| C-B + %            | Split the current pane into two, left and right.  |
| C-B + Arrow Keys   | Navigate through the panes.                       |
| C-B + Q            | Show pane index                                   |
| C-B + Q INDEX      | Switch to specific pane index                     |
| C-B + C Arrow Keys | Resize selected pane                              |
| C-B + Alt 1..5     | Resize all panes in a preconfigured layout        |
| C-B + C            | Create a new window                               |
| C-B + N            | Move sequentially through the windows             |
| C-B + ,            | Rename window                                     |
| C-B + W            | Open commander                                    |
| C-B + x            | Kill the selected pane                            |
| C-B + &            | Kill the selected window                          |
| C-B + [            | Enter copy mode to copy text or view the history. |
| C-B + C-SPACE      | Start copy selection                              |
| C-B + C-ENTER      | End copy selection                                |
| C-B + ]            | Paste the most recently copied buffer of text.    |

### tmux settings

```bash
# ~/.tmux.conf

# activate mouse
set -g mouse on

# enable vi commands
setw -g mode-keys vi
```