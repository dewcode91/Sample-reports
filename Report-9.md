# XSS in search parameter

#### Description

I have found a Cross-Site Scripting vulnerability in search query https://www.example.com/search?q=[payload], by injecting malicious JavaScript code through the search parameter, an attacker can exploit this vulnerability to execute arbitrary code in the context of other users' browsers. This could potentially lead to various malicious activities, such as session hijacking, defacement, or phishing attacks.

#### Steps to reproduce

1. Visit https://www.example.com/search?q=%27-alert%28document.domain%29-%27.
2. Now you can see pop on screen.

#### Impact

The XSS vulnerability in the search parameter could allow an attacker to compromise user accounts, steal sensitive information, or perform actions on behalf of other users. This can lead to severe reputational damage, loss of user trust, and potential legal implications.
