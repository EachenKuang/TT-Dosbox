DOSBox v0.73


=====
NOTA: 
=====

Enquanto n�s estamos torcendo para que um dia o DOSBox rode todos os programas
j� feitos para PC, ainda n�o estamos l�. Hoje o DOSBox, rodando
numa m�quina potente, dificilmente ser� equivalente a um PC 486.
O DOSBox pode ser configurado para rodar um leque variado de jogos DOS,
desde cl�ssicos CGA/Tandy/PCjr at� jogos da era Quake.


Arquivo LEIA-ME traduzido por: Lex Leite   / ableite@msn.com
                               Sael Aran   / lord.sael@hokkaido-fansubber.com

                 com ajuda de: Mosca-Ninja / - -
                               David Tuka  / david_tuka@hotmail.com



=======
�NDICE:
=======
1. In�cio R�pido
2. Perguntas & Respostas
3. Uso
4. Programas Internos
5. Teclas Especiais
6. Mapeador de Teclas
7. Layout do teclado
8. Fun��o Multi-Jogador via Serial
9. Como rodar jogos que necessitam mais recursos
10. Solu��o de Problemas
11. O arquivo das configura��es
12. O arquivo do idioma
13. Fazendo sua pr�pria vers�o do DOSBox
14. Agradecimentos especiais
15. Contato


=================
1. In�cio R�pido:
=================

Digite INTRO no DOSBox para um tour r�pido. 
� essencial que voc� se familiarize com a ideia de montar
diret�rios. O DOSBox n�o faz com que qualquer unidade
(ou parte dela) seja automaticamente acess�vel para emula��o.
Veja a parte de P&R "Eu tenho um diret�rio Z ao inv�s de
um C no prompt." assim como a explica��o do comando MOUNT
(se��o 4)



=======
2. P&R:
=======

Algumas perguntas feitas frequentemente:

P: Aparece um diret�rio Z ao inv�s de um C no prompt.
P: Sempre deverei digitar esses comandos? N�o existe uma forma autom�tica?
P: Como eu coloco tela cheia?
P: Meu CD-ROM n�o funciona.
P: O jogo/aplicativo n�o consegue achar seu CD-ROM.
P: O mouse n�o funciona.
P: O aplicativo n�o tem som.
P: O som sai cortado ou estranho/difuso.
P: Eu n�o consigo digitar \ ou : no DOSBox.
P: Estou com atraso no teclado.
P: O cursor est� se movendo em apenas uma dire��o!
P: O jogo/aplicativo roda muito lento!
P: O jogo/aplicativo n�o chega a rodar/trava!
P: O DOSBox pode danificar meu computador?
P: Eu queria trocar o tamanho da mem�ria/Velocidade da CPU/ems/soundblaster IRQ.
P: Quais hardwares de som o DOSBox emula atualmente?
P: DOSBox trava no in�cio e eu estou rodando artes/cinem�tica.
P: Estou tendo problemas para rodar um jogo feito com a Build Engine (Duke3D/Blood/Shadow Warrior).
P: Excelente LEIAME, mas eu ainda n�o entendi.




P: Aparece um diret�rio Z ao inv�s de um C no prompt.
R: Voc� deve fazer seus diret�rios ficarem dispon�veis no DOSBox usando 
   o comando "mount". Por exemplo, no Windows "mount C D:\JOGOS" vai criar
   um drive C no DOSBox que leva ao seu diret�rio D:\JOGOS.
   No Linux, "mount c /home/username" criar� um drive C no DOSBox
   que leva para o /home/username no Linux.
   Para mudar o drive montado, digite "C:". Se tudo ocorreu
   bem, DOSBox ir� mostrar no prompt "C:\>".


P: Sempre deverei digitar esses comandos? N�o existe uma forma autom�tica?
R: No arquivo de configura��es do DOSBox, existe uma se��o [autoexec]. Os comandos
   ali escritos s�o executados quando o DOSBox iniciar, ent�o voc� pode usar esta se��o 
   para a montagem.


P: Como eu coloco tela cheia?
R: Pressione alt-enter. Alternativamente: Edite o arquivo de configura��es do DOSBox e
   mude a op��o fullscreen=false para fullscreen=true. Se na tela cheia lhe parece 
   errada: Altere a op��o fullresolution no arquivo de configura��es do
   DOSBox. Para sair do modo tela cheia: Pressione alt-enter novamente.


P: Meu CD-ROM n�o funciona.
R: Para montar seu CD-ROM no DOSBox, voc� deve especificar algumas op��es adicionais 
   ao montar o CD-ROM. 
   Para ativar o suporte ao CD-ROM (incluindo MSCDEX):
     - mount d f:\ -t cdrom (windows)
     - mount d /media/cdrom -t cdrom (linux)

   Em alguns casos voc� pode querer usar uma interface CD-ROM diferente,
   por exemplo, caso o �udio do CD n�o funcione:
     Para ativar o suporte ao SDL (n�o inclui acesso do CD em baixo n�vel!):
       - mount d f:\ -t cdrom -usecd 0 -noioctl
     Para ativar o acesso do ioctl usando extra��o digital de �udio para CDs de �udio
     (apenas no windows, �til para o Vista):
       - mount d f:\ -t cdrom -ioctl_dx
     Para ativar o acesso do ioctl usando MCI para CDs de �udio (apenas no windows):
       - mount d f:\ -t cdrom -ioctl_mci
     Para for�ar apenas o acesso pelo ioctl (apenas no windows):
       - mount d f:\ -t cdrom -ioctl_dio
     Para ativar o suporte aspi em baixo n�vel (win98 com aspi-layer instalado):
       - mount d f:\ -t cdrom -aspi
   
   Nos comandos:    - d   letra da unidade que aparecer� no DOSBox
                    - f:\ localiza��o do CD-ROM no seu PC.
                    - 0   O n�mero da unidade de CD-ROM, reportado pelo comando "mount -cd"
                          (note que este valor s� � necess�rio quando o SDL � utilizado
                           para CDs de �udio, de qualquer outra maneira � ignorado)
   Veja tamb�m a pr�xima pergunta: O jogo/aplicativo n�o consegue achar seu CD-ROM.


P: O jogo/aplicativo n�o consegue achar seu CD-ROM.
R: Tenha certeza de montar o CD-ROM com o switch -t cdrom, isso ativar� a
   interface MSCDEX requerida por jogos em DOS para se comunicar com os CD-ROMs.
   Tente tamb�m adicionar o r�tulo correto (-label R�TULO) no comando mount,
   onde R�TULO � o r�tulo do CD (ID do volume).
   No Windows, voc� pode especificar -ioctl, -aspi ou -noioctl. Olhe a 
   descri��o do comando mount na Se��o 4 para entender seus significados e 
   op��es adicionais, relacionadas com CDs de �udio, -ioctl_dx, ioctl_mci, ioctl_dio.
   
   Tente criar uma imagem do CD-ROM (preferivelmente o par CUE/BIN) e usar a 
   ferramenta interna IMGMOUNT do DOSBox para montar a imagem (a lista CUE).
   Isso ativa o suporte ao CD-ROM em baixo n�vel para qualquer sistema operacional.


P: O mouse n�o funciona.
R: Normalmente, o DOSBox detecta quando um jogo utiliza o mouse. Quando voc� clica na 
   tela, o mouse dever� ser capturado pelo DOSBox e funcionar.
   Em alguns jogos a detec��o do mouse n�o funciona. Nesses casos 
   voc� dever� capturar o mouse manualmente apertando CTRL-F10.


P: O aplicativo n�o tem som.
R: Tenha certeza que o som est� configurado corretamente no jogo. Isso pode ser
   feito durante a instala��o ou no programa setup/setsound que acompanha 
   o jogo. Primeiro, veja se existe uma op��o para auto-detec��o. Se n�o 
   existe, tente selecionar soundblaster ou soundblaster16 com as configura��es
   padr�es, sendo "address=220 irq=7 dma=1". Voc� talvez queira selecionar o
   midi no address 330 como dispositivo de m�sica.
   Os par�metros das placas de som emuladas podem ser alterados no arquivo de 
   configura��es do DOSBox.
   Se continuar sem som, coloque o n�cleo (core) em normal e use valores
   menores e fixos para os ciclos (como cycles=2000). Tamb�m assegure que 
   o seu sistema operacional est� com som ativado.
   Em alguns casos, pode ser �til usar um dispositivo emulador de som diferente
   como soundblaster pro (sbtype=sbpro1 no arquivo de configura��es do DOSBox) ou
   o gravis ultrasound (gus=true).


P: O som sai cortado ou estranho/difuso.
R: Voc� est� exigindo muito da sua CPU para manter o DOSBox rodando naquela velocidade.
   Voc� pode diminuir os ciclos, pular quadros, reduzir a taxa de amostragem do
   dispositivo de som (veja o arquivo de configura��es do DOSBox) ou
   o dispositivo mixador. Voc� pode tamb�m aumentar o pr�buffer no arquivo de configura��es do DOSBox.
   Se voc� est� usando cycles=max ou =auto, ent�o tenha certeza que n�o existe
   nenhum processo em segundo plano interferindo! (especialmente se estes acessam o disco r�gido)


P: Eu n�o consigo digitar \ ou : no DOSBox.
R: Isso pode acontecer em v�rias situa��es, caso o layout do seu teclado n�o possua uma
   representa��o adequada no DOS (ou n�o foi detectada corretamente),
   ou o mapeamento das teclas est� errado.
   Algumas poss�veis solu��es:
     1. Use /, ou ALT-58 para : e ALT-92 para \.
     2. Mude o layout do teclado do DOS (veja Se��o 7: Layout do teclado).
     3. Adicione os comandos que voc� quer na se��o [autoexec]
        do arquivo de configura��es do DOSBox.
     4. Abra o arquivo de configura��es do DOSBox e mude o valor do usescancodes.
     5. Mude o layout do teclado do seu sistema operacional.
   
   Note que se o layout do seu teclado n�o puder ser identificado, ou o keyboardlayout est� ajustado
   para none no arquivo de configura��es do DOSBox, o layout padr�o dos EUA � usado.
   Nessa configura��o tente as teclas ao redor do "enter" para a tecla \ (barra invertida),
   e para a tecla : (dois pontos) use shift e as teclas entre "enter" e "l".


P: Estou com atraso no teclado.
R: Diminua a prioridade no arquivo de configura��es do DOSBox, por exemplo
   ajuste "priority=normal,normal". Voc� tamb�m pode tentar diminuir os ciclos
   (come�e com um ciclo fixo, como cycles=10000).


P: O cursor est� se movendo em apenas uma dire��o!
R: Veja se isso ainda acontece ao desabilitar a emula��o do joystick,
   coloque joysticktype=none na se��o [joystick] do arquivo de configura��es
   do DOSBox. Tente tamb�m desconectar qualquer joystick/gamepad.
   Se voc� quiser usar o joystick no jogo, tente ajustar timed=false
   e tenha certeza de calibrar o joystick (no seu sistema operacional e 
   no jogo ou no programa de instala��o do jogo).


P: O jogo/aplicativo roda muito lento!
R: Olhe a se��o "Como rodar jogos que necessitam mais recursos"
   para maiores informa��es.   


P: O jogo/aplicativo n�o chega a rodar/trava!
R: Olhe a Se��o 10: Solu��o de Problemas


P: O DOSBox pode danificar meu computador?
R: O DOSBox n�o pode danificar seu computador mais do que qualquer outro programa que
   necessita muitos recursos. Aumentando os ciclos n�o faz um overclock no seu CPU.
   Quando os ciclos est�o muito altos a performance do software executado no DOSBox cai.


P: Eu queria trocar o tamanho da mem�ria/velocidade da CPU/ems/soundblaster IRQ.
R: � poss�vel! Apenas crie um arquivo de configura��es: config -writeconf arquivodeconfigura��es.
   Abra seu editor de texto favorito e modifique as configura��es. Para iniciar o DOSBox
   com suas novas configura��es: dosbox -conf arquivodeconfigura��es
   Veja como funciona o comando config na Se��o 4 para mais detalhes.


P: Quais hardwares de som o DOSBox emula atualmente?
R: DOSBox emula v�rios dispositivos de som:
   - Som interno do PC
     Essa emula��o inclui o gerador de tons e v�rias formas de
     sa�da de som digital atrav�s da caixa de som interna.
   - Creative CMS/Gameblaster
     � a primeira placa feita pela Creative Labs(R). A localiza��o padr�o 
     da configura��o est� na porta 0x220. Nota-se que ao habilitar essa
     emula��o com a emula��o do Adlib poder� resultar em conflitos.
   - Tandy 3 voice
     A emula��o deste hardware � completa, com a exce��o do 
     canal de ru�do. Esse canal n�o � muito bem documentado,
     com isso, seja talvez a melhor op��o quanto a precis�o do som.
   - Tandy DAC
     A emula��o do Tandy DAC utiliza o emulador Soundblaster, ent�o
     esteja certo de que o soundblaster est� habilitado no arquivo de configura��es
     do DOSBox. O Tandy DAC � emulado apenas em n�vel de BIOS.
   - Adlib
     Esta emula��o � quase perfeita e inclui a habilidade do Adlib de 
     tocar quase todo som digitalizado.
   - SoundBlaster 16 / SoundBlaster Pro I & II / SoundBlaster I & II
     Por padr�o, o DOSBox fornece Soundblaster 16 em 16-bit de som est�reo. 
     � poss�vel selecionar uma vers�o diferente do SoundBlaster no arquivo de
     configura��es do DOSBox (Ver Programas internos: CONFIG).
   - Disney Soundsource
     Usando a porta da impressora, esse dispositivo apenas gera som digital.
   - Gravis Ultrasound
     A emula��o deste hardware est� quase completa, apesar da capacidade
     de tocar MIDI ter sido deixada de lado, pois o MPU-401
     come�ou a ser emulado em outro c�digo.
   - MPU-401
     A interface MIDI � tamb�m emulada. Esse m�todo de sa�da som
     somente funcionar� quando usado com um dispositivo de "General Midi" ou MT-32.


P: DOSBox trava no in�cio e eu estou rodando artes/cinem�tica.
R: Esse n�o � realmente um problema no DOSBox, mas a solu��o � colocar a
   vari�vel do ambiente SDL_AUDIODRIVER para alsa ou oss.


P: Estou tendo problemas para rodar um jogo feito com a Build Engine (Duke3D/Blood/Shadow Warrior).
R: Primeiramente, tente encontrar alguma portabilidade do jogo. Essas fornecer�o uma 
   melhor velocidade. Para consertar problemas gr�ficos que ocorrem no  
   DOSBox em altas resolu��es: Abra o arquivo de configura��es do DOSBox
   e procure por machine=svga_s3. Mude de svga_s3 para vesa_nolfb


P: Excelente LEIAME, mas eu ainda n�o entendi.
R: O f�rum "The Newbie's pictorial guide to DOSBox" localizado em 
   http://vogons.zetafleet.com/viewforum.php?f=39 poder� te ajudar.
   Tente tamb�m o wiki do DOSBox:
   http://www.dosbox.com/wiki/


Para mais perguntas, leia o restante desse LEIAME e/ou verifique o
site/f�rum:
http://www.dosbox.com



=======
3. Uso:
=======

Aqui voc� ter� uma vis�o ampla das op��es da linha de comando que voc�
pode dar ao DOSBox. Usu�rios do Windows devem executar o cmd.exe,
command.com, ou editar um atalho para o DOSBox para isso.
Essas op��es s�o v�lidas para qualquer sistema operacional,
menos quando indicado na descri��o da op��o:

dosbox [nome] [-exit] [-c comando] [-fullscreen] [-conf arquivodeconfig] 
       [-lang arquivodeidioma] [-machine tipodem�quina] [-noconsole]
       [-startmapper] [-noautoexec] [-securemode] 
       [-scaler escala | -forcescaler escala]
       [-version]
       
dosbox -version
dosbox -editconf programa
dosbox -opencaptures programa
dosbox -printconf
dosbox -eraseconf

  name   
        Se "nome" for um diret�rio, ele ser� montado como se fosse a unidade C:.
        Se "nome" for um execut�vel, ser� montado o diret�rio de "name" como
        a unidade C: e ent�o "nome" ser� executado.
    
  -exit  
        O DOSBox vai fechar automaticamente assim que o aplicativo "nome" for
        encerrado.

  -c comando
        Essa fun��o executa comandos antes de "nome" ser executado.
        V�rios comandos podem ser especificados, embora cada um
        deles deva ser iniciado com um "-c".
        Um comando pode ser: um Programa Interno, um comando do pr�prio
        DOS ou um execut�vel que esteja em uma unidade emulada.

  -fullscreen
        Inicia o DOSBox j� no modo de tela cheia.

  -conf arquivodeconfig
        Abre o DOSBox com as op��es que foram especificadas em "arquivodeconfig".
        V�rias op��es -conf podem ser usadas.
        Para mais informa��es, veja a Se��o 11.

  -lang arquivodeidioma
        Executa o DOSBox usando o idioma programado em "arquivodeidioma".

  -machine tipodem�quina
        Faz com que o DOSBox emule um determinado tipo de m�quina. Algumas
        das op��es s�o: hercules, cga, pcjr, tandy, svga_s3 (padr�o) assim
        como os chipsets svga adicionais, que est�o listadas no arquivo de
        configura��es do DOSBox.
        O svga_s3 tamb�m permite uma emula��o vesa.
        Para alguns efeitos especiais do vga, somente o tipo de m�quina vgaonly
        poder� ser usado. Perceba que essa op��o ir� desabilitar as capacidades
        do svga, e poder� ficar (consideravelmente) mais lento devido � melhor
        precis�o na emula��o.
        A fun��o machinetype afeta tanto as placas de v�deo como as placas de
        som dispon�veis.

  -noconsole (Apenas Windows)
        Inicia o DOSBox sem mostrar a janela do console. O log de sa�da ser�
        redirecionado para stdout.txt e stderr.txt


  -startmapper
        Inicia o mapeador de teclas logo no inicio. Essa fun��o � �til para pessoas
        que possuam algum tipo de problema no seu teclado.

  -noautoexec
        Esse comando "pula" a se��o [autoexec] do arquivo de configura��es
        que foi carregado.

  -securemode
        Possui a mesma fun��o do -noautoexec, por�m ele adiciona
        config.com -securemode no final do AUTOEXEC.BAT (o que, em troca,
        ignora quaisquer mudan�as que foram feitas em rela��o � como as
        unidades s�o emuladas, dentro do DOSBox).

  -scaler escala
        Usa a escala que foi especificada em "escala". Abra o arquivo de
        configura��es do DOSBox para verificar quais as escalas dispon�veis.

  -forcescaler escala
        Fun��o parecida com o par�metro -scaler, mas esse for�a o
        uso da escala determinada, mesmo que ela n�o seja necessariamente
        adequada.

  -version
        Mostra informa��es sobre a vers�o e fecha o DOSBox.
        �til para a cria��o de frontends.

  -editconf programa
        Chama "programa" como o primeiro par�metro do arquivo de configura��es.
        Voc� pode especificar esse comando mais de uma vez. Nesse caso,
        ele ir� se dirigir ao segundo programa, caso o primeiro falhe na
        execu��o.

  -opencaptures programa
        Chama "programa" como o primeiro par�metro a localiza��o
        da pasta de captura.
  
  -printconf
        Imprime a localiza��o do arquivo de configura��es padr�o.

  -eraseconf
        Exclui o arquivo de configura��es padr�o.

Nota: Se por acaso o nome/comando/arquivo de configura��es/arquivo de
      idioma possuir algum espa�o, ponha todo o nome/comando/arquivo
      de configura��es/arquivo de idioma entre aspas:
      ("comando ou nome do arquivo"). Se voc� quiser usar aspas dentro
      das pr�prias aspas (provavelmente quando for usar -c e mount):
      Usu�rios do Windows e OS/2 podem usar aspas simples dentro de aspas
      duplas.
      Outros usu�rios poder�o usar aspas com uma barra (\") dentro das aspas duplas.
      Windows: -c "mount c 'c:\program files\'" 
      Linux: -c "mount c \"/tmp/name with space\""

Aqui vai um exemplo:

dosbox c:\atlantis\atlantis.exe -c "MOUNT D C:\SAVES"
  Isso vai montar c:\atlantis como c:\ e executar atlantis.exe.
  Antes dele fazer isso ele vai montar C:\SAVES como sendo a unidade D.

No Windows, voc� tamb�m pode arrastar os diret�rios/arquivos diretamente
para o execut�vel do DOSBox.



======================
4. Programas Internos:
======================

O DOSBox suporta a maioria dos comandos do DOS encontrados no command.com.
Para ver uma lista dos programas internos digite "HELP" no prompt de comando.

Al�m desses, os seguintes comandos podem ser usados: 

MOUNT "Letra da Unidade emulada" "Unidade Real ou Diret�rio" 
      [-t tipo] [-aspi] [-ioctl] [-noioctl] [-usecd n�mero] [-size tam_unidade] 
      [-label r�tulo] [-freesize tam_em_mb]
      [-freesize tam_em_kb (disquetes)]
MOUNT -cd
MOUNT -u "Letra da Unidade emulada"

  Programa para montar diret�rios locais como unidades dentro do DOSBox.

  "Letra da Unidade emulada"
        A letra da unidade dentro do DOSBox (ex. C).

  "Letra Real da Unidade (geralmente para CD-ROMs no Windows) ou Diret�rio"
        O diret�rio local que voc� deseja acessar com o DOSBox.

  -t tipo
        Tipo da unidade a ser montada. Os suportados s�o: dir (padr�o),
        floppy (disquete), cdrom.

  -size tam_unidade
        Ajusta o tamanho da unidade, onde tam_unidade � pode ser
        "bps,spc,tcl,fcl":
           bps: bytes por setor. Por padr�o, 512 para unidades convencionais
                e 2048 para unidades de CD-ROM
           spc: setores por cluster, geralmente entre 1 e 127
           tcl: total de clusters, entre 1 e 65534
           fcl: total de clusters livres, entre 1 e tcl

  -freesize tam_em_mb | tam_em_kb
        Ajusta a quantidade de espa�o dispon�vel na unidade em megabytes
        (unidades convencionais) ou kilobytes (unidades de disquete).
        Essa � uma vers�o mais simples de -size.	

  -label r�tulo
        Ajusta o nome da unidade para "r�tulo". � necess�rio em alguns
        sistemas caso o r�tulo do CD-ROM n�o seja lido corretamente (�til quando
        o programa n�o consegue encontrar seu CD-ROM). Se o r�tulo n�o for especificado
        ou o suporte de baixo n�vel n�o for selecionado (isto �, omitir os par�metros
        -usecd # e/ou -aspi, ou especificando -noioctl): 
          No Windows: o r�tulo ser� lido da "Unidade Real".
          No Linux: o r�tulo ser� NO_LABEL.

        Se voc� especificar um r�tulo, esse r�tulo ser� mantido enquanto a unidade
        estiver montada. Ele n�o ser� atualizado em caso de mudan�a de CD, etc !!

  -aspi
        For�a o uso da camada aspi. S� funciona montando a unidade de CD-ROM 
        em ambiente Windows que possuam a Camada ASPI.

  -ioctl (sele��o autom�tica da interface de CDs de �udio)
  -ioctl_dx (extra��o de �udio digital usado em CDs de �udio)
  -ioctl_dio (chamadas ioctl usadas em CDs de �udio)
  -ioctl_mci (MCI usado em CDs de �udio)
        For�a o uso de comandos ioctl. S� � v�lido se a unidade de CD-ROM for montada 
        no Windows que suporte esses comandos (Win2000/XP/NT).
        As diferentes op��es diferem apenas na maneira de como o CD de �udio � manuseado.
        Tenha prefer�ncia por -ioctl_dio (requer menor processamento), mas ele pode n�o
        funcionar em todos os sistemas, ent�o, -ioctl_dx (ou -ioctl_mci) devem ser usados.

  -noioctl
        For�a o uso da camada SDL do CD-ROM. V�lido para qualquer sistema.

  -usecd n�mero
        V�lido para qualquer sistema, no Windows o par�metro -noioctl deve
        estar presente para se poder fazer o uso do par�metro -usecd.
        Ativa a sele��o da unidade que dever� ser usada pelo SDL. Use isso se
        a unidade de CD-ROM n�o existir ou n�o estiver montada enquanto usa
        a interface de CD-ROM do SDL. "n�mero" pode ser encontrado atrav�s de "MOUNT -cd".

  -cd
        Exibe todas as unidades de CD-ROM detectadas pelo SDL e seus respectivos
        n�meros. Veja mais informa��es na se��o -usecd acima.

  -u
        Desmonta a unidade. N�o funciona para a Z:\.

  Observa��o: � poss�vel montar um diret�rio local como unidade de CD-ROM. 
              Sendo assim, n�o existir� suporte de hardware.

  Basicamente o MOUNT permite voc� conectar o hardware do seu computador
  ao PC emulado pelo DOSBox.
  Ent�o, "MOUNT C C:\JOGOS" diz ao DOSBox para usar a pasta C:\JOGOS como a unidade C:
  dentro do DOSBox. Ele tamb�m permite que voc� mude a letra da unidade para
  programas que necessitam unidades com letras espec�ficas.
  
  Por exemplo: "Touche: Adventures of The Fifth Musketeer" deve ser executado
  na unidade C:. Usando o DOSBox juntamente com seu comando mount, voc� pode
  fazer com que o jogo pense que ele est� na unidade C, enquanto ele est� em
  qualquer outro lugar que voc� queira colocar. Por exemplo, se o jogo estiver
  em D:\JOGOSANTIGOS\TOUCHE, o comando "MOUNT C D:\JOGOSANTIGOS" permitir� voc�
  executar o Touche a partir da unidade D.

  Montar a sua unidade C inteira com "MOUNT C C:\" N�O � recomendado! O mesmo
  � v�lido ao montar a raiz de qualquer outra unidade, exceto para CD-ROMs (devido
  sua natureza de somente leitura). Se n�o, caso voc� ou o DOSBox fa�a algum erro,
  voc� poder� perder todos os seus arquivos.
  � recomendado colocar todos os seus aplicativos/jogos em um subdiret�rio e mont�-lo.

  Exemplos gerais de MOUNT:
    1. Para montar c:\DirX como um disquete : 
         mount a c:\DirX -t floppy
    2. Para montar a unidade de CD-ROM E: do sistema como unidade de CD-ROM D: no DOSBox:
         mount d e:\ -t cdrom
    3. Para montar a unidade de CD-ROM do sistema como pontodemontagem /m�dia/cdrom como
       unidade de CD-ROM D: no DOSBox:
         mount d /media/cdrom -t cdrom -usecd 0
    4. Para montar uma unidade com ~870 MB de espa�o dispon�vel (vers�o simples):
         mount c d:\ -freesize 870
    5. Para montar uma unidade com ~870 MB de espa�o dispon�vel (modo avan�ado, controle total):
         mount c d:\ -size 512,127,16513,13500
    6. Para montar /home/user/dirY como unidade C no DOSBox:
         mount c /home/user/dirY
    7. Para montar o diret�rio onde o DOSBox foi iniciado como D no DOSBox:
         mount d .
         (note o . que representa a pasta onde o DOSBox foi iniciado)


MEM
  Programa para mostrar a quantidade de mem�ria dispon�vel.


VER
VER set vers�o_maior [vers�o_menor]
  Mostra a vers�o atual do DOSBox e a vers�o relatada do DOS
  (uso sem par�metros).
  Altera a vers�o relatada do DOS com o par�metro "set",
  por exemplo: escreva "VER set 6 22" para que a vers�o relatada
  do DOS pelo DOSBox seja a 6.22.


CONFIG -writeconf localdoarquivo
CONFIG -writelang localdoarquivo
CONFIG -securemode
CONFIG -set "se��o propriedade=valor"
CONFIG -get "se��o propriedade"

  O CONFIG pode ser usado para alterar ou obter informa��es de v�rias configura��es do DOSBox 
  durante sua execu��o. Ele pode salvar as configura��es atuais e os textos do idioma para um
  arquivo no disco r�gido. Informa��es sobre todas as poss�veis se��es e propriedades podem ser
  encontradas na Se��o 11 (O Arquivo de Configura��es).

  -writeconf localdoarquivo
       Escreve as atuais configura��es do DOSBox em um arquivo. "localdoarquivo" �
       um local do seu disco r�gido, n�o uma unidade montada no DOSBox. 
       O arquivo de configura��es cont�m v�rios ajustes do DOSBox: 
       a quantidade de mem�ria emulada, as placas de som emuladas dentre muitas outras
       coisas. Ele tamb�m permite acesso ao AUTOEXEC.BAT.
       Veja a Se��o 11 (O Arquivo de Configura��es) para maiores informa��es.

  -writelang localdoarquivo
       Escreve os textos do idioma atual em um arquivo. "localdoarquivo" �
       um local do seu disco r�gido, n�o uma unidade montada no DOSBox.
       O arquivo de idioma controla toda a sa�da vis�vel dos comandos internos
       do DOSBox e do DOS interno.

  -securemode
       Alterna o DOSBox para um modo mais seguro. Nesse modo, os comandos internos
       MOUNT, IMGMOUNT e BOOT n�o funcionar�o. Tamb�m n�o � poss�vel criar um novo
       arquivo de configura��es ou de idiomas enquanto estiver nesse modo.
       (Aten��o: a �nica maneira de sair desse modo � reiniciando o DOSBox.)

  -set "se��o propriedade=valor"
       O CONFIG tentar� ajustar um novo valor para uma certa propriedade. Atualmente
       o CONFIG n�o tem como informar se o comando foi conclu�do com sucesso ou n�o.

  -get "se��o propriedade"
       O valor atual de uma determinada propriedade � relatada e gravada na vari�vel
       ambiente %CONFIG%. Isso pode ser usado para gravar um determinado valor quando
       estiver usando arquivos batch.

  Ambos "-set" e "-get" funcionam a partir de arquivos batch e podem ser usados para
  ajustar suas pr�prias configura��es para cada jogo.
  
  Exemplos:
    1. Para criar um arquivo de configura��es no diret�rio atual:
        config -writeconf dosbox.conf
    2. Para ajustar os ciclos da CPU em 10000:
        config -set "cpu cycles=10000"
    3. Para desligar a emula��o da mem�ria ems:
        config -set "dos ems=off"
    4. Para verificar qual n�cleo da CPU est� sendo usada.
        config -get "cpu core"


LOADFIX [-tamanho] [programa] [par�metros-do-programa]
LOADFIX -f
  Programa usado para reduzir a quantidade de mem�ria convencional dispon�vel.
  �til para programas antigos que n�o esperam que muita mem�ria esteja dispon�vel. 

  -tamanho	        
        n�mero de kilobytes para "comer" (reduzir), padr�o = 64kb
  
  -f
        libera todas as mem�rias alocadas anteriormente
  
  Exemplos:
    1. Para iniciar mm2.exe e alocar uma mem�ria de 64kb 
       (mm2 ter� menos 64 kb de mem�ria dispon�vel) :
       loadfix mm2
    2. Para iniciar mm2.exe e alocar uma mem�ria de 32kb :
       loadfix -32 mm2
    3. Para liberar as mem�rias anteriormente alocadas :
       loadfix -f


RESCAN
  Faz o DOSBox reanalizar a estrutura do diret�rio. �til caso voc� tenha
  alterado algo, em uma das unidades montadas, fora do DOSBox. (CTRL - F4 � um atalho!)
  

MIXER
  Faz o DOSBox exibir suas configura��es atuais do volume. 
  Logo abaixo est� como alter�-las:
  
  mixer canal esquerdo:direito [/NOSHOW] [/LISTMIDI]
  
  canal
      S�o op��es poss�veis: MASTER, DISNEY, SPKR, GUS, SB, FM [, CDAUDIO].
      CDAUDIO est� dispon�vel apenas se a interface do CD-ROM com controle
      de volume estiver ativada (imagem do CD, ioctl_dx).
  
  esquerdo:direito
      Os n�veis de volume em porcentagens. Se voc� colocar um D na frente o
      valor ser� em decib�is (Exemplo: mixer gus d-10).
  
  /NOSHOW
      Previne o DOSBox de mostrar o resultado caso voc� tenha ajustado algum
      dos n�veis de volume.

  /LISTMIDI
      Lista os dispositivos MIDI dispon�veis no seu PC (Windows). Para escolher
      um dispositivo que n�o seja o mapeador de midi padr�o do Windows, adicione
      uma linha 'midiconfig=id' na se��o [midi] no arquivo de configura��es,
      onde 'id' � o n�mero do dispositivo listado pelo LISTMIDI.


IMGMOUNT
  � um utilit�rio para montar imagens de disco ou de CD-ROM dentro do DOSBox.
  
  IMGMOUNT UNIDADE [arquivo_imagem] -t [tipo_imagem] -fs [formato_imagem] 
            -size [setoresporbyte, setoresporcabe�a, cabe�as, cilindros]
  IMGMOUNT UNIDADE [arquivodeimagem1, .. ,arquivodeimagemN] -t iso -fs iso 

  arquivo_imagem
      Local do arquivo de imagem para montar no DOSBox. O local pode
      ser uma unidade montada dentro do DOSBox, ou o seu disco r�gido real.
      Tamb�m � poss�vel montar imagens de CD-ROM (ISOs ou CUE/BIN), caso
      voc� necessite trocar o CD em um determinado momento especifique
      todas as imagens em sucess�o (veja pr�ximo t�pico).
      Os pares CUE/BIN s�o melhores op��es para imagens de CD-ROM pois elas
      guardam informa��es sobre faixas de �udio em compara��o com ISOs
      (que armazenam apenas dados). Para montar um par CUE/BIN sempre
      especifique a lista CUE.
      
  arquivodeimagem1, .. ,arquivodeimagemN
      Local dos arquivos de imagem para montar no DOSBox. S� � permitido
      especificar um n�mero de imagens para imagens de CD-ROM. Os CDs
      podem ser trocados, a qualquer momento, com CTRL-F4. Isso � necess�rio
      para jogos que usam v�rios CD-ROMs e que precisem, em um determinado
      ponto do jogo, que os CDs sejam trocados.
   
  -t 
      A seguir est�o os tipos de imagens v�lidas:
        floppy: Especifica uma imagem de disquete. O DOSBox automaticamente
                identificar� a geometria do disco (360K, 1.2MB, 720K, 1.44MB, etc).
        iso:    Especifica uma imagem de CD-ROM. A geometria � autom�tica e
                � ajustada para seu tamanho. Pode ser uma iso ou um par cue/bin.
        hdd:    Especifica uma imagem de disco r�gido. A geometria CHS apropriada
                deve ser colocada para que isso funcione.

  -fs 
      A seguir est�o os sistemas de arquivos v�lidos:
        iso:  Especifica o formato CD-ROM ISO 9660.
        fat:  Especifica que a imagem usa o sistema de arquivos FAT. O DOSBox tentar�
              montar essa imagem como uma unidade no DOSBox e fazer com que seus arquivos
              estejam dispon�veis dentro do DOSBox.
        none: O DOSBox n�o ler� o sistema de arquivos do disco.
              � �til caso voc� precise formatar ou caso voc� queira iniciar
              o disco atrav�s do comando BOOT. Quando o sistema de arquivo "none" 
              � usado, voc� deve especificar o n�mero da unidade (2 ou 3, 
              onde 2 = master, 3 = slave) ao inv�s da letra da unidade. 
              Por exemplo, para montar uma imagem de 70MB como uma unidade slave, 
              voc� dever� escrever (sem as aspas):
                "imgmount 3 d:\teste.img -size 512,63,16,142 -fs none" 
                Compare isso com o mount para ser poss�vel acessar a unidade
                pelo DOSBox, que deveria ser: 
                "imgmount e: d:\teste.img -size 512,63,16,142"

  -size 
     Os Cilindros, Cabe�as e Setores (CHS) da unidade.
     Necess�rio para montar imagens de disco r�gido.
     
  Um exemplo de como montar imagens de CD-ROM:
    1a. mount c /tmp
    1b. imgmount d c:\minhaiso.iso -t iso
    ou (que funciona igual):
    2. imgmount d /tmp/minhaiso.iso -t iso


BOOT
  O BOOT inicia imagens de disquete ou de disco r�gido independente da
  emula��o do sistema operacional oferecido pelo DOSBox. Isso permite
  jogar boot�veis de disquetes ou iniciar outros sistemas operacionais
  dentro do DOSBox. Se o sistema emulado for PCjr (machine=pcjr) o
  comando de boot pode ser usado para carregar cartuchos PCjr (.jrc). 

  BOOT [diskimg1.img diskimg2.img .. diskimgN.img] [-l letradaunidade]
  BOOT [cart.jrc]  (apenas PCjr)

  diskimgN.img 
     Isso � n�mero de imagens de disquete que voc� deseja que sejam montadas
     depois do DOSBox iniciar a letra da unidade especificada.
     Para alternar entre as imagens, aperte CTRL-F4 para mudar do disco atual
     para o disco seguinte da lista. Quando chegar ao �ltimo disco da lista
     o pr�ximo ser� o primeiro.

  [-l letradaunidade]
     Esse par�metro permite que voc� especifique de qual unidade ser� inicializado.
     A unidade padr�o � A:, a unidade de disquete. Voc� tamb�m pode iniciar uma
     imagem de disco r�gido montada como "master" ao especificar "-l C" 
     (sem as aspas) ou como "slave" ao especificar "-l D"
     
   cart.jrc (apenas PCjr)
     Quando a emula��o do PCjr est� ativada, cartuchos podem ser carregados com
     o comando BOOT. O suporte ainda � limitado.


IPX

  � preciso ativar a rede IPX no arquivo de configura��es do DOSBox.

  Toda a rede IPX � gerenciada pelo programa interno do DOSBox,
  IPXNET. Para obter ajuda sobre a rede IPX dentro do DOSBox, digite
  "IPXNET HELP" (sem aspas) e o programa listar� os comandos com uma
  documenta��o relevante.

  Em rela��o a como ajustar uma rede, um sistema precisa ser o servidor.
  Para faz�-lo, digite "IPXNET STARTSERVER" (sem as aspas) numa sess�o do
  DOSBox. A sess�o onde o DOSBox est� sendo servidor automaticamente
  se adicionar� para a rede virtual IPX. Para cada computador adicional
  que dever� fazer parte da rede virtual IPX, voc� dever� digitar
  "IPXNET CONNECT <nome do computador host ou IP>". 
  Por exemplo, se o servidor estiver no joao.dosbox.com, voc� dever� digitar
  "IPXNET CONNECT joao.dosbox.com" em cada sistema que n�o seja o servidor. 
  
  Para jogar os jogos que precisam do Netbios, o arquivo NETBIOS.EXE da Novell
  � necess�rio. Estabele�a a conex�o IPX como explicado acima, e ent�o
  execute o "netbios.exe". 

  A seguir est�o as refer�ncias do comando IPXNET: 

  IPXNET CONNECT 

     IPXNET CONNECT abre uma conex�o e cria um t�nel com o servidor IPX
     rodando em outra sess�o do DOSBox. O par�metro "endere�o" especifica
     o endere�o de IP ou nome do host do computador servidor. Voc� tamb�m
     pode especificar qual a porta UDP que ser� usada. Por padr�o, o IPXNET
     usa a porta 213 - que � a porta IANA associada para t�neis IPX - para
     sua conex�o. 

     A sintaxe para o IPXNET CONNECT �: 
     IPXNET CONNECT endere�o <porta> 

  IPXNET DISCONNECT 

     IPXNET DISCONNECT fecha o t�nel da conex�o com o servidor IPX. 

     A sintaxe para o IPXNET DISCONNECT �: 
     IPXNET DISCONNECT 

  IPXNET STARTSERVER 

     IPXNET STARTSERVER inicia um servidor IPX nessa sess�o do DOSBox.
     Por padr�o, o servidor aceitar� conex�es na porta 213 UDP,
     mas isso pode ser alterado. Uma vez que o servidor for iniciado, o
     DOSBox automaticamente iniciar� uma conex�o com o cliente atrav�s do
     t�nel do servidor IPX.

     A sintaxe para o IPXNET STARTSERVER �:
     IPXNET STARTSERVER <porta>

     Se o servidor estiver por tr�s de um router, a porta UDP <porta> dever� ser
     encaminhada �quele computador (fazer um port-fowarding).

     Nos sistemas Linux/Unix-based: N�meros menores que 1023 para as portas s�
     podem ser usadas com privil�gios de root. Use portas maiores que 1023
     nesses sistemas.

  IPXNET STOPSERVER

     IPXNET STOPSERVER fecha o t�nel do servidor IPX rodando nessa sess�o do
     DOSBox. Um certo cuidado deve ser tomado; assegure-se que todas as outras
     conex�es tenham sido terminadas antes, pois deixar de ser um servidor poder�
     travar as outras m�quinas que ainda est�o usando o t�nel de conex�o com o
     servidor.

     A sintaxe para o IPXNET STOPSERVER �: 
     IPXNET STOPSERVER 

  IPXNET PING

     IPXNET PING emite um pedido de ping atrav�s do t�nel da rede IPX. 
     Em resposta, todos os outros computadores conectados responder�o ao ping
     e reportar�o o tempo que levou para receber e enviar a mensagem de ping. 

     A sintaxe para o IPXNET PING �: 
     IPXNET PING

  IPXNET STATUS

     IPXNET STATUS mostra o estado atual do t�nel da rede IPX da sess�o
     atual do DOSBox. Para ver a lista de todos os computadores conectados
     na rede use o comando IPXNET PING.

     A sintaxe para o IPXNET STATUS �: 
     IPXNET STATUS 


KEYB [c�digodeidioma [codepage [arquivodecodepage]]]
  Altera o layout do teclado. Para informa��es detalhadas sobre os layouts
  do teclado veja a Se��o 7.

  [c�digodeidioma] s�o os caracteres que especificam o layout do teclado
     que ser� usado. Geralmente s�o 2 caracteres mas, em casos especiais, mais.
     Exemplos s�o GK (Gr�cia) ou IT (It�lia).

  [codepage] � o n�mero da codepage a ser usada. O layout do teclado deve
     apresentar suporte para a codepage especificada, caso contr�rio o
     carregamento layout falhar�.
     Se nenhuma codepage for especificada, uma codepage apropriada para o
     layout escolhido � automaticamente selecionado.

  [arquivodecodepage] pode ser usado para carregar codepages que ainda n�o est�o
     compiladas no DOSBox. S� � necess�rio quando o DOSBox n�o encontra a codepage.


  Exemplos:
    1. Para carregar o layout do teclado alem�o (automaticamente usa a codepage 858):
         keyb gr
    2. Para carregar o layout do teclado russo com codepage 866:
         keyb ru 866
       Para escrever os caracteres russos aperte ALT+SHIFT DIREITO.
    3. Para carregar o layout do teclado franc�s com codepage 850 (onde a
       codepage est� no arquivo EGACPI.DAT):
         keyb fr 850 EGACPI.DAT
    4. Para carregar a codepage 858 (sem o layout do teclado):
         keyb none 858
       Isso pode ser usado para mudar a codepage do utilit�rio FreeDOS keyb2.
    5. Para exibir a codepage atual e, se carregado, o layout do teclado:
         keyb



Para maiores informa��es, use o switch /? na linha de comando com os programas.



====================
5. Teclas Especiais:
====================


ALT-ENTER   : Alterna entre o modo janela e tela-cheia.
ALT-PAUSE   : Pausa o DOSBox. (aperte ALT-PAUSE novamente para continuar)
CTRL-F1     : Executa o mapeador de teclas.
CTRL-F4     : Alterna entre as imagens dos discos montadas.
              Atualiza a cache dos diret�rios de todas as unidades.            
CTRL-ALT-F5 : Inicia/Para a grava��o de v�deo � um arquivo. (formato AVI)
CTRL-F5     : Captura e salva a imagem da tela. (formato PNG)
CTRL-F6     : Inicia/Para a grava��o do �udio � um arquivo wave.
CTRL-ALT-F7 : Inicia/Para a grava��o de comandos OPL. (formato DRO)
CTRL-ALT-F8 : Inicia/Para a grava��o de comandos MIDI sem processar.
CTRL-F7     : Diminui o frameskip.
CTRL-F8     : Aumenta o frameskip.
CTRL-F9     : Encerra o DOSBox.
CTRL-F10    : Captura/Libera o mouse.
CTRL-F11    : Desacelera a emula��o (Diminui os ciclos do DOSBox).
CTRL-F12    : Acelera a emula��o (Aumenta os ciclos do DOSBox).
ALT-F12     : Desativa o limitador de velocidade (Bot�o turbo).


(NOTA: Uma vez que voc� ultrapassar o m�ximo de ciclos que o computador
suporta, a velocidade come�ar� a diminuir. Esse m�ximo varia para cada
computador.)

Essas s�o atribui��es de teclas padr�o. Elas podem ser alteradas atrav�s
do mapeador de teclas. (Veja se��o 6: Mapeador de teclas)

Arquivos salvos/gravados podem ser encontrados em diret�rio_atual/capture 
(isso pode ser alterado no arquivo de configura��es do DOSBox). 
Essa pasta dever� existir antes do DOSBox ser iniciado, se n�o nada ser�
salvo/gravado ! 



======================
6. Mapeador de Teclas:
======================

Quando o mapeador de teclas do DOSBox � iniciado (Pressionando CTRL+F1 ou
escrevendo o par�metro -startmapper na linha de comando do execut�vel)
na tela ser� exibido um teclado virtual e um joystick virtual.

Esses dispositivos virtuais corresponder�o �s teclas e eventos que o
DOSBox ir� relatar para as aplica��es DOS (que est� sendo emulado).
Quando voc� clicar em um bot�o com o mouse, no canto inferior esquerdo
aparecer� o evento a que est� associado (EVENT) e com que tecla est�
atualmente atribu�da.

Event: EVENT
BIND: BIND
                        Add   Del
mod1  hold                    Next
mod2
mod3


EVENT
    A tecla ou dire��o/bot�o do joystick que ser� relatada pelo DOSBox
    �s aplica��es DOS.
BIND
    Que tecla do seu teclado ou bot�o/dire��o do seu joystick (os de verdade)
    (o mostrado pelo SDL) que est�o associadas ao EVENT.

mod1,2,3 
    Modificadores. Essas s�o as teclas que tamb�m dever�o ser pressionadas
    enquanto voc� aperta a tecla associada (BIND). mod1 = CTRL e mod2 = ALT.
    Elas normalmente s� s�o usadas quando voc� quer mudar as teclas especiais
    do DOSBox.
Add 
    Adiciona uma nova BIND ao EVENT. Basicamente adiciona uma tecla do seu
    teclado ou um bot�o/dire��o do seu joystick que ir� resultar num EVENT
    no DOSBox.
Del 
    Apaga o BIND associado a esse EVENT. Se o EVENT n�o possui nenhum BIND,
    ent�o n�o � poss�vel ativ�-lo no DOSBox (ou seja, n�o h� como usar
    a tecla ou usar a respectiva a��o no joystick).
Next
    Mostra quais as BINDS (teclas) est�o atribu�das ao determinado EVENT.


Exemplo:
P1. Voc� quer que o X do seu teclado digite um Z no DOSBox.
    R. Clique no Z do mapeador de teclas. Clique em "Add". Agora
       pressione o X do seu teclado.

P2. Se voc� clicar em "Next" algumas vezes, ver� que o Z do seu teclado
    tamb�m faz aparecer um Z no DOSBox.
    R. Sendo assim, selecione o Z novamente e clique em "Next" at� que o BIND
       seja o Z do seu teclado. Agora clique em "Del".

P3. Se voc� apertar X no DOSBox perceber� o aparecimento de XZ.
    R. O X do seu teclado tamb�m est� mapeado como X!! Clique no X do mapeador
    de teclas e procure com o "Next" at� que voc� ache o X mapeado. Ap�s isso,
    clique em "Del".


Exemplos sobre o remapeamento do joystick:
  Voc� tem um joystick conectado, que funciona muito bem com o DOSBox, mas voc�
  quer jogar um jogo, que s� aceita o teclado, com o joystick (assume-se que o
  jogo seja controlado pelas setinhas do teclado):
    1. Inicie o mapeador, clique em uma das setas localizadas no
       centro-esquerdo da tela (logo acima dos bot�es Mod1/Mod2).
       O EVENT deve ser key_left. Agora clique em Add e mova o seu joystick na
       respectiva dire��o. Com isso, voc� deve ter adicionado uma BIND ao evento.
    2. Repita os passos anteriores para a adi��o das tr�s dire��es restantes.
       � claro que os bot�es do joystick tamb�m podem ser remapeados (atirar,
       pular, etc.)
    3. Clique em Save, depois em Exit e teste sua nova configura��o com algum jogo.

  Voc� quer inverter o eixo y do joystick porque alguns simuladores de v�o usam
  esses movimentos de uma maneira que voc� n�o gosta e n�o � configur�vel no jogo:
    1. Inicie o mapeador e clique no Y- no campo superior direito
       (essa op��o � para o primeiro joystick, caso voc� tenha dois deles
       conectados), ou no campo logo abaixo do anterior (essa op��o � para
       o segundo joystick ou, caso voc� s� tenha um encaixado, o segundo
       eixo se inverte).
       O EVENT dever� ser jaxis_0_1- (ou jaxis_1_1-).
    2. Clique em Del para remover a BIND atual, e depois clique em Add e mova o
       seu joystick para baixo. Feito isso, uma nova bind dever� criada.
    3. Repita essa opera��o para configurar o Y+, salve sua configura��o e
       teste-a em algum jogo.



Se voc� modificar o mapeamento padr�o, poder� salvar suas altera��es clicando
em "Save". O DOSBox vai salvar esse mapeamento no local especificado no arquivo
de configura��es (op��o mapperfile=). Na inicializa��o, o DOSBox vai
carregar o seu arquivo de mapeamento, se o mesmo estiver preenchido
no arquivo de configura��es.



=====================
7. Layout do teclado:
=====================

Para mudar o layout do teclado basta preencher a configura��o "keyboardlayout"
na se��o [dos] do arquivo de configura��es do DOSBox ou utilizar o programa
interno keyb.com do DOSBox. Ambos aceitam c�digos de idioma (veja abaixo), mas
somente � poss�vel especificar uma codepage customizada atrav�s do programa
keyb.com.

A op��o "keyboardlayout=auto" atualmente s� funciona em ambiente Windows.
O layout � escolhido baseado no qual o sistema operacional est� usando.

Mudando o Layout
  Por padr�o, o DOSBox j� suporta um certo n�mero de layouts de teclado
  e codepages. Nesse caso, apenas o identificador do layout precisa ser
  especificado (ex: keyboardlayout=br no arquivo de configura��o do
  DOSBox, ou escrevendo "keyb br" no prompt de comando do DOSBox).
  
  Alguns layouts de teclado (por exemplo, o layout GK codepage 869 e o layout RU
  codepage 808) t�m suporte para layout duplo que pode ser ativado pressionando
  ALT ESQUERDO+SHIFT DIREITO e desativado usando ALT ESQUERDO+SHIFT ESQUERDO.

Arquivos externos suportados
  Os arquivos .kl do FreeDOS s�o suportados (arquivos de layout do FreeDOS keyb2)
  assim como suas bibliotecas, (keyboard.sys/keybrd.sys/keybrd3.sys) que consistem
  na uni�o dos arquivos .kl existentes.
  Caso os layouts integrados do DOSBox n�o funcionem, acesse o site
  http://projects.freedos.net/keyb/ para obter layouts de teclado precompilados
  com suas devidas atualiza��es, caso estejam dispon�veis.

  Os arquivos .CPI (Arquivos MS-DOS e de codepages compat�veis) e .CPX (Arquivos de
  codepage UPX-condesadas do FreeDOS) podem ser usados. Algumas codepages j� foram
  pr�-compiladas no DOSBox. N�o h� necessidade de se preocupar com arquivo de
  codepage externo. Se voc� necessitar de um arquivo de codepage diferente
  (ou customizado), copie ele para o diret�rio do arquivo de configura��o do DOSBox
  para que o DOSBox possa acess�-lo.

  Layouts adicionais podem ser aplicados copiando o arquivo .kl para o
  diret�rio do arquivo de configura��es do DOSBox e usando a primeira parte do
  nome do arquivo como o c�digo do idioma.
  Exemplo: Para o arquivo UZ.KL (layout de teclado para o Uzbequist�o), especifique
           "keyboardlayout=uz" no arquivo de configura��es do DOSBox.
  A integra��o das bibliotecas de layouts de teclado (ex: keybrd2.sys) funciona da
  mesma maneira.


Observe que o layout do teclado faz com que os caracteres estrangeiros apare�am, mas
atualmente N�O h� suporte para eles nos nomes dos arquivos. Evite-os tanto no DOSBox
quanto nos arquivos do seu computador que est�o sendo acessados pelo DOSBox.



===================================
8. Fun��o Multi-Jogador via Serial:
===================================

O DOSBox pode emular cabos seriais e nullmodem atrav�s da rede local e da internet.
Essa op��o pode ser configurada atrav�s da se��o "Porta Serial" no arquivo de
configura��o do DOSBox.

Para estabelecer uma conex�o Null Modem, uma pessoa dever� ser o servidor
e o outra dever� ser o cliente.

Quem decidir ser o servidor ter� que ajustar o arquivo de configura��o
do DOSBox, da seguinte maneira:
   serial1=nullmodem

E o arquivo de configura��o do DOSBox no cliente dever� ficar assim:
   serial1=nullmodem server:<IP ou o nome do servidor>

Agora inicie o jogo e escolha, na COM1, uma dentre essas op��es de multiplayer:
Nullmodem / Cabo Serial / J� conectado. Lembre-se de deixar as baudrates iguais
nos dois computadores.

Al�m disso, outros par�metros podem ser ajustados para melhorar a conex�o
do Null Modem. Estes s�o os par�metros dispon�veis:

 * port:         - N�mero da porta TCP. Padr�o: 23
 * rxdelay:      - Em quanto tempo (milissegundos) os dados recebidos ser�o atrasados,
                   caso a interface ainda n�o esteja pronta. Aumente esse valor
                   se voc� encontrar erros na Janela de Status do DOSBox. Padr�o: 100
 * txdelay:      - Quanto tempo levar para que as informa��es sejam
                   acumuladas, antes de serem enviadas de uma vez em um pacote.
                   Padr�o:12
                   (Isso diminui a sobrecarga do servidor)
 * server:       - Esse Null Modem ser� um cliente se conectando � um servidor
                   previamente especificado.
                   (Se n�o houver servidor: Seja um.)
 * transparent:1 - Apenas enviar as informa��es do serial, sem nenhum handshake
                   de RTS/DTR. Use essa op��o quando estiver se conectando via
                   algo que n�o seja um Null Modem.
 * telnet:1      - Interpreta informa��es de Telnet provenientes do site remoto.
                   Automaticamente ativa a transpar�ncia.
 * usedtr:1      - A conex�o n�o ser� estabelecida at� que o DTR seja ligado pelo
                   programa DOS. �til para terminais de modem.
 * inhsocket:1   - Usar um socket que ser� enviado ao DOSBox atrav�s de uma linha
                   de comando. Automaticamente ativa a transpar�ncia.
                   (Compatibilidade do Socket: � usado para rodar jogos do DOS
                   antigos em softwares da BBS novos.)

Exemplo: Para ser um servidor conectado � Porta TCP 5000
   serial1=nullmodem server:<IP ou nome do servidor> port:5000 rxdelay:1000



============================================================
9. Como rodar jogos que requerem mais recursos do computador 
============================================================

O DOSBox emula a CPU, as placas de som e de v�deos, e outros perif�ricos
de um computador, tudo de uma s� vez. A velocidade do aplicativo emulado
no DOS depende de quantas instru��es podem ser emuladas.
Esse valor � ajust�vel (n�mero de ciclos).

Ciclos da CPU
  Por padr�o (cycles=auto). O DOSBox tentar� descobrir quanto um jogo
  necessita para executar as tantas instru��es emuladas por intervalo de
  tempo poss�vel. � poss�vel for�ar esse comportamento ajustando os ciclos
  para cycles=max no arquivo de configura��es do DOSBox.
  A janela do DOSBox mostrar� uma linha "Cpu Cycles: max" na barra de t�tulo.
  Nesse modo � poss�vel reduzir a quantidade de ciclos por percentual
  (CTRL-F11) ou aumentar novamente (CTRL-F12).
  
  As vezes obtem-se melhores resultados ajustando manualmente o n�mero de ciclos.
  Ajuste, por exemplo, no arquivo de configura��es do DOSBox cycles=30000.
  � poss�vel aumentar ainda mais o n�mero de ciclos, enquanto voc� roda algum
  programa do DOS, apertando CTRL-F12 mas esse valor ser� limitado pela pot�ncia
  da sua CPU. Voc� pode ver o quanto de carga est� sendo processado pela sua CPU
  pelo Gerenciador de Tarefas no Windows 2000/XP/Vista e pelo Monitor de Sistema
  no Windows 95/98/ME. Uma vez que 100% do seu processador real esteja em uso n�o
  ser� mais poss�vel aumentar a velocidade do DOSBox, a menos que voc� reduza a
  carga de processamento de outros aplicativos que n�o sejam o do DOSBox.

N�cleos da CPU
  Em arquiteturas x86 (32 bits) voc� pode tentar for�ar o uso de um n�cleo
  recompilador din�mico (coloque core=dynamic no arquivo de configura��es).
  Isso geralmente tr�s melhores resultados se a auto detec��o (core=auto) falhar.
  A melhor op��o � colocar cycles=max. Mas note que poder�o existir jogos
  que funcionem pior do que com o n�cleo din�mico, ou que at� nem funcionem.

Emula��o de gr�ficos
  A emula��o do VGA � uma parte bastante delicada do DOSBox em termos de
  uso da CPU. Aumentar o n�mero de quadros que n�o ser�o emulados (frameskip)
  apertando CTRL-F8 (incrementos de um) poder�o ajudar no aumento da velocidade.
  A carga sobre a CPU dever� diminuir quando o n�mero de ciclos est� fixo.
  Repita esse procedimento at� que o jogo tenha uma velocidade agrad�vel para
  voc�. Note que isso � uma troca: o que voc� perde em fluidez do v�deo voc� ganha
  em velocidade.

Emula��o de som
  Voc� pode tentar desativar o som atrav�s do instalador do jogo para reduzir
  a quantidade de informa��es que dever�o ser processadas. Colocar nosound=true
  N�O desativa a emula��o dos dispositivos de som, apenas a sa�da de som ser�
  desativada.

Tente fechar todos os programas em execu��o, exceto o DOSBox, para aumentar ainda
mais os recursos para o DOSBox.


Configura��es avan�adas dos ciclos:
As op��es cycles=auto e cycles=max podem ser parametrizadas para possu�rem
diferentes padr�es de inicializa��o. A sintaxe �
  cycles=auto ["padr�o modoreal"] ["padr�o modo protegido"%] 
              [limite do "limite do ciclo"]
  cycles=max ["padr�o modo protegido"%] [limite do "limite do ciclo"]
Exemplo:
  cycles=auto 1000 80% limit 20000
  utilizar� cycles=1000 para jogos em modo real, 80% da acelera��o da CPU
  para jogos no modo protegido juntamente com um limite r�gido de 20000 ciclos



=========================
10. Solu��o de Problemas:
=========================

O DOSBox n�o inicia:
  - use valores diferentes para a op��o output= no arquivo de configura��o do DOSBox
  - atualize os drivers da sua placa de v�deo e o DirectX

Executar certos tipos de jogos faz o DOSBox fechar, mostrar mensagens de erro ou parar
de responder:
  - verifique se o jogo funciona com a instala��o padr�o do DOSBox
    (com arquivo de configura��o n�o modificado)
  - tente jogar com o som desativado (altere as configura��es do som
    no instalador do jogo. Tente tamb�m usar sbtype=none e gus=false no arquivo
    de configura��es do DOSBox)
  - tente alterar algumas op��es no arquivo de configura��es, especialmente:
      core=normal
      ciclos fixos (por exemplo cycles=10000)
      ems=false
      xms=false
    ou combina��es para as op��es acima,
    use configura��es similares a da m�quina que controla
    o chipset emulado e funcionalidade:
      machine=vesa_nolfb
    ou
      machine=vgaonly
  - use o loadfix antes de executar o jogo

O jogo � finalizado e retorna ao prompt do DOSBox com uma mensagem de erro:
  - leia a mensagem com aten��o e tente localizar o erro
  - utilize as dicas nas se��es acima descritas
  - monte em outros diret�rios pois alguns jogos s�o chatos quanto a localiza��o,
    por exemplo, se voc� utilizou "mount d d:\jogosantigos\jogox" tente
    "mount c d:\jogosantigos\jogo" ou "mount c d:\jogosantigos"
  - se o jogo necessitar de uma unidade de CD-ROM verifique se voc� digitou "-t cdrom"
    ao montar a unidade e tente usar outros par�metros adicionais (Os par�metros
    ioctl, usecd e label. Veja na se��o apropriada)
  - verifique as permiss�es dos arquivos do jogo (desmarque os atributos
    de somente-leitura e adicione permi��es para grava��es etc.)
  - tente reinstalar o jogo pelo dosbox

===============================
11. O Arquivo de Configura��es:
===============================

O arquivo com as configura��es pode gerado pelo CONFIG.COM, que est� localizado
na unidade interna (Z:) do dosbox. Leia a se��o "Programas Internos" para
entender o funcionamento do CONFIG.COM.
� poss�vel modificar o arquivo de configura��es gerado para personalizar o DOSBox.

O arquivo � dividido em diversas se��es (elas est�o destacadas por [] ). 
Algumas se��es possuem op��es que podem ser configuradas.
Linhas de coment�rio s�o indicadas por # e %. 
O arquivo de configura��es gerado cont�m as configura��es atuais. Voc� pode alter�-las
e ent�o iniciar o DOSBox com o par�metro -conf para carregar o arquivo e consequentemente
as novas configura��es.

O DOSBox buscar� o arquivo de configura��o especificado pelo par�metro -conf.
Se nenhum arquivo for especificado com o par�metro, o DOSBox ir� procurar pelo
arquivo "dosbox.conf" no diret�rio atual.
Se n�o existir nenhum, o DOSBox carregar� o arquivo de configura��es do usu�rio.
Esse arquivo ser� criado se ele n�o existir.
O arquivo pode ser encontrado em ~/.dosbox (no Linux) ou "~/Library/Preferences" (no MAC OS X).
No Windows os atalhos do menu iniciar dever�o ser usados para encontr�-lo.



========================
12. O Arquivo de Idioma:
========================

Um arquivo de idioma pode ser gerado pelo CONFIG.COM (CONFIG -writelang nomedoarquivo).
Leia-o, e esperamos que voc� entenda como mud�-lo. 
Inicie o DOSBox com o par�metro -lang para usar seu novo arquivo de idioma.
Alternativamente, voc� pode colocar o nome do arquivo na se��o [dosbox] do arquivo de configura��es.
L� existe uma entrada language= onde dever� ser adicionado o nome do arquivo.



=========================================
13. Criando sua pr�pria vers�o do DOSBox:
=========================================

Fa�a o download da fonte.
Verifique o INSTALADOR na distribui��o da fonte.



=============================
14. Agradecimentos Especiais:
=============================

Ver o arquivo THANKS.


============
15. Contato:
============

Acesse o site:
http://www.dosbox.com
para ver o email (Na p�gina "Crew").

