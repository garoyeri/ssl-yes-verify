---
title: Introduction
---

## Introduction

When working in corporate environments, you may encounter SSL Proxies
from your friendly neighborhood security departments that insist on
scanning your SSL / TLS traffic. Normally this will be transparent to
you, but if you're developing software, you'll start to bump against
the infamous `"SSL certificate problem: self signed certificate in
certificate chain"` message.

When working with modern runtime platforms like .NET, Java, Node, Ruby,
Python, and so on, you'll run into wrinkles in the way each platform handles
TLS communication across different operating systems (Linux, Windows, Mac).
It is enough to drive you mad and make you give up and just turn off SSL
verification. DON'T DO THIS! You can fight it!

This site is meant to gather and document as many of the examples of how to
properly deal with self-signed certificates and corporate SSL proxies. Sometimes
this means creating custom container images, or just setting different environment
variables.

Pull requests and contributed content are super welcome! The more we can get consolidated
here, the easier it will be for everyone rather than trying to find the result
across many other websites, blogs, documentation, and whatever.
