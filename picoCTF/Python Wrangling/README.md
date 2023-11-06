# Python Wrangling

## Description

> Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?

## Files

- [ende.py](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Python%20Wrangling/ende.py)
- [flag.txt.en](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Python%20Wrangling/flag.txt.en)
- [pw.txt](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Python%20Wrangling/pw.txt)

## Solution

Firstly, you need to check [ende.py](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Python%20Wrangling/ende.py) to know what is doing. Once you get that it needs one argument, the encrypted file you want to decrypt. Then the script will need to enter the password saved in the [pw.txt](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Python%20Wrangling/pw.txt). Once you have all this information gathered, you run the script.

>     $ python3 ende.py -d flag.txt.en
>     Please enter the password:dbd1bea4dbd1bea4dbd1bea4dbd1bea4

This'll return the flag.