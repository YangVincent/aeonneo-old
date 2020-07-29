---
title: Lecture 2
---
# What happens when you type a URL and press enter?

### [[DNS]] (Domain Name Server)
* We ping the Root Nameserver returns a list of authoritative name servers for the TLD.
* TLD goes from ".edu" to "go to stanford".
* The final server is the **Authoritative name server**

#### DNS Hijacking Vectors
* Malware changes user's local DNS settings `/etc/hosts`
* Hacked recursive DNS resolver
* Hacked router
* Hacked DNS nameserver
* Compromised user account at DNS provider
* This can get past https, since they can act like the actual server. Letsencrypt will give you a cert if you can prove that you own a domain.
* ISP's used to point to their own pages with their ads if a page didn't exist. Comcast, TMobile both do this. [Example](http://lookup.t-mobile.com/search/?q=http://questionablecontent.net)

#### DNS Privacy
* Queries are in plaintext; ISPs have been known to sell this data.
* Cloudflare `1.1.1.1` or another providers have better privacy policies. Unfortunately, ISPs can still see this, cause they can see that you're sending to cloudflare. The solution is DNS-over-HTTPS (default on Firefox; flag-blocked in Chrome via `chrome://flags/#dns-over-https`). You can also set this at the router level.

### When you get IP address
* Send http request, receive response from the given server

### Anatomy of an HTTP Request
* Method (GET/POST/PUT)
* Path (/)
* Protocol (HTTP/1.1)
* Example: `GET / HTTP/1.1`

### Anatomy of an HTTP Response
```
HTTP/1.1 200 OK
Content-Length: 9001
Content-Type: text/html; charset=UTF-8
Date: Tue, 24 Sep 2019 20:30:00 GMT

<!DOCTYPE html ...
```
* Protocol Version
* Status Code
* Status Message

#### Useful Headers
* Host: Domain name
* User-Agent: Name of browser & OS
* Referer: webpage that led you to this one
* Cookie: Cookie the server gave you
* Range: Subset of bytes to fetch
* Cache-Control: Do you want a cached response?
* If-Modified-Since: Only load response if modified recently
* Connection: Control TCP socket (`keep-alive` or `close`)
* Accept: What type of content we want (ex: `text/html`)
* Accept-Encoding: Encoding algs we understand (ex: `gzip`)
* Accept-Language: What language we want

### HTTP Protocol
* Extensible: Just add HTTP headers to add new features
* Stateless: Two requests have no relation to each other
* Transport protocol agnostic: The only requirement is reliability (doesn't have to be TCP)
* Proxy servers can be used to let multiple servers seem as a single server (Client -> Proxy -> One of many serverns)

### Status Codes
* 1xx: Informational
* 2xx: Success
* 3xx: Redirection
* 4xx: User messed up
* 5xx: Server messed up

### Layers of the internet
1. HTML/CSS/JS
2. HTTP
3. TLS
4. TCP
5. IP

### Cookies
Cookie: theme=dark; (Header name, cookie name, cookie value)
