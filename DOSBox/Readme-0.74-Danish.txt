DOSBox v0.74 Manual (brug altid den sidste nye version fra www.dosbox.com)


======
NOTAT: 
======

Selvom Vi h�ber at DOSBOX en dag vil kunne k�re alle programmer der
nogensinde er lavet til PCen, er vi der ikke endnu. 
Lige nu er DOSBox, der k�rer p� en high-end maskine, nogenlunde lig med en 
Pentium I PC.
 DOSBox Kan indstilles til at k�re en bred vifte af DOS spil, fra
CGA/Tandy/PCjr klassikere til spil fra Quake �raen.



======
INDEX:
======
1. Hurtigstart
2. FAQ (Ofte Stillede Sp�rgsm�l)
3. Kommando Linie Parametre
4. Interne Programmer
5. Specielle taster
6. Joystick/Gamepad
7. KeyMapper (Tastatur og joystick indstillinger)
8. Tastatur Layout
9. Serial Multiplayer feature
10. Hvordan du �ndrer hastigheden p� DOSBox
11. Probleml�sning
12. DOSBOX's statusvindue
13. Config-filen (indstillingsfilen)
14. Sprog-filen
15. Hvordan du bygger din egen version af DOSBox
16. Special thanks
17. Kontakt



===============
1. Hurtigstart:
===============

 For en hurtig introduktion, skriv INTRO i DOSBox.
Det er vigtigt at du bliver dus med det at montere(mount-kommandoen),
DOSBox g�r ikke selv automatisk drev(ene) (eller dele af drev(ene)), 
tilg�ngelige for emuleringen. 
Se FAQ : "Kom igang", og beskrivelsen af MOUNT kommandoen 
og beskrivelsen af Mount kommandoen (sektion 4 "Interne Programmer"). Hvis du har
et spil p� cdrom, 
kan du evt. pr�ve denne guide: http://vogons.zetafleet.com/viewtopic.php?t=8933
 



=======
2. FAQ:
=======

KOM IGANG:      Hvordan starter man?
AUTOMATISERING: Skal jeg altid skrive disse "mount" kommandoer?
FULDSK�RM:      Hvordan skifter jeg til fuldsk�rm?
CD-ROM:         Min CD-ROM virker ikke.
CD-ROM:         Spillet/Programmet kan ikke finde sin CD-ROM.
MUS:            Musen Virker Ikke
LYD:            Der er Ingen Lyd.
LYD:            Hvilken Lyd-hardware underst�tter DOSBox ikke/endnu? 
LYD:            Lyden hakker eller lyder forl�nget/m�rkeligt.
TASTATUR:       Jeg kan ikke skrive \ eller : i DOSBox.
TASTATUR:       H�jre skift og "\" Virker ikke i DOSBOx.  
TASTATUR:       Tastaturet hakker.
KONTROL:        Figuren/cursoren bev�ger sig altid i en retning!
HASTIGHED:      Spillet/Programmet k�rer for langsomt/for hurtigt!
NEDBRUD:        Spillet/Programmet k�rer overhovedet ikke/bryder ned!  
NEDBRUD:        DOSBox bryder ned ved opstart!
SPIL:           Mit Build spil(Duke3D/Blood/Shadow Warrior) har problemer.
SIKKERHED:      Kan DOSBox skade min Computer?
Indstillinger:  Jeg vil gerne �ndre DOSBox's indstillinger.   
HJ�LP:          God manual, men jeg forst�r det stadig ikke.



START: Kom igang?
    Til at begynde med har du et Z:\ istedet for C:\ ved prompten.
    Du kan g�re dine mapper/directories/biblioteker brugbare som drev i DOSBox
    ved hj�lp af "mount" kommandoen. F. eks. vil, i Windows, kommandoen 
    "mount C D:\GAMES" give dig et C drev i DOSBox som peger mod din Windows 
    D:\GAMES Mappe.
    I Linux, vil "mount c /home/username" give dig et C drev i DOSBox som
    peger mod /home/username i Linux.
    Skriv "C:" for at skifte til det f�rn�vnte monterede drev. Hvis Alting gik 
    godt, vil DOSBox will vise the prompten "C:\>". 


AUTOMATISERING: Skal jeg altid udf�re disse kommandoer?
    Der er i DOSBox's config-fil en [autoexec] sektion. Kommandoerne som er 
    skrevet der k�res n�r DOSBox startes, s� du kan bruge denne sektion til at 
    montere. Se sektion 13. Config-filen (indstillingsfilen) 



FULDSK�RM: Hvordan �ndrer jeg til fuldsk�rm modus?
    Pres alt-enter. Alternativt: Ret DOSBox's config-fil og �ndr muligheden   
    fullscreen=false til fullscreen=true. Leg med muligheden : fullresolution hvis
    fuldsk�rms modus ser forkert ud efter din mening. Pres alt-enter igen for at 
    komme tilbage fra fuldsk�rms modus. 


CD-ROM: Min CD-ROM virker ikke.
    For at montere din CD-ROM i DOSBox Skal du specificere yderligere nogle mulig-
    heder n�r du monterer. 
    For at muligg�re den mest grundl�ggende CD-ROM underst�ttelse (inkluderer 
    MSCDEX) :
      - mount d f:\ -t cdrom (Windows)
      - mount d /media/cdrom -t cdrom (Linux) 

    M�ske �nsker du m�ske at bruge et andet CD-ROM interface,
    f.eks hvis CD audio ikke virker:      
    For SDL-underst�ttelse(inkluderer ikke lav-niveau CD adgang)
      - mount d f:\ -t cdrom -usecd 0 -noioctl
    For underst�ttelse af ioctl med digital audio extraction for CD audio
    (kun Windows, nyttigt for Vista):
      - mount d f:\ -t cdrom -ioctl_dx
    For underst�ttelse af ioctl med MCI for CD audio(kun Windows):
      - mount d f:\ -t cdrom -ioctl_mci
    For at tvinge brug af ioctl-only(kun Windows):
      - mount d f:\ -t cdrom -ioctl_dio
    For at muligg�re lav-niveau aspi-underst�ttelse(win98 med aspi-lag installeret) :
      - mount d f:\ -t cdrom -aspi
    
    Kommandoerne :   - d   drevbogstav du f�r i DOSBox
                     - f:\ placering af cdrom i din PC.
                     - 0   Nummeret af �CD-ROM drevet, findes med mount -cd   
                           (bem�rk at denne v�rdi er kun n�dvendig n�r du bruger 
                            SDL til CD audio, ellers ignoreres den)
    Se ogs� n�ste sp�rgsm�l : Spillet/Programmet kan ikke finde sin CD-ROM.


CD-ROM: Spillet/programmetgamet kan ikke finde sin CD-ROM.
    V�r sikker p� at montere din CD-ROM med -t cdrom switchen, dette vil starte
    MSCDEX fladen som DOS spil kr�ver for at give adgang til CD-ROM.
    Pr�v ogs� at tilf�je korrekt label/etik�t (-label LABEL) til mount kommandoen. 
    Hvor LABEL er CD-ROMens CD-label(volume ID).
    Under Windows kan du specificere -ioctl -aspi eller -noioctl. Se beskrivelse 
    i sektion 4: "Interne Programmer"om deres betydning og deres audio-relaterede
    muligheder -ioctl_dx, ioctl_mci, ioctl_dio.
   
    Pr�v at lave et CD-ROM billede/image(helst CUE/BIN), og brug DOSBox's interne 
    IMGMOUNT kommando til at montere billedet. Dette muligg�r meget god lav-niveau
    CD-ROM support p� alle operativ systemer.


MUS: Musen virker ikke.
    Normalt finder DOSBox ud af om et spil bruger Mus.N�r du klikker p� sk�rmen
    (DOSBox vinduet)skulle den l�se/bindes, og virke. 
    Ved nogle spil virker dette ikke, s� du m� selv l�se/binde musen, ved at taste
    CTRL-F10. 


LYD: Der er ingen lyd.
    V�r sikker p� at lyden er korrekt indstillet i spillet. Dette g�res under 
    installationen eller med et setup/setsound program som f�lger med spillet. 
    Se f�rst om der er auto-detektion. Hvis der ikker er det, s� pr�v at v�lge
    soundblaster eller soundblaster 16 med default settings : "address=220 irq=7 
    dma=1". Du �nsker m�ske ogs� at v�lge 
    Sound Canvas/SCC/MPU-401/General MIDI/Wave Blaster p� address 330 IRQ=2 som 
    musik enhed.
    Parametrene til de emulerede lydkort kan �ndres i DOSBox's config-fil.
    Hvis du stadig ikke f�r nogen lyd kan du s�tte core til normal og bruge nogle 
    lavere valgte cycles v�rdier (F.eks. cycles=2000). V�r ogs� sikker p� at din
    lydenhed leverer lyd.
    I visse tilf�lde kan det v�re godt at bruge en anden emuleret lydenhed
    f.eks soundblaster pro(sbtype=sbpro1 i DOSBox's config fil) eller
    gravis ultrasound(gus=true).  


LYD: Hvilken Lyd-hardware emulerer DOSBox lige nu?
    DOSBox emulerer adskillige lyd-enheder:
    - Indbygget PC-h�jtaler/Buzzer
      Denne emulering inkluderer b�de tonegeneratoren og flere former for digital 
      lyd gennem den indbyggede h�jtaler.
    - Creative CMS/Gameblaster
      Dette er Creative Labs(R)'s f�rste kort. Standard config s�tter det p� 
      adressen 220. Det er sl�et fra som standard.
    - Tandy 3 voice
      Emuleringen mangler "st�j-kanalen", som ikke er s�rlig godt dokumenteret, og
      er som s�dan kun det "et bedre g�t" p� lyd n�jagtigheden. Det er sl�et fra 
      som standard.
    - Tandy DAC
      Nogle spil kan kr�ve at sound blaster emuleringen sl�s fra(sbtype=none), for 
      at give bedre tandy DAC underst�ttelse(husk at s�tte sbtype tilbage p� sb16
      efter brug).
    - Adlib
      Denne emulering er n�sten perfekt og inkluderer Adlib's evne n�sten til at 
      spille "digitized" lyd. Adressen er 220 (ogs� 388).
    - SoundBlaster 16 / SoundBlaster Pro I og II / SoundBlaster I og II
      Som standard leverer SoundBlaster 16 niveau 16-bit stereo lyd . Du kan v�lge
      en anden SoundBlaster version i DOSBox's indstillinger. AWE32 musik er ikke
      emuleret, da du kan bruge MPU-401 istedet(se nedenunder).  
    - Disney Sound source og Covox Speach Thing
      Bruger printerporten, enheden sender kun digital lyd ud. Placeret p� LPT1.
    - Gravis Ultrasound          
      Emuleringen af denne hardware er n�sten komplet, selvom midi-funktionerne er 
      udeladt, da der er en MPU-401, emuleret i anden kode. For at f� Gravis 
      musik, kan det v�re n�dvendigt at installere Gravis Drivere i selve DOSBox. 
      Det er sl�et fra som standard.
    - MPU-401
      Et midi gennemgangs interface er ogs� emuleret. Denne form for lydudgang 
      virker kun med "udenoms" enhed/emulator.
      Windows XP/Vista/7 og MAC OS har standard en emulator der er kompatibel
      med: Sound Canvas/SCC/General Standard/General MIDI/Wave Blaster.
      Der skal bruges en anden enhed/emulator til Roland LAPC/CM-32L/MT-32
      kompatabilitet.   


 
LYD: Lyden hakker eller lyder m�rkelig.
    Du bruger m�sk� for meget cpu kraft til at holde DOSBox k�rende ved den 
    aktuelle hastighed. Du kan neds�tte cycles, skippe frames reducere sampling 
    raten p� den p�g�ldende lydenhed (se DOSBox's config-fil) eller mixer-enheden.
    Du kan ogs� for�ge prebufferen. Se sektion 13. "Config-filen (indstillingsfilen)" 
    Hvis du bruger cycles=max eller =auto , s� v�r sikker p� at der ingen bag-
    grundsprocesser k�rer, som forstyrrer! (s�rligt hvis de bruger harddisken)
    Se ogs� sektion 10. "Hvordan du �ndrer hastigheden p� DOSBox" 



TASTSTUR: Jeg kan ikke skrive \ eller : i DOSBox.
    Dette er et kendt problem. Det opst�r hvis dit keyboard/tastatur layout 
    ikke er har et tilsvarende DOS layout (eller ikke blev genkendt korrekt),
    eller tasterne er forkert tildelt.
    Nogle mulige l�sninger:
      1. Brug / istedet for, eller Alt-58 istedet for : og Alt-92 istedet for \.
      2. Lav om p� dit DOS tastatur layout (se sektion 8 : Tastatur layout).
      3. Tilf�j de kommandoer(extra) som du vil k�re i [autoexec]-sektionen 
         i DOSBox's "config-fil".
      4. �bn config-filen og lav usescancodes=false om til usescancodes=true.
      5. Skift tastatur layout i dit operativsystem.  

     Bem�rk at hvis v�rtslayoutet ikke kan genkendes, eller tastaturlayout er 
     sat til none i DOSBox's config-fil, bruges standard US layout.
     Pr�v i s�fald tasterne omkring "enter" for \ og pr�v skift og tasterne 
     imellem "enter" og "L" for ":" .   



TASTATUR: H�jre Skift og "\" virker ikke i DOSBox. (kun Windows)
     Dette forekommer n�r Windows "tror" at du har mere end �t tastatur tilsluttet,
     fordi du bruger fjernstyrede enheder. tjek det med :
     start cmd.exe
     navig�r til DOSBox's programfolder
     skriv set sdl_videodriver=windib og tast enter
     tast dosbox.exe og tast enter
     Hvis det virker som det skal, er det bedre at bruge en af de to l�sninger h�r:
     http://vogons.zetafleet.com/viewtopic.php?t=24072 (da windib er langsommere). 

 
    
TASTATUR: Keyboardet/tastaturet forsinkes.
    S�nk prioritetssindstillingen i DOSBox's config-fil, pr�v f.eks. :
    "priority=normal,normal". Du kan ogs� s�tte et lavere antal cycles
    (brug fast antal cycles under start f.eks cycles=10000).    



KONTROL: Figuren/mark�ren bev�ger sig altid i en retning!
    Se om det stadig sker hvis du sl�r joystick emuleringen fra,
    s�t joysticktype=none i [joystick] sektionen i DOSBox's config-fil.
    Du skal m�sk� ogs� pr�ve at tr�kke stik(ene) ud p� dit/dine joystick(s).
    Hvis du �nsker at bruge joystick i spillet, pr�v s� at s�tte timed=false,
    calibr�r joysticket(b�de dit OS og i spillet eller dit spil's setup).  



HASTIGHED: Spillet/Programmet k�rer for langsomt/for hurtigt!
    Se i sektion 10. "Hvordan du �ndrer hastigheden p� DOSBox".



NEDBRUD: Spillet/Programmet k�rer overhovedet ikke/bryder ned!  
    Se sektion 11: "Probleml�sning".



NEDBRUD: DOSBox bryder ned ved opstart!
    Se sektion 11: "Probleml�sning".


        
SPIL: Mit Build spil(Duke3D/Blood/Shadow Warrior)virker ikke som det skal.
    Pr�v f�rst at finde en �ndret udgave af spillet. disse giver en
    en bedre spil-oplevelse. For at l�se grafik-problemerne som forekommer med
    DOSBox i h�jere opl�sninger. �bn DOSBox's config-fil find machine=svga_s3
    lav svga_s3 om til vesa_nolfb.
    �ndr memsize=16 til memsize=63



SIKKERHED: Kan DOSBox skade min computer?
    DOSBox kan ikke skade din computer mere et hvilket som helst andet resource
    kr�vende program. for�gelse af cycles overclocker ikke din fysiske CPU.
    for h�jt sat cycles har en negativ ydelseseffekt p� software der k�rer i 
    DOSBox. 



Indstillinger:  Jeg vil gerne �ndre DOSBox's indstillinger.   
    Se sektion 13. "Config-filen (indstillingsfilen)"



HJ�LP: God manual, men jeg forst�r det stadig ikke.
    L�s resten af denne Manual Tag ogs� et kig p� guider du kan finde p�:
    http://vogons.zetafleet.com/viewforum.php?f=39
    DOSBox's wiki http://www.dosbox.com/wiki/
    Forumet: http://www.dosbox.com



===========================
3. Kommando Linie Parametre
===========================

Et overblik over kommandolinie options/mulighederne du kan bruge med DOSBox.
Selvom det, i de fleste tilf�lde, er nemmere at bruge DOSBox's config-fil.
Se sektion 13. "Config-filen (indstillingsfilen)"

For at kunne bruge kommando-parametre, skal du:
(windows)  �bne cmd.exe, eller command.com, eller rette i Genvej/shortcut til 
DOSBox.exe.
(Linux)  Brug konsollen.
(MAX OS X) start terminal.app og navig�r til:
           /applications/dosbox.app/contents/macos/dosbox

Mulighederne er brugbare for alle operativ systemer medmindre der st�r andet
i options beskrivelsen:

dosbox [navn] [-exit] [-c command] [-fullscreen] [-userconf] [-conf congfig-fil] 
       [-lang sprog-fil] [-machine maskinetype] [-noconsole]
       [-startmapper] [-noautoexec] [-securemode] 
       [-scaler scaler | -forcescaler scaler]
       [-version] [-socket socket]
       
       
dosbox -version
dosbox -editconf program
dosbox -opencaptures program
dosbox -printconf
dosbox -eraseconf
dosbox -erasemapper

  name   
        Hvis "navn" er et directory/en mappe/et bibliotek, bliver det/den/det 
        monteret som C: drevet.
        Hvis "navn" er en eksekverbar fil, bliver "navn"s 
        directory/mappe/bibliotek monteret som C: drevet og "navn" eksekveret.
    
  -exit  
        DOSBox lukker sig selv n�r programmet "navn" afsluttes.

  -c command
        K�rer den specificerede kommando f�r "navn" k�res. Der kan specificeres 
        flere kommandoer. Hver kommando starter dog med "-c".
        En kommando kan v�re et internt program, en DOS kommando eller en 
        eksekverbar fil p� et monteret drev.

  -fullscreen
        Starter DOSBox i fuldsk�rm modus.

  -userconf
        StartER DOSBox MED BRUGER-specifiK config-fil. kan bruges sammen med flere
        -conf parametre, men -userconf indl�ses altid f�rst.

  -conf config-fil
        Starer DOSBox med options/muligheder specificeret i "config-fil"(KAN 
        v�re n�dvendig med fuld sti).
        Der kan v�re flere -conf muligheder.
        Se sektion 13 for flere detaljer.

  -lang sprog-fil 
        Start DOSBox med sproget specificeret i "sprog-fil".
        Se sektion 14 for flere detaljer.

  -machine maskinetype
        S�t DOSBox til at emulere en speciel type maskine. brugbare valg er:
        hercules, cga, ega, pcjr, tandy, svga_s3 (standard) som de andre
        svga chipsets der er n�vnt i DOSBox's config-fil.
        b�de grafikkort og tilg�ngelige lydkort. svga_s3 tilf�jer ogs� vesa-
        emulering. For nogle specielle vga-effekter, kan v�lges machine typen 
        vgaonly, bem�rk at dette fjerner svga muligheder og kan v�re (betydelig)
        langsommere p� grund af den meget st�rre emuleringsprecission.
        Valget af maskinetype anf�gter b�de grafikkort og tilg�ngelige lydkort.
        

  -noconsole (Windows Only)
        Start DOSBox uden at vise konsol-vinduet. Output bliver omstillet til
        stdout.txt and stderr.txt
	
  -startmapper
        F� direkte adgang til keymapperen ved opstart. Brugbart hvis du har 
        keyboard/tastatur problemer.

  -noautoexec
        Skipper [autoexec] sektionen af den indl�ste config-fil.

  -securemode
        Samme som -noautoexec, men tilf�jer config.com -securemode i 
        bunden af AUTOEXEC.BAT (hvilket fjerner �ndringer i forhold  til hvordan 
        drevene monteres i selve DOSBox).

  -scaler scaler
        Bruger scaleren angivet med "scaler". Se i DOSBox's config-fil
        hvilke scalere du kan bruge.

  -forcescaler scaler
        Ligesom -scaler parameteren, men pr�ver at tvinge brugen af
        den specificerede scaler selvom den m�sk� ikke passer.

  -version
        Skriver version information og afslutter. Brugbart for Frontends.

  -editconf program
        Kalder program med config-filen som f�rste parameter.
        Man kan skrive denne kommando mere end en gang. Hvis man g�r det
        �bnes andet program, hvis det f�rste fejler.

  -opencaptures program
        Kalder program med captures folderen/directoryet/biblioteket som
        f�rste parameter.
  
  -printconf
        Skriver placeringen af standard config-fil.

  -resetconf
        Fjerner standard config-fil.

  -resetmapper
        Fjerner mapperfilen der bliver brugt af standard config-fil.

  -socket
        Sender sokkel nummer til nullmodem emul�ringen. See Section 9:
        "Serial Multiplayer feature."

Note: Hvis navn/kommando/configfil/sprog-fil indeholder mellemrum, skal du s�tte
     navn/kommando/configfil/sprog-fil i anf�relsestegn("kommando eller filnavn").
     Hvis skal bruge anf�reslsetegn inden i anf�reslsetegn(sansynligvis med 
     -c og mount): 
     Windoes og Os2 brugere kan bruge enkelt anf�rselstegn inden i almindelige 
     anf�rselstegn. Andre b�r kunne bruge "escaped double quotes"(\") inden
     i lamindelige anf�rselstegn.
     Windows: -c "mount c 'c:\My folder with DOS games\'"
     Linux: -c "mount c \"/tmp/name with space\""

 
Et noget us�dvanligt eksempel, til demonstration (windows):
dosbox.exe D:\folder\file.exe -c "MOUNT Y H:\MyFolder"
  Dette monterer D:\folder as C:\ and runs file.exe.
  men f�r den g�r dette monteres H:\MyFolder som Y drevet.

I Windows kan du ogs� tr�kke foldere/filer hen p� DOSBox.exe(ell. p� genvej til).



=======================
4. Interne Programmmer:
=======================

DOSBox underst�tter de fleste DOS kommandoer der bruges i command.com.
Du kan skrive "HELP" ved prompten(efterfulgt af enter) for at f� en liste over 
de interne kommandoer.

Desuden er de f�lgende kommandoer tilg�ngelige: 

MOUNT "Emuleret Drev bogstav" "Rigtige Drev eller Folder" 
      [-t type] [-aspi] [-ioctl] [-noioctl] [-usecd nummer] [-size drevst�rrelse] 
      [-label drevlabel] [-freesize st�rrelse_i_mb]
      [-freesize st�rrelse_i_kb (floppies)]  
MOUNT -cd
MOUNT -u "Emuleret Drev Bogstav"

  Program til at montere lokale directories/mapper/biblioteker som drev i DOSBox.

  "Emuleret Drev Bogstav"
        Drev Bogstavet i DOSBox (f.eks. C).

  "Rigtige Drev bogstav (normalt for CD-ROMMer i Windows) eller Folder"
        Det/den lokale directory/mappe/bibliotek du �nsker at tilg�ngeligt i DOSBox.

  -t type
        Type af monteret directory. f�lgende kan bruges: dir (default),
        floppy, cdrom.

  -size drevst�rrelse     
        S�tter st�rrelsen p� drevet, hvor drevst�rrelse er angivet i :
        "bps,spc,tcl,fcl":
           bps: bytes pr sektor, default 512 for regul�re drev og
                2048 for CD-ROM drev
           spc: sektorer pr klynge, normalt mellem 1 and 127
           tcl: total klynger, mellem 1 and 65534
           fcl: total frie klynger, mellem 1 og tcl

  -freesize st�rrelse_i_mb | st�rrelse_i_kb
        S�tter m�ngden af fri plads p� drev i megabytes.
        (regul�re drev) eller kilobytes  (floppy drev).
        Dette er en simplere version af -size.	

  -label drevlabel
        S�tter navnet p� drevet til "drevlabel". Er n�dvendigt p� nogle systemer
        hvis CD'ens label ikke bliver l�st korrekt (V�rdifuldt n�r et program 
        ikke kan finde sin CDROM). Hvis du ikke specificerer en/et label og der
        ikke er valgt lav-niveau underst�ttelse (-usecd # og/eller -ioctl/-aspi
        /-noioctl): 
          Windows: label bliver hentet fra "Rigtige Drev".
          Linux: label bliver sat til NO_LABEL.

        Hvis du specificerer en/et label, vil den/dette label vare lige s� l�nge
        som drevet er monteret. Det vil ikke blive opdateret !!

  -aspi
        Tvinger brugen af aspi-lag. Kun brugbar hvis cdrom monteres under 
        Windows systemer med ASPI-Lag.

  -ioctl (automatisk valg af CD audio interface)
  -ioctl_dx (der bruges digital audio extraction til CD audio)
  -ioctl_dio (ioctl kald bruges til CD audio)
  -ioctl_mci (MCI bruges til CD audio)
        Tvinger brug af ioctl kommandoer, kan kun bruges til at montere CD-ROM
        p� et Windows OS som underst�tter dem (Win2000/XP/NT).
        De forskellige valg er kun forskellige i m�den CD-Audio h�ndt�res,
        bedste valg kan v�re -ioctl_dio(mindst resourcekr�vende), men virker
        det ikke, kan -ioctl_dx (eller -ioctl_mci) bruges.
   
  -noioctl   
        Tvinger brug af SDL CD-ROM laget. Brugbart til alle systemer.

  -usecd nummer
        Kan bruges p� alle systemer, under Windows skal -noioctl switchen v�re
        tilstede for at kunne bruge -usecd switchen. 
        G�r det muligt at v�lge drevet, SDL skal bruge. Brug det hvis det forkerte 
        eller ingen CDROM-drev bliver monteret n�r du bruger SDL CDROM interfacet.
        "nummer" kan findes med kommandoen "MOUNT -cd". 
      
  -cd
        Viser alle SDL-fundne cdrom drev og deres numre Bruges sammen med -usecd.
        Se informationen under -usecd ovenover. 
  -u
        Fjerner monteringen. Virker ikke for Z:\.

  Note: Det er muligt at montere lokalt directory/mappe/bibliotek som cdrom drev. 
        i s� fald er der ingen Hardware Underst�ttelse.

  I bund og grund tillader MOUNT dig at montere reel hardware til DOSBox's emu-
  leret PC.
  S� MOUNT C C:\Dosspil f�r DOSBox til at bruge din  C:\Dosspil Folder som C:
  i DOSBox. I DOSBox vil MOUNT C E:\EnFOlder lade DOSBox bruge E:\EnFolder som 
  drev C: i DOSBox.

  Det er ikke anbefalet at Montere hele C drevet med MOUNT C C:\ Det samme g�lder
  for at montere roden et andet drev, bortset fra CD-ROMer (grundet af deres ikke 
  skrivebare natur). Eller du eller DOSBox kan lave fejl - s� du risikerer at 
  miste alle dine filer. Lad ogs� v�re med at Montere "Windows" eller "Programmer"
   eller deres under-foldere i Windows Vista/7 , da det kan forhindre DOSBox i at 
  virke korrekt, eller virke korrekt senere. Det anbefales at have alle spil/
  programmer i en simpel folder, f.eks c:\Dosspil(eller underfoldere til) og 
  s� montere den.


  Du b�r altid installere dit spil I DOSBox
  S� hvis du har CD'en b�r du altid(selv efter installation) montere b�de 
  Folderen som harddisk og CDROMMEN
  Harddisk b�r monteres som c
    CDROM b�r monteres som  d
    Floppy b�r monteres som a (ell. b)

  Generelle MOUNT Eksempler (windows):

  1. At montere Folder som Harddiskdrev :
          mount c d:\Dosspil

  3. At montere dit CDROM drev E som cdrom drev D i DOSBox:
          mount d e:\ -t cdrom

  2. At montere a: som diskette : 
          mount a a:\ -t floppy
  
  Avancerede monteringseksempler (windows):

  4. At montere et drev med 870 mb fri diskplads (simpel version):
          mount c d:\Dosspil -freesize 870


  5. At montere et drev med 870 mb free diskspace (kun eksperter, fuld kontrol):
          mount c d:\Dosspil -size 512,127,16513,13500

  1. At montere c:\Dosspil\floppy som diskette : 
          mount a c:\Dosspil\floppy -t floppy


  Andre monteringseksempler:

  3. At montere system cdrom drev p� mountpoint /media/cdrom som cdrom drev D 
     i DOSBox:
          mount d /media/cdrom -t cdrom -usecd 0

  6. At montere /home/user/Dosspil som drev C in DOSBox:
          mount c /home/user/Dosspil

  7. At montere Mappe hvor DOSBox blev startet som D i DOSBox:
     mount d .
     (l�g m�rke til . som repr�senter mappen hvor DOSBox blev startet)  

  Hvis du �nsker at montere et cd-billede/image, pr�v IMGMOUNT.
  Mount virker ogs� med cd-billeder/images, men kun hvis du bruger 
  eksterne programmer f.eks(begge er gratis):
  - Daemon Tools Lite (til CD billeder/images),
  - Virtual Floppy Drive (til floppy images).
  Selvom IMGMOUNT skulle give en bedre kompatabilitet.


MEM
  Program til at vise st�rrelsen p� fri hukommelse.


VER
VER set hoved_version [under_version]
  Viser nuv�rende DOSBox version og raporteret DOS version
  (uden parameter).
  �ndrer den raporterede DOS version med "set" parameteren,
  f.eks: "VER set 6 22" for at f� DOSBox til at raportere DOS 6.22
  som version nummer.


CONFIG -writeconf lokal-fil
CONFIG -writelang lokal-fil
CONFIG -securemode
CONFIG -set "sektion egenskab=v�rdi"
CONFIG -get "sektion egenskab"

  CONFIG kan bruges til at �ndre eller foresp�rge forskellige indstillinger i 
  DOSBox under brug. CONFIG kan gemme "nuv�rende indstillinger" og "sprogstrenge"
  til disken(f.eks generere en dansk dosbox.conf). CONFIG Information om alle 
  mulige sektioner kan findes i sektion 13: "Config-filen (indstillingsfilen)".

  -writeconf lokal-fil
       Skriver de nuv�rende indstillinger til fil "lokal-fil" er lokaliseret p� 
       det lokale drev ikke p� et monteret drev i DOSBox. 
       CONFIG-filen kontrollerer forskellige DOSBox-indstillinger : 
       st�rrelsen p� emuleret hukommelse, de emulerede lydkortog mange andre ting
       CONFIG-filen giver dig ogs� adgang til AUTOEXEC.BAT.
       Se gerne sektion 13. "Config-filen (indstillingsfilen)".

  -writelang lokal-fil
       Skriver de nuv�rende sprog-indstillinger til fil. "lokal-fil" er lokali-
       seret p� det lokale drev ikke p� et monteret drev i DOSBox. 
       Sprog-filen kontrolerer alle synlige output fra de interne kommandoer og
       den interne DOS.
       Se gerne sektion 14 "sprog-filen".
  
  -securemode
       Skifter DOSBox til mere sikker modus. I dette modus virker de interne
       kommandoer MOUNT, IMGMOUNT and BOOT ikke. Det er heller ikke muligt at 
       kreere en ny config-fil eller language-fil i dette modus.
       (Advarsel: du kan kun afslutte dette modus ved at genstarte DOSBox.)

  -set "sektion egenskab=v�rdi"
       CONFIG vil pr�ve at s�tte p�g�ldende egenskab til en ny v�rdi. Lige nu
       kan CONFIG ikke fort�lle om kommandoen lykkedes eller ikke.

  -get "sektion egenskab"
       Nuv�rende v�rdi af p�g�ldende egenskab skrives og gemmes i milj�-variablen 
       %CONFIG%.Denne kan bruges til at gemme v�rdien n�r man bruger batch filer.

  B�de "-set" og "-get" virker fra batch filer og kan bruges til at generere egne
  indstillinger for hvert spil. Det er dog m�ske lettere at bruge forskellige
  DOSBox config-filer.
  
  Eksempler:
  1. At lave  en config-fil i nuv�rende i din c:\Dosspil folder:
      config -writeconf c:\dosspil\dosbox.conf
  2. At s�tte cpu cycles til 10000:
      config -set "cpu cycles=10000"
  3. At afbryde ems hukommelses emulering:
      config -set "dos ems=off"
  4. At se hvilken cpu core/kerne der bruges.
      config -get "cpu core"


LOADFIX [-st�rrelse] [program] [program-parameters]
LOADFIX -f
  Program til at reducere m�ngden af fri hukommelse. Brugbar til gamle
  programmer der ikke forventer meget fri hukommelse. 

  -size	        
        antal kilobytes at "�de op", default = 64kb
  
  -f
        frig�r alt tidligere allokeret hukommelse
  

Eksempler:
  1. At starte mm2.exe og allokere 64kb hukommelse 
     (mm2 will have 64 kb less available) :
     loadfix mm2
  2. At starte mm2.exe og allokere 32kb hukommelse :
     loadfix -32 mm2
  3. At frig�re tidligere allokeret hukommelse :
     loadfix -f


RESCAN
  F�r DOSBox til at genindl�se directory/mappe/biblioteks strukturen. Brugbar 
  hvis du har �ndret noget, p� et monteret drev, udenfor DOSBox. (CTRL-F4 g�r ogs�
  dette!)
  

MIXER
  F�r DOSBox til at vise nuv�rende lydindstillinger. 
  Her er mulighederne for at �ndre dem:
  
  mixer channel left:right [/NOSHOW] [/LISTMIDI]
  
  channel
      Kan v�re : MASTER, DISNEY, SPKR, GUS, SB, FM,  [, CDAUDIO].
      CDAUDIO er kun tilg�ngeligt hvis et CDROM interface med volume  kontrol
      er muliggjort (CD image, ioctl_dx). 

  left:right
      Lydniveauet i procent. Hvis du s�tter D foran �ndres det til 
      decibell (eksempel mixer gus d-10).
  
  /NOSHOW
      Forhindrer DOSBox  i at vise resultatet hvis du s�tter et lydniveau.

  /LISTMIDI
      Skriver en liste over tilg�ngelige midi enheder p� din pc (Windows). 
      Du kan v�lge en anden enhed end Windows default midi-mapper, ved at �ndre
      linien 'midiconfig=' [midi] sektionen i Config-filen, til 
      'midiconfig=id', hvor 'id' er nummeret p� enheden fra listen genereret af 
      LISTMIDI f.eks midiconfig=2.

      Dette virker ikke i Linux, men du kan n� tilsvarende resultat(er) ved at
      bruge 'pmidi -l' i konsol. S� �ndre linien 'midiconfig=' til 
      'midiconfig=port', hvor 'port' er porten for enheden listet med 'pmidi -l'.
       f.eks. midiconfig=128:0 


IMGMOUNT
  Et program til am montere disk images og CD-ROM images i DOSBox (f.eks. en iso).
  
  IMGMOUNT DREV [imagefil] -t [image_type] -fs [image_format] 
            -size [sectorsbytesize, sectorsperhead, heads, cylinders]
  IMGMOUNT DRIVE [imagefile1, .. ,imagefileN] -t iso -fs iso 

  imagefil
      Placering af image-fil der skal monteres i DOSBox. Placeringen kan v�re p� 
      et monteret drev i DOSBox, eller p� din fysiske disk. Det er ogs� muligt at
      montere CD-ROM images (ISOer eller CUE/BIN), Hvis du har brug for at kunne 
      "skifte cd" skal du skrive alle images i r�kkef�lge 
      (se n�ste indgang)
   
      CUE/BIN s�t, er de foretrukne CD-ROM images da de kan indeholde lydspor,
      modsat ISOer (som kun kan indeholde data-spor). N�r du skal 
	      montere CUE/BIN, skal du altid bruge .CUE-filen

  imagefile1, .. ,imagefileN
      Placeringen af image-filer der skal monteres i DOSBox. At specificere et 
      antal image-filer er kun tilladt for CD-ROM images. CD'erne kan 
      skiftes med CTRL-F4 til enhver tid. Dette er n�dvendigt med spil som bruger
      flere CD-ROMMER og kr�ver at CD'en bliver skiftet undervejs i spillet.
   
  -t 
      F�lgende er godkendte image typer:
        floppy: Specificerer et eller flere floppy image(s).  DOSBox finder selv 
                diskens geometri (360K, 1.2MB, 720K, 1.44MB, osv.).
        cdrom:  Specificerer et CD-ROM iso image.  Geometrien bliver sat automa-
                tisk. Kan v�re en iso eller cue/bin.
        hdd:    Specificerer et harddisk image. Den brugelige CHS geometri skal
                skrives for at det virker.

  -fs 
      F�lgende er brugbare filsystem formater:
        iso:  Specificerer ISO 9660 CD-ROM formatet.
        fat:  Specificerer at imaget bruger FAT filsystemet. DOSBox vil fors�ge
              at montere dette image som et drev i DOSBox og g�re filerne tilg�ngelige 
              i DOSBox.
        none: DOSBox G�r ikke noget fors�g p� at l�se filsystemet p� disken.
              Dette bruges hvis hvis du skal formatere den eller starte den med med 
              BOOT kommandoen.  N�r du bruger "none" filsystem, er det bedre at
              specificere drevnummer (2 eller 3, 
               2 = master, 3 = slave) end et drevbogstav.  
              For eksempel monteres et 70MB image som slave drev, 
              s�dan(uden anf�relsestegn):
                "imgmount 3 d:\test.img -size 512,63,16,142 -fs none" 
                (uden anf�relsestegn)  sammenlignet med en montering for at l�se 
                drevet i DOSBox, som ser s�dan ud: 
                "imgmount e: d:\test.img -size 512,63,16,142"

  -size 
     Specificering af drevets Cylindre, Heads og Sektorer.
     Er n�dvendigt for at montere harddisk drev images.
     
  Et eksempel p� hvordan man monterer CD-ROM images (i Linux):
    1. imgmount d /tmp/cdimage1.cue /tmp/cdimage2.cue -t cdrom
  eller(som ogs� virker) 
    2a. mount c /tmp
    2b. imgmount d c:\cdimage1.cue cdimage2.cue -t iso
  (i Windows):
    imgmount d f:\img\CD1.cue f:\img\CD2.cue f:\img\CD3.cue -t cdrom
    imgmount d "g:\img\7th Guest CD1.cue" "g:\img\7th Guest CD2.cue" -t cdrom
  Glem ikke at du ogs� kan bruge MOUNT med image(s), men kun hvis du bruger externe 
  programmer(begge er gratis):
  - Daemon Tools Lite (for CD images),
  - Virtual Floppy Drive (for floppy images).
  Selvom IMGMOUNT kan give bedre kompatabilitet.


BOOT
  Boot starter floppy images eller harddisk images uafh�ngigt af operativ-
  systemes emuleringen DOSBox tilbyder. Dette tillader dig at spille starter-
  disketter eller starte andre operativsystemer.
  Hvis det valgte emulerede system er PCjr (machine=pcjr) kan boot kommandoen
  bruges til at indl�se PCjr magasiner (.jrc). 

  BOOT [diskimg1.img diskimg2.img .. diskimgN.img] [-l drevbogstav]
  BOOT [cart.jrc]  (PCjr only)

  diskimg1.img diskimg2.img .. diskimgN.img
     Kan v�re et relativt nummer p� diskette/floppy -images, der �nskes monteret
     efter at DOSBox starter(booter) det specificerede drevbogstav.
     du kan taste CTRL-F4 for at skifte fra nuv�rende disk til n�ste disk
     p� listen. Listen starter forfra efter sidst disk image.

  [-l drevbogstav]
     Denne parameter tillader dig at specificere drevet du vil starte fra.  
     Default er A drevet, floppy drevet. Du kan ogs� starte et harddisk image 
     monteret som master ved at specificere "-l C" uden anf�relsestegn, eller
     starte drevet som slave ved at specificere "-l D"
     
   cart.jrc (PCjr only)
     N�r emulering af PCjr er sl�et til, kan man indl�se magasiner med 
     BOOT kommandoen. Der er stadig begr�nset underst�ttelse.


IPX

  For IPX, er det er n�dvendigt at muligg�re IPX netv�rk i DOSBox's Config-fil.

  Al IPX-netv�rk bliver styret gennem det interne DOSBox program IPXNET. 
  For hj�lp til IPX netv�rk i DOSBox, tast "IPXNET HELP" (uden anf�relsestegn),
  s� f�r du en liste over kommandoer og relevant dokumentation. 

  Hvad ang�r at s�tte et netv�rk op, skal den ene PC v�re server. Dette sker med 
  kommandoen : "IPXNET STARTSERVER" (uden anf�relsestegn) i en k�rende DOSBox. 
  Server DOSBox'en tilf�jer automatisk sig selv til det virtuelle IPX netv�rk.
  Du skal taste "IPXNET CONNECT <computer v�rts name eller IP>" for hver eneste 
  computer som tilf�jes det virtuelle IPX netv�rk, 
  For eksempel, hvis din server er p� bob.dosbox.com, skal du taste 
  "IPXNET CONNECT bob.dosbox.com" p� hver eneste ikke-server maskine. 
  
  At spille spil der kr�ver Netbios skal du bruge en fil som hedder NETBIOS.EXE 
  fra Novell. Opret IPX forbindelsen som forklaret ovenover og k�r s� "netbios.exe". 

  F�lgende er en IPXNET kommando reference: 

  IPXNET CONNECT 

     IPXNET CONNECT  �bner forbindelsen til en IPX kanaliseret server, som k�rer
     p� en anden DOSBox maskine. "addresse" parameteren specificerer IP adressen
     eller v�rtsnavnet p� server-PC'en. Du kan ogs� specificere hvilken UDP port
     du vil bruge. Default bruger IPXNET port 213 - den til IPX kanaliseret 
     tildelte IANA port - til sin forbindelse. 

     Syntaxen for IPXNET CONNECT er: 
     IPXNET CONNECT addresse <port> 

  IPXNET DISCONNECT 

     IPXNET DISCONNECT lukker forbindelsen til den IPX kanaliserende server. 

     Syntaxen for IPXNET DISCONNECT er: 
     IPXNET DISCONNECT 

  IPXNET STARTSERVER 

     IPXNET STARTSERVER starter en IPX kanaliserende server p� den k�rende DOSBox. 
     Standard, vil serveren acceptere forbindelser p� UDP port 213, selvom dette kan 
     �ndres. DOSBox opretter automatisk en klient-forbindelse til IPX 
     kanaliseringsserveren n�r denne er startet.

     Syntaxen for IPXNET STARTSERVER er:
     IPXNET STARTSERVER <port>

     Hvis serveren er bag en router skal UDP port <port> viderestilles til den 
     computer.

     P� Linux/Unix-based systemer kan port numre lavere end 1023 kun bruges med 
     root privilegier. Brug porte h�jere end 1023 p� disse systemer.

  IPXNET STOPSERVER

     IPXNET STOPSERVER stopper IPX kanaliserings-serveren som er k�rer p� nuv�rende
     DOSBox. Man b�r forsikre sig om at alle andre forbindelser til ogs� er af-
     sluttet, da nedlukning af serveren kan v�re skyld i lockups/frysninge p� andre 
     maskiner som stadig benytter IPX kanaliserings-serveren. 

     Syntax for IPXNET STOPSERVER er: 
     IPXNET STOPSERVER 

  IPXNET PING

     IPXNET PING rundsender en ping foresp�rgsel p� det IPX kanaliserede netv�rk.
     Til svar vil alle de tilsluttede computere rapportere tiden det tog at sende 
     og modtage ping foresp�rgslen. 

     Syntaxen for IPXNET PING er: 
     IPXNET PING

  IPXNET STATUS

     IPXNET STATUS, rapporterer status p� nuv�rende DOSBox's IPX kanaliserede 
     netv�rk. Hvis du vil have en liste over alle computere tilsluttet netv�rket,
     skal du bruge IPXNET PING kommandoen. 

     Syntaxen for IPXNET STATUS er: 
     IPXNET STATUS 


KEYB [tastaturlayoutkode [kodeside [kodesidefil]]]

  �ndrer tastatur layoutet.V�r venlig at se sektion 8 : "Tastatur Layout", hvis
  du �nsker detaljeret information om tastatur layouts.

  [tastaturlayoutkode] er en streng best�ende af fem eller f�rre bogstaver,
  nogle eksempler er : it141 itl42 (IT) (Italy) eller dk159 (DK) (Danmark). Den 
  specificerer hvilket keyboard/tastatur layout der skal bruges.
  Listen over samtlige DOSBox layouts findes her:
  http://vogons.zetafleet.com/viewtopic.php?t=21824


  [kodeside] er nummeret p� kodesiden der skal bruges. Keyboard/tastatur layoutet 
  skal give underst�ttelse for den specificerede kodeside, ellers kan layoutet ikke 
  indl�ses. Hvis der ikke er angivet nogen kodeside, bliver der automatisk valgt 
  en passende kodeside for det �nskede layout.

  [kodesidefil] kan bruges til at indl�se kodesider som endnu ikke er indbyggede i 
   DOSBox. Det bruges kun n�r DOSBox ikke kan finde kodesiden.
   Hvis der ikke er specificeret en kodesidefil, men alle ti ega.cpx filer fra 
   FreeDOS er placeret i DOSBox-program folderen, v�lges der en passende 
   kodesidefil for forespurgte layout/kodeside, automatisk.

  Eksempler:
  1) At indl�se et polsk Keyboard/tastatur layout (bruger automatisk kodeside 852):
       keyb pl214
  2) At indl�se et af de russiske Keyboard/tastatur layout med kodeside 866:
       keyb ru441 866
     For at kunne skrive russiske bogstaver tast ALT+H�JRE-SKIFT.
  3) At indl�se det franske Keyboard/tastatur layout med kodeside 850 (hvor kode-
      siden er defineret i filen EGACPI.DAT):
       keyb fr189 850 EGACPI.DAT
  4) At indl�se kodeside 858 (uden keyboard/tastatur layout):
       keyb none 858
     Dette kan bruges til at �ndre kodesiden for FreeDos's keyb2 program.
  5) For at vise nuv�rende kodeside og, hvis indl�st, tastatur layoutet
     keyb (efterfulgt af Enter/Return) 



Hvis du vil vide mere, brug /? efter program/kommandoen.



====================
5. Specielle taster:
====================

ALT-ENTER     Fuldsk�rm til/fra.
ALT-PAUSE     Pause DOSBox.
CTRL-F1       Starter keymapper.
CTRL-F4       Skifter imellem monterede disk-images. Opdaterer 
              directory-/mappe-/bibliotek-lageret for alle drev!
CTRL-ALT-F5   Starter/Stopper optagelse af film af sk�rmbillede. (avi video optagelse)
CTRL-F5       Gemmer et sk�rmbillede. (png type)
CTRL-F6       Starter/Stopper optagelse af lyd til en wave file.
CTRL-ALT-F7   Starter/Stopper optagelse af OPL kommandoer (DRO format).
CTRL-ALT-F8   Starter/Stopper optagelse af r� MIDI kommandoer.
CTRL-F7       Formindske tab af frames/rammer.
CTRL-F8       Forst�rre tab af frames/rammer.
CTRL-F9       Lukke for DOSBox.
CTRL-F10      Binde/frig�re musen.
CTRL-F11      Sl�ve emul�ringen (Neds�tte DOSBox Cycles).
CTRL-F12      S�tte mere fart p� emuleringen (�ge DOSBox Cycles).*
ALT-F12       Frig�re hastighed (turbo knap).**
F11, ALT-F11  (machine=cga) �ndre farvetonen i NTSC mode***
F11           (machine=hercules) bladre igennem farverne : ambra, gr�n, hvid***

*NOTAT: Hvis du for�ger DOSBox's cycles over din computers maximum ydeevne,
        vil det give samme effekt som at sl�ve emuleringen.
        Dette maximum vil variere fra computer til computer.

**NOTAT: Du skal have frie resourcer for dette(jo flere du har, jo hurtigere g�r
         det), s� det virker overhovedet ikke med cycles=max eller et for h�jt 
         sat "fixed cycles". Du skal holde tasterne nedtrykket, for at det 
         virker!

***NOTE: Disse taster virker ikke hvis du tidligere har gemt en mapperfil med en
         anden machine type. S� enten skal du tildele dem igen eller nulstille
         /resette mapper.

S�dan er default tastebindinger. De kan �ndres med keymapper
(se Sektion 7:  KeyMapper (Tastatur og joystick indstillinger)).

I MAC OS kan du pr�ve at bruge cmd (�bletasten) sammen med ctrl hvis tasten ikke
virker f.eks. cmd-ctrl-F1, men nogle taster skal nok stadig "mappes om"
(ogs� i Linux).

Gemte indspillede filer kan findes i:
   (Windows)    "Start/WinLogo Menu"->"All Programs"->DOSBox-0.74->Extras
   (Linux)      ~/.dosbox/capture
   (MAC OS X)   "~/Library/Preferences/capture"
dette kan �ndres i DOSBox's Config-fil. 



====================
6. Joystick/Gamepad:
====================

Dos's Standard Joystick port underst�tter et max p� 4 akser og 4 knapper.
For flere, blev der brugt forskellige �ndringer.

Du kan bruge linien "joysticktype" i [joystick] sektionen i DOSBox's config-fil,
til at �ndre type.

none  - sl�r controleren fra
auto  - (standard) finder automatisk ud af om du har een eller to controlere 
        tilsluttet.
          hvis du har een - bruges '4axis' ,
          hvis du har to - bruges '2axis'.
2axis - Hvis du har 2 controlere sat til, vil de hver is�r, emulere et joystick
        med 2 akser og 2 knapper. Hvis du kun har een controler sat til, emu-
        l�res der et joystick med med 2 akser og 2 knapper.
4axis - Underst�tter kun f�rste controler, og emul�rer et joystick med 4 akser 
        og 4 knapper, eller et gamepad med 2 akser og 6 knapper.             
4axis_2 -  Underst�tter kun anden controler.        
fcs   - Underst�tter kun f�rste controler, emul�rer ThrustMaster
        Flight Control System, med 3 akser, 4 knapper og en hat.
ch    - Underst�tter kun f�rste controler, emul�rer CH Flightstick,
        med 4-akser, 6 knapper og en hat, men du kan ikke bruge mere end een 
        knap af gangen.

Du skal ogs� konfigu�re controleren rigtigt i selve spillet.

Det er vigtigt at huske, at hvis du gemte mapperfilen uden joysticket tilsluttet,
eller med andre joystick indstillinger, virker de nye indstillinger ikke korrekt,
eller overhovedet ikke f�r du har nulstillet DOSBox's mapperfil.
  

Hvis controleren virker perfekt udenfor DOSBox, men ikke calibr�rer ordentligt i
DOSBox, kan du pr�ve forskellige 'timed' indstillinger i DOSBox's config-fil.



===============================================
7. Mapper (Tastatur og joystick indstillinger):
===============================================

N�r du starter DOSBox mapper (enten med CTRL-F1 eller med -startmapper
som kommandolinieargument) bliver du presenteret for et virtuelt 
keyboard/tastatur og et virtualt joystick.

Disse virtuelle enheder reagere p� tasterne/knapperne som DOSBox videresender til
DOS programmer. Hvis du klikker p� en tast/knap med din mus, kan du se nederst
i venstre hj�rne, hvilken funktion den er bundet til (EVENT) og hvilke funktioner
der lige nu er bundet.

Event: EVENT
BIND: BIND
                        Add   Del
mod1  hold                    Next
mod2
mod3


EVENT
    Tasten eller joystick akse/knap/hat DOSBox videresender til DOS program/spil.
    (den handling som bliver udf�rt i spillet, (f.eks skydning/hop/bev�gelse)
BIND
    Knappen p� dit fyssike keyboard/tastatur eller akse/knap/hat p� dit/dine fy-
    siske joystick(s) (som meddelt af SDL) som er bundet til EVENT(en).
mod1,2,3 
    Modfiers. Dette er taster du skal have nedtrykkede imens du taster BIND. 
    mod1 = CTRL og mod2 = ALT. Disse bliver generelt kun brugt n�r du �nsker at 
    �ndre DOSBox's specielle taster.
Add 
    Tilf�jer en ny BIND til denne EVENT. Tilf�jer grundl�ggende en tast fra dit 
    keyboard/tastatur eller en funktion joysticket (trykket knap, akse/hat bev�-
    gelse) dette skaber en EVENT(handling) i DOSBox.
Del 
    Sletter denne  EVENT's BIND. Hvis en EVENT ingen BINDS har, er det ikke muligt 
    at udl�se den i DOSBox (man kan ikke udl�se tasten eller joystick-funktionen).
Next
    Gennemg� listen over bindinger som leder til denne EVENT.


Eksempel:
Q1. Du �nsker at X'et p� dit keyboard/tastatur skriver Z i DOSBox.
    A. Klik p� Z'et i keyboard mapper. klik "Add". 
       tryk nu x tasten p� dit keyboard/tastatur. 

Q2. Hvis du klikker "Next" et par gange, vil du bem�rke, at Z'et p� dit 
    keyboard/tastatur ogs� laver et Z i DOSBox.
    A. Derfor skal du v�lge Z igen, og v�lge "Next" til du har Z p� dit
    tastatur. V�lg nu "Del".

Q3. Hvis du pr�ver det i DOSBox, vil du bem�rke at n�r du taster X kommer ZX
    frem.
     A. X'et p� dit keyboard/tastatur er ogs� stadig kortlagt til X! Klik p�
        X'et i keyboard mapper og s�g med "Next" til du finder den kortlagte
        X tast. Klik "Del".


Eksempler p� at omprogramere joysticket:
  Du har et joystick tilsluttet, det virker fint i DOSBox og du �nsker at spille
  et kun-for-keyboard/tastatur spil med joysticket (det formodes at spillet
  kontrolleres med piletasterne p� keyboardet/tastaturet):
    1) Start mapper, klik s� p� en af pilene i midten af venstre side af sk�rmen
       (lige over Mod1/Mod2 knapperne).
       EVENT skal v�re key_left. Klik nu p� Add og flyt dit joystick i samme ret-
       ning(som pilen peger), dette skulle tilf�je en handling til BIND.
    2) Gentag ovenst�ende for de sidste 3 retninger, i tilf�jelse kan knapperne
       p� joysticket ogs� omprogrameres (fire/jump).
    3) Klik p� Save, s� p� Exit og test det med et spil.

  Hvis du �nsker at �ndre y-aksen p� joysticket fordi nogle flysimulatorer bruger
  joystickens op/ned  bev�gelse p� en m�de du ikke kan lide, og det ikke kan ind-
  stilles i selve spillet:
    1) Start mapper og klik p� Y- i det �vre joystick felt
       EVENT skulle v�re jaxis_0_1-.
    2) Klik p� Del for at fjerne nuv�rende binding, klik s� p� Add og flyt dit
       joystick nedad. der skulle nu v�re  skabt et nyt bind.
    3) Gentag dette for Y+, gem layoutet, og test det til slut i et spil.

  Hvis du �nsker at omprogramere noget med din d-pad/hat er du n�dt til �ndre
  'joystick=auto' til 'joystick=fcs' i config-filen. Dette bliver m�sk� for-
  bedret i n�ste DOSBox version.



Hvis du �ndrer standard mapping, kan du gemme dine �ndringer ved at klikke p�
"Save". DOSBox gemmer din mapping til en lokalitet specificeret i config-filen
(mapperfile= linien). DOSBox indl�ser din mapper-fil, hvis den er tilstede i
config-filen.



===================
8. Tastatur Layout:
===================

For at skifte til et andet keyboard/tastatur layout, kan bruges enten punktet
"keyboardlayout" i [dos]-sektionen i dosbox.conf, eller det interne DOSBox
program keyb.com. Begge dele accepterer dos-afpassede sprog koder (se nedenunder), 
men du kan kun indl�se en tilpasset sprogkode-fil med keyb.com.

Standard keyboardlayout=auto, som lige nu kun virker under Windows, layoutet
bliver valgt i forhold til OS'ets layout, men tastatur layoutet bliver ikke genkendt.

Skiftning af Layout
  DOSBox underst�tter som standard et vist antal keyboard/tastatur layouts  og kode-
  sider,i disse tilf�lde er det kun n�dvendigt at specificere layoutkoden (som f.eks
  tastaturlayout=dk159 i DOSBox's config-fil, eller "keyb dk159" ved DOSBox's komman-
  doprompt). Listen over alle DOSBox's indbyggede layouts kan findes 
  her: http://vogons.zetafleet.com/viewtopic.php?t=21824
  
  Nogle keyboard/tastatur layouts (f.eks layout GK319 kodeside 869 og layout RU441
  kodeside 808) har underst�ttelse for dobbelt-layouts, som kan aktiveres med
  tasterne VENSTRE-ALT+H�JRE-SKIFT for et layout og VENSTRE-ALT+VENSTRE-SKIFT for 
  det andet.
  Nogle tastatur layouts (for eksempel LT456 kodeside 771) har underst�ttelse for
  tre layouts, det tredje kan aktiveres med VENSTRE-ALT+VENSTRE-CTRL.

Underst�ttede eksterne filer
  FreeDos's .kl filer er underst�ttet (FreeDos keyb2 tastatur layoutfiler) 
  ligesom FreeDos's keyboard.sys/keybrd2.sys/keybrd3.sys biblioteker som 
  best�r af alle tilg�ngelige .kl filer.
  Se p� http://www.freedos.org/ for pr�kompilerede tastatur/keyboard layouts
  hvis de DOSBox-integrerede layouts, af en eller anden grund ikke virker, eller 
  efter opdaterede/nye tilg�ngelige layouts. 

  B�de .CPI (MSDOS/kompatible kodeside filer) og .CPX (FreeDos UPX-komprimerede
  kodeside filer) kan bruges. Nogle kodesider er indbygget i DOSBox s� det for 
  det meste ikke er n�dvendigt at t�nke p� kodeside filer. Hvis du har brug for 
  en anden (eller en specielt tilpasset) kodeside fil, kan du kopiere den ind i
  Directoriet/mappen/biblioteket hvor DOSBox config-fil er s� DOSBox kan finde den.
  Hvis der ikke er specificeret en kodesidefil, men alle ti ega.cpx filer fra 
  FreeDOS er placeret i DOSBox-program folderen, v�lges der en passende 
  kodesidefil for forespurgte layout/kodeside

  Yderligere layouts kan tilf�jes ved at kopiere de tilsvarende .kl-filer til
  dosbox.conf's directory/mappe/bibliotek og bruge f�rste del af fil-navnet som
  sprog-kode.
  Eksempel: For filen UZ.KL (keyboard/tastatur layout for Uzbekistan) specificeres
           "keyboardlayout=uz" i DOSBox's config-fil.
  Integreringen af keyboard layout pakker (som keybrd2.sys) virker p� samme m�de.


Bem�rk at keyboard/tastatur layoutet tillader udenlandske karakt�rer at 
blive skrevet, men der er ikke underst�ttelse for dem i filnavne. Pr�v at undg� 
dem(tegnene) b�de i DOSBox og det v�rts operativ system som er tilg�ngeligt
fra DOSBox.



==============================
9. Serial Multiplayer feature:
==============================
 
DOSBox kan emulere et serielt nullmodem kabel over netv�rk og internet.
Dette kan konfigureres i [serialports] sektionen i DOSBox's Config-fil.

For at oprette en nullmodem forbindelse, skal �n v�re server og �n klient.

Serveren skal s�ttes s�dan op i DOSBox's config-fil:
   serial1=nullmodem

Klient:
   serial1=nullmodem server:<IP eller navn p� serveren>

Start nu spillet og v�lg nullmodem / serial cable / already connected
som multiplayer m�de p� COM1. Set same baudrate p� begge computere.

Desuden, kan der tilf�jes yderligere parametreametre for at kontrollere opf�r-
slen af nullmodem forbindelsen. Dette er alle parametrene:

 * port:         - TCP port nummer. Default: 23
 * rxdelay:      - hvor l�nge (millisekunder) de modtagne data skal forsinkes hvis
                   enheden ikke er klar. For�g denne v�rdi hvis du oplever
                   overrun errors i DOSBox's Status vindue. Standard: 100
 * txdelay:      - hvor l�nge der skal samles data f�r der sendes en pakke. 
                   Standard: 12 (reducerer Netv�rk overhovede)
 * server:       - Dette nullmodem vil v�re en klient som tilslutter til den spe-
                   cificerede server. (ingen server argument: V�r en server.)
 * transparent:1 - Sender kun de serielle data, ingen RTS/DTR handshake. Bruges
                   n�r der tilsluttes til alt andet end et nullmodem.
 * telnet:1      - Overs�tter Telnet data fra et andet sted(tilsluttet). S�tter
                   automatisk transparent.
 * usedtr:1      - Forbindelsen bliver ikke lavet f�r DTR bliver sl�et til af
                   DOS programmet. Bruges med modem terminaler.
                   S�tter automatisk transparent.
 * inhsocket:1   - Brug en socket sendt til DOSBox ad kommandolinien. S�tter
                   automatisk transparent. (Socket Inheritance: Det bruges til at 
                   spille gamle DOS door games p� ny BBS software.)

Eksempel: V�r en server der lytter p� TCP port 5000.
   serial1=nullmodem server:<IP eller navn p� serveren> port:5000 rxdelay:1000



===========================================
10.Hvordan du �ndrer hastigheden p� DOSBox: 
===========================================

DOSBox emulerer CPUen, lyd- og grafik- kort , og andre dele af PCen, det hele
p� samme tid. Hastigheden p� den emulerede DOS applikation afh�nger af hvor
mange instruktioner der kan emuleres, kan justeres(antal cycles).

CPU Cycles
  Standard pr�ver DOSBox (cycles=auto) at detektere om et spil har brug for, at 
  blive k�rt med s� mange instruktioner emuleret per tids-interval som muligt 
  (cycles=max, f�r til tider et spil til at k�re for hurtigt eller ustabilt),
  eller om der skal bruges et fiks�ret antal cycles(cycles=3000 , f�r til tider 
  spillet til at arbejde for langsomt eller for hurtigt). Men du kan altid, 
  manuelt, indf�re en anden indstilliong i DOSBox's config-fil.

  Man kan tvinge langsom eller hurtig opf�rsel igennem ved at s�tte et fiks�ret antal
  cycles i DOSBox's config-fil. Hvis du f.eks. s�tter cycles=10000 viser DOSBox 
  �verst en linie "Cpu Speed: fixed 10000 cycles" . I dette modus kan du reducere
  antal cycles endnu mere med tasterne CTRL-F11(s� lavt som du �nsker), eller h�ve 
  antal cycles med tasterne CTRL-F12, s� meget som du �nsker(dog begr�nset af een 
  kerne's styrke i din computers CPU). Du kan se hvor meget fritid din rigtige CPU's 
  kerner har i Taskmanager i Windows 2000/XP/VISTA/ og System Monitor i Windows 
  95/98/ME. N�r du har brugt 100% af din rigtige CPU's ene kerne's styrke, er der ikke
  videre mulighed for at h�ve hastigheden p� DOSBox (DOSBox begynder faktisk at ar-
  bejde langsommere), undtagen hvis du mindsker belastningen p� ikke-cpu delene af 
  DOSBox. DOSBox kan kun bruge een CPU-kerne, s� hvis du har en CPU med f.eks. 4 
  kerner, kan DOSBox ikke bruge de andre 3 kerner.
 
  Man kan tvinge hurtig opf�rsel igennem ved at s�tte cycles=max i DOSBox's config-
  fil. DOSBox's vindue viser i s� fald linien "Cpu Speed: max 100% cycles", �verst. 
  I denne tilstand beh�ver du ikke bekymre dig over hvor meget fritid din rigtige 
  CPU har, for DOSBox vil altid bruge 100% af din rigtige CPU's ene kerne. I dette
  modus kan du aflaste dig rigtige CPU med tasterne CTRL-F11, eller �ge belastningen
  igen med CTRL-F12.

CPU Kerner(Cores)
  P� x86 arkitekturer kan du pr�ve at tvinge brugen af "dynamisk genindsamlings 
  kerne" (s�t core=dynamic i DOSBox's config-fil).
  Dette giver normalt bedre resultater, hvis auto genkendeklsen (core=auto) fejler.
  Indstillingen fungerer bedst sammen med cycles=max. Men du kan ogd� pr�ve sammen 
  med et h�jt antal cycles (f.eks. 20000 eller mere).Der kan dog v�re spil som 
  virker d�rligere med "dynamisk genindsamlings kerne" indstillingen (g�m dit 
  spil ofte), eller slet ikke!.

Grafik emulering (h�ve hastigheden)
  VGA emulering er en meget kr�vende del af DOSBox's reelle CPU forbrug. Du kan 
  forst�rre tabet af antal rammer/frames der skippes (for�ges med antallet et) ved
  at nedtrykke tasterne CTRL-F8. Dit CPU forbrug skulle formindskes n�r du bruger
  en fast "cycles" indstilling, og du kan h�ve antallet af cycles med CTRL-F12.
  Dette kan du g�re til spillet k�rer hurtigt nok.
  L�g dog m�rke til at dette er et kompromis : du mister tilsvarende kvalitet i 
  billede som du vinder hastighed.

Lyd emulering (h�ve hastigheden)
  Du kan ogs� pr�ve at sl� lyden fra i spillets setup program for at reducere
  CPU forbruget yderligere. indstillingen nosound=true i DOSBox's config-fil sl�r
  IKKE emuleringen af lydenheder fra, det er kun lyd-outputet der bliver sl�et fra.

Pr�v ogs� at lukke alle andre programmer for at reservere s� mange resourcer som
muligt til DOSBox.


Avanceret cycles indstillinger:
Cycles=auto og cycles=max indstillingerne kan s�ttes med andre parametre 
for forskellige start standarder. Syntaksen er
  cycles=auto ["realmode default"] ["protected mode default"%] 
              [limit "cycles begr�nsning"]
  cycles=max ["protected mode default"%] [limit "cycles begr�nsning"]
Eksempel:
  cycles=auto 1000 80% limit 20000
  bruger cycles=1000 for real mode spil, 80% cpu effekt for 
  protected mode spil sammen med en h�rd cycle begr�nsning p� 20000



====================
11. Probleml�sning:
====================

Generel tip:
  Tjek meddelelser i DOSBox's Statusvindue. Se sektion 12 "DOSBox's statusvindue"  


DOSBox d�r lige efter start:
  - brug andre v�rdier i output= indstillingen i din DOSBox
    config-fil
  - pr�v at opdatere grafikkort-driver og DirectX
  - (Linux) s�t milj�variablen SDL_AUDIODRIVER til alsa eller oss.

N�r du k�rer et bestemt spil lukker DOSBox, med en/flere besked(er) eller h�nger:
  - se om det virker med Standard DOSBox installation
    (u�ndret config-fil)
  - pr�v uden lyd (brug det lydindstillingsprogram som er med spillet, endvidere
    kan du pr�ve sbtype=none og gus=false)
  - lav om p� nogle af indstillingerne i DOSBox's config-fil, pr�v specielt :
      core=normal
      faste cycles (for eksempel cycles=10000)
      ems=false
      xms=false
    eller en kombination af ovenst�ende
    machine indstilling der har samme chipset og funktion
    funktionsm�ssigt:
      machine=vesa_nolfb
    eller
      machine=vgaonly
  - brug loadfix f�r du starter spillet 

Spillet g�r tilbage til DOSBox's kommandoprompt med fejlmeddelelse:
  - l�s fejlmeddelelsen koncentreret og pr�v at lokalisere fejlen
  - pr�v tipsene i ovenn�vnte sektioner
  - monter anderledes da nogle spil er fintf�lende med lokaliteterne,
    pr�v for eksempel hvis du har monteret d d:\Gamlespil\spil"
    "mount c d:\Gamlespil\spil" istedet "mount c d:\Gamlespil"
  - hvis spillet kr�ver cdrom, v�r sikker p� at du skrev "-t cdrom" da du
    monterede og pr�v forskellige andre yderligere parametre (ioctl, usecd og label
    switchene, se den rette sektion)
  - Tjek filerne til spillet's tilladelser (fjern read-only attributter,
    tilf�j skrivetilladelser og lignende.)
  - pr�v at geninstallere spillet i selve DOSBox



=========================
12. DOSBox Status Window:
=========================

DOSBox's Statusvindue indeholder meget nyttig information om dine nuv�rende ind-
stillinger, hvad du g�r i DOSBox, fejl der opst�r og meget mere. 
Tjek disse meddelelser, n�r du oplever fejl.

Hvordan du starter DOSBox's Statusvindue:
  (Windows)  Statusvinduet starter sammen med Hoved-DOSBox-vinduet.
  (Linux)    Det kan v�re n�dvendigt at starte DOSBox fra Konsollen, for at f�
             et Statusvindue.
  (MAC OS X) H�jreklik p� DOSBox.app, v�lg "Show Package Contents" ->
             ->enter "Contents"->enter "MACOS"->run "DOSBox"



=====================================
13. Config-filen (indstillingsfilen):
=====================================

config-filen genereres automatisk f�rste gang du starter DOSBox.
Filen kan findes i: (engelsk, den danske skal (som standard) v�re i DOSBox's 0.74 
mappen, i de fleste tilf�lde "c:\programmer\DOSBox-0.74", lav selv en genvej til
dosbox.conf i startmenuen)
   (Windows)  "Start/WinLogo Menu"->"All Programs"->DOSBox-0.74->Options
   (Linux)    ~/.dosbox/dosbox-0.74.conf
   (MAC OS X) "~/Library/Preferences/DOSBox 0.74 Preferences"
Filen er indelt i adskillige sektioner. Hver sektion starter med en
[sektion navn] linie. Indstillingerne er beskrivelse=v�rdi linier hvor v�rdi kan 
�ndres for tilpasse DOSBox.
# og % viser komentarlinier


Der kan genereres en config-fil med CONFIG.COM, som kan findes p� det interne
DOSBox Z: drev hvor du starter DOSBox. Se i sektione 4 :"interne programmer"
af denne readme hvordan du bruger CONFIG.COM. Du kan tilpasse den genererede 
config-fil til dit DOSBox behov. Du kan starte DOSBox med -conf "config-fil"
switchen og indl�se den gener�rede fil og dens indstillinger

DOSBox bruger config-filer der er angivet med -conf. Hvis der ikke er
angivet en fil, s�ges efter "dosbox.conf" i det lokale directory/mappe/bibliotek.
Hvis der ingen er, vil DOSBox hente brugerens config-fil. 
Denne fil bliver skabt, hvis den ikke allerede eksisterer



================
14. Sprog-filen:
================


Der kan genereres en Sprog-fil med CONFIG.COM , som kan findes p� det interne Z: 
drev, n�r du starter DOSBox. Se i Sektion 4:"Interne programmer", hvordan man bruger 
config.com 
L�s den, s� forst�r du forh�bentligt hvordan man �ndrer den. 
Start med DOSBox -lang "sprog-fil" switchen og indl�s din sprog-fil.
Du kan alternativt indf�re filenavnet i config-filen i [dosbox] Sektionen. 
Der er en language= indstilling der kan �ndres med et filnavn.



=================================================
15. Hvordan du bygger din egen version af DOSBox:
=================================================


Hent/Download kildefilerne (source).
L�s INSTALL i  kilde-distributionen.



===================
14. Special thanks:
===================


Se THANKS filen.



============
15. Kontakt:
============

See the site: 
http://www.dosbox.com
for an email address (The Crew-page).
(email adresse p� : http://www.dosbox.com  The Crew-siden)



