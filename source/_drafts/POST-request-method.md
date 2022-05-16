---
title: POST request method
tags: web
---

There're some reasons I would always try dodging POST request whenever I have a chance. 

Number One and the most, it's more complex to grasp than GET. Number Two, HTTP proxies are highly error tolerant (or more obscure on the other view) so that if something appears to be wrong, you barely know which side it belongs to. Number three, some head fields at different parts have very similar and overlapped definitions which make things more tangled.

But one day I was being trapped in a problem for a couple of hours where uploading a file to a remote server was somehow always failed, and it's the time that I realized I had nowhere to escape. It's the time to confront this issue now. So I began to dig around how POST request really works.


