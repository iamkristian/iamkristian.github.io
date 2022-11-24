---
layout: post
title:  "Vim registers"
date:   2014-04-29 06:50
image: IMG_7154.png
image_thumb: IMG_7154_thumb.png
subtitle: The one about vim registers
categories: vim
---
So I'm an avid vim user. I just wanted to write this down to remind myself, or
as [Gary Bernhardt](https://twitter.com/garybernhardt) expresses it

> Store it into my muscle memory!

Vim have registers. So when ever you perform an action of ``` cut```, ``` paste ```, ``` copy ```,
the selection is stored in a register.

## Chose your register

You chose a register with ``` "<name of register> ``` and from there you can
do your motion, yank or whatever action you desire.

## List your registers

You can list your register content with

``` :reg ```

### The unnamed register ```""```

This is the default register, and vim will use this if you don't specify a
register.

### The named register ```"a--"z```

Vim has a named register for each of the letters in the alphabet. So you can
``` "ad ```, ``` "ay ```, or paste ``` "ap ```

### The /dev/null register ``` "_ ```

Sometimes you don't want to store the text you manipulate, if you send it to
``` "_ ``` it will not be stored.

### The system clipboard register ``` "+ ```

This will store the text in the default X11 clipboard, pretty handy!

### The selection register ``` "* ```

This will store the text in the X11 selection clipboard, pretty handy! Note this will be the same as the system clipboard on windows or OSX, since there is only one clipboard.


### The expression register ``` "= ```

This register is different, since vim drops into commandline mode, and reads the input from the script you execute.

### And the rest

Here are the rest of the registers:

|Register | Content |
|:---------:|-------|
|``` "# ``` | Alternate file      |
|``` "% ``` | Current file        |
|``` "/ ``` | Last search pattern |
|``` ": ``` | Last Ex command     |
|``` ". ``` | Last inserted text  |


I hope you'll enjoy some more productivity in vim using registers!

