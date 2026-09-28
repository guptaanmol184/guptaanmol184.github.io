---
layout: post
title: Jekyll collections are just folders
date: 2026-09-28 00:15:00 +0530
description: Why a new content type is a folder and three lines of config.
tags: jekyll
categories: notes-meta
---

A Jekyll collection is a directory starting with an underscore plus an entry in `_config.yml`. That is genuinely most of it.

Put markdown files in `_notes/`, declare `notes: output: true`, and every file becomes a page. No registration, no index to update, no menu entry to touch.

The one sharp edge: only `_posts` reads dates out of filenames. A collection document with no `date:` in its front matter silently falls back to the file's _modification time_ — so the day you `touch` a file, it jumps to the top of the list. Write the date explicitly.
