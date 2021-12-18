# HODL de Bitcoin seguro (v1.3)

  - **IMPORTANTE:** Este método puede ser igual de seguro que utilizar una hardware wallet comercial, pero sólo si se realiza **SIEMPRE** de manera estricta y cuidadosa. Si estás empezando o sospechas que puede ser muy complicado para tí, lo mejor es comenzar utilizando una hardware wallet comercial como Ledger, Trezor o Coldcard. Luego, siempre puedes volver a este tutorial y aprender a utilizarlo, teniendo la confianza de disponer ya de antemano de una manera segura para almacenar y gestionar tus bitcoins.


* 1.- Introducción
  * 1.1.- Objetivo de la guía
  * 1.2.- Recomendaciones extra
* 2.- Requisitos
* 3.- Descargas necesarias
  * 3.1.- Generador de cartera
  * 3.2.- Linux TAILS
  * 3.3.- (Opcional) Script "rolls.py"
* 4.- Instalacion Linux TAILS
  * 4.1.- Pendrive 1 OFFLINE
  * 4.2.- Pendrive 2 ONLINE
* 5.- Funcionamiento de cartera
  * 5.1.- Generar cartera
  * 5.2.- Cartera privada
  * 5.3.- Cartera sólo lectura
  * 5.4.- Recibir fondos
  * 5.5.- Enviar fondos
  * 5.6.- Confirmar fondos (Opcional)
* 6.- Extras
  * 6.1.- Actualizar TAILS
  * 6.2.- Actualizar Electrum
  * 6.3.- Instalar cartera Sparrow
  * 6.4.- Cómo regalar bitcoins a alguien sin cartera  
        * 6.4.1.- Introducción  
        * 6.4.2.- Generar semilla para regalo  

## 1.- Introducción
### 1.1.- Objetivo de la guía
  - El objeto de esta guía es explicar la manera de custodiar tus bitcoins de la manera más segura y barata, utilizando un **almacenamiento frío (cold storage)** y **separado por aire (airgapped)**, firmando las transacciones utilizando un PC securizado y desconectado de la red. Para consultar la cartera, utilizaremos el PC conectado a la red. Es un tutorial orientado a quienes custodian Bitcoin a largo plazo, habitualmente ingresan bitcoins en la cartera, y sólo esporádicamente necesitan enviarlos. Si vas a hacer muchos envíos de bitcoins a menudo, existen otras soluciones comerciales más cómodas, como Coldcard MK3.  

  - Una cartera Bitcoin consta de dos Claves Maestras: la **Clave Pública Maestra** y la **Clave Privada Maestra**. La Clave Pública Maestra permite sólo-lectura de los fondos de la cartera, mientras que la Clave Privada Maestra permite acceder dichos fondos y transferirlos. Conociendo la clave Privada, se puede conocer la clave Pública, pero nunca al revés. Por todo esto, la clave Privada debe custodiarse de manera muy segura, mientras que con la Pública podemos ser un poco menos precavidos ya que si alguien la obtuviera, podría llegar a ver nuestros fondos, pero nunca obtenerlos. Si esta clave pública de sólo lectura (watch-only) la utilizamos en un PC con TAILS, reducimos al mínimo el riesgo de esta fuga de privacidad.  
  
  - Para facilitar el almacenamiento de la Clave Privada Maestra, se utiliza la **Seed o semilla**, que son una serie de **12 o 24 palabras** que sirven para obtener la clave privada y restaurar la cartera. Esta semilla va unida a una Passphrase, que sería como la palabra 13 o 25, una palabra extra que elegimos nosotros mismos para añadir otra capa de seguridad extra. Con una misma semilla, cada Passphrase generaría una cartera diferente. Esto permite que almacenemos de forma segura una semilla y luego memoricemos la Passphrase o la almacenemos en un sitio diferente, por lo que si alguien accede a la semilla, necesita conocer tambien la Passphrase para acceder a los fondos. Con una misma semilla, podemos tener varias Passphrases, por lo que tendríamos diferentes carteras, desde esa única semilla. Es importante anotar tambien el tipo de cartera Bitcoin (tambien conocido como "derivation path", ruta de derivación), en nuestro caso usaremos Segwit (m/84'/0'/0'). Es una cartera de tipo HD (Hierarquical Deterministic).  
**MUY IMPORTANTE NO PERDER NUNCA LA SEMILLA Y LA PASSPHRASE, AMBAS NECESARIAS PARA RECUPERAR LA CARTERA**.  
  
  - En lugar de utilizar un PC con Windows para almacenar y trabajar con la Clave Privada Maestra, sistema que consideramos inseguro y propenso a virus/spyware/hackers tanto por el Sistema Operativo como por estar conectado a Internet, utilizaremos dos pendrives con el sistema operativo securizado live Linux TAILS en cada uno de ellos. Uno de ellos con la conexión a Internet configurada (conteniendo sólo la clave Pública, para poder ver los fondos en sólo-lectura, y generar transacciones sin firmar), y el otro sin conexión a Internet offline (donde guardaremos la clave Privada, y firmaremos las transacciones que haremos en el pendrive con la clave Pública). 
Si asumimos el riesgo de que alguien pueda conocer nuestros fondos (pero no moverlos), tambien podríamos cargar la clave pública en una cartera en en un sistema menos seguro como Windows o Android/iOS para mayor comodidad, por lo que no necesitaríamos el pendrive llamado "Pendrive 2 ONLINE". Es por ello que este pendrive es opcional.
**NUNCA CARGAR LA CLAVE PRIVADA MAESTRA EN UN PC CONECTADO A INTERNET. SÓLO CARGAR LA CLAVE PÚBLICA MAESTRA**.  
  
  - No necesitamos un ordenador diferente para cada función, estos pendrives podremos cargarlos en cualquier PC o portátil que tengamos disponible, incluso usar el mismo arrancando cada vez con un pendrive. Se trata de un Linux que carga desde el pendrive y no accede ni cambia nada en el ordenador donde se arranca. Tras apagarlo no queda ningún rasto, ni pueden acceder a él virus que haya en el Windows instalado de ese mismo PC.  

  - Utilizaremos el **almacenamiento persistente encriptado** en cada uno de los pendrive Linux TAILS. TAILS genera una partición encriptada con una contraseña, por lo que nadie podría acceder al contenido en caso de obtener dicho pendrive. Aquí podremos almacenar, aparte de la cartera, cualquier documento privado que queramos. No se podrá acceder a ningún fichero en el pendrive encriptado sin conocer la contraseña.  

### 1.2.- Recomendaciones extra
  - Utilizar un nodo propio, en lugar de uno público. Con esto logramos tanto mantener la privacidad en nuestras transacciones, como garantizar que nuestras consultas sobre las transacciones son verídicas y no han sido manipuladas. Garantizamos que el envío de transacciones a la red lo realizaremos nosotros mismos, con nuestro propio servidor, sin depender de equipos de terceros. Hay opciones sencillas y con una mínima configuración como **[Umbrel](https://getumbrel.com)**, otras más personalizadas pero manteniendo la sencillez de hacerlo todo automático como **[Raspiblitz](https://github.com/rootzoll/raspiblitz)**, y otras como el tutorial **[RaspiBolt](https://raspibolt.org)** donde el objetivo es aprender a hacer paso a paso lo necesario para montar a mano nuestro propio nodo.  
  
## 2.- Requisitos
  * -1x pendrive de 8Gb mínimo (lo llamaremos "Pendrive 1 OFFLINE").
  * -1x pendrive de 8Gb mínimo (lo llamaremos "Pendrive 2 ONLINE") (Opcional, para mayor privacidad).
  * -1x pendrive del tamaño que sea (lo llamaremos "Pendrive 3") (Opcional, si se usan webcams con QR).
  * -1x ordenador con conexión a internet.
  * -4x Contraseñas (por comodidad, se puede usar la misma para todo):
      - "Pendrive 1 OFFLINE"
      - "Cartera Pendrive 1 OFFLINE"
      - "Pendrive 2 ONLINE"
      - "Cartera Pendrive 2 ONLINE"
  * -(Opcional) 2x Webcams y 2x PCs. Método más seguro. Puede evitarse utilizar el "Pendrive 3" para transferir la transacción entre PCs si se utilizan 2 PCs, cada uno con una webcam, y se transfiere mediante lector QR.  
    
## 3-. Descargas necesarias
###   3.1.- Generador de cartera
  - Accedemos al repositorio Github de **[SegWitAddress.org](https://github.com/coinables/segwitaddress/releases) (https://github.com/coinables/segwitaddress/releases)** (es un generador de semilla HD para direcciones Segwit). Nos descargamos de la última versión, el fichero "Source Code.zip". Lo guardamos en "Pendrive 3" y lo descomprimimos en el mismo pendrive.  
  
###   3.2.- Linux TAILS:
  - Accedemos a la **[web de TAILS](https://tails.boum.org) (https://tails.boum.org)**, vamos al menú "Obtener TAILS", click en instalar desde Windows, y seguimos los pasos para descargar el fichero de imagen (fichero .img). Hacemos click en "Verificar la descarga". Continuamos descargando el programa **[Balena Etcher](https://www.balena.io/etcher/)**, y grabamos el "Pendrive 1 OFFLINE" siguiendo las instrucciones. Repetimos el grabado de la misma imagen sobre el "Pendrive 2 ONLINE" (Opcional).  
  
###   3.3.- (Opcional) Script "rolls.py":
  - Nos debemos descargar el script **[rolls.py](https://raw.githubusercontent.com/Coldcard/firmware/master/docs/rolls.py)** (https://raw.githubusercontent.com/Coldcard/firmware/master/docs/rolls.py) y copiarlo mediante al "Pendrive 3".  

## 4.- Instalacion Linux TAILS:
### 4.1.- Pendrive 1 OFFLINE
  - Apagamos el PC. Desconectamos el cable de red del PC. Conectamos el "Pendrive 1 OFFLINE" y lo encendemos. Debe arrancar Linux TAILS. Si no lo hace, seguir las instrucciones de **[Starting with the Boot Menu key](https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key)** (https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key) .  

  - En la ventana de Bienvenida de TAILS, elegimos el idioma, el teclado y la región. Hacemos click debajo en el símbolo "+". Elegimos la opción "Offline mode" y "Disable all networking", y le damos a "Start TAILS". Una vez en el Escritorio, si aparece una ventana de TOR la cerramos, ya que este pendrive no tendrá acceso a la red de ninguna manera.  

  - Para crear el almacenamiento persistente encriptado, nos vamos al menú "Applications/Tails/Configure persistent volume", e introducimos la contraseña "Pendrive 1 OFFLINE". En el siguiente menú, marcamos las opciones "Personal Data", "Welcome Screen", "Bitcoin Client" y "Dotfiles". Reiniciamos.  

  - De nuevo, elegimos el idioma, el teclado y la región. Introducimos la contraseña "Pendrive 1 OFFLINE" en el campo de passphrase, y clicamos en "Unlock". Hacemos click debajo en el símbolo "+". Elegimos la opción "Offline mode" y "Disable all networking", y le damos a "Start TAILS". En los siguientes arranques, bastará con introducir la contraseña para que cargue estas opciones automáticamente.  
    
### 4.2.- Pendrive 2 ONLINE (Opcional)
  
  - Apagamos el PC. Conectamos el "Pendrive 2 ONLINE", y lo encendemos. **Debemos conectarle el cable de red o logarnos en la red WIFI al arrancar el sistema**. Debe arrancar Linux TAILS. Si no lo hace, seguir las instrucciones de **[Starting with the Boot Menu key](https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key)** (https://tails.boum.org/doc/first_steps/start/pc/index.es.html#boot-menu-key).  

  - En la ventana de Bienvenida de TAILS, elegimos el idioma, el teclado y la región. Hacemos click debajo en el símbolo "+". Le damos a "Start TAILS". Una vez en el Escritorio, en la ventana de Tor elegimos "Connect Tor automatically" y le damos a Connect. Cerramos la ventana.  

  - Para crear el almacenamiento persistente, nos vamos al menú "Applications/Tails/Configure persistent volume", e introducimos la contraseña "Pendrive 2 ONLINE". En el siguiente menú, marcamos las opciones "Personal Data", "Welcome Screen", "Network Connections", "Bitcoin Client" y "Dotfiles". Reiniciamos.  

  - De nuevo, elegimos el idioma, el teclado y la región. Introducimos la contraseña "Pendrive 2 ONLINE" en el campo de passphrase, y clicamos en "Unlock". Hacemos click debajo en el símbolo "+" y habilitamos la opción "Administration password". Le damos a "Start TAILS". En los siguientes arranques, bastará con introducir la contraseña para que cargue estas opciones automáticamente.  
    
## 5.- Funcionamiento de cartera
  - El **primer paso 5.1** es generar la cartera. Obtendremos una semilla de tipo HD BIP39, la cual nos podrá servir en el futuro para otros software de cartera diferentes a Electrum. Debemos anotarla en papel y guardarla bien, haciendo varias copias de seguridad en lugares diferentes. Si se pierde la semilla, perderemos todo. Si alguien obtiene nuestra semilla, podrá llevarse nuestros fondos. Generaremos una contraseña (passphrase) para complementar la semilla, la cual es IMPRESCINDIBLE para recuperar la cartera, no sirve sólo con la semilla. Podemos anotarla junto a la semilla o en un lugar diferente para mayor seguridad, memorizarla, etc.  

  - El **segundo paso 5.2** es cargar la cartera con la semilla en el "Pendrive 1 OFFLINE", donde generaremos tanto la clave privada como la pública. Este pendrive sólo lo arrancaremos offline cuando necesitemos realizar envíos de bitcoin mediante la clave privada.  

  - El **tercer paso 5.3** es cargar la cartera sólo lectura en "Pendrive 2 ONLINE". Para ello copiaremos la Clave Pública Maestra desde la cartera de "Pendrive 1 OFFLINE", y desde este pendrive sólo podremos hacer ingresos. Este pendrive se conectará a la Internet para comprobar el estado de fondos de la cartera, pero al haber cargado sólo la Clave Pública Maestra (y no la Privada), no corremos el riesgo de que puedan quitarnos nuestros fondos aunque se viera comprometida. Es por ello que la Clave Pública Maestra puede cargarse sin problemas en otras carteras para Windows o Android, sin riesgo que nos quiten los fondos (pero sí de perder nuestra privacidad y que puedan ver cuántos fondos tenemos).  
  
### 5.1.- Generar cartera (semilla)
  - La semilla secreta para generar nuestra cartera se basa en el estándar **[BIP-0039](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)**.  

  - Arrancamos el PC con el "Pendrive 1 OFFLINE". Conectamos el "Pendrive 3" y desde el explorador de ficheros, accedemos a la carpeta que hemos descomprimido de "Source Code.zip", y la copiamos en la carpeta que pone "Tor Browser (persistent)" en el menú izquierdo del explorador (ruta completa: /home/amnesia/Persistent), si no la copiamos no puede abrirse directamente desde el pendrive por falta de permisos. Entramos a la carpeta "bip39" y abrimos "index.html". Click en "Generate New Mnemonic" y 24 palabras, movemos el raton en el recuadro para generar aleatoriedad. Anotamos en un papel las 24 palabras (llamadas semilla o seed), es importante el orden y que nadie más pueda verlas. **NO HACER FOTOGRAFIAS O GUARDARLAS EN NINGÚN MEDIO DIGITAL, SÓLO EN PAPEL**. Cerramos el navegador.  

  - (Opcional) Otra manera de generar la semilla alternativa al proceso anterior, es utilizando unos dados de 6 caras. Utilizaremos el script "rolls.py", creado por la gente de Coldcard y de código abierto. Con un dado sirve, pero con varios se hace más rápido. A continuación lanzamos el/los dado/s unas 100 veces, y vamos anotando la secuencia (46302388123...) en la línea de comandos. Desde la línea de comandos en linux, nos movemos hacia el directorio donde tenemos el script "rolls.py" y lanzamos el comando `echo XXXXXX | python3 rolls.py`, sustituyendo "XXXXXX" por la secuencia de 100 números generados mediante dados. Anotamos en un papel las 24 palabras (llamadas semilla o seed), es importante el orden y que nadie más pueda verlas. **NO HACER FOTOGRAFIAS O GUARDARLAS EN NINGÚN MEDIO DIGITAL, SÓLO EN PAPEL**.  
 
    
### 5.2.- Cartera privada para firmar
  - Desde el PC arrancado con "Pendrive 1 OFFLINE", abrimos Electrum desde el menú. Le ponemos un nombre a la cartera (por ejemplo "MiCartera1"), seleccionamos "Standard Wallet" y despues "I already have a seed". Introducimos las 24 palabras una detrás de otra, dejando un espacio entre cada una, en el orden preciso. En "Options", marcamos "BIP39" y "Extend this seed with custom words". Deberá indicar el estado "checksum: OK". En la siguiente ventana, introducimos una passpharase que queramos (tambien llamada palabra 25), **ESTA PALABRA ES NECESARIA PARA RECUPERAR LA CARTERA**. Es importante **[elegir una Passphrase segura](https://xkcd.com/936/)** , se admiten mayúsculas, minúsculas y números, pero **no se recomienda utilizar caracteres extraños** por futuros problemas de copmpatibilidad. En la siguiente ventana, dejamos seleccionado "native segwit (p2wpkh)" y verificamos que la ruta de derivación sea "m/84'/0'/0'". Introducimos una contraseña para acceder al fichero de la cartera (**IMPORTANTE**, esto no es la Passphrase de recuperación, sino una contraseña para poder abrir el fichero de la cartera desde Electrum, ya que por seguridad se guarda encriptada. La Passphrase es lo que usaremos junto a la Semilla cuando necesitemos restaurar las claves privadas en algún momento. Por eso es tan importante guardar ambas con seguridad y por duplicado en varios lugares).  

  - Una manera segura de generar una Passphrase consiste en lanzar un dado 5 veces y anotar la palabra **[de la lista de una lista de palabras](https://www.eff.org/files/2016/07/18/eff_large_wordlist.txt)**. Repetimos este proceso unas 6 u 8 veces, unimos todas las palabras una detrás de otra, y ya tenemos una Passphrase extremadamente segura. Tambien podemos hacer lo mismo abriendo un libro en páginas aleatorias, y colocando el dedo sobre zonas aleatorias para así obtener las palabras.  
  
### 5.3.- Cartera sólo lectura
  - Con la cartera privada abierta en "Pendrive 1 OFFLINE", vamos al menú "Wallet/Information" y copiamos la Master Public Key en un fichero de texto en "Pendrive 3" (opcionalmente, si tenemos webcams y 2 PCs podemos transmitirlo mediante QR). Apagamos el sistema, quitamos el "Pendrive 1 OFFLINE" y conectamos "Pendrive 2 ONLINE", y encendemos el PC. Abrimos Electrum, en nombre de cartera usamos la misma que anteriormente (por ejemplo "MiCartera1"), elegimos "Standard Wallet" y despues "Use Public or Private keys". Pegamos aqui la Master Public Key que hemos guardado en "Pendrive 3" (o mediante QR con webcams), y en la siguiente ventana escribimos la contraseña que hemos usado para la cartera privada (NO LA PASSPHRASE). A continuación se conectará a la red y nos indicará que ha sincronizado, mostrando 0 bitcoins de fondo. Ya tenemos nuestra cartera de sólo lectura.  

  - Este mismo paso 5.3 puede hacerse en otros PC con Windows o en la aplicación de Android (puede leerse el QR en lugar de copiar la clave a mano), para poder consultar (no mover fondos) nuestra cartera desde cualquier sitio.  
  
  
### 5.4.- Recibir fondos
  - Para recibir fondos, arrancamos "Pendrive 2 ONLINE" (o desde el PC que sea con la cartera de solo lectura), abrimos Electrum y desde la pestaña "Receive", indicamos una "Description" para identificar la transacción en el futuro y le damos a "New Address", si ponemos una cantidad sugerimos una cantidad a pagar (como una factura). Ya podemos indicar esa dirección a quien sea para que nos envíen bitcoins.  

  - Es importante por privacidad, no reutilizar nunca esa dirección para más pagos, aunque sea el mismo pagador. Para cada transacción nueva a recibir, debemos generar una nueva dirección cada vez. Esto evita que cualquiera a quien enviemos o recibamos bitcoins pueda relacionar otros pagos o estimar la cantidad que poseemos.  

  - Todo este proceso podemos hacerlo desde la cartera de sólo lectura en Windows, Android, MAC o el sistema que permita cargar carteras de sólo lectura (no tiene por qué ser la cartera Electrum).  
  
### 5.5.- Enviar fondos
  - Para enviar fondos, arrancamos "Pendrive 2 ONLINE" (o desde el PC que sea con la cartera de solo lectura), nos vamos al menú "Send", escribimos la dirección de envío que nos hayan indicado, una "Description" para identificar el concepto en el futuro y la cantidad de bitcoins a enviar. Le damos a "Pay", elegimos cuánto queremos pagar por la tasa (fee) de transacción (cada bloque son unos 10 minutos, pagamos según la prisa) y le damos a "Send". Lo que tenemos es la transacción sin firmar aún, como indica arriba ("Unsigned"). Hacemos click en "Export" y "Export to file", y lo guardamos en el "Pendrive 3" (opcionalmente, exportamos el QR para webcam).  

  - Arrancamos el PC con "Pendrive 1 OFFLINE", abrimos Electrum, click en "Tools/Load transaction/From file...", conectamos "Pendrive 3" y cargamos el fichero (opcionalmente, importamos el QR para webcam). **Este es el momento más crítico de todo el procedimiento**, nos aseguramos bien que toda la información de dirección de origen (UTXOs), destino y cantidad de bitcoin son correctas, y clicamos en "Sign". El estado de la transacción en la parte de arriba ha cambiado a "Signed". Le damos de nuevo a "Export/Export to file" y guardamos la transacción, ya firmada, en el "Pendrive 3" (opcionalmente, exportamos el QR para webcam).  

  - Arrancamos de nuevo "Pendrive 2 ONLINE", abrimos Electrum y desde "Tools/Load transaction/From file..." cargamos el fichero de la transacción firmada (opcionalmente, importamos el QR para webcam). Clicamos en "Broadcast" para enviarla a la red, y esperamos a que sea aceptada en un bloque minado. **Es importante que como mínimo haya 1 confirmación de red para asegurar que hemos enviado o recibido los fondos**, para estar seguros 100% esperar al menos 2 o 3 confirmaciones (para los más paranoicos o para Electrum, se consideran 6 confirmaciones).  

### 5.6.- Confirmar fondos (Opcional)
  - Podemos ver el estado de una transacción y su posición en la cola de espera utilizando el servicio de **[mempool.space](https://mempool.space)** (https://mempool.space). Para ello, hacemos doble click sobre una transacción y en la ventana que se nos abre, copiamos el número de transacción y lo pegamos en el cuadro de búsqueda de la web. En caso que no se haya confirmado aún, podremos ver con una flecha blanca en que posición está dentro de la mempool (la cola de espera de transacciones para ser confirmadas) en función de la tasa (fee) que hayamos pagado.  

  - Podemos acelerar el envío si hemos puesto una tasa demasiado baja mediante la función [CPFP](https://academy.bit2me.com/que-es-child-pays-for-parent-cpfp/) (https://academy.bit2me.com/que-es-child-pays-for-parent-cpfp/) y la función [RBF](https://academy.bit2me.com/que-es-replace-by-fee-rbf/) (https://academy.bit2me.com/que-es-replace-by-fee-rbf/), pero esto queda fuera del alcance de este documento.  


## 6.- Extras

### 6.1.- Actualizar TAILS
  - Primero actualizamos el pendrive ONLINE. Arrancamos el PC con el pendrive conectado y el cable de red (o WIFI), deberá informarnos que tiene una actualización al arrancar. Si no lo hace, hay que **[seguir estas instrucciones](https://tails.boum.org/doc/upgrade/index.es.html)** abriendo una ventana de Terminal desde el menú inicio e introduciendo el comando `tails-upgrade-frontend-wrapper`. Al terminar, reiniciamos el sistema tal como nos solicita.    

  - Puesto que el pendrive OFFLINE no puede conectarse a Internet, lo actualizaremos conectándolo al PC tras haber arrancado con el pendrive ONLINE, una vez ha sido actualizado de antemano. Seguiremos **[el punto 5/5 de esta guía](https://tails.boum.org/upgrade/tails/index.es.html)**, desde el menú inicio Applications / Tails / Tails Installer, seleccionamos el pendrive insertado OFFLINE y le damos a Upgrade.  

### 6.2.- Actualizar Electrum
  - Arrancando con el pendrive ONLINE, nos descargamos la última versión Appimage para Linus desde **[su página de descarga](https://electrum.org/#download)** y la copiamos en nuestra carpeta personal persistente. Hacemos click derecho / Propiedades sobre el archivo, y en la pestaña permisos, le damos permisos de ejecución. A partir de ahora, ejecutaremos este archivo de Electrum en lugar de versión del menú inicio. Copiamos el fichero mediante un tercer pendrive para llevárnoslo al PC offline.  

  - Arrancando con el pendrive OFFLINE, copiamos el fichero a la carpeta persistente y le damos permisos de ejecución como hicimos en el paso anterior.  

### 6.3.- Instalar cartera Sparrow
  - El inconveniente de utilizar Sparrow en TAILS, es que hay que hacer el paso de instalación cada vez que se reinicie el sistema. Si se quiere añadir la cartera Sparrow, esta puede descargarse directamente en el pendrive ONLINE a través de TOR, utilizando la descargar **[Linux (Ubuntu/Debian)](https://sparrowwallet.com/download/)** y lanzando el comando `sudo dpkg -i sparrow_1.5.2-1_amd64.deb` desde la consola de TAILS. Desde el menú "Applications" y dentro "Other", podremos lanzar Sparrow. A continuación, se puede copiar este archivo al pendrive OFFLINE e instalar con el mismo comando.  

  - Es importante una vez configurada una cartera en Sparrow, hacer una copia de la misma en la partición persistente de TAILS desde el menú "File" y "Export Wallet", para evitar tener que configurarla cada vez que iniciemos TAILS (aunque la propia aplicación Sparrow sí habría que instalarla cada vez con el comando anterior).  

### 6.4.- Cómo regalar bitcoins a alguien sin cartera.
#### 6.4.1.- Introducción
  - Queremos regalar bitcoins a amigos o familiares, pero no saben nada de como funciona Bitcoin, ni disponen de cartera de ningún tipo. La mejor opción pasaría por generarles una semilla de cartera Bitcoin, transferirles los fondos a una dirección de esa cartera y entregarles las 24 palabras en mano. La llamaremos, familiarmente, semilla-regalo.    

  - Estas palabras de la semilla-regalo podrían entregarse escritas a lapicero (no se borra si se moja) en una tarjeta de felicitación navideña o una carta escrita a mano, se pueden [grabar sobre unas arandelas]([Linux (Ubuntu/Debian)](https://sparrowwallet.com/download/)) o por cualquier método físico que se nos ocurra (nunca medios digitales). Lo bueno, si es simple, es doblemente bueno. No hagas complicado lo sencillo. No estás tratando con bitcoiners veteranos. Piensa en tu familia. Ellos no lo harían.   

  - Para mantener el **almacenamiento frío**, evitaremos introducir las palabras en cualquier ordenador conectado a internet, teléfono móvil o sistema offline que no garanticemos como seguro. Por supuesto, quedan descartadas tiendas que diseñan regalos personalizados como tazas o fotografías de recuerdo. Cualquier método que implique dar a conocer la semilla a terceras personas o transmitirla por medios digitales.  

  - **SIEMPRE** nos guardaremos una copia nosotros bien custodiada de dicha semilla. Primero, porque al haberla generado nosotros, no estamos vulnerando la privacidad de a quien se le regala, porque ya sabe (y debería asumir) que disponemos de una copia y por tanto, no es una cartera segura. Segundo, y más importante, las personas que no tienen contacto habitual con Bitcoin, no estiman el valor y la importancia de custodiar una semilla y no perderla. Les haremos un gran favor custodiando una copia para ellos, si dentro de unos años se dan cuenta que la perdieron entre una nube de turrones y licores navideños.  

  - Sería recomendable anexar algún tipo de indicación advirtiendo **en contra** de utilizar esa misma semilla como cartera personal más allá del propio regalo, al no considerarse privada por no haberla generado ellos mismos. Alguien novato e incauto podría tratar de aprovechar esa misma cartera para hodlear bitcoins. Debemos indicarles que la mejor opción para usar esos fondos llegado el momento, sería hacer un "sweep" o "barrido" de dichos fondos a una cartera propia, segura y privada, generada por ellos mismos, una hardware wallet, etc.  

#### 6.4.2.- Generar semilla para regalo 
  - No es requisito haber realizado ningún paso previo del tutorial para generar la semilla-regalo. Sólo necesitaremos un pendrive de al menos 8Gb, y otro pendrive del tamaño que sea (sólo necesitamos unos pocos megabytes).

  - **Paso 1:**  Desde un PC con internet, nos descargamos lo indicado en los puntos 3.1 (generador de cartera) y 3.3 (opcional, generador de cartera mediante dados) y lo copiamos en el pendrive pequeño. Nos descargamos la imagen de disco TAILS del punto 3.2 y la grabamos en el pendrive de 8Gb según instrucciones.
 
  - **Paso 2:**  Realizamos completo el punto 4.1, inicializar el PC con el pendrive TAILS (Pendrive 1 OFFLINE). Es importante realizar todo el proceso sin cable de red o wifi conectado.

  - **Paso 3:**  Realizamos completo el punto 5.1, generar la semilla-regalo usando uno de los dos métodos propuestos. Anotamos las 24 palabras en un papel.

  - **Paso 4:**  Realizamos el punto 5.2, pero **NO MARCAMOS la opcion “Extend this seed with custom words”**. Es decir, no utilizaremos una passphrase. Despues nos pedirá una "password" para encriptar el fichero de la cartera, lo dejamos en blanco, pues va a ser borrada despues.

  - **Paso 5:**  Ahora sólo nos queda coger de esta cartera cargada en Electrum la primera dirección y enviar allí los bitcoins. Si hacemos click en "Recibir", podemos hacer la transferencia leyendo el QR de la dirección con un móvil, podemos copiar esa dirección en un txt o el método que queramos.

  - **Paso 6:**  Cuando hemos confirmado que se han enviado correctamente los fondos a la dirección de destino, podemos desconectar y formatear el pendrive, siempre asegurando antes que tenemos bien copiadas las palabras de la semilla-regalo.
