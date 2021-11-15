# HODL de Bitcoin seguro

* 1.- Introducción
* 2.- Requisitos
* 3.- Descargas necesarias
  * 3.1.- Wallet generator
  * 3.2.- Linux TAILS
* 4.- Instalacion Linux TAILS
  * 4.1.- Pendrive 1 OFFLINE
  * 4.2.- Pendrive 2 ONLINE
* 5.- Funcionamiento de cartera
  * 5.1.- Generar cartera
  * 5.2.- Cartera privada
  * 5.3.- Cartera sólo lectura
  * 5.4.- Recibir fondos
  * 5.5.- Enviar fondos

## 1.- Introducción
  - El objeto de esta guía es explicar la manera de custodiar tus Bitcoins de la manera más segura y barata, utilizando un **almacenamiento en frío** y firmando las transacciones utilizando un PC seguro y desconectado de la red. Para consultar la cartera, utilizaremos el PC conectado a la red. Es un tutorial orientado a quienes ahorran Bitcoin a largo plazo, habitualmente ingresan bitcoins en la wallet, y sólo esporádicamente necesitan sacarlos de la wallet.
  
  - Una cartera con Bitcoins consta de dos Claves Maestras: la **Clave Pública Maestra** y la **Clave Privada Mestra**. La clave Pública permite sólo-lectura de los fondos de la cartera, mientras que la clave Privada permite acceder dichos fondos y transferirlos. Conociendo la clave Privada, se puede conocer la clave Pública, pero nunca al revés. Por todo esto, la clave Privada debe custodiarse de manera muy segura, mientras que con la Pública podemos ser un poco menos precavidos ya que si alguien la obtuviera, podría ver cuáles son nuestros fondos, pero nunca obtenerlos.
  
- Para facilitar el almacenamiento de esta clave privada, se utilizan las **Seeds o semillas**, que son una serie de **12 o 24 palabras** que sirven para obtener la clave privada y restaurar la cartera. Esta semilla va unida a una Passphrase o palabra clave, que sería como la palabra 13 o 25. Con una misma semilla, cada Passphrase generaría una cartera diferente. Esto permite que almacenemos de forma segura una semilla y luego memoricemos la Passphrase o la almacenemos en un sitio diferente, por lo que si alguien accede a la semilla, necesita conocer tambien la Passphrase para acceder a los fondos. Con una misma semilla, podemos tener varias Passphrases, por lo que tendríamos diferentes carteras, con una única semilla.
**MUY IMPORTANTE NO PERDER NUNCA LA SEMILLA Y LA PASSPHRASE, AMBAS NECESARIAS PARA RECUPERAR LA CARTERA**.
  
- En lugar de utilizar un PC con Windows, que consideramos inseguro y propenso a virus/spyware/hackers, utilizaremos dos pendrives con el sistema operativo securizado live Linux TAILS en cada uno de ellos. Uno de ellos con la conexión a Internet configurada (conteniendo sólo la clave Pública, para poder ver los fondos en sólo-lectura, y generar transacciones sin firmar), y el otro sin conexión a Internet offline (donde guardaremos la clave Privada, y firmaremos las transacciones que haremos en el pendrive con la clave Pública). 
Si asumimos el riesgo de que alguien pueda conocer nuestros fondos (pero no moverlos), tambien podríamos cargar la clave pública en una cartera en en un sistema menos seguro como Windows o Android/iOS.
  
- No necesitamos un ordenador aparte dedicado, estos pendrive podremos cargarlos en cualquier PC o portátil que tengamos disponible. Se trata de un Linux que carga desde el pendrive y no accede ni cambia nada en el ordenador donde se arranca. Tras apagarlo no queda ningún rasto, ni pueden acceder a él virus que haya en el Windows instalado de ese mismo PC.

- Utilizaremos el **almacenamiento persistente encriptado** en cada uno de los Linux TAILS. Aquí podremos almacenar, aparte de la Wallet, cualquier documento privado encriptado. No se podrá acceder a ningún documento en el pendrive encriptado sin conocer la contraseña.
  
## 2.- Requisitos
  * -2x pendrive de 8Gb mínimo (los llamaremos "Pendrive 1 OFFLINE" y Pendrive 2 ONLINE").
  * -1x pendrive de 64Mb mínimo (lo llamaremos "Pendrive 3").
  * -1x ordenador con conexión a internet.
  * -4x Contraseñas (se puede usar la misma para todo):
      - "Pendrive 1 OFFLINE"
        - "Wallet Pendrive 1 OFFLINE"
      - "Pendrive 2 ONLINE"
        - "Wallet Pendrive 2 ONLINE"  
  * - (OPCIONAL) 2x Webcams. Puede evitarse utilizar el pendrive para firmar la transacción si se utilizan 2 PCs, cada uno con una webcam, y se transfiere mediante QR.      
    
  
## 3-. Descargas necesarias
### 3.1.- Wallet Generator
  - Accedemos a la web de Github de segwitaddress.org (es un generador de semilla HD para direcciones Segwit) dirigiéndonos a https://github.com/coinables/segwitaddress/releases . Nos descargamos la última versión, el fichero "Source Code.zip". Lo descargamos en "Pendrive 3" y lo descomprimimos en el mismo pendrive.
  
###   3.2.- Linux TAILS:
  - Accedemos a la web de TAILS (https://tails.boum.org), vamos al menú "Obtener TAILS", click en instalar desde Windows, y seguimos los pasos para descargar el fichero de imagen (fichero .img). Hacemos click en Verificar la descarga. Continuamos descargando el programa Etcher, y grabamos el "Pendrive 1 OFFLINE" siguiendo las instrucciones. Repetimos el grabado de la misma imagen sobre el "Pendrive 2 ONLINE".
  
## 4.- Instalacion Linux TAILS:
  ### 4.1.- Pendrive 1 OFFLINE
  - Apagamos el PC. Conectamos el "Pendrive 1 OFFLINE" y lo encendemos. Debe arrancar Linux TAILS, si no lo hace, seguir las instrucciones: https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key  
  - En la ventana de Bienvenida de TAILS, elegimos el idioma, el teclado y la región. Hacemos click debajo en el símbolo "+". Elegimos la opción "Offline mode" y "Disable all networking", y le damos a "Start TAILS". Una vez en el Escritorio, cerramos la ventana de TOR, ya que este pendrive no tendrá acceso a la red de ninguna manera.  
  - Para crear el almacenamiento persistente, nos vamos al menú "Applications/Tails/Configure persistent volume", e introducimos la contraseña "Pendrive 1 OFFLINE". En el siguiente menú, marcamos las opciones "Personal Data", "Welcome Screen", "Bitcoin Client" y "Dotfiles". Reiniciamos.  
  - De nuevo, elegimos el idioma, el teclado y la región. Introducimos la contraseña "Pendrive 1 OFFLINE" en el campo de passphrase, y clicamos en "Unlock". Hacemos click debajo en el símbolo "+". Elegimos la opción "Offline mode" y "Disable all networking", y le damos a "Start TAILS". En los siguientes arranques, bastará con introducir la contraseña para que cargue estas opciones automáticamente.  
    
  ### 4.2.- Pendrive 2 ONLINE
  
   - Apagamos el PC. Conectamos el "Pendrive 2 ONLINE" y lo encendemos. Debe arrancar Linux TAILS, si no lo hace, seguir las instrucciones: https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key  
   - En la ventana de Bienvenida de TAILS, elegimos el idioma, el teclado y la región. Hacemos click debajo en el símbolo "+". Le damos a "Start TAILS". Una vez en el Escritorio, en la ventana de Tor elegimos "Connect Tor automatically" y le damos a Connect. Cerramos la ventana.  
   - Para crear el almacenamiento persistente, nos vamos al menú "Applications/Tails/Configure persistent volume", e introducimos la contraseña "Pendrive 2 ONLINE". En el siguiente menú, marcamos las opciones "Personal Data", "Welcome Screen", "Network Connections", "Bitcoin Client" y "Dotfiles". Reiniciamos.  
   - De nuevo, elegimos el idioma, el teclado y la región. Introducimos la contraseña "Pendrive 2 ONLINE" en el campo de passphrase, y clicamos en "Unlock". Hacemos click debajo en el símbolo "+". Elegimos la opción "Offline mode" y "Disable all networking", y le damos a "Start TAILS". En los siguientes arranques, bastará con introducir la contraseña para que cargue estas opciones automáticamente.  
    
## 5.- Funcionamiento de cartera
  - El primer paso es generar la wallet. Obtendremos una semilla de tipo HD BIP39, la cual nos servirá en el futuro para otros software de wallet. Debemos anotarla en papel y guardarla bien, haciendo varias copias de seguridad en lugares diferentes. Si se pierde la semilla, perderemos todo. Si alguien obtiene nuestra semilla, podrá robarnos nuestros fondos. Generaremos una contraseña (passphrase) para complementar la semilla, la cual es IMPRESCINDIBLE para recuperar la cartera, no sirve sólo con la semilla. Podemos anotarla junto a la semilla o en un lugar diferente para mayor seguridad, memorizarla, etc.  
  - El segundo paso es cargar la wallet con la semilla en el "Pendrive 1 OFFLINE", donde generaremos tanto la clave privada como la pública. Este pendrive sólo lo arrancaremos offline cuando necesitemos realizar envíos de bitcoin mediante la clave privada.  
  - El tercer paso es cargar la wallet sólo lectura en "Pendrive 2 ONLINE". Para ello copiaremos la Clave Pública Maestra desde la wallet de "Pendrive 1 OFFLINE", y desde este pendrive sólo podremos hacer ingresos. Este pendrive se conectará a la Internet para comprobar el estado de fondos de la cartera, pero al haber cargado sólo la Clave Pública Maestra (y no la Privada), no corremos el riesgo de que puedan quitarnos nuestros fondos aunque se viera comprometida. Es por ello que la Clave Pública Maestra puede cargarse sin problemas en otras carteras para Windows o Android, sin riesgo que nos quiten los fondos (pero sí de perder nuestra privacidad y que puedan ver cuántos fondos tenemos).  
  
  ### 5.1.- Generar cartera
  - Arrancamos el PC con el "Pendrive 1 OFFLINE". Conectamos el "Pendrive 3" y desde el explorador de ficheros, accedemos a la carpeta que hemos descomprimido de "Source Code.zip", y la copiamos en la carpeta que pone "Tor Browser (persistent)" en el menú izquierdo del explorador (ruta completa: /home/amnesia/Persistent), si no la copiamos no puede abrirse directamente desde el pendrive por falta de permisos. Entramos a la carpeta "bip39" y abrimos "index.html". Click en "Generate New Mnemonic" y 24 palabras, movemos el raton en el recuadro para generar aleatoriedad. Anotamos en un papel las 24 palabras, es importante el orden y que nadie más pueda verlas. NO HACER FOTOGRAFIAS O GUARDARLAS EN NINGÚN MEDIO DIGITAL, SÓLO EN PAPEL. Cerramos el navegador.
    
  ### 5.2.- Cartera privada para firmar
  - Desde el PC arrancado con "Pendrive 1 OFFLINE", abrimos Electrum desde el menú. En nombre de cartera ponemos lo que queramos (por ejemplo "MiCartera1"), seleccionamos "Standard Wallet" y despues "I already have a seed". Introducimos las 24 palabras una detrás de otra, dejando un espacio entre cada una. En "Options", marcamos "BIP39" y "Extend this seed with custom words". Deberá indicar el estado "checksum: OK". En la siguiente ventana, introducimos una passpharase que queramos (tambien llamada palabra 25), ESTA PALABRA ES NECESARIA PARA RECUPERAR LA CARTERA. En la siguiente ventana, dejamos seleccionado "native segwit (p2wpkh)". Introducimos una contraseña para acceder al fichero de la wallet (IMPORTANTE, esto no es la passphrase de recuperación, sino una contraseña para acceder al fichero de la cartera desde Electrum). 
  
  ### 5.3.- Cartera sólo lectura
  - Con la cartera privada cargada desde "Pendrive 1 OFFLINE", vamos al menú "Wallet/Information" y copiamos la Master Public Key en un fichero de texto en "Pendrive 3". Apagamos el sistema, quitamos el "Pendrive 1 OFFLINE" y conectamos "Pendrive 2 ONLINE", y encendemos el PC. Abrimos Electrum, en nombre de cartera usamos la misma que anteriormente (por ejemplo "MiCartera1"), elegimos "Standard Wallet" y despues "Use Public or Private keys". Pegamos aqui la Master Public Key que hemos guardado en "Pendrive 3", y en la siguiente ventana pegamos la contraseña que hemos usado para la cartera privada (NO LA PASSPHRASE). A continuación se conectará a la red y nos indicará que ha sincronizado, mostrando 0 bitcoins de fondo. Ya tenemos nuestra cartera de sólo lectura.
  - Este mismo paso 5.3 puede hacerse en otros PC con Windows o en la aplicación de Android (puede leerse el QR en lugar de copiar la clave a mano), para poder consultar (sólo consultar) nuestra cartera desde cualquier sitio.
  
  
  ### 5.4.- Recibir fondos
  - Para recibir fondos, arrancamos "Pendrive 2 ONLINE", abrimos ELectrum y desde la pestaña "Receive", indicamos una "Description" para identificar la transacción en el futuro y le damos a "New Address". Ya podemos indicar esa dirección a quien sea para que nos envíen bitcoin. 
  - Es IMPORTANTE, por privacidad, no reutilizar nunca esa dirección para más pagos, aunque sea el mismo pagador. Para cada transacción nueva a recibir, debemos generar una nueva dirección cada vez.
  - Todo este proceso podemos hacerlo desde la cartera de sólo lectura en Windows, Android etc...
  
  ### 5.5.- Enviar fondos
  - Para enviar fondos, nos vamos al menú "Send", escribimos la dirección de envío que nos hayan indicado, una "Description" para identificar el concepto en el futuro y la cantidad de bitcoin a enviar. Le damos a "Pay", elegimos cuanto queremos pagar por la transacción (cada bloque son unos 10 minutos, pagamos según la prisa) y le damos a "Send". Lo que vemos es la transacción, pero como indica arriba, sin firmar aún ("Unsigned"). Hacemos click en "Export" y "Export to file", y lo guardamos en el "Pendrive 3".  
  - Arrancamos el PC con "Pendrive 1 OFFLINE", abrimos Electrum, click en "Tools/Load transaction/From file...", conectamos "Pendrive 3" y cargamos el fichero. Este es el momento más crítico, nos aseguramos bien que toda la información de dirección de origen, destino y cantidad de bitcoin son correctas, y clicamos en "Sign". El estado de la transacción en la parte de arriba ha cambiado a "Signed". Le damos de nuevo a "Export/Export to file" y guardamos la transacción, ya firmada, en el "Pendrive 3".  
  - Arrancamos de nuevo "Pendrive 2 ONLINE", abrimos Electrum y desde "Tools/Load transaction/From file..." cargamos el fichero de la transacción firmada. Clicamos en "Broadcast" para enviarla a la red, y ya estaría en proceso.
    
