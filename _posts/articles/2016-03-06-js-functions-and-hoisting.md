---
layout: post
title: Function Declarations vs Expressions (and a bit about Hoisting)
excerpt: "An exploration of the differences between function declaration, expressions, and hoisting"
categories: articles
tags: [function, hoisting, declaration, expression]
image:
  feature: function-notes.jpg
  credit: mrkeith
  creditlink: www.markrichardkeith.com
comments: true
share: true
search_omit: false
---

This article is intended to explore the primary differences between Function Declarations and Function Expressions. By no means is this intended to be an exhaustive or authoritative resource for each and every nuance of the topic, but I hope that it helps to provide clarity. Additionally explored in this article is the idea of "Hoisting" as it relates to functions.  

## Function Declarations

A function declaration defines a named or anonymous function with specified parameters. It does not involve variable assignment. An important idea about function declarations is that they are not executed immediately. Rather, function declarations are "saved" and will be executed later in the program when they are invoked or called. Function declarations MUST begin with the word "function".

#### Types of Function Declarations:

**Named Function Declaration:** 
{% highlight html %}
{% raw %}
  <script>
    function hola (decir) {
      console.log("Buenos días");
      return decir;
    }
    //Can be invoked as follows
    hola("Vuelvo enseguida")
  </script> 
{% endraw %}
{% endhighlight %}

**Anonymous Function Declaration:**

I actually don't know of a good use case for an anonymous function declaration... In order for this function to be called, it must be immediately invoked. See below. 

{% highlight html %}
{% raw %}
  <script>
    function (decir) {
      console.log("anónimo");
      return decir;
    }
    //immediately invoked
    function (decir) {
      console.log("anónimo");
      return decir;
    }("Vuelvo enseguida");
  </script>
{% endraw %}
{% endhighlight %} 

#### Hoisting Characteristics:

Function declarations are ALWAYS hoisted to the top of the JavaScript scope in which they are contained by the JavaScript interpreter. In fact, function declarations are hoisted as an entire function body ABOVE variable declarations. 

One other thing to note about the function declaration's hoisting characteristics (and this pertains to hoisting in general) is that it is stacked under any previously hoisted function declarations. That is to say, if the same named function is declared twice, the function located closest to the bottom of the page will be on the outside of the "stack" and will be the function that is accessible to the code below it.


See the below code for a before and after of simple function declaration hoisting: 

**Before:**
{% highlight html %}
{% raw %}
  <script>

    var chica = "bonita"; 
    var chico = function(que) {
      return que;
    }
    hola("Buenas tardes"); //returns "Buenas tardes"

    function hola (decir) {
      console.log("Buenos días");
      return decir;
    }
  </script> 
{% endraw %}
{% endhighlight %}

**After:** 
{% highlight html %}
{% raw %}
  <script>
    function hola (decir) {
      console.log("Buenos días");
      return decir;
    }

    hola("Buenas tardes"); //returns "Buenas tardes"

    var chica = "bonita"; 
    var chico = function(que) {
      return que;
    }

    /*function hola (decir) {
      console.log("Buenos días");
      return decir;
    }*/
  </script> 
{% endraw %}
{% endhighlight %}

*^^ Notice how the function declaration was after the function invocation and the function still runs.* 

## Function Expressions

A function expression typically defines a function as part of a larger expression syntax. In plain English, a function definition is usually assigned to a variable. As such, a function assigned to a variable is significantly more portable than a function declaration. It can be passed as an argument to other functions or used as a callback (in it's anonymous form as well) in other functions.  

#### Types of Function Expressions:

**Named Function Expression:** 
{% highlight html %}
{% raw %}
  <script>
    var aFunc = function hola (decir) {
      console.log("Buenos días");
      return decir;
    }
    //Can be invoked as follows
    aFunc("Vuelvo enseguida");
  </script> 
{% endraw %}
{% endhighlight %}
*^^ In my limited experience with the JS language, I can't say I've seen any applied benefit to the "named function expression". Some supporters may say that it more easily allows for precise debugging if the bug is easily traced to a named function.*

**Anonymous Function Expression:**

{% highlight html %}
{% raw %}
  <script>
    var aFunc = function (decir) {
      console.log("anónimo");
      return decir;
    }
    //Can be invoked as follows
    aFunc("Vuelvo enseguida");
  </script>
{% endraw %}
{% endhighlight %}
*^^ Based on my experience, this is the most widely used.* 

**Also a Function Expression:** 

{% highlight html %}
{% raw %}
  <script>
    //This is a function expression.
    (function () {})

    //We may be more used to seeing it in this context
    _.each(collection, function(){})

  </script>
{% endraw %}
{% endhighlight %}
*^^Function Expressions like this one (which, on the surface look a lot like an anonymous function declaration) are, in fact, a common example of a function expression. As such, the hoisting characteristics are as follows:*

#### Hoisting Characteristics:
The variable declarations of function expressions are, in fact, hoisted to the top of the scope in which they are contained. This may sound similar to function declarations, but the important distinction is that the BODY of the function expression remains where it is defined. The variable declaration, in fact, is hoisted to the top of the scope (directly under any and all function declarations) and are set to a value of "undefined" until invoked. See below for an illustration: 

**Before:**
{% highlight html %}
{% raw %}
  <script>
    var chica = "bonita"; 
    chico("Buenas tardes");
    var chico = function(que) {
      return que;
    }
  </script> 
{% endraw %}
{% endhighlight %}

**After:** 
{% highlight html %}
{% raw %}
  <script>
    var chica = "bonita";
    var chico = undefined; 
    chico("Buenas tardes"); //returns [Type Error: chico is not a function];
    /*var chico = function(que) {
      return que;
    }*/
  </script> 
{% endraw %}
{% endhighlight %}
*^^Notice how the variable declaration is hoisted to the top of the scope and the function invocation doesn't invoke the function and doesn't return undefined. Rather, it validates the fact that chico is, in fact, completely decoupled from it's value (the function body).*

Thank you for reading and I hope this was helpful! 




