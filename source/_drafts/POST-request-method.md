---
title: POST request method (1)
tags: web
---

There're some reasons I would try dodging POST requests whenever I get a chance. 

Number One and the most, it's more complex to grasp than GET. Number Two, HTTP proxies are highly error-tolerant (or more obscure on the other view) so that if something appears to be wrong, you barely know which side it belongs to. Number three, some header definitions at different parts are overlapped, which gets things more tangled.

But one day I was being trapped in a problem for a couple of hours where uploading a file to a remote server somehow always failed, and it's the time that I realized I had nowhere to escape anymore. Maybe it's the time to confront this issue now. So I began to dig around how POST request really works.

## All is starting from HTTP requests
I guess developers won't feel strange with HTTP requests, but wait... think that again. Do they? The fact is people rarely handcraft these messages by their own, which is instead constructed by an API of a program such as a Browser in most cases. So it's true that we could see them very often, but only would when something goes wrong hence a quick check is needed. OK, for example, in my Chrome I saw all parameters have been packed into this GET request, so at least it's not a part of the problem, then let's look somewhere else.

That's how I as a frontend developer deal with them in my daily work and Yes, I can barely remember anything about that request message once it's done, only except one word or two with those parameters. Seriously, even for a very simple HTTP request you'll eventually get a bunch of key-values coming from the browser. There is no reason to follow up what each of them is for.

[img]

So when it comes to uploading a file via POST and when I start to notice how to put binary data in a request message, I realize there is an optional 'body' part, which usually appears in a response message when you want to GET some data from the server. Again here is where the strange feeling comes in: WE ACTUALLY CAN NOT CONSTRUCT THIS MESSAGE MANUALLY even if we know the HTTP rules. We have to ask some sort of HTTP client programs to do it for us. So the way of how to encapsulate binary data into the request message totally depends on what client/library we're using, and they vary a lot.

[img]

And back to old decent days, POST is used to submit some kind of form data(there is even a \<form/\> tag in HTML, remember? normally with a couple of \<input/\> or \<label/\> elements in it). What's more is that, there are two types of data underneath, **multipart/form-data** and **application/x-www-form-urlencoded**(each name has its own ugly aesthetic taste IMO). Such types are called **MIME types**, or **Content-Types**(There're more stories about this concept below). I don't mean to bring all of these concepts here at once, but it already explains a lot why I don't like POST, at all.

[img]

## POST is normally to commit key-value based data with binary-data (files) included
To put it another way, in contrast to GET being used like a read() method in a program, POST is just like a write() method. So the thing is how do we represent data to be written. We should allow it to be a number, a string, an array or even an object. It literally can be anything. Let's pick up a proper data structure which looks as generic as possible: Numbers or Strings are primitive and they can not represent others. Arrays or Lists are better but lack of the ability to describe hierarchical levels. Objects(in javascript) or HashTables, are the best to include various types talked above, and that's our choice. And that's why FormData is chosen to be the POST's body too, because FormData is exactly a kind of key-value based data structure. 

Just like you set some data in a HashTable, for each item you want to add, you give it a key name and a value. For example a 'name' with 'Jayson', a 'age' with 37, a 'male' is true, a 'skills' with ['javascript', 'graphics', '...'], and so on. We can then submit this data to the server via POST. 

```
{
  name: 'Jayson',
  age: 37,
  male: true,
  skills: ['javascript', 'graphics', '...']
}
```

Next comes the interesting part: a 'cv' with a file stored in my hard-drive is also a valid item. Its value no doubt is a binary data. Again as a reminder we do this by borrowing some kind of client API rather than manually hand write them somewhere.

```
{
  cv: SOME BINARY DATA (we need a API to do so)
}
```

We'll discuss this BINARY part later, but now the point is that POST is used to submit arbitrary key-value based data to the server, including the binary type, which is often used to upload files. 


## There're two ways of encoding these key-value based data in POST


## Content-Type in the request header is to specify which type of data  you're using

## Mind that multipart/form-data is used to upload files. Why?

## Mind that there is also a sub header config under a file-field declaration and a same name 'Content-Type'

## When running in different environments(on browser or on the server), there're different ways to specify what is the Content-Type of a specified file in POST form-data

