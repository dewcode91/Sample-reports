# Information disclosure (robots.txt file disclose admin panel)

### Description
At its most basic, vertical privilege escalation arises where an application does not enforce any protection over sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might simply be able to access the administrative functions by browsing directly to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:

https://insecure-website.com/admin

This might in fact be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the robots.txt file:

https://insecure-website.com/robots.txt

Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality. 


### Steps to reproduce

1. Go to the lab and view `robots.txt` by appending `/robots.txt` to the lab URL.

2. Note that the disallow line identifies the path to the admin panel. 

3. In the URL bar replace `/robots.txt` with `/administrator-panel` to load the admin panel. 

4. Delete user carlos . 

### Proof of concept

Attachments : Lab_poc.png ,Lab_poc1.png

### Impact 

**An attacker can takeover administrator account and perform various actions**

* Write more about impact like what a attacker can do and what type of damages could be possible against organization (reputational,financial damages) 