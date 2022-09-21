# Task

AUTHOR: MADSTACKS

Description
Find the flag being held on this server to get ahead of the competition http://mercury.picoctf.net:21939/

---

# Write up

On the site there are only two buttons `Choose Red` and `Choose Blue`. When clicking first one we are sending a _GET_ request and when clicking the second we are sending an empty _POST_. The name of the task suggest to send a _HEAD_ request. When we do so, we get such a response:

```
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
Content-type: text/html; charset=UTF-8
```

With the flag inside.
