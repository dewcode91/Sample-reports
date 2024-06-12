# Unprotected admin functionality (robots.txt file disclose admin panel)

#### Description
At its most basic, vertical privilege escalation arises where an application does not enforce any protection over sensitive functionality. For example, administrative functions might be linked from an administrator's welcome page but not from a user's welcome page. However, a user might simply be able to access the administrative functions by browsing directly to the relevant admin URL.

For example, a website might host sensitive functionality at the following URL:

https://insecure-website.com/admin

This might in fact be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the robots.txt file:

https://insecure-website.com/robots.txt

Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality. 


#### Steps to Reproduce

1. Go to the lab and view `robots.txt` by appending `/robots.txt` to the lab URL.
2. Note that the disallow line identifies the path to the admin panel. 
3. In the URL bar replace `/robots.txt` with `/administrator-panel` to load the admin panel. 
4. Delete user `carlos`. 

#### Impact 

By gaining access to admin functionality, a low privilege user can perform actions that are typically restricted to administrators or privileged users. This could include modifying or deleting sensitive data, altering system configurations, or creating new user accounts with elevated privileges.
