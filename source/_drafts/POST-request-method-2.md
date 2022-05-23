---
title: POST request method (2)
tags:
---

## Two ways in encoding data in POST
In the previous article I talked about that POST is used to commit key-value based data to a server. Also we can call this K-V paired data as 'payload'. Despite how they're done behind the scene, there're two ways in representing(or encoding) the data. Since as a user you're the one who make the choice, it's also your job to learn them well. These two ways are: `application/x-www-form-urlencoded` and `multipart/form-data`.

You may feel a little dizzy as the same way as I have experienced before. 'What the hell is these, some mysterious cipher?'. It's fine, let's just keep them in mind for now and I'll give an explanation later.

### application/x-www-form-urlencoded
In this way a '=' character is placed between the key and the value, and each K-V pair is concatenated with each other using the '&' character. So the payload mentioned in the last article
```
{
  name: 'Jayson',
  age: 37,
  male: true,
  skills: ['frontend', 'javascript', 'graphics', '...'],
}
```
could just be represented as 
```
name=Jayson&age=37&male=true&skills=frontend%2Cjavascript%2Cgraphics%2C...
```

You may notice there are some strange characters in this string, such like '%2C'. They're referred to as [Percent encoding](https://developer.mozilla.org/en-US/docs/Glossary/percent-encoding) and it's just because of their existence the name of this way is being called *'...-urlencoded'*. In essence that's a safer approach to transfer data via internet to avoid some special non-alphanumeric characters to be treated as having some special meanings in some intermediate steps. There's a list in the above link where you can find all special characters and what each of them is encoded into. Typically one such a char is turned into a '%' followed by its hexadecimal representation in the ASCII table.

While pros of this approach are prominent, it also brings the cons: for those special characters

### multipart/form-data


## MIME or Content-Type


## Content-Type in the request header is to specify which type of data  you're using

## Mind that multipart/form-data is used to upload files. Why?

## Mind that there is also a sub header config under a file-field declaration and a same name 'Content-Type'

## When running in different environments(on browser or on the server), there're different ways to specify what is the Content-Type of a specified file in POST form-data
