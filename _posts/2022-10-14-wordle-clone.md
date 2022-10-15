---
layout: post
title:  "Week 1: Wordle Clone"
date:   2022-10-14 3:25:00 -0600
categories: jekyll update
---
The final project in Brian Holt's [intro to front-end development](https://btholt.github.io/intro-to-web-dev-v2/intro) is a Wordle clone. It requires you to learn how to access JSON formatted data via an API and post data to an API to validate it. 

<h3>Here it is! </h3>
<break>
[<h3>Here is the source code</h3>](https://github.com/dlesky/wordle_clone)
<break>
[<h3>Here is the game on its own page</h3>](https://dlesky.github.io/wordle_clone/index.html)

<p style="text-align:center"> <br>   
<iframe
  src="https://dlesky.github.io/wordle_clone/index.html"
  style="width:100%; height:700px;border:none;"
></iframe>
</p>


Aside from some of the CSS animations that are present in Wordle and data-tracking features, it's pretty close. At some point I would like to go back and:

1) Fix the CSS animations (the boxes should change shape when you type and they should flip after you hit enter.)
2) Use animations instead of alert boxes, which are mildly obnoxious. 
3) Implement the IP address tracking feature that limits you to one attempt per day. 
4) With IP address tracking, it would make sense to include the multi-day data tracking features present in the actual version. 
5) Go back and clean up the code to make it more modular. 
6) Prevent new input after you win. 
7) Change color of keys to 'knock out' letters that have been used already. 
8) You have to click on the app's window to be able to enter input via the keyboard. There must be a way to fix this. 

<u>Async and scope: </u>
The thing that tripped me up the most was not being able to modify variables outside of the async function. This forced me to make the whole program run inside an async function. I'm sure there are other ways to do this. I've only scratched the surface of async and APIs. I think I spent at least two hours struggling to try to find a way to do this before giving up. I'll write another blog post on async functions dissecting the options.

{% highlight javascript %}
async function init() {
    const GET_URL = 'https://words.dev-apis.com/word-of-the-day';
    const POST_URL = 'https://words.dev-apis.com/validate-word';
    const promise = await fetch(GET_URL);
    const { word: wordOfDay } = await promise.json();

    ...remainder of code... 
}
{% endhighlight %}

<u>Conditional OR statements: </u>
I also lost some time to the following bug. 

{% highlight javascript %}
if (currentInput === "BACK" || "BACKSPACE") { backspace() }
{% endhighlight %}

The conditional expression (currentInput === "BACK" || "BACKSPACE") always evaluates to true. This is because "BACKSPACE" is <em>truthy</em>. The following code functions as intended.

{% highlight javascript %}
if (currentInput === "BACK" || currentInput === "BACKSPACE") { backspace() }
{% endhighlight %}

