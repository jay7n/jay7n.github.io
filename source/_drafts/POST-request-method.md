---
title: POST request method
tags: web
---

There're some reasons I would try dodging POST request whenever I get a chance. 

Number One and the most, it's more complex to grasp than GET. Number Two, HTTP proxies are highly error tolerant (or more obscure on the other view) so that if something appears to be wrong, you barely know which side it belongs to. Number three, some header definitions at different parts are overlapped, which gets things more tangled.

But one day I was being trapped in a problem for a couple of hours where uploading a file to a remote server was somehow always failed, and it's the time that I realized I had nowhere to escape anymore. Maybe it's the time to confront this issue now. So I began to dig around how POST request really works.

## All starts from HTTP requests
I guess developers won't feel strange with HTTP requests, but wait... think that again. Do they? The fact is people rarely handcraft these messages by their own, which is instead constructed by an API of a program such as a Browser in most cases. So it's true that we could see them very often, but only would when something goes wrong hence a quick check is needed. OK, in my Chrome I saw all parameters have been packed into this GET request, so at least it's not a part of the problem. Let's look somewhere else.

That's how I as a frontend developer deal with them on my daily work and Yes, I could barely remember anything about that request message, only except for one word or two with my parameters. Seriously, even for a very simple HTTP request you'll get a bunch of headers from the browser. There is no reason to follow up what each of them is for.

So when it comes to uploading a file via POST, 


## POST is used to add new resources to the server


## POST is normally to upload files or commit form data

## There're two distinguish types of data POST could handle with

## Content-Type in the request header is to specify which type of data  you're using

## Mind that multipart/form-data is used to upload files. Why?

## Mind that there is also a sub header config under a file-field declaration and a same name 'Content-Type'

## When running in different environments(on browser or on the server), there're different ways to specify what is the Content-Type of a specified file in POST form-data

