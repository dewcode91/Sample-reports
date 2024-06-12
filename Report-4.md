# Broken access control can lead to access of admin's account

#### Description
Some applications enforce access controls at the platform layer by restricting access to specific URLs and HTTP methods based on the user's role. For example an application might configure rules like the following:

DENY: POST,` /admin/deleteUser`, managers

This rule denies access to the POST method on the URL `/admin/deleteUser`, for users in the managers group. Various things can go wrong in this situation, leading to access control bypasses.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as `X-Original-URL` and `X-Rewrite-URL`. If a web site uses rigorous front-end controls to restrict access based on URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following:
```
POST / HTTP/1.1
X-Original-URL: /admin/deleteUser
You can see a full HTTP request can sent by an attcaker in-order to exploit the vulnurbility
```
```
GET /delete?username=carlos HTTP/1.1
Host: ac881fc61f2d6d3f80166598000a0060.web-security-academy.net
X-Original-URL: /admin
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:75.0) Gecko/20100101 Firefox/75.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://ac881fc61f2d6d3f80166598000a0060.web-security-academy.net/
Connection: close
Cookie: session=PZEti039Ndjxfya2anDNigFiMWv78pdZ
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0

```

#### Steps to Reproduce

1. Try to load `/admin` and observe that you get blocked. 
2. Observe that the response is very plain, suggesting it may originate from a front-end system. 
3. Send the request to Burp Repeater. Change the URL in the request line to `/` and add the HTTP header `X-Original-URL: /invalid`.        Observe that theapplication returns a "not found" response. This indicates that the back-end system is processing the URL from the `X  Original-URL` header. 
4. Change the value of the `X-Original-URL` header to `/admin`. Observe that you can now access the admin page. 
5. To delete the user carlos, add `?username=carlos` to the real query string, and change the `X-Original-URL` path to `/admin/delete`.

#### Impact 

Inexperienced or malicious users who access admin functionalities can unintentionally or intentionally make changes that destabilize the system. They may delete critical files, misconfigure settings, or introduce malicious code, resulting in system crashes, performance degradation, or even the complete loss of data.
