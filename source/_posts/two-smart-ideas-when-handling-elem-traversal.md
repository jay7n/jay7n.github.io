---
title: Two smart ideas when handling elem-traversal
date: 2022-03-04 21:54:49
tags: algorithms
---

Just as same as the Death is inevitable to human, Traversing Elements of a Sequence is also inevitable to programmers. If you're a developer who's been working for a few years, I bet you've probably written the for-loop-clause thousands of times.

When Given a list or an array, People Typically peek elements one by one in a simple and brutal-force way. Well, nothing's special. I didn't look into it too much either until I began to sharp my algorithm skills recently. Reading the section *LinkedList Questions* from the book *CTCI*, I learnt that there exists two pretty smart and elegant ideas when handling elem-traversal problems.



## 1. Recursion and Backward-Traversal

A function could call another function, which could keep on calling others, and so on. This forms a Call-Stack. Call-Stack is a type of Stack data structure that follows LIFO(Last In and First Out) rule. This means when function A is calling function B, there is a chance for A to do something (before and) after the context has left B's scope, but before leaving A's scope.

Now think about this question: For a singly linked list(which means there's only a next-> pointer but no prev-> pointer for each node of the list), how do you traverse this list backward?

{% codeblock %}
how do you traverse this list backward?

1 -> 2 -> 3 -> 4 -> ...
{% endcodeblock%}

Here is where Function Recursion comes in.

If we design a function to peek an element of a list and send its next element to the same function within the call, we can implement a list traversal. The function we're using here is called recursive function.

The order between peeking an element and sending next element into recursion is the key. If we peek first and then send, it results in a forward traversal; If it's the other way around, we get a backward traversal.

{% codeblock lang:js%}
function traverse_backward(node) {
	if (node) {
		traverse_backward(node.next)；
		peek(node);
	}
}
{% endcodeblock%}


## 2. Fast/Slow Runner (or Pointer)

Sometimes we care about a certain element which has something to do with the
last one but isn't the last itself. For example maybe we want the third element
to the last one, or the mid-element of the list. What is a bit tricky here is
that the given list is singly and yet we don't know its length in advance.

Allow me to clarify something first. The recursive function mentioned above
could of course solve these questions too. When reach the list end we get the
length of list and then can backward-traverse a certain number of times to meet
the condition. This would take 2 loops(forward and backward), though it still
costs a O(n) time. But if we were more cautious and want to do it better, we
may ask is it possible to just run for only 1 loop?

Yes. We can do it with Fast/Slow Runner algorithm. The idea is that we create
two pointers, one following the other. The first pointer is deemed as Fast
Runner which runs in the normal speed(once a time); the pointer following it is
deemed as Slow Runner, which is launched when some conditions are met, in some
speed depending on the specific cases. When Fast Runner reaches the last
element, the position where the Slow Runner is currently located is exactly the
answer we got for this question.

For example suppose we need to get the 3rd element to the end of list. We create
two pointers and let the first one go as normal, and after 3 steps it did, we
then let the second pointer begin to go. Both go 1 step once time. In the end
when the first is done, the second one's position is exactly the 3rd to the
last. In the whole process there is only one for-loop travelling. 

Let's look at another example. How do we retrieve the mid-element? The idea is
simple as well. When the Fast Runner goes 2 steps a time, the Slow Runner moves
1 step forward. This will result in a fact that at anytime the Slow Runner is at
the half location of the Fast Runners'.



