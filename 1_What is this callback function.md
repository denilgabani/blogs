![cover Image](https://blog.denilgabani.com/_next/image?url=https%3A%2F%2Fcdn.hashnode.com%2Fres%2Fhashnode%2Fimage%2Fupload%2Fv1641108201327%2FtYooNF1th.jpeg%3Fw%3D1600%26h%3D840%26fit%3Dcrop%26crop%3Dentropy%26auto%3Dcompress%2Cformat%26format%3Dwebp&w=1920&q=75)

# What is this callback function?

Whoever comes into the Javascript world🌎 I am sure most of them would have gotten a question❓ **why do we use these callback functions?** and **how does it work?** even I had the same questions so let's deep dive🏊🏻‍♂️ into these questions and learn👨🏻‍🏫 from them.

## What is Callback Function?

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

![whatdoesthatevenmean.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641060518526/Oy02PfLh0.gif)

Don't worry it will become more clearer as we go further but first, let's know why do we even use these callback functions anyway?

## Why do we use the Callback Function?

As we all know Javascript is a Single Threaded🧵 programming language it can only run one task at a time, but if you imagine let's take a task that takes 2 minutes to complete, and to execute other tasks you have to wait for these 2 minutes to complete this current running task that's not good as the whole UI is stuck for these 2 minutes🤯.

![loading.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641060845927/eAmBAR9Jn.gif)

So it's not efficient and as a human, we should do things efficiently at least that's what the world expects😶 and that's when Event Loop and Callback Functions come to the rescue.

## How does Callback Function Work exactly?

Let's learn it by example:

```plaintext
function makeupCompleted() {
  console.log("Hey now we are ready for show");
}

console.log("Hi, Welcome to the callback show!");

setTimeout(makeupCompleted, 5000);

console.log("While actors are being ready let's do some jokes!");
```

How does it work behind this code?

![callback_1_2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641045688341/WX6hgZNjW.gif)

**Beware⚠ above visual representation is in slow motion it does not actually execute this slow.**

If you see in the above visualizer there are mainly 4 components:

**1\. Call Stack📚:**

Call Stack is used for keeping track of function calls.

Whenever a function is called while executing code it is pushed into this call stack and whenever the top function of the call stack is finished then that top function is removed from this call stack.

This call stack is based on a simple data structure called stack (Who goes last comes out first - like a stack of trays) let's not get into that right now. We will keep it simple.

So basically Call Stack is used to track the function calls That's it.

**2\. Web APIs🧩 :**

[Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) are the list of APIs and objects provided by the browser itself, not by Javascript. Web APIs include many useful APIs like setTimeout, DOM, HTTP requests(XHR).

So any of the async, non-blocking Web API functions execute it goes into the Web API rectangle area.

**3\. Callback Queue 🚶🚶🚶🚶:**

The callback function does not execute directly. First, every callback function goes to this callback queue, and then when the call stack becomes finally empty then it adds to the call stack.

This Callback Queue is based on the queue data structure (Who goes first comes out first - just like a long ticket line).

So whichever callback function is added first in the queue will come out first from the callback queue.

But the question is when it will come out and what happens after🤔?

Whenever the call stack becomes totally empty and no more things to add there then the callback function will be moved from callback queue -&gt; call stack and after call stack does it works and Wheel of Time continues.

![wheeloftime.webp](https://cdn.hashnode.com/res/hashnode/image/upload/v1641061841143/lDDlit0A3.webp)

**4\. Event Loop🔄:**

When the question comes who will watch when the call stack becomes empty and move callback function from callback queue -&gt; call stack that time Event Loop makes its entry.

![entry.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641062053146/H5RuCU8iB.gif)

Event Loop watches👀 over this call stack and callback queue and moves callback function from callback queue -&gt; call stack when call stack becomes empty.

Now that was too much explanation🥱 but it was necessary to get an underlying picture of the working callback function. Hey, we have to do what we have to do but we will do it with fun!

![spirit.webp](https://cdn.hashnode.com/res/hashnode/image/upload/v1641062257154/4xQg6avzf.webp)

Let's get back to the above snippet code the one we have seen at the start of the blog if you remember😜.

Now the execution of code will start from top to bottom⬇.

▶ First is the definition of makeupCompleted() function. So now Javascript knows there is a function name makeupCompleted().

▶ After that it executes console.log("Hi, Welcome to the callback show!");

So this console.log() goes to Call Stack and then it removes from stack and prints the log on console "Hi, Welcome to the callback show!" which greets you🙋🏻‍♂️ and welcomes you to the show.

▶ Now comes setTimeout(makeupCompleted, 5000); function comes to play because some actors need to complete their makeup.

For those who do not know about setTimeout don't worry we got you covered:

setTimeout is one of the methods of WebAPIs used for setting a timer⏳ that executes a function or specified piece of code once the timer expires.

So setTimeout goes into the call stack and the call stack executes it and removes it. As setTimeout is WebAPIs and timer is set to 5000ms (5s) with given handler function makeupCompleted() it will wait into WebAPI box for this 5000ms meanwhile code execution is still running parallelly.

So as long as setTimeout executes and goes to WebAPI the next line console.log("While actors are being ready let's do some jokes!"); makes its entry to call stack of course while actors are doing their makeup we can not make the audience👨‍👩‍👧‍👧 to wait so we are starting to do some jokes parallelly.

so the call stack executes this function logs "While actors are being ready let's do some jokes!" over the console.

After 5000ms when the timer expires the callback function makeupCompleted() is being added into the callback queue from WebAPIs.

▶ EventLoop is always watching👀 to get the opportunity of clear ground to make an attack⚔.

Meaning when the call stack is empty and no more things remain to add into the call stack EventLoop makes its play and adds this callback function makeupCompleted() into the call stack and now the call stack does its work again and the cycle🔁 continues.

So this is how callback functions work.

![finally.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641063017992/RpPwM7MSA.gif)

**If you want to see more nested callback functions you can check the below code snippet:**

```plaintext
function jokesCompleted() {
  console.log("Hey we have laughed enough just stop it no more...");
}

function makeupCompleted() {
  console.log("Hey now we are ready for show");
  setTimeout(jokesCompleted, 3000);
}

function checkingOnActors() {
  console.log("Checked on actors they are being ready...");
}

function getSomeDrinks() {
  console.log("Drinks are coming");
}

function playSomeMusic() {
  console.log("Music is playing on background");
}

console.log("Hi, Welcome to the callback show!");

setTimeout(checkingOnActors, 1000);

setTimeout(getSomeDrinks, 1000);

setTimeout(playSomeMusic, 500);

setTimeout(makeupCompleted, 5000);

console.log("While actors are being ready let's do some jokes!");
```

![callback_2.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641057402199/-hgI6kPOb.gif)

Hey, now we know how callback works behind the scene.

If you want to get more and clear understanding🧠 of this you can check out this below video of Philip Roberts over the JSConf:

[![video of Philip Roberts over the JSConf](https://img.youtube.com/vi/8aGhZQkoFbQ/0.jpg)](https://youtu.be/8aGhZQkoFbQ)

If you also want to play🏏 with the Callback function visualizer you can check out this tool which is provided by Philip Roberts [http://latentflip.com/loupe/](http://latentflip.com/loupe/)

Special Thanks to Philip for this🙏🏻.

Now even we know how the callback function works it does not get that much easy to work with these callback functions because when we work on more complex projects we will be using more and more callbacks for non-blocking behavior and it creates too many nested levels.

![nested.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641063358172/sR4kzownV.gif)

When callbacks are nested too much and then it's hard to keep track of it and understand it and we call it **callback hell👿 in the Javascript world**. We all try to keep our distance with callback hell.

Example of callback hell:

```plaintext
fs.readdir(source, function (err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function (filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function (err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function (width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(dest + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
})
```

![031f1899cdf541ef26d7988bc1a45d57.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641058774703/wh9Bg7hrI.gif)

## So which good karmas🙏🏻 can help us to keep away with this callback hell?

You can follow **3 popular rules** to avoid callback hell:

**1\. Keep your code shallow🤏🏻:**

- Give descriptive names
- Put a limit to use nested functions

**2\. Modularize🧩:**

- Modularize your code by splitting it and adding it into different files and then you can combine it into another file that can do big things.

**3\. Handle every single error❌:**

- This rule is to make your code more stable than readable. Handle every possible exception in your code ideally of course.

Now, what if I tell you there are other ways to handle async and non-blocking code other than callback.

![what.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641064008614/c1_l2103N.gif)

We can use the below 3 ways to handle async code:

**1\. Promises**

**2\. Async/Await**

**3\. Generators**

We will not cover these now as we all need some snacks🍴 now so we will explain these in our upcoming blogs.

**To stay updated and learn together follow me on: [@denilgabani](https://twitter.com/denilgabani)**

![follow me.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641064398610/mvOrPEA3z.gif)

I hope you enjoy it. So See you later now😃.

![seeyoulater.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641064201912/zW3eLKCJB.gif)
