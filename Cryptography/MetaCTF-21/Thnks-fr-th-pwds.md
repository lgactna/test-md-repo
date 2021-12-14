# Thnks fr th Pwds
- **Author:** lgactna/Lloyd Gonzales (originally solved by Rogue King/Miguel M.)
- **Tools used:** CyberChef
- **Description:** Simple Base64 decode
- **Difficulty:** 1

## Details 
- **Competition:** MetaCTF 2021
- **Scope:** Public
- **Category:** Cryptography
- **Subcategory:** Encoding Formats

## Prompt 
On a red team engagement, you discover a text file on an administrator’s desktop with all of their passwords - you now have the keys to the kingdom!

During the engagement debrief, you explain what you found and how you were able to access so many systems. The administrator says that's impossible, because they encrypted all of the passwords in the file.

Here’s an example of one of their “encrypted” passwords: `TWV0YUNURntlbmNvZGluZ19pc19OMFRfdGhlX3NhbWVfYXNfZW5jcnlwdGlvbiEhfQ==`

See if you’re able to recover the Administrator's password.

**Additional files:** none

## Solution 
This looks a lot like a Base64-encoded message, judging by the alphanumeric characters and the equal-sign padding at the end. Let's put it into [CyberChef with the From Base64 recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=VFdWMFlVTlVSbnRsYm1OdlpHbHVaMTlwYzE5T01GUmZkR2hsWDNOaGJXVmZZWE5mWlc1amNubHdkR2x2YmlFaGZRPT0):

`TWV0YUNURntlbmNvZGluZ19pc19OMFRfdGhlX3NhbWVfYXNfZW5jcnlwdGlvbiEhfQ==` -> `MetaCTF{encoding_is_N0T_the_same_as_encryption!!}`

The flag is **`MetaCTF{encoding_is_N0T_the_same_as_encryption!!}`**
