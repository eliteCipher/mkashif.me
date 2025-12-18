---
title: "Advent of Cyber 2025 | Challenge 1: Linux CLI Shell Bells"
tags: ["shell", "linux"]
style:
color:
image: "/assets/images/post_3/AOC.jpeg"
description: "Lessons Learned from AOC 2025 Challenge 1"
permalink: Advent-of-Cyber-2025-Challenge1
---

{% include elements/figure.html image="/assets/images/post_3/AOC.jpeg" caption='Malware Detected' %}

> _**“In Linux we trust; in GUI we adjust.”**_ 

TryHackMe's Advent of Cyber kicked off, and it's the perfect time to start discussing the challenges.

The very first challenge, “Shells Bells”, focuses on the basics of CLI commands — super helpful for anyone who still has a bit of Linuxophobia 👀🐧:

To **jump into a directory**, simply use
{% highlight shell %}
cd [folder_name]
{% endhighlight %}


Want to **look what's inside the folder**: 
{% highlight shell %}
ls
{% endhighlight %}
It will list everything in your current dirctory.
But wait... something is hidden? Spill the beans by using: 
{% highlight shell %}
ls -la
{% endhighlight %}

There you go, found a hidden secret? **Read** it using:
{% highlight shell %}
cat secret.txt
{% endhighlight %}

## Now let's use these commands to perform some basic investigation:

{% highlight shell %}
cd /var/log/
{% endhighlight %}
– The magical land where all your system’s drama is stored.

{% highlight shell %}
grep "Failed password" auth.log
{% endhighlight %}
– Finds failed login attempts. Spoiler: there will be many.

{% highlight shell %}
find /home/socmas -name *egg* 
{% endhighlight %}
– Search for files like you're hunting Easter eggs, but far less fun.


## Special Symbols
**Pipe symbol (|)**	Send the output from the first command to the second
{% highlight shell %}
cat unordered-list.txt | sort | uniq
{% endhighlight %}


**Output redirect (>/>>)**	Use > to overwrite a file, and >> to append to the end	
{% highlight shell %}
some-long-command > /home/mcskidy/output.txt
{% endhighlight %}


**Double ampersand (&&)**	Run the second command if the first was successful	
{% highlight shell %}
grep "secret" message.txt && echo "Secret found!"
{% endhighlight %}

