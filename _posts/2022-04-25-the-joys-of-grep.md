---
layout: post
date:   2022-04-25 09:00:00
title: The Joys of Grep
image: IMG_7153.png
image_thumb: IMG_7153_thumb.png
subtitle: The one about the joys of grep
categories: grep unix
---
I had this problem where I needed to match a lot of ids (approx. 10.000) against a data file. It would take too long time to write a program that validated the ids precense. What to do?

The Unix shell to the rescue. I remembered ``` grep ``` have some of the functionality I wanted.

```shell
man grep
```

Gave me that

```shell
grep -f <file>
```

will read the match patterns from a file. Next problem is to get ``` grep ```  to match the pattern on a fixed word.

```shell
grep -f <file> -Fw <match file>
```

This got me some of the way. Only problem remaining is the match result wasn't complete - treating the file as ascii helped.

```shell
grep -f <file> -Fwa <match file> | cut -d \; -f <index> > matches
```

Gave the result I hoped for. All of the matching ids in a file ( ``` matches ``` ) of its own.

Thank you ``` grep ```
