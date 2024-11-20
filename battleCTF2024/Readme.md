# BattleCTF 2024


## Misc
### Rules
Upon joining the discord server and nagivating to the #announcements channel we obtain the flag.
![Rule Challenge flag](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Rules/images/rules_flag.png)  
Flag: `battleCTF{HereWeGo}`

### Invite Code
This challenge was a bit tricky because many i overlooked the message in the #notification channel before the CTF began. Luckily, after sometime i discovered it.   
![Invite Code First Image](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Invite%20Code/images/invite_code_discord.png) 

First thing i did was to pick up the encoded data and place it into `cyberchef`.    
![Cyber Chef Hex Data Decode](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Invite%20Code/images/invite_code_cyberchef_from_hex.png)   
We can see that the data provided was a hex dump and `cyberchef` decoded it successfully resulting in a contatenation of base64 string and a link. The base64 string just leads us to the Rick Roll video in YouTube and so that isn't vert relevant.

The other link `https://bugpwn.com/invite.ini` leads us to a page where some data is hosted on the website.
![Invite .ini file](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Invite%20Code/images/invite_ini_file.png)

This looks like some base64 data. We can use `cyberchef` to decode this.
![Invite .ini b64 data decoded](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Invite%20Code/images/invite_ini_b64_data_decoded.png)    

From `cyberchef` i downloaded the raw binary file and run the file command on it.
```
mcsam@0x32:~/Desktop/ctf/AfricaBattleCTF$ file download.gz 
download.gz: gzip compressed data, last modified: Fri Oct  4 11:25:31 2024, max compression, original size modulo 2^32 1081
```

I then decided to attempt unzipping the file with gunzip. After unzipping i read the contents of the file.
```
mcsam@0x32:~/Desktop/ctf/AfricaBattleCTF$ gunzip download.gz 
mcsam@0x32:~/Desktop/ctf/AfricaBattleCTF$ cat download
b'\xac\xed\x00\x05t(\x83<?xml version="1.0" encoding="utf-8" standalone="no" ?>
<!DOCTYPE users SYSTEM >
<users max="81">
	<user >
		<loginname>battlectf</loginname>
		<password>$2a$12$ecui1lTmMWKRMR4jd44kfOkPx8leaL0tKChnNid4lNAbhr/YhPPxq</password>
		<4cr_encrypt>05 5F 26 74 9B 8D D7 09 49 EB 61 94 5D 07 7D 13 AA E8 75 CD 6A 1E 79 12 DA 1E 8A E7 2F 5F DB 87 E4 0D D2 13 E4 82 EE 10 AC A7 3A BF 54 B2 A4 A5 36 EA 2C 16 00 89 AE B8 22 0B F5 18 CA 03 32 C8 C6 6B 58 80 EC 70 77 6E 16 5C 56 82 6F AD 0B C5 97 69 E9 B8 4E 54 90 95 BB 4D ED 87 99 98 BF EC D4 E2 8A 0D C5 76 03 89 A6 11 AB 73 67 A0 75 AE 3C 84 B6 5D 21 03 71 B8 D9 A0 3B 62 C0 5B 12 DA 5C 91 87 19 63 02 A4 3B 04 9F E0 AD 75 3E 35 C3 FB 1B 5E CB F0 5A A7 8B DF 00 8B DC 88 24 EF F4 EE CE 5C 3B F3 20 10 C2 52 DF 57 D2 59 5E 3E 46 D0 85 10 89 AC 09 07 EF C5 EE 1D 2F 89 1D 83 51 C6 52 38 13 2A D0 20 66 6D 52 B1 93 1B 21 06 9F E5 00 B7 AB 30 EB 98 7F CB 80 17 36 16 EF 73 BB 59 60 E4 4B F0 8A BD FF 85 A1 37 5D 4E C0 91 92 F2 68 C5 20 68 A0 A7 84 EB</4cr_encrypt>
	</user>
</users>\r\n<!-- battleCTF AFRICA 2024 -->\r\n
``` 
The content of the .gz file is an XML file with some interesting fields. The `4cr_encrypt` field contains some encrypted data. I assumed that the name `4cr_encrypt` was just a wordplay of the actual enctyption scheme `rc4_encrypt`. Now that we are aware if the encyption scheme used we can attempt to decrypt it which would require a password. Luckily, we also have a password field in the XML file which is also hashed.

At this point i saved the hash to a file and attempted to crack the password with John The Ripper. After a while we obtain the password.
```
mcsam@0x32:~/Desktop/ctf/AfricaBattleCTF$ hashcat -m 3200 hashes ~/Downloads/rockyou.txt 
...
$2a$12$ecui1lTmMWKRMR4jd44kfOkPx8leaL0tKChnNid4lNAbhr/YhPPxq:nohara
``` 

Using this password and cyberchef i decrypted the data successfully to obtain the flag.
![Invite Code Flag Image](https://github.com/theMcSam/battleCTF-writeups/blob/main/battleCTF2024/Invite%20Code/images/invite_code_flag.png) 
Flag: `battleCTF{pwn2live_d7c51d9effacfe021fa0246e031c63e9116d8366875555771349d96c2cf0a60b}`

## Forensics
### Do[ro x2]

## Pwn
### Universe
