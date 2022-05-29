---
title: POST request method (1)
tags: web
---

There're some reasons I would try dodging POST requests whenever I stand a chance. 

Number One and the most, it's more complex to grasp than GET from the first glance. Number Two, HTTP proxies are highly error-tolerant (or more obscure on the other view) so that if something appears to be wrong, you barely know which side it belongs to. And Number Three, some header definitions at different parts are overlapped, which gets things more tangled.

But one day I was being trapped in a problem for a couple of hours where uploading a file to a remote server somehow always failed, and it's the time that I realized I had nowhere to escape anymore. Maybe it's the time to confront this issue now. So I began to dig around how POST request really works.

But first, a little background about me. I'm not the guy who chose to be a web frontend specialist at the beginning of the career. I have general programming skills, senses and taste though. So however Javascript is my favorite, HTML, CSS or HTTP is not as that much, which I should be ashamed of myself about. Anyway, let's get started.

------

I guess developers won't feel strange with HTTP requests, but wait... think that again. Do they? The fact is people rarely handcraft these messages on their own, instead they construct them by a program such as a Browser in most cases. So it's true that we could see them very often, but only would really dig in it when something goes wrong. For example let's say, one day something was broken, and in my Chrome I saw all parameters have been packed into this GET request, so at least it's not a part of the problem, then let's look somewhere else.

That's how I deal with them in my daily work and Yes, I can barely remember anything about those request messages once they're done, well, except only one word or two with those parameters. To be frank, even for a very simple HTTP request you'll eventually get a bunch of key-values coming from the browser. it is no reason to follow up what each of them is for, isn't it?

[img]

So when it comes to uploading a file via POST which I got stuck with, I begin to think how the binary data is really put in a request message, and then I remember there is an optional 'BODY' part we can rely on, which more usually appears in a response message when we want to GET something from the server. Well, on hand hand we get BODY from a GET request, and on the other hand we will put a BODY to a POST request. Does this look like something else?

Analogous to GET being used like a read() method in a program, POST is just like a write() method. The thing here is how do we handle the data to be written. This question can be split into two sub questions.

------

Question 1, how do we represent the data? In theory We should allow it to be a number, a string, an array or even an object. It literally can be anything. So what is a proper data structure which could just be as generic as possible? Numbers or Strings are primitive and they can not represent others. Arrays or Lists are better but lack of the ability to describe hierarchical levels. Objects(in javascript) or HashTables, are the best choice to include various types talked above.
u

Just like how we set some data in a HashTable, for each item we want to add, we will give it a key name and a value. For example a 'name' with 'Jayson', a 'age' with 37, a 'male' with true, a 'skills' with ['javascript', 'graphics', '...'], and so on. We pack them together and then submit it to the server via POST. 

```
{
  name: 'Jayson',
  age: 37,
  male: true,
  skills: ['javascript', 'graphics', '...'],
}
```

But that's not the end of this story. The above content is just a theoretical representation. In practice there're two typical ways of encoding the data. One is called `'application/x-www-form-urlencoded'` and the other one is called `'multipart/form-data'`. What the hell is this? They're called [`Content-Type`]()(or [`MIME`]()) which is used to indicate what type of the content the user want to send to the sever. How to specify them? There's a field of the HTTP header named `'Content-Type'` for this purpose. What is the difference between the two? OKay let's continue on.

### application/x-www-form-urlencoded
In this way a '=' character is placed between the key and the value, and each K-V pair is concatenated with each other using the '&' character. So the data mentioned above is actually encoded like this:

```
name=Jayson&age=37&male=true&skills=frontend%2Cjavascript%2Cgraphics%2C...
```

You may notice there are some strange characters in this string, such like '%2C'. They're referred to as [Percent encoding](https://developer.mozilla.org/en-US/docs/Glossary/percent-encoding) and just because of their existence its name is being called *'...-urlencoded'*. In essence that's a safer approach to transfer data via internet to avoid some non-alphanumeric characters to be treated as having some special meanings in some relay points. There's a list in the above link where you can find all special characters and what each of them is encoded into. Typically one such a char is turned into a '%' followed by its hexadecimal representation in the ASCII table, in the form of '%XX'.So it adds to the cost: it takes three times the cost in space for each encoded character.

How do we implement such an encoding? While we can do it on our own, there're also some tools. In browsers we can construct a builtin [`URLSearchParams`]() object to finish the job.



### multipart/form-data
TODO

------
Question 2, How do we transfer the data?
As we all know that POST is one method of HTTP proxy which lies on the topmost level of networking model, there're a few other proxies playing the role beneath HTTP. Only with them and through a long and complicated electronic way, the client and the server are able to communicate with each other. So in most cases as a non-system developer you need to count on some tools to send/receive HTTP requests. It may be a lib, a sdk or an app (like a Browser). The tool guarantees the message is shaped as a valid request that conforms to HTTP proxy, however filling whatever contents is up to you.

In browsers we can create an object of the '[XmlHTTPRequest]()' class, or use a global builtin method '[fetch]()' to send the HTTP request and receive the response. In some other scenarios there're other similar counterparts. Either of these tools provides a low-level functionality though, which means we should construct the message body ourselves and let them conform to the **Content Type** declared in the HTTP request header. 

**What if they aren't kept in step? Nothing happened. The tools will send whatever data we thrust into them**. For example, we can construct a **FormData** object as the POST message body but somehow provide with a **`application/x-www-form-urlencoded`**, which is obviously wrong since it breaks rules. But the message is allowed to be sent. However it's hard to say that the server will give a absolute rejection when they receive the message. It depends.

This leads to a twisted problem which is more usually seen in network programming. That's also one of reasons why I don't like to play with them. According to the proxy, you should follow the rules, but as long as you take charge of both sides(the client as well as the server), basically you can do whatever you want, because you can decide how to encode/decode the message on two ends. 

Things have got evolved a bit further. Due to such an unpredictability, some ends will try to **'sniff'** the message which they got and do some auto-corrections if they can. So it's still possible that you send a wrong message which didn't obey the HTTP rules with this respect but you find the server understands you well.

For some people (like me) who're not fully aware what they're doing, these kind of 'protection' are definitely a disaster. It gives them a hint, like to say, "Great! You're doing things right." while they don't. People either think they do things right OR think servers always have advanced 'magic' to guess out what you really want to express. But the fact is that not every single server will do that. Some servers just simply obey rules and directly take you down.



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

