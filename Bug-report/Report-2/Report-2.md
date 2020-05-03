# JavaScript file discloses the hidden the admin-panel path

#### Description
In some cases, sensitive functionality is not robustly protected but is concealed by giving it a less predictable URL: so called security by obscurity. Merely hiding sensitive functionality does not provide effective access control since users might still discover the obfuscated URL in various ways.

For example, consider an application that hosts administrative functions at the following URL:

https://insecure-website.com/administrator-panel-yb556

This might not be directly guessable by an attacker. However, the application might still leak the URL to users. For example, the URL might be disclosed in JavaScript that constructs the user interface based on the user's role:

```
<script>
var isAdmin = false;
if (isAdmin) {
  ...
  var adminPanelTag = document.createElement('a');
  adminPanelTag.setAttribute('https://insecure-website.com/administrator-panel-yb556');
  adminPanelTag.innerText = 'Admin panel';
  ...
}
</script>
```

This script adds a link to the user's UI if they are an admin user. However, the script containing the URL is visible to all users regardless of their role. 

#### Steps to reproduce

1. Review the lab homepage's source using `view-source:` URI Scheme to put infront of URL.
2. Observe that it contains some JavaScript that discloses the URL of the admin panel.
3. Load the admin panel and delete `carlos.` 


#### Proof of conecpt

Attachments: 

1. admin-panel.png
2. view-source.png

#### Impact 

**An attacker can take-over administrator account and misuse the administrator privilege.**

* You can explain more about how an attacker can take advantage. like what an attacker can do and what type of damages could be possible against the 
  organization (reputational, financial damages)
  