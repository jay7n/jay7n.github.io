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
could be represented as 
```
name=Jayson&age=37&male=true&skills=frontend%2Cjavascript%2Cgraphics%2C...
```


### multipart/form-data


## MIME or Content-Type


## Content-Type in the request header is to specify which type of data  you're using

## Mind that multipart/form-data is used to upload files. Why?

## Mind that there is also a sub header config under a file-field declaration and a same name 'Content-Type'

## When running in different environments(on browser or on the server), there're different ways to specify what is the Content-Type of a specified file in POST form-data
