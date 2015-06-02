---
title: Easy async workers for Haskell
author: Bob Long
---

TLDR: [Sidekiq inspired worker in Haskell](https://github.com/bobjflong/simple-worker)

I do a lot of web programming, and I'm currently learning the [Yesod](http://www.yesodweb.com/) framework. I think it's important to have lightweight workers in your toolbelt and gain the ability to easily async some tasks, to reduce response times and overhead. When using Ruby on Rails I normally use Sidekiq, so I'm using that as a simple model for a worker in a Haskell enviroment. Here's what I'm looking for:

* Few dependencies - Redis is fine
* Deployable on Heroku
* Handles failure by re-enqueuing work with exponential backoff
* Handles abrupt termination reasonably well, by re-enqueueing work in progress
* Drop jobs after they fail n times

I found this fairly easy to accomplish, and you can check out the results [here](https://github.com/bobjflong/simple-worker). Really it's a quite simple interaction between threads using the STM monad, and using the [async](https://hackage.haskell.org/package/async) library to contain failures. This isn't bomb proof, it is susceptible to the [same problems as default Sidekiq](https://github.com/mperham/sidekiq/wiki/Reliability#server). I may or may not look at using the `RPOPLPUSH` redis command to tighten this up.
