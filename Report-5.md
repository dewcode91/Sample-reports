# Open redirect can lead to cross site scripting

#### Description
The application main functionality is allows a user to select a choice based course and provide online study material. While testing this workflow I noticed when a user clicks on `view course`, the application redirects it to an external website. as you can see in URL https://insecure-website.com/resources/course/redirect?destUrl=payload, `destURL` parameter is responsible for redirection. While this is an open redirection, an attacker can abuse this behavior and able to redirect users to any website.   

#### Steps to Reproduce

1. Login to your account.
2. Click on resources > onlinecourses. 
3. Select a course and click on `View Course` 
4. Now you are redirected to tutorial website(before redirection copy the link from address bar)
5. Append a payload `javascript:alert(document.cookie)` in `destURL` parameter. 
6. Now you can see a pop on your screen.

#### Impact 
This vulnerability allows an attacker to inject and execute arbitrary script code within the context of a user's web browser. This malicious script code can be used to steal sensitive user information, perform phishing attacks, or even gain unauthorised access to the user's account.
