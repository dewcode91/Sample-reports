## Unauthorised user's can access admin panel 

#### Description

Some applications determine the user's access rights or role at login, and then store this information in a user-controllable location, such as a hidden field, cookie, or preset query string parameter. The application makes subsequent access control decisions based on the submitted value. For example:

https://insecure-website.com/login/home.jsp?admin=true

https://insecure-website.com/login/home.jsp?role=1

This approach is fundamentally insecure because a user can simply modify the value and gain access to functionality to which they are not authorized, such as administrative functions. You can observe `Admin=false` parameter at cookie header below in HTTP request. 

```
GET /admin HTTP/1.1
Host: ac961f1c1ef4adef80bd6a6c0000006c.web-security-academy.net
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:75.0) Gecko/20100101 Firefox/75.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://ac961f1c1ef4adef80bd6a6c0000006c.web-security-academy.net/login
Connection: close
Cookie: session=DOOAJa8Mkf2EDu4mLoLImfnDaP5My8yS; Admin=false
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
```


#### Steps to reproduce

1. Browse to `/admin` and observe that you can't access the admin panel. 
2. Browse to the login page. 
3. In Burp Proxy, turn interception on and enable response interception.
4. Complete and submit the login page, and forward the resulting request in Burp. 
5. Observe that the response sets the cookie `Admin=false` Change it to `Admin=true` 
6. Load the admin panel and delete `carlos.` 


#### Impact 

The low privilege user might identify and exploit vulnerabilities in the admin functionality, leading to further compromise of the system. They may use this access to escalate their privileges, execute arbitrary code, or launch additional attacks against other users or systems
