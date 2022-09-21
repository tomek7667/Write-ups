# Task

AUTHOR: MADSTACKS

Description
Who doesn't love cookies? Try to figure out the best one. http://mercury.picoctf.net:17781/

---

# Write up

When clicking to search for a cookie (after entering `snickerdoodle`) we are redirected to the `/check` URL and then a POST request to `/search` is sent.
The first GET `/check` is sent with `Cookie: name=0` and POST `/search` is sent with `Cookie: name=-1` and body `name=snickerdoodle`.

When modifying a request cookie to `Cookie: name=1` in Burp repeater in GET `/check` request (POST is redirecting to it), we get a response `I love chocolate chip cookies!` so I assume the name determines which cookie name we get.

The best way to solve this quickly is to send the request to _Intruder_ and try to brute force the cookie.
I set up a simple payload, with the _Numbers_ type and entered a range from -5 to 105 with step 1, and `min/max fraction digits` to 0.
I started the attack and quickly after I noticed some responses with status code of `302` with `Set-cookie: session=eyJ...` which gave me a hint that it's a JWT token which I decoded at `jwt.io` and message inside was `"That doesn't appear to be a valid cookie."`. So I only looked at the responses with status 200. Each _non-flag_ response contains `Not very special though.` string which I entered to a filter to verify quickly whether it's a flag response.

The 18th one didn't have any matches with the query, so I rendered the response and the flag was in the body:

```html
<code>picoCTF{3v3ry1_l0v3s_c00k135_bb3b3535}</code>
```
