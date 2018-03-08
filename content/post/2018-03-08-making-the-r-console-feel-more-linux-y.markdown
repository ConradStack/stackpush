---
title: Making the R console feel more linux-y
author: Conrad
date: '2018-03-08'
slug: making-the-r-console-feel-more-linux-y
categories:
  - R
tags: []
---

When I am working in R interactively, through the console, I often find myself trying to run the common linux shell commands: `pwd` and `ls` (instead of `getwd()` and `list.files()`, respectively).  

While reading a [nice explanation of active binding in R from Colin Fay](http://colinfay.me/ractivebinfing/), I realized that active binding provides a way to bring the `pwd` and `ls` commands to the R console:


```r
# pwd - print present working directory
makeActiveBinding(sym = "pwd", 
	fun = function(value){
		getwd()
	}, 
	env = .GlobalEnv
)

# ls - list files
makeActiveBinding(sym = "ls", 
	fun = function(value){
		list.files(all.files=T)
	}, 
	env = .GlobalEnv
)
```

There are a couple of important caveats to the above code:

- Binding `ls` does not break calls to `ls()`, but it obviously will break the default behavior of typing `ls`, which would return to the function definition
- `ls` cannot be called using any additional arguments that you might use on your linux shell (e.g., `ls -laht`).  This greatly lessens the usefulness of the implementation above.  

It is tempting to explore this kind of R console customization further, but I imagine it will be more worthwhile to learn to use Rstudio's built-in Terminal.





