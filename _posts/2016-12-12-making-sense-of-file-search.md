---
layout: post
title: search file content in the terminal
excerpt: Making sense of the options for searching the content of files using the terminal
author: daxaar
categories:
  - terminal
  - bash
tags:

draft: true
comments: true
---


find /path/to/dir -type f -print0 | xargs -0 grep -l "foo"
