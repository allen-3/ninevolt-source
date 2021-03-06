---
title: "Setting up shortcuts for (slightly) better typography on Windows"
date: 2021-07-12T15:51:56-04:00
draft: true
slug: windows-symbol-shortcuts
description: "Curly quotes, ellipses, and dashes can be produced using simple shortcuts on MacOS. You can use an AutoHotkey script to make these important typographic symbols accessible on Windows."
---

## Motivation

The modern keyboard layout shares a considerable amount of <span class="abbr">DNA</span> with the typewriter, whose physical constraints created limitations on the number of keys that could be included on the machine. The keyboards of today are still missing keys for symbols that show up all the time in writing.

<aside>This leads to an interesting way to guess at what operating system someone is using. If you see straight quotes in, say, a YouTube comment, chances are that person typed it from a <span class="abbr">PC</span> or Android device.</aside>

- Quotation marks and apostrophes should be curly, resembling the numbers 6 and 9. On Windows, the quote key <kbd>'</kbd> most often produces a straight, vertical quote instead.

- The ellipsis, or “dot-dot-dot” symbol, is correctly set using a single character which spaces each dot an optimal distance from the rest. Usually, we just type three periods instead.

- The typographic error that is probably most closely tied to English grammar is an improper substitution of en dashes (–) and em dashes (—) with a hyphen character (-).

Half of the problem is that people aren’t aware of the difference between the approximations we type and the correct counterparts. The other half is that there’s no easy way to type curly quotes, ellipses, en dashes, and em dashes in Windows. Some word processors, like Microsoft Word, automatically replace the approximations we type with their correct counterparts, but most often what Windows users type is left unchanged.

MacOS was designed with ??publishing and graphic design?? in mind, and has built-in shortcuts on the Option layer that allows for inputting a suite of special characters, including the ones just mentioned. We can steal this idea and use AutoHotkey to easily type these symbols by combining <kbd>Alt</kbd> with another key.

## The AutoHotkey script

If you know how AutoHotkey works, you can copy the full script below into a new `.ahk` file. The rest of this post explains how AutoHotkey works for the uninitiated, compares my chosen shortcuts with the respective MacOS macros, and hopefully provides some insight that can help you edit and augment this script to your liking.

## Curly quotes

In any professionally typeset text, quotation marks and apostrophes are curly, resembling 6s and 9s. Yet, on Windows, the quote key <kbd>'</kbd> almost always produces a straight, vertical quote. Apple devices have a feature called _smart quotes_ enabled by default, which automatically inserts proper curly quotes depending on context. This leads to inconsistency between user messages in threads, tweets, and YouTube comments sent between people on different operating systems. The best solution would be if smart quote algorithms were available for everybody, but this probably won’t happen for the forseeable future.

On MacOS, an opening double quote is entered using <kbd>⌥ Option</kbd>+<kbd>[</kbd> and a closing double quote with <kbd>⌥ Option</kbd>+<kbd>Shift</kbd>+<kbd>[</kbd>. While you could simulate this on Windows with a shortcut that simply replaces Option with Alt, I think this choice of key combination is confusing and unwieldy. It’s difficult to remember both that a double quote uses the left bracket _and_ that the closing one requires the Shift key.

Instead, I suggest tweaking these shortcuts to be more intuitive, as follows:

| | Item | Shortcut |
:-:|:--|:--
| <span class="big-table-symbol">‘</span> | opening single quote | <kbd>Alt</kbd>+<kbd>[</kbd> |
| <span class="big-table-symbol">’</span> | closing single quote, apostrophe | <kbd>Alt</kbd>+<kbd>]</kbd> |
| <span class="big-table-symbol">“</span> | opening double quote | <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>[</kbd> |
| <span class="big-table-symbol">”</span> | closing double quote | <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>]</kbd> |

[Example of tweet]. Caption: What a great tweet. And, it was probably written on a <span class="abbr">PC</span>.

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

## Why does this matter?

Although the difference between straight and curly quotes might seem inconsequential, our minds are used to processing the curly version from the thousands of times we encounter them in professionally typeset texts (novels, textbooks, advertisements, articles, etc.)

Remember, the point of typography is to serve the reader — if that makes things a bit harder for the writer, so be it ([Practical Typography: _Who is Typography For?_](https://practicaltypography.com/who-is-typography-for.html)).

## Further reading

Matthew Butterick’s online book _Practical Typography_ covers the topics of [curly quotes](https://practicaltypography.com/straight-and-curly-quotes.html), [ellipses](https://practicaltypography.com/ellipses.html), and [dashes](https://practicaltypography.com/hyphens-and-dashes.html) concisely. The entire book is worth a read (and a purchase) — it taught me tons about typography and inspired many of the design decisions on this website.
