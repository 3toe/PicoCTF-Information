# PicoCTF-Information
Write-up for a PicoCTF challenge

Location: https://play.picoctf.org/practice/challenge/186

Category: Forensics

Description: Files can always be changed in a secret way. Can you find the flag? [cat.jpg]

How to solve:
  1. After opening the image and looking at it, I saw no flags in the image itself. I expected the flag to be hidden in the metadata anyways, since putting it in an image is too easy and not aligned with the description.
  2. I opened the details in windows and saw nothing of note, so I loaded the image into https://jimpl.com/ which displays image metadata for free online. This method would have gotten me halfway there, but I didn't notice the clue at the time.
  3. Next I tried an online steganography tool: https://stegonline.georgeom.net/upload. This was overkill but was a nice discovery / tool that I will bookmark for later!
  4. At this point I checked the hints which provided nothing useful beyond what I was trying.
  5. After messing with stegonline a little more and finding nothing (I did see "ATeem=#1" in embedded text and thought i was getting somewhere, but this was a red herring), i decided to look up the solution online. The key was in the license, which was displayed by jimpl earlier, but I didn't think it was relevant at the time. For the given cat.jpg image, the license in the metadata was "cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9". Without knowing what a typical value for this field is, one might not get suspicious of this.  However, after doing some research, you might expect either nothing in this field (relatively common) or something like "Creatice commons (CC)" or a URL.
  6. Once you suspect this text to contain a lead to the flag, you would have to realize its encoded and either recognize it as base64 (which I did not), or use something like CyberChef (https://gchq.github.io/CyberChef/) which I found while researching this CTF. This is a free platform that can encode or decode text using some common algorithms, and (most importantly for this challenge) can detect which algorithm was used to encode something, and reverse it if successful (using the "magic" mode). Upon pasting the encoded text into CyberChef and running it through the "magic" decoding operation, the flag is revealed.

Flag: picoCTF{the_m3tadata_1s_modified}

Notes: While this challenge was considerably more challenging than the first 4 and the hint was misleading (checking the file "details" as the hint suggested in windows gets you nowhere), the tools and tricks I learned about while cheating to get the answer made the experience worthwhile.
