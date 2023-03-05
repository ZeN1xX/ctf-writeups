
# Lama Glama

## Enunciado

> Mi mascota Josefina, podéis llamarla Josefi, lleva unos días un poco rebelde y
> se ha comido cosas que no debería.
> ¿Puedes ayudarme a encontrar mi flag antes de que tenga graves consecuencias
> sobre mi Josefina?

## Files

- [Josefina.jpg](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf/Lama-Glama/Josefina.jpg)

---

## Solución

Primero, vamos a imprimir las secuencias de caracteres imprimibles del fichero.

Para ellos vamo a ayudarnos del comando strings, de la siguiente forma:

>~~~
>$ strings Josefina.jpg
>...
>...
>Password: SGFrdW5hTWF0YXRh==
>ctfsugus/UT
>ctfsugus/flag.txtUT
>GZ/MyM
>f8C~
>ctfsugus/UT
>ctfsugus/flag.txtUT
>~~~

Observamos en la salida dos campos bastante interesantes:

- Password: SGFrdW5hTWF0YXRh==
- ctf\_sugus/flag.txt

Empezando por el campo password, se ve que el formato podría estar codificado
mediante base64, por tanto decodificamos con:

>     $ echo SGFrdW5hTWF0YXRh | base64 --decode

Produce como salida:

> HakunaMatata

Otra opción prodría haber sido utilizar la herramienta online [CyberChef](https://gchq.github.io/CyberChef/)
para decodificar el password mencionado anteriormente.

Continuando con la salida del comando strings, observamos que hay un fichero
flag.txt dentro de la imagen, por tanto con la herramienta *binwalk* vamos a
averiguar de que se trata.

Esta herramienta puede instalarse mediante:

>     $ sudo apt-get install binwalk

Binwalk permite buscar archivos y código ejecutable dentro de otros
archivos, para ello:

>~~~
>$ binwalk Josefina.jpg
>DECIMAL       HEXADECIMAL     DESCRIPTION
>--------------------------------------------------------------------------------
>0             0x0             JPEG image data, JFIF standard 1.01
>78465         0x13281         Zip archive data, at least v1.0 to extract, name: ctfsugus/
>78532         0x132C4         Zip archive data, encrypted at least v1.0 to extract, compressed size: 119, uncompressed size: 107, name: ctfsugus/flag.txt
>78908         0x1343C         End of Zip archive, footer length: 22
>~~~

En la salida observamos que los ficheros que se encuentran dentro de
[Josefina.jpg](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf/Lama-Glama/Josefina.jpg)
son simplemente archivos comprimidos ZIP.

Para proceder a la estracción del fichero:

>~~~
>$ unzip Josefina.jpg
>Archive:  Josefina.jpg
>warning [Josefina.jpg]:  78465 extra bytes at beginning or within zipfile
>  (attempting to process anyway)
>   creating: ctfsugus/
>[Josefina.jpg] ctfsugus/flag.txt password: HakunaMatata
> extracting: ctfsugus/flag.txt
>~~~

Como se puede observar, nos ha exigido una contraseña para poder extraer el
fichero ZIP, para ello hemos utilizado la contraseña que decodificamos
anteriormente, ***HakunaMatata***

Esto ha producido un nuevo directorio *ctfsugus*, con un fcihero dentro, *flag.txt*

Accedemos a dicho fichero mediante:

>~~~
>$ cat ctfsugus/flag.txt
>Aquí tienes tu flag:
>Q0VRRUN7RHIwYzNfZ1IwX01rWF8xd0s2c1hvX2tYaTdyMXg2X21LeF9tQjNrRDNfZHIzXzF3ejBjQ3NsVjN9
>~~~

Se puede ver que de nuevo la flag se encuentra codificada en base64. Para decodificarla
simplemente como hemos hecho anteriormente.

>     $ echo Q0VRRUN7RHIwYzNfZ1IwX01rWF8xd0s2c1hvX2tYaTdyMXg2X21LeF9tQjNrRDNfZHIzXzF3ejBjQ3NsVjN9 | base64 --decode

Su salida sería:

> CEQEC{Dr0c3_gR0_MkX_1wK6sXo_kXi7r1x6_mKx_mB3kD3_dr3_1wz0cCslV3}

Observamos que el formato es como debería ser la flag, pero con los caracteres rotados.
Utilizando la herramienta [CyberChef](https://gchq.github.io/CyberChef/)
procedemos a descifrar la flag.

Concretamente con la opción ROT13 Brute Force de [CyberChef](https://gchq.github.io/CyberChef/)
nos devuelve todas las combinaciones posibles de rotación de caracteres, y,
rotando exactamente 16 veces los caracteres obtenemos el formato de la flag correcto.

> ***SUGUS{Th0s3_wH0_CaN_1mA6iNe_aNy7h1n6_cAn_cR3aT3_th3_1mp0sSibL3}***
