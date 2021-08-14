---
title: "Setting up shortcuts for (slightly) better typography on Windows"
date: 2021-07-12T15:51:56-04:00
draft: true
description: "Curly quotes, ellipses, and dashes can be produced using simple shortcuts on MacOS. You can use a simple AutoHotkey script to make these important typographic symbols available on Windows."
---

The modern keyboard layout shows many remnants of the time of the typewriter, when physical constraints imposed limitations of the number of keys that could be included on the device.

## Curly quotes

In any professionally typeset text, quotation marks and apostrophes are curly, resembling 6s and 9s. Yet, if you are on a Windows computer, typing out a <kbd>'</kbd> will almost always produce a vertical quote. Although the difference might seem inconsequential, our minds are used to processing the curly version. Moreover, Apple devices have a feature called _smart quotes_ enabled by default, which automatically inserts proper curly quotes depending on context. This leads to inconsistency between user comments in threads, messages sent between people on different operating systems, etc. The best solution would be if smart quote algorithms were available for everybody, but this won’t happen in the forseeable future.

The best Windows users can do is insert curly quotes manually. Luckily, this is a fairly simple endeavour with a simple AutoHotkey script and some rewiring of muscle memory.

[Margin note] This leads to an interesting way to guess what operating system someone uses. If you see straight quotes in, say, a YouTube comment, chances are that person typed it from a PC or Android device.

[Example of tweet]. Caption: What a great tweet. And, it was probably written on a PC.

Note: Modern word processors, including Microsoft Word, have a feature called _smart quotes_ enabled (by default?). This causes quotation marks and apostrophes to “intelligently” render as the proper curly symbols. This feature mostly works fine; you don’t have to worry about using a curly quote shortcut when typing in Word.

## Set up AutoHotkey

```ahk
#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
; #Warn  ; Enable warnings to assist with detecting common errors.
SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

; Alt + [   ->   Opening single quote
![::
    Send, ‘
return

; Alt + ]   ->   Closing single quote
!]::
    Send, ’
return

; Alt + Shift + [   ->   Opening double quote
!+[::
    Send, “
return

; Alt + Shift + ]   ->   Closing double quote
!+]::
    Send, ”
return

; Alt + hyphen: en dash
!-::
    Send, –
return

; Alt + Shift + hyphen: em dash
!+-::
    Send, —
return

; Alt + semicolon: ellipsis
!`;::
    Send, …
return
```

Whenever you see a semicolon `;`, the text to the end of the line is a comment.

## Further reading

Matthew Butterick’s online book _Practical Typography_ covers the topics of [curly quotes](https://practicaltypography.com/straight-and-curly-quotes.html), [ellipses](https://practicaltypography.com/ellipses.html), and [dashes](https://practicaltypography.com/hyphens-and-dashes.html) concisely. The entire book is worth a read (and a purchase) — it taught me tons about typography and inspired many of the design decisions on this website.
