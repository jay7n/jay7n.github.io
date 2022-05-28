---
title: POST request method (1)
tags: web
---

There're some reasons I would try dodging POST requests whenever I get a chance. 

Number One and the most, it's more complex to grasp than GET from the first glance. Number Two, HTTP proxies are highly error-tolerant (or more obscure on the other view) so that if something appears to be wrong, you barely know which side it belongs to. And Number Three, some header definitions at different parts are overlapped, which gets things more tangled.

But one day I was being trapped in a problem for a couple of hours where uploading a file to a remote server somehow always failed, and it's the time that I realized I had nowhere to escape anymore. Maybe it's the time to confront this issue now. So I began to dig around how POST request really works.

But first, a little background about me. I'm not the guy who chose to be a web frontend specialist at the beginning of the career. I have general programming skills, senses and taste though. So however Javascript is my favorite, HTML, CSS or HTTP is not as that much, which I should be ashamed of myself about. Anyway, let's get started.

------

I guess developers won't feel strange with HTTP requests, but wait... think that again. Do they? The fact is people rarely handcraft these messages on their own, instead they construct them by a program such as a Browser in most cases. So it's true that we could see them very often, but only would really dig in it when something goes wrong. For example let's say, one day something was broken, and in my Chrome I saw all parameters have been packed into this GET request, so at least it's not a part of the problem, then let's look somewhere else.

That's how I deal with them in my daily work and Yes, I can barely remember anything about those request messages once they're done, well, except only one word or two with those parameters. To be frank, even for a very simple HTTP request you'll eventually get a bunch of key-values coming from the browser. it is no reason to follow up what each of them is for, isn't it?

[img]

So when it comes to uploading a file via POST which I got stuck with, I begin to think how the binary data is really put in a request message, and then I remember there is an optional 'BODY' part we can rely on, which more usually appears in a response message when we want to GET something from the server. Well, on hand hand we get BODY from a GET request. On the other hand we will put a BODY to a POST request. Does this look like something else?

Analogous to GET being used like a read() method in a program, POST is just like a write() method. The thing is how do we represent data to be written. We should allow it to be a number, a string, an array or even an object. It literally can be anything. So what is a proper data structure which could just be as generic as possible? Numbers or Strings are primitive and they can not represent others. Arrays or Lists are better but lack of the ability to describe hierarchical levels. Objects(in javascript) or HashTables, are the best choice to include various types talked above.

Just like how we set some data in a HashTable, for each item we want to add, we will give it a key name and a value. For example a 'name' with 'Jayson', a 'age' with 37, a 'male' with true, a 'skills' with ['javascript', 'graphics', '...'], and so on. We pack them together and then submit it to the server via POST. 

```
{
  name: 'Jayson',
  age: 37,
  male: true,
  skills: ['javascript', 'graphics', '...'],
}
```

------
As we all know that POST is one method of HTTP proxy which lies on the topmost level of networking model, there're a few other proxies playing the role beneath HTTP. Only with them and through a long and complicated electronic way, the client and the server are able to communicate with each other. So in most cases as a non-system developer you need to count on some tools to send/receive HTTP requests. It may be a lib, a sdk or an app (like a Browser). The tool guarantees the message is shaped as a valid request that conforms to HTTP proxy, however filling whatever contents is up to you.



------
Again here is where the strange feeling comes in: WE ACTUALLY CAN NOT CONSTRUCT THIS MESSAGE DIRECTLY even if we know the HTTP rules. We have to ask some sort of HTTP client programs to do it for us. So the way of how to encapsulate binary data into the request message totally depends on what client/library we're using, and they vary a lot.
------

[img]

And back to old decent days, POST is used to submit some kind of form data(there is even a \<form/\> tag in HTML, remember? normally with a couple of \<input/\> or \<label/\> elements in it). What's more, there are two types of data underneath, **multipart/form-data** and **application/x-www-form-urlencoded**(each name has its own ugly aesthetic taste IMO). Such types are called **MIME types**, or **Content-Types**. I don't mean to be mumbling about all of these here, but it already gives you a good idea why I don't like POST, at all.

[img]



## 

Next comes the interesting part: a 'cv' with a file stored in my hard-drive is also a valid item. Its value no doubt is a binary data. Again as a reminder we do this by borrowing some kind of client API rather than manually hand write them somewhere.

```
{
  cv: SOME BINARY DATA (we need a API to do so)
}
```

We'll discuss this BINARY part later, but now the main point is that POST is used to submit arbitrary key-value based data to the server, including the binary type which is often used to upload files. 

