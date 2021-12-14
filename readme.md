# Nevada Cyber Club writeups
The goal of this repo is to have a standardized list covering major challenges that we've encountered as a club. 

For both new and old members, it helps a lot to know how to approach problems that appear similar from CTF to CTF without needing to retread old ground. But it's especially for new members to learn how to use stuff like Wireshark and Python scripting effectively, as well as picking up more generalized problem-solving skills and computing knowledge.

## Competitions
The below are a full list of competitions and challenges that this repository covers.
### Public
Public writeups are for competitions that allow for the open distribution of writeups. 
- MetaCTF 2021
- Selected CyberStart challenges 
### Private 
Private writeups are for competitions that allow internal distribution of writeups that must be stored behind some form of an authentication system. *Do not share writeups labeled as private outside of the club! Call your writeups for private-scope competitions `PRIVATE-<writeup-name>.md`*.
- NCL Fall 2021

## Categories 
There are also additional subcategories to help separate common or expansive categories. These don't fall under separate folders, but they are given their own section on their category's readme.
- **Binary Exploitation:** Anything to do with the reverse engineering of binaries and source code.  This includes binaries running on a remote server (e.g. `nc` is required) and those that can be downloaded on your local computer.  
	- No subcategories 
- **Cryptography:** Message encryption and obfuscation.  
	- Encoding formats
	- Ciphers 
	- Steganography
	- Advanced crypto
- **Forensics:** Investigation and analysis of digital files and evidence, usually involving a bunch of Googling.  
	- Geoguessr style problems 
	- Filesystems
- **Log Analysis:** Generic log analysis from various services and programs.  
	- Tabular 
	- Non-tabular 
- **Network Traffic Analysis:** Networking-specific log analysis, usually involving packet captures.  
	- Generic Wireshark problems 
	- Random 
- **OSINT**: Open-source everything.
	- Identifiers 
	- Random 
- **Password Cracking:** What it says on the label.  
	- Standard 
	- Custom wordlists
- **Reconnaissance:** Target scanning and establishing an attack surface.  
	- No subcategories 

## Format 
If your challenge has additional files, then go to that category's "Assets" folder. Make a subfolder named exactly the same as your writeup file, and then place all of the files in that subfolder. For example, if you had a file called `coffee` for a binary exploitation writeup called `Coffee-Break.md`:
- `/Binary Exploitation`
	- `/Assets`
		- `/Coffee-Break`
			- `/screenshots`
				- `ss-1.png`
				- `ss-2.png`
			- `coffee`
	- `Coffee-Break.md`
	- `readme.md`
- `/Crytography`
	- `...`
- `...`

Note how you should also put screenshots of your solution into the folder above, too.

When you make a writeup, put the full formal name of the writeup, a brief description in that category's readme, and the competition. For example:
`- **[Coffee Break](Coffee-Break.md):** Reversing XOR encryption in a Java file. (WolfHack F21)`
Which shows up as (without the hyperlink):
- **Coffee Break:** Reversing XOR encryption in a Java file.s (WolfHack F21)

Hyperlink the **bolded title** to your writeup file on the category's readme file. Likewise, hyperlink to the folder containing your challenge's assets on your writeup file.

All writeups are Markdown files. They don't *have* to be named the exact same as the title, but it helps a lot. Please follow the following format:

```
# Title
- **Author:** you
- **Tools used:** CyberChef
- **Description:** Simple Base64 decode
- **Difficulty (0-10):** 1 (Make your best judgement - difficulty can differ based on time taken, special knowledge necessary, etc. 5 should represent a challenge that requires several hours to solve (a high-end hard NCL problem).)

## Details 
- **Competition:** None
- **Scope:** Private
- **Category:** Cryptography
- **Subcategory:** Encoding Formats

## Prompt 
What's he never gonna give me? `ZFF3NHc5V2dYY1E=`

**Additional files:** none

## Solution 
This looks a lot like a Base64-encoded message, judging by the alphanumeric characters and the equal-sign padding at the end. Let's put it into [CyberChef with the From Base64 recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=WkZGM05IYzVWMmRZWTFFPQ):

`ZFF3NHc5V2dYY1E=` -> `dQw4w9WgXcQ`

Sure enough, we get something out. Looking up the result on Google reveals a certain video, to which the answer is **up**.
```

Here's what that looks like:

---

# Title
- **Author:** you
- **Tools used:** CyberChef
- **Description:** Simple Base64 decode
- **Difficulty (0-10):** 1

## Details 
- **Competition:** None
- **Scope:** Private
- **Category:** Cryptography
- **Subcategory:** Encoding Formats

## Prompt 
What's he never gonna give me? `ZFF3NHc5V2dYY1E=`

**Additional files:** none

## Solution 
This looks a lot like a Base64-encoded message, judging by the alphanumeric characters and the equal-sign padding at the end. Let's put it into [CyberChef with the From Base64 recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=WkZGM05IYzVWMmRZWTFFPQ):

`ZFF3NHc5V2dYY1E=` -> `dQw4w9WgXcQ`

Sure enough, we get something human-readable out. Looking up the result on Google reveals a certain video, to which the answer is **up**.