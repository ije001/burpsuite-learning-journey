**Burp Suite Learning Journey & Bottlenecks - Project Documentation**

**Author: Ijeoma | Date: August 2026 | Status: Work in Progress (30+ PortSwigger Labs Completed)**

**Executive Summary**

Over the past weeks, I've extensively used Burp Suite Community Edition for web application security testing, specifically focusing on SQL injection exploitation. This document outlines my learning journey, critical issues encountered, solutions implemented, and key takeaways for future reference.

1. Initial Setup & Configuration Challenges

1.1 Proxy Configuration Issues

Problem: Firefox wouldn't connect to Burp Suite even when proxy was configured.

Root Cause: Burp Suite wasn't running when Firefox tried to use the proxy.

Solution:

**•**	Always START Burp Suite FIRST before enabling proxy in Firefox

**•**	Understand the workflow: Burp running → Configure proxy → Browse

Timeline:

**•**	First attempt: Proxy configured, Burp not running → Connection refused

**•**	Second attempt: Burp running + proxy configured → Works

Learning: Tool orchestration matters - the order of operations is critical.

1.2 SSL Certificate Error

Problem: "Software is preventing Firefox from safely connecting to this site" error on PortSwigger labs.

Root Cause: Burp Suite intercepts HTTPS traffic and creates its own SSL certificates. Firefox doesn't trust Burp's CA certificate by default.

Solution:

**•**	Download Burp's CA certificate from http\://burpsuite (when proxy is configured)

**•**	Import it into Firefox → Settings → Network Settings → View Certificates → Authorities → Import

**•**	Enable "Trust this CA to identify websites"

Impact: Without this, HTTPS sites couldn't be accessed through Burp.

1.3 FoxyProxy Extension Setup

Problem: Constantly enabling/disabling manual proxy settings was tedious and error-prone.

Solution: Install FoxyProxy Standard extension

**•**	Create proxy profile: "Burp Suite" (127.0.0.1:8080)

**•**	One-click toggle between "Burp Suite" and "Disabled"

Benefit: Professional workflow - switch seamlessly between Burp testing and normal browsing.

2. Understanding Burp Suite's Core Concepts

2.1 Intercept ON vs OFF - Critical Distinction

Initial Confusion:

**•**	Thought Intercept must be ON to capture traffic

**•**	Pages would freeze/timeout when Intercept was ON

Correct Understanding:

Setting Behavior Use Case

Intercept ON BLOCKS every request, waits for manual forward When you need to modify request BEFORE sending

Intercept OFF Requests flow normally, still captured in history 99% of labs - normal browsing with capture

Professional Workflow:

**1.**	Set Intercept to OFF (default)

**2.**	Browse normally to the vulnerable feature

**3.**	Go to Proxy → HTTP History

**4.**	Find the request you need

**5.**	Right-click → Send to Repeater

**6.**	Modify in Repeater tab

**7.**	Test payloads

Why This Matters: Early on, I wasted ~30 minutes with Intercept ON, wondering why nothing was loading. Flipping to OFF instantly solved it.

## Key Takeaways

- Tool orchestration matters — always start Burp before enabling the proxy
- SSL certificate trust is foundational to HTTPS interception, understand it once, never troubleshoot it again
- Intercept OFF is your default state — HTTP History is where the real work happens
- FoxyProxy transforms Burp from frustrating to seamless —install it immediately
- 30+ PortSwigger labs completed — every bottleneck encountered was a lesson that stuck
