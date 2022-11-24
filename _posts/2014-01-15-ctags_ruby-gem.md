---
layout: post
title:  "ctags_ruby gem"
date:   2014-01-16 09:00:00
image: IMG_6049.png
image_thumb: IMG_6049_thumb.png
subtitle: The one about the ctags ruby gem
categories: ruby
---
I created a [gem](https://github.com/iamkristian/ctags_ruby) for doing ctags on my ruby project files and gem dependencies. Basically it will find all ruby files in your project, and run ctags on them. Then it will dive into your ```Gemfile``` and trawl through the source files of each gem.


It will store tags in ```.tags``` and ```.gemtags``` respectively.

### Installing it

Just do a

```bash
gem install ctags_ruby
```

### Making that play nice in vim

Simply add the following to your ```.vimrc```

```vimrc
set tags=.tags,.gemtags
```

And you're good to go.

