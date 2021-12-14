# Unbreakable Encryption
- **Author:** lgactna/Lloyd Gonzales
- **Tools used:** Python
- **Description:** One-time pad using XOR encryption with unknown key.
- **Difficulty:** 3

## Details 
- **Competition:** MetaCTF 2021
- **Scope:** Public
- **Category:** Cryptography
- **Subcategory:** Ciphers/Encryption

## Prompt 
There is a form of truly unbreakable encryption: the one time pad. Nobody, not Russia, not China, and not even Steve, who lives in his mom's basement and hacks governments for fun, can decrypt anything using this cipher... as long as it's used correctly. In this scheme, a truly random string as long as the plaintext is chosen, and the ciphertext is computed as the bitwise XOR of the plaintext and the key. However, if the key is reused even once, it can be cracked. We've intercepted some messages between some criminals, and we're hoping you could crack the one time pad they used. We're pretty sure they reused it, so you should be able to crack it...

Ciphertext 1: `4fd098298db95b7f1bc205b0a6d8ac15f1f821d72fbfa979d1c2148a24feaafdee8d3108e8ce29c3ce1291`

Plaintext 1: hey let's rob the bank at midnight tonight!

Ciphertext 2: `41d9806ec1b55c78258703be87ac9e06edb7369133b1d67ac0960d8632cfb7f2e7974e0ff3c536c1871b`

**Additional files:** none

## Solution 

### Intro
One-time pads work by taking each bit or character of the plaintext and performing some operation with the key, typically modular addition. For example, if our plaintext were `password` and we had a key of `12345678`, we would shift `p` by 1 letter, `a` by 2 letters, and so on to get `rcvwbuyl`. With a fully random key, this is unbreakable since you could map the ciphertext to a very large number of valid plaintexts. (More reading at [this Wikipedia page](https://en.wikipedia.org/wiki/One-time_pad).)

ASCII characters are generally stored in 1 byte (8 bits) of information. 1 hex number covers 4 bits, so two hex numbers covers 8 bits. If you check the length of the first ciphertext, it's 43 hex pairs long - exactly the length of the first plaintext. Therefore, each character is somehow turned into a hex pair in the ciphertext using the key from the one-time pad. 

However, we've been told that we're supposed to XOR each character with the key instead of using modular addition. In other words:

`h` XOR `??` = `4f`

`e` XOR `??` = `d0`

`y` XOR `??` = `98`

and so on. Our goal is to figure out what's being XORed for each character, and then use that same key on Ciphertext 2 to get the plaintext. But now that we've figured out what we need to do, how do we actually get the key?

### Breaking an individual character of the ciphertext
XOR is notable in that it's pretty straightforward to reverse. If you XOR the plaintext with a certain key, you can XOR the ciphertext with the same key to get the original plaintext. But more importantly, we can XOR a plaintext byte with a ciphertext byte to get the key for that byte. 

So, let's figure out the first byte of the key. 

First, let's convert `h` to its ASCII decimal representation - `104` - and then convert that to its binary representation - `01101000`. 

Then, let's convert `4f` to its binary representation - `01001111`. 

The result of `01101000 XOR 01001111` is `00100111`. That's the binary form of the key for the first character.

So now, if we take the first hex pair of the second ciphertext and convert it to binary - `41` -> `01000001` - we can now XOR it with our key to get the first plaintext character.

The result of `01000001 XOR 00100111` is `01100110`. This is 102 in binary, and corresponds to the letter `f` in ASCII. So, the first letter of Plaintext 2 is `f`.

### Automating this process
Obviously doing this process manually for every character is going to take some time. So here's a Python script to automate the process above:

```python
import binascii

cipher_1 = '4fd098298db95b7f1bc205b0a6d8ac15f1f821d72fbfa979d1c2148a24feaafdee8d3108e8ce29c3ce1291'
#break down the cipher text into its hex pairs
cipher_1_strs = [cipher_1[i:i+2] for i in range(0, len(cipher_1), 2)]
#and then convert the hex pairs into their integer representation
cipher_1_ints = [int(hex_val, 16) for hex_val in cipher_1_strs]

plain_1 = "hey let's rob the bank at midnight tonight!"
#convert each character of the plaintext string into its ASCII representation
plain_1_ints = [ord(a) for a in plain_1]

key = []

for i in range(0, len(cipher_1_ints)):
    #now, XOR each character/hex pair to get that specific character's key
    #and then add the key to our array
    key.append(cipher_1_ints[i]^plain_1_ints[i])


#perform the same process we did on the original ciphertext
cipher_2 = '41d9806ec1b55c78258703be87ac9e06edb7369133b1d67ac0960d8632cfb7f2e7974e0ff3c536c1871b'
cipher_2_strs = [cipher_2[i:i+2] for i in range(0, len(cipher_2), 2)]
cipher_2_ints = [int(hex_val, 16) for hex_val in cipher_2_strs]


plain_2_arr = []
for i in range(0, len(cipher_2_ints)):
    #for each character, xor the key with the second ciphertext, getting an integer result
    dec_result = cipher_2_ints[i]^key[i]
    #and map the integer to its ASCII character equivalent
    plain_2_arr.append(chr(dec_result))

#print out the entirety of the second plaintext, which should be the flag
print("".join(plain_2_arr))
```

Plaintext 2 is **flag is MetaCTF{you're_better_than_steve!}**.
