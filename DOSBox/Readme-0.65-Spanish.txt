DOSBox v0.65


====
NOTA
====

Aunque esperamos que alg�n d�a DOSBox pueda ejecutar cualquier programa hecho
para PC, todav�a no estamos en ese punto. Actualmente, DOSBox en un equipo tope
de gama se aproxima a un 486. La versi�n 0.60 ha a�adido soporte para
"modo protegido", permitiendo la emulaci�n de programas m�s recientes y complejos,
pero hay que tener en cuenta que este soporte todav�a est� en fase de desarrollo y
al contrario que el soporte de juegos en "modo real" para 386 (o anteriores) todav�a
no est� completo. Tambi�n es de notar que los juegos en "modo protegido" necesitan
bastantes m�s recursos y pueden necesitar un procesador mucho m�s rapido para
emularlos correctamente en DOSBox.



======
INDICE
======
 1. Inicio r�pido
 2. Preguntas frecuentes
 3. Uso
 4. Comandos internos
 5. Teclas especiales
 6. Asignador de teclas
 7. Requisitos del sistema
 8. Ejecutar juegos que necesitan muchos recursos
 9. El archivo config
10. El archivo de idioma
11. Haciendo tu propia versi�n de DOSBox
12. Agradecimientos Especiales
13. Contacto


================
1. Inicio r�pido
================

Teclea INTRO dentro de DOSBox. Eso es todo. 


=======================
2. Preguntas frecuentes
=======================

Algunas Preguntas Frecuentes:

Q: Tengo una Z en vez de una C como prompt.
Q: Mi juego se cuelga al usar opengl/nb o es mucho m�s lento.
Q: Mi CD-ROM no funciona.
Q: El rat�n no funciona.
Q: El sonido se entrecorta o suena extra�o.
Q: No puedo escribir \ o : en DOSBox.
Q: El juego/aplicaci�n no puede encontrar su CD-ROM.
Q: �El juego/aplicaci�n funciona muy lento!
Q: Me gustar�a cambiar la memoria/velocidad de procesador/EMS/SoundBlaster IRQ.
Q: �Qu� hardware de sonido emula actualmente DOSBox?
Q: DOSBox se cuelga al arrancar y estoy ejecutando arts.
Q: Gran LEEME, pero todav�a no lo cojo.





Q: Tengo una Z en vez de una C como prompt.
A: Debes hacer que tus directorios est�n disponibles como unidades en DOSBox
   usando el comando "mount". Por ejemplo, en Windows "mount C D:\JUEGOS" te
   dar� una unidad C en DOSBox que apunta a tu directorio de windows D:\JUEGOS.
   En Linux, "mount c /home/usuario" te dara una unidad C dentro de DOSBox que
   apunta a /home/usuario en Linux.


Q: Mi juego se cuelga al usar opengl/nb o es mucho m�s lento.
A: Por alguna raz�n nuestro c�digo opengl no es completamente estable en algunas
   plataformas. Usa el metodo "surface" en su lugar.


Q: Mi CD-ROM no funciona.
A: Para montar tu CD-ROM en DOSBox debes especificar algunas opciones adicionales
   al montar el CD-ROM.
   Para activar el soporte de CD-ROM m�s b�sico:
     - mount d f:\ -t cdrom
   Para activar soporte de bajo nivel SDL:
     - mount d f:\ -t cdrom -usecd 0
   Para activar soporte de bajo nivel ioctl(win2k/xp/linux):
     - mount d f:\ -t cdrom -usecd 0 -ioctl
   Para activar soporte de bajo nivel aspi (win98 con capa aspi instalada):
     - mount d f:\ -t cdrom -usecd 0 -apsi
   
   En los comandos: - d   letra de unidad que obtendr�s en DOSBox
                    - f:\ ubicaci�n del cdrom en tu ordenador.
                    - 0   el n�mero de la unidad de CD-ROM, devuelto por mount -cd
   Echa un vistazo tambi�n a la pregunta: El juego/aplicaci�n no puede encontrar su CD-ROM.


Q: El rat�n no funciona.
A: Normalmente, DOSBox detecta cuando un juego se maneja con rat�n. Al pulsar sobre
   la pantalla deber�a ser capturado (confinado a la ventana de DOSBox) y funcionar.
   Con algunos juegos, la detecci�n de rat�n no funciona. En este caso deber�s capturar
   el rat�n manualmente pulsando CTRL-F10.


Q: El sonido se entrecorta o suena extra�o.
A: Est�s usando demasiada potencia de procesador para mantener DOSBox funcionando
   a la velocidad actual. Puedes disminuir los ciclos, usar un frameskip mayor o
   conseguir un ordenador m�s rapido. Tambi�n puedes incrementar el "prebuffer"
   en el archivo de configuraci�n.


Q: No puedo escribir \ o : en DOSBox.
Nota del traductor: Esto ocurre cuando se usa un teclado que no es estadounidense.
Si tienes un teclado espa�ol (esto es, de Espa�a), prueba estas teclas:

Car�cter   Teclado espa�ol
   \         <
   /         -
   *         (
   -         '
   :         �

A: Este problema ocurre si la disposici�n de tu teclado no es la estadounidense.
   Algunas soluciones posibles:
   1. Cambia la disposici�n de tu teclado.
   2. Usa la barra normal / en lugar de la invertida.
   3. Abre dosbox.conf y cambia usescancodes=false por usescancondes=true.
   4. A�ade los comandos que quieras ejecutar al archivo de configuraci�n.
   5. Inicia el asignador de teclas (CTRL-F1 o a�ade el argumento -startmapper a DOSBox).
   6. Usa ALT-58 para : y ALT-92 para \.
   7. Para la \ prueba las teclas alrededor del Enter. Para los : prueba con las
      teclas entre el Enter y la "l" mientras mantienes pulsada la tecla Shift.
   8. Usa el keyb.com de FreeDOS (http://projects.freedos.net/keyb).


Q: El juego/aplicaci�n no puede encontrar su CD-ROM.
A: Asegurate de montar el CD-ROM con el argunmento -t cdrom. Prueba tambi�n a�adiendo
   la etiqueta correcta (-label ETIQUETA). Para activar soporte a bajo nivel del CD-ROM,
   a�ade el siguiente argumento a mount: -usecd #, donde # es el n�mero de tu unidad de
   CD-ROM (puedes verlo con mount -cd). Si usas Win32 puedes especificar -ioctl o -aspi.
   Busca la descripci�n en este documento para ver su significado.


Q: �El juego/aplicaci�n funciona muy lento!
A: Echa un vistazo a la secci�n sobre ejecuci�n de juegos que requieren muchos recursos.


Q: Me gustar�a cambiar la memoria/velocidad de procesador/EMS/SoundBlaster IRQ.
A: �Se puede hacer! Simplemente crea un archivo de configuraci�n:
   config -writeconf archivo .
   Arranca tu editor favorito y mira todas las opciones. Para arrancar DOSBox con
   la nueva configuraci�n: dosbox -conf archivo-de-configuraci�n.


Q: �Qu� hardware de sonido emula actualmente DOSBox?
A: DOSBox emula varios dispositivos de sonido antiguos:
   - Altavoz interno del PC (PC Speaker)
     Esta emulaci�n incluye el generador de tonos y tambi�n varias formas de
     salida de sonido digital a trav�s del PC Speaker.
   - Creative CMS / GameBlaster
     La primera tarjeta de Creative Labs(R). La configuraci�n por defecto la sit�a
     en el puerto 0x220. Ten en cuenta que activar esto a la vez que emulaci�n Adlib
     puede generar conflictos.
   - Voz Tandy 3
     La emulaci�n de este sistema es completa con la excepci�n del canal de ruido.
     El canal de ruido no est� muy bien documentado, por lo que la precisi�n del
     sonido es solo una aproximaci�n.
   - Adlib
     Tomado prestado del MAME, esta emulaci�n es casi perfecta e incluye la capacidad
     de la Adlib de casi reproducir sonido digitalizado.
   - SoundBlaster 16/soundBlaster Pro I y II/SoundBlaster I y II
     Por defecto DOSBox emula SoundBlaster 16 con sonido stereo 16 bits.
     Puedes seleccionar una versi�n distinta de SoundBlaster el el archivo de
     configuraci�n (ver comandos internos: CONFIG).
   - Disney Sound Source
     Usando el puerto de impresora, este dispositivo de sonido solo produce sonido
     digital.
   - Gravis Ultrasound
     La emulaci�n de este dispositivo est� casi acabada, a pesar de que se ha dejado
     de lado la capacidad MIDI, pues ya hay emulado un MPU-401.
   - MPU-401
     Tambi�n hay emulada una interfaz MIDI. Este m�todo de salida de sonido solo
     funciona cuando se usa con un dispositivo General Midi o MT-32.
     

Q: DOSBox se cuelga al arrancar y estoy ejecutando arts.
A: Este no es realmente un problema de DOSBox, pero la soluci�n es es establecer
   el valor de la variable de entorno SDL_AUDIODRIVER a alsa u oss.


Q: Gran LEEME, pero todav�a no lo cojo.
A: Aunque extra�o, parece que puede ocurrir. Puede que un vistazo a "La gu�a gr�fica
   de DOSBox para principiantes" (en ingl�s) te sirva de ayuda. Puedes encontrarlo en
   http://vogons.zetafleet.com/viewforum.php?f=39
   Tambi�n podr�as probar con el wiki de dosbox:
   http://dosbox.sourceforge.net/wiki/


Para otras preguntas lee el resto de este LEEME y/o comprueba el sitio/foro:
http://dosbox.sourceforge.net




======
3. Uso
======

Un vistazo a las opciones de la l�nea de comandos que puedes dar a DOSBox.
Los usuarios de Windows deben abrir cmd.exe o command.com o editar el acceso
directo a DOSBox para esto.
Las opciones son v�lidas para todos los sistemas operativos a no ser que se diga
lo contrario en la descripci�n de la opci�n:

dosbox [nombre] [-exit] [-c comando] [-fullscreen] [-conf archivo-de-configuraci�n] 
       [-lang archivo-de-idioma] [-machine tipo-de-m�quina] [-noconsole]
       [-startmapper] [-noautoexec]
       
dosbox -version

  name   
        Si "nombre" es un directorio se montar� como unidad C:
        Si "nombre" es un ejecutable se montar� su directorio como C:
        y se ejecutar� "nombre".
    
  -exit  
        DOSBox se cerrar� cuando la aplicaci�n "nombre" termine su ejecuci�n.

  -c command
        Ejecuta el comando especificado antes de ejecutar "nombre". Se pueden
        especificar varios comandos, poniendo a cada uno la opci�n "-c".
        Un comando puede ser un programa interno, un comando DOS o un ejecutable
        en una unidad montada.

  -fullscreen
        Arranca DOSBox en modo de pantalla completa.

  -conf archivo-de-configuraci�n
        Arranca DOSBox con las opciones definidas en "archivo-de-configuraci�n".
        Ver el Cap�tulo 9 para m�s detalles.

  -lang archivo-de-idioma
        Arranca DOSBox usando el idioma especificado en "archivo-de-idioma".

  -noconsole (Solo Windows)
        Lanza DOSBox sin mostrar la ventana de la consola. La salida ser�
        redirigida a stdout.txt y stderr.txt.
	
  -machine tipo-de-m�quina
        Configura DOSBox para emular un tipo concreto de m�quina. Los tipos
        v�lidos son: hercules, cga, pcjr, tandy, vga (opci�n por defecto).
        El tipo de m�quina afecta a la tarjeta gr�fica y a las tarjetas de
        sonido disponibles.

  -startmapper
        Entra en el asignador de teclas directamente al arrancar. Util
        cuando tienes problemas con el teclado.

  -noautoexec
        Ignora la secci�n [autoexec] del archivo de configuraci�n.

  -version
        Muestra informaci�n sobre la versi�n y sale. Util para los
        frontends.

Nota: Si un nombre/comando/archivo-de-configuraci�n/archivo-de-idioma contiene un
      espacio, escr�belo entre comillas ("").

Por ejemplo:

dosbox c:\atlantis\atlantis.exe -c "MOUNT D C:\PARTIDAS"
  Monta C:\atlantis como C: y ejecuta atlantis.exe
  Antes de hacerlo monta C:\PARTIDAS como unidad D:.

En Windows, tambi�n puedes arrastrar directorios/archivos sobre el ejecutable
de DOSBox.



====================
4. Comandos internos
====================

DOSBox soporta la mayor�a de los comandos de DOS internos al command.com.
Adem�s, est�n disponibles los siguientes comandos: 

MOUNT "Letra de la Unidad Emulada" "Unidad o Directorio Real" 
      [-t tipo] [-aspi] [-ioctl] [-usecd n�mero] [-size tama�o] 
      [-label etiqueta] [-freesize tama�o_en_Mb]
MOUNT -cd
MOUNT -u "Letra de la Unidad Emulada"

  Programa para montar directorios locales como unidades dentro de DOSBox.

  "Letra de la Unidad Emulada"
        La letra de la unidad dentro de DOSBox (Por ejemplo, C).

  "Unidad o Directorio Real"
        El directorio local que quieres tener disponible en DOSBox
        (Por ejemplo: mount c c:\juegos).

  -t tipo
        Tipo del directorio montado. Los soportados son: dir (est�ndar),
        floppy, cdrom.

  -size tama�o
        Establece el tama�o de la unidad.

  -freesize tama�o_en_Mb
        Establece la cantidad de espacio libre disponible en la unidad en Mb.
        Es una versi�n m�s simple de -size.

  -label etiqueta
        Establece el nombre de la unidad a "etiqueta". Es necesario en algunos
        sistemas si la etiqueta del CD no se lee correctamente. Util cuando un
        programa no puede encontrar su CD-ROM. Si no especificas una etiqueta y
        el soporte de bajo nivel no est� activado (-usecd # y/o -ioctl/aspi):
          En Windows la etiqueta es extraida de la "Unidad Real".
          En Linux la etiqueta se establece en NO_LABEL.

        Si especificas una etiqueta, esta se mantendr� mientras la unidad est�
        montada. �No se actualizar�!
        
  -aspi
        Fuerza el uso de la capa ASPI. Solo es v�lida al montar un CD-ROM en
        sistemas Windows con la capa ASPI instalada.

  -ioctl   
        Fuerza el uso de comandos ioctl. Solo es v�lida al montar un CD-ROM en
        sistemas WINDOWS que los soporten (Win2000/XP/NT).

  -usecd n�mero
        Fuerza el uso de soporte de CD-ROM SDL para la unidad cuyo n�mero se
        especifica. Se puede ver el n�mero correspondiente ejecutando el comando
        mount -cd. V�lido en todos los sistemas.

  -cd
        Muestra todas las unidades de CD detectadas y sus n�meros. Para usar
        junto con mount -usecd.

  -u
        Desmonta una unidad. No funciona con Z:.

  Nota: Es posible montar un directorio local como unidad de CD, pero entonces
        no es posible el soporte a bajo nivel.

  B�sicamente, MOUNT permite conectar hardware real al ordenador "emulado" en
  DOSBox. As�, MOUNT C C:\JUEGOS le dice a DOSBox que use el directorio C:\JUEGOS
  como la unidad C: en DOSBox. Tambien permite cambiar la letra de una unidad para
  aquellos programas que requieren una letra de unidad espec�fica.
  
  Por ejemplo: "Touche: Las Aventuras del Quinto Mosquetero" debe ejecutarse desde
  la unidad C:. Usando DOSBox y el comando mount, puedes enga�ar al juego para que
  crea que est� en la unidad C, y ponerlo en realidad donde t� quieras. Por ejemplo,
  si el juego est� en D:\TOUCHE, el comando MOUNT C D:\ te permitir� ejecutar
  Touche desde la unidad D:.
  
  �No es recomendable montar la unidad C: entera con MOUNT C C:\!
  Si hay un error en DOSBox o comentes un fallo, podr�as perder todos tus archivos.
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

  Se puede usar CONFIG para cambiar o averiguar la configuraci�n de DOSBox
  durante su ejecuci�n. Puede grabar la configuraci�n actual y el texto del
  idioma actual en disco. Puedes encontrar informaci�n sobre todas las
  secciones del archivo de configuraci�n y sus propiedades en la
  secci�n 9 (El Archivo de Configuraci�n).

  -writeconf archivo-local
       Guarda la configuraci�n actual en un archivo, "archivo-local", en la
       unidad local, no en una unidad montada de DOSBox. El archivo de
       configuraci�n controla diversas opciones de DOSBox:
       La cantidad de memoria emulada, las tarjetas de sonido emuladas y muchas
       otras cosas. Tambien permite acceso al AUTOEXEC.BAT. Ver la
       s ecci�n 9 (El Archivo de Configuraci�n) para m�s informaci�n.

  -writelang archivo-local
       Escribe el texto del idioma actual a un archivo situado en el disco duro
       local, no en una unidad montada en DOSBox. El archivo de idioma controla
       toda la salida visible de los comandos internos y del DOS interno.

  -set "propiedad=valor"
       CONFIG tratara de establecer el nuevo valor para la propiedad. Actualmente
       CONFIG no puede informar de si el comando tuvo �xito o no.

  -get "propiedad"
       El valor actual de la propiedad es devuelto y almacenado en la variable
       de entorno %CONFIG%. Puede usarse para almacenar el valor al trabajar con
       archivos por lotes.

  Tanto "-set" como "-get" funcionan en archivos por lotes y pueden usarse para
  establecer tus propias preferencias para cada juego.
  
  Ejemplos:
  1. Para crar un archivo de configuraci�n en tu directorio actual:
      config -writeconf dosbox.conf
  2. Para establecer los ciclos del procesador a 10000:
      config -set "cpu cycles=10000"
  3. Para desactivar la emulaci�n de memoria EMS:
      config -set "dos ems=off"
  4. Para comprobar qu� n�cleo del procesador se est� usando:
      config -get "cpu core"

LOADFIX [-size] [programa] [parametros-del-programa]
LOADFIX -f
  Programa para reducir la cantidad de memoria disponible. Util para viejos
  programas que no esperan encontrar mucha memoria libre.

  -size	        
        n�mero de kb a "comerse", por defecto 64kb
  
  -f
        libera toda la memoria reservada anteriormente
  

Ejemplos:
  1. Para iniciar mm2.exe y reservar 64 kb de memoria
     (mm2 tendr� 64 kb menos de memoria disponible):
     loadfix mm2
  2. Para iniciar mm2.exe y reservar 32 kb de memoria:
     loadfix -32 mm2
  3. Para liberar la memoria reservada anteriormente:
     loadfix -f


RESCAN
  Hace que DOSBox relea la estructura de directorios. Util si has cambiado algo
  de una unidad montada desde fuera de DOSBox. (CTRL - F4 tambi�n hace lo mismo).
  

MIXER
  Muestra la configuraci�n actual de volumen.
  As� es como puedes cambiarla:
  
  mixer canal izquierda:derecha [/NOSHOW] [/LISTMIDI]
  
  canal
      Puede ser uno de los siguientes: MASTER, DISNEY, SPKR, GUS, SB, FM.
  
  izquierda:derecha
      El nivel de volumen en porcentajes. Si pones una D delante ser� en 
      decibelios (por ejemplo mixer gus d-10).
  
  /NOSHOW
      Evita mostrar el resultado si cambias alguno de los niveles de volumen.

  /LISTMIDI
      Lista los dispositivos midi disponibles en tu ordenador (Windows). Para
      elegir un dispositivo distinto al asignador-midi por defecto de Windows,
      a�ade una l�nea 'config=id' a la secci�n [midi] del archivo de configuraci�n,
      donde 'id' es el n�mero del dispositivo listado por LISTMIDI.


IMGMOUNT
  Una utilidad para montar im�genes de disco y de CD-ROM en DOSBox.
  
  IMGMOUNT DRIVE [imagen] -t [tipo_de_imagen] -fs [formato] 
            -size [bytes_por_sector, sectores_por_cabezal, cabezales, cilindros]

  imagen
      Ubicaci�n del archivo de imagen a montar en DOSBox. La ubicaci�n se
      refiere a una unidad montada dentro de DOSBox. Las im�genes de CD-ROM
      pueden montarse directamente, no tienen por qu� encontrarse dentro de
      una unidad montada.
   
  -t 
      Los siguientes son tipos v�lidos de imagen:
        floppy: Especifica una imagen de disquete.  DOSBox identificar� autom�ticamente 
                la geometr�a del disco (360K, 1.2MB, 720K, 1.44MB, etc).
        iso:    Especifica una imagen ISO de CD-ROM.  La geometr�a es autom�tica para
                este tama�o. Puede ser una ISO o un CUE/BIN.
        hdd:    Especifica una imagen de disco duro. Es necesario a�adir la geometr�a
                correcta (cilindros, cabezas y sectores) para que funcione.

  -fs 
      Los siguiente son tipos v�lidos de sistemas de ficheros:
        iso:  Especifica el formato de CD-ROM ISO-9660.
        fat:  Especifica que la imagen usa el sistema de ficheros FAT. DOSBox
              tratara de montar esta imagen como una unidad y hacer los ficheros
              disponibles dentro de DOSBox.
        none: Dosbox no intentar� leer el sistema de archivos del disco. Esto
              puede ser util si necesitas formatearlo o si quieres arrancarlo
              usando el comando BOOT. Al usar el sistema de ficheros "none", debes
              especificar el n�mero de la unidad (2 � 3, donde 2 = maestro, 3 = esclavo)
              en vez de una letra de unidad.
              Por ejemplo, para montar una imagen de 70MB como la unidad esclava,
              se escribir�a:
                "imgmount 3 d:\prueba.img -size 512,63,16,142 -fs none"
                (sin las comillas)  Compara esto con un mount para leer la
                unidad en DOSBox, que ser�a:
                "imgmount e: d:\prueba.img -size 512,63,16,142"

  -size 
     La especificaci�n de los cilindros, cabezales y sectores de la unidad.
     Necesarios para montar im�genes de disco duro.
     
  Un ejemplo de imagen de CD-ROM:
    1a. mount c /tmp
    1b. imgmount d c:\miiso.iso -t iso
  o tambi�n:
    2. imgmount d /tmp/miiso.iso -t iso


BOOT
  Boot arrancar� im�genes de disco duro o disquete independientes de la
  emulaci�n del sistema operativo ofrecida por DOSBox. Esto hace posible
  jugar a juegos en disquetes autoarrancables o arrancar otros sistemas
  operativos dentro de DOSBox.

  BOOT [imagen1.img imagen2.img .. imagenN.img] [-l letra-de-unidad]

  imagenN.img 
     Esto puede ser cualquier n�mero de im�genes de disquete que se quieran
     tener montadas despu�s de que DOSBox arranque desde la unidad especificada.
     Para cambiar de imagen, pulsa CTRL-F4 para pasar a la siguiente de la lista.
     Una vez alcanzada la �ltima, se volver� a la primera imagen.

  [-l letra-de-unidad]
     Este parametro permite especificar la unidad desde la que arrancar.
     La unidad por defecto es A, la unidad de disquetes. Tambi�n se puede arrancar
     una imagen de disco duro montada como unidad maestra especificando "-l C", sin
     las comillas, o una unidad esclava con "-l D".


IPX

  Debes activar el protocolo de red IPX en el archivo de configuraci�n de DOSBox.

  Todo el sistema de red por IPX es gestionado a trav�s del programa interno de
  DOSBox IPXNET. Para ver la ayuda sobre IPX dentro de DOSBox, escribe
  "IPXNET HELP" (sin las comillas) y el programa listar� los comandos y su
  documentaci�n correspondiente.

  Respecto a la puesta en funcionamiento de una red, un sistema debe hacer de servidor.
  Para ello, escribe "IPXNET STARTSERVER" (sin las comillas) en una sesi�n de DOSBox.
  El servidor se a�adir� autom�ticamente a si mismo a la red IPX virtual. Para cada
  equipo adicional que se quiera forme parte de la red, necesitar�s escribir
  "IPXNET CONNECT <nombre o IP del servidor>". Por ejemplo, si tu servidor se encuentra
  en bob.dosbox.com, deber�as escribir "IPXNET CONNECT bob.dosbox.com" en cada equipo
  distinto al servidor.
  
  La siguiente es una referencia de comandos de IPXNET:

  IPXNET CONNECT 

     IPXNET CONNECT abre una conexi�n a un servidor IPX (encapsulado)
     ejecutandose en otra sesi�n de DOSBox. El par�metro "direcci�n"
     especifica la direcci�n IP o nombre del ordenador servidor. Tambi�n
     puedes especificar el puerto UDP a usar. Por defecto IPXNET usa el
     puerto 213 (El puerto asignado por la IANA para el encapsulado de IPX)
     para la conexi�n.

     La sintaxis de IPXNET CONNECT es: 
     IPXNET CONNECT direcci�n <puerto> 

  IPXNET DISCONNECT 

     IPXNET DISCONNECT cierra la conexi�n al servidor IPX. 

     La sintaxis de IPXNET DISCONNECT es: 
     IPXNET DISCONNECT 

  IPXNET STARTSERVER 

     IPXNET STARTSERVER inicia un servidor IPX (encapsulado) en la sesi�n actual
     de DOSBox. Por defecto, el servidor aceptar� conexiones en el puerto UDP 213,
     aunque esto se puede cambiar. Una vez iniciado el servidor, DOSBox iniciar�
     autom�ticamente una conexi�n cliente al servidor.

     La sintaxis de IPXNET STARTSERVER es:
     IPXNET STARTSERVER <puerto>

  IPXNET STOPSERVER

     IPXNET STOPSERVER detiene el servidor IPX que est� ejecutandose en la sesi�n
     actual de DOSBox. Hay que tener cuidado y asegurarse de que no haya conexiones
     activas en el momento de detener el servidor, pues esto podr�a provocar
     cuelgues en las m�quinas que todav�a lo est�n usando.

     La sintaxis de IPXNET STOPSERVER es: 
     IPXNET STOPSERVER 

  IPXNET PING

     IPXNET PING transmite una petici�n de ping a trav�s de la red IPX
     (encapsulada). Todas las dem�s maquinas conectadas a la red responder�n
     a la petici�n e informar�n del tiempo de respuesta.

     La sintaxis de IPXNET PING es: 
     IPXNET PING

  IPXNET STATUS

     IPXNET STATUS informa sobre el estado actual de la red IPX (encapsulada)
     en esta sesi�n de DOSBox. Para obtener una lista de todos los ordenadores
     conectados a la red usa el comando IPXNET PING.

La sintaxis de IPXNET STATUS es: 
IPXNET STATUS 

Para m�s informaci�n sobre alguno de los comandos usa el parametro /? con dicho
comando.




====================
5. Teclas especiales
====================

ALT-ENTER     Cambiar entre el modo ventana y pantalla completa.
ALT-PAUSE     Hacer una pausa en la emulaci�n.
CTRL-F1       Iniciar el asignador de teclas.
CTRL-F4       Cambiar entre im�genes de disco montadas.
              �Tambi�n Actualiza la cach� de directorio de todas las unidades!
CTRL-F5       Grabar una captura de la pantalla (png).
CTRL-ALT-F5   Comenzar/Detener la grabaci�n de un video de la pantalla.
CTRL-F6       Comenzar/Detener la grabaci�n de la salida de sonido a un fichero.
CTRL-ALT-F7   Comenzar/Detener la grabaci�n de los comandos OPL.
CTRL-ALT-F8   Comenzar/Detener la grabaci�n de comandos MIDI sin procesar.
CTRL-F7       Decrementar el frameskip.
CTRL-F8       Incrementar el frameskip.
CTRL-F9       Detener dosbox.
CTRL-F10      Capturar/Liberar el rat�n.
CTRL-F11      Ralentizar la emlaci�n (Decrementa los ciclos de DOSBox).
CTRL-F12      Acelerar la emulaci�n (Incrementa los ciclos de DOSBox).
ALT-F12       Desactiva el limitador de velocidad (bot�n turbo).

Estas son las asignaciones de teclas por defecto. Pueden cambiarse usando
el asignador de teclas.

Los ficheros grabados pueden encontrarse en directorio_actual/capture
(puede cambiarse en el archivo de configuraci�n).
El directorio debe existir antes de iniciar DOSBox, �


NOTA: Una vez incrementas los ciclos de DOSBox hasta alcanzar el l�mite
      de tu ordenador, seguir aumentandolos solo producira el efecto
      contrario, ralentizar� la emulaci�n. El l�mite var�a de un
      ordenador a otro, y depende de cada configuraci�n hardware y
      software concreta.



======================
6. Asignador de teclas
======================

Cuando inicias el asignador (bien con CTRL-F1 o el parametro -startmapper
en la l�nea de comandos al lanzar DOSBox) aparece un teclado virtual.

Este teclado se corresponde con las pulsaciones de teclas que DOSBox enviar�
a los programas. Si pulsas sobre una tecla con el rat�n, puedes ver en la
esquina inferior izquierda a que tecla de tu teclado real corresponde.

Event: EVENTO
BIND: ASIGNACI�N
                        Add   Del
mod1  hold                    Next
mod2
mod3


EVENTO
    La tecla que DOSBox enviar� a los programas que se est�n emulando.
ASIGNACI�N
    La tecla de tu teclado (tal como informe SDL) que est� conectada al EVENTO.
mod1,2,3 
    Modificadores. Son teclas que tambi�n deben estar presionadas al presionar
    ASIGNACI�N. mod1 = CTRL y mod2 = ALT. Normalmente solo se usan si se quieren
    cambiar las teclas especiales de DOSBox.
Add 
    A�ade una nueva ASIGNACI�N a este EVENTO. Basicamente hace que una tecla del
    teclado real produzca el EVENTO en DOSBox.
Del 
    Elimina la ASIGNACI�N a este EVENTO. Si un EVENTO no tiene ASIGNACIONES,
    no se podr� pulsar esta tecla en DOSBox.
Next
    Recorrer la lista de teclas(ASIGNACIONES) que corresponden a este EVENTO.


Ejemplo:
Q1. Quieres que la X de tu teclado escriba una Z en DOSBox.
A.  Haz click sobre la Z en el teclado virtual. Pulsa "Add", y a
    continuaci�n pulsa la X en tu teclado.

Q2. Si haces click sobre "Next" un par de veces, ver�s que la Z de tu teclado
    tambi�n produce una Z en DOSBox.
A.  Por lo tanto, selecciona de nuevo la Z, pulsa "Next" hasta que tengas la
    Z en tu teclado y entonces pulsa "Del".

Q3. Al probar la asignaci�n en DOSBox y pulsar la X, en la pantalla aparece ZX.
A.  �La X de tu teclado todav�a est� asignada a la X tambi�n! Haz click en la X
    del teclado virtual y busca con "Next" hasta que encuentres la tecla asignada
    X. Pulsa en "Del".


Si modificas las asignaciones por defecto, puedes guardar tus cambios pulsando
"Save". DosBox guardar� las asignaciones en la ubicaci�n especificada en el
archivo de configuraci�n (mapperfile=mapper.txt). Al inicio, DOSBox cargar�
tu archivo de asignaciones, si est� presente en el archivo de configuraci�n.



=========================
7. Requisitos del sistema
=========================

Un equipo r�pido. Yo dir�a que que un Pentium II 400 o m�s para obtener una
emulaci�n decente de juegos escritos para 286.
Para juegos de modo protegido un equipo de al menos 1Ghz de velocidad es
recomendable. �Pero no esperes que funcionen muy r�pido! Asegurate de leer
la secci�n siguiente sobre como acelerarlos en la medida de lo posible.



================================================
8. Ejecutar juegos que necesitan muchos recursos
================================================

DOSBox emula el procesador, la tarjeta gr�fica y la de sonido, y algunas otras
cosas, todo a la vez. Puedes acelerar DOSBox pulsando CTRL-F12, pero estar�s
limitado por la potencia de tu procesador real. Puedes ver la ocupaci�n de tu
procesador usando el Administrador de Tareas en Windows 2000/XP o el 
Monitor del Sistema en Windows 9x/Me. Una vez el uso del procesador alcanza el
100% no hay otra manera de acelerar DOSBox a no ser que reduzcas la carga generada
por otros subsistemas distintos al procesador.

As� que: 

Cierra todos los programas que se est�n ejecutando

Acelera DOSBox hasta que el uso de tu procesador sea del 100%

Ya que la emulaci�n VGA es la parte de DOSBox que mas recursos requiere en terminos
de uso de procesador real, empieza por ah�. Aumenta el frameskip (de uno en uno)
pulsando CTRL-F8. El uso de procesador deber�a disminuir. Vuelve un paso atras y
repite esto hasta que el juego funcione lo suficientemente r�pido.
Por favor, ten en cuenta que esto tiene su parte negativa: perder�s fluidez de video
para ganar en velocidad

Tambi�n puedes probar desactivando el sonido a traves de la utilidad de configuraci�n
del juego para reducir la carga del procesador un poco m�s.



====================
9. El archivo config
====================

CONFIG.COM puede generar un archivo de configuraci�n, que puedes encontrar
en la unidad Z: dentro de DOSBox. Mira en la secci�n de comandos internos
del leeme si quieres saber como se usa CONFIG.COM.
Puedes editar este archivo de configuraci�n para personalizar DOSBox.

El archivo est� dividido en diversas secci�nes (los nombres llevan [] alrededor).
Algunas secciones tienen opciones que puedes modificar.
# y % indican l�neas de comentarios.
El archivo de configuraci�n generado contiene la configuraci�n actual. Puedes
modificarla y lanzar DOSBox con el argumento -conf para cargar el archivo y usar
esa configuraci�n.

Si no se especifica un archivo de configuraci�n, DOSBox buscara el archivo dosbox.conf
en el directorio actual. Despu�s buscara ~/.dosboxrc (Linux), ~\Dosbox.conf (Win32) o
"~/Library/Preferences/DOSBox Preferences" (MACOSX).



========================
10. El archivo de idioma
========================

CONFIG.COM puede generar un archivo de idioma.
Leelo, y seguramente entiendas como cambiarlo.
Arranca DOSBox con el argumento -lang para usar tu nuevo archivo de idioma.
Tambi�n, puedes configurar el nombre del archivo en el archivo de configuraci�n
en la secci�n [dosbox]. Hay una entrada language= que puedes cambiar.



========================================
11. Haciendo tu propia versi�n de DOSBox
========================================

Descarga los archivos fuente.
Comprueba el archivo INSTALL que se incluye.



==============================
12. Agradecimientos especiales
==============================

Vlad R. del proyecto VDMSound por su excelente informaci�n sobre la SoundBlaster.
Tatsuyuki Satoh del Equipo Mame por hacer un excelente emulador FM.
Los proyectos Bochs y DOSemu, que us� para obtener informaci�n.
Freedos por las ideas para mi int�rprete de comandos.
Pierre-Yves G�rardy por albergar el antiguo tabl�n de anuncios.
Colin Snover por albergar nuestro foro.
Los Beta Testers.



============
13. Contacto
============

Visita el sitio: 
http://dosbox.sourceforge.net
All� puedes ver la direcci�n de correo electr�nico (The Crew-page).
