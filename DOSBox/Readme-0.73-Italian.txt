DOSBox v0.73


=====
NOTA: 
=====

La nostra speranza � che un giorno DOSBox possa fare girare tutti i
programmi mai fatti per PC, ma ancora non siamo a quel punto. Attualmente
DOSBox in esecuzione su un computer potente � pi� o meno l'equivalente
di un PC 486. DOSBox pu� essere configurato in modo da far girare
un certo numero di giochi DOS, dai classici in CGA/Tandy/PCjr fino
ai giochi dell'era di Quake.



=======
INDICE:
=======
1. Iniziare subito
2. FAQ
3. Uso
4. Programmi Interni
5. Tasti Speciali
6. Mapper
7. Layout della Tastiera
8. Funzione Multiplayer Seriale
9. Come giocare a giochi particolarmente esigenti
10. Risoluzione dei problemi
11. Il file di configurazione
12. Il file linguaggio
13. Costruire la tua versione di DOSBox
14. Ringraziamenti speciali
15. Contatti



===================
1. Iniziare subito:
===================

Digita INTRO in DOSBox per una rapida occhiata alle opzioni.
� importantissimo che impari velocemente concetti come "montare drive",
DOSBox non crea automaticamente nessun drive (o sue parti) accessibili
dall'interno dell'emulazione.
Per maggiori informazioni vedi la FAQ "Ho una Z invece che una C al prompt"
e anche la descrizione del comando MOUNT (sezione 4).



=======
2. FAQ:
=======

Alcune domande poste frequentemente (FAQ):

D: Ho una Z invece che una C al prompt.
D: Devo sempre digitare questi comandi? Nessuna automazione?
D: Come passo a schermo intero ?
D: Il mio CD-ROM non funziona.
D: Il gioco/applicazione non riesce a trovare il suo CD-ROM.
D: Il mouse non funziona.
D: Non c'� il suono.
D: Il suono � a singhiozzo, rallentato o comunque strano.
D: Non posso digitare \ o : in DOSBox.
D: L'input da tastiera soffre di rallentamenti.
D: Il cursore si muove sempre nella stessa direzione!
D: Il gioco/applicazione gira troppo lentamente!
D: Il gioco/applicazione non gira per niente, o va in crash!
D: DOSBox pu� danneggiare il mio computer?
D: Vorrei cambiare la dimensione della memoria/velocit� cpu/ems/IRQ soundblaster.
D: Attualmente, quali dispositivi sonori sono emulati da DOSBox?
D: DOSBox crasha all'avvio e sto eseguendo arts.
D: Il mio gioco Build (Duke3D/Blood/Shadow Warrior) ha problemi.
D: Ottimo README, ma ancora non capisco.




D: Ho una Z invece che una C al prompt.
R: Devi fare in modo che le tue directory diventino disponibili sottoforma di
   drive in DOSBox usando il comando "mount". Per esempio, sotto Windows, il
   comando "mount C D:\GAMES" creer� un drive C in DOSBox, che punta alla tua
   directory reale D:\GAMES. Sotto Linux, "mount c /home/nomeutente" creer�
   un drive C in DOSBox, che punta alla directory /home/nomeutente di Linux.
   Per spostarti nel drive appena montato digita "C:". Se tutto � andato bene,
   DOSBox mostrer� il prompt "C:\>".


D: Devo sempre digitare questi comandi? Nessuna automazione?
R: Nel file di configurazione di DOSBox c'� una sezione chiamata [autoexec].
   I comandi presenti in questa sezione vengono eseguiti ad ogni avvio di
   DOSBox, quindi puoi usarla per montare i drive.


D: Come passo a schermo intero ?
R: Premi alt-invio. In alternativa: Modifica il file di configurazione di
   DOSBox e cambia l'opzione fullscreen=false in fullscreen=true. Se la
   modalit� a schermo intero non ti va bene, gioca con l'opzione fullresolution
   nel file di configurazione di DOSBox. Per tornare indietro dalla modalit�
   schermo intero: Premi alt-invio di nuovo.


D: Il mio CD-ROM non funziona.
R: Per montare il tuo CD-ROM in DOSBox devi specificare qualche opzione addizionale
   all'atto del montaggio.
   Per abilitare il supporto CD-ROM (include MSCDEX):
     - mount d f:\ -t cdrom
   Per abilitare il supporto CD-ROM di basso livello (usa ioctl se possibile):
     - mount d f:\ -t cdrom -usecd 0
   Per abilitare il supporto SDL di basso livello:
     - mount d f:\ -t cdrom -usecd 0 -noioctl
   Per abilitare il supporto aspi di basso livello (win98 con l'aspi-layer installato):
     - mount d f:\ -t cdrom -usecd 0 -aspi
   
   Nei comandi: - d   lettera di drive che avrai nel DOSBox
                - f:\ percorso del CD-ROM nel tuo PC.
                - 0   Il numero del drive CD-ROM, ottenuto tramite mount -cd
                      (nota che questo valore � necessario solo quando si usa SDL per i
                       CD audio, altrimenti viene ignorato)
   Vedi anche la domanda: Il gioco/applicazione non riesce a trovare il suo CD-ROM.


D: Il gioco/applicazione non riesce a trovare il suo CD-ROM.
R: Assicurati di montare il CD-ROM col parametro -t cdrom, ci� abiliter�
   l'interfaccia MSCDEX richiesta dai giochi DOS per interfacciarsi con i
   CD-ROM. Prova anche ad aggiungere la giusta etichetta (-label ETICHETTA)
   al comando mount, dove ETICHETTA � l'etichetta CD (volume ID) del CD-ROM.
   Sotto Windows puoi specificare -ioctl, -aspi o -noioctl. Leggi la descrizione
   del comando mount nella Sezione 4 per capirne il significato e per vedere
   le altre opzioni legate ai CD audio -ioctl_dx, -ioctl_mci, -ioctl_dio.

   Prova a creare una immagine CD-ROM (preferibilmente di tipo CUE/BIN) e usa
   lo strumento interno di DOSBox IMGMOUNT per montarla (il file CUE).
   Questo permette un supporto di basso livello del CD molto buono su qualsiasi
   sistema operativo.


D: Il mouse non funziona.
R: Solitamente, DOSBox capisce quando un gioco usa il controllo via mouse.
   Quando clicchi sullo schermo dovrebe essere catturato (cio� confinato alla
   finestra di DOSBox) e funzionare. Con certi giochi, la rilevazione del mouse
   da parte di DOSBox non funziona. In questo caso dovrai catturare il mouse
   manualmente premendo CTRL-F10.


D: Non c'� il suono.
R: Assicurati che il suono sia correttamente configurato nel gioco. Ci� pu�
   di solito essere fatto durante l'installazione o con un setup/setsound
   allegato al gioco. Prima controlla che sia possibile fare l'autorilevazione.
   Se non � disponibile prova a scegliere la soundblaster o soundblaster16
   con le impostazioni di default "address=220 irq=7 dma=1". Potresti anche
   dover impostare la musica midi all'indirizzo 330 come dispositivo.
   Questi parametri delle schede audio emulate possono essere cambiati nel
   file di configurazione di DOSBox.
   Se ancora non senti niente imposta il core su normal e usa valori pi� bassi
   per cycles (come cycles=2000). Assicurati inoltre che la tua scheda audio
   reale funzioni correttamente.
   In certi casi potrebbe essere utile usare una scheda audio emulata differente
   come una soundblaster pro (sbtype=sbpro1 nel file di configurazione DOSBox) o
   la gravis ultrasound (gus=true).


D: Il suono � a singhiozzo, rallentato o comunque strano.
R: Stai sfruttando troppa potenza CPU per mantenere DOSBox a quella velocit�.
   Puoi abbassare i cicli, saltare dei fotogrammi, ridurre la frequenza di campionamento
   del dispositivo audio (vedi il file di configurazione di DOSBox) o del dispositivo
   mixer. Puoi anche aumentare il prebuffer nel file di configurazione.
   Se stai usando cycles=max o =auto, assicurati che non ci siano processi
   in sottofondo che interferiscano! (specialmente se accedono al disco rigido)


D: Non posso digitare \ o : in DOSBox.
A: Pu� capitare in vari casi, come se la il layout della tua tastiera non ha una
   corrispondente rappresentazione DOS (o non � stata correttamente rilevata),
   o le assegnazioni dei tasti sono errate.
   Alcune possibili soluzioni:
     1. Usa piuttosto / , o ALT-58 per : e ALT-92 per \.
     2. Cambia il layout tastiera DOS (vedi la Sezione 7: Layout Tastiera).
     3. Aggiungi i comandi che vuoi eseguire alla sezione [autoexec] del file
        di configurazione DOSBox.
     4. Apri il file di configurazione e cambia la voce usescancodes.
     5. Cambia il layout tastiera del tuo sistema operativo.
   
   Nota che se � impossibile identificare il layout del tuo sistema, o keyboardlayout
   � impostato a none nel file di configurazione DOSBox, viene usato il layout standard
   americano (US). In questa configurazione, prova i tasti vicino a "invio" per il
   tasto \ (backslash), e per il tasto : (due punti) usa maiusc e i tasti tra "invio"
   e "l".


D: L'input da tastiera soffre di rallentamenti.
R: Abbassa il livello di priorit� nel file di configurazione di DOSBox
   come ad esempio "priority=normal,normal". Puoi anche provare
   a diminuire i cicli.
   (usa un numero fisso di cicli da cui partire, come cycles=10000).


D: Il cursore si muove sempre nella stessa direzione!
R: Vedi se succede ancora quando disattivi l'emulazione joystick,
   imposta joysticktype=none nella sezione [joystick] del tuo file
   di configurazione di DOSBox. Puoi anche provare a scollegare ogni
   joystick. Se vuoi usare il joystick nei giochi, prova a impostare
   timed=false e assicurati di calibrare il joystick (sia nel tuo
   SO come anche nel gioco, o nel setup del gioco).


D: Il gioco/applicazione gira troppo lentamente!
R: Guarda nella sezione "Come avviare giochi pesanti" per maggiori
   informazioni.


D: Il gioco/applicazione non gira per niente, o va in crash!
A: Guarda la Sezione 10: Risoluzione dei problemi


D: DOSBox pu� danneggiare il mio computer?
R: Non pi� di qualsiasi altro programma che richieda molte risorse. L'incremento
   dei cicli non � un overclock della tua CPU reale. Impostare un valore troppo
   alto ha un effetto negativo sulle prestazioni del software che gira all'interno
   di DOSBox.


D: Vorrei cambiare la dimensione della memoria/velocit� cpu/ems/IRQ soundblaster.
R: Puoi farlo! Basta che crei un file di configurazione: config -writeconf nomefile.
   Apri il tuo editor preferito e guarda le impostazioni. Per avviare DOSBox con
   i tuoi nuovi settaggi: dosbox -conf nomefile
   Guarda la descrizione del comando config nella Sezione 4 per ulteriori dettagli.


D: Attualmente, quali dispositivi sonori DOSBox emula?
R: DOSBox emula diversi dispositivi sonori:
   - Altoparlante interno PC
     Questa emulazione include sia il generatore di note che diverse forme
     di output audio digitale attraverso l'altoparlante interno.
   - Creative CMS/Gameblaster
     E' la prima scheda rilasciata da Creative Labs(R).  La configurazione
     di default la piazza nella porta 0x220.  Andrebbe notato che abilitarla
     assieme all'emulazione Adlib potrebbe portare a conflitti.
   - Tandy 3 voice
     L'emulazione di questo hardware audio � completa ad eccezione del
     noise channel. Il noise channel non � ben documentato e di conseguenza
     vi si pu� andare solo per immaginazione, cercando l'accuratezza sonora.
   - Tandy DAC
     L'emulazione della Tandy DAC usa quella della soundblaster, quindi
     assicurati che l'emulazione soundblaster non sia disattivata nel file
     di configurazione di DOSBox. La Tandy DAC � emulata soltanto a livello
     di BIOS.
   - Adlib
     This emulation is almost perfect and includes the Adlib's ability to 
     almost play digitized sound.
   - SoundBlaster 16/ SoundBlaster Pro I & II /SoundBlaster I & II
     Per default DOSBox fornisce suono a 16-bit Soundblaster 16.
     Puoi selezionare una versione diversa di SoundBlaster nel file di
     configurazione di DOSBox (Vedi Comandi Interni: CONFIG).
   - Disney Soundsource
     Usando la porta stampante, questo dispositivo sonoro produce soltanto
     audio digitale.
   - Gravis Ultrasound
     L'emulazione di questo hardware � quasi completa, anche se le funzioni
     MIDI sono state lasciate fuori, dato che � gi� stato emulato MPU-401
     in altro codice.
   - MPU-401
     Una interfaccia MIDI � anch'essa emulata.  Questo metodo di output
     sonoro funzioner� soltanto se usato con un dispositivo General Midi o
     MT-32.


D: DOSBox crasha all'avvio e sto eseguendo arts.
R: Non � un problema di DOSBox, comunque la soluzione � di impostare
   la variabile d'ambiente SDL_AUDIODRIVER su alsa o oss.


D: Il mio gioco Build (Duke3D/Blood/Shadow Warrior) ha problemi.
A: Prima di tutto, prova a trovare un port del gioco. Con quelli ti troverai
   certamente meglio. Per sistemare i problemi grafici che avvengono in
   DOSBox alle risoluzioni pi� alte, apri il file di configurazione DOSBox
   e cerca machine=svga_s3. Cambia svga_s3 in vesa_nolfb


D: Ottimo README, ma ancora non capisco.
R: Potrebbe aiutarti uno sguardo a "The Newbie's pictorial guide
   to DOSBox" che si trova qui
   http://vogons.zetafleet.com/viewforum.php?f=39
   Prova anche il wiki di DOSBox:
   http://www.dosbox.com/wiki/
   (documenti in inglese)


Per altre domande leggi il resto di questo README e/o controlla il
sito/forum:
http://www.dosbox.com



=======
3. Uso:
=======

Una panoramica sui parametri di linea di comando da passare a DOSBox.
Gli utenti di Windows devono aprire cmd.exe o command.com o modificare
il collegamento a DOSBox.exe per poterli usare.
Le opzioni sono valide per tutti i sistemi operativi tranne quando
espressamente specificato nelle descrizioni:

dosbox [nome] [-exit] [-c comando] [-fullscreen] [-conf fileconfig] 
       [-lang filelinguaggio] [-machine tipomacchina] [-noconsole]
       [-startmapper] [-noautoexec] [-securemode] 
       [-scaler scaler | -forcescaler scaler]
       [-version]
       
dosbox -version
dosbox -editconf programma
dosbox -opencaptures programma
dosbox -printconf
dosbox -eraseconf

  nome
        Se "nome" � una directory verr� montata come drive C:.
        Se "nome" � un eseguibile, verr� montata la directory in cui "nome" si trova
        come drive C: e verr� eseguito "nome".
    
  -exit  
        DOSBox si chiuder� quando l'applicazione DOS "nome" sar� terminata.

  -c comando
        Esegue il comando specificato prima di avviare "nome". Possono essere
        specificati comandi multipli. Ogni comando dovrebbe partire con "-c".
        Un comando pu� essere: un Programma Interno, un comando DOS o un
        eseguibile su un drive montato.

  -fullscreen
        Avvia DOSBox in modalit� a schermo intero.

  -conf fileconfig
        Avvia DOSBox con le impostazioni speficicate in "fileconfig".
        Possono essere specificate diverse opzioni -conf.
        Vedi la Sezione 11 per maggiori dettagli.

  -lang filelinguaggio
        Avvia DOSBox usando la lingua specificata in "filelinguaggio".

  -machine tipomacchina
        Imposta DOSBox per emulare un tipo specifico di macchina. Scelte valide
        sono: hercules, cga, pcjr, tandy, svga_s3 (default) oltre agli altri
        chipset svga elencati nella guida del file di configurazione DOSBox.
        svga_s3 abilita anche l'emulazione vesa.
        Per alcuni effetti speciali vga, pu� essere usato solo il tipomacchina
        vgaonly, nota che ci� disattiva le funzionalit� svga e potrebbe
        essere (considerevolmente) pi� lento a causa della maggiore precisione
        di emulazione richiesta.
        Il tipo di macchina influenza sia la scheda video che le schede
        audio disponibili.

  -noconsole (Solo Windows)
        Avvia DOSBox senza mostrare la finestra console. L'output sar�
        ridirezionato verso stdout.txt e stderr.txt
	
  -startmapper
        Avvia il keymapper immediatamente. Utile per gli utenti con
        problemi di tastiera.

  -noautoexec
        Salta la sezione [autoexec] del file di configurazione caricato.

  -securemode
        Uguale a -noautoexec, ma aggiunge config.com -securemode alla fine
        di AUTOEXEC.BAT (che, a sua volta, disabilita qualsiasi cambiamento
        su come i drive vengono montati dentro DOSBox).

  -scaler scaler
        Usa lo scaler specificato da "scaler". Vedi il file di configurazione DOSBox
        per conoscere che scaler sono disponibili.

  -forcescaler scaler
        Simile al parametro -scaler, ma prova a forzare l'uso dello scaler
        specificato anche qualora non fosse adatto.

  -version
        mostra le informazioni di versione ed esce. Utile per i frontend.

  -editconf programma
        avvia "programma" e gli passa come parametro il file di configurazione.
        Puoi specificare questo comando pi� volte. In questo caso, avvier�
        il secondo programma se il primo dovesse non avviarsi.

  -opencaptures programma
        avvia "programma" e gli passa come parametro la cartella degli
        screenshot.
  
  -printconf
        stampa la posizione del file di configurazione di default.

  -eraseconf
        rimuove il file di configurazione.

Nota: Se un nome/comando/fileconfigurazione/filelinguaggio contiene uno
      spazio, metti l'intero nome/comando/fileconfigurazione/filelinguaggio
      tra doppi apici ("comando o nome di file"). Se hai bisogno, ecco come
      usare doppi apici all'interno di altri doppi apici (succede spesso
      con -c e mount):
      Gli utenti Windows e OS/2 possono usare apici singoli all'interno di
      doppi apici. Gli altri dovrebbero essere in grado di usare doppi apici
      preceduti dal carattere di escape, all'interno di altri doppi apici.
      Windows: -c "mount c 'c:\miei programmi\'"
      Linux: -c "mount c \"/tmp/nome con spazio\""

Per esempio (Windows):

dosbox c:\atlantis\atlantis.exe -c "MOUNT D C:\SAVES"
  Questo monta c:\atlantis come c:\ ed esegue atlantis.exe.
  Prima di fare questo, monta C:\SAVES come drive D.

Sotto Windows, puoi anche trascinare directory/file sull'eseguibile di DOSBox.



=====================
4. Programmi Interni:
=====================

DOSBox supporta la maggior parte dei comandi DOS trovati in command.com.
Per avere una lista dei comandi interni digita "HELP" al prompt.

Inoltre sono disponibili i seguenti comandi:

MOUNT "Lettera Drive Emulato" "Drive o directory reale"
      [-t tipo] [-aspi] [-ioctl] [-noioctl] [-usecd numero] [-size dimensionedrive] 
      [-label etichettadrive] [-freesize dimensione_in_mb]
      [-freesize dimensione_in_kb (per i floppy)]
MOUNT -cd
MOUNT -u "Lettera Drive Emulato"

  Programma per montare le directory locali come drive dentro DOSBox.

  "Lettera Drive Emulato"
        La lettera di drive dentro DOSBox (es. C).

  "Lettera Drive Reale (solitamente per i CD-ROM in Windows) o Directory"
        La directory locale cui vuoi accedere da dentro DOSBox.

  -t tipo
        Tipo di directory montata. Valori supportati: dir (default),
        floppy, cdrom.

  -size dimensionedrive
        Imposta la dimensione del drive, dove dimensionedrive � nella forma
        "bps,spc,tcl,fcl":
           bps: byte per settore, di default 512 per i drive regolari e
                2048 per i drive CD-ROM
           spc: settori per cluster, di solito tra 1 e 127
           tcl: cluster totali, tra 1 e 65534
           fcl: cluster totali disponibili, tra 1 e tcl

  -freesize dimensione_in_mb | dimensione_in_kb
        Imposta la quantit� di spazio libero disponibile sul drive in
        megabyte (drive regolari) o kilobyte (drive floppy).
        Si tratta di una versione semplificata di -size.

  -label etichettadrive
        Imposta il nome del drive a "etichettadrive". Richiesto da
        alcuni sistemi se l'etichetta del cd non � letta correttamente.
        Utile quando un programma non riesce a trovare il proprio CD-ROM.
        Se non specifichi un'etichetta e non � selezionato nessun supporto
        di basso livello (ci� avviene quando ometti -usecd # e/o -aspi o
        quando specifichi -noioctl):
          Per Windows: l'etichetta � estratta dal "Drive Reale".
          Per Linux: l'etichetta � impostata su NO_LABEL.

        Se specifichi un'etichetta, questa verr� mantenuta fin quando il drive
        rimarr� montato. Non verr� modificata !!

  -aspi
        Forza l'uso del layer aspi. Valido soltanto se si sta montando un
        CD-ROM sotto sistemi Windows con un layer ASPI installato.

  -ioctl (selezione automatica dell'interfaccia CD audio)
  -ioctl_dx (estrazione dell'audio digitale usata per i CD audio)
  -ioctl_dio (chiamate ioctl usate per i CD audio)
  -ioctl_mci (MCI usato per i CD audio)
        Forza l'uso dei comandi ioctl. Valido solo se si monta un CD-ROM sotto 
        un SO Windows che li supporti (Win2000/XP/NT).
        Le varie scelte variano solo nel modo in cui il CD audio � gestito,
        preferibilmente viene usato -ioctl_dio (il pi� leggero), ma potrebbe non
        funzionare su tutti i sistemo, quindi si pu� anche provare con -ioctl_dx
        (o -ioctl_mci).

  -noioctl   
        Forza l'uso di un layer CD-ROM SDL. Valido su tutti i sistemi.

  -usecd numero
        Valido su tutti i sistemi, ma sotto windows va abbinato a -noioctl.
        Permette di scegliere il drive che deve essere usato da SDL. Usalo
        quando l'interfaccia SDL CD-ROM monta il drive sbagliato o non ne monta
        nessuno. "numero" pu� essere ricavato digitando "MOUNT -cd".

  -cd
        Mostra tutti i drive CD-ROM rilevati da SDL, e i rispettivi numeri.
        Vedi le informazioni alla voce -usecd, qui sopra.

  -u
        Rimuove il mount. Non funziona per Z:\.

  Nota: E' possibile montare una directory locale come drive CD-ROM.
        In questo caso per� mancher� il supporto hardware.

  In pratica MOUNT ti permette di connettere l'hardware reale al PC emulato da
  DOSBox. Quindi MOUNT C C:\GIOCHI dice a DOSBox di usare la tua directory
  C:\GIOCHI come drive C: in DOSBox. Ti permette anche di cambiare la lettera
  identificativa del drive per venire incontro a quei programmi che richiedono
  lettere di drive specifiche.
  
  Per esempio: Touche: Adventures of The Fifth Musketeer deve essere avviato
  sul tuo drive C:. Usando DOSBox e il suo comando mount, puoi ingannare il
  gioco e fargli credere di trovarsi nel drive C, mentre puoi continuare a
  mettere il gioco dove preferisci. Per esempio, se il gioco si trova in
  D:\GIOCHI\TOUCHE, il comando MOUNT C D:\GIOCHI\TOUCHE ti permetter� di
  avviare Touche dal drive D.

  Montare l'intero drive C con MOUNT C C:\ � ALTAMENTE sconsigliato! Stesso
  discorso vale per il montare la directory radice di qualsiasi altro drive,
  eccetto che per i CD-ROM (a causa della loro natura a sola lettura).
  In caso contrario, se fai errori all'interno del DOSBox potresti perdere
  tutti i tuoi file.
  E' consigliato mettere tutte le tue applicazioni/giochi in una sottodirectory
  e montare quella.

  Esempi di MOUNT generali:
    1. Per montare c:\DirX come floppy : 
         mount a c:\DirX -t floppy
    2. Per montare il cdrom di sistema E come cdrom sul drive D in DOSBox:
         mount d e:\ -t cdrom
    3. Per montare il drive CD-ROM di sistema nel punto di mount /media/cdrom come
       drive CD-ROM D in dosbox:
         mount d /media/cdrom -t cdrom -usecd 0
    4. Per montare un drive con ~870 mb di spazio disponibile (versione semplice):
         mount c d:\ -freesize 870
    5. Per montare un drive con ~870 mb di spazio disponibile (solo esperti, pieno controllo):
         mount c d:\ -size 512,127,16513,13500
    6. Per montare /home/user/dirY come drive C in DOSBox:
         mount c /home/user/dirY
    7. Per montare la directory da cui DOSBox � stato eseguito come D in DOSBox:
         mount d .
         (nota che . rappresenta la directory da cui DOSBox � avviato)


MEM
  Programma per visualizzare la quantit� di memoria disponibile.


VER
VER set versione_maggiore [versione_minore]
  Mostra la versione attuale di DOSBox, e la versione di DOS riportata
  (utilizzo senza parametri).
  Cambia la versione di DOS riportata col parametro "set",
  per esempio: "VER set 6 22" per far s� che DOSBox riporti DOS 6.22
  come versione DOS.


CONFIG -writeconf filelocale
CONFIG -writelang filelocale
CONFIG -securemode
CONFIG -set "sezione propriet�=valore"
CONFIG -get "sezione propriet�"

  CONFIG pu� essere usato per cambiare o visualizzare varie impostazioni di
  DOSBox durante la sua esecuzione. Pu� salvare le impostazioni correnti o
  le stringhe di linguaggio su disco. Informazioni a riguardo di tutte le
  possibili sezioni e propriet� possono essere trovate nella sezione 11
  (Il File di Configurazione).

  -writeconf filelocale
       Scrive la configurazione attuale su un file. "filelocale" �
       localizzato sul drive locale, non su un drive montato in DOSBox.
       Il file di configurazione controlla varie impostazioni di DOSBox:
       la quantit� di memoria emulata, le schede audio emulate e tante
       altre cose. Permette anche l'accesso ad AUTOEXEC.BAT.
       Vedi la Sezione 11 (Il File di Configurazione) per ulteriori
       informazioni.

  -writelang filelocale
       Scrive le impostazioni di linguaggio attuali su un file. "filelocale"
       � localizzato sul drive locale, non su un drive montato in DOSBox.
       Il file di linguaggio controlla tutto l'output dei comandi interni
       visibile nel dosbox e il dos interno.

  -securemode
       Imposta DOSBox su una modalit� pi� sicura. In questa modalit� i
       comandi interni MOUNT, IMGMOUNT e BOOT non funzionano. Non � inoltre
       possibile creare un nuovo file di configurazione o di linguaggio.
       (Attenzione: puoi annullare questa modalit� solo riavviando DOSBox.)

  -set "sezione propriet�=valore"
       CONFIG prover� a impostare la propriet� al nuovo valore. Attualmente
       CONFIG non � ancora in grado di riportare se il comando ha avuto
       successo o meno.

  -get "sezione propriet�"
       Il valore attuale della propriet� � riportato e memorizzato nella
       variabile di ambiente %CONFIG%. Questo � utile per memorizzarne il
       valore all'interno di file batch.

  Sia "-set" che "-get" funzionano dai file batch e possono essere usati per
  impostare i tuoi settaggi preferiti per ogni gioco. 
  
  Esempi:
    1. Per creare un file di configurazione nella tua directory corrente:
        config -writeconf dosbox.conf
    2. Per impostare i cicli cpu a 10000:
        config -set "cpu cycles=10000"
    3. Per disattivare l'emulazione ems:
        config -set "dos ems=off"
    4. Per controllare che cpu core si sta utilizzando:
        config -get "cpu core"


LOADFIX [-size] [programma] [parametri-programma]
LOADFIX -f
  Programma per ridurre la quantit� di memoria disponibile. Utile per i vecchi
  programmi che non si aspettano di avere molta memoria disponibile.

  -size	        
        numero di kilobyte da "mangiare", default = 64 kb
  
  -f
        libera tutta la memoria precedentemente allocata
  
  Esempi:
    1. Per avviare mm2.exe e allocare 64kb di memoria
       (mm2 avr� 64 kb in meno disponibili) :
       loadfix mm2
    2. Per avviare mm2.exe e allocare 32kb di memoria :
       loadfix -32 mm2
    3. Per liberare la memoria precedentemente allocata :
       loadfix -f


RESCAN
  Fa s� che DOSBox rilegga la struttura delle directory. Utile se hai fatto
  qualche cambiamento sui drive montati da fuori DOSBox. (CTRL - F4 fa la stessa
  cosa!)
  

MIXER
  Fa s� che DOSBox visualizzi i correnti settaggi di volume.
  Ecco come cambiarli:
  
  mixer canale sinistra:destra [/NOSHOW] [/LISTMIDI]
  
  canale
      Pu� essere uno dei seguenti: MASTER, DISNEY, SPKR, GUS, SB, FM [, CDAUDIO].
      CDAUDIO � disponibile solo se � disponibile una interfaccia CD-ROM con
      controllo del volume (Immagine CD, ioctl_dx).
  
  sinistra:destra
      I livelli di volume in percentuale. Se preceduti da una D, sono
      espressi in decibel (esempio mixer gus d-10).
  
  /NOSHOW
      Evita che DOSBox mostri i risultati se imposti uno dei
      livelli di volume.

  /LISTMIDI
      Lista i dispositivi midi disponibili sul tuo PC (Windows). Per
      selezionare un dispositivo diverso dal midi-mapper standard di
      Windows, aggiungi una riga 'midiconfig=id' alla sezione [midi] del
      file di configurazione, dove 'id' � il numero del dispositivo
      cos� come elencato da LISTMIDI.


IMGMOUNT
  Una utilit� per montare immagini disco e immagini CD-ROM in DOSBox.
  
  IMGMOUNT DRIVE [fileimmagine] -t [tipo_immagine] -fs [formato_immagine] 
            -size [dimensionesettoreinbyte, settoripertestina, testine, cilindri]
  IMGMOUNT DRIVE [fileimmag1, .. ,fileimmagN] -t iso -fs iso 

  fileimmagine
      Locazione dei file immagine da montare in DOSBox. La locazione pu�
      essere su un drive montato dentro DOSBox, o sul tuo disco reale.
      E' anche possibile montare immagini CD-ROM (ISO o CUE/BIN), se ti
      serve cambiare le immagini "in corsa" specificale tutte in successione.
      (vedi la successiva voce).
      CUE/BIN � il formato preferito per le immagini CD-ROM perch� possono
      immagazzinare tracce audio, mentre le ISO soltanto dati. Quando monti
      un CUE/BIN, riferisciti sempre al CUE.
      
  fileimmag1, .. ,fileimmagN
      Posizione dei file immagine da montare in DOSBox. E' permesso specificare
      pi� file immagine solo per le immagini CD-ROM. I CD possono poi essere
      cambiati con CTRL-F4 in qualsiasi momento. Ci� � richiesto dai giochi
      che usano pi� CD-ROM e richiedono che il CD venga sostituito nel bel
      mezzo della partita.
   
  -t 
      I seguenti sono tipi di immagine validi:
        floppy: Specifica una immagine floppy.  DOSBox rilever� automaticamente la
                geometria del disco ( 360K, 1.2MB, 720K, 1.44MB, ecc).
        iso:    Specifica un'immagine iso CD-ROM.  La geometria � settata
                automaticamente per la dimensione. Pu� essere in formato iso o cue/bin.
        hdd:    Specifica un'immagine disco rigido. Va impostata la corretta geometria
                del drive perch� essa funzioni.

  -fs 
      I seguenti sono formati di file system validi:
        iso:  Specifica il formato CD-ROM ISO 9660.
        fat:  Specifica che l'immagine usa il file system FAT. DOSBox prover� a
              montare questa immagine come un drive in DOSBox e a rendere i file
              disponibili da dentro DOSBox.
        none: DOSBox non prover� a leggere il file system del disco. Questo �
              utile se ti serve formattarlo o se vuoi avviare il disco usando
              il comando BOOT.  Quando usi il filesystem "none", devi specificare
              il numero del drive (2 o 3, dove 2 = master, 3 = slave) piuttosto
              che una lettera di drive.
              Per esempio, per montare una immagine da 70MB come drive slave,
              dovresti digitare (senza le virgolette):
                "imgmount 3 d:\test.img -size 512,63,16,142 -fs none" 
                Confrontalo con un mount per leggere il drive
                in DOSBox, che sarebbe qualcosa del genere:
                "imgmount e: d:\test.img -size 512,63,16,142"

  -size
     Le specifiche in Cilindri, Testine e Settori del drive.
     Richiesto per montare immagini disco rigido.
     
  Esempio su come montare immagini CD-ROM:
    1a. mount c /tmp
    1b. imgmount d c:\mia_iso.iso -t iso
  o (funziona ugualmente):
    2. imgmount d /tmp/mia_iso.iso -t iso


BOOT
  Boot avvia immagini floppy o immagini disco rigido indipendentemente dal
  sistema operativo emulato da DOSBox. Questo ti permetter� di avviare
  i dischetti di avvio o altri sistemi operativi dentro DOSBox.
  Se il sistema emulato � PCjr (machine=pcjr) il comando boot pu� essere
  usato per caricare cartucce PCjr (.jrc).

  BOOT [imgdisco1.img imgdisco2.img .. imgdiscoN.img] [-l letteradrive]
  BOOT [cart.jrc]  (solo PCjr)

  imgdiscoN.img 
     Questo pu� essere qualsiasi numero di immagini floppy disk che si
     vuole montare dopo che DOSBox abbia avviato la lettera di drive
     specificata.
     Per cambiare tra le varie immagini, premi CTRL-F4 per passare al
     successivo disco nella lista. La lista ricomincer� da capo quando
     raggiunta la fine.

  [-l letteradrive]
     Questo parametro ti permette di specificare il drive da cui effettuare
     il boot. Per default � il drive A, il floppy.  Puoi anche avviare
     una immagine disco rigido montata come master specificando "-l C"
     senza i doppi apici, o come slave specificando "-l D"
     
   cart.jrc (solo PCjr)
     Quando l'emulazione di PCjr � attivata, le cartucce possono essere
     caricate col comando BOOT. Il supporto, tuttavia, � ancora limitato.


IPX

  Devi abilitare il networking IPX nel file di configurazione di DOSBox.

  Tutto il networking IPX � gestito attraverso il programma interno DOSBox
  IPXNET. Per aiuto riguardo il networking IPX da dentro DOSBox, digita
  "IPXNET HELP" (senza doppi apici) e il programma mostrer� i comandi
  e la documentazione.

  Al fine di impostare una rete vera e propria, un sistema deve essere il
  server. Per impostarlo, digita "IPXNET STARTSERVER" (senza doppi apici)
  all'interno di una sessione DOSBox. La sessione server DOSBox si aggiunger�
  automaticamente alla rete IPX virtuale. Per ogni computer aggiuntivo che
  dovr� far parte della rete IPX virtuale, dovrai digitare
  "IPXNET CONNECT <nome host o indirizzo IP del computer>".
  Per esempio, se il tuo server � bob.dosbox.com, dovrai digitare
  "IPXNET CONNECT bob.dosbox.com" su ogni sistema che non sia il server.
  
  Per giocare a giochi che necessitano di Netbios, serve un file chiamato
  NETBIOS.EXE fornito da Novell. Stabilisci la connessione IPX come spiegato
  sopra, quindi avvia "netbios.exe".

  Segue una lista di comandi IPXNET come riferimento:

  IPXNET CONNECT 

     IPXNET CONNECT apre una connessione a un tunneling server IPX in
     esecuzione su un'altra sessione DOSBox. Il parametro "indirizzo"
     specifica l'indirizzo IP o il nome host del computer server. Puoi
     anche specificare la porta UDP da usare. Per default IPXNET usa la
     porta 213 - assegnata da IANA per il tunneling IPX - per le connessioni.

     La sintassi di IPXNET CONNECT �: 
     IPXNET CONNECT indirizzo <porta> 

  IPXNET DISCONNECT 

     IPXNET DISCONNECT chiude la connessione col tunneling server IPX.

     La sintassi di IPXNET DISCONNECT �:
     IPXNET DISCONNECT 

  IPXNET STARTSERVER 

     IPXNET STARTSERVER avvia un tunneling server IPX in questa sessione DOSBox.
     Per default, il server accetter� le connessioni sulla porta UDP 213,
     anche se questo pu� essere cambiato. Quando il server � avviato, DOSBox
     avvier� automaticamente una connessione client al server stesso.

     La sintassi di IPXNET STARTSERVER �:
     IPXNET STARTSERVER <porta>

     Se il server � dietro ad un router, la porta UDP <porta> deve essere
     inoltrata a quel computer.

     Sui sistemi basati su Linux/Unix i numeri di porta minori di 1023 possono
     essere usati soltanto con i privilegi di amministratori. Su questi sistemi
     usare porte maggiori di 1023.

  IPXNET STOPSERVER

     IPXNET STOPSERVER ferma il tunneling server IPX in esecuzione in questa
     sessione DOSBox. Bisogna per� assicurarsi che tutte le altre connessioni
     siano anch'esse terminate, dato che fermare il server pu� causare blocchi
     sulle altre macchine che ancora lo stanno utilizzando.

     La sintassi di IPXNET STOPSERVER �: 
     IPXNET STOPSERVER

  IPXNET PING

     IPXNET PING manda in broadcast una richiesta di ping attraverso il
     network IPX. In risposta, tutti gli altri computer connessi risponderanno
     al ping e sar� riportato il tempo necessario a ricevere ed inviare il
     messaggio di ping.

     La sintassi di IPXNET PING �: 
     IPXNET PING

  IPXNET STATUS

     IPXNET STATUS visualizza lo stato del network IPX sulla sessione corrente
     di DOSBox. Per una lista di tutti i computer connessi alla rete usa il
     comando IPXNET PING.

     La sintassi di IPXNET STATUS �: 
     IPXNET STATUS 


KEYB [codicelinguaggio [codepage [filecodepage]]]
  Cambia il layout della tastiera. Per informazioni dettagliate riguardo
  i layout della tastiera, guarda la Sezione 7.

  [codicelinguaggio] � una stringa che consiste di due caratteri (o in casi
     speciali anche di pi�), ad esempio GK (Grecia) o IT (Italia). Specifica
     il layout di tastiera da utilizzare.

  [codepage] � il numero del codepage da utilizzare. Il layout tastiera deve
     fornire supporto per il codepage specificato, altrimenti il caricamento
     del layout non andr� a buon fine.
     Se non viene specificato nessun codepage, verr� caricato un codepage
     opportuno per il layout che � stato scelto.

  [filecodepage] pu� essere usato per caricare codepage che non sono ancora inclusi
     dentro DOSBox. E' necessario soltanto quando DOSBox non trova il codepage.


  Esempi:
    1. Per caricare il layout tastiera tedesco (che usa automaticamente il codepage 858):
         keyb gr
    2. Per caricare il layout russo con codepage 866:
         keyb ru 866
       Per potere usare i caratteri russi premi ALT+MAIUSC-DI-DESTRA.
    3. Per caricare il layout francese con codepage 850 (dove il codepage
       � definito in EGACPI.DAT):
         keyb fr 850 EGACPI.DAT
    4. Per caricare il codepage 858 (senza un layout di tastiera):
         keyb none 858
     Questo pu� essere usato per cambiare il codepage per l'utility keyb2 del FreeDOS.
    5. Per visualizzare il codepage attuale e, se caricato, il layout tastiera:
         keyb



Per ulteriori informazioni usa il parametro /? dopo i vari comandi.



==================
5. Tasti Speciali:
==================

ALT-ENTER     Attiva e disattiva la visualizzazione a schermo intero.
ALT-PAUSE     Mette in pausa l'emulazione (premi nuovamente ALT-PAUSE per riprenderla).
CTRL-F1       Avvia il keymapper.
CTRL-F4       Cambia l'immagine disco montata. Aggiorna la cache directory per tutti i drive!
CTRL-ALT-F5   Avvia/Ferma la registrazione dell'output video su un filmato. (cattura video avi)
CTRL-F5       Salva uno screenshot. (formato PNG)
CTRL-F6       Avvia/Ferma la registrazione dell'output audio su un file wave.
CTRL-ALT-F7   Avvia/Ferma la registrazione dei comandi OPL. (formato DRO)
CTRL-ALT-F8   Avvia/Ferma la registrazione dei comandi grezzi MIDI.
CTRL-F7       Diminuisce il frameskip.
CTRL-F8       Aumenta il frameskip.
CTRL-F9       Chiude istantaneamente DOSBox.
CTRL-F10      Cattura/Rilascia l'uso del mouse.
CTRL-F11      Rallenta l'emulazione (diminuisce i cicli DOSBox).
CTRL-F12      Accelera l'emulazione (aumenta i cicli DOSBox).
ALT-F12       Sblocca la velocit� (bottone turbo).

NOTA: Quando aumenti i cicli di DOSBox oltre le capacit� che il tuo computer
pu� gestire, avrai l'effetto opposto, cio� quello di rallentare l'emulazione.
Questa capacit� varia da computer a computer.


Questi sono i tasti di default. Possono essere cambiati col keymapper.
(vedi la Sezione 6: Mapper)

I file salvati/registrati possono essere trovati in directory_corrente/capture
(pu� essere modificata nel file di configurazione).
La directory deve esistere prima di avviare DOSBox, altrimenti non verr�
salvato/registrato niente !



==========
6. Mapper:
==========

Quando avvii il mapper del DOSBox (con CTRL-F1 o col parametro -startmapper
quando avvii l'eseguibile di DOSBox) ti viene presentata una tastiera virtuale
e un joystick virtuale.

Questi dispositivi virtuali corrispondono ai tasti che DOSBox riporter�
alle applicazioni DOS. Se clicchi su un tasto col tuo mouse, potrai vedere
nell'angolo in basso a sinistra quale evento vi � associato (EVENT) e a
quali eventi � attualmente collegato.

Event: EVENT
BIND: BIND
                        Add   Del
mod1  hold                    Next
mod2
mod3


EVENT
    Il tasto o bottone/asse del joystick che DOSBox riporter� alle applicazioni DOS.
BIND
    Il tasto sulla tua tastiera reale o il bottone/asse/stick sul tuo joystick
    reale (come riportato da SDL) che � connesso all'EVENT.
mod1,2,3 
    Modfiers. Questi sono tasti che devono essere premuti durante la pressione del
    tasto BIND. mod1 = CTRL e mod2 = ALT. Vengono in genere usati soltanto quando
    vuoi cambiare i tasti speciali del DOSBox.
Add 
    Aggiunge un nuovo BIND per questo EVENT. In pratica aggiunge un tasto dalla
    tua tastiera o un evento dal joystick (pressione di un tasto, movimento di
    un asse) che produrr� un EVENT in DOSBox.
Del 
    Elimina il BIND a questo EVENT. Se un EVENT non ha BIND, allora non �
    possibile far partire questo evento in DOSBox (cio� non vi � modo di usare
    quel tasto o quel bottone del joystick).
Next
    Scorre la lista di collegamenti che si riferiscono a questo EVENT.


Esempio:
D1. Vuoi che la X della tua tastiera produca una Z nel DOSBox.
    R. Clicca sulla Z del mapper. Clicca su "Add".
       Ora premi il tasto X sulla tua tastiera.

D2. Se clicchi su "Next" un paio di volte, noterai che anche la Z sulla tua
    tastiera produce una Z in DOSBox.
    R. Quindi scegli la Z di nuovo, e clicca su "Next" fin quando non avrai la
       Z sulla tastiera. Ora clicca "Del".

D3. Provando in DOSBox, noti che la pressione di X fa apparire ZX.
     R. La X sulla tua tastiera � ancora mappata alla X! Clicca sulla X della
        tastiera del mapper e scorri con "Next" fin quando non trovi il tasto X.
        A questo punto clicca su "Del".


Esempi riguardanti il rimappare il joystick:
  Hai un joystick collegato, funziona bene sotto DOSBox e vuoi giocare
  ad un gioco che funziona solo con la tastiera, col tuo joystick (assumeremo
  che il gioco � controllato attraverso le frecce direzionali sulla
  tastiera):
    1. Avvia il mapper, quindi clicca su una delle frecce al centro
       della parte sinistra dello schermo (proprio sopra i bottoni mod1
       e mod2). EVENT dovrebbe essere key_left. Orra clicca su Add e
       muovi il joystick nella relativa direzione, questo dovrebbe aggiungere
       un evento al BIND.
    2. Ripeti il punto precedente per le altre tre direzioni. E' anche
       possibile rimappare anche i bottoni del joystick (fuoco/salto).
    3. Clicca su Save, quindi su Exit e prova con qualche gioco.

  Vuoi invertire l'asse y del joystick perch� un gioco di simulazione aerea
  usa il movimento sopra/sotto in un modo che non ti va, e non � configurabile
  nel gioco stesso:
    1. Avvia il mapper e clicca su Y- nello spazio del joystick in alto (questo
       si riferisce al primo joystick se ne hai due attaccati) o nello spazio in
       basso (secondo joystick o, se ne hai solo uno attaccato, l'altra croce
       di assi).
       EVENT dovrebbe essere jaxis_0_1- (o jaxis_1_1-).
    2. Clicca su Del per eliminare i collegamenti correnti, quindi clicca Add e muovi
       il tuo joystick in basso. Dovrebbe essere creato un nuovo collegamento.
    3. Ripeti per Y+, salva il layout e prova qualche gioco.



Se cambi le associazioni di default, puoi salvare i tuoi cambiamenti cliccando
su "Save". DOSBox salver� le nuove associazioni su una locazione specificata
nel file di configurazione (la voce mapperfile= ). All'avvio, DOSBox caricher�
il suddetto file, se � presente nel file di configurazione.



=========================
7. Layout della Tastiera:
=========================

Per passare ad un diverso layout di tastiera, puoi usare sia la voce
"keyboardlayout" nella sezione [dos] di dosbox.conf, oppure il comando
keyb.com interno di DOSBox. Entrambi accettano codici linguaggio conformi
al DOS (vedere in basso), ma solo usando keyb.com � possibile specificare
dei codepage personalizzati.

L'impostazione di default, keyboardlayout=auto attualmente funziona solo
sotto windows, il layout � scelto in accordo a quello del SO.

Cambiare layout
  DOSBox supporta un certo numero di layout di tastiera e di codepage per
  default, in questo caso � necessario speficicare solo l'identificativo
  del layout (come keyboardlayout=it nel file di configurazione di DOSBox,
  o l'uso di "keyb it" al prompt dei comandi di DOSBox).
  
  Certi layout di tastiera (ad esempio il layout GK codepage 869 e il layout
  RU codepage 808) hanno il supporto per i layout doppi che possono essere
  attivati premento ALT-DI-SINISTRA+SHIFT-DI-DESTRA e disattivati premendo
  ALT-DI-SINISTRA+SHIFT-DI-SINISTRA

File esterni supportati
  I file .kl del FreeDOS sono supportati (FreeDOS keyb2 keyboard layoutfiles)
  come anche le librerie del FreeDOS keyboard.sys/keybrd2.sys/keybrd3.sys che
  consistono in tutti i file .kl disponibili.
  Vedi http://projects.freedos.net/keyb/ per layout di tastiera precompilati
  nel caso che quelli integrati in DOSBox non dovessero funzionare, o nel caso
  che vengano rilasciati layout nuovi/pi� aggiornati.

  Possono essere usati sia i file .CPI (file codepage compatibili con MSDOS)
  che .CPX (file codepage FreeDOS compressi con UPX). Alcuni codepage sono
  inclusi in DOSBox in modo che nella maggior parte dei casi non sia necessario
  andare a cercare file codepage esterni. Se ti serve un file codepage diverso
  (o presonalizzato), copialo nella directory del file di configurazione di
  DOSBox in modo che sia accessibile da DOSBox.

  Layout aggiuntivi possono essere aggiunti copiando il corrispondente file
  .kl dentro la directory di dosbox.conf e usando la prima parte del nome del
  file come codice linguaggio.
  Esempio: Per il file UZ.KL (layout tastiera per l'Uzbekistan) specifica
           "keyboardlayout=uz" in dosbox.conf.
	L'integrazione dei pacchetti di layout tastiera (come keybrd2.sys) funziona
  in modo simile.


Nota che il layout di tastiera permette di immettere caratteri stranieri,
ma NON � possibile usarli nei nomi dei file. Cerca di evitarli sia dentro
DOSBox che nel tuo sistema operativo, in quei file/directory che saranno
poi accessibili da DOSBox.



================================
8. Funzione Multiplayer Seriale:
================================
 
DOSBox pu� emulare un cavo nullmodem seriale attraverso una rete e
internet. Pu� essere configurato attraverso la sezione [serialports]
nel file di configurazione di DOSBox.

Per creare una connessione nullmodem, uno dei lati deve agire da server e
uno da client.

Il server deve essere impostato nel file di configurazione di DOSBox cos�:
   serial1=nullmodem

Il client:
   serial1=nullmodem server:<IP o nome del server>

Ora avvia il tuo gioco e scegli nullmodem / serial cable / already connected
come metodo multiplayer su COM1. Imposta lo stesso baudrate su entrambi i
computer.

Inoltre possono essere specificati parametri aggiuntivi per controllare il
comportamento della connessione nullmodem. Questi sono tutti i parametri:

 * port:         - Numero porta TCP. Default: 23
 * rxdelay:      - quanto a lungo (millisecondi) mettere in attesa i dati ricevuti
                   se l'interfaccia non � pronta. Aumenta questo valore se
                   incontri molti errori di overrun nella Status Window di DOSBox.
                   Default: 100
 * txdelay:      - quanto a lungo trattenere i dati prima di inviare un pacchetto.
                   Default: 12
                   (riduce l'overhead della rete)
 * server:       - Questo nullmodem sar� una connessione client al server specificato.
                   (Se non viene specificato un server: sii un server.)
 * transparent:1 - Invia solo i dati seriali, nessun handshake RTS/DTR. Usa questo
                   parametro se ti connetti a qualsiasi altra cosa che non sia un
                   nullmodem.
 * telnet:1      - Interperta dati Telnet dal sistema remoto. Imposta transparent
                   automaticamente.
 * usedtr:1      - La connessione non sar� stabilita fun quando DTR non � attivato
                   dal programma DOS. Utile per i terminali modem.
                   Imposta transparent automaticamente.
 * inhsocket:1   - Usa un socket passato a DOSBox da linea di comando. Imposta
                   transparent automaticamente. (Eredit� dei Socket: Viene usato
                   per giocare vecchi giochi DOS sui nuovi software BBS.)

Esempio: Essere server in ascolto sulla porta TCP 5000.
   serial1=nullmodem server:<IP o nome del server> port:5000 rxdelay:1000



==================================================
9. Come giocare a giochi particolarmente esigenti:
==================================================

DOSBox emula la CPU, il suono e le schede video, e altre periferiche di un
PC, tutte allo stesso tempo. La velocit� di una applicazione DOS emulata
dipende da quante istruzioni possono essere emulate, che � impostabile
(numero di cicli).

Cicli CPU
  Per default (cycles=auto) DOSBox prova a rilevare se un gioco ha bisogno
  di tutti i cicli possibili per essere eseguito. Puoi forzare questo
  comportamento impostando cycles=max nel file di configurazione di DOSBox.
  Allora la finestra di DOSBox mostrer� una riga "Cpu Cycles: max" in alto.
  In questa modalit� puoi ridurre la quantit� di cicli su base percentuale
  (premi CTRL-F11) o aumentarla nuovamente (CTRL-F12).
  
  A volte impostare in maniera manuale il numero di cicli porta a risultati
  migliori, ad esempio specificando nel file di configurazione cycles=30000.
  Durante l'esecuzione delle applicazioni DOS puoi aumentare i cicli con
  CTRL-F12 anche di pi�, ma avrai comunque il limite della potenza del tuo
  processore reale. Puoi vedere in che misura � impegnato andando sul Task
  Manager di Windows 2000/XP o nel Monitor di Sistema in Windows 95/98/ME.
  Quando la CPU sar� usata al 100%, non vi � pi� modo di velocizzare DOSBox,
  a meno che tu non riduca la quantit� di CPU occupata dalle parti di DOSBox
  non strettamente legate alla CPU.

Core CPU
  Sulle architetture x86 puoi provare a forzare l'uso di un core ricompilato
  dinamicamente (imposta core=dynamic nel file di configurazione di DOSBox).
  Di solito questo fornisce migliori risultati se l'autorilevazione (core=auto)
  fallisce. E' bene accoppiarvi cycles=max. Nota che potrebbero esserci dei
  giochi che funzionano peggio col core dinamico, o che non funzionino affatto!

Emulazione grafica
  L'emulazione VGA � una parte molto esigente di DOSBox in termini di uso
  della CPU. Aumenta il numero di fotogrammi saltati (in passi di uno)
  premendo CTRL-F8. L'uso della CPU dovrebbe scendere quando si usa un
  numero di cicli fisso.
  Vai indietro di un passo e ripeti questo fin quando il gioco gira
  abbastanza velocemente per i tuoi gusti. Nota che questo � un baratto:
  perdi in fluidit� video ci� che guadagni in velocit�.

Emulazione sonora
  Puoi anche provare a disattivare il suono attraverso l'utilit� di setup dei
  giochi per ridurre ulteriormente il carico sulla CPU. Impostando nosound=true
  NON disabiliti l'emulazione sonora, ma semplicemente la riproduzione dell'output.

Inoltre cerca di chiudere tutti i programmi eccetto DOSBox per riservargli
la quantit� massima possibile di risorse.


Configurazione avanzata dei cicli:
I settaggi cycles=auto e cycles=max possono avere dei parametri per ottenere
diversi standard quando si avviano i programmi. La sintassi �
  cycles=auto ["default modalit� reale"] ["default modalit� protetta"%] 
              [limit "limite cicli"]
  cycles=max ["default modalit� protetta"%] [limit "limite cicli"]
Esempio:
  cycles=auto 1000 80% limit 20000
  user� cycles=1000 per i giochi in modalit� reale, 80% CPU variabile per i giochi
  in modalit� protetta con un limite superiore di 20000



============================
10. Risoluzione dei problemi
============================

DOSBox crasha proprio dopo averlo avviato:
  - usa diversi valori per l'opzione output= nel file di
    configurazione
  - prova ad aggiornare i driver video e le DirectX


L'avvio di un certo gioco chiude DOSBox, causa un crash con qualche messaggio o blocca tutto:
  - vedi se funziona con una installazione incontaminata di DOSBox
    (file di configurazione non modificato)
  - provalo col sonoro disattivato (usa il programma di configurazione
    del suono incluso nel gioco, oppure imposta sbtype=none e gus=false nel
    file di configurazione di DOSBox)
  - cambia alcune opzioni nel file di configurazione di DOSBox, in particolare:
      core=normal
      un numero fisso di cicli (ad esempio cycles=10000)
      ems=false
      xms=false
    oppure combinazioni dei settaggi sopra,
    aggiusta i settaggi della macchina che controllano il chipset e le
    funzionalit� emulate:
      machine=vesa_nolfb
    o
      machine=vgaonly
  - usa loadfix prima di avviare il gioco

Il gioco esce al prompt di DOSBox con qualche strano messaggio di errore:
  - leggi il messaggio di errore attentamente e prova a localizzarne la causa
  - prova i suggerimenti delle sezioni sopra
  - monta in modo diverso i drive, dato che alcuni giochi sono schizzinosi
    riguardo i percorsi, per esempio se hai usato "mount d d:\giochi\abc" prova
    "mount c d:\giochi\abc" e "mount c d:\giochi"
  - se il gioco richiede un CD-ROM assicurati di usare "-t cdrom" quando
    monti, e prova altri parametri diversi (come ioctl, usecd e label, vedi
    la sezione appropriata)
  - controlla i permessi sui file del gioco (togli gli attributi di sola lettura,
    aggiungi i permessi in scrittura ecc.)
  - prova a reinstallare il gioco da dentro DOSBox



==============================
11. Il file di configurazione:
==============================

Un file di configurazione pu� essere generato usando CONFIG.COM, che pu�
essere trovato nel drive interno Z: quando avvii DOSBox. Leggi la sezione
dei programmi interni del readme per sapere come usare CONFIG.COM.
Puoi modificare il file di configurazione generato, per personalizzare
DOSBox.

Il file � diviso in varie sezioni (i cui nomi sono racchiusi tra [] ).
Alcune sezioni hanno opzioni che puoi impostare.
# and % indicate comment-lines. 
# e % indicano righe commentate.
Il file di configurazione generato contiene i settaggi attuali. Puoi modificarli
e avviare DOSBox col parametro -conf per caricare il file e usare i nuovi settaggi.

DOSBox caricher� i file di configurazione che sono specificati da -conf.
Se non ve n'� nessuno, prover� a caricare "dosbox.conf" dalla directory
locale. Se non c'�, DOSBox caricher� il file di configurazione utente.
Questo file, se inesistente, verr� creato. Il file pu� essere trovato
in ~/.dosbox (Linux) o  "~/Library/Preferences" (MAC OS X in inglese).
Gli utenti Windows dovrebbero usare la scorciatoia nel menu Start per
trovarlo.




=======================
12. Il file linguaggio:
=======================

CONFIG.COM pu� generare un file linguaggio (CONFIG -writelang filelinguaggio).
Leggilo e, si spera, capirai come modificarlo.
Avvia DOSBox col parametro -lang per usare il tuo nuovo file linguaggio.
In alternativa, puoi impostarne il nome nel file di configurazione nella
sezione [dosbox]. Troverai un'opzione language= che puoi cambiare come pi�
ti aggrada.



========================================
13. Costruire la tua versione di DOSBox:
========================================

Scarica i sorgenti.
Guarda l'INSTALL che sta al loro interno.



============================
14. Ringraziamenti speciali:
============================

Vedi il file THANKS.


=============
15. Contatti:
=============

Vai nel sito:
http://www.dosbox.com
per gli indirizzi email (pagina Crew).
