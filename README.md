# Pico-CTF-crack-the-gate-1-web-Exoitation-walkThrough
# picoCTF - Developer Header Bypass

## Challenge Type

Web Exploitation

---

## Objective

Gain access to a protected endpoint and retrieve the flag.

---

## What We Did

### Step 1: Inspect the Website

Viewed the page source.

Found a hidden comment:

<!-- ABGR: Wnpx - grzcbenel olcnff: hfr urnqre "K-Qri-Npprff: lrf" -->

This indicated hidden information was stored in the source code.

---

### Step 2: Decode the Message

Challenge hint:

"A common trick is to rotate each letter by 13 positions."

This means ROT13.

Decoded message:

NOTE: Jack - temporary bypass: use header "X-Dev-Access: yes"

---

### Step 3: Understand the Clue

The developer left a note saying:

Use header:

X-Dev-Access: yes

This suggested the application might trust a special HTTP header.

---

### Step 4: Use Burp Suite

Opened Burp Suite Repeater.

Captured the login request.

Original response:

401 Unauthorized

Meaning access was denied.

---

### Step 5: Modify the Request

Added:

X-Dev-Access: yes

to the request headers.

Sent the request again.

---

### Step 6: Observe the Response

Response changed from:

401 Unauthorized

to:

200 OK

The server returned the flag.

---

## Flag

picoCTF{brut4_f0rc4_3e21b3a3}

---

# What We Learned

## 1. Source Code Inspection

Always inspect:

* HTML
* CSS
* JavaScript
* Comments

Developers often leave clues there.

---

## 2. ROT13 Encoding

ROT13 shifts every letter by 13 positions.

Example:

hello → uryyb

Common in CTFs.

---

## 3. HTTP Requests

Every request contains:

* Method (GET, POST)
* URL
* Headers
* Body

Example:

POST /login

Headers:
User-Agent
Cookie
Authorization
X-Dev-Access

Body:
email
password

---

## 4. HTTP Headers

Headers provide extra information to the server.

Example:

Cookie: session=123

Authorization: Bearer token

X-Dev-Access: yes

Applications sometimes make decisions based on headers.

---

## 5. Burp Suite Repeater

Used to:

* Modify requests
* Add headers
* Change parameters
* Test responses

One of the most important web pentesting tools.

---

## 6. HTTP Status Codes

200 = Success

401 = Unauthorized

403 = Forbidden

404 = Not Found

500 = Internal Server Error

Status codes help identify what is happening.

---

## 7. Developer Backdoors

Developers sometimes leave:

* Debug pages
* Test accounts
* Hidden endpoints
* Secret headers
* Admin bypasses

These can become vulnerabilities.

---

## Important Lesson

Just because we add:

X-Dev-Access: yes

does NOT mean every website will grant access.

It worked because the application was specifically programmed to trust that header.

The real skill is:

Find clues → Understand them → Test them → Observe the response

---

# CTF Workflow Learned

1. Read hints.
2. Inspect source code.
3. Search for comments.
4. Decode strange strings.
5. Use Burp Suite.
6. Analyze requests.
7. Modify headers/parameters.
8. Compare responses.
9. Identify the vulnerability.
10. Capture the flag.

---

# Key Takeaway

Web CTFs are often solved by:

Inspect → Decode → Modify → Observe

not by randomly attacking the application.
