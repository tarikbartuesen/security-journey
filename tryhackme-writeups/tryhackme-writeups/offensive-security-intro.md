# Offensive Security Intro

**Date:** 2026-07-22
**Difficulty:** Easy
**Category:** Web Security / Broken Access Control
**Platform:** TryHackMe

## Summary
This room focused on discovering hidden directories on a fake banking website 
and exploiting a broken access control vulnerability to access a sensitive 
money transfer function without authentication.
## Tools Used
- Dirb (directory brute-forcing)

## Methodology

### 1. Directory Enumeration
Ran a directory brute-force scan against the target to discover hidden or 
undocumented paths:

dirb http://fakebank.thm

The scan returned two results:
- `/bank-transfer` (CODE:200) — a page returning a successful response, 
  meaning it was directly accessible
- `/images` (CODE:301) — a redirect, less relevant to this scenario

### 2. Exploiting Broken Access Control
The `/bank-transfer` page was expected to require a logged-in session, since 
it exposes a money transfer function. However, navigating directly to 
`http://fakebank.thm/bank-transfer` granted immediate access without any 
authentication check.

### 3. Abusing the Functionality
With direct access to the transfer page, I was able to initiate a fund 
transfer without ever logging in or proving identity — demonstrating how a 
missing access control check on a sensitive endpoint can be abused.

## Key Takeaways
- Hidden or "unlinked" pages are not a substitute for real access control — 
  if a URL isn't protected server-side, anyone who finds it (e.g. via 
  directory brute-forcing) can use it.
- Directory brute-forcing tools like `dirb` are a standard first step in 
  web app assessments, since they reveal endpoints not visible through 
  normal navigation.
- Sensitive functionality (like financial transactions) should always 
  enforce authentication and authorization checks server-side, regardless 
  of whether the URL is publicly linked.

## Reflection
This room was a clear demonstration of Broken Access Control (OWASP Top 10 
category). It helped me understand that "security through obscurity" 
(hiding a page instead of protecting it) is not real security. I want to 
explore this category further, especially IDOR (Insecure Direct Object 
Reference) vulnerabilities, which follow a similar logic but involve 
manipulating identifiers rather than finding hidden paths.
