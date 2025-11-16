## 🌐 HTTP Analysis

## 🧠 What is HTTP?

HTTP (HyperText Transfer Protocol) is an application-layer protocol used for communication between web clients (browsers) and web servers.
It is:
Stateless
Text-based
Works over TCP (usually port 80)
Foundation for websites and REST APIs
Often replaced by HTTPS (encrypted) but still widely used


## ⚙️ Capture Setup

To generate DNS traffic for analysis:

1. Start capturing on the main network interface
2. Visit any http website (http://neverssl.com)


## 🔍 HTTP Request Analysis

- **Request Line:**  GET /online HTTP/1.1\r\n
- **Host:**  soothingsplendidrelaxedsecret.neverssl.com
- **User-Agent:**  Mozilla/5.0
- **Accept:**  text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8
- **Connection:**  keep-alive\r\n


## 📤 HTTP Response Analysis

-**Status Line:**  HTTP/1.1 200 OK\r\n
-**Response Version:**  HTTP/1.1
-**Server:**  Apache/2.4.62
-**Content-Type:**  text/html; charset=UTF-8


## 🔄 Common HTTP Methods Observed
|  Method	|  Purpose  |
| GET	    | Retrieve resource
| POST	    | Send data (forms, login, API)
| HEAD	    | Like GET but header only
| PUT       | Upload/replace resource
| DELETE    | Remove resource


## 🔧 Useful Wireshark Filters
- http
- http.request
- http.response
- http.request.method == "POST"
- tcp.port == 80
- http contains "password"

## Conclusion
In this HTTP analysis, I inspected HTTP requests and responses, including headers, cookies, and message bodies. I observed how clients fetch resources using GET and send data using POST. The analysis also highlighted the security risks of using HTTP, as sensitive information like cookies and credentials can be easily captured.
