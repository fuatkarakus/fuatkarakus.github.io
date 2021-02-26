---
layout: post
title: Multiple JDK install on macOS
subtitle: 
tags: [JDK]
comments: true
---

This is a post to show how to install and manage multiple java versions on macos.

**Before start we need brew**

Install JDK 8 and 11 together with brew cask.

```
brew install --cask AdoptOpenJDK/openjdk/adoptopenjdk{8,11}
```

Then edit .zshrc file add following lines.

```
export JAVA_8_HOME=$(/usr/libexec/java_home -v1.8)
export JAVA_11_HOME=$(/usr/libexec/java_home -v11)

export JAVA_HOME=$JAVA_8_HOME

export PATH=$PATH:$JAVA_HOME/bin
```