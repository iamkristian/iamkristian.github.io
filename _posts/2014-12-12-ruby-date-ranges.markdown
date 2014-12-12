---
layout: post
title:  "Ruby & Rails Date ranges"
date:   2014-12-12 08:58
categories: ruby date ranges
---

So I found myself wanting to iterate over a date range in Rails. Naively I
started out doing this:

```ruby
 (5.days.ago..Date.today).each { |d| puts d }
TypeError: can't iterate from ActiveSupport::TimeWithZone
```
Which of course is wrong, since the expression ``` 5.days.ago ``` is not a date.

Things weren't entirely obvious. So I broke out irb, and started to experiment.

First off lets try ranges in plain ruby

```ruby
require 'date'
(Date.new(2014,12,8)..Date.today).each { |d| puts d }
 2014-12-08
2014-12-09
2014-12-10
2014-12-11
2014-12-12
=> #<Date: 2014-12-08 ((2457000j,0s,0n),+0s,2299161j)>..#<Date: 2014-12-12 ((2457004j,0s,0n),+0s,2299161j)>
```

So that works pretty good - remember to add the parens, or you'll be having a hard time.

And in Rails, mixed with the wonders of ``` ActiveSupport::TimeWithZone ```

```ruby
(5.days.ago.to_date..Date.today).each { |d| puts d }
2014-12-07
2014-12-08
2014-12-09
2014-12-10
2014-12-11
2014-12-12
=> Sun, 07 Dec 2014..Fri, 12 Dec 2014
```

The lesson learned is

> Always use the same object in the range, don't mix apples and bananas

