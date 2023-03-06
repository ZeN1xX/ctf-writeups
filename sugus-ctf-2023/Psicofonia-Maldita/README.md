# Psicofonía Maldita

## Enunciado

> Hemos encontrado esta pista de audio entre unas cajas de unos antiguos investigadores paranormales. Parace ser que un espectro se adueño del cuerpo de la mascota de la familia, la llama Josefina. 
¿Serías capaz de saber que nos quiere decir?

## Files

- [psicofonia.wav](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf/Psicofonia-Maldita/psicofonia.wav)

---

## Solución

Después de escuchar el audio, nos centramos en el enunciado, el cual dice que un ***espectro*** ha poseído a Josefina.

Una forma muy común de ver mensajes ocultos en audios es a través del espectograma de éste.

Para ellos vamos a utilizar la herramienta ***Audacity***. Esta herramienta puede instalarse desde [Audacity Download](https://www.audacityteam.org/download/).

Una vez instalado, si estas en Linux se te habrá descargado un ejecutable al que habrá que darle permisos de ejecución mediante:

>     $ chmod 700 audacity-linux-3.2.1-x64.AppImage

Después ejecutamos:

>     $ ./audacity-linux-3.2.1-x64.AppImage

Una vez dentro de audacity, importamos [psicofonia.wav](https://github.com/ZeN1xX/ctf-writeups/blob/main/sugus-ctf/Psicofonia-Maldita/psicofonia.wav) y cambiamos el formato de visión a **espectograma** puslando *'Shift + M'* y pulsando la forma de ***especograma***.

Debería presentarse una imagen del estilo a esta:

![Espectograma](https://user-images.githubusercontent.com/114481026/223090866-030385fa-af74-4197-963e-2f4c797632ea.png)

Donde se puede ver ya el formato flag buscado. Solamente habría que rotar los caracteres hasta la posición en la que la flag se encuentre adecuadamente.

Concretamente con la opción ROT13 de [CyberChef](https://gchq.github.io/CyberChef/)
nos devuelve la rotación de 13 caracteres, obteniendo así el formato de la flag correcto.

> ***SUGUS{3sCuCha_C0n_7u5_0jo5}***
