---
layout: post
title: Silent YAML failures
date: 2026-09-27 21:40:00 +0530
description: An unquoted colon in front matter makes a page vanish with no error at all.
tags: yaml debugging
categories: notes-meta
---

`title: Notes: on YAML` is not valid YAML. The parser reads the second colon as a key separator and gives up, and because the failure happens before the page is registered, the file never becomes a page.

There is no warning. The build succeeds. The file is simply not in the output.

The general rule I keep relearning: quote any front-matter value containing a colon, a hash, or a leading bracket. It costs two characters and removes an entire class of mystery.
