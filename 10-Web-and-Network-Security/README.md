# Module 10 — Web and Network Security

## Learning Objectives

- Understand HTTP and HTTPS
- Explain TLS fundamentals
- Read HTTP requests and responses
- Know HTTP methods and status codes
- Understand basic encryption concepts

---

## HTTP vs HTTPS

| | HTTP | HTTPS |
|---|------|-------|
| Port | 80 | 443 |
| Encryption | None — plaintext | TLS encrypted |
| Security | Vulnerable to interception | Traffic is protected |

---

## TLS — Transport Layer Security

TLS provides three things:

| Property | Meaning |
|----------|---------|
| Confidentiality | Data is encrypted, cannot be read by third parties |
| Integrity | Data cannot be modified in transit without detection |
| Authentication | The server proves its identity via a certificate |

---

## HTTP Request

```
GET /index.html HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: text/html
```

## HTTP Response

```
HTTP/1.1 200 OK
Content-Type: text/html

<html>...</html>
```

---

## HTTP Methods

| Method | Purpose |
|--------|---------|
| GET | Retrieve a resource |
| POST | Submit data (forms, logins) |
| PUT | Update a resource |
| DELETE | Delete a resource |
| OPTIONS | Ask what methods are supported |

---

## HTTP Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK — success |
| 301 | Moved Permanently |
| 302 | Temporary redirect |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Certificates

A TLS certificate proves a server's identity. Issued by a Certificate Authority (CA).

The certificate contains: domain name, public key, issuing CA, expiry date, digital signature.

When your browser shows the padlock, it has verified the certificate is valid and matches the domain.

---

## Cybersecurity Relevance

- HTTP sends passwords in plaintext — easily captured with Wireshark
- HTTPS protects data in transit but not on the server
- Expired or self-signed certificates are a warning sign
- Status codes reveal application behaviour: 403 = endpoint exists, access denied
- TLS downgrade attacks force weaker encryption

---

## Quick Revision

1. HTTP = plaintext, port 80
2. HTTPS = encrypted, port 443
3. TLS = confidentiality + integrity + authentication
4. 200 = OK, 403 = Forbidden, 404 = Not Found, 500 = Server Error
5. Certificate = server identity proof from a trusted CA

---

## Practice Questions

1. What is the difference between HTTP and HTTPS?
2. Which HTTP method submits a login form?
3. What does a 403 status code mean?
4. What three properties does TLS provide?
5. Why is HTTP dangerous on public Wi-Fi?
