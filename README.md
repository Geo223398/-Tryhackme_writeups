# Cache Me Outside - TryHackMe Walkthrough

## Objective

The challenge provides a short conversation between two individuals. Our goal is to identify a retired hacker using the limited information available and answer a series of OSINT-based questions.

---

## Step 1: Investigating the Komoot Profile

The conversation contained a Komoot profile link:

```text
http://www.komoot.com/user/5667624959835
```

After opening the profile, the retired hacker's identity was revealed.

 <img width="940" height="417" alt="image" src="https://github.com/user-attachments/assets/227111db-6be3-4a49-b21f-0cba4e079583" />


### Answer 1

**What is the retired hacker's full name?**

**Jim Lee**

---

## Step 2: GitHub Enumeration

The Komoot profile contained a link to a GitHub account:

```text
https://github.com/jiml33t
```

While examining the repositories, the commit history appeared interesting.

Repository commits:

```text
https://github.com/jiml33t/jiml33t/commits/main/
```

One commit stood out:

```text
7b2c8e0a540c36f2e09da5945066020621d6a059
```

Git commit metadata often contains information that is not immediately visible on the repository page, such as usernames and email addresses.

### Clone the Repository

```bash
git clone https://github.com/jiml33t/jiml33t.git
cd jiml33t
```

### Inspect the Commit

```bash
git show 7b2c8e0a540c36f2e09da5945066020621d6a059
```

Relevant output:

```text
commit 7b2c8e0a540c36f2e09da5945066020621d6a059
Author: jimleepro1-cell <jimleepro1@gmail.com>
Date: Thu Apr 16 03:27:19 2026 -0400

Initial commit
```

The commit metadata exposed the author's email address.

### Answer 2

**What email address did he accidentally expose?**

**jimleepro1@gmail.com**

---

## Step 3: Email Investigation

Using the exposed email address, an email was sent to the target as instructed by the challenge.

The automated response contained additional contact information.

 <img width="940" height="466" alt="image" src="https://github.com/user-attachments/assets/1f1deeeb-60a4-4809-ae28-54e0bc6d6e9c" />

### Answer 3

**What is his phone number?**

**+40 743 321 239**

The Romanian country code (**+40**) would later become an important geographical clue.

---

## Step 4: Username Enumeration

To identify additional online accounts associated with the target, username enumeration was performed.

### Using Holehe

Installation:

```bash
sudo apt update
sudo apt install pipx -y
pipx install holehe
```

Usage:

```bash
holehe jimleepro1@gmail.com
```

Although Holehe confirmed the email existed on multiple platforms, it did not provide enough information for the challenge.

### Using Maigret

Installation:

```bash
pipx install maigret
```

Usage:

```bash
maigret jiml33t
```

Results:

```text
Instagram: https://www.instagram.com/jiml33t/
GitHub: https://github.com/jiml33t
Threads: https://www.threads.net/@jiml33t
Mastodon: https://mastodon.cloud/@jiml33t
```

The Threads account appeared particularly promising.

---

## Step 5: Threads Investigation

The Threads profile contained several posts.

One post mentioned:

> Finished my last run before the big day and heading on the tram for a coffee at my favourite French supermarket.

The attached image provided a valuable geolocation clue.

<img width="940" height="446" alt="image" src="https://github.com/user-attachments/assets/603378c7-7efe-4919-8cfc-ba31edfa5b03" />

After carefully examining the image, a visible sign could be seen on the left side of the road:

```text
IRIGATII.RO
```

---

## Step 6: Geolocation

The sign was searched online:

```text
IRIGATII.RO Romania
```

Using Google Maps and Street View, the surrounding area was compared with the image posted on Threads.

 <img width="940" height="512" alt="image" src="https://github.com/user-attachments/assets/81cf1781-c045-4720-9320-5b94da9da686" />

Matching indicators included:

- IRIGATII.RO signage
- Yellow/orange building
- Road layout
- Tram infrastructure
- Overhead tram wires
- Nearby surroundings

The location matched an area on DJ592 in Timișoara, Romania.

Combined with the Romanian phone number (+40), this strongly confirmed the location.

### Answer 4

**In which city is he located?**

**Timișoara**

---

## Step 7: Identifying the Tram Station

The final challenge required identifying the tram station where Jim got off on 7 May 2026.

Using:

- The Threads post
- The identified location in Timișoara
- Nearby tram routes
- Local transport infrastructure

The most likely matching tram stop was determined.

### Answer 5

**At which tram station did he get off?**

**Piața Gheorghe Domășneanu**

---

## Final Answers

| Question | Answer |
|-----------|---------|
| Retired hacker's full name | Jim Lee |
| Exposed email address | jimleepro1@gmail.com |
| Phone number | +40 743 321 239 |
| City | Timișoara |
| Tram station | Piața Gheorghe Domășneanu |

---
