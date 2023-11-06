# Nice Netcat...

## Description

> There is a nice program that you can talk to by using this command in a shell: $ nc mercury.picoctf.net 22902, but it doesn't speak English...

## Solution

When we run the given command, it returns random characters.

>     $ nc mercury.picoctf.net 22902
>     112 
>     105 
>     99 
>     111 
>     67 
>     84 
>     70 
>     123 
>     103 
>     48 
>     48 
>     100 
>     95 
>     107 
>     49 
>     116 
>     116 
>     121 
>     33 
>     95 
>     110 
>     49 
>     99 
>     51 
>     95 
>     107 
>     49 
>     116 
>     116 
>     121 
>     33 
>     95 
>     100 
>     51 
>     100 
>     102 
>     100 
>     54 
>     100 
>     102 
>     125 
>     10

Now, just looking to this output we might assume is ASCII code so we try pasting the output into this [website](https://www.duplichecker.com/ascii-to-text.php) and it returned the flag.