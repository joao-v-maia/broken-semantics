+++
title = 'Journey to the Center of Goland'
date = 2026-03-01T21:19:20-03:00
draft = false
categories = ['Programming']
tags = ['golang', 'languages']
+++

## Journey to the Center of Goland

One of my favorite classes in college was "Programming Paradigms" in which the professor would introduce new languages and paradigms every week or so. During the 6 months of the course I've learned a bit of Haskell, Lisp, Prolog, Lua and Jason, applying to solve the same problem, a game called Suguru. That experience showed me that programming languages are just interfaces that allows us to lead the computer through the perilous path of problem solving.

Nowadays I have less time available to tinker with new languages and it's been a couple of years since I've learned one from scratch, at least on a level that I can consider useful. Considering that my brain may be a little bit rusty when it comes to new languages, it seemed prudent to start with a language that was designed to be simple to the unnitiated, so I've picked Go to be the first step of this comeback tour.

I'm planning to document my path, highlighting what I think to be important and comparing with other languagens I use daily on my work life (PHP, Javascript, Python and Dart). I'll try to write shorter articles, focusing on one or two subjects, to keep them frequent and modular. So bear with me while I make my journey to the center of Goland.

## Philosophy

As with other types of tools, the first thing to learn about a programming language is it's purpose and capabilities, if you use a jackhammer to cut down a tree it may do the job but it will take a while and probably won't be the cleanest cut. In this sense, Go is a general purpose language, so it's not designed to optimize a single set of tasks, but it does have some principles that are more useful on certain scenarios.

The language's official website cites reliability, efficiency and simplicity as three pillars to be highlighted. The presence of features like explicit error handling, a garbage collector and the race condition and the absence of others like operator overloadings and type coercion are the proof of that commitment. Go aims to keep it simple, even at the cost of some better developer experience, and that's why the language is very used in projects that need a solid base, like Docker and Kubernetes.

If you're used to work with a language like PHP where everything is magic, Go can look a bit boring and constrictive, but you'll get used after some time, specially when you start to notice that a lot of that PHP magic usually backfires and turns into bugs. Ultimately the decision of restrict yourself to simpler code to ensure reliability and efficiency is based on the necessities of the project.

## Ecossystem

The first point to make my eyes shine was the module and packaging system. Here the language understood flaws from earlier projects and tackled the majority of common problems, starting with first party CLI being a multi-tool that handles compiling, execution, packaging and dependencies. No discussion about `yarn vs npm vs pnpm` or feuds on `node vs bun`, just use the language's own tool that comes bundled with it's installation.

Installing and hosting packages is also simple, any URL that points to a VCS can be direct used as an import path, even allowing custom domains with redircts on HTML meta tags. This approach decentralizes hosting and empower users to scaffold projects as they wish, with the possibility of custom and private proxies to protect enterprise packages.

Another huge selling point to me is Go's standard library, which is unusually self-sufficient and implements the reliability and simplicity principles at the language's core. Most languages rely heavily on third-party packages for basic infrastructure work, but Go ships with production-ready implementations of HTTP/1.1 and HTTP/2 servers and clients, a full crypto suite, JSON and XML encoding, SQL database interfaces, HTML templating with automatic XSS escaping, and more. This means a large class of networked services and CLI tools can be built with zero external dependencies, which directly reduces supply chain risk and eliminates dependency version conflicts for the most common use cases.

## Final remarks

While I'm still on a honey-moon period with this language, I do believe that these foundational decisions made by the Go team among the years created a really unique developer experience matched with a powerful runtime that explains the language's adoption and success with so many great companies.

My next experiments with go will be focused in the language's use case for microservices and I hope to find some writing subjects there to expose here.

## References

1. The Go Programming Language by Alan Donovan and Brian Kernighan, 2015.
2. [Official Go documentation](https://go.dev/doc/).