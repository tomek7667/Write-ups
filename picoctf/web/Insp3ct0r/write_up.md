# Task

AUTHOR: ZARATEC/DANNY

Description
Kishor Balan tipped us off that the following code may need inspection: https://jupiter.challenges.picoctf.org/problem/41511/ (link) or http://jupiter.challenges.picoctf.org:41511

---

# Write up

After entering the website `CTRL + u` to view the source code and we get the following:

```html
<p>
  I used these to make this site: <br />
  HTML <br />
  CSS <br />
  JS (JavaScript)
</p>
<!-- Html is neat. Anyways have 1/3 of the flag: picoCTF{tru3_d3 -->
```

After going into `mycss.css`:

```css
/* You need CSS to make pretty pages. Here's part 2/3 of the flag: t3ct1ve_0r_ju5t */
```

and finally into `myjs.js`:

```js
/* Javascript sure is neat. Anyways part 3/3 of the flag: _lucky?832b0699} */
```

So the flag is `picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?832b0699}`
