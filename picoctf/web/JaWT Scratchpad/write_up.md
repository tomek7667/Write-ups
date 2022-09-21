# Task

AUTHOR: JOHN HAMMOND

Internal server errors can be intentionally returned by this challenge. If you experience one, try clearing your cookies.

Description
Check the admin scratchpad! https://jupiter.challenges.picoctf.org/problem/63090/ or http://jupiter.challenges.picoctf.org:63090

---

# Write up

After entering the website and entering `john` we are sending a POST request with body `user=john`. It returns a response with a cookie `session=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW5cdTAwMDAifQ.YOiibGfMeXuW4imGtbeL5AZ-fC3NZgwfmAE4NoDY9YI` which is a JWT token. I decoded it at `jwt.io` and got the following:

```json
{
  "user": "John"
}
```

and the signature is verified with algorithm `HS256` (which is short form of HMAC-SHA256).

Now we are getting our scratchpad and a logout button below. After using it to log: POST with `user=admin`
we are getting the following message on the site:

`YOU CANNOT LOGIN AS THE ADMIN! HE IS SPECIAL AND YOU ARE NOT.`

When I entered `admin%00` (which is `admin` with a null byte at the end) as a username, however the data in JWT:

```json
{
  "user": "admin\u0000"
}
```

is not exactly `admin` but the website loaded with

```html
<h2>Hello admin!</h2>
```

But this was a rabbit hole.

The clear hint of what to do was on the page:

` use a short and cool one like John!` which had a link to the github of a cracking tool called (JohnTheRipper)[https://github.com/magnumripper/JohnTheRipper].

I used it to crack the JWT secret with `rockyou.txt` wordlist with a following command (On VMWare with Kali Linux image):

```bash
john jwt.txt --wordlist=/usr/share/wordlists/rockyou.txt --format=HMAC-SHA256
```

We got the secret of jwt: `ilovepico`

Now we can forge our token (in jwt.io) with the secret `ilovepico` and get the following:
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiYWRtaW4ifQ.di2J1a0H3IhZtGmIfw7ltVq7sZL2orh8WIP1isDkgdw`
When we visit the site with this cookie, we will get the flag in the scratchpad:

```
picoCTF{jawt_was_just_what_you_thought_f859ab2f}
```
