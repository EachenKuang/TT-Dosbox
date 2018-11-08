DOSBox v0.73 | Deutsche Lokalisierung von Andreas (weapon.zero@gmx.net)
unter Zuhilfenahme der deutschen �bersetzung 0.72 von Christian K�nig (krischn@gmx.net)



=========
Anmerkung
=========


Nat�rlich hoffen wir, dass sich irgendwann einmal wirklich jedes erdenkliche
PC-Programm unter DOSBox ausf�hren l�sst, aber noch sind wir nicht ganz so
weit. Im Moment f�hlt sich DOSBox auf einem High-End-Rechner in etwa wie ein
guter 486er an.

DOSBox kann so eingestellt werden, dass darauf eine gro�e Bandbreite von IBM-
kompatiblen Spielen - von den Klassikern aus der Zeit von CGA, Tandy und PCjr
bis hin zu Titeln der Quake-�ra - l�uft.



======
Inhalt
======


1. Schnelleinstieg
2. FAQ
3. Syntax
4. Interne Befehle/Programme
5. Tastaturk�rzel
6. Der Keymapper
7. Tastaturlayouts
8. Mehrspieler mittels Nullmodem-Emulation
9. Verbessern der Spielgeschwindigkeit
10. Fehlerbehebung
11. Die Konfigurationsdatei
12. Die Sprachdatei
13. Eine eigene Version von DOSBox erstellen
14. Danksagungen
15. Kontaktinformation



==================
1. Schnelleinstieg
==================


Starten Sie DOSBox und tippen Sie "INTRO", um eine kurze Einf�hrung zu
erhalten.

Sie sollten sich unbedingt mit dem Konzept des Einbindens ("mounten") von
Laufwerken und Verzeichnissen vertraut machen, da DOSBox nicht von sich aus
auf Laufwerke (oder Teile davon) zugreift und diese in der Emulation
bereitstellt.
Lesen Sie dazu den Eintrag "Mein C-Prompt sagt Z:\>!" in den FAQ und die
Beschreibung des Befehls "MOUNT" in Abschnitt 4.



======
2. FAQ
======


Hier einige Fragen, Antworten, Quintessenzen:

F: Mein C-Prompt sagt Z:\>!
F: Muss ich diese Befehle jedes Mal eingeben? Wie geht das automatisch?
F: Wie komme ich in den Vollbildmodus?
F: Mein CD-ROM-Laufwerk geht nicht!
F: Die Maus funktioniert nicht!
F: Es kommt kein Sound!
F: Der Sound stockt/stottert (oder klingt sonstwie seltsam)!
F: Ich kann keinen Backslash ("\") tippen! Und wo ist der Doppelpunkt?
F: Die Tastatur "h�ngt"!
F: Der Cursor bewegt sich nur in eine Richtung!
F: Das Spiel/Programm kann seine CD-ROM nicht finden!
F: Das Spiel/Programm l�uft viel zu langsam!
F: Kann DOSBox meinen Computer besch�digen?
F: Wie �ndere ich die Gr��e des Arbeitsspeichers/des EMS, die Prozessor-
   Geschwindigkeit oder den Soundblaster-IRQ?
F: Welche Sound-Hardware emuliert DOSBox?
F: Auf meinem Linux l�uft aRts und DOSBox st�rzt beim Start ab!
F: Tolle README, aber ich kapier's noch immer nicht...


F: Mein C-Prompt sagt Z:\>!

A: DOSBox muss erst Ordner/Verzeichnisse freigegeben bekommen, um mit (bzw.
   in) ihnen arbeiten zu k�nnen. Daf�r gibt es den MOUNT-Befehl.

   Unter Windows w�rde der Befehl "MOUNT C D:\DOS" Ihnen innerhalb von DOSBox
   ein C-Laufwerk einbinden, das auf den Windows-Ordner D:\DOS verweist.
   Unter Linux w�rde "MOUNT C /home/username" Ihnen in DOSBox ein C-Laufwerk
   anlegen, das auf das Linux-Verzeichnis /home/username verweist.

   Um auf das eben eingebundene Laufwerk zu wechseln, tippen Sie "C:". Jetzt
   sollte DOSBox Ihnen die Eingabeaufforderung "C:\>" anzeigen.


F: Muss ich diese Befehle jedes Mal eingeben? Wie geht das automatisch?

A: In der DOSBox-Konfigurationsdatei gibt es den Abschnitt [autoexec], wo Sie
   Befehle eintragen k�nnen, die dann beim Start von DOSBox ausgef�hrt werden.


F: Wie komme ich in den Vollbildmodus?

A: Dr�cken Sie Alt-Enter. Alternativ k�nnen Sie auch die DOSBox-
   Konfigurationsdatei bearbeiten und die Zeile "fullscreen=false" in
   "fullscreen=true" �ndern. Wenn Ihnen der Vollbildmodus irgendwie komisch
   vorkommt, probieren Sie verschiedene Werte f�r die Variable
   "fullresolution" aus. Um den Vollbildmodus wieder zu verlassen, dr�cken Sie
   erneut Alt-Enter.


F: Mein CD-ROM-Laufwerk geht nicht!

A: Um in DOSBox ein CD-ROM-Laufwerk einbinden zu k�nnen, k�nnen Sie zwischen
   verschiedenen M�glichkeiten w�hlen.
   F�r einfachste CD-ROM-Unterst�tzung mit MSCDEX:
     MOUNT D F:\ -T cdrom
   F�r "low-level" CD-ROM-Unterst�tzung (wenn m�glich �ber IOCTL):
     MOUNT D F:\ -T cdrom -USECD 0
   F�r "low-level" SDL-Unterst�tzung:
     MOUNT D F:\ -T cdrom -USECD 0 -NOIOCTL
   F�r "low-level" ASPI-Unterst�tzung (Windows 98/Me mit ASPI-Layer):
     MOUNT D F:\ -T cdrom -USECD 0 -ASPI

   Wobei
     "D" f�r den gew�nschten DOSBox-Laufwerksbuchstaben,
     "F:\" f�r die Pfad des CD-ROM-Laufwerks und
     "0" f�r die Nummer steht, die Sie nach Eingabe von "MOUNT -CD" f�r das
     betreffende CD-ROM-Laufwerk erhalten haben.

   Siehe auch FAQ: Das Spiel/Programm kann seine CD-ROM nicht finden!


F: Die Maus funktioniert nicht!

A: Normalerweise erkennt DOSBox die Maus, wenn ein Spiel sie benutzt. Durch
   einmaliges Klicken innerhalb des DOSBox-Fensters sollte sie erfasst werden
   und funktionieren. Bei bestimmten Spielen kommt es aber vor, dass die
   Mauserkennung fehlschl�gt. In diesem Fall m�ssen Sie das Erfassen u.U.
   erzwingen: dr�cken Sie dazu Strg-F10.


F: Es kommt kein Sound!

A: Stellen Sie zun�chst sicher, dass der Sound f�r das Spiel richtig
   eingestellt ist. M�glicherweise m�ssen Sie daf�r ein zum Spiel geh�rendes
   Programm namens SETUP, SETSOUND oder INSTALL ausf�hren. Pr�fen Sie, ob es
   dort eine "Autodetect"-Option gibt. Falls nicht, w�hlen Sie eine "Sound
   Blaster"- oder "SoundBlaster 16"-Karte mit den Einstellungen "Adresse=220,
   IRQ=7, DMA=1" aus. Wenn Sie ein MIDI-Ger�t ausw�hlen k�nnen/wollen, w�hlen
   Sie die Einstellung "Adresse=330". In der DOSBox-Konfigurationsdatei k�nnen
   Sie diese Werte auch �ndern.

   Falls das Problem damit nicht behoben ist, setzen Sie den "core" in der
   Konfigurationsdatei von "auto" auf "normal" und reduzieren Sie die Zahl der
   Cycles auf einen niedrigen statischen Wert (zum Beispiel "cycles=2000").
   Pr�fen Sie auch, ob ihr Wirtsbetriebssystem �berhaupt Sound ausgibt.


F: Der Sound stockt/stottert (oder klingt sonstwie seltsam)!

A: Sie benutzen zuviel Prozessorleistung, um die DOSBox-Geschwindigkeit zu
   halten. Sie sollten entweder die Zahl der Cycles verringern, mehr Frames
   �berspringen oder die Abtastfrequenz (sampling rate) der verwendeten
   Soundkartenemulation reduzieren (siehe Konfigurationsdatei). Oder Sie
   schaffen sich einen schnelleren Rechner an.
   Sie k�nnen auch versuchen, in der Konfigurationsdatei den "prebuffer"
   f�r die Soundemulation zu erh�hen.

   Wenn die Cycles auf "max" oder "auto" eingestellt sind, stellen Sie sicher,
   dass keine Hintergrundprozesse st�ren (insbesondere, wenn diese auf die
   Festplatte zugreifen).


F: Ich kann keinen Backslash ("\") tippen! Und wo ist der Doppelpunkt?

A: Dieses Problem tritt auf, wenn Sie ein anderes als das US-amerikanische
   Tastaturlayout benutzen. M�gliche Abhilfen:
     1. Das Tastaturlayout �ndern (siehe Abschnitt "Tastaturlayouts")
     2. Im Wirtsbetriebssystem das US-Tastaturlayout einstellen.
     3. Statt Backslash den Schr�gstrich ("/") benutzen.
     4. In der Konfigurationsdatei die Variable "usescancodes" von "false"
        nach "true" setzen.
     5. Die gew�nschten Befehle in der Konfigurationsdatei eintragen.
     6. Die Kombinationen Alt-58 und Alt-92 f�r ":" und "\" verwenden.
     7. Auf der deutschen Tastatur liegt der Backslash auf der "#"-Taste, den
        Doppelpunkt bekommt man mit Shift-�.
     8. Benutzen Sie das Programm KEYB (http://projects.freedos.net/keyb/),
        am besten in der Version 2.0 pre4, weil neuere wie �ltere Versionen
        einen Programmfehler in den Laderoutinen aufweisen.


F: Die Tastatur "h�ngt"!

A: Reduzieren Sie in der Konfigurationsdatei die Priorit�t von DOSBox im
   System (z.B. "priority=normal,normal"). Eine andere M�glichkeit besteht
   darin, die Zahl der Cycles zu verringern.


F: Der Cursor bewegt sich nur in eine Richtung!

A: Schalten Sie die Joystick-Simulation ab und pr�fen Sie, ob das Problem dann
   immer noch besteht (setzen Sie "joysticktype=none" im Abschnitt [joysticks]
   der DOSBox-Konfigurationsdatei. Sie k�nnen auch einfach den Joystick
   abklemmen (Stecker ziehen).
   Wenn Sie in dem Spiel einen Joystick verwenden m�chten, setzen Sie
   versuchshalber "timed=false" und kalibrieren Sie den Joystick sowohl in
   Ihrem Betriebssystem als auch im Setup-Programm des Spiels.


F: Das Spiel/Programm kann seine CD-ROM nicht finden!

A: Stellen Sie sicher, dass Sie die CD-ROM mit dem Parameter "-T cdrom"
   eingebunden haben, dadurch wird das MSCDEX-Interface geladen, mit dem
   DOS-Spiele mit CD-ROM-Laufwerken kommunizieren.

   Sie k�nnen auch versuchen, das richtige CD-Label (Laufwerksbezeichnung)
   anzugeben ("-LABEL Bezeichnung"). F�r "low-level" CD-ROM-Unterst�tzung
   benutzen Sie alternativ den Parameter "-USECD x", wobei das "x" f�r die
   Nummer des CD-Laufwerks steht. Diese erhalten Sie durch Eingabe von
   "MOUNT -CD". Unter Windows k�nnen Sie auch noch "-IOCTL", "-ASPI" oder
   "-NOIOCTL" angeben (dazu mehr bei der Beschreibung des MOUNT-Befehls).
   Siehe auch FAQ: Mein CD-ROM-Laufwerk geht nicht!

   Versuchen Sie, ein CD-ROM-Image anzulegen (vorzugsweise im Format CUE/BIN)
   und binden Sie dieses mit dem DOSBox-Befehl IMGMOUNT ein. Dadurch erhalten
   Sie unter jedem Betriebssystem eine ausgezeichnete "low-level" CD-ROM-
   Unterst�tzung.


F: Das Spiel/Programm l�uft viel zu langsam!

A: Siehe Abschnitt "Verbessern der Spielgeschwindigkeit"


F: Kann DOSBox meinen Computer besch�digen?

A: DOSBox kann Ihren Computer nicht mehr besch�digen als jedes andere Programm
   mit hohen Systemvoraussetzungen. Wenn Sie die Zahl der Cycles erh�hen, wird
   nicht wirklich Ihr Prozessor �bertaktet. Eine zu hoch eingestellte Cycles-
   Zahl hat negative Auswirkungen auf die Geschwindigkeit, mit der innerhalb
   von DOSBox Programme ausgef�hrt werden.


F: Wie �ndere ich die Gr��e des Arbeitsspeichers/des EMS, die Prozessor-
   Geschwindigkeit oder den Soundblaster-IRQ?

A: Erstellen Sie eine Konfigurationsdatei: "CONFIG -WRITECONF dosbox.conf";
   �ffnen Sie diese in Ihrem Lieblings-Text-Editor und schauen Sie sich die
   Einstellungen an. Um DOSBox mit den neuen Einstellungen zu laden, benutzen
   Sie "dosbox -CONF dosbox.conf" (�ndern Sie u.U. Ihre Verkn�pfung
   entsprechend).


F: Welche Sound-Hardware emuliert DOSBox?

A: DOSBox emuliert verschiedene alte Soundwiedergabe-Ger�te:
   - PC-Lautsprecher
     Die Emulation umfasst den Ton-Generator und verschiedene Formen von
     digitaler Soundausgabe �ber den internen Lautsprecher.
   - Creative CMS/Gameblaster
     Die erste Karte von Creative Labs. In der Voreinstellung belegt sie
     Port 0x220. Vorsicht: wenn Sie die Karte zusammen mit der Adlib-Emulation
     aktivieren, kann es zu Problemen kommen.
   - Tandy 3 Voice
     Diese Hardware wird bis auf den Noise-Channel komplett emuliert. Dieser
     ist nicht besonders gut dokumentiert und was die Sauberkeit des Sounds
     angeht, half nur raten.
   - Adlib
     Diese Emulation wurde von MAME entliehen und ist fast perfekt. Sie umfasst
     auch die F�higkeit des Adlib, beinahe digitalisierten Sound wiederzugeben.
   - SoundBlaster 16, SoundBlaster Pro I & II, SoundBlaster I & II
     In der Voreinstellung bietet DOSBox 16-Level/16-bit Stereo-Sound.
     Sie k�nnen in der Konfigurationsdatei auch ein anderes Modell einstellen.
   - Disney Soundsource
     Diese Soundkarte benutzt den Druckeranschluss und gibt nur Digital-Sound
     aus.
   - Gravis Ultrasound
     Diese Hardware wird fast komplett emuliert, jedoch wurden die MIDI-
     Funktionen weggelassen, da anderweitig ein MPU-401 emuliert wird.
   - MPU-401
     Auch ein MIDI-Interface wird emuliert, allerdings nur, wenn sie �ber ein
     General MIDI- oder MT-32-Ger�t verf�gen.


F: Auf meinem Linux l�uft aRts und DOSBox st�rzt beim Start ab!

A: Auch wenn es sich hierbei nicht wirklich um ein DOSBox-Problem handelt, so
   kann es beseitigt werden, indem Sie die Umgebungsvariable "SDL_AUDIODRIVER"
   nach "alsa" oder "oss" �ndern.


F: Tolle README, aber ich kapier's noch immer nicht...

A: Vielleicht kann Ihnen "The Newbie's pictorial guide to DOSBox" unter
   http://vogons.zetafleet.com/viewforum.php?f=39 weiterhelfen.
   Alternativ k�nnen Sie es im DOSBox-Wiki probieren:
   http://dosbox.sourceforge.net/wiki/
   Beide Angebote sind nur in englischer Sprache verf�gbar, es sollten sich
   �ber die bekannten Suchmaschinen aber auch zahlreiche deutschsprachige
   Tutorials und Anleitungen finden lassen.


Sollten Sie noch Fragen haben, lesen diese README aufmerksam durch und/oder
schauen Sie auf folgender Seite und dem dazugeh�rigen Forum nach:
http://dosbox.sourceforge.net



=========
3. Syntax
=========


Dieser Abschnitt gibt einen �berblick �ber die Kommandozeilenparameter, mit
denen DOSBox gestartet werden kann. Windows-Benutzer sollten dazu ihre DOSBox-
Verkn�pfung entsprechend bearbeiten ("Ziel:") oder die Eingabeaufforderung
benutzen (CMD.EXE bzw. COMMAND.COM).

Die Parameter gelten - wenn nicht anders angegeben - f�r alle verwendeten
Betriebssysteme.

dosbox [Name] [-EXIT] [-C Befehl] [-FULLSCREEN] [-CONF Konfigurationsdatei]
       [-LANG Sprachdatei] [-MACHINE System] [-NOCONSOLE]
       [-STARTMAPPER] [-NOAUTOEXEC] [-SCALER Filter] [-FORCESCALER Filter]

dosbox -VERSION


  Name
        Wenn "Name" ein Verzeichnis ist, wird es als C-Laufwerk eingebunden.
        Wenn "Name" ein Programm ist, wird das Verzeichnis von "Name"
        eingebunden und "Name" ausgef�hrt.

  -EXIT
        DOSBox wird nach der Ausf�hrung von "Name" beendet.

  -C Befehl
        F�hrt vor dem Aufrufen von "Name" einen bezeichneten "Befehl" aus.
        Es k�nnen mehrere Befehle angegeben werden, vor jedem sollte aber "-C"
        stehen.
        M�gliche "Befehle" sind: ein internes Programm, ein DOS-Befehl oder
        ein Programm auf einem eingebundenen Laufwerk.

  -FULLSCREEN
        F�hrt DOSBox im Vollbildmodus aus.

  -CONF Konfigurationsdatei
        F�hrt DOSBox mit den in "Konfigurationsdatei" angegebenen Optionen
        aus. Der Parameter "-CONF" kann mehrfach benutzt werden.
        Siehe dazu den Abschnitt "Die Konfigurationsdatei".

  -LANG Sprachdatei
        DOSBox benutzt die in "Sprachdatei" angegebenen Zeichenketten.

  -MACHINE System
        DOSBox anweisen, ein bestimmtes Computermodell zu emulieren. M�gliche
        Werte sind: hercules, cga, pcjr, tandy, vga (Voreinstellung).
        Die Wahl des Systems hat Einfluss auf den Grafikmodus und verf�gbare
        Soundkarten.

  -NOCONSOLE (nur unter Windows)
        DOSBox ohne Status-Fenster laden. Meldungen werden in die Dateien
        stdout.txt und stderr.txt umgeleitet.

  -STARTMAPPER
        Ruft direkt beim Programmstart den Keymapper auf. Hilfreich bei
        Tastaturproblemen.

  -NOAUTOEXEC
        DOSBox ignoriert den Abschnitt [autoexec] der Konfigurationsdatei.

  -SCALER Filter
        Benutzt den durch "Filter" angegebenen Scaling-Methode. Die
        verf�gbaren Filter finden Sie in der DOSBox-Konfigurationsdatei.

  -FORCESCALER Filter
        �hnlich dem Parameter -SCALER; erzwingt die Anwendung des gew�hlten
        Filters auch wenn dieser m�glicherweise nicht passt.

  -VERSION
        Gibt Versions-Information aus und beendet DOSBox. Zur Verwendung durch
        Frontends.


ANMERKUNG: Wenn Name/Befehl/Konfigurationsdatei/Sprachdatei ein Leerzeichen
enth�lt, setzen Sie Name/Befehl/Konfigurationsdatei/Sprachdatei komplett in
Anf�hrungszeichen ("hier ein Beispiel").

Wenn Sie innerhalb der Anf�hrungszeichen weitere Anf�hrungszeichen benutzen
m�ssen (am wahrscheinlichsten bei den Parametern -C und -MOUNT), benutzen Sie
unter Windows und OS/2 einfache Anf�hrungszeichen (') innerhalb der doppelten
Anf�hrungszeichen, unter anderen Betriebssystemen versuchen Sie einen
vorangestellten umgekehrten Schr�gstrich (\).

  Beispiel Windows:
    -C "MOUNT C 'C:\Mein Ordner'"
  Beispiel Linux:
    -C "MOUNT C \"/tmp/mein spiel\""


Beispiel:

dosbox C:\ATLANTIS\ATLANTIS.EXE -C "MOUNT D C:\SAVES"
  Bindet den Ordner C:\ATLANTIS als C-Laufwerk ein und f�hrt das Programm
  ATLANTIS.EXE aus, nachdem C:\SAVES als D-Laufwerk eingebunden wurde.


Unter Windows k�nnen Verzeichnisse oder Dateien auch mittels Drag & Drop auf
die dosbox.exe gezogen werden.



============================
4. Interne Befehle/Programme
============================


DOSBox unterst�tzt die meisten DOS-Befehle aus COMMAND.COM; eine Liste der
internen Kommandos erhalten Sie durch den Befehl HELP.

Zus�tzlich sind folgende Befehle verf�gbar:


MOUNT "Virtueller Laufwerksbuchstabe" "Laufwerk oder Ordner"
      [-T Typ] [-ASPI] [-IOCTL] [-NOICTL] [-USECD Nummer]
      [-SIZE Laufwerksgr��e] [-LABEL Bezeichnung] [-FREESIZE Speicherplatz]
MOUNT -CD
MOUNT -U "Virtueller Laufwerksbuchstabe"

  Programm zum Einbinden lokaler Laufwerke bzw. Verzeichnisse/Ordner als
  virtuelle Laufwerke innerhalb von DOSBox.

  "Virtueller Laufwerksbuchstabe"
        Der Laufwerksbuchstabe innerhalb von DOSBox (z.B. C)

  "Laufwerk oder Ordner"
        Das lokale Verzeichnis, das in DOSBox verf�gbar gemacht werden soll.
        Es wird empfohlen, ganze Laufwerke nur dann einzubinden, wenn es sich
        bei ihnen um CD-ROMs handelt.

  -T Typ
        Typ des eingebundenen Verzeichisses. Unterst�tzt werden:
        dir (Voreinstellung), floppy, cdrom.

  -SIZE Laufwerksgr��e
        Legt die Gr��e des Laufwerks fest. Format f�r Laufwerksgr��e:
        "BpS,SpK,ACg,ACf"
          BpS: Bytes pro Sektor, in der Grundeinstellung 512 f�r normale und
            2048 f�r CD-ROM-Laufwerke
          SpC: Sektoren pro Cluster, normalerweise zwischen 1 und 127
          ACg: Anzahl der Cluster (gesamt), zwischen 1 und 65534
          ACf: Anzahl der freien Cluster, zwischen 1 und ACg

  -FREESIZE Speicherplatz
        Eine vereinfachte Version von -SIZE; legt die Gr��e des auf dem
        Laufwerk verf�gbaren freien Speichers fest.
        F�r normale Laufwerke wird der Wert in Megabytes interpretiert, f�r
        Disketten in Kilobytes.

  -LABEL Bezeichnung
        Laufwerksbezeichnung als "Bezeichnung" festlegen. Wird manchmal
        ben�tigt, wenn das CD-Label nicht richtig gelesen wird. Kann hilfreich
        sein, wenn ein Programm seine CD-ROM nicht findet. Falls keine
        Bezeichnung angegeben und keine "low-level" Unterst�tzung (-USECD
        und/oder -ASPI bzw. -NOICTL) gew�hlt wird:
          Windows: Bezeichnung wird �bernommen von "Verzeichnis"
          Linux: Bezeichnung lautet "NO_LABEL"
        Wenn eine Bezeichnung angegeben wird, ist diese solange g�ltig, wie
        das Laufwerk eingebunden ist und wird nicht geupdatet (CD-Wechsel)!

  -ASPI
        Immer ASPI-Layer benutzen. Nur g�ltig, wenn eine CD-ROM auf einem
        Windows-System mit ASPI-Layer eingebunden wird.

  -IOCTL
        Immer IOCTL-Befehle benutzen. Nur g�ltig, wenn eine CD-ROM auf einem
        kompatiblen System eingebunden wird (Windows NT/2000/XP).

  -NOICTL
        Immer SDL-CD-ROM-Layer benutzen. G�ltig auf allen Systemen.

  -USECD Nummer
        SDL-CD-ROM-Unterst�tzung f�r bestimmte Laufwerksnummer erzwingen. Die
        Nummer erfahren sie mit -CD. G�ltig auf allen Systemen.

  -CD
        Zeigt alle erkannten CD-ROM-Laufwerke und ihre Nummern. Zur Benutzung
        mit -USECD.

  -U
        Laufwerk "entbinden". Nicht zu verwenden mit Z:\.

  ANMERKUNG: Ein lokales Verzeichnis kann auch als CD-ROM-Laufwerk eingebunden
  werden, die Hardware-Unterst�tzung fehlt dann.

  Im Grunde kann mit MOUNT echte Hardware mit dem von DOSBox emulierten PC
  verbunden werden. MOUNT C C:\GAMES weist DOSBox an, Ihren Ordner C:\GAMES
  als C-Laufwerk innerhalb DOSBox zu verwenden. Es erlaubt Ihnen auch, die
  Laufwerksbuchstaben f�r Programme zu �ndern, die bestimmte
  Laufwerksbuchstaben ben�tigen.

  Das Spiel Touch�: Adventures of the Fifth Musketeer muss beispielsweise
  vom C-Laufwerk gestartet werden. Mit DOSBox und dem MOUNT-Befehl kann man
  dem Spiel vorgaukeln, es bef�nde sich auf dem C-Laufwerk, w�hrend Sie es
  ablegen k�nnen, wo Sie wollen. Wenn das Spiel also in D:\GAMES\TOUCHE w�re,
  k�nnten Sie den Befehl "MOUNT C D:\GAMES" benutzen, um Touch� vom D-Laufwerk
  auszuf�hren.

  Es wird DRINGEND davon abgeraten, das gesamte C-Laufwerk mit "MOUNT C C:\"
  einzubinden. Dasselbe gilt f�r die Urverzeichnisse egal welches Laufwerks,
  mit Ausnahme von CD-ROMs (da diese schreibgesch�tzt sind). Falls Ihnen oder
  DOSBox ein Fehler unterl�uft, k�nnten alle Daten verloren gehen.
  Es wird deshalb empfohlen, alle Programme/Spiele in einem Unterverzeichnis
  abzulegen und dieses einzubinden.

  Allgemeine MOUNT-Beispiele:

  1. C:\OrdnerX als Diskettenlaufwerk A einbinden:
       MOUNT A C:\OrdnerX -T floppy
  2. Das CD-ROM-Laufwerk E als CD-ROM-Laufwerk D in DOSBox einbinden:
       MOUNT D E:\ -T cdrom
  3. Das CD-ROM-Laufwerk bei /media/cdrom als Laufwerk D in DOSBox einbinden:
       MOUNT D /media/cdrom -T cdrom -USECD 0
  4. D:\ als Laufwerk mit ~870 MB freiem Speicher einbinden (einfach):
       MOUNT C D:\ -FREESIZE 870
  5. D:\ als Laufwerk mit ~870 MB freiem Speicher einbinden (komplex, nur f�r
     Profis!):
       MOUNT C D:\ -SIZE 512,127,16513,13500
  6. Verzeichnis /home/user/OrdnerY als C-Laufwerk in DOSBox einbinden:
       MOUNT C /home/user/OrdnerY
  7. Das DOSBox-Verzeichnis als Laufwerk D einbinden:
       MOUNT D


MEM

  Zeigt die Gr��e des freien Arbeitsspeichers an.


CONFIG -WRITECONF Datei
CONFIG -WRITELANG Datei
CONFIG -SET Abschnitt Variable=Wert
CONFIG -GET Abschnitt Variable

  Mit CONFIG k�nnen verschiedene Einstellungen von DOSBox abgefragt oder
  ge�ndert werden, w�hrend das Programm l�uft. Die gew�hlten Einstellungen
  und Zeichenketten k�nnen direkt gespeichert werden. Informationen �ber
  m�gliche Abschnitte und Variablen finden Sie im Abschnitt "Die
  Konfigurationsdatei".

  -WRITECONF Datei
       Die aktuelle Konfigurationsdatei in "Datei" abspeichern. "Datei"
       befindet sich im lokalen DOSBox-Verzeichnis, nicht im eingebundenen
       DOSBox-Laufwerk!).

       Die Konfigurationsdatei steuert verschiedene DOSBox-Einstellungen: die
       Gr��e des emulierten Speichers, die emulierten Soundkarten und vieles
       mehr. Sie beinhaltet auch die AUTOEXEC.BAT-Einstellungen. Mehr Infor-
       mationen im Abschnitt "Die Konfigurationsdatei".

  -WRITELANG Datei
       Die aktuellen Spracheinstellungen abspeichern, wobei "Datei" sich im
       lokalen DOSBox-Verzeichnis befindet, nicht im eingebundenen DOSBox-
       Laufwerk. Die Sprachdatei beinhaltet (fast) alle auf dem Bildschirm
       sichtbaren Ausgaben der internen Befehle und des internen DOS.

  -SET Abschnitt Variable=Wert
       CONFIG versucht, der Variablen einen neuen Wert zuzuordnen. CONFIG kann
       zu diesem Zeitpunkt nicht ausgeben, ob der Versuch erfolgreich war.

  -GET Abschnitt Variable
       Der aktuelle Wert der Variable wird ausgegeben und und in der Umge-
       bungsvariable %CONFIG% gespeichert. Hilfreich, wenn mit Stapeldateien
       gearbeitet wird.

  Sowohl "-SET" als auch "-GET" funktionieren aus Stapeldateien heraus und
  k�nnen benutzt werden, um f�r einzelne Spiele eigene Einstellungen festzu-
  legen.

  Beispiele:

  1. Eine Konfigurationsdatei im DOSBox-Verzeichnis abspeichern:
       CONFIG -WRITECONF dosbox.conf
  2. Die CPU-Cycles auf 10000 setzen:
       CONFIG -SET cpu cycles=10000
  3. EMS-Speicheremulation abschalten:
       CONFIG -SET dos ems=off
  4. Pr�fen, wieviel Prozessorleistung DOSBox im System nutzt:
       CONFIG -GET cpu core


LOADFIX [-Gr��e] [Programm] [Programm-Parameter]
LOADFIX -F

  Programm zum Speicher-"Fressen". Hilfreich bei alten Programmen, die wenig
  freien Speicher erwarten.

  -Gr��e
        Gr��e des zu "fressenden" Speichers in KB, Voreinstellung: 64 KB

  -F
        Vorher zugeteilten Speicher freigeben.

  Beispiele:

  1. Programm MM2.EXE laden und 64 KB Speicher zuteilen (MM2 erh�lt 64 KB
     weniger Speicher):
       LOADFIX MM2.EXE
  2. Programm MM2.EXE laden und 32 KB Speicher zuteilen:
       LOADFIX -32 MM2.EXE
  3. Vorher zugeteilten Speicher freisetzen:
       LOADFIX -F


RESCAN

  DOSBox liest die Verzeichnisstruktur erneut ein. Hilfreich, wenn au�erhalb
  von DOSBox etwas in dem/den eingebundenen Verzeichnis/sen ge�ndert wurde.
  Alternativ kann auch Strg-F4 benutzt werden.


MIXER Kanal Links:Rechts [/NOSHOW] [/LISTMIDI]

  Zeigt die Lautst�rkeeinstellungen an und �ndert sie.

  Kanal
        Einer der folgenden Werte: master, disney, spkr, gus, sb, fm.

  Links:Rechts
        Eine Lautst�rkeangabe in Prozent (f�r die jeweilige Seite).
        Ein vorangestelltes D sorgt daf�r, dass die Zahl als Dezibelangabe
        interpretiert wird (Beispiel: MIXER gus d-10).

  /NOSHOW
        Die Lautst�rke�nderung erfolgt stumm (keine Textmeldung).

  /LISTMIDI
        Zeigt die auf Ihrem Rechner verf�gbaren MIDI-Ger�te an (Windows).
        Um ein anderes Ger�t als den standardm��igen MIDI-Mapper auszuw�hlen,
        f�gen Sie eine Zeile "config=id" im Abschnitt [midi] der
        Konfigurationsdatei hinzu, wobei "id" die Nummer ist, die Sie nach
        Benutzung von /LISTMIDI f�r das betreffende Ger�t erhalten.


IMGMOUNT

  Programm zum Einbinden von Disketten-, Festplatten- und CD-ROM-Images
  in DOSBox.

  IMGMOUNT "Virtueller Laufwerksbuchstabe" Imagedatei -T Imagetyp
           -FS Imageformat
           -SIZE Sektorengr��e, Sektoren pro Kopf, K�pfe, Zylinder

  Imagedatei
        Adresse der in DOSBox einzubindenden Imagedatei. Diese befindet sich
        entweder auf einem in DOSBox eingebundenen Laufwerk oder einem
        physischen Ger�t. Es k�nnen auch CD-ROM-Images (ISO oder CUE/BIN)
        eingebunden werden. Wenn Sie mehrere CD-ROMs ben�tigen, geben Sie
        die Images hintereinander an. Diese k�nnen dann jederzeit mit Strg-F4
        gewechselt werden.

  -T Imagetyp
      G�ltige Imagetypen:
        floppy: Gibt ein Disketten-Image bzw. -Images an. DOSBox erkennt das
                Format automatisch (360 KB, 1,2 MB, 720 KB, 1,44 MB usw.)
        iso:    Gibt ein CD-ROM-Image an. Das Format wird automatisch erkannt.
                Es kann ein ISO- oder CUE/BIN-Image benutzt werden.
        hdd:    Gibt ein Festplatten-Image an. Es muss die korrekte CHS-
                Laufwerksgeometrie angegeben werden.

  -FS Imageformat
      G�ltige Dateisystem-Formate:
        iso:    ISO 9660 CD-ROM-Format.
        fat:    FAT-Dateisystem. DOSBox versucht, dieses Image als Laufwerk
                in DOSBox einzubinden und die Dateien in DOSBox verf�gbar zu
                machen.
        none:   DOSBox versucht nicht, das Dateisystem auf dem Image zu lesen.
                Dies kann n�tzlich sein, wenn man es formatieren oder mit dem
                BOOT-Befehl davon booten will. F�r das "none"-Dateisystem muss
                statt einem Laufwerksbuchstaben eine Laufwerksnummer angegeben
                werden (2 oder 3; wobei 2=Master, 3=Slave).
                Um beispielsweise ein 70 MB-Image D:\TEST.IMG als Slave-
                Laufwerk einzubinden, benutzen Sie:
                  IMGMOUNT 3 D:\TEST -SIZE 512,63,16,142 -FS none
                Zum Vergleich der Befehl, um das Laufwerk in DOSBox zu lesen:
                  IMGMOUNT E D:\TEST.IMG -SIZE 512,63,16,142

  -SIZE
        Die Laufwerksgeometrie (Angaben zur Anzahl von Zylindern, K�pfen und
        Sektoren) des Laufwerks. Wird ben�tigt, um Festplatten-Images
        einbinden zu k�nnen.

  Ein Beispiel zum Einbinden von CD-ROM-Images:

    1a. MOUNT C /tmp
    1b. IMGMOUNT D C:\CDROM.ISO -T iso
  oder alternativ:
    2. IMGMOUNT D /tmp/CDROM.ISO -T iso


BOOT

  BOOT startet Disketten- oder Festplatten-Images unabh�ngig von der DOS-
  Emulation von DOSBox. Damit k�nnen sog. Booter-Spiele oder andere
  Betriebssysteme innerhalb von DOSBox gebootet werden.
  Wenn das emulierte System ein PCjr ist ("machine=pcjr"), k�nnen mit dem
  BOOT-Befehl auch PCjr-Cartridges (.jrc) geladen werden.

  BOOT [Image1.img Image2.img ... ImageN.img] [-L Laufwerksbuchstabe]
  BOOT Cartridge.jrc
    (nur g�ltig bei PCjr-Emulation)

  ImageN.img
        Eine beliebige Anzahl von Disketten-Images, die eingebunden werden
        sollen, nachdem DOSBox vom angegebenen Laufwerk gebootet hat.
        Um zwischen den eingebundenen Disketten zu wechseln, benutzen Sie
        Strg-F4. Dadurch wird die aktuelle Diskette "ausgeworfen" und die
        n�chste auf der Liste "eingelegt". Sobald die letzte Diskette auf der
        Liste ausgeworfen wurde, wird wieder bei der ersten begonnen.

  -L Laufwerksbuchstabe
        Gibt das Laufwerk an, von dem gebootet werden soll.
        Die Voreinstellung ist A, also das Diskettenlaufwerk. Es kann auch von
        einem als Master eingebundenen Festplatten-Image gebootet werden,
        dazu muss "-L C" angegeben werden. Soll das Laufwerk als Slave
        behandelt werden, lautet der Parameter: "-L D".

   Cartridge.jrc
        Wenn das emulierte System ein PCjr ist, k�nnen auch PCjr-Cartridges
        gebootet werden. Die Emulation ist aber noch nicht perfekt.


IPX

  Die IPX-Netzwerkunterst�tzung muss zun�chst in der Konfigurationsdatei
  aktiviert werden ("ipx=true").

  Alles, was mit dem IPX-Netzwerk zusammenh�ngt, wird durch den internen
  Befehl IPXNET gesteuert. Um Hilfe �ber das IPX-Netzwerk innerhalb von DOSBox
  zu erhalten, benutzen Sie "IPXNET HELP" (ohne Anf�hrungszeichen). Das
  Programm wird Ihnen eine Liste der g�ltigen Parameter und dazugeh�rige
  Informationen ausgeben.

  Um das Netzwerk nun tats�chlich einrichten zu k�nnen, muss ein System als
  Server fungieren. Um es einzurichten, geben Sie unter DOSBox den Befehl
  "IPXNET STARTSERVER" ein. Es wird sich automatisch eine DOSBox-
  Serversitzung zum virtuellen IPX-Netzwerk hinzuf�gen. Auf den Rechnern, die
  mit dem virtuellen IPX-Netzwerk verbunden werden sollen, geben Sie jeweils
  den Befehl "IPXNET CONNECT Adresse" ein.

  Wenn der Server zum Beispiel horst.dosbox.com hei�t, m�ssen Sie folgenden
  Befehl auf jedem Client eingeben: "IPXNET CONNECT horst.dosbox.com".

  F�r Spiele, die NetBIOS benutzen, wird ein Programm namens NETBIOS.EXE von
  Novell ben�tigt. Richten Sie die IPX-Verbindung wie oben beschrieben ein
  und starten Sie NetBIOS.

  Es folgt die IPXNET-Syntax:

  IPXNET CONNECT Adresse Port
        �ffnet eine Verbindung zu einem IPX-Tunnelserver innerhalb einer
        anderen DOSBox-Sitzung. Der Parameter "Adresse" gibt die IP-Adresse
        oder den Host-Namen des Servers an. Sie k�nnen auch einen UDP-Port
        angeben, den Sie benutzen wollen. Standardm��ig benutzt IPXNET den
        Port 213. Dies ist der Anschluss, der von IANA f�r den IPX-
        Tunnelserver zugewiesen wird.

  IPXNET DISCONNECT
        beendet die Verbindung mit dem IPX-Tunnelserver.

  IPXNET STARTSERVER Port
        startet einen IPX-Tunnelserver innerhalb der aktuellen DOSBox-Sitzung.
        Standardm��ig akzeptiert der Server Verbindungen auf UDP-Port 213,
        Sie k�nnen diese Einstellung aber �ndern.
        Wenn dem Server ein Router vorgeschaltet ist, muss der Port angegeben
        werden.
        Auf Linux-/Unix-basierten Systemen k�nnen Ports unterhalb von 1023 nur
        von Root-Accounts benutzt werden. Auf diesen Systemen sollten Sie
        Ports oberhalb von 1023 benutzen.

  IPXNET STOPSERVER
        beendet den IPX-Tunnelserver der aktuellen DOSBox-Sitzung. Sie sollten
        vorsichtshalber sicherstellen, dass alle anderen Verbindungen
        ebenfalls beendet wurden, ansonsten k�nnten sich die noch auf den
        Tunnelrechner zugreifenden Rechner eventuell aufh�ngen.

  IPXNET PING
        sendet einen Broadcast-Ping durch das Tunnelnetzwerk, auf den die
        angeschlossenen Rechner antworten und die Zeit angeben, die ben�tigt
        wurde, um den Ping zu senden und zu empfangen.

  IPXNET STATUS
        zeigt den Status des IPX-Tunnelnetzwerks der aktuellen DOSBox-Session
        an. Um eine Liste aller an das Netzwerk angeschlossenen Rechner zu
        erhalten, benutzen Sie den Befehl IPXNET PING.


KEYB [Tastaturcode [Codeseite [Tastaturdefinitionsdatei]]]

  Programm zum �ndern des Tastaturcodes (Tastaturlayouts). Mehr dar�ber im
  Abschnitt "Tastaturlayouts".

  Tastaturcode
        Der aus zwei (oder mehr) Buchstaben bestehende Tastaturcode f�r ein
        Land, beispielsweise GK (Griechenland) oder IT (Italien). Damit wird
        das zu verwendende Tastaturlayout ausgew�hlt.

  Codeseite
        Die Nummer der zu verwendenden Codeseite (Codepage). Wenn der
        Tastaturcode nicht mit der Codeseite kompatibel ist, kann diese nicht
        geladen werden.
        Wenn keine Codeseite angegeben wird, benutzt DOSBox automatisch das
        entsprechende Standard-Layout.

  Tastaturdefinitionsdatei
        Diese kann/muss angegeben werden, falls die gew�nschte Codeseite nicht
        durch DOSBox zur Verf�gung gestellt wird und wird auch nur in solchen
        F�llen ben�tigt.

  Beispiele:

  1) Standard-Tastaturlayout f�r Deutschland und �sterreich (es wird
     automatisch die Codeseite 858 verwendet):
       KEYB GR
  2) Russisches Tastaturlayout mit Codeseite 866:
       KEYB RU 866
         (Benutzen Sie LinksAlt-RechtsShift f�r kyrillische Zeichen)
  3) Franz�sisches Tastaturlayout mit Codeseite 850 aus der Datei EGACPI.DAT:
       KEYB FR 850 EGACPI.DAT
  4) Codeseite 858 (ohne Tastaturlayout):
       KEYN none 858


Um Hilfe f�r einen internen Befehl oder ein bestimmtes Programm zu erhalten,
kann auch der Kommandozeilenparameter "/?" benutzt werden.



=================
5. Tastaturk�rzel
=================


Die folgende Auflistung erhalten Sie auch mit dem Befehl INTRO SPECIAL:

Alt-Enter       Vollbildmodus an/aus
Alt-Pause       Emulation unterbrechen
Strg-F1         Keymapper starten
Strg-F4         Disketten-Image wechseln; Verzeichnisstruktur neu lesen
Strg-F5         Screenshot als PNG-Datei abspeichern
Strg-Alt-F5     Bildschirmausgabe und Sound als Videoclip speichern an/aus
Strg-F6         Soundausgabe in WAV-Datei schreiben an/aus
Strg-Alt-F7     OPL-Daten aufzeichnen an/aus
Strg-Alt-F8     Raw-MIDI-Daten aufzeichnen an/aus
Strg-F7         Frames �berspringen -1
Strg-F8         Frames �berspringen +1
Strg-F9         DOSBox schlie�en
Strg-F10        Maus erfassen/freigeben
Strg-F11        Emulation verlangsamen (DOSBox-Cycles verringern)
Strg-F12        Emulation beschleunigen (DOSBox-Cycles erh�hen)
Alt-F12         Drosselung aufheben (Turbo-Knopf)

Diese Voreinstellungen k�nnen im Keymapper ge�ndert werden.

Gespeicherte/aufgenommene Dateien werden im Unterverzeichnis "capture" im
DOSBox-Ordner abgelegt (diese Einstellung kann in der Konfigurationsdatei
ge�ndert werden).
Das Verzeichnis muss vor dem Start von DOSBox vorhanden sein, sonst kann
nichts gespeichert/aufgenommen werden!

ANMERKUNG: Sobald die DOSBox-Cycles derart erh�ht wurden, dass es das
Leistungsmaximum Ihres Rechners �bersteigt, hat das denselben Effekt, als
w�rden Sie die Emulation verlangsamen. Dieses Maximum ist von Rechner zu
Rechner unterschiedlich, es gibt keinen allgemein g�ltigen Wert.



================
6. Der Keymapper
================


Wenn Sie den Keymapper starten (entweder mit Strg-F1 oder dem
Kommandozeilenparameter "-STARTMAPPER"), erhalten Sie eine virtuelle Tastatur
und einen virtuellen Joystick.

Diese virtuellen Ger�te entsprechen den Tasten, die DOSBox an die ausgef�hrten
Programme �bergibt. Durch einen Mausklick auf die jeweilige Taste sehen Sie
links unten, mit welcher Taste/Funktion diese verkn�pft ist (EVENT).

EVENT: Taste/Funktion
BIND: Belegung
                        Add   Del
mod1  hold              Next
mod2
mod3

  EVENT
    Die Taste/Joystick-Knopf bzw -Achse, die DOSBox den emulierten Programmen
    meldet.

  BIND
    Die Taste auf Ihrer Tastatur/Ihrem Joystick (bzw. die Joystick-Achse), die
    dem EVENT (Taste/Funktion) durch SDL zugewiesen wird.

  mod1,2,3
    Zusatztasten: die Tasten, die zusammen mit BIND gedr�ckt werden m�ssen.
    mod1=Strg, mod2=Alt. Diese werden i.A. nur gebraucht, wenn die DOSBox-
    Sondertasten ge�ndert werden sollen.

  Add
    Dem EVENT ein neues BIND zuweisen, also: eine Taste (oder einen Joystick-
    Knopf usw.) in DOSBox mit einem EVENT belegen.

  Del
    Den BIND des EVENTs l�schen. Wenn ein EVENT keine BINDs hat, ist die Taste
    in DOSBox nicht belegt. Die entsprechende Taste/der Knopf hat also keine
    Funktion.

  Next
    Den n�chsten BIND eines EVENTs anzeigen.


Beispiele f�r die Tastaturbelegung:

  1. Das X auf Ihrer Tastatur soll in DOSBox ein U ausgeben:
     Mit der Maus auf das U im Keymapper klicken. "Add" anklicken. Die X-Taste
     auf der Tastatur dr�cken.
  2. Wenn Sie jetzt ein paarmal auf "Next" klicken, werden Sie bemerken, dass
     das U auf Ihrer Tastatur auch in DOSBox ein U ausgibt.
     W�hlen Sie also erneut U aus und klicken sie solange auf "Next", bis Sie
     das U auf Ihrer Tastatur haben. Klcken Sie jetzt auf "Del".
  3. Wenn Sie in der DOSBox-Shell jetzt probeweise X dr�cken, wird ein "UX"
     ausgegeben.
     Das X auf Ihrer Tastatur ist noch immer mit X belegt. Klicken Sie im
     Keymapper auf das X und suchen Sie mit "Next", bis Sie die Belegung X
     gefunden haben. Klicken Sie auf "Del".


Beispiele f�r die Joystick-Tastenbelegung:

  Es ist ein Joystick angeschlossen, der durch DOSBox einwandfrei erkannt
  wird, und Sie m�chten damit ein Spiel steuern, dass normalerweise nur die
  Tastatur erkennt (wir nehmen an, das Spiel wird �ber die Richtungstasten
  gesteuert):
  1. Starten Sie den Keymapper und klicken Sie auf eine der Pfeiltasten im
     mittleren linken Bereich des Fensters (direkt �ber den Mod1/Mod2-Tasten).
     Als EVENT sollte "key_left" angegeben sein. Klicken Sie auf "Add" und
     bewegen Sie das Achsenkreuz des Joysticks nach links. Jetzt sollte dem
     BIND der Event zugewiesen worden sein.
  2. Wiederholen Sie das Obengenannte f�r die drei anderen Richtungen;
     zus�tzlich k�nnen die Joystick-Kn�pfe anderen Events zugewiesen werden,
     etwa den Funktionen "springen" oder "schie�en".
  3. Klicken Sie auf "Save", dann auf "Exit" und starten Sie das Spiel, um
     auszuprobieren, ob die Einstellungen erfolgreich waren.

  Die Y-Achse soll so ge�ndert werden, dass eine Bewegung nach oben der nach
  unten entspricht - und umgekehrt -, weil Sie damit besser zurechtkommen und
  sich das Spiel selbst nicht entsprechend konfigurieren l�sst:
  1. Starten Sie den Keymapper und klicken Sie auf "Y-" im Joystick-Bereich
     oben rechts (falls Sie zwei Joysticks angeschlossen haben, stellen Sie
     damit den ersten Joystick ein), oder im Joystick-Bereich weiter unten
     (zweiter Joystick, oder - falls Sie nur einen angeschlossen haben - das
     zweite Achsenkreuz des ersten Joysticks).
     Also EVENT sollte jetzt angegeben sein: "jaxis_0_1-" (bzw. "jaxis_1_1-).
  2. Klicken Sie auf "Del", um die aktuelle Verkn�pfung zu l�schen, klicken
     Sie danach auf "Add" und bewegen Sie das Achsenkreuz des Joysticks nach
     unten. Es sollte ein neuer Bind angelegt worden sein.
  3. Gehen Sie entsprechend f�r "Y+" vor, speichern Sie die Belegung ab und
     probieren Sie es aus.


Wenn Sie die Einstellungen bearbeitet haben, k�nnen Sie die �nderungen
abspeichern, indem Sie auf "Save" klicken. DOSBox speichert die Belegungen am
in der Konfigurationsdatei angegebenen Ort ab ("mapperfile=mapper.txt").

Beim Start von DOSBox wird die Tastenbelegung geladen, sofern die angegebene
Datei vorhanden ist.



==================
7. Tastaturlayouts
==================


Um das verwendete Tastaturlayout (den Tastaturcode) zu �ndern, kann entweder
die Variable "keyboardlayout" im Abschnitt [dos] der Konfigurationsdatei
bearbeitet werden, oder Sie benutzen das interne Programm KEYB unter DOSBox.
Bei beiden M�glichkeiten k�nnen Sie DOS-konforme Sprachcodes (siehe unten)
verwenden, eine benutzerdefinierte Codeseite kann jedoch nur mit KEYB
ausgew�hlt werden.


Einstellen des Tastaturcodes

  DOSBox bringt bereits eine ganze Anzahl von voreingestellten Tastaturlayouts
  und Codeseiten mit. Wenn das gew�nschte Layout dabei ist, muss es nur noch
  in der Konfigurationsdatei oder �ber das Programm KEYB angegeben werden (zum
  Beispiel "keyboardlayout=sv" in der Konfigurationsdatei oder "KEYB SV"
  an der DOSBox-Eingabeaufforderung).

  Voreingestellte Tastaturcodes:
    BG     (Bulgarien)                  NL (Niederlande)
    CZ243  (Tschechien)                 NO (Norwegen)
    FR     (Frankreich)                 PL (Polen)
    GK     (Griechenland)               RU (Russland)
    GR     (Deutschland/�sterreich)     SK (Slowakei)
    HR     (Kroatien)                   SP (Spanien)
    HU     (Ungarn)                     SU (Finnland)
    IT     (Italien)                    SV (Schweden)

  Bestimmte Layouts (z.B. GK mit Codeseite 869 und RU mit Codeseite 808)
  unterst�tzen kombinierte Layouts mit lateinischen und l�nderspezifischen
  Zeichen, die durch die Tastenkombination LinksAlt-RechtsShift aktiviert, und
  mit LinksAlt-LinksShift deaktiviert werden.


Unterst�tze Tastaturdefinitionsdateien

  Es werden sowohl die FreeDOS-Tastaturdefinitionsdateien mit der Endung "KL"
  ("FreeDOS Keyb2 Keyboard Layoutfiles") als auch die aus allen verf�gbaren
  FreeDOS-Tastaturdefinitionsdateien bestehenden Bibliotheken Keyboard.sys,
  Keybrd2.sys und Keybrd3.sys unterst�tzt. Falls die in DOSBox integrierten
  Layouts aus irgendwelchen Gr�nden nicht funktionieren oder neuere verf�gbar
  werden, finden Sie diese unter http://projects.freedos.net/keyb/

  Ebenfalls verwendet werden k�nnen Dateien mit den Endungen CPI (DOS-
  kompatible Codeseiten-Spezifikationen) und CPX- (mit UPX komprimierte
  FreeDOS-Codeseiten-Dateien). DOSBox beinhaltet schon einige Codeseiten, so
  dass es selten erforderlich ist, externe Codeseiten-Dateien zu verwenden.
  Falls Sie eine andere - oder eigene - Codeseiten-Datei benutzen m�chten,
  kopieren Sie diese in denselben Ordner wie die Konfigurationsdatei, so dass
  DOSBox auf sie zugreifen kann.

  Zus�tzliche Layouts k�nnen verwendet werden, indem Sie die entsprechende KL-
  Datei in denselben Ordner wie die Konfigurationsdatei kopieren und den
  Dateinamen (ohne Endung) als Tastaturcode verwenden.
  F�r die Datei UZ.KL (das Tastaturlayout f�r Usbekistan) w�rden Sie also in
  der Konfigurationsdatei "keyboardlayout=uz" angeben.
  Die Verwendung von Bibliotheken wie Keybrd2.sys funktioniert �hnlich.


ANMERKUNG: Zwar k�nnen mit einem eingestellten Tastaturlayout Sonderzeichen
an der Kommandozeile getippt werden, jedoch werden Dateinamen aus solchen
Zeichen (Umlaute usw.) nicht unterst�tzt. Versuchen Sie, diese in DOSBox und
f�r Dateien, auf die DOSBox zugreifen kann/soll, zu vermeiden.



==========================================
8. Mehrspieler mittels Nullmodem-Emulation
==========================================


DOSBox kann ein serielles Nullmodem-Kabel �ber Ihr Netzwerk oder das Internet
emulieren.

Dieses muss zun�chst im Abschnitt [serialports] in der Konfigurationsdatei
eingerichtet werden. Hierbei fungiert ein Rechner als Server, der andere als
Client.

In der Konfigurationsdatei des Servers tragen Sie unter [serialports]
folgendes ein:
  serial1=nullmodem

Die entsprechende Eintragung beim Client:
  serial1=nullmodem server:Adresse
    "Adresse" bezeichnet die IP-Adresse oder den Host-Namen des Servers.

Starten Sie jetzt das Spiel und w�hlen Sie als Mehrspieler-Methode an COM1:

  "Nullmodem", "Serial Cable", "already connected"

Stellen Sie auf beiden Rechnern dieselbe Baudrate ein.


Es k�nnen weitere Parameter angegeben werden, um die Nullmodem-Verbindung
einzurichten:

  port
    TCP-Port. Voreinstellung: 23

  rxdelay
    Wie lange sollen empfangene Daten bereitgehalten werden, wenn das
    Interface nicht bereit ist (in Millisekunden)?
    Erh�hen Sie diesen Wert, wenn das DOSBox-Status-Fenster wiederholt
    die Meldung "overrun error" ausgibt. Voreinstellung: 100

  txdelay
    Wie lange sollen Daten gesammelt werden, bis ein Paket versendet wird?
    Voreinstellung: 12 (kann die Netzwerk-Belastung reduzieren)

  server:Adresse
    Diese Seite des Nullmodems agiert als Client. Wenn der Parameter fehlt,
    agiert diese Seite als Server.

  transparent:1
    Nur serielle Daten senden, keine RTS/DTR-Kontrolle. Benutzen Sie diesen
    Parameter, wenn zu etwas anderem als einem Nullmodem verbunden wird.

  telnet:1
    Telnet-Daten des anderen Rechners auswerten.
    Parameter "transparent" wird automatisch gesetzt.

  usedtr:1
    Die Verbindung wird erst eingerichtet, wenn DTR vom DOS-Programm auf
    "an" gestellt ist. Zur Verwendung mit Modem-Terminals.
    Parameter "transparent" wird automatisch gesetzt.

  inhsocket:1
    Einen Socket verwenden, der DOSBox durch die Kommandozeile angegeben
    wurde (um alte DOS-Spiele �ber neue Mailboxen spielen zu k�nnen).
    Parameter "transparent" wird automatisch gesetzt.


Beispiel:

  Einen Client einrichten, der TCP-Port 5000 abh�rt:
    serial1=nullmodem server:Adresse port:5000 rxdelay:1000



======================================
9. Verbessern der Spielgeschwindigkeit
======================================


DOSBox emuliert den Prozessor, Sound- und Grafikkarten und einiges anderes
mehr - und das alles gleichzeitig. Die Geschwindigkeit, mit der ein DOS-
Programm emuliert werden kann, h�ngt davon ab, wie viele Maschinenbefehle
innerhalb einer gegebenen Zeit emuliert werden k�nnen. Diese Zahl von
Prozessorzyklen oder "Cycles" kann in der Konfigurationsdatei eingestellt
werden (Abschnitt [cpu]).


Cycles

  Die Voreinstellung ("cycles=auto") weist DOSBox an, automatisch zu erkennen,
  ob das Spiel bei h�chstm�glicher Geschwindigkeit (so viele Maschinenbefehle
  wie m�glich) ausgef�hrt werden muss. Durch die Einstellung "cycles=max"
  kann dieses Maximum auch zum Standard gemacht werden. In der Titelleiste des
  DOSBox-Fensters wird dann der Text "Cpu Cycles: max" angezeigt. In diesem
  Modus k�nnen Sie die Zahl der Cycles relativ zum Maximum (also in Prozent)
  reduzieren (Strg-F11) oder wieder erh�hen (Strg-F12).

  Manchmal werden bessere Ergebnisse erreicht, wenn die Zahl der Cycles
  manuell eingestellt wird, beispielsweise indem Sie "cycles=30000" angeben.
  Bei einigen DOS-Programmen k�nnen Sie vielleicht sogar einen noch h�heren
  Wert einstellen (Strg-F12), die Geschwindigkeit ihres Prozessors wird Ihnen
  aber irgendwann Grenzen setzen.
  Die CPU-Auslastung kann im Task-Manager (unter Windows 2000/XP) bzw. im
  System-Monitor (Windows 98/Me) abgelesen werden. Sobald diese Auslastung
  100% erreicht hat, kann DOSBox nicht noch schneller werden, es sei denn, die
  Rechenleistung, die DOSBox f�r Peripherieger�te aufbringen muss, wird
  reduziert.


Cores

  Wenn Ihr Rechner mit einem Intel-kompatiblen CPU (x86-Architektur) l�uft,
  k�nnen Sie versuchen, die Benutzung eines sich dynamisch rekompilierendieren
  Kerns zu erzwingen (setzen Sie in der Konfigurationsdatei die Einstellung
  "core=dynamic"). Sollte die automatische Erkennung ("core=auto") scheitern,
  werden damit oft bessere Ergebnisse erreicht. Am besten benutzen Sie diese
  Einstellung zusammen mit "cycles=max". Bitte beachten Sie aber, dass manche
  Spiele mit dem dynamischen Kern unter Umst�nden schlechter oder sogar
  �berhaupt nicht laufen.


Grafik-Emulation

  Die Emulation der VGA-Grafik ist - was die Prozessorleistung angeht - ein
  sehr anspruchsvoller Teil von DOSBox. Dr�cken Sie Strg-F8, um die Zahl der
  �bersprungenen Frames (in Einserschritten) zu erh�hen. Wenn sie einen
  statischen Cycles-Wert benutzen, sollte sich jetzt die Prozessorbelastung
  reduzieren und der Cycles-Wert kann erh�ht werden (Strg-F12).
  Wiederholen Sie dies so lange, bis das Spiel schnell genug l�uft. Beachten
  Sie bitte, dass Sie hier nur einen Kompromiss aushandeln k�nnen: zwar steigt
  die Geschwindigkeit, daf�r ist das Bild aber nicht mehr so fl�ssig.


Sound-Emulation

  Sie k�nnen auch versuchen, den Sound abzustellen (im Setup-Programm des
  Spiels), um dadurch die Prozessorbelastung zu verringern. Bitte beachten
  Sie, dass die Einstellung "nosound=true" nicht die Emulation der
  Soundkarten unterbindet, sondern lediglich die Soundausgabe.


Versuchen Sie grunds�rtlich, nur so wenige Hintergrundprozesse (oder andere
Programme) wie n�tig am Laufen zu haben, damit DOSBox m�glichst viele
Systemressourcen zur Verf�gung stehen.


Erweiterte Cycles-Konfiguration:

  Die Einstellungen "cycles=auto" und "cycles=max" k�nnen parametriesiert
  werden, um unterschiedliche Voreinstellungen zu setzen:

    cycles=auto "Realmode-Standard" "Protected Mode-Standard"%
                limit "Cycles-H�chstzahl"
    cycles=max "Protected Mode-Standard"% limit "Cycles-H�chstzahl"

    Beispiel: cycles=auto 1000 80% limit 20000
      Benutzt "cycles=10000" im Real Mode sowie 80% CPU-Leistung und h�chstens
      20000 Cycles im Protected Mode.



==================
10. Fehlerbehebung
==================


Wenn DOSBox direkt nach dem Start abst�rzt:

  - bearbeiten Sie die Konfigurationsdatei und probieren Sie verschiedene
    Werte f�r die Variable "output"
  - pr�fen Sie, ob das Problem mit einem Update des Grafikkartentreibers
    oder von DirectX behoben werden kann.


Wenn DOSBox bei bestimmten Spielen abst�rzt, sich schlie�t, oder sich mit
irgendwelchen Fehlermeldungen aufh�ngt:

  - probieren Sie, ob das Spiel mit einer frischen DOSBox-Installation
    funktioniert (unbearbeitete Konfigurationsdatei);
  - deaktivieren Sie den Sound (entweder �ber das Setup-Programm des Spiels
    oder mit den Einstellungen "sbtype=none" und/oder "gus=false" in der
    Konfigurationsdatei;
  - versuchen Sie unterschiedliche Einstellungen in der Konfigurationsdatei,
    insbesondere folgende (u.U. auch eine Kombination davon):
      core=normal
      statischer Cylces-Wert (z.B. "cycles=10000")
      ems=false
      xms=false
  - f�hren Sie vor dem Spiel das interne Programm LOADFIX aus.


Wenn DOSBox das Programm anscheinend l�dt, dann aber mit einer Fehlermeldung
zur Eingabeaufforderung zur�ckkehrt:

  - lesen Sie die Fehlermeldung und versuchen Sie, den Fehler abzustellen;
  - gehen Sie wie beim o.g. Fehler vor;
  - versuchen Sie, das Spieleverzeichnis in einen anderen Ordner oder ein
    anderes Laufwerk einzubinden; manche Spiele lassen sich nur von bestimmten
    Pfaden aus starten; versuchen Sie z.B. statt "MOUNT D D:\GAMES\EARTH"
    den Befehl "MOUNT C D:\GAMES\EARTH" oder auch "MOUNT C D:\GAMES";
  - falls das Spiel eine eingelegte CD-ROM erwartet, stellen Sie sicher, dass
    Sie diese mit dem Parameter "-T cdrom" eingebunden haben und versuchen Sie
    auch zus�tzliche Parameter (-IOCTL, -USECD, -LABEL; siehe den
    entsprechenden Abschnitt);
  - pr�fen Sie, ob das Spiel auf alle Dateien zugreifen kann (Attribut
    "schreibgesch�tzt" entfernen, andere Programme schlie�en, die eventuell
    auf die Dateien zugreifen usw.);
  - versuchen Sie, das Spiel innerhalb von DOSBox neu zu installieren.



===========================
11. Die Konfigurationsdatei
===========================


Eine Konfigurationsdatei kann mithilfe von CONFIG.COM erstellt werden, das
beim Start von DOSBox auf dem internen Z-Laufwerk liegt. N�here Informationen
zur Syntax von CONFIG finden Sie im Abschnitt "Interne Befehle/Programme"
dieser README.
Sie k�nnen die Konfigurationsdatei mit einem Text-Editor bearbeiten, um DOSBox
Ihren Bed�rfnisse anzupassen.

Die Datei besteht aus verschiedenen, durch eckige Klammern gekennzeichneten
Abschnitten. In einigen Abschnitten k�nnen Sie Optionen (Werte) setzen/�ndern.
Kommentarzeilen sind durch die Zeichen "#" oder "%" gekennzeichnet.
Die generierte Konfigurationsdatei beinhaltet die aktuellen Einstellungen. Sie
k�nnen diese �ndern und DOSBox mit dem Parameter "-CONF Datei" starten, um die
Datei zu laden und die neuen Einstellungen zu benutzen.

Zuerst verarbeitet DOSBox die in "~/.dosboxrc" (Linux), bzw. "~\dosbox.conf"
(Windows) oder "~/Library/Preferences/DOSBox Preferences" (MacOS X)
gew�hlten Einstellungen. Danach verarbeitet DOSBox alle Konfigurationsdateien,
die durch den Parameter "-CONF" angegeben wurden. Falls keine angegeben wurde,
wird im aktuellen Verzeichnis nach dosbox.conf gesucht.



===================
12. Die Sprachdatei
===================


Eine Sprachdatei kann mithilfe von CONFIG.COM erstellt werden.
Lesen Sie diese, und Sie werden mit hoher Wahrscheinlichkeit verstehen, wie
man Sie anpasst.

Um Ihre neue Sprachdatei zu verwenden, starten Sie DOSBox mit dem Parameter
"-LANG Datei", alternativ k�nnen Sie den Dateinamen auch im entsprechenden
Abschnitt [dosbox] in der Konfigurationsdatei eintragen ("language=Datei").



============================================
13. Eine eigene Version von DOSBox erstellen
============================================


Laden Sie sich den Source-Code herunter und folgen Sie den Anweisungen in der
im Paket enthaltenen Datei INSTALL.



================
14. Danksagungen
================


Danksagungen der Entwickler finden Sie in der Datei THANKS.



======================
15. Kontaktinformation
======================


E-Mail-Adressen der Entwickler finden Sie unter auf der Crew-Page unter:
http://dosbox.sourceforge.net
