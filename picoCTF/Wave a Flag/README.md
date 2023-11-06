# Wave a Flag

## Description

> Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information...

## Files

- [warm](https://github.com/ZeN1xX/ctf-writeups/blob/main/picoCTF/Wave%20a%20Flag/warm)

## Solution

This challenge is very simple, you just need to use the strings command and pipe it with grep to get the flag. As you know the flag format ***picoCTF*** you just grep that to the strings output.

>     $ strings wave | grep picoCTF

This will output the desired flag.