# TryHackMe — HTTP in Detail

**Path:** Pre Security
**Date completed:** [13/05/2026]
**Room link:** [https://tryhackme.com/room/httpindetail]

---

## 🎯 What I Learned

- What HTTP is and the role it plays in web communication
- How HTTPS differs from HTTP and why encryption matters
- The structure of a URL and what each part means
- Common HTTP methods, status codes, and headers
- What cookies are and how they're used

## 🧠 In My Own Words

**HTTP (Hyper Text Transfer Protocol)** is the set of rules that governs how
web browsers and web servers communicate to transmit webpage data — it's the
underlying protocol that makes browsing possible.

**HTTPS** is the secure version of HTTP. It encrypts the data being
transmitted so that no one intercepting the traffic can read it (preventing
eavesdropping), and it also verifies that you're actually communicating with
the legitimate web server you intended to reach, not an impostor.

**A URL** is essentially the instruction for how to access a specific
resource on the internet. It breaks into distinct parts:
- **Scheme:** the protocol used, e.g. `http://` or `https://`
- **Host/Domain:** the actual website address, e.g. `example.com`
- **Port:** the specific port the server is listening on (often hidden by
  default, e.g. 80 for HTTP, 443 for HTTPS)
- **Path:** the specific resource/page location on the server, e.g. `/login`
- **Query string:** extra parameters passed in the URL, e.g. `?id=123`
- **Fragment:** a reference to a specific part of the page, e.g. `#section2`

**HTTP methods** define the type of action being requested:
- **GET:** retrieve data from the server
- **POST:** send data to the server (e.g. submitting a form)
- **PUT:** update/replace existing data on the server
- **DELETE:** remove data from the server

**Status codes** tell you the result of a request:
- **200** — OK, request succeeded
- **201** — Created, a new resource was successfully created
- **301 / 302** — Redirect, the resource has moved (permanently/temporarily)
- **404** — Not Found, the requested resource doesn't exist
- **401** — Unauthorized, authentication is required
- **500** — Internal Server Error, something went wrong on the server's side

**Headers** are extra pieces of information sent along with a request or
response, beyond just the core data — this can include things like the type
of content being sent, the browser being used, or authentication details.
Both requests and responses have their own common headers.

**Cookies** are small pieces of data stored on the user's computer by the
browser. The web server can request this stored data back on future
requests, which is how sites remember things like login sessions or
preferences between visits.

## 🛠️ Key Terms Introduced

- HTTP vs HTTPS
- URL structure: scheme, host, port, path, query string, fragment
- HTTP methods: GET, POST, PUT, DELETE
- Status codes: 200, 201, 301, 302, 401, 404, 500
- Request/response headers
- Cookies

## ❓ Questions I Had / Things to Revisit

- Want to look closer at specific header names (e.g. `User-Agent`,
  `Content-Type`, `Set-Cookie`) and what each one actually does in practice
- Curious how cookies get abused in real attacks (session hijacking, cookie
  theft) since this seems directly relevant to blue team/SOC work later
- Want to see real HTTP traffic in a tool like Burp Suite or browser dev
  tools to connect this theory to something visual

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through URL structure, methods, status codes, and cookies confidently. Header
specifics are the one area I'd want to brush up on before teaching it.

---

*HTTP knowledge feels directly useful for reading web/proxy logs later in SOC
work — status codes and methods show up constantly when spotting suspicious
web traffic (e.g. repeated 401s could indicate a brute-force attempt).*
