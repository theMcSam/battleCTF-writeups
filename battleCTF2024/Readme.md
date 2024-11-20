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


## Forensics
### Do[ro x2]

## Pwn
### Universe
