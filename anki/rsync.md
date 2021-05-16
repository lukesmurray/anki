---
title: "Rsync"
date: "2021-01-05T13:58:01"
description: "Anki deck for Rsync cards."
draft: true
# image: /path/to/image
css: custom-styles.css
---

# Rsync

## What does the a flag do in rsync?

The `a` flag stands for archive which means it will sync recursively, preserve permissions, times, group, owner, and resolve sym links.

These are usually what you want when you are syncing from one file system to another so try to use the `a` flag unless you specifically choose not to.

## What does the z flag do in rsync?

The `z` flag enables compression

## What does the P flag do in rsync?

The `P` flag enables `--partial` or resuming of aborted syncs and `--progress` which shows progress during the sync.

## How do you sync two directories in rsync?

`rsync -a source/ target`

The `/` after source says place the contents of source in the target directory.
Without the `/` rsync would place the `source` directory in the `target` directory.

The `a` flag is used to perform recursive syncing which is necessary for directory syncing.

## How do you specify a remote source or target in rsync?

Using the syntax `username@remote_host:path_to_directory`.

If you have set a `Host` to a `hostname` in your ssh config you can use `hostname:path_to_directory`