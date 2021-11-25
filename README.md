# Linuxserial

Saudações!!

Este emulador de porta serial foi criado originalmente por Luis Claudio Gamboa Lopes,
após algumas pesquisas atualizei por sugestões do qastack, no seguinte endereço:

https://qastack.com.br/programming/52187/virtual-serial-port-for-linux

E seguindo os passos de instalação conforme em:

https://qastack.com.br/ubuntu/588800/setup-virtual-serial-ports-linux-null-modem-emulator-using-tty0tty

O resumo atualizado dos passos para instalar é:

1. Baixe o pacote tty0tty de uma destas fontes:

        clone o repo https://github.com/canalcleyton/linuxserial       
        git clone https://github.com/canalcleyton/linuxserial


2. Construa o módulo do kernel a partir da fonte fornecida

	```
        cd linuxserial/module      
        make
	``` 
       
3. Copie o novo módulo do kernel no diretório de módulos do kernel

	```
        sudo cp tty0tty.ko /lib/modules/$(uname -r)/kernel/drivers/misc/
	```
        
4. Carregue o módulo

	```
        sudo depmod
        sudo modprobe tty0tty
        Você deve ver novas portas seriais em /dev/(ls /dev/tnt*)
	```
	        
5. Conceda permissões apropriadas às novas portas seriais

	```
        sudo chmod 666 /dev/tnt*
	```

6. Incluir a linha seguinte no arquivo /etc/modules-load.d/modules.conf (para que o módulo seja carregado automaticamente)

        tty0tty

Lembrando que seu S.O. Linux deve estar com os arquivos fontes de cabeçalho instalados, bem como as ferramentas
de compilação GNU ou compatível. Para tal, nas distros Debian ou Ubuntu, execute os comandos:

        sudo apt-get install linux-headers-$(uname -r) build-essential linux-headers-generic manpages-dev
        sudo apt-get install linux-image-$(uname -r)
 	
How to work with serial port on linux using tty0tty made by Luis Claudio Gamboa Lopes


        tty0tty - linux null modem emulator v1.2 


This is the tty0tty directory tree:

  > module         - linux kernel module null-modem
  > pts		 - null-modem using ptys (without handshake lines)


pts (unix98): 

When run connect two pseudo-ttys and show the connection names:

        (/dev/pts/1) <=> (/dev/pts/2) 

## the connection is:
  
        TX -> RX
        RX <- TX

## module:

The module is tested in kernel 3.10.2 (debian) 

## When loaded, create 8 ttys interconnected:

        /dev/tnt0  <=>  /dev/tnt1 
        /dev/tnt2  <=>  /dev/tnt3 
        /dev/tnt4  <=>  /dev/tnt5 
        /dev/tnt6  <=>  /dev/tnt7 

## the connection is:
  
        TX   ->  RX
        RX   <-  TX
        RTS  ->  CTS
        CTS  <-  RTS
        DSR  <-  DTR
        CD   <-  DTR
        DTR  ->  DSR
        DTR  ->  CD
  

## Requirements:

        for module build is necessary kernel-headers or kernel source

### For e-mail suggestions :  lcgamboa@yahoo.com
