---
layout: post
title: Email validation using Javascript
permalink: /js-email-validation/
---


Javascript is very useful in validating user data. It can be a name, number, email, credit card number, password etc., 

![Email validation by simple javascript](/images/email-validation-javascript.svg)

Validating data as soon as the user starts to enter it is the trend these days. It is an interactive process that saves a lot of time wasted on debugging.


Here is a simple example to show how email validation works.
<div style="padding:40px; border: 1px dashed #777;margin: 1em;">
<span  id="check">Enter email</span><br />
<input type="text" name="email" onkeydown="validate(this.value);"> 
</div>
<script language="JavaScript">

var ev = /^([_a-zA-Z0-9-]+)(\.[_a-zA-Z0-9-]+)*@([a-zA-Z0-9-]+\.)+([a-zA-Z]{2,3})$/;
var x = document.getElementById("check");
function validate(email){
    if(!ev.test(email))
        {
            x.innerHTML	= "Not a valid email";
            x.style.color = "red"
        }
    else
        {
            x.innerHTML	= "Looks good!";
            x.style.color = "green"
        }
    }
</script>


I was searching for a simple code to make my form to provide instant error report. I found many in jQuery but none in simple javascript.

Finally, I came up with something close to what I was looking for. Then after furnishing it a bit, I came up with this.

{% highlight javascript %}
    var ev = /^([_a-zA-Z0-9-]+)(\.[_a-zA-Z0-9-]+)*@([a-zA-Z0-9-]+\.)+([a-zA-Z]{2,3})$/;
    var x = document.getElementById("check");
    
    function email_validate(email){
        if(!ev.test(email))
            {
                x.innerHTML	= "Not a valid email";
                x.style.color = "red"
            }
        else
            {
                x.innerHTML	= "Looks good!";
                x.style.color = "green"
            }
        }
{% endhighlight %}

Here, I'm checking the entered value with special characters. I still don't know how exactly does the series ```/^([_a-zA-Z0-9-]+)(\.[_a-zA-Z0-9-]+)*@([a-zA-Z0-9-]+\.)+([a-zA-Z]{2,3})$/``` works.

I believe that it takes data in 4 parts. 

1. Data before ``@``
2. Data after ``@``
3. Data before ``.``
4. Data after ``.``

But data after **@** and before **.** is same. So 3 parts.

1. Data before ``@`` : Either numbers or characters
2. Middle data : Either numbers or characters 
3. Data after ``.`` : Either numbers or characters (at least two digits)

I guess that's how it is. I can be wrong here. The test() method tests for a match in a string. So in the if condition, if any character doesn't match with above 3 conditions then it throws an error.

If I were to code this all by myself, then I would have used 3 or more if conditions. It is good to see that we can do it in very few lines of code.

This code clearly explains how you can modify DOM on condition. I'm changing the text in the span tag along with color. This kind of makes sure user enters the right email.

Full HTML code

{% highlight html %}
<html>
    <body>
        <div style="padding:40px; border: 1px dashed #777;margin: 1em;">
            <span  id="check">Enter email</span><br />
            <input type="text" name="email" onkeydown="validate(this.value);"> 
        </div>


        <script language="JavaScript">
            var ev = /^([_a-zA-Z0-9-]+)(\.[_a-zA-Z0-9-]+)*@([a-zA-Z0-9-]+\.)+([a-zA-Z]{2,3})$/;
            var x = document.getElementById("check");
            function validate(email){
            if(!ev.test(email))
                {
                    x.innerHTML	= "Not a valid email";
                    x.style.color = "red"
                }
            else
                {
                    x.innerHTML	= "Looks good!";
                    x.style.color = "green"
                }
            }
        </script>
    </body>
</html>
{% endhighlight %}

In the input field, use ``onkeypress`` or ``onkeyup`` to validate on entering a character.

1. onkeydown: Happens as soon as you press a key.
2. onkeyup: Happens as soon as you leave a pressed key.
3. onkeypress: Happens on typing a character.

I'm using keydown because it happens sooner than the other two.


Thanks for reading!