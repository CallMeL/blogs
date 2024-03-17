---
title: "Symbolic debugging in Xcode"
slug: "Symbolic-debugging-in-Xcode"
description: Symbolic debugging, LLDB and a little assembly langauge
date: 2024-03-10T22:11:29+01:00
image: cover.jpg
categories:
    - Tech Sharing
comments: true
draft: true
---

## What is Symbolic breakpoints

“Symbolic breakpoints are a great debugging feature of Xcode. They let you set a breakpoint on a certain symbol within your application. An example of a symbol is -[NSObject init], which refers to the init method of NSObject instances.”

Symbolic breakpoint is a solution when we know what cause the issue but don't know where it is.

To debug some issues, you need to pause on a symbol that your source code doesn’t define. For example, when you encounter an Auto Layout issue, the error message recommends setting a breakpoint on UIViewAlertForUnsatisfiableConstraints. To do that, use a symbolic breakpoint. [1]

“In the Symbol part of the popup type: -[NSObject init]. Under Action, select Add Action and then select Debugger Command from the dropdown. Next, enter po [$arg1 class] in the box below.”

“When the breakpoint fires, a command runs in LLDB, and execution of the program continues automatically.”
“ $arg1 is synonymous to the $rdi register and can be loosely thought of as holding the instance of a class when init is called”


## Assembly, Registers and Calling Convention

Cover Photo by <a href="https://unsplash.com/@andreiamza2000?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Amza Andrei</a> on <a href="https://unsplash.com/photos/black-laptop-computer-turned-on-showing-music-player-Bss5nhYnLKU?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
  
[1] [Setting breakpoints to pause your running app ](https://developer.apple.com/documentation/xcode/setting-breakpoints-to-pause-your-running-app
[2] Excerpt From Advanced Apple Debugging