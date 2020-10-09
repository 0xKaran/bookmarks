# FILE UPLOAD VULNERABILITY
File upload is actually not a vulnerability but a functionality in a website.<br>
We are hackers, and what we do? Exploit every functionality.😀<br>
That's why this post is dedicated to all types, techniques and ways to exploit the functionality to gain unauthorised access to the server.

Reconnaissance and find which server software is running on the backend.<br>
Upload `.asp` or `.aspx` shell for Windows server. <br>
Upload `.php` for Linux server.

## Unrestricted file upload:
If the server is poorly configured and allow every file to be uploaded and don't have security implementations like filters and WAFs, You can simply upload any file including web shells.

## File Extension Check Bypass:
  - If server is checking file extension. <br>
    Rename file name. For eg.: `evil-file.php` ---> `evil-file.php.jpeg` <br>
    If modified file doesn't work, add null char `%00` to bypass last extension, in this example `.jpeg` <br>
    So it would look like this `evil-file.php%00.jpeg` <br>
    Null Byte/Char is like an end point and says there is nothing after me, I'm the last and I'm nothing. LOL <br>
    
  - Use `?`, `#`, or `.`, At the end of the main file and before spoofed extension. <br>
    for eg.: `https://example.com/evil-file.php` --> `https://example.com/evil-file.php?.svg`

## JavaScript Bypass:
Some websites perform validation on the client side via JavaScript. <br>
Just disable Javascript on the browser.

  - To disable JS on Firefox:
  	  - Open Firefox,
  	  - In the address bar, type `about:config` and press Enter,
  	  - Click the Accept the Risk and Continue button in the center of the screen,
  	  - In the Search preference name text field, type `javascript.enabled`,
  	  - For the javascript.enabled search result, click the Toggle Firefox toggle for JavaScript icon on the far right. The true value changes to false to indicate JavaScript is disabled.
  	  - To re-enable JavaScript, repeat these steps, changing false to true.

  - You can google for other browsers too.

You can also replace the file in the proxy like BurpSuite or ZapProxy.

## MIME Type:
Websites perform validation through MIME Type in the POST data value. <br>
Upload you evil file and tamper the MIME Type value to the allowed one. <br>
For eg. `MIME Type: application/php` ---> `MIME Type: image/jpeg`

## Magic Byte / Header Check:
During the upload process web apps also verify the header of the file. <br>
Every file has a structure, different file types are simply chunks of bytes that follow a predefined structure. <br>
There are magic bytes at the start of the file that indicates that the file is of a certain format.
for eg: JPEG files begin with `FF` `D8` and end with `FF` `D9`.
        PDF files start with “%PDF” (hex `25` `50` `44` `46`).

**Solution:** Add magic byte of allowed filetype with your evil-file's content.

## Content-Type check via HEAD method request:
Some web apps or it's API perform a Content-Type check by sending a HEAD request to the remote resource (evil-file). <br>
If this happens then, add a `Content-Type` header in your evil-file providing value as of allowed one. <br>
Let's take an example of a `.php` file: <br>
`<?php
header("Content-Type: image/svg+xml")
// shell code goes here
?>`
