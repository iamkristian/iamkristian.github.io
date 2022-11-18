---
layout: post
title:  "Web Development With Elixir"
date:   2014-05-22 06:43:00
categories: elixir web
---
About a month ago [@jamiemhodge](https://twitter.com/jamiemhodge) talked me
into giving a talk about web developement with [Elixir](http://elixir-lang.org)
for the [Copenhagen Ruby Brigade](http://copenhagenrb.dk/).

So this post contains the recorded talk and links to the code used in the talk.

 <iframe width="640" height="360" src="//www.youtube.com/embed/mh6kNxoO19A?rel=0" frameborder="0" allowfullscreen></iframe>

The source from the talk can be found here:

* [iamkristian/web_development_with_elixir](https://github.com/iamkristian/web_development_with_elixir_talk)
* [iamkristian/elixir_commits](https://github.com/iamkristian/elixir_commits)
* [iamkristian/rack_example](https://github.com/iamkristian/rack_example)

## Performance

| Language | Options | Result |
|:---------|-------|------:|
|Ruby 2.1.1 MRI|none|788 req/s|
|Ruby 2.1.1 MRI|puma|10700 req/s|
|Ruby 2.1.1 MRI|puma -q -t 10 -w 4 | 22356 req/s|
|Elixir 0.13.2| Weber | 23126 req/s|
|[Elixir 0.13.2](https://gist.github.com/gudmundur/0513a965c1cf6b8a7327)| Dynamo | 31295 req/s|
|[Go](https://gist.github.com/gudmundur/0513a965c1cf6b8a7327)| | 53071 req/s|

The talk produced some additional talk on twitter afterwards.
[@gudmundur](https://twitter.com/gudmundur) made a _hello world_
[example](https://gist.github.com/gudmundur/0513a965c1cf6b8a7327) in [Go](http://golang.org/).

All tests were performed using

```bash
wrk -t 10 -c 400 <url>
```

## Resources for learning more

* [Elixirsips](http://elixirsips.com)
* [Learn You Some Erlang](http://learnyousomeerlang.com/)
* [Programming Elixir](http://pragprog.com/book/elixir/programming-elixir)
* [Erlang & OTP in Action](http://www.manning.com/logan/)
* [The Little Elixir & OTP Guidebook](http://www.exotpbook.com/)

Thank you to the [Copenhagen Ruby Brigade](http://copenhagenrb.dk) for being an awesome audience.
