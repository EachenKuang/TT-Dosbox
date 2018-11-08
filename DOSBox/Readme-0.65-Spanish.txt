DOSBox v0.65


====
NOTA
====

Aunque esperamos que algún día DOSBox pueda ejecutar cualquier programa hecho
para PC, todavía no estamos en ese punto. Actualmente, DOSBox en un equipo tope
de gama se aproxima a un 486. La versión 0.60 ha añadido soporte para
"modo protegido", permitiendo la emulación de programas más recientes y complejos,
pero hay que tener en cuenta que este soporte todavía está en fase de desarrollo y
al contrario que el soporte de juegos en "modo real" para 386 (o anteriores) todavía
no está completo. También es de notar que los juegos en "modo protegido" necesitan
bastantes más recursos y pueden necesitar un procesador mucho más rapido para
emularlos correctamente en DOSBox.



======
INDICE
======
 1. Inicio rápido
 2. Preguntas frecuentes
 3. Uso
 4. Comandos internos
 5. Teclas especiales
 6. Asignador de teclas
 7. Requisitos del sistema
 8. Ejecutar juegos que necesitan muchos recursos
 9. El archivo config
10. El archivo de idioma
11. Haciendo tu propia versión de DOSBox
12. Agradecimientos Especiales
13. Contacto


================
1. Inicio rápido
================

Teclea INTRO dentro de DOSBox. Eso es todo. 


=======================
2. Preguntas frecuentes
=======================

Algunas Preguntas Frecuentes:

Q: Tengo una Z en vez de una C como prompt.
Q: Mi juego se cuelga al usar opengl/nb o es mucho más lento.
Q: Mi CD-ROM no funciona.
Q: El ratón no funciona.
Q: El sonido se entrecorta o suena extraño.
Q: No puedo escribir \ o : en DOSBox.
Q: El juego/aplicación no puede encontrar su CD-ROM.
Q: ¡El juego/aplicación funciona muy lento!
Q: Me gustaría cambiar la memoria/velocidad de procesador/EMS/SoundBlaster IRQ.
Q: ¿Qué hardware de sonido emula actualmente DOSBox?
Q: DOSBox se cuelga al arrancar y estoy ejecutando arts.
Q: Gran LEEME, pero todavía no lo cojo.





Q: Tengo una Z en vez de una C como prompt.
A: Debes hacer que tus directorios estén disponibles como unidades en DOSBox
   usando el comando "mount". Por ejemplo, en Windows "mount C D:\JUEGOS" te
   dará una unidad C en DOSBox que apunta a tu directorio de windows D:\JUEGOS.
   En Linux, "mount c /home/usuario" te dara una unidad C dentro de DOSBox que
   apunta a /home/usuario en Linux.


Q: Mi juego se cuelga al usar opengl/nb o es mucho más lento.
A: Por alguna razón nuestro código opengl no es completamente estable en algunas
   plataformas. Usa el metodo "surface" en su lugar.


Q: Mi CD-ROM no funciona.
A: Para montar tu CD-ROM en DOSBox debes especificar algunas opciones adicionales
   al montar el CD-ROM.
   Para activar el soporte de CD-ROM más básico:
     - mount d f:\ -t cdrom
   Para activar soporte de bajo nivel SDL:
     - mount d f:\ -t cdrom -usecd 0
   Para activar soporte de bajo nivel ioctl(win2k/xp/linux):
     - mount d f:\ -t cdrom -usecd 0 -ioctl
   Para activar soporte de bajo nivel aspi (win98 con capa aspi instalada):
     - mount d f:\ -t cdrom -usecd 0 -apsi
   
   En los comandos: - d   letra de unidad que obtendrás en DOSBox
                    - f:\ ubicación del cdrom en tu ordenador.
                    - 0   el número de la unidad de CD-ROM, devuelto por mount -cd
   Echa un vistazo también a la pregunta: El juego/aplicación no puede encontrar su CD-ROM.


Q: El ratón no funciona.
A: Normalmente, DOSBox detecta cuando un juego se maneja con ratón. Al pulsar sobre
   la pantalla debería ser capturado (confinado a la ventana de DOSBox) y funcionar.
   Con algunos juegos, la detección de ratón no funciona. En este caso deberás capturar
   el ratón manualmente pulsando CTRL-F10.


Q: El sonido se entrecorta o suena extraño.
A: Estás usando demasiada potencia de procesador para mantener DOSBox funcionando
   a la velocidad actual. Puedes disminuir los ciclos, usar un frameskip mayor o
   conseguir un ordenador más rapido. También puedes incrementar el "prebuffer"
   en el archivo de configuración.


Q: No puedo escribir \ o : en DOSBox.
Nota del traductor: Esto ocurre cuando se usa un teclado que no es estadounidense.
Si tienes un teclado español (esto es, de España), prueba estas teclas:

Carácter   Teclado español
   \         <
   /         -
   *         (
   -         '
   :         Ñ

A: Este problema ocurre si la disposición de tu teclado no es la estadounidense.
   Algunas soluciones posibles:
   1. Cambia la disposición de tu teclado.
   2. Usa la barra normal / en lugar de la invertida.
   3. Abre dosbox.conf y cambia usescancodes=false por usescancondes=true.
   4. Añade los comandos que quieras ejecutar al archivo de configuración.
   5. Inicia el asignador de teclas (CTRL-F1 o añade el argumento -startmapper a DOSBox).
   6. Usa ALT-58 para : y ALT-92 para \.
   7. Para la \ prueba las teclas alrededor del Enter. Para los : prueba con las
      teclas entre el Enter y la "l" mientras mantienes pulsada la tecla Shift.
   8. Usa el keyb.com de FreeDOS (http://projects.freedos.net/keyb).


Q: El juego/aplicación no puede encontrar su CD-ROM.
A: Asegurate de montar el CD-ROM con el argunmento -t cdrom. Prueba también añadiendo
   la etiqueta correcta (-label ETIQUETA). Para activar soporte a bajo nivel del CD-ROM,
   añade el siguiente argumento a mount: -usecd #, donde # es el número de tu unidad de
   CD-ROM (puedes verlo con mount -cd). Si usas Win32 puedes especificar -ioctl o -aspi.
   Busca la descripción en este documento para ver su significado.


Q: ¡El juego/aplicación funciona muy lento!
A: Echa un vistazo a la sección sobre ejecución de juegos que requieren muchos recursos.


Q: Me gustaría cambiar la memoria/velocidad de procesador/EMS/SoundBlaster IRQ.
A: ¡Se puede hacer! Simplemente crea un archivo de configuración:
   config -writeconf archivo .
   Arranca tu editor favorito y mira todas las opciones. Para arrancar DOSBox con
   la nueva configuración: dosbox -conf archivo-de-configuración.


Q: ¿Qué hardware de sonido emula actualmente DOSBox?
A: DOSBox emula varios dispositivos de sonido antiguos:
   - Altavoz interno del PC (PC Speaker)
     Esta emulación incluye el generador de tonos y también varias formas de
     salida de sonido digital a través del PC Speaker.
   - Creative CMS / GameBlaster
     La primera tarjeta de Creative Labs(R). La configuración por defecto la sitúa
     en el puerto 0x220. Ten en cuenta que activar esto a la vez que emulación Adlib
     puede generar conflictos.
   - Voz Tandy 3
     La emulación de este sistema es completa con la excepción del canal de ruido.
     El canal de ruido no está muy bien documentado, por lo que la precisión del
     sonido es solo una aproximación.
   - Adlib
     Tomado prestado del MAME, esta emulación es casi perfecta e incluye la capacidad
     de la Adlib de casi reproducir sonido digitalizado.
   - SoundBlaster 16/soundBlaster Pro I y II/SoundBlaster I y II
     Por defecto DOSBox emula SoundBlaster 16 con sonido stereo 16 bits.
     Puedes seleccionar una versión distinta de SoundBlaster el el archivo de
     configuración (ver comandos internos: CONFIG).
   - Disney Sound Source
     Usando el puerto de impresora, este dispositivo de sonido solo produce sonido
     digital.
   - Gravis Ultrasound
     La emulación de este dispositivo está casi acabada, a pesar de que se ha dejado
     de lado la capacidad MIDI, pues ya hay emulado un MPU-401.
   - MPU-401
     También hay emulada una interfaz MIDI. Este método de salida de sonido solo
     funciona cuando se usa con un dispositivo General Midi o MT-32.
     

Q: DOSBox se cuelga al arrancar y estoy ejecutando arts.
A: Este no es realmente un problema de DOSBox, pero la solución es es establecer
   el valor de la variable de entorno SDL_AUDIODRIVER a alsa u oss.


Q: Gran LEEME, pero todavía no lo cojo.
A: Aunque extraño, parece que puede ocurrir. Puede que un vistazo a "La guía gráfica
   de DOSBox para principiantes" (en inglés) te sirva de ayuda. Puedes encontrarlo en
   http://vogons.zetafleet.com/viewforum.php?f=39
   También podrías probar con el wiki de dosbox:
   http://dosbox.sourceforge.net/wiki/


Para otras preguntas lee el resto de este LEEME y/o comprueba el sitio/foro:
http://dosbox.sourceforge.net




======
3. Uso
======

Un vistazo a las opciones de la línea de comandos que puedes dar a DOSBox.
Los usuarios de Windows deben abrir cmd.exe o command.com o editar el acceso
directo a DOSBox para esto.
Las opciones son válidas para todos los sistemas operativos a no ser que se diga
lo contrario en la descripción de la opción:

dosbox [nombre] [-exit] [-c comando] [-fullscreen] [-conf archivo-de-configuración] 
       [-lang archivo-de-idioma] [-machine tipo-de-máquina] [-noconsole]
       [-startmapper] [-noautoexec]
       
dosbox -version

  name   
        Si "nombre" es un directorio se montará como unidad C:
        Si "nombre" es un ejecutable se montará su directorio como C:
        y se ejecutará "nombre".
    
  -exit  
        DOSBox se cerrará cuando la aplicación "nombre" termine su ejecución.

  -c command
        Ejecuta el comando especificado antes de ejecutar "nombre". Se pueden
        especificar varios comandos, poniendo a cada uno la opción "-c".
        Un comando puede ser un programa interno, un comando DOS o un ejecutable
        en una unidad montada.

  -fullscreen
        Arranca DOSBox en modo de pantalla completa.

  -conf archivo-de-configuración
        Arranca DOSBox con las opciones definidas en "archivo-de-configuración".
        Ver el Capítulo 9 para más detalles.

  -lang archivo-de-idioma
        Arranca DOSBox usando el idioma especificado en "archivo-de-idioma".

  -noconsole (Solo Windows)
        Lanza DOSBox sin mostrar la ventana de la consola. La salida será
        redirigida a stdout.txt y stderr.txt.
	
  -machine tipo-de-máquina
        Configura DOSBox para emular un tipo concreto de máquina. Los tipos
        válidos son: hercules, cga, pcjr, tandy, vga (opción por defecto).
        El tipo de máquina afecta a la tarjeta gráfica y a las tarjetas de
        sonido disponibles.

  -startmapper
        Entra en el asignador de teclas directamente al arrancar. Util
        cuando tienes problemas con el teclado.

  -noautoexec
        Ignora la sección [autoexec] del archivo de configuración.

  -version
        Muestra información sobre la versión y sale. Util para los
        frontends.

Nota: Si un nombre/comando/archivo-de-configuración/archivo-de-idioma contiene un
      espacio, escríbelo entre comillas ("").

Por ejemplo:

dosbox c:\atlantis\atlantis.exe -c "MOUNT D C:\PARTIDAS"
  Monta C:\atlantis como C: y ejecuta atlantis.exe
  Antes de hacerlo monta C:\PARTIDAS como unidad D:.

En Windows, también puedes arrastrar directorios/archivos sobre el ejecutable
de DOSBox.



====================
4. Comandos internos
====================

DOSBox soporta la mayoría de los comandos de DOS internos al command.com.
Además, están disponibles los siguientes comandos: 

MOUNT "Letra de la Unidad Emulada" "Unidad o Directorio Real" 
      [-t tipo] [-aspi] [-ioctl] [-usecd número] [-size tamaño] 
      [-label etiqueta] [-freesize tamaño_en_Mb]
MOUNT -cd
MOUNT -u "Letra de la Unidad Emulada"

  Programa para montar directorios locales como unidades dentro de DOSBox.

  "Letra de la Unidad Emulada"
        La letra de la unidad dentro de DOSBox (Por ejemplo, C).

  "Unidad o Directorio Real"
        El directorio local que quieres tener disponible en DOSBox
        (Por ejemplo: mount c c:\juegos).

  -t tipo
        Tipo del directorio montado. Los soportados son: dir (estándar),
        floppy, cdrom.

  -size tamaño
        Establece el tamaño de la unidad.

  -freesize tamaño_en_Mb
        Establece la cantidad de espacio libre disponible en la unidad en Mb.
        Es una versión más simple de -size.

  -label etiqueta
        Establece el nombre de la unidad a "etiqueta". Es necesario en algunos
        sistemas si la etiqueta del CD no se lee correctamente. Util cuando un
        programa no puede encontrar su CD-ROM. Si no especificas una etiqueta y
        el soporte de bajo nivel no está activado (-usecd # y/o -ioctl/aspi):
          En Windows la etiqueta es extraida de la "Unidad Real".
          En Linux la etiqueta se establece en NO_LABEL.

        Si especificas una etiqueta, esta se mantendrá mientras la unidad esté
        montada. ¡No se actualizará!
        
  -aspi
        Fuerza el uso de la capa ASPI. Solo es válida al montar un CD-ROM en
        sistemas Windows con la capa ASPI instalada.

  -ioctl   
        Fuerza el uso de comandos ioctl. Solo es válida al montar un CD-ROM en
        sistemas WINDOWS que los soporten (Win2000/XP/NT).

  -usecd número
        Fuerza el uso de soporte de CD-ROM SDL para la unidad cuyo número se
        especifica. Se puede ver el número correspondiente ejecutando el comando
        mount -cd. Válido en todos los sistemas.

  -cd
        Muestra todas las unidades de CD detectadas y sus números. Para usar
        junto con mount -usecd.

  -u
        Desmonta una unidad. No funciona con Z:.

  Nota: Es posible montar un directorio local como unidad de CD, pero entonces
        no es posible el soporte a bajo nivel.

  Básicamente, MOUNT permite conectar hardware real al ordenador "emulado" en
  DOSBox. Así, MOUNT C C:\JUEGOS le dice a DOSBox que use el directorio C:\JUEGOS
  como la unidad C: en DOSBox. Tambien permite cambiar la letra de una unidad para
  aquellos programas que requieren una letra de unidad específica.
  
  Por ejemplo: "Touche: Las Aventuras del Quinto Mosquetero" debe ejecutarse desde
  la unidad C:. Usando DOSBox y el comando mount, puedes engañar al juego para que
  crea que está en la unidad C, y ponerlo en realidad donde tú quieras. Por ejemplo,
  si el juego está en D:\TOUCHE, el comando MOUNT C D:\ te permitirá ejecutar
  Touche desde la unidad D:.
  
  ¡No es recomendable montar la unidad C: entera con MOUNT C C:\!
  Si hay un error en DOSBox o comentes un fallo, podrías perder todos tus archivos.
  Es recomendable poner todos tus juegos/aplicaciones en un subdirectorio y montarlo.
  
  Ejemplos generales de MOUNT:
  1. Para montar c:\DirX como un disquete: 
       mount a c:\DirX -t floppy
  2. (Windows) Para montar la unidad de cd E como unidad de cd D en DOSBox:
       mount d e:\ -t cdrom
  3. (Linux) Para montar la unidad de cd en /media/cdrom como unidad D en DOSBox:
       mount d /media/cdrom -t cdrom -usecd 0
  4. Para montar una unidad con 870 Mb de espacio libre (version simple):
       mount c d:\ -freesize 870
  5. Para montar una unidad con 870 Mb de espacio libre (solo expertos, control total):
       mount c d:\ -size 4025,127,16513,1700
  6. (Linux) Para montar /home/user/dirY como unidad C en DOSBox:
       mount c /home/user/dirY

MEM
  Programa para mostrar la cantidad de memoria libre.

CONFIG [-writeconf] [-writelang] archivo-local
CONFIG -set "propiedad=valor"
CONFIG -get "propiedad"

  Se puede usar CONFIG para cambiar o averiguar la configuración de DOSBox
  durante su ejecución. Puede grabar la configuración actual y el texto del
  idioma actual en disco. Puedes encontrar información sobre todas las
  secciones del archivo de configuración y sus propiedades en la
  sección 9 (El Archivo de Configuración).

  -writeconf archivo-local
       Guarda la configuración actual en un archivo, "archivo-local", en la
       unidad local, no en una unidad montada de DOSBox. El archivo de
       configuración controla diversas opciones de DOSBox:
       La cantidad de memoria emulada, las tarjetas de sonido emuladas y muchas
       otras cosas. Tambien permite acceso al AUTOEXEC.BAT. Ver la
       s ección 9 (El Archivo de Configuración) para más información.

  -writelang archivo-local
       Escribe el texto del idioma actual a un archivo situado en el disco duro
       local, no en una unidad montada en DOSBox. El archivo de idioma controla
       toda la salida visible de los comandos internos y del DOS interno.

  -set "propiedad=valor"
       CONFIG tratara de establecer el nuevo valor para la propiedad. Actualmente
       CONFIG no puede informar de si el comando tuvo éxito o no.

  -get "propiedad"
       El valor actual de la propiedad es devuelto y almacenado en la variable
       de entorno %CONFIG%. Puede usarse para almacenar el valor al trabajar con
       archivos por lotes.

  Tanto "-set" como "-get" funcionan en archivos por lotes y pueden usarse para
  establecer tus propias preferencias para cada juego.
  
  Ejemplos:
  1. Para crar un archivo de configuración en tu directorio actual:
      config -writeconf dosbox.conf
  2. Para establecer los ciclos del procesador a 10000:
      config -set "cpu cycles=10000"
  3. Para desactivar la emulación de memoria EMS:
      config -set "dos ems=off"
  4. Para comprobar qué núcleo del procesador se está usando:
      config -get "cpu core"

LOADFIX [-size] [programa] [parametros-del-programa]
LOADFIX -f
  Programa para reducir la cantidad de memoria disponible. Util para viejos
  programas que no esperan encontrar mucha memoria libre.

  -size	        
        número de kb a "comerse", por defecto 64kb
  
  -f
        libera toda la memoria reservada anteriormente
  

Ejemplos:
  1. Para iniciar mm2.exe y reservar 64 kb de memoria
     (mm2 tendrá 64 kb menos de memoria disponible):
     loadfix mm2
  2. Para iniciar mm2.exe y reservar 32 kb de memoria:
     loadfix -32 mm2
  3. Para liberar la memoria reservada anteriormente:
     loadfix -f


RESCAN
  Hace que DOSBox relea la estructura de directorios. Util si has cambiado algo
  de una unidad montada desde fuera de DOSBox. (CTRL - F4 también hace lo mismo).
  

MIXER
  Muestra la configuración actual de volumen.
  Así es como puedes cambiarla:
  
  mixer canal izquierda:derecha [/NOSHOW] [/LISTMIDI]
  
  canal
      Puede ser uno de los siguientes: MASTER, DISNEY, SPKR, GUS, SB, FM.
  
  izquierda:derecha
      El nivel de volumen en porcentajes. Si pones una D delante será en 
      decibelios (por ejemplo mixer gus d-10).
  
  /NOSHOW
      Evita mostrar el resultado si cambias alguno de los niveles de volumen.

  /LISTMIDI
      Lista los dispositivos midi disponibles en tu ordenador (Windows). Para
      elegir un dispositivo distinto al asignador-midi por defecto de Windows,
      añade una línea 'config=id' a la sección [midi] del archivo de configuración,
      donde 'id' es el número del dispositivo listado por LISTMIDI.


IMGMOUNT
  Una utilidad para montar imágenes de disco y de CD-ROM en DOSBox.
  
  IMGMOUNT DRIVE [imagen] -t [tipo_de_imagen] -fs [formato] 
            -size [bytes_por_sector, sectores_por_cabezal, cabezales, cilindros]

  imagen
      Ubicación del archivo de imagen a montar en DOSBox. La ubicación se
      refiere a una unidad montada dentro de DOSBox. Las imágenes de CD-ROM
      pueden montarse directamente, no tienen por qué encontrarse dentro de
      una unidad montada.
   
  -t 
      Los siguientes son tipos válidos de imagen:
        floppy: Especifica una imagen de disquete.  DOSBox identificará automáticamente 
                la geometría del disco (360K, 1.2MB, 720K, 1.44MB, etc).
        iso:    Especifica una imagen ISO de CD-ROM.  La geometría es automática para
                este tamaño. Puede ser una ISO o un CUE/BIN.
        hdd:    Especifica una imagen de disco duro. Es necesario añadir la geometría
                correcta (cilindros, cabezas y sectores) para que funcione.

  -fs 
      Los siguiente son tipos válidos de sistemas de ficheros:
        iso:  Especifica el formato de CD-ROM ISO-9660.
        fat:  Especifica que la imagen usa el sistema de ficheros FAT. DOSBox
              tratara de montar esta imagen como una unidad y hacer los ficheros
              disponibles dentro de DOSBox.
        none: Dosbox no intentará leer el sistema de archivos del disco. Esto
              puede ser util si necesitas formatearlo o si quieres arrancarlo
              usando el comando BOOT. Al usar el sistema de ficheros "none", debes
              especificar el número de la unidad (2 ó 3, donde 2 = maestro, 3 = esclavo)
              en vez de una letra de unidad.
              Por ejemplo, para montar una imagen de 70MB como la unidad esclava,
              se escribiría:
                "imgmount 3 d:\prueba.img -size 512,63,16,142 -fs none"
                (sin las comillas)  Compara esto con un mount para leer la
                unidad en DOSBox, que sería:
                "imgmount e: d:\prueba.img -size 512,63,16,142"

  -size 
     La especificación de los cilindros, cabezales y sectores de la unidad.
     Necesarios para montar imágenes de disco duro.
     
  Un ejemplo de imagen de CD-ROM:
    1a. mount c /tmp
    1b. imgmount d c:\miiso.iso -t iso
  o también:
    2. imgmount d /tmp/miiso.iso -t iso


BOOT
  Boot arrancará imágenes de disco duro o disquete independientes de la
  emulación del sistema operativo ofrecida por DOSBox. Esto hace posible
  jugar a juegos en disquetes autoarrancables o arrancar otros sistemas
  operativos dentro de DOSBox.

  BOOT [imagen1.img imagen2.img .. imagenN.img] [-l letra-de-unidad]

  imagenN.img 
     Esto puede ser cualquier número de imágenes de disquete que se quieran
     tener montadas después de que DOSBox arranque desde la unidad especificada.
     Para cambiar de imagen, pulsa CTRL-F4 para pasar a la siguiente de la lista.
     Una vez alcanzada la última, se volverá a la primera imagen.

  [-l letra-de-unidad]
     Este parametro permite especificar la unidad desde la que arrancar.
     La unidad por defecto es A, la unidad de disquetes. También se puede arrancar
     una imagen de disco duro montada como unidad maestra especificando "-l C", sin
     las comillas, o una unidad esclava con "-l D".


IPX

  Debes activar el protocolo de red IPX en el archivo de configuración de DOSBox.

  Todo el sistema de red por IPX es gestionado a través del programa interno de
  DOSBox IPXNET. Para ver la ayuda sobre IPX dentro de DOSBox, escribe
  "IPXNET HELP" (sin las comillas) y el programa listará los comandos y su
  documentación correspondiente.

  Respecto a la puesta en funcionamiento de una red, un sistema debe hacer de servidor.
  Para ello, escribe "IPXNET STARTSERVER" (sin las comillas) en una sesión de DOSBox.
  El servidor se añadirá automáticamente a si mismo a la red IPX virtual. Para cada
  equipo adicional que se quiera forme parte de la red, necesitarás escribir
  "IPXNET CONNECT <nombre o IP del servidor>". Por ejemplo, si tu servidor se encuentra
  en bob.dosbox.com, deberías escribir "IPXNET CONNECT bob.dosbox.com" en cada equipo
  distinto al servidor.
  
  La siguiente es una referencia de comandos de IPXNET:

  IPXNET CONNECT 

     IPXNET CONNECT abre una conexión a un servidor IPX (encapsulado)
     ejecutandose en otra sesión de DOSBox. El parámetro "dirección"
     especifica la dirección IP o nombre del ordenador servidor. También
     puedes especificar el puerto UDP a usar. Por defecto IPXNET usa el
     puerto 213 (El puerto asignado por la IANA para el encapsulado de IPX)
     para la conexión.

     La sintaxis de IPXNET CONNECT es: 
     IPXNET CONNECT dirección <puerto> 

  IPXNET DISCONNECT 

     IPXNET DISCONNECT cierra la conexión al servidor IPX. 

     La sintaxis de IPXNET DISCONNECT es: 
     IPXNET DISCONNECT 

  IPXNET STARTSERVER 

     IPXNET STARTSERVER inicia un servidor IPX (encapsulado) en la sesión actual
     de DOSBox. Por defecto, el servidor aceptará conexiones en el puerto UDP 213,
     aunque esto se puede cambiar. Una vez iniciado el servidor, DOSBox iniciará
     automáticamente una conexión cliente al servidor.

     La sintaxis de IPXNET STARTSERVER es:
     IPXNET STARTSERVER <puerto>

  IPXNET STOPSERVER

     IPXNET STOPSERVER detiene el servidor IPX que esté ejecutandose en la sesión
     actual de DOSBox. Hay que tener cuidado y asegurarse de que no haya conexiones
     activas en el momento de detener el servidor, pues esto podría provocar
     cuelgues en las máquinas que todavía lo estén usando.

     La sintaxis de IPXNET STOPSERVER es: 
     IPXNET STOPSERVER 

  IPXNET PING

     IPXNET PING transmite una petición de ping a través de la red IPX
     (encapsulada). Todas las demás maquinas conectadas a la red responderán
     a la petición e informarán del tiempo de respuesta.

     La sintaxis de IPXNET PING es: 
     IPXNET PING

  IPXNET STATUS

     IPXNET STATUS informa sobre el estado actual de la red IPX (encapsulada)
     en esta sesión de DOSBox. Para obtener una lista de todos los ordenadores
     conectados a la red usa el comando IPXNET PING.

La sintaxis de IPXNET STATUS es: 
IPXNET STATUS 

Para más información sobre alguno de los comandos usa el parametro /? con dicho
comando.




====================
5. Teclas especiales
====================

ALT-ENTER     Cambiar entre el modo ventana y pantalla completa.
ALT-PAUSE     Hacer una pausa en la emulación.
CTRL-F1       Iniciar el asignador de teclas.
CTRL-F4       Cambiar entre imágenes de disco montadas.
              ¡También Actualiza la caché de directorio de todas las unidades!
CTRL-F5       Grabar una captura de la pantalla (png).
CTRL-ALT-F5   Comenzar/Detener la grabación de un video de la pantalla.
CTRL-F6       Comenzar/Detener la grabación de la salida de sonido a un fichero.
CTRL-ALT-F7   Comenzar/Detener la grabación de los comandos OPL.
CTRL-ALT-F8   Comenzar/Detener la grabación de comandos MIDI sin procesar.
CTRL-F7       Decrementar el frameskip.
CTRL-F8       Incrementar el frameskip.
CTRL-F9       Detener dosbox.
CTRL-F10      Capturar/Liberar el ratón.
CTRL-F11      Ralentizar la emlación (Decrementa los ciclos de DOSBox).
CTRL-F12      Acelerar la emulación (Incrementa los ciclos de DOSBox).
ALT-F12       Desactiva el limitador de velocidad (botón turbo).

Estas son las asignaciones de teclas por defecto. Pueden cambiarse usando
el asignador de teclas.

Los ficheros grabados pueden encontrarse en directorio_actual/capture
(puede cambiarse en el archivo de configuración).
El directorio debe existir antes de iniciar DOSBox, ¡


NOTA: Una vez incrementas los ciclos de DOSBox hasta alcanzar el límite
      de tu ordenador, seguir aumentandolos solo producira el efecto
      contrario, ralentizará la emulación. El límite varía de un
      ordenador a otro, y depende de cada configuración hardware y
      software concreta.



======================
6. Asignador de teclas
======================

Cuando inicias el asignador (bien con CTRL-F1 o el parametro -startmapper
en la línea de comandos al lanzar DOSBox) aparece un teclado virtual.

Este teclado se corresponde con las pulsaciones de teclas que DOSBox enviará
a los programas. Si pulsas sobre una tecla con el ratón, puedes ver en la
esquina inferior izquierda a que tecla de tu teclado real corresponde.

Event: EVENTO
BIND: ASIGNACIÓN
                        Add   Del
mod1  hold                    Next
mod2
mod3


EVENTO
    La tecla que DOSBox enviará a los programas que se estén emulando.
ASIGNACIÓN
    La tecla de tu teclado (tal como informe SDL) que está conectada al EVENTO.
mod1,2,3 
    Modificadores. Son teclas que también deben estar presionadas al presionar
    ASIGNACIÓN. mod1 = CTRL y mod2 = ALT. Normalmente solo se usan si se quieren
    cambiar las teclas especiales de DOSBox.
Add 
    Añade una nueva ASIGNACIÓN a este EVENTO. Basicamente hace que una tecla del
    teclado real produzca el EVENTO en DOSBox.
Del 
    Elimina la ASIGNACIÓN a este EVENTO. Si un EVENTO no tiene ASIGNACIONES,
    no se podrá pulsar esta tecla en DOSBox.
Next
    Recorrer la lista de teclas(ASIGNACIONES) que corresponden a este EVENTO.


Ejemplo:
Q1. Quieres que la X de tu teclado escriba una Z en DOSBox.
A.  Haz click sobre la Z en el teclado virtual. Pulsa "Add", y a
    continuación pulsa la X en tu teclado.

Q2. Si haces click sobre "Next" un par de veces, verás que la Z de tu teclado
    también produce una Z en DOSBox.
A.  Por lo tanto, selecciona de nuevo la Z, pulsa "Next" hasta que tengas la
    Z en tu teclado y entonces pulsa "Del".

Q3. Al probar la asignación en DOSBox y pulsar la X, en la pantalla aparece ZX.
A.  ¡La X de tu teclado todavía está asignada a la X también! Haz click en la X
    del teclado virtual y busca con "Next" hasta que encuentres la tecla asignada
    X. Pulsa en "Del".


Si modificas las asignaciones por defecto, puedes guardar tus cambios pulsando
"Save". DosBox guardará las asignaciones en la ubicación especificada en el
archivo de configuración (mapperfile=mapper.txt). Al inicio, DOSBox cargará
tu archivo de asignaciones, si está presente en el archivo de configuración.



=========================
7. Requisitos del sistema
=========================

Un equipo rápido. Yo diría que que un Pentium II 400 o más para obtener una
emulación decente de juegos escritos para 286.
Para juegos de modo protegido un equipo de al menos 1Ghz de velocidad es
recomendable. ¡Pero no esperes que funcionen muy rápido! Asegurate de leer
la sección siguiente sobre como acelerarlos en la medida de lo posible.



================================================
8. Ejecutar juegos que necesitan muchos recursos
================================================

DOSBox emula el procesador, la tarjeta gráfica y la de sonido, y algunas otras
cosas, todo a la vez. Puedes acelerar DOSBox pulsando CTRL-F12, pero estarás
limitado por la potencia de tu procesador real. Puedes ver la ocupación de tu
procesador usando el Administrador de Tareas en Windows 2000/XP o el 
Monitor del Sistema en Windows 9x/Me. Una vez el uso del procesador alcanza el
100% no hay otra manera de acelerar DOSBox a no ser que reduzcas la carga generada
por otros subsistemas distintos al procesador.

Así que: 

Cierra todos los programas que se estén ejecutando

Acelera DOSBox hasta que el uso de tu procesador sea del 100%

Ya que la emulación VGA es la parte de DOSBox que mas recursos requiere en terminos
de uso de procesador real, empieza por ahí. Aumenta el frameskip (de uno en uno)
pulsando CTRL-F8. El uso de procesador debería disminuir. Vuelve un paso atras y
repite esto hasta que el juego funcione lo suficientemente rápido.
Por favor, ten en cuenta que esto tiene su parte negativa: perderás fluidez de video
para ganar en velocidad

También puedes probar desactivando el sonido a traves de la utilidad de configuración
del juego para reducir la carga del procesador un poco más.



====================
9. El archivo config
====================

CONFIG.COM puede generar un archivo de configuración, que puedes encontrar
en la unidad Z: dentro de DOSBox. Mira en la sección de comandos internos
del leeme si quieres saber como se usa CONFIG.COM.
Puedes editar este archivo de configuración para personalizar DOSBox.

El archivo está dividido en diversas secciónes (los nombres llevan [] alrededor).
Algunas secciones tienen opciones que puedes modificar.
# y % indican líneas de comentarios.
El archivo de configuración generado contiene la configuración actual. Puedes
modificarla y lanzar DOSBox con el argumento -conf para cargar el archivo y usar
esa configuración.

Si no se especifica un archivo de configuración, DOSBox buscara el archivo dosbox.conf
en el directorio actual. Después buscara ~/.dosboxrc (Linux), ~\Dosbox.conf (Win32) o
"~/Library/Preferences/DOSBox Preferences" (MACOSX).



========================
10. El archivo de idioma
========================

CONFIG.COM puede generar un archivo de idioma.
Leelo, y seguramente entiendas como cambiarlo.
Arranca DOSBox con el argumento -lang para usar tu nuevo archivo de idioma.
También, puedes configurar el nombre del archivo en el archivo de configuración
en la sección [dosbox]. Hay una entrada language= que puedes cambiar.



========================================
11. Haciendo tu propia versión de DOSBox
========================================

Descarga los archivos fuente.
Comprueba el archivo INSTALL que se incluye.



==============================
12. Agradecimientos especiales
==============================

Vlad R. del proyecto VDMSound por su excelente información sobre la SoundBlaster.
Tatsuyuki Satoh del Equipo Mame por hacer un excelente emulador FM.
Los proyectos Bochs y DOSemu, que usé para obtener información.
Freedos por las ideas para mi intérprete de comandos.
Pierre-Yves Gérardy por albergar el antiguo tablón de anuncios.
Colin Snover por albergar nuestro foro.
Los Beta Testers.



============
13. Contacto
============

Visita el sitio: 
http://dosbox.sourceforge.net
Allí puedes ver la dirección de correo electrónico (The Crew-page).
