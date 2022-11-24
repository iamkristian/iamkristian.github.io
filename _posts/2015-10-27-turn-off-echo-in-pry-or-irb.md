---
layout: post
title:  "Turn off echo in pry or irb"
date:   2015-10-27 13:30
image: IMG_6547.png
image_thumb: IMG_6547_thumb.png
subtitle: The one about turning off echo in Pry or Irb
categories: ruby pry irb
---
When you do something in pry or irb that returns a looong result, sometimes
you don't want the result in your terminal. So to turn it off you can do this.

```ruby
# In irb
irb_context.echo = false

# In pry
_pry_config.print = proc {}

# If you want to restore echo in pry, save the print proc before overwriting it.
pry_print = _pry_config.print
_pry_config.print = proc {}
```

