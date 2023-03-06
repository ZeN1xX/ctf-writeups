# Conexión Remota

## Enunciado

> Hemos detectado una conexión remota a nuestro sistema. Te proporcionamos lo que nuestros sistemas han captado del rastro que ha dejado.
¿Serías capaz de recuperar los ficheros extraídos?

## Files

- [evidencias.pcapng](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf-2023/Conexion-Remota/evidencias.pcapng)

---

## Solución

Para resolver este reto requeriremos de la herramienta [Wireshark](https://www.wireshark.org/download.html) la cual nos permite analizar el tráfico capturado en la evidencia proporcionada.

En Linux podría instalarse de la siguiente forma:

>     $ sudo apt install wireshark

Una vez instalado, abriremos [evidencias.pcapng](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf-2023/Conexion-Remota/evidencias.pcapng) y nos pondremos a investigar.

Observamos que hay una conexión ***Telnet*** entre dos máquinas, como bien sabemos, Telnet es un protocolo que envía la información en ***texto plano***, es decir, no cifra el intercambio de mensajes. Por ello vamos a indagar en dicha conexión a ver que encontramos.

Para ello solo es necesario dar Click Derecho sobre un paquete ***Telnet*** y navegar hasta la opción ***Seguir > Flujo TCP***, o simplemente la combinación de teclas ***Ctrl + Alt + Mayusc + T***.

Esto abrirá una ventana donde podremos observar mas claramente el intercambio de mensajes.

>     ...
>     ...
>     ionia login: aakkaallii
>     .
>     Password: akali
>     .
>     .[?2004hakali@ionia:~$ zziipp  ----eennccrryypptt  ffllaagg..zziipp  ffllaagg..ttxxtt
>     .
>     .[?2004l
>     .Enter password: CTFSUGUS2023
>     .
>     Verify password: CTFSUGUS2023
>     .
>       adding: flag.txt (stored 0%)
>     .[?2004hakali@ionia:~$ rrmm  ffllaa	.g.tt	xt 
>     .
>     .[?2004l
>     ..[?2004hakali@ionia:~$ ffttpp  aazziirr
>     .
>     .[?2004l
>     .Connected to azir.
>     220 (vsFTPd 3.0.5)
>     Name (azir:akali): aazziirr
>     .
>     331 Please specify the password.
>     Password: azir
>     .
>     230 Login successful.
>     Remote system type is UNIX.
>     Using binary mode to transfer files.
>     ftp> ppuutt  ffllaa	
>     ..[13Gg.zip 
>     .
>     local: flag.zip remote: flag.zip
>     229 Entering Extended Passive Mode (|||49989|)
>     150 Ok to send data.
>     
>     .  0% |                                                       |     0        0.00 >     KiB/s    --:-- ETA
>     .100% |*******************************************************|   225        2.82 >     MiB/s    00:00 ETA
>     226 Transfer complete.
>     225 bytes sent in 00:00 (156.16 KiB/s)
>     ftp> bbyyee
>     .
>     221 Goodbye.
>     ...
>     ...

Podemos ver en este snippet de la captura, que despues de logearse, comprime un archivo llamado flag.txt en un ZIP y lo protege con una contraseña, pero, debido a que ***Telnet*** no cifra el paso de mensajes, somos capaces de leer la contraseña con la que se ha comprimido dicho fichero ZIP.

> ***CTFSUGUS2023***

Después de comprimir este fichero, procede a eliminarlo mediante:

>     $ rm flag.txt

Finalmente, se abre una conexión ***FTP (File Transfer Protocol)*** consigo mismo para enviarse ese fichero que ha comprimido. Así mismo, como ocurre con ***Telnet*** podemos tener tener acceso a los datos que han sido transferidos.

Para ello vamos a filtrar los paquetes mediante el filtro:

>     ftp-data

Con esto logramos que solo nos aparezcan los datos que han sido transmitidos mediante ***FTP***. Para extraer el ZIP que ha sido enviado, simplemente con seguir los mismos pasos que para ver la conversación ***Telnet***, Click Derecho sobre el paquete y después ***Seguir > Flujo TCP***. 

Ahora con los datos de la transmisión queremos tenerlos tal cual han sido enviados, sin formato, es decir, en crudo. Para ello desde esta ventana en la opcion ***"Mostrar datos como"*** desplegamos el menú y seleccionamos la opción ***Raw***.

Una vez hecho esto, solo queda guardar el fichero mediante la opción ***"Guardar como"*** y añadirle la extensión *.zip*. Ahora, extraemos el contenido de dicho fichero mediante:

>     $ unzip <ruta/nombreFichero>

Después con un simple cat accedemos a la flag.

>     $ cat flag.txt  
>     SUGUS{P3oP1e_7hE_W3ak357_L1nK}

Se puede ver ya la flag en su formato correcto.

> ***SUGUS{P3oP1e_7hE_W3ak357_L1nK}***