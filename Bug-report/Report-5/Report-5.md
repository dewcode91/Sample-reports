# Open redirect can lead to stealing the user session cookie 

#### Description
Open redirection vulnerabilities arise when an application incorporates user-controllable data into the target of a redirection in an unsafe way. An attacker can construct a URL within the application that causes a redirection to an arbitrary external domain. This behavior can be leveraged to facilitate phishing attacks against users of the application. The ability to use an authentic application URL, targeting the correct domain and with a valid SSL certificate (if SSL is used), lends credibility to the phishing attack because many users, even if they verify these features, will not notice the subsequent redirection to a different domain.

The application main functionality is to allows a user to select a choice based course and provide online study material. While testing this workflow I noticed when a user clicks on `view course`, the application redirects it to an external website. as you can see in URL https://insecure-website.com/resources/course/redirect?destUrl=payload, `destURL` parameter is responsible for redirection. While this is an open redirection, An attacker can abuse this behavior and able to redirect users at any websites.    

#### Steps to reproduce

1. Login to your account.
2. Click on resources > onlinecourses. 
3. Select a course and click on `View Course` 
4. Now you are redirected to tutorial website.
5. Before redirection copy the link from address bar.
6. Append a payload `javascript:alert(document.cookie)` in `destURL` parameter. 
7. Now you can see a pop on your screen.

#### Proof of concept

Video link https://vimeo.com/000000000

#### Impact 

**An attacker can redirect a user to a malicious website and able to run javascript on victim's browser and steal victim's session cookies.**
