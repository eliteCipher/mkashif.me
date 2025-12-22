---
title: "Advent of Cyber 2025 | Challenge: Splunk Basics – Did You SIEM?"
tags: ["splunk", "siem", "log analysis", "soc"]
style:
color:
image: "/assets/images/post_3/AOC.jpeg"
description: "Lessons learned from Advent of Cyber 2025 Splunk log analysis challenge"
permalink: Advent-of-Cyber-2025-Splunk-Did-You-SIEM
---

{% include elements/figure.html image="/assets/images/post_3/AOC.jpeg" caption='Investigating logs using Splunk' %}

> _**“Logs don’t lie — but they do hide.”**_

Before alerts, before dashboards, before incident calls —  
there are **logs**.

A **SIEM (Security Information and Event Management)** tool is where all those logs come together.  
It ingests data from web servers, firewalls, endpoints, and applications, allowing security teams to **search, correlate, and investigate events** across the environment.

In this challenge, that SIEM is **Splunk** — one of the most widely used tools in modern SOCs.

---

### Scenario: Something Went Wrong…

TryHackMe’s **Advent of Cyber 2025** drops us straight into a real-world situation.

A company’s environment has started behaving strangely:
- Unusual web traffic
- Suspicious activity patterns
- Signs of an active attack

---

### Getting Started with Splunk

#### Anomaly Detection

To see the spike in the **web traffic**:

{% highlight shell %}
index=main sourcetype=web_traffic 
| timechart span=1d count
{% endhighlight %}
The **timechart** command gives us the visibility into web traffic on a daily basis.

{% include elements/figure.html image="/assets/images/aoc3/timechart.png" caption='Timechart command' %}

This helps identify peak activity days, often correlating directly with attacker behavior.

Now, it's time to dive deep into the interesting fields in web traffic logs:
- client_ip 
- user_agent
- path


##### Hacker's IP
High-frequency IPs with unusual user agents are often the attacker.

{% include elements/figure.html image="/assets/images/aoc3/ip.png" caption='Client IP' %}

To find the most active IPs:

{% highlight shell %}
index=main sourcetype=web_traffic 
index=main sourcetype=web_traffic
| stats count by client_ip
| sort -count
{% endhighlight %}



##### User Agents

High-frequency IPs with unusual user agents are often the attacker.
{% include elements/figure.html image="/assets/images/aoc3/ua.png" caption='Client IP' %}


{% highlight shell %}
index=main sourcetype=web_traffic
| search user_agent!="*Mozilla*" user_agent!="*Chrome*"
{% endhighlight %}

##### Path
The third field we will examine is path, which contains the URI being requested and accessed by the client IPs. The results shown below clearly indicate some attacks worth investigating.

{% include elements/figure.html image="/assets/images/aoc3/path.png" caption='Path' %}
