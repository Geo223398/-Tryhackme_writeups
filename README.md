**Cache Me Outside - TryHackMe Walkthrough
Objective**
The challenge provides a short conversation between two individuals. Our goal is to identify a retired hacker using the limited information available and answer a series of OSINT-based questions.
________________________________________
**Step 1: Investigating the Komoot Profile**
The conversation contained a Komoot profile link:
http://www.komoot.com/user/5667624959835
After opening the profile, the retired hacker's identity was revealed.
 <img width="940" height="417" alt="image" src="https://github.com/user-attachments/assets/227111db-6be3-4a49-b21f-0cba4e079583" />

**Answer 1**
What is the retired hacker's full name?
Jim Lee
________________________________________
**Step 2: GitHub Enumeration**
The Komoot profile contained a link to a GitHub account:
https://github.com/jiml33t
While examining the repositories, the commit history appeared interesting.
Repository commits:
https://github.com/jiml33t/jiml33t/commits/main/
One commit stood out:
7b2c8e0a540c36f2e09da5945066020621d6a059
Git commit metadata often contains information that is not immediately visible on the repository page, such as usernames and email addresses.

Clone the Repository
```git clone https://github.com/jiml33t/jiml33t.git
cd jiml33t
Inspect the Commit
(alone㉿kali)-[~]
└─$ git clone https://github.com/jiml33t/jiml33t.git
Cloning into 'jiml33t'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (3/3), done.
                                                                                                      
┌──(alone㉿kali)-[~]

From the commit info we get the second question answer

What email address did he accidentally expose?

jimleepro1@gmail.com

─(alone㉿kali)-[~/jiml33t]
└─$ git show 7b2c8e0a540c36f2e09da5945066020621d6a059
commit 7b2c8e0a540c36f2e09da5945066020621d6a059 (HEAD -> main, origin/main, origin/HEAD)
Author: jimleepro1-cell <jimleepro1@gmail.com>
Date:   Thu Apr 16 03:27:19 2026 -0400

    Initial commit

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..488f2e9
--- /dev/null
+++ b/README.md
@@ -0,0 +1,16 @@
+## Hi there 👋
+
+<!--
+**jimleepro1-cell/jimleepro1-cell** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.
+
+Here are some ideas to get you started:
+
+- 🔭 I’m currently working on ...
+- 🌱 I’m currently learning ...

Initial commit
The commit metadata exposed the author's email address.
Answer 2
What email address did he accidentally expose?
jimleepro1@gmail.com```
________________________________________
Step 3: Email Investigation
Using the exposed email address, an email was sent to the target as instructed by the challenge.
The automated response contained additional contact information.
 <img width="940" height="466" alt="image" src="https://github.com/user-attachments/assets/1f1deeeb-60a4-4809-ae28-54e0bc6d6e9c" />

Answer 3
What is his phone number?
+40 743 321 239
The Romanian country code (+40) would later become an important geographical clue.
________________________________________
Step 4: Username Enumeration
To identify additional online accounts associated with the target, username enumeration was performed.

Using holehe
sudo apt update
pipx –version ( if not installed install (sudo apt install pipx -y))
pipx install holehe
running - holehe jimleepro1@gmail.com

[+] Email used, [-] Email not used, [x] Rate limit
121 websites checked in 10.8 seconds
Twitter : @palenath
Github : https://github.com/megadose/holehe
For BTC Donations : 1FHDM49QfZX6pJmhjLE5tB2K6CaTLMZpXZ
100%|██████████████████████████████████████████████████████████████| 121/121 [00:10<00:00, 11.22it/s]
                                                                                                      
┌──(alone㉿kali)-[~]

But the result is not giving much info like expected trying with maigret

                                                                                                    
┌──(alone㉿kali)-[~]
└─$ pipx install maigret
  installed package maigret 0.6.1, installed using Python 3.13.12
  These apps are now available
    - maigret
    - update_sitesmd
done! ✨ 🌟 ✨
                                                                                                      
┌──(alone㉿kali)-[~]
└─$ maigret jiml33t
[*] DB auto-update: checking for updates...
[*] DB auto-update: downloading database (3159 sites)...
[+] DB auto-update: database updated successfully (3159 sites)
[+] Using sites database: /home/alone/.maigret/data.json (3159 sites)
[-] Starting a search on top 509 sites from the Maigret database...
[!] You can run search by full list of sites with flag `-a`
[*] Checking username jiml33t on:
[+] Instagram: https://www.instagram.com/jiml33t/
       └─username: jiml33t
[+] GitHub: https://github.com/jiml33t
       ├─uid: 276522146
       ├─image: https://avatars.githubusercontent.com/u/276522146?v=4
       ├─created_at: 2026-04-16T07:24:48Z
       ├─follower_count: 35
       ├─following_count: 0
       ├─public_gists_count: 0
       ├─public_repos_count: 1
       ├─bio: Currently starting my security consulting firm | Ex-Hacker | Avid Runner
       └─is_company: Jim Lee Security Consulting
[+] Threads: https://www.threads.net/@jiml33t
        ├─fullname: JimLee
        ├─username: jiml33t
        ├─follower_count: 9
        └─posts_count: 3
[+] mastodon.cloud: https://mastodon.cloud/@jiml33t
[+] GitHubGist [GitHub]: https://gist.github.com/jiml33t
Searching |████████████████████████████████████████| 509/509 [100%] in 43.3s (11.79/s) 
[!] Too many errors of type "Access denied" (10.0%)
[-] You can see detailed site check errors with a flag `--print-errors`
[-] Extracted IDs: {'jiml33t': 'username'}
[*] Short text report:
Search by username jiml33t returned 5 accounts.
Extended info extracted from 3 accounts.
Countries: pk
Interests (tags): social, coding, photo, sharing
                                                                                                      
┌──(alone㉿kali)-[~]
└─$



holehe jimleepro1@gmail.com
While Holehe confirmed the email existed on multiple platforms, it did not provide enough useful information for the challenge.
Maigret
pipx install maigret

maigret jiml33t
Results:
Instagram: https://www.instagram.com/jiml33t/
GitHub: https://github.com/jiml33t
Threads: https://www.threads.net/@jiml33t
Mastodon: https://mastodon.cloud/@jiml33t
The Threads account looked particularly promising.
________________________________________
Step 5: Threads Investigation
The Threads profile contained several posts.
One post mentioned:
Finished my last run before the big day and heading on the tram for a coffee at my favourite French supermarket.
The attached image provided a valuable geolocation clue.
<img width="940" height="446" alt="image" src="https://github.com/user-attachments/assets/603378c7-7efe-4919-8cfc-ba31edfa5b03" />

After carefully examining the image, a visible sign could be seen on the left side of the road:
IRIGATII.RO
 
________________________________________
Step 6: Geolocation
The sign was searched online:
IRIGATII.RO Romania
Using Google Maps and Street View, the surrounding area was compared with the image posted on Threads.
 <img width="940" height="512" alt="image" src="https://github.com/user-attachments/assets/81cf1781-c045-4720-9320-5b94da9da686" />

Matching indicators included:
•	IRIGATII.RO signage
•	Yellow/orange building
•	Road layout
•	Tram infrastructure
•	Overhead tram wires
•	Nearby surroundings
The location matched an area on DJ592 in Timișoara, Romania.
Combined with the Romanian phone number (+40), this strongly confirmed the location.
Answer 4
In which city is he located?
Timișoara
________________________________________
Step 7: Identifying the Tram Station
The final challenge required identifying the tram station where Jim got off on 7 May 2026.
Using:
•	The Threads post
•	The identified location in Timișoara
•	Nearby tram routes
•	Local transport infrastructure
The most likely matching tram stop was determined.
Answer 5
At which tram station did he get off?
Piața Gheorghe Domășneanu
________________________________________
Final Answers
Question	Answer
Retired hacker's full name	Jim Lee
Exposed email address	jimleepro1@gmail.com

Phone number	+40 743 321 239
City	Timișoara
Tram station	Piața Gheorghe Domășneanu
________________________________________


