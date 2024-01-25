---
weight: 999
title: "Useful git commands"
description: ""
icon: "article"
date: "2024-01-01T19:42:02+01:00"
lastmod: "2024-01-01T19:42:02+01:00"
draft: false
toc: true
---

# Remove file from git

Source: [git-tower](https://www.git-tower.com/learn/git/commands/git-rm)

To remove a file both from the Git repository and the filesystem, you can use git rm without any parameters (except for the file's name, of course):

```bash
git rm file1.txt
```

If you only want to remove the file from the repository, but keep it on the filesystem, you can add the --cached flag:

```bash
git rm file2.txt --cached
```

When trying to delete multiple files in a directory or via a glob pattern, you might want to perform a "dry-run" first and see which files would be removed:

```bash
git rm css/* --dry-run
rm 'css/about.css'
rm 'css/general.css'
```