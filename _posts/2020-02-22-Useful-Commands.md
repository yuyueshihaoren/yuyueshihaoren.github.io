---
layout: post
title:  "Useful Commands"
date:   2020-02-22
categories: [notes]
comment: true
---

- Use ffmpeg and parallel to convert media types
	- eg. Convert all flac audio files to mp3 files
```sh
ls *.flac | parallel ffmpeg -loglevel panic -i {} {/.}.mp3
```
