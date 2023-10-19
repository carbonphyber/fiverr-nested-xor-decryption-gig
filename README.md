# Fiverr project example decryption task

## Problem statement
Search for the keys and plaintext to an encrypted block of text which has been progressively XORed many times with different keys.

The goal is to find a decryption fitness function -- an algorithm to quickly search a large search space and detect if decoding with that key yields good quality plaintext candidates. This algorithm will then be used to find the best keys and the plaintext.

## Gig Requirements
The gig is to come up with a fitness function -- the logic used to determine which key is most likely to be successful. You need not write an entire program if you don't want to.

The *algorithm* must be delivered, not the keys or plaintext. You are solving an *example* decryption problem, not the real one. I must be able to replicate your algorithm with the real ciphertext to find the real plaintext.

You may choose pseudocode (simply describing the program/function logic in English text) or any common programming language, but I would prefer Python, JavaScript, C/C++, or CUDA C/C++.

If you deliver a brute force algorithm (eg. massively parallel GPU code), you *must* also filter and sort the resulting plaintext candidates by highlest likelihood of matching the fitness function.

## Encryption Algorithm
The encryption algorithm consists of multiple rounds of XOR with different keys. The algorithm makes a decryption pattern like this:

```
CIPHERTEXT ????????????????????????????????????????????????????????????????????????????????????
KEY        APPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPLEAPPL
XOR        ====================================================================================
           THIS PL?????????????????????????????????????????????????????????????????????????????
KEY        BANANABANANABANANABANANABANANABANANABANANABANANABANANABANANABANANABANANABANANABANANA
XOR        ====================================================================================
           *******AINTEX???????????????????????????????????????????????????????????????????????
KEY        COOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIECOOKIE
XOR        ====================================================================================
           *************T IS E?????????????????????????????????????????????????????????????????
KEY        DANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANCEDANC
XOR        ====================================================================================
           *******************NGLIS????????????????????????????????????????????????????????????
KEY        EMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJIEMOJ
XOR        ====================================================================================
           ************************H, WITH PUNCTUATION A???????????????????????????????????????
KEY        FACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACEFACE
XOR        ====================================================================================
           *********************************************ND HEXAD???????????????????????????????
KEY        GARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDENGARDEN
XOR        ====================================================================================
           *****************************************************ECIMAL?????????????????????????
KEY        HIPPOPOTAMUSHIPPOPOTAMUSHIPPOPOTAMUSHIPPOPOTAMUSHIPPOPOTAMUSHIPPOPOTAMUSHIPPOPOTAMUS
XOR        ====================================================================================
           *********************************************************** STRING??????????????????
KEY        IDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLICIDYLLIC
XOR        ====================================================================================
           ******************************************************************S. 0xBAD0F????????
KEY        JACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOTJACKPOT
XOR        ====================================================================================
           ****************************************************************************F1CEF00D

PLAINTEXT
           THIS PLAINTEXT IS ENGLISH, WITH PUNCTUATION AND HEXADECIMAL STRINGS. 0xBAD0FF1CEF00D
```

### Explanation
In this example, there are 10 rounds of XOR encryption with the following keys: APPLE, BANANA, COOKIE, DANCE, EMOJI, FACE, GARDEN, HIPPOPOTAMUS, IDYLLIC, JACKPOT. The keys are of varying length (each key could have a different length) and unknown (we, the solvers, do not know any of the keys). The real keys could include ASCII letters (as in this example) or be mixed with other characters including non-printable bytes (the example keys are simple and contrived compared to the real problem's search space).

This example is 84 bytes of cyphertext / plaintext length, but the real puzzle is over 5000 bytes, so frequency analysis could be useful.

The strings "?????" in the example represent ciphertext bytes (not necessarily human-readable letters). The strings "*****" represent text positions that have already been previously decrypted, thus we can ignore these bytes.

Note how the plaintext is revealed progressively through a different number of XOR iterations with different keys. This is presumably done to limit the effectiveness of simple frequency analysis.

The example shows the final plaintext at the beginning of each result of the XOR round plaintext. Do not assume it will always be at the beginning. It may always be located at the end of each round's XOR result, or it may be randomly located within each round XOR result. We can assume that it will be mostly contiguous (all of the plaintext will be located near each other, not interspersed throughout the result).

## Decryption Parameters / Hints
Plaintext is mostly English text (ASCII letters) with some grammar characters (whitespace, ASCII English punctuation, ASCII English numbers). It is likely to include hexadecimal or octal strings.

The plaintext could very likely include alterations to make frequency analysis less effective. Perhaps whitespaces were replaced with Q or Z characters.

Each of the XOR keys are unknown length. We can assume at least 3 bytes per key, but we don't know an upper bound.

Your delivered algorithm should be compatible with 10 iterations / depth. The actual encryption depth / number of iterations (nested XOR encryptions) is unknown. Do not hard-code assumptions about depth (eg. the algorithm should continue working if I increase the XOR decryption depth to 18 or reduce it to 3).

Assume we do not have any exact "crib text" (known plaintext sequences). This means we would likely need to use frequency analysis for the characters we expect to be most common in the plaintext.

Remember that XOR is a bit-wise operation. The most-sigificant bit of all ASCII printable characters we care about is 0, so we can safely eliminate any key which XORs to the most significant bit equals 1 in a position where we exect a printable ASCII plaintext character.

## Gig Hints

I don't want to create any unnecessary work for you:
  - I can find expected character frequency charts for English.
  - Use pseudocode if you choose not to compile and run your solution.

I may choose to hire you for similar future gigs if I am pleased with the solution quality of this gig.
