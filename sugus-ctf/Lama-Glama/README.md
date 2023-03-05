
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

Primero, vamos a imprimir las seuencias de caracteres imprimibles del fichero.

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

Empezando por el campo passwors, se ve que el formato podría estar codificado
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

En la salida [Figura 2.1] observamos que los ficheros que se encuentran dentro de
[Josefina.jpg](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf/Lama-Glama/Josefina.jpg)
son simplemente archivos comprimidos ZIP.

~~~

~~~

![Figura 2.1](https://user-images.githubusercontent.com/114481026/222983443-a3955532-a07d-4f63-82de-077136d0673c.png "Figura 2.1")

Para proceder a la estracción del fichero, habría dos opciones:

- Opción 1:
	
