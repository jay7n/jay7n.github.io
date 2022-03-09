---
title: Two smart ideas when handling elem-traversal
date: 2022-03-04 21:54:49
tags: algorithms
---

Just as same as the Death is inevitable to human, Traversing Elements of a Sequence is also inevitable to programmers. If you're a developer who's been working for a few years, I bet you've probably written the for-loop-clause thousands of times.

When Given a list or an array, People Typically peek elements one by one in a simple and brutal-force way. Well,nothing is special. I didn't think about it too much either until I began to sharp my algorithm skills recently. Reading the section *LinkedList Questions* from the book *CTCI*, I learnt that there exists two pretty smart and elegant ideas when handling elem-traversal problems.


## 1. Recursion and Backward-Traversal
A function could call another function, which could keep on calling others. This is called a Call-Stack. Call-Stack is a type of Stack data structure that follows LIFO(Last In and First Out) rule. This means when function A is calling function B, there is a chance for A to do something after the context has left B's scope, but before leaving A's scope.

Now think about this question: For a singly linked list(which means there's only a next-> pointer but no prev-> pointer for each node of the list), how should we traverse this list backward?

{% codeblock %}
how do you traverse this list backward?

1 -> 2 -> 3 -> 4 -> ...
{% endcodeblock%}

Here is where Function Recursion comes in.

If we design a function to peek an element of a list and send its next element to the same function within the call, we can implement a list traversal. The function we're using here is called Recursive function.

The order between peeking an element and sending next element into recursion is the key. If we peek first and then send, it results in a forward traversal; If it's the other way around, we get a backward traversal.

{% codeblock lang:js%}
function traverse(node) {
	if (node) {
		traverse(node.next)；
		peek(node);
	}
}
{% endcodeblock%}

## 2. Fast/Slow Runner (or Pointer)