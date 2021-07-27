# Seguridad Bitcoin para pobres

1.- Introducción
2.- Requisitos
3-. Preparación previa
4.- Funcionamiento de cartera
  4.1.- Generar cartera
  4.2.- Cartera privada
  4.3.- Cartera sólo lectura

1.- Introducción
  El objeto de esta guía es explicar la manera de custodiar tus Bitcoins de la manera más segura y barata, utilizando un almacenamiento en frío y firmando las transacciones utilizando un PC seguro y desconectado de la red. Para consultar la cartera, utilizaremos el PC conectado a la red.
  
  Una cartera con Bitcoins consta de dos claves Maestras: la clave Pública y la clave Privada. La clave Pública permite sólo-lectura de los fondos de la cartera, mientras que la clave Privada permite acceder dichos fondos y transferirlos. Conociendo la clave Privada, se puede conocer la clave Pública, pero nunca al revés. Por todo esto, la clave Privada debe custodiarse de manera muy segura, mientras que con la Pública podemos ser un poco menos precavidos ya que si alguien la obtuviera, podría ver cuáles son nuestros fondos, pero nunca obtenerlos.
  
Para facilitar el almacenamiento de esta clave privada, se utilizan las Seeds o semillas, que son una serie de 12 o 24 palabras que sirven para obtener la clave privada y restaurar la cartera. Esta semilla va unida a una Passphrase o palabra clave, que sería como la palabra 13 o 25. Con una misma semilla, cada Passphrase generaría una cartera diferente. Esto permite que almacenemos de forma segura una semilla y luego memoricemos la Passphrase o la almacenemos en un sitio diferente, por lo que si alguien accede a la semilla, necesita conocer tambien la Passphrase para acceder a los fondos. Con una misma semilla, podemos tener varias Passphrases, por lo que tendríamos diferentes carteras, pero una única semilla.
MUY IMPORTANTE NO PERDER NUNCA LA SEMILLA Y LA PASSPHRASE, AMBAS NECESARIAS PARA RECUPERAR LA CARTERA.
  
  En lugar de utilizar un PC con Windows, que consideramos inseguro y propenso a virus/spyware/hackers, utilizaremos dos pendrives con el sistema operativo securizado Linux TAILS en cada uno de ellos. Uno de ellos con la conexión a Internet configurada (conteniendo sólo la clave Pública, para poder ver los fondos en sólo-lectura, y generar transacciones sin firmar), y el otro sin conexión a Internet offline (donde guardaremos la clave Privada, y firmaremos las transacciones que haremos en el pendrive con la clave Pública). 
Si asumimos el riesgo de que alguien pueda conocer nuestros fondos (pero no moverlos), tambien podríamos cargar la clave pública en una cartera en Windows o Android/iOS para mayor usabilidad.
  
No necesitamos un ordenador aparte dedicado, estos pendrives podremos cargarlos en cualquier PC o portátil que tengamos disponible. Se trata de un Linux que carga desde el pendrive y no accede ni cambia nada en el ordenador donde se arranca. Tras apagarlo no queda ningún rasto, ni pueden acceder a él virus que haya en el Windows instalado de ese mismo PC.
  
2.- Requisitos
  -2x pendrive de 8Gb mínimo (los llamaremos "Pendrive 1 OFFLINE" y Pendrive 2 ONLINE").
  -1x pendrive de 64Mb mínimo (lo llamaremos "Pendrive 3").
  -1x ordenador con conexión a internet.

3-. Preparación previa
  3.1.- Accedemos a la web de Github de segwitaddress.org (es un generador de semilla HD para direcciones Segwit) dirigiendonos a https://github.com/coinables/segwitaddress/releases . Nos descargamos la última versión que haya, el fichero "Source Code.zip". Lo descargamos en "Pendrive 3" y lo descomprimimos en el mismo pendrive.
  
  3.2.- Accedemos a la web de TAILS (https://tails.boum.org), vamos al menú "Obtener TAILS", click en instalar desde Windows, y seguimos los pasos para descargar el fichero de imagen (fichero .img). Hacemos click en Verificar la descarga. Continuamos descargando el programa Etcher, y grabamos el Pendrive 1 siguiendo las instrucciones. Repetimos el grabado de la misma imagen sobre el Pendrive 2.
  

  







