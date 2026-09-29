# Configuración del router

## Operatividad del router

Un router es un ordenador construido para desempeñar funciones específicas de capa tres, proporciona el hardware y software necesarios para encaminar paquetes entre redes. Se trata de dispositivos importantes de interconexión que permiten conectar subredes LAN y establecer conexiones de área amplia entre las subredes.

Las dos tareas principales son las de conmutar los paquetes desde una interfaz perteneciente a una red hacia otra interfaz de una red diferente y la de enrutar, es decir, encontrar el mejor camino hacia la red destino. Además de estas funciones los routers pueden llevar a cabo diferentes desempeños, tales como filtrados, dominios de colisión y broadcast, direccionamiento y traslación de direcciones IP, enlaces troncales, etc.

Además de los componentes de hardware los routers también necesitan un sistema operativo, los routers Cisco funcionan con un sistema operativo llamado IOS (*Internetwork Operating System*). Un router puede ser exclusivamente un dispositivo LAN, o puede ser exclusivamente un dispositivo WAN, pero también puede estar en la frontera entre una LAN y una WAN y ser un dispositivo LAN y WAN al mismo tiempo.

### Componentes principales de un router

Los componentes básicos de la arquitectura interna de un router comprenden:

- **CPU:** unidad central de procesamiento, es un microprocesador que ejecuta las instrucciones del sistema operativo. Estas funciones incluyen la inicialización del sistema, las funciones de enrutamiento y el control de la interfaz de red. Los grandes routers pueden tener varias CPU.
- **RAM:** memoria de acceso aleatorio, se usa para la información de las tablas de enrutamiento, el caché de conmutación rápida, la configuración actual y las colas de paquetes. En la mayoría de los routers, la RAM proporciona espacio de tiempo de ejecución para el software IOS de Cisco y sus subsistemas. El contenido de la RAM se pierde cuando se apaga la unidad. En general, la RAM es una memoria de acceso aleatorio dinámica (DRAM) y puede ampliarse agregando más módulos de memoria en línea doble (DIMM).
- **Memoria flash:** se utiliza para almacenar una imagen completa del software IOS de Cisco. Normalmente el router adquiere el IOS por defecto de la memoria flash. Estas imágenes pueden actualizarse cargando una nueva imagen en la memoria flash. El IOS puede estar comprimido o no. En la mayoría de los routers, una copia ejecutable del IOS se transfiere a la RAM durante el proceso de arranque. En otros routers, el IOS puede ejecutarse directamente desde la memoria flash. Agregando o reemplazando los módulos de memoria en línea simples flash (SIMM) o las tarjetas PCMCIA se puede ampliar la cantidad de memoria flash.
- **NVRAM:** memoria de acceso aleatorio no volátil, se utiliza para guardar la configuración de inicio. En algunos dispositivos, la NVRAM se implementa utilizando distintas memorias de solo lectura programables, que se pueden borrar electrónicamente (EEPROM). En otros dispositivos, se implementa en el mismo dispositivo de memoria flash desde donde se cargó el código de arranque. En cualquiera de los casos, estos dispositivos retienen sus contenidos cuando se apaga la unidad.
- **Buses:** la mayoría de los routers contienen un bus de sistema y un bus de CPU. El bus de sistema se usa para la comunicación entre la CPU y las interfaces y/o ranuras de expansión. Este bus transfiere los paquetes hacia y desde las interfaces. La CPU usa el bus para tener acceso a los componentes desde el almacenamiento del router. Este bus transfiere las instrucciones y los datos hacia o desde las direcciones de memoria especificadas.
- **ROM:** memoria de solo lectura, se utiliza para almacenar de forma permanente el código de diagnóstico de inicio (Monitor de ROM). Las tareas principales de la ROM son el diagnóstico del hardware durante el arranque del router y la carga del software IOS de Cisco desde la memoria flash a la RAM. Algunos routers también tienen una versión más básica del IOS que puede usarse como fuente alternativa de arranque. Las memorias ROM no se pueden borrar. Solo pueden actualizarse reemplazando los chips de ROM en los routers.
- **Fuente de alimentación:** brinda la energía necesaria para operar los componentes internos. Los routers de mayor tamaño pueden contar con varias fuentes de alimentación o fuentes modulares. En algunos de los routers de menor tamaño, la fuente de alimentación puede ser externa al router.

### Tipos de interfaces

Las interfaces son las conexiones físicas de los routers con el exterior. Los tres tipos de interfaces características son:

- Interfaz de red de área local (LAN).
- Interfaz de red de área amplia (WAN).
- Interfaz de consola/AUX.

Estas interfaces tienen chips controladores que proporcionan la lógica necesaria para conectar el sistema a los medios. Las interfaces LAN pueden ser configuraciones fijas o modulares y pueden ser Ethernet o Token Ring. Las interfaces WAN incluyen la Unidad de servicio de canal (CSU) integrada, la RDSI y el serial. Al igual que las interfaces LAN, las interfaces WAN también cuentan con chips controladores para las interfaces. Las interfaces WAN pueden ser de configuraciones fijas o modulares. Los puertos de consola/AUX y los USB son puertos que se utilizan principalmente para la configuración inicial del router. Estos puertos no son puertos de red. Se usan para realizar sesiones terminales desde los puertos de comunicación del ordenador o a través de un módem.

### WAN y routers

La capa física WAN describe la interfaz entre el equipo terminal de datos (DTE) y el equipo de transmisión de datos (DCE). Normalmente el DCE es el proveedor del servicio, mientras que el DTE es el dispositivo localmente conectado. En este modelo, los servicios ofrecidos al DTE están disponibles a través de un módem o CSU/DSU.

Cuando un router usa los protocolos y los estándares de la capa de enlace de datos y física asociados con las WAN, opera como dispositivo WAN.

Los protocolos y estándares de la capa física WAN son:

- EIA/TIA-232
- EIA/TIA-449
- V.24
- V.35
- X.21
- G.703
- EIA-530
- RDSI
- T1, T3, E1 y E3
- xDSL
- SONET (OC-3, OC-12, OC-48, OC-192)

Los protocolos y estándares de la capa de enlace de datos WAN:

- Control de enlace de datos de alto nivel (HDLC)
- Frame-Relay
- Protocolo punto a punto (PPP)
- Control de enlace de datos síncrono (SDLC)
- Protocolo Internet de enlace serial (SLIP)
- X.25
- ATM
- LAPB
- LAPD
- LAPF

## Instalación inicial

En la instalación inicial, el administrador de la red configura generalmente los dispositivos de la red desde un terminal de consola, conectado a través del puerto de consola. Posteriormente y una vez configurados ciertos parámetros mínimos el router puede ser configurado desde distintas ubicaciones:

- Si el administrador debe dar soporte a dispositivos remotos, una conexión local por módem con el puerto auxiliar del dispositivo permite a aquél configurar los dispositivos de red.
- Dispositivos con direcciones IP establecidas pueden permitir conexiones Telnet para la tarea de configuración.
- Descargar un archivo de configuración de un servidor TFTP (*Trivial File Transfer Protocol*).
- Configurar el dispositivo por medio de un navegador HTTP (*Hypertext Transfer Protocol*).

### Conectándose por primera vez

Para la configuración inicial del router se utiliza el puerto de consola conectado a un cable transpuesto o de consola y un adaptador RJ-45 a DB-9 o adaptador USB para conectarse al puerto COM1 del ordenador o a un puerto USB del mismo. Este debe tener instalado un software de emulación de terminal.

Los parámetros de configuración son los siguientes:

- El puerto COM adecuado.
- 9600 baudios.
- 8 bits de datos.
- Sin paridad.
- 1 bit de parada.
- Sin control de flujo.

Para utilizar la opción del puerto USB para la configuración inicial, tome en cuenta que posiblemente necesitará un driver controlador en su PC según el sistema operativo que utilice. Para las conexiones desde su PC al puerto USB, posiblemente también necesite un cable adaptador.

### Rutinas de inicio

Cuando un router o un switch Catalyst Cisco se ponen en marcha, hay tres operaciones fundamentales que han de llevarse a cabo en el dispositivo de red:

1. El dispositivo localiza el hardware y lleva a cabo una serie de rutinas de detección del mismo. Un término que se suele utilizar para describir este conjunto inicial de rutinas es el POST (*Power-on Self Test*), o pruebas de inicio.
2. Una vez que el hardware se muestra en una disposición correcta de funcionamiento, el dispositivo lleva a cabo rutinas de inicio del sistema. El switch o el router inicia localizando y cargando el software del sistema operativo IOS secuencialmente desde la Flash, servidor TFTP o la ROM, según corresponda.
3. Tras cargar el sistema operativo, el dispositivo trata de localizar y aplicar las opciones de configuración que definen los detalles necesarios para operar en la red. Generalmente, hay una secuencia de rutinas de arranque que proporcionan alternativas al inicio del software cuando es necesario.

### Comandos ayuda

El router proporciona la posibilidad de ayudas pues resulta difícil memorizar todos los comandos disponibles, el signo de interrogación (`?`) y el tabulador del teclado brindan la ayuda necesaria a ese efecto. El tabulador completa los comandos que no recordamos completos o que no queremos escribir en su totalidad.

El `?` colocado inmediatamente después de un comando muestra todos los que comienzan con esas letras, colocado después de un espacio (barra espaciadora+`?`) lista todos los comandos que se pueden ejecutar en esa posición.

La ayuda se puede ejecutar desde cualquier modo:

```text
Router#?
Exec commands:
  access-enable   Create a temporary Access-List entry
  access-template Create a temporary Access-List entry
  bfe             For manual emergency modes setting
  clear           Reset functions
--More--

Router(config)#?
Configure commands:
  aaa        Authentication, Authorization and Accounting.
  alias      Create command alias
  appletalk  Appletalk global configuration commands
  arp        Set a static ARP entry
--More--
```

Inmediatamente, o después de un espacio, según la ayuda solicitada:

```text
Router#sh?
Show

Router#show ?
  access-expression List access expression
  access-lists       List access lists
  accounting         Accounting data for active sessions
  aliases            Display alias commands
--More--

Router(config)#inte?
interface

Router(config)#interface ?
  CTunnel         CTunnel interface
  FastEthernet    FastEthernet IEEE 802.3
  GigabitEthernet GigabitEthernet IEEE 802.3z
  Loopback        Loopback interface
  Null            Null interface
  Port-channel    Ethernet Channel of interfaces
  Tunnel          Tunnel interface
  Vif             PGM Multicast Host interface
  Vlan            Catalyst Vlans
  fcpa            Fiber Channel
  range           interface range command
```

La indicación `--More--` significa que existe más información disponible. La barra espaciadora pasará de página en página, mientras que el Intro lo hará línea por línea.

El acento circunflejo (`^`) indicará un fallo de escritura en un comando:

```text
Router#configure terbinal
                   ^
% Invalid input detected at '^' marker.
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#
```

Estos comandos quedan registrados en un búfer llamado historial y pueden verse con el comando `show history`, por defecto la cantidad de comandos que se guardan en memoria es de 10, pero puede ser modificado por el administrador utilizando el `history size`:

```text
Router#terminal history size ?
  <0-256>  Size of history buffer

Router#show history
en
conf t
show arp
ping 10.0.0.1
copy run star
show history
```

### Comandos de edición

Las diferentes versiones de IOS ofrecen combinaciones de teclas que permiten una configuración del dispositivo más rápida y simple. La siguiente tabla muestra algunos de los comandos de edición más utilizados.

| Tecla | Efecto |
| --- | --- |
| Delete | Elimina un carácter a la derecha del cursor. |
| Retroceso | Elimina un carácter a la izquierda del cursor. |
| TAB | Completa un comando parcial. |
| Ctrl+A | Mueve el cursor al comienzo de la línea. |
| Ctrl+R | Vuelve a mostrar una línea escrita anteriormente. |
| Ctrl+U | Borra una línea. |
| Ctrl+W | Borra una palabra. |
| Ctrl+Z | Finaliza el modo de configuración y vuelve al modo EXEC. |
| Esc-B | Desplaza el cursor hacia atrás una palabra. |
| Flecha arriba / Ctrl+P | Repite hacia adelante los comandos anteriores. |
| Flecha abajo / Ctrl+N | Repite hacia atrás los comandos anteriores. |
| Flecha derecha / Ctrl+F | Desplaza el cursor hacia la derecha sin borrar caracteres. |
| Flecha izquierda / Ctrl+B | Desplaza el cursor hacia la izquierda sin borrar caracteres. |

## Configuración inicial

Un router o un switch pueden ser configurados desde distintas ubicaciones, una vez configurados ciertos parámetros mínimos el router puede ser configurado desde distintas ubicaciones:

- Si el administrador debe dar soporte a dispositivos remotos, una conexión local por módem con el puerto auxiliar del dispositivo permite a aquél configurar los dispositivos de red (según modelo y antigüedad).
- En los equipos más modernos con una configuración básica y desde cualquier sitio de la red el dispositivo puede cargar la configuración a través de algún servidor de gestión centralizada.
- Dispositivos con direcciones IP establecidas pueden permitir conexiones Telnet para la tarea de configuración.
- Descargar un archivo de configuración de un servidor TFTP (*Trivial File Transfer Protocol*).
- Configurar el dispositivo por medio de un navegador HTTP (*Hypertext Transfer Protocol*).

Las rutinas de inicio del software Cisco IOS tienen por objetivo inicializar las operaciones del router. Las rutinas de puesta en marcha deben hacer lo siguiente:

- Asegurarse que el router cuenta con hardware verificado (POST).
- Localizar y cargar el software Cisco IOS que usa el router para su sistema operativo.
- Localizar y aplicar las instrucciones de configuración relativas a los atributos específicos del router, funciones del protocolo y direcciones de interfaz.

El router se asegura de que el hardware haya sido verificado. Cuando un router Cisco se enciende, realiza unas pruebas al inicio (POST). Durante este autotest, el router ejecuta una serie de diagnósticos para verificar la operatividad básica de la CPU, la memoria y la circuitería de la interfaz. Tras verificar que el hardware ha sido probado, el router procede con la inicialización del software.

Al iniciar por primera vez un router Cisco, no existe configuración inicial alguna. El software del router le pedirá un conjunto mínimo de detalles a través de un diálogo opcional llamado Setup.

El modo Setup es el modo en el que inicia un router no configurado al arrancar, puede mostrarse en su forma básica o extendida. Se puede salir de este modo respondiendo que NO a la pregunta inicial.

```text
Would you like to enter the initial configuration dialog? [yes]: No
Would you like to terminate autoinstall? [yes]: INTRO
```

Desde la línea de comandos el router se inicia en el modo EXEC usuario, las tareas que se pueden ejecutar en este modo son solo de verificación ya que NO se permiten cambios de configuración. En el modo EXEC privilegiado se realizan las tareas típicas de configuración.

Modo EXEC usuario y modo EXEC privilegiado respectivamente:

```text
Router>
Router#
```

Para pasar del modo usuario al privilegiado ejecute el comando `enable`, para regresar `disable`. Esto es posible porque no se ha configurado contraseña, de lo contrario sería requerida cada vez que se pasara al modo privilegiado.

```text
Router>
Router>enable
Router#disable
Router>
```

Modo global y de interfaz:

```text
Router#configure terminal
Router(config)#interface tipo número

Router>enable
Router#configure terminal
Router(config)#interface ethernet 0
Router(config-if)#exit
Router(config)#exit
Router#
```

Para pasar del modo privilegiado al global debe introducir el comando `configure terminal`, para pasar del modo global al de interfaz ejecute el comando `interface`. Para regresar un modo más atrás utilice el `exit` o `Control+Z` que lo llevará directamente al modo privilegiado.

### Comandos show

Saber utilizar e interpretar los comandos `show` permite el rápido diagnóstico de fallos, en modo usuario se permite la ejecución de los comandos show de forma restringida, desde el modo privilegiado la cantidad es ampliamente mayor.

| Comando | Descripción |
| --- | --- |
| `show interfaces` | Muestra las estadísticas completas de todas las interfaces del router. |
| `show controllers` | Muestra información específica de la interfaz de hardware. |
| `show hosts` | Muestra la lista en caché de los nombres de host y sus direcciones. |
| `show users` | Muestra todos los usuarios conectados al router. |
| `show sessions` | Muestra las conexiones de telnet efectuadas desde el router. |
| `show flash` | Muestra información acerca de la memoria flash (EEPROM) y qué archivos IOS se encuentran almacenados allí. |
| `show version` | Despliega información acerca del router y de la imagen de IOS y el valor del registro de configuración del router. |
| `show protocols` | Muestra el estado global y por interfaz de cualquier protocolo de capa 3 que haya sido configurado. |
| `show startup-config` | Muestra el archivo de configuración almacenado en la NVRAM. |
| `show running-config` | Muestra el contenido del archivo de configuración activo. |
| `show processes` | Muestra los procesos que se están ejecutando en la CPU. |
| `show clock` | Muestra la hora fijada en el router. |
| `show arp` | Muestra la tabla ARP del router. |
| `show history` | Muestra un historial de los comandos introducidos. |

**Comparativa de los comandos show disponibles en los modos usuario y privilegiado:**

```text
Router>show ?
  arp
  cdp
  class-map
  clock
  controllers
  crypto
  flash:
  frame-relay
  history
  hosts
  interfaces
  ip
  policy-map
  privilege
  protocols
  queue
  queueing
  sessions
  ssh
  tcp
  terminal
  users
  version
```

```text
Router#show ?
  aaa
  access-lists
  arp
  cdp
  class-map
  clock
  controllers
  crypto
  debugging
  dhcp
  file
  flash:
  frame-relay
  history
  hosts
  interfaces
  ip
  logging
  login
  ntp
  policy-map
  privilege
  processes
  protocols
  queue
  queueing
  running-config
  sessions
  snmp
  ssh
  startup-config
  tcp
  tech-support
  terminal
  users
  version
```

!!! note "NOTA"
    La información que aparece entre corchetes después de una pregunta es la que el router sugiere como válida. Bastará con aceptar con un Intro.

### Asignación de nombre y contraseñas

La primera tarea recomendable de configuración es asignar un nombre único y exclusivo en la red al router. Desde el modo de configuración global, ejecute el comando `hostname`.

```text
Router>enable
Router#configure terminal
Router(config)#hostname nombre

Router#configure terminal
Router(config)#hostname MADRID
MADRID(config)#
```

Los comandos `enable password` y `enable secret` se utilizan para restringir el acceso al modo EXEC privilegiado. El comando `enable password` se utiliza solo si no se ha configurado previamente `enable secret`.

Se recomienda habilitar siempre `enable secret`, ya que a diferencia de `enable password`, la contraseña estará siempre cifrada utilizando el algoritmo MD5 (*Message Digest 5*).

```text
Router>enable
Router#configure terminal
Router(config)#enable password contraseña
Router(config)#enable secret contraseña
```

En la siguiente sintaxis se copia parte de un `show running-config` donde se ha configurado como hostname del router MADRID y como contraseña `cisco` en la `enable secret` y la `enable password`. Abajo se ve cómo la contraseña secret aparece encriptada por defecto mientras que la otra se lee perfectamente.

```text
Router>enable
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#hostname MADRID
MADRID(config)#enable password cisco
MADRID(config)#enable secret cisco
MADRID#show running-config
hostname MADRID
!
enable secret 5 $1$EBMD$0rTOiN4QQab7s8AFzsSof/
enable password cisco
```

### Contraseñas de consola, auxiliar y telnet

Para configurar la contraseña para consola se debe acceder a la interfaz de consola con el comando `line console 0`:

```text
Router#configure terminal
Router(config)#line console 0
Router(config-line)#login
Router(config-line)#password contraseña
```

El comando `exec-timeout` permite configurar un tiempo de desconexión determinado en la interfaz de consola. El comando `logging synchronous` impedirá mensajes dirigidos a la consola de configuración que pueden resultar molestos.

Para configurar la contraseña para telnet se debe acceder a la interfaz de telnet con el comando `line vty 0 4`, donde `line vty` indica dicha interfaz, `0` el número de la interfaz y `4` la cantidad máxima de conexiones múltiples a partir de 0, en este caso se permiten 5 conexiones múltiples:

```text
Router#configure terminal
Router(config)#line vty 0 4
Router(config-line)#login
Router(config-line)#password contraseña
```

El comando `show sessions` muestra las conexiones de telnet efectuadas desde el router, el comando `show users` muestra las conexiones de usuarios remotos.

```text
Router#show users
Line       User       Host(s)              Idle       Location
* 1 vty 0               idle                 00:00:00   192.168.59.132
  2 vty 1               idle                 00:00:02   192.168.59.156
Interface    User               Mode                     Idle      Peer Address

Router#show sessions
Conn Host Address         Byte  Idle  Conn Name
    1    10.99.59.49       10.99.59.49      0     1  10.99.59.49
*   2    10.99.55.1        10.99.55.1       0     0  10.99.55.1
```

Las diferentes sesiones de Telnet abiertas en un router pueden conmutarse con la secuencia de teclas `Ctrl+Shift+6` y luego `x`, regresar con 2 veces intro. El comando `clear line` desactivará una sesión de Telnet indeseada. Desde una conexión de consola, puede ejecutarse el comando `disconnect` para cancelar una conexión de un router remoto.

Para configurar la contraseña para auxiliar se debe acceder a la interfaz de auxiliar con el comando `line aux 0`:

```text
Router#configure terminal
Router(config)#line aux 0
Router(config-line)#login
Router(config-line)#password contraseña
```

En todos los casos el comando `login` suele estar configurado por defecto, permite que el router pregunte la contraseña al intentar conectarse, con el comando `login local` el router preguntará qué usuario intenta entrar y su respectiva contraseña.

### Configuración de interfaces

Las interfaces de un router forman parte de las redes que están directamente conectadas al dispositivo. Estas interfaces activas deben llevar una dirección IP y su correspondiente máscara, como un host perteneciente a esa red.

Las interfaces de LAN pueden ser:

- Ethernet a 10 Mbps.
- FastEthernet a 100 Mbps.
- GigabitEthernet a 1000 Mbps.

Las secuencias de comandos para la configuración básica de una interfaz de LAN son los siguientes:

```text
Router(config)#interface tipo número
Router(config-if)#ip address dirección IP máscara
Router(config-if)#speed [10|100|1000|auto]
Router(config-if)#duplex [auto|full|half]
Router(config-if)#no shutdown
```

Las interfaces suelen estar deshabilitadas por defecto por el comando `shutdown`, para habilitarlas debe ejecutarse el comando `no shutdown` en el modo de interfaz.

La mayoría de dispositivos llevan ranuras o slots donde se instalan los módulos de interfaces o para ampliar la cantidad de estas. Los slots están numerados y se configuran por delante del número de interfaz separado por una barra.

```text
Router(config)#interface tipo slot/int
```

Las interfaces permiten la configuración de subinterfaces que pueden utilizarse como interfaces independientes pero dentro de un mismo espacio físico.

```text
Router(config)#interface tipo número.número de subinterfaz
```

Es posible configurar en la interfaz un texto a modo de comentario que solo tendrá carácter informativo y que no afecta al funcionamiento del router. Puede tener cierta importancia para los administradores a la hora de solucionar problemas.

```text
Router(config-if)#description comentario
```

El comando `show interfaces ethernet 0` muestra en la primera línea cómo la interfaz está UP administrativamente y UP físicamente. Recuerde que si la interfaz no estuviera conectada o si existiesen problemas de conectividad, el segundo UP aparecería como down. La tercera línea muestra la descripción configurada a modo de comentario. A continuación aparece la dirección IP, la encapsulación, paquetes enviados, recibidos, etc.

```text
Ethernet0 is up, line protocol is up
Hardware is Lance, address is 0000.0cfb.6c19 (bia 0000.0cfb.6c19)
Description: INTERFAZ_DE_LAN
Internet address is 192.168.1.1/24
MTU 1500 bytes, BW 10000 Kbit, DLY 1000 usec, rely 183/255, load 1/255
Encapsulation ARPA, loopback not set, keepalive set (10 sec)
ARP type: ARPA, ARP Timeout 04:00:00
Last input never, output 00:00:03, output hang never
Last clearing of "show interface" counters never
Queueing strategy: fifo
Output queue 0/40, 0 drops; input queue 0/75, 0 drops
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes, 0 no buffer
     Received 0 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 input packets with dribble condition detected
     188 packets output, 30385 bytes, 0 underruns
     188 output errors, 0 collisions, 2 interface resets
     0 babbles, 0 late collision, 0 deferred
     188 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out
```

Si el administrador deshabilita la interfaz se verá:

```text
Ethernet0 is administratively down, line protocol is down
```

!!! note "NOTA"
    Si una interfaz está administrativamente down no significa que exista un problema, pues el administrador ha decidido dejarla shutdown. Por el contrario si el line protocol is down existe un problema, seguramente de capa física.

Las interfaces seriales se configuran siguiendo el mismo proceso que las Ethernet, se debe tener especial cuidado para determinar quién es el DCE (*Data Communications Equipment*) y quién el DTE (*Data Terminal Equipment*) debido a que el DCE lleva el sincronismo de la comunicación, este se configurará solo en la interfaz serial del DCE, el comando `clock rate` activará el sincronismo en ese enlace.

```text
Router(config)#interface tipo número
Router(config-if)#ip address dirección IP máscara
Router(config-if)#clock rate [300-4000000]
```

`Clock rate` y ancho de banda no es lo mismo: recuerde que existe un comando `bandwidth` para la configuración del ancho de banda, el router solo lo utilizará para el cálculo de costes y métricas para los protocolos de enrutamiento, mientras que el `clock rate` brinda la verdadera velocidad del enlace.

```text
Router(config-if)#bandwidth ?
  <1-10000000>  Bandwidth in kilobits

MADRID(config)#interface serial 0/0
MADRID(config-if)#ip address 204.20.31.5 255.255.255.240
MADRID(config-if)#clock rate 56000
MADRID(config-if)#description interfaz de salida WEB
MADRID(config-if)#bandwidth 128000
MADRID(config-if)#no shutdown
```

Las interfaces loopback son interfaces virtuales que sirven, por ejemplo, para el cálculo de métrica en los protocolos de enrutamiento o a efectos de pruebas de conectividad.

```text
Router(config)#interface loopback ?
  <0-2147483647>  Loopback interface number
```

## Configuración avanzada

### Seguridad de acceso

La autenticación por usuario añade una función de seguridad. Hay dos métodos para configurar nombres de usuario de cuentas locales: `username password` y `username secret`.

```text
Router(config)#username usuario1 password contraseña1
Router(config)#username usuario2 password contraseña2
Router(config)#username usuario secret contraseña
```

El comando `username secret` es más seguro porque utiliza el algoritmo MD5 (*Message Digest 5*) para crear las claves.

```text
Router#show running-config
!
username ernesto secret 5 $1$aI44$fJoWcpIOAzTbkCd.bKxPS1
username matias password 0 contraseña
```

El comando `login local` en las configuraciones de línea habilita la base de datos local para autenticación.

```text
Router(config)#line vty 0 15
Router(config-line)#login local
Router(config-line)#password contraseña
```

Un añadido de seguridad es el comando `service password-encryption` que encripta con un cifrado leve las contraseñas que no están cifradas por defecto como las de telnet, consola, auxiliar, etc. Una vez cifradas las contraseñas no se podrán volver a leer en texto plano.

```text
MADRID(config)#line vty 0 4
MADRID(config-line)#password cisco
MADRID(config-line)#login
MADRID(config-line)#^Z
MADRID#
%SYS-5-CONFIG_I: Configured from console by console
MADRID#show running-config
Building configuration...
!
hostname MADRID !
line con 0
line vty 0 4
 password cisco
 login
MADRID#conf t
Enter configuration commands, one per line. End with CNTL/Z.
MADRID(config)#service password-encryption
MADRID(config)#^Z
MADRID#
%SYS-5-CONFIG_I: Configured from console by console
MADRID#show running-config
!
line con 0
line vty 0 4
 password 7 0822455D0A16
 login
!
```

!!! note "NOTA"
    Las contraseñas sin encriptación aparecen en texto plano en el `show running` debiendo tener especial cuidado ante la presencia de intrusos.

Los routers pueden ser configurados por HTTP si el comando `ip http server` está habilitado en el dispositivo. Por defecto la configuración por web viene deshabilitada y por razones de seguridad se recomienda dejarlo desactivado. Para habilitarlo se utiliza el siguiente comando.

```text
Router(config)#ip http server
```

### Mensajes o banners

Los banners son muy importantes para la red desde una perspectiva legal. Además de advertir a intrusos potenciales, los banners también pueden ser utilizados para informar a administradores remotos de las restricciones de uso.

Los banners están deshabilitados por defecto y deben ser habilitados explícitamente. Use el comando `banner` desde el modo de configuración global para especificar mensajes apropiados.

```text
Router(config)#banner ?
  LINE c  banner-text c, where 'c' is a delimiting character
  exec       Set EXEC process creation banner
  incoming   Set incoming terminal line banner
  login      Set login banner
  motd       Set Message of the Day banner
```

El banner motd es de poco uso en entornos de producción y se utiliza raramente. El banner exec, por el contrario, es útil para mostrar mensajes de administrador, ya que se presenta solo para los usuarios autenticados.

```text
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#banner exec#
Enter TEXT message. End with the character '#'.
+--------------------------------------------------------------+
| ADVERTENCIA                                                    |
| -------                                                        |
| Este sistema es para el uso exclusivo de los usuarios autorizados
| para fines oficiales. Usted no tiene ninguna autorización de su
| uso y para asegurarse de que el sistema funciona correctamente,
| las personas que administran esta red monitorizan toda la
| actividad. La utilización de este dispositivo sin consentimiento
| expreso revela evidencias de un posible abuso o actividad
| criminal denunciable a las autoridades competentes según las     |
| leyes vigentes.                                                |
+--------------------------------------------------------------+
#
```

### Configuración de SSH

SSH (*Secure Shell*) ha reemplazado a telnet como práctica recomendada para proveer administración remota con conexiones que soportan confidencialidad e integridad de la sesión. Provee una funcionalidad similar a una conexión telnet de salida, con la excepción de que la conexión está cifrada y opera en el puerto 22.

1. Configure la línea vty para que utilice nombres de usuarios locales con el comando `login local`.
2. Asegúrese de que haya una entrada de nombre de usuario válida en la base de datos local. Si no la hay, cree una usando el comando `username nombre secret contraseña`.
3. Deben generarse las claves secretas de una sola vía para que el router cifre el tráfico SSH. Estas claves se denominan claves asimétricas RSA (*Rivest, Shamir y Adleman*). Primero configure el nombre de dominio DNS de la red usando el comando `ip domain-name` en el modo de configuración global. Luego para crear la clave RSA, use el comando `crypto key generate rsa` en el modo de configuración global.
4. En muchas versiones actuales de IOS la configuración de las sesiones SSH viene configurada por defecto, sin embargo si fuera necesario habilite las sesiones SSH vty de entrada con el comando de línea vty `transport input ssh`. Para prevenir sesiones de telnet configure el comando `no transport input telnet` para todas las líneas vty.
5. De manera opcional puede configurarse la versión 2 de SSH con el comando de configuración global `ip ssh version 2`.

```text
Router#
Router#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#hostname CCNA
CCNA(config)#line vty 0 15
CCNA(config-line)#login local
CCNA(config-line)#transport input telnet ssh
CCNA(config-line)#exit
CCNA(config)#username ernesto secret cisco
CCNA(config)#ip domain-name aprenderedes.com
CCNA(config)#crypto key generate rsa
The name for the keys will be: ernesto.aprenderedes.com
Choose the size of the key modulus in the range of 360 to 2048 for your General Purpose Keys.
Choosing a key modulus greater than 512 may take a few minutes.
How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys ...[OK]
00:03:58: %SSH-5-ENABLED: SSH 1.99 has been enabled
```

Puede verificar el estado y las conexiones SSH con los comandos `show ip ssh` y `show ssh`.

```text
CCNA#show ip ssh
SSH Enabled - version 2.0
Authentication timeout: 120 secs; Authentication retries: 3

CCNA#show ssh
Connection  Version Mode Encryption    State         Username
          2.0     IN   DES              Session started ernesto
```

Será posible conectarse usando un cliente SSH público y disponible comercialmente ejecutándose en un host. Algunos ejemplos de estos clientes son PuTTY, OpenSSH y TeraTerm.

!!! tip "RECUERDE"
    El comando `username secret` cifra la contraseña del usuario por defecto mientras que el comando `username password` muestra la contraseña en texto plano. Ambos comandos tienen el mismo efecto en el dispositivo y permiten establecer niveles de cifrado.

!!! note "NOTA"
    Asegúrese de que los dispositivos destino estén ejecutando una imagen IOS que soporte SSH. Muchas versiones básicas o antiguas no lo soportan.

### Resolución de nombre de host

El DNS (*Domain Name System*) es una base de datos distribuida en la que se pueden asignar nombres de host a direcciones IPv4 e IPv6 a través del protocolo DNS desde un servidor DNS. Cada dirección IP única puede tener un nombre de host asociado. Seguramente resultará más familiar identificar un dispositivo, un host o un servidor con un nombre que lo asocie a sus funciones o a otros criterios de desempeño.

Por lo general, es más fácil referirse a los dispositivos de red mediante nombres en lugar de direcciones numéricas (servicios tales como Telnet pueden utilizar nombres de host o direcciones). Los nombres de host y direcciones IP se pueden asociar entre sí a través de medios estáticos o dinámicos.

Los routers Cisco permiten mapear estáticamente nombres de host con direcciones IPv4 o IPv6 acelerando el proceso de conversión de nombres a direcciones. Esto se hace creando una tabla de host, que asociará un nombre a una o varias direcciones IP. La asignación manual de nombres de host a direcciones es útil cuando el mapeo dinámico no está disponible.

```text
Router(config)#ip host nombre [1ª dirección IP][2ª dirección IP]...
```

Opcionalmente se puede especificar un nombre de dominio predeterminado que el software IOS utilizará para completar las solicitudes de nombres de dominio. Puede especificar un nombre de dominio o una lista de nombres de dominio.

Cualquier nombre de host que no contenga un nombre de dominio completo tendrá el nombre de dominio predeterminado que se añade a éste antes del propio nombre de host.

```text
Router(config)#ip domain name nombre
Router(config)#ip domain list nombre
```

Especifica uno o más hosts (hasta seis) que pueden funcionar como un servidor de nombres para suministrar información de nombre de DNS.

```text
Router(config)#ip name-server [1ª dirección IP][2ª dirección IP]...
```

DNS está activado por defecto. Si estuviese desactivado el siguiente comando habilita la traducción de direcciones basado en DNS.

```text
Router(config)#ip domain lookup [source-interface interface-type interface-number]
```

Una vez creada la tabla de host puede verse con el comando `show hosts`.

```text
CCNA#show hosts
Default Domain is not set
Name/address lookup uses domain service
Name servers are 255.255.255.255
Codes: UN - unknown, EX - expired, OK - OK, ?? - revalidate
       temp - temporary, perm - permanent
       NA - Not Applicable  None - Not defined
Host              Port  Flags  Age Type Address(es)
Impresora         None  (perm, OK)  0 IP  192.168.5.6
Router_Internet   None  (perm, OK)  0 IP  192.168.45.8
Servidor_Web      None  (perm, OK)  0 IP  192.168.1.33
Catalyst          None  (perm, OK)  0 IP  10.1.55.3
                                    10.1.2.3
```

El siguiente es un ejemplo de salida del `debug domain` que corresponde a una consulta DNS de la tabla de host local cuando el dispositivo está configurado como servidor.

```text
Apr 4 22:16:35.279: DNS: Incoming UDP query (id#8409)
Apr 4 22:16:35.279: DNS: Type 1 DNS query (id#8409) for host 'ns1.example.com' from 192.0.2.120(1279)
Apr 4 22:16:35.279: DNS: Finished processing query (id#8409) in 0.000 secs
```

A partir de la creación de la tabla de host pueden ejecutarse comandos reemplazando las direcciones IP de los hosts contenidos en la tabla por el nombre del mismo.

```text
CCNA#ping Impresora
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.5.6, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 0/12/16 ms
```

### Guardar la configuración

Las configuraciones actuales son almacenadas en la memoria RAM, este tipo de memoria pierde el contenido al apagarse el router. Para que esto no ocurra es necesario poder hacer una copia a la NVRAM. El comando `copy` se utiliza con esta finalidad, identificando un origen con datos a guardar y un destino donde se almacenarán esos datos. Se puede guardar la configuración de la RAM a la NVRAM, de la RAM a un servidor TFTP, etc.

Copia de la RAM a la NVRAM:

```text
Router#copy running-config startup-config
```

Copia de la NVRAM a la RAM:

```text
Router#copy startup-config running-config
```

```text
Router#copy ?
  flash:         Copy from flash: file system
  ftp:           Copy from ftp: file system
  running-config Copy from current system configuration
  startup-config Copy from startup configuration
  tftp:          Copy from tftp: file system

Router#copy running-config ?
  flash:         Copy to flash file
  ftp:           Copy to current system configuration
  startup-config Copy to startup configuration
  tftp:          Copy to current system configuration

Router#copy running-config startup-config
Destination filename [startup-config]?
Building configuration...
[OK]
```

Para la copia a un servidor TFTP se debe tener como mínimo una conexión de red activa hacia el servidor (verifique la conexión a través de un `ping`); se solicitará el nombre de archivo con el que se guardará la configuración y la dirección IP del servidor.

```text
CCNA#ping 192.168.1.25
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.25, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 31/31/32 ms

CCNA#copy running-config tftp
Address or name of remote host []? 192.168.1.25
Destination filename [CCNA-confg]?
Writing running-config....!!!!!!!!!!!!!!!!
[OK - 1080 bytes]
1080 bytes copied in 3.074 secs (0 bytes/sec)
```

!!! tip "RECUERDE"
    El comando `copy` identifica un origen y un destino para los datos a guardar. El resultado de la copia sobrescribe los datos existentes, por lo tanto se debe tener especial atención asegurándose de que los datos que se copiarán son los correctos y que no se eliminarán datos sensibles.

Los siguientes comandos muestran el contenido de la RAM y de la NVRAM respectivamente.

```text
Router#show running-config
Router#show startup-config
```

A continuación se copia parte de un `show startup-config`, se observa entre otras cosas en la primera línea la cantidad de memoria y la que se está utilizando, luego la versión del software IOS:

```text
CCNA#show startup-config
Building configuration...
Using 886 out of 131066 bytes
!
version 11.2
no service password-encryption
no service udp-small-servers
no service tcp-small-servers
!
hostname MADRID
!
enable secret 5 $1$EBMD$0rTOiN4QQab7s8AFzsSof/
enable password cisco
!
ip host SERVIDOR_WEB 204.200.1.2
ip host ROUTER_A 220.220.10.32
ip host HOST_ADMIN 210.210.2.22
!
interface Ethernet0
 description INTERFAZ_DE_LAN
 ip address 192.168.1.1 255.255.255.0
 shutdown
!
interface Ethernet1
 no ip address
--More--
```

!!! note "NOTA"
    La memoria RAM es la `running-config`, su contenido se pierde al apagar y no existe comando para borrado. La memoria NVRAM es la `startup-config`, no pierde su contenido al apagar.

### Borrado de las memorias

Los datos de configuración almacenados en la memoria no volátil no son afectados por la falta de alimentación, el contenido permanecerá en la NVRAM hasta tanto se ejecute el comando `erase` para su eliminación:

```text
Router#erase startup-config
Router#erase startup-config
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
```

Por el contrario no existe comando para borrar el contenido de la RAM. Si el administrador pretende dejar sin ningún dato de configuración debe reiniciar o apagar el router. La RAM se borra únicamente ante la falta de alimentación eléctrica:

```text
Router#reload
System configuration has been modified. Save? [yes/no]: no
Proceed with reload? [confirm]
```

Para borrar completamente la configuración responda NO a la pregunta si quiere salvar.

!!! note "NOTA"
    Tenga especial cuidado al borrar las memorias, asegúrese de eliminar lo que desea antes de confirmar el borrado.

### Copia de seguridad del Cisco IOS

Cuando sea necesario restaurar o actualizar el IOS se debe hacer desde un servidor TFTP. Es importante que se guarden copias de seguridad de todas las IOS en un servidor central.

El comando para esta tarea es el `copy flash tftp`, verifique el nombre del archivo a guardar mediante el comando `show flash`:

```text
Router#show flash
System flash directory:
File Length Name/status
  3 33591768 c2900-universalk9-mz.SPA.151-4.M4.bin
  2 28282 sigdef-category.xml
  1 227537 sigdef-default.xml
[33847587 bytes used, 221896413 available, 255744000 total]
249856K bytes of processor board System flash (Read/Write)

Router#copy flash tftp
Source filename []? c2900-universalk9-mz.SPA.151-4.M4.bin
Address or name of remote host []? 192.168.1.25
Destination filename [c2900-universalk9-mz.SPA.151-4.M4.bin]?
Writing c2900-universalk9-mz.SPA.151-4.M4.bin...!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
[OK - 33591768 bytes]
33591768 bytes copied in 3.564 secs (9425000 bytes/sec)
```

En el proceso inverso al anterior puede utilizarse para IOS corruptas que necesiten ser restablecidas o para actualizar la versión del IOS. Es importante verificar si existe espacio suficiente en la memoria flash antes de iniciar el proceso de copiado con el comando `show flash`. El comando `copy tftp flash` inicia la copia desde el servidor TFTP. El dispositivo pedirá confirmación del borrado antes de copiar en la memoria.

```text
Router#show flash
System flash directory:
File Length Name/status
  3 33591768 c2900-universalk9-mz.SPA.151-4.M4.bin
  2 28282 sigdef-category.xml
  1 227537 sigdef-default.xml
[33847587 bytes used, 221896413 available, 255744000 total]
249856K bytes of processor board System flash (Read/Write)

Router#copy tftp flash
Address or name of remote host []? 192.168.1.25
Source filename []? c2900-universalk9-mz.SPA.151-4.M4.bin
Destination filename [c2900-universalk9-mz.SPA.151-4.M4.bin]?
%Warning:There is a file already existing with this name
Do you want to over write? [confirm]
Erase flash: before copying? [confirm]
Erasing the flash filesystem will remove all files! Continue? [confirm]
Erasing device...
eeee...erased
Erase of flash: complete
Accessing tftp://192.168.1.25/c2900-universalk9-mz.SPA.151-4.M4.bin...
Loading c2900-universalk9-mz.SPA.151-4.M4.bin from 192.168.1.25:
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
[OK - 33591768 bytes]
33591768 bytes copied in 0.569 secs (6198588 bytes/sec)
```

### Preferencia de carga del Cisco IOS

Los comandos `boot system` especifican el nombre y la ubicación de la imagen IOS que se debe cargar.

Indica al router que debe arrancar utilizando la IOS que está ubicada en la memoria flash.

```text
Router(config)#boot system flash nombre_archivo
```

Indica al router que debe buscar la IOS en la memoria ROM.

```text
Router(config)#boot system rom
```

Indica al router que al arrancar cargue la imagen IOS de un servidor TFTP.

```text
Router(config)#boot system tftp nombre_archivo IP_servidor
```

!!! note "NOTA"
    Si no existen comandos `boot system` en la configuración, el router carga por omisión el primer archivo encontrado en la memoria flash y lo ejecuta.

### Registro de configuración

Cuando un router arranca, se comprueba el registro de configuración virtual para determinar (entre otras cosas) el modo en que debe entrar tras el arranque, dónde conseguir la imagen del software y cómo gestionar el archivo de configuración de la NVRAM.

Este registro de 16 bits controla funciones como la velocidad en baudios del puerto de la consola, la operación de carga del software, la habilitación o deshabilitación de la tecla de interrupción durante las operaciones normales, la dirección de multidifusión predeterminada, así como establecer una fuente para arrancar el router.

El comando `show version` muestra la información de hardware y de IOS de un router o switch, sobre las últimas líneas se observa el valor del registro de configuración. El valor del registro para una secuencia de arranque normal debe ser `0x2102` (el `0x` indica un valor hexadecimal).

```text
Router#show version
Cisco IOS Software, C2900 Software (C2900-UNIVERSALK9-M), Version 15.0(1)M1, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2009 by Cisco Systems, Inc.
Compiled Wed 02-Dec-09 15:23 by prod_rel_team
ROM: System Bootstrap, Version 15.0(1r)M1, RELEASE SOFTWARE (fc1)
c2921-CCP-1-xfr uptime is 2 weeks, 22 hours, 15 minutes
System returned to ROM by reload at 06:06:52 PCTime Mon Apr 2 1900
System restarted at 06:08:03 PCTime Mon Apr 2 1900
System image file is "flash:c2900-universalk9-mz.SPA.150-1.M1.bin"
Last reload reason: Reload Command
................................................................
If you require further assistance please contact us by sending email to export@cisco.com.
Cisco CISCO2921/K9 (revision 1.0) with 475136K/49152K bytes of memory.
Processor board ID FHH1230P04Y
 1 DSL controller
 3 Gigabit Ethernet interfaces
 9 terminal lines
 1 Virtual Private Network (VPN) Module
 1 Cable Modem interface
 1 cisco Integrated Service Engine-2(s)
Cisco Foundation 2.2.1 in slot 1
DRAM configuration is 64 bits wide with parity enabled.
 255K bytes of non-volatile configuration memory.
248472K bytes of ATA System CompactFlash 0 (Read/Write)
 62720K bytes of ATA CompactFlash 1 (Read/Write)
Technology Package License Information for Module: 'c2900'
-----------------------------------------------------------------------------
Technology    Technology-package  Technology-package
   Current       Type               Next reboot
-----------------------------------------------------------------------------
ipbase         ipbasek9            Permanent ipbasek9
security       securityk9          Permanent securityk9
uc             uck9               Permanent uck9
data           datak9             Permanent datak9
Configuration register is 0x2102
```

Para cambiar el campo de arranque del registro de configuración, se hace desde el modo de configuración global, una vez ejecutado el comando se deberá reiniciar el router para que el cambio tenga efecto:

```text
Router#configure terminal
Router(config)#config-register 0x2142
```

El valor del registro de configuración se ha cambiado a `0x2142`, observe el siguiente `show`, el registro solo funcionará al reiniciar el router. Tenga en cuenta que el router preguntará si se desea guardar los cambios a lo que se deberá responder `Yes` con el fin de que quede almacenada dicha modificación.

```text
Router#show version
Cisco IOS Software, C2900 Software (C2900-UNIVERSALK9-M), Version 15.0(1)M1, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2009 by Cisco Systems, Inc.
Compiled Wed 02-Dec-09 15:23 by prod_rel_team
ROM: System Bootstrap, Version 15.0(1r)M1, RELEASE SOFTWARE (fc1)
.............................................................
DRAM configuration is 64 bits wide with parity enabled.
 255K bytes of non-volatile configuration memory.
248472K bytes of ATA System CompactFlash 0 (Read/Write)
 62720K bytes of ATA CompactFlash 1 (Read/Write)
Configuration register is 0x2142 (will be 0x2102 at next reload)

Router#reload
System configuration has been modified. Save? [yes/no]: yes
Building configuration...
[OK]
Proceed with reload? [confirm]
```

Existen gran cantidad de opciones de valores de registros de configuración, los más importantes a tener en cuenta son los siguientes:

- Para entrar al modo de monitor de la ROM, configure como el valor del registro de configuración `0xnnn0`. Arranque el sistema operativo manualmente. Para ello ejecute el comando `b` al estar en pantalla el indicador del modo monitor de la ROM.
- Para arrancar usando la primera imagen en memoria Flash, o para arrancar usando el IOS en memoria ROM (dependiendo de la plataforma), fije el registro de configuración en `0xnnn1`.
- Para configurar el sistema de modo que arranque automáticamente desde la NVRAM, fije el registro de configuración en cualquier valor entre `0xnnn2` y `0xnnnF`. El uso de los comandos `boot system` almacenados en la NVRAM es el esquema por defecto.

## Configuración de IPv6

### Dual-Stack

Una forma de implementar IPv6 en una empresa basada en IPv4 es la funcionalidad dual-stack. De esta forma los routers pueden ser configurados para enrutar paquetes de IPv6 e IPv4 al mismo tiempo independientemente del tipo de direccionamiento que implementen los host.

La funcionalidad dual-stack admite la configuración de IPv6 e IPv4 en una interfaz. No es necesario introducir comandos especiales para ello, basta con introducir los comandos de configuración de IPv4 y de IPv6 como lo que se hace normalmente. Será necesaria de manera independiente la configuración de una ruta predeterminada para IPv4 e IPv6.

### Configuración estática unicast

Los routers Cisco permiten implementar dos tipos de configuraciones estáticas IPv6:

- Configuración completa de 128 bits.
- Configuración EUI-64.

La configuración estática de la dirección completa es simple. La dirección puede estar abreviada o completa con sus 32 dígitos hexadecimales.

```text
Router(config)#interface tipo número
Router(config-if)#ipv6 address IPv6/prefijo
```

Para que los routers puedan enviar paquetes IPv6 deben tener habilitado el enrutamiento IPv6.

```text
Router(config)#ipv6 unicast-routing
```

Para verificar las configuraciones de las interfaces pueden utilizarse los siguientes comandos: `show ipv6 interface` y `show ipv6 interface brief`.

```text
Router#show ipv6 interface fastEthernet 0/0
FastEthernet0/0 is up, line protocol is down
IPv6 is enabled, link-local address is FE80::20A:F3FF:FE58:5101 [TEN]
No Virtual link-local address(es):
Global unicast address(es):
 2001:DB8:1111:1::1, subnet is 2001:DB8:1111:1::/64 [TEN]
Joined group address(es):
  FF02::1
  FF02::2
  FF02::1:FF00:1
  FF02::1:FF58:5101
MTU is 1500 bytes
ICMP error messages limited to one every 100 milliseconds
ICMP redirects are enabled
ICMP unreachables are sent
ND DAD is enabled, number of DAD attempts: 1
ND reachable time is 30000 milliseconds
ND advertised reachable time is 0 milliseconds
ND advertised retransmit interval is 0 milliseconds
ND router advertisements are sent every 200 seconds
ND router advertisements live for 1800 seconds
ND advertised default router preference is Medium
Hosts use stateless autoconfig for addresses.

Router#show ipv6 interface brief
FastEthernet0/0 [up/up]
  FE80::20A:F3FF:FE58:5101
  2001:DB8:1111:1::1
FastEthernet0/1 [administratively down/down]
Vlan1 [administratively down/down]
```

La configuración conocida como EUI-64 (*Extended Unique Identifier*) añade una palabra clave para que el router utilice las reglas EUI-64 junto con el prefijo de 64 bits. Cuando el router crea el identificador de interfaz utilizando las reglas EUI-64 sigue el siguiente proceso:

1. Divide la dirección MAC en dos partes iguales, de 6 dígitos hexadecimales.
2. Inserta entre las dos mitades `FFFE`, sumando un total de 16 dígitos hexadecimales.
3. Invierte el séptimo bit del identificador de la interfaz.

```text
Router(config)#interface tipo número
Router(config-if)#ipv6 address IPv6/prefijo eui-64
```

Al utilizar EUI-64, el valor de la dirección en el comando `ipv6 address` debe ser el del prefijo, y no la dirección completa de 128 bits. Sin embargo, si por error se escribe la dirección completa y se utiliza el parámetro `eui-64`, se acepta el comando convirtiendo la dirección al prefijo.

### Configuración dinámica unicast

Las interfaces de los routers Cisco soportan dos formas de configuración dinámica:

- **Stateful DHCP.**
- **SLAAC (*Stateless Address Autoconfiguration*).**

Estos comandos habilitan un mecanismo que le indica al router qué método utilizar para aprender sus IPv6. Cualquiera de los dos métodos se configura con el comando `ipv6 address`.

```text
Router(config)#interface tipo número
Router(config-if)#ipv6 address dhcp

Router(config)#interface tipo número
Router(config-if)#ipv6 address autoconfig
```

El mecanismo de asignación de direcciones de DHCP es básicamente similar en las dos versiones de IPv4 e IPv6. El funcionamiento preciso de DHCPv4 se detalla más adelante.

!!! note "NOTA"
    Para versiones anteriores de IOS el comando para la configuración del cliente DHCPv6 en una interfaz es `ipv6 dhcp client pd`.

### Configuración Link-Local

Cisco IOS crea automáticamente la dirección Link-local a partir de la configuración de la dirección IPv6 configurada en la interfaz. Si por ejemplo se ha configurado la interfaz con el parámetro EUI-64 el router calcula la porción perteneciente al identificador de la interfaz y le añade el prefijo `FE80::/10`.

```text
Router(config)#interface fastEthernet 0/0
Router(config-if)#ipv6 address 2001:0:1AB:5::/64 eui-64
Router(config-if)#no shutdown

Router#show ipv6 interface fastEthernet 0/0
FastEthernet0/0 is up, line protocol is up
IPv6 is enabled, link-local address is FE80::20A:F3FF:FE58:5101
No Virtual link-local address(es):
Global unicast address(es):
 2001:0:1AB:5:20A:F3FF:FE58:5101, subnet is 2001:0:1AB:5::/64 [EUI]
Joined group address(es):
  FF02::1
  FF02::2
  FF02::1:FF58:5101
MTU is 1500 bytes
ICMP error messages limited to one every 100 milliseconds
```

## Recuperación de contraseñas

La recuperación de contraseñas le permite alcanzar el control administrativo de su dispositivo si ha perdido u olvidado su contraseña. Para lograr esto necesita conseguir acceso físico al router, ingresar sin la contraseña, restaurar la configuración y restablecer la contraseña con un valor conocido.

1. Conecte un terminal o PC con software de emulación de terminal al puerto de consola del router. Acceda físicamente y apague el router.
2. Retire la memoria flash del slot y encienda el router. Para otros tipos de routers pulse la tecla de interrupción del terminal durante los primeros sesenta segundos del encendido del router. Normalmente la combinación de teclas control+pausa dará la señal de interrupción en el router. Aparecerá el símbolo `rommon>`. Si no aparece, el terminal no está enviando la señal de interrupción correcta. En este caso, compruebe la configuración del terminal o del emulador de terminal.
3. Introduzca el comando `confreg 0x2142` en el símbolo `rommon>` para arrancar desde la memoria flash e ignorar la NVRAM.
4. En el símbolo `rommon>` introduzca el comando `reset` para reiniciar el router. Esto hace que el router se reinicie pero ignore la configuración grabada en la NVRAM.
5. Siga los pasos de arranque normales. Aparecerá el símbolo `router>`.
6. La memoria RAM estará vacía, copie el contenido de la NVRAM a la RAM. De esta manera recuperará la configuración y también la contraseña no deseada. El nombre de router volverá a ser el original.

```text
Router#copy startup-config running-config
MADRID#
```

7. Cambie la contraseña no deseada por la conocida:

```text
MADRID#configure terminal
MADRID(config)#enable secret contraseña nueva
```

8. Guarde su nueva contraseña en la NVRAM, y si fuera necesario levante administrativamente las interfaces con el comando `no shutdown`:

```text
MADRID#copy running-config startup-config
```

9. Introduzca desde el modo global el comando `config-register 0x2102`.

10. Introduzca el comando `reload` en el símbolo del nivel EXEC privilegiado. Responda `Yes` a la pregunta para guardar el registro de configuración y confirme el reinicio:

```text
MADRID#reload
System configuration has been modified. Save? [yes/no]: yes
Building configuration...
[OK]
Proceed with reload? [confirm]
```

!!! warning "ATENCIÓN"
    Si por error ejecuta el comando inverso, es decir de la RAM a la NVRAM borrará todo el contenido de la startup-config dejando el dispositivo sin ningún tipo de configuración.

### Protección adicional de archivos y contraseñas

Si un intruso ganara acceso físico al router, podría tomar control del dispositivo a través del procedimiento de recuperación de contraseña. Si la configuración o la imagen del IOS se borran, el operador quizás nunca recupere una copia archivada para restaurar el router.

El comando `no service password-recovery` desactiva todos los accesos a la ROMMON, es un comando oculto de IOS y no tiene argumentos o palabras clave. Si se configura un router con este comando, se desactivan todos los accesos rommon impidiendo la recuperación de contraseñas por la vía tradicional.

```text
Router(config)#no service password-recovery
```

Durante la secuencia de inicio aparecerá el siguiente mensaje:

```text
PASSWORD RECOVERY FUNCTIONALITY IS DISABLED
```

Para recuperar un router luego de que se ingresa el comando `no service password-recovery`, se debe efectuar la secuencia interrupción dentro de los cinco segundos luego de que la imagen se descomprima durante el arranque y seguir las indicaciones del dispositivo.

```text
The password-recovery mechanism has been triggered, but
is currently disabled. Access to the boot loader prompt
through the password-recovery mechanism is disallowed at
this point. However, if you agree to let the system be
reset back to the default system configuration, access
to the boot loader prompt can still be allowed.
Would you like to reset the system back to the default configuration (y/n)?
```

Finalmente y luego de reiniciado el router puede deshabilitarse la seguridad ROMMON ejecutando el comando `service password-recovery`.

La función de *Resilient Configuration* del IOS de Cisco permite una recuperación más rápida si alguien reformatea la memoria flash o borra el archivo de configuración de inicio en la NVRAM. La copia segura de la configuración de inicio se almacena en la memoria flash junto con la imagen segura del IOS.

Hay dos comandos de configuración global disponibles para configurar las funciones de *Resilient Configuration* del IOS de Cisco:

- **`secure boot-image`:** habilita *Resilient Configuration* de la imagen del IOS. Cuando se configura por primera vez, se asegura la imagen actual, al mismo tiempo que se crea una entrada en el registro. Esta función puede ser deshabilitada solo por medio de una sesión de consola anteponiendo un `no` antes del comando.

```text
Router(config)#secure boot-image
%IOS_RESILIENCE-5-IMAGE_RESIL_ACTIVE: Successfully secured running image
```

- **`secure boot-config`:** permite registrar la configuración actual del router y archivarla de manera segura en el dispositivo de almacenamiento permanente. Se mostrará un mensaje del registro en la consola notificando al usuario que la función de adaptabilidad de la configuración ha sido activada. El archivo de configuración está oculto y no puede ser visto o eliminado directamente desde la CLI.

```text
Router(config)#secure boot-config
%IOS_RESILIENCE-5-CONFIG_RESIL_ACTIVE: Successfully secured config archive [flash:.runcfg-19930301-000255.ar]
```

Desde la CLI, el nombre de los archivos puede verse en la salida del comando `show secure bootset`. Restaure la configuración segura al nombre de archivo proporcionado usando el comando `secure boot-config restore` con el nombre de archivo correspondiente.

## Protocolos de descubrimiento

### CDP

El protocolo CDP (*Cisco Discovery Protocol*) se utiliza para obtener información de routers y switches que están conectados localmente. El CDP es un protocolo propietario de Cisco, destinado al descubrimiento de vecinos y es independiente de los medios y del protocolo de enrutamiento. Aunque el CDP solamente mostrará información sobre los vecinos conectados de forma directa, constituye una herramienta de gran utilidad.

El Protocolo de descubrimiento de Cisco (CDP) es un protocolo de capa 2 que conecta los medios físicos inferiores con los protocolos de red de las capas superiores. CDP viene habilitado por defecto en los dispositivos Cisco, los dispositivos de otras marcas serán transparentes para el protocolo. CDP envía actualizaciones por defecto cada 60 segundos y un tiempo de espera antes de dar por caído al vecino (holdtime) de 180 segundos.

#### Configuración

Como se explicó anteriormente CDP viene habilitado por defecto, sin embargo si fuera necesario configurarlo se ejecuta desde el modo global:

```text
Router(config)#cdp run
```

Hay dos formas de deshabilitar CDP, una es en una interfaz específica para que no funcione particularmente con las conexiones locales y la otra de forma general para que no funcione completamente en ninguna interfaz. Las sintaxis muestran los respectivos comandos desde una interfaz y de modo total.

```text
Router#configure terminal
Router(config)#interface tipo y número de interfaz
Router(config-if)#no cdp enable
Router(config)#no cdp run
```

El ajuste de los temporizadores se realiza con los siguientes comandos.

```text
Router(config)#cdp timer segundos
Router(config)#cdp holdtime segundos
```

La lectura del comando `show cdp neighbors detail` es idéntica al `show cdp entry *` e incluye la siguiente información bien detallada:

- Dirección IP del router vecino.
- Información del protocolo.
- Plataforma.
- Capacidad.
- ID del puerto.
- Tiempo de espera.
- La ID del dispositivo vecino.
- La interfaz local.

Los siguientes datos se agregan en el CDPv2:

- Administración de nombres de dominio VTP.
- VLAN nativas.
- Full o half-duplex.

#### Verificación

| Comando | Descripción |
| --- | --- |
| `show cdp neighbors` | Para obtener los nombres y tipos de plataforma de routers vecinos, nombres y versión de IOS. |
| `show cdp neighbors detail` | Para obtener datos de routers vecinos con más detalle. |
| `show cdp traffic` | Para saber el tráfico de CDP en el router. |
| `show cdp interface` | Muestra el estado de todas las interfaces que tienen activado CDP. |
| `clear cdp counters` | Restaura los contadores a cero. |
| `clear cdp table` | Borra la información contenida en la tabla de vecinos. |

Los siguientes comandos pueden utilizarse para mostrar la versión, la información de actualización, las tablas y el tráfico:

```text
show cdp traffic
show debugging
debug cdp adjacency
debug cdp events
debug cdp ip
debug cdp packets
cdp timer
cdp holdtime
show cdp
```

Ejemplo de `show cdp neighbors`:

```text
Router#sh cdp neighbors
Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone
Device ID        Local Intrfce Holdtme Capability Platform Port ID
Switch           Gig 0/1        155             S 3560    Fas 0/1
Router           Gig 0/0        135             R C2900   Gig 0/0
Router           Gig 0/2        165             R C1841   Fas 0/0
Phone            Gig 9/26       166             H P M     IP Phone Port 1
```

```text
R_2901#show cdp neighbors detail
-------------------------
Device ID: R_2901
Entry address(es):
  IP address : 192.168.1.2
Platform: cisco C2900, Capabilities: Router
Interface: GigabitEthernet0/0, Port ID (outgoing port): GigabitEthernet0/0
Holdtime: 168
Version :
  Cisco IOS Software, C2900 Software (C2900-UNIVERSALK9-M), Version 15.1(4)M4, RELEASE SOFTWARE (fc2)
  Technical Support: http://www.cisco.com/techsupport
  Copyright (c) 1986-2012 by Cisco Systems, Inc.
  Compiled Thurs 5-Jan-12 15:41 by pt_team
  advertisement version: 2
  Duplex: full
-------------------------
Device ID: AP99INSINTRV
Entry address(es):
  IP address: 10.99.165.30
  IPv6 address: FE80::32F7:DFF:FE5C:A791 (link-local)
Platform: cisco AIR-LAP1142N-E-K9, Capabilities: Trans-Bridge Source-Route-Bridge IGMP
Interface: GigabitEthernet2/3, Port ID (outgoing port): GigabitEthernet0
Holdtime : 174 sec
Version :
  Cisco IOS Software, C1140 Software (C1140-K9W8-M), Version 15.3(3)JA5, RELEASE SOFTWARE (fc1)
  Technical Support: http://www.cisco.com/techsupport
  Copyright (c) 1986-2015 by Cisco Systems, Inc.
  Compiled Thu 15-Oct-15 09:05 by prod_rel_team
  advertisement version: 2
  Duplex: full
  Power drawn: 15.400 Watts
  Power request id: 51424, Power management id: 2
  Power request levels are:15400 14500 0 0 0
Management address(es):
  IP address: 10.9.65.30
```

### LLDP

El protocolo LLDP (*Link Layer Discovery Protocol*) es similar a CDP pero se basa en el estándar IEEE 802.1ab. Como resultado LLDP funciona en redes de múltiples proveedores.

La información de los vecinos se anuncia mediante la agrupación de atributos en estructuras TLV (*Type-Length-Value*). Por ejemplo, un dispositivo puede anunciar su nombre de sistema con un TLV, su dirección de gestión en otro TLV, la descripción del puerto con otro TLV, sus requerimientos de energía en otro TLV, y así sucesivamente. Los anuncios LLDP de convierten en una cadena de varios TLV que pueden ser interpretados por el dispositivo receptor.

LLDP es compatible con los dispositivos que utilizan TLV adicionales tales como los teléfonos de VoIP, los LLDP-MED (*Media Endpoint Device*) proveen información más exacta acerca de las políticas de red, como número de VLAN, calidad de servicio necesaria para el tráfico de voz, administración de energía, la gestión de inventarios y datos de localización física.

LLDP soporta por defecto LLDP MED TLVs, pero no puede enviar simultáneamente la TLV básica y TLV-MED por un puerto del switch. LLDP envía solo los TLV básicos a los dispositivos conectados. Si un switch recibe un TLV-MED iniciara el envío de TLV-MED hacia el switch que iniciou el envío.

Por defecto el tiempo de actualización de los paquetes LLDP es de 30 segundos, el holdtime es de 120 segundos.

#### Configuración

Por defecto, LLDP está deshabilitado globalmente en un switch Catalyst. Para habilitarlo o deshabilitarlo utilice los siguientes comandos globales de configuración:

```text
Switch(config)#lldp run
Switch(config)#end

Switch(config)#no lldp run
Switch(config)#end
```

Una vez LLDP está habilitado, los anuncios se envían y reciben en cada interfaz del switch. Es posible controlar el funcionamiento LLDP en una interfaz determinada con el siguiente comando:

```text
Switch(config-if)# [no] lldp { receive | transmit }
```

#### Verificación

Para ver si se está ejecutando o no, utilice el comando `show lldp`.

```text
Switch1#show lldp neighbors [ type member/module/number ][ detail ]
```

Para obtener un resumen de los vecinos que han sido descubiertos:

```text
Switch1#show lldp neighbors
Capability codes:
  (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
  (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other
Device ID           Local Intf Hold-time Capability Port ID
Switch2             Gi1/0/24   113        B           Gi2/0/24
APb838              Gi1/0/23   91         B,R         Gi0
SEP2893FEA2E7F4     Gi1/0/22   180        B,T         2893FEA2E7F4:P1
Total entries displayed: 2
```

Para especificar un vecino descubierto por una interfaz determinada:

```text
Switch1#show lldp neighbors gig1/0/22 detail
------------------------------------------------
  Chassis id: 10.120.48.177
  Port id: 2893FEA2E7F4:P1
  Port Description: SW PORT
  System Name: SEP2893FEA2E7F4.voice.uky.edu
  System Description:
    Cisco IP Phone 7942G,V6, SCCP42.9-3-1-1S
  Time remaining: 124 seconds
  System Capabilities: B,T
  Enabled Capabilities: B,T
  Management Addresses:
    IP: 10.120.48.177
  Auto Negotiation - supported, enabled
  Physical media capabilities:
    1000baseT(HD)
    1000baseX(FD)
    Symm, Asym Pause(FD)
    Symm Pause(FD)
  Media Attachment Unit type: 16
  Vlan ID: - not advertised
  MED Information:
    MED Codes:
      (NP) Network Policy, (LI) Location Identification
      (PS) Power Source Entity, (PD) Power Device
      (IN) Inventory
    H/W revision: 6
    F/W revision: tnp42.8-3-1-21a.bin
    S/W revision: SCCP42.9-3-1-1S
    Serial number: FCH1414A0BA
    Manufacturer: Cisco Systems, Inc.
    Model: CP-7942G
    Capabilities: NP, PD, IN
    Device type: Endpoint Class III
    Network Policy(Voice): VLAN 837, tagged, Layer-2 priority: 5, DSCP: 46
    Network Policy(Voice Signal): VLAN 837, tagged, Layer-2 priority: 4, DSCP: 32
    PD device, Power source: Unknown, Power Priority: Unknown, Wattage: 6.3
    Location - not advertised
Total entries displayed: 1
```

!!! tip "RECUERDE"
    Ejecutar un proceso debug desmedido puede saturar al router o al switch hasta hacerlo inoperable. Termine el proceso debug con el comando `no debug all` o `undebug all`.

!!! note "NOTA"
    Los switches que utilizan LLDP pueden recoger información detallada de los dispositivos a medida que se unen o dejan la red o cambian de ubicación, exportando la información a través de Cisco MSE (*Management Services Engine*).

## DHCP

DHCP (*Dynamic Host Control Protocol*) desciende del antiguo protocolo BootP, permite a un servidor asignar automáticamente a un host direcciones IP y otros parámetros cuando está iniciándose. DHCP ofrece dos principales ventajas:

- DHCP permite que la administración de la red sea más fácil y versátil, evitando asignar manualmente el direccionamiento a todos los hosts, tarea bastante tediosa y que generalmente conlleva errores.
- DHCP asigna direcciones IP de manera temporal creando un mayor aprovechamiento del espacio en el direccionamiento.

El proceso DHCP sigue los siguientes pasos:

1. El cliente envía un broadcast preguntando por configuración IP a los servidores, DHCP discover.
2. Cada servidor en la red responderá con un Offer.
3. El cliente considera todas las ofertas y elije una. A partir de este momento el cliente envía un mensaje llamado Request.
4. El servidor responde con un ACK informando a su vez que toma conocimiento que el cliente se queda con esa dirección IP.
5. Finalmente, el cliente envía un ARP request para esa nueva dirección IP. Si alguien responde, el cliente sabrá que esa dirección está en uso y que ha sido asignada a otro cliente lo que iniciará el proceso DHCP nuevamente. Este paso se llama *Gratuitous ARP*.

Cuando se detecta un host con una dirección IP 169.254.X.X significa que no ha podido contactar con el servidor DHCP.

### Configuración del servidor DHCP

Los siguientes pasos describen la configuración de un router ejecutando IOS como servidor DHCP:

1. Crear un almacén (pool) de direcciones asignables a los clientes.

```text
Router(config)#ip dhcp pool nombre del pool
```

2. Determinar el direccionamiento de red y máscara para dicho pool.

```text
Router(config-dhcp)#network dirección IP máscara
```

3. Configurar el período que el cliente podrá disponer de esta dirección.

```text
Router(config-dhcp)#lease tiempo estipulado
```

4. Identificar el servidor DNS.

```text
Router(config-dhcp)#dns-server dirección IP
```

5. Identificar la puerta de enlace o gateway.

```text
Router(config-dhcp)#default-router dirección IP
```

6. Excluir si es necesario las direcciones que por seguridad o para evitar conflictos no se necesita que el DHCP otorgue.

```text
Router(config)#ip dhcp excluded-address IP inicio-IP fin
```

Las direcciones IP son siempre asignadas en la misma interfaz que tiene una IP dentro de ese pool. La siguiente sintaxis muestra un ejemplo de configuración dentro de ese contexto:

```text
Router(config)#interface fastethernet 0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config)#ip dhcp pool 1
Router(config-dhcp)#network 192.168.1.0 /24
Router(config-dhcp)#default-router 192.168.1.1
Router(config-dhcp)#lease 3
Router(config-dhcp)#dns-server 192.168.77.100
```

Algunos dispositivos IOS reciben direccionamiento IP en algunas interfaces y asignan direcciones IP en otras. Para estos casos DHCP puede importar las opciones y parámetros de una interfaz a otra. El siguiente comando para ejecutar esta acción es:

```text
Router(config-dhcp)#import all
```

Este comando es muy útil cuando se debe configurar DHCP en oficinas remotas. El router una vez localizado en su sitio puede determinar el DNS y las opciones locales.

Los servidores DHCP detectan conflictos utilizando `ping`, mientras que los clientes lo hacen con *Gratuitous ARP*. En cualquiera de los casos si se detecta un conflicto, la dirección se elimina del grupo y no será asignada hasta que un administrador resuelva el conflicto.

El comando `show ip dhcp conflict` muestra el método con el que se ha detectado el conflicto. El comando `clear ip dhcp conflict` permite al administrador borrar el conflicto de la lista para que el servidor pueda volver a ofrecer la dirección.

Los siguientes comandos muestran detalles de la configuración de DHCP: `show ip dhcp server statistics`, `show ip dhcp pool` y `show ip dhcp binding`.

```text
R1#show ip dhcp binding
Bindings from all pools not associated with VRF:
IP address      Client-ID/Hardware address/   Lease expiration   Type
                User name
192.168.1.101   0063.6973.636f.2d            May 12 2007 08:24 PM Automatic
192.168.1.111   0100.1517.1973.2c            May 12 2007 08:26 PM Automatic

Router#show ip dhcp pool MIPOOL
Pool MIPOOL:
  Utilization mark (high/low)   : 85 / 15
  Subnet size (first/next)      : 24 / 24 (autogrow)
  VRF name                      : abc
  Total addresses               : 28
  Leased addresses              : 11
  Pending event                 : none
  2 subnets are currently in the pool :
Current index  IP address range                     Leased addresses
10.1.1.12      10.1.1.1 - 10.1.1.14                 11
10.1.1.17      10.1.1.17 - 10.1.1.30                0
Interface Ethernet0/0 address assignment
 10.1.1.1 255.255.255.248
 10.1.1.17 255.255.255.248 secondary
```

### Configuración de un cliente DHCP

Configurar IOS para la opción del DHCP como cliente es simple.

```text
Router(config)#interface tipo número
Router(config-if)#ip address dhcp
```

Un router puede ser cliente, servidor o ambos a la vez en diferentes interfaces.

### Configuración de DHCP Relay

Un router configurado para dejar pasar los DHCP request es llamado DHCP Relay. Cuando es configurado, el router permitirá el reenvío de broadcast que haya sido enviado a un puerto UDP determinado hacia una localización remota. El DHCP Relay reenvía los requests y configura la puerta de enlace en el router local.

```text
Router(config-if)#ip helper-address dirección IP
```

## ICMP

El protocolo ICMP (*Internet Control Message Protocol*) suministra capacidades de control y envío de mensajes. Herramientas tales como `ping` y `trace` utilizan ICMP para poder funcionar, enviando un paquete a la dirección destino específica y esperando una determinada respuesta.

El campo código de la cabecera ICMP puede contener uno de los siguientes valores:

| Campo | Descripción |
| --- | --- |
| 0 | Respuesta de eco. |
| 3 | Destino inaccesible. |
| 4 | Disminución del tráfico desde el origen. |
| 5 | Redireccionar ruta. |
| 8 | Solicitud de eco. |
| 11 | Tiempo excedido. |
| 12 | Problema de parámetros. |
| 13 | Solicitud de marca de tiempo. |
| 14 | Respuesta de marca de tiempo. |
| 15 | Solicitud de información. |
| 16 | Respuesta de información. |
| 17 | Solicitud de máscara. |
| 18 | Respuesta de máscara. |

### Ping

El `ping` (*Packet Internet Groper*) es la herramienta de diagnóstico más utilizada por los administradores. Mediante esta utilidad puede diagnosticarse el estado, velocidad y calidad de la red de forma rápida y sencilla.

El comando `ping` prueba conectividad de sitio a sitio, en sus dos formas, básica y extendida, enviando y recibiendo paquetes echo según muestran las siguientes sintaxis.

```text
Router>ping 10.99.60.1
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.99.60.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 1/5/16 ms

Router#ping ipv6 2001:0:1ab:5:1111::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2001:0:1ab:5:1111::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 49/59/63 ms
```

La versión extendida del comando `ping` permite efectuar variantes tales como cantidad y tamaño de paquetes, tiempo entre cada envío, etc. Es una eficaz herramienta de pruebas cuando se desea no solo pruebas de conectividad sino también de carga.

```text
Router#ping
Protocol [ip]: ip
Target IP address: 10.99.60.1
Repeat count [5]: 50
Datagram size [100]: 100
Timeout in seconds [2]: 2
Extended commands [n]: n
Sweep range of sizes [n]: n
Type escape sequence to abort.
Sending 50, 100-byte ICMP Echos to 10.99.60.1, timeout is 2 seconds:
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Success rate is 100 percent (50/50), round-trip min/avg/max = 1/2/4 ms
```

La siguiente tabla muestra algunos de los caracteres con los que `ping` muestra efectividad o fallos en los routers.

| Carácter | Descripción |
| --- | --- |
| `!` | Cada signo de exclamación indica la recepción de una respuesta. |
| `.` | Cada punto indica agotado el tiempo esperando por una respuesta. |
| `U` | El destino resulta inalcanzable. |
| `Q` | Destino muy congestionado. |
| `?` | Tipo de paquete desconocido. |
| `&` | Curso de vida de los paquetes se ha superado. |

### TTL

Los paquetes IP poseen un campo que especifica el tiempo de vida del paquete. El TTL (*Time To Live*) impide que un paquete esté dando vueltas indefinidamente por la red de redes. El valor del TTL contenido en este campo disminuye en una unidad cada vez que el paquete atraviesa un router. Cuando el TTL llega a 0, éste se descarta y se envía un mensaje ICMP de tipo 11 para informar al origen.

!!! note "NOTA"
    Los sistemas operativos añaden un valor de TTL al paquete al salir. Por ejemplo, el valor de TTL de Linux: 64, Windows 10: 128.

### Traceroute

Los mensajes ICMP de tipo 11 se pueden utilizar para hacer una traza del camino que siguen los paquetes hasta llegar a su destino.

El comando `traceroute` utiliza el principio de funcionamiento del `ping` pero mostrando e identificando cada salto a lo largo de la ruta y disminuyendo el valor del TTL en cada salto. Cuando un paquete echo reply (ping) no llega a su destino `traceroute` mostrará el salto donde dicho paquete no consigue llegar. Si no se especifica lo contrario el límite de saltos es 30. En rutas extremadamente grandes la traza puede abortarse con las teclas `Ctrl+Shift+6`.

```text
Router#traceroute ?
  WORD    Trace route to destination address or hostname
  ip      IP Trace
  ipv6    IPv6 Trace

Router#traceroute 10.99.60.1
Type escape sequence to abort.
Tracing the route to 10.99.60.1
 1 10.99.170.11 0 msec 0 msec 4 msec
 2 81.46.16.48  4 msec 0 msec 4 msec
 3 10.99.60.1   4 msec 0 msec 0 msec
```

El comando `traceroute` también tiene una versión extendida que se puede utilizar para ver qué ruta toman los paquetes para llegar a un destino y comprobar el enrutamiento al mismo tiempo. Esto es útil para solucionar problemas con los bucles de enrutamiento, o para cuando se determina que los paquetes se pierden, si una ruta no está presente, o si los paquetes están siendo bloqueados (por ejemplo, por una ACL o un firewall). Puede utilizar el comando `ping` extendido con el fin de determinar el tipo de problema de conectividad y, a continuación, utilizar el comando `traceroute` extendido con el fin de deducir donde se produce exactamente el problema.

El comando termina en cualquiera de estos casos:

- El destino responde.
- Se supera el TTL máximo.
- El usuario interrumpe la traza con la secuencia de escape.

```text
Router#traceroute
Protocol [ip]: ip
Target IP address: 102.29.59.1
Source address: 102.29.119.10
Numeric display [n]:
Timeout in seconds [3]:
Probe count [3]:
Minimum Time to Live [1]:
Maximum Time to Live [30]:
Port Number [33434]:
Loose, Strict, Record, Timestamp, Verbose [none]:
Type escape sequence to abort.
Tracing the route to 10.99.59.1
VRF info: (vrf in name/id, vrf out name/id)
 1 102.29.119.7   0 msec  0 msec  0 msec
 2 102.29.52.15   0 msec  0 msec  4 msec
 3 81.46.16.20    4 msec  4 msec  4 msec
 4 102.29.59.1    8 msec  *     4 msec
```

## NTP

NTP (*Network Time Protocol*) permite a los routers de la red sincronizar sus configuraciones de tiempo con un servidor NTP. Un grupo de clientes NTP puede obtener información de fecha y hora de una sola fuente y tener configuraciones más consistentes. NTP utiliza el puerto UDP 123 y está documentado en la RFC 1305.

Cuando se implementa NTP en la red, puede configurarse para que se sincronice con un reloj privado o puede sincronizarse con un servidor NTP disponible públicamente en Internet.

Muchos servidores NTP en Internet no solicitan autenticación de sus pares, NTPv3 (NTP versión 3) y posteriores soportan un mecanismo de autenticación criptográfico entre pares NTP.

### Configuración del servidor

En una red configurada con NTP, se designan uno o más routers como master NTP, que serán los encargados de mantener el reloj. El siguiente comando habilita un NTP master.

```text
Router(config)#ntp master estrato
```

NTP utiliza un modelo jerárquico, donde el valor de estrato hace referencia a una fuente externa, como puede ser un reloj atómico.

### Configuración del cliente

La configuración manual funciona adecuadamente en un ambiente de una red pequeña, a medida que la red crece se vuelve difícil asegurarse de que todos los dispositivos de la infraestructura estén operando con la fecha sincronizada.

La configuración manual de la fecha y hora se realiza con el comando:

```text
Router#clock set hh:mm:ss day month year

Router#clock set 14:38:00 feb 10 2016

Router#show clock
14:38:11.292 PST Tue Feb 10 2016
```

Las asociaciones entre máquinas que ejecutan NTP generalmente tienen una configuración estática. Se da a cada dispositivo la dirección IP de los masters NTP. Es posible obtener una fecha y hora precisas intercambiando mensajes NTP entre cada par de máquinas con una asociación.

Para que el reloj de un cliente NTP sincronice con un servidor NTP se utiliza el siguiente comando:

```text
Router(config)#ntp server dirección-IP
```

Los comandos `show ntp status` y `show ntp associations` permiten ver el estado y las asociaciones de los pares NTP.

```text
Router#show ntp status
Clock is synchronized, stratum 6, reference is 204.99.239.60
nominal freq is 250.0000 Hz, actual freq is 249.9978 Hz, precision is 2**18
reference time is D5EC0BCF.3A424882 (15:02:07.227 CET Tue Sep 24 2013)
clock offset is 0.0701 msec, root delay is 3.97 msec
root dispersion is 47.01 msec, peer dispersion is 0.31 msec
```

### Configuración zona horaria y horario de verano

Para configurar el desplazamiento de la zona horaria UTC (*Coordinated Universal Time*), utilice el comando `clock timezone` en el modo de configuración global. Para volver a la configuración predeterminada, utilice la forma `no` de este comando.

```text
clock timezone zone-name offset-hours offset-minutes
```

Para configurar el sistema para que cambie automáticamente al horario de verano utilice el comando `clock summer-time` en el modo de configuración global. Para quitar el ajuste del horario de verano, utilice la forma `no` de este comando.

```text
clock summer-time zone { date { date month year hh:mm date month year hh:mm | month date year hh:mm month date year hh:mm } | recurring week day month hh:mm week day month hh:mm } [offset]
```

## FHRP

La mayoría de los dispositivos finales requieren la configuración de una puerta de enlace para su funcionamiento. Los routers y switches multicapa pueden proporcionar tolerancia a fallos o alta disponibilidad cuando están actuando como puertas de enlace como lo hacen los routers tradicionales.

Los FHRP (*First Hop Redundancy Protocol*) hacen referencia a aquellos protocolos orientados a proporcionar IPs y MACs virtuales con el fin de dotar de redundancia y/o balanceo a la red.

Los switch multicapa pueden utilizar los siguientes protocolos:

- **HSRP (*Host Standby Routing Protocol*).**
- **VRRP (*Virtual Router Redundancy Protocol*).**
- **GLBP (*Gateway Load Balancing Protocol*).**

### HSRP

HSRP (*Host Standby Router Protocol*) es un protocolo propietario de Cisco que permite que varios routers o switches multicapa aparezcan como una sola puerta de enlace. Cada uno de los routers que proporcionan redundancia es asignado a un grupo HSRP común, un router es elegido como primario o active y otro como secundario o standby, si existen más routers estarán escuchando en estado listen.

La elección del tipo de router está basada en una escala de prioridades en un rango de 0 a 255 y que por defecto toma el valor de 100. El router con la prioridad más alta se convierte en el router active del grupo y en caso de que todos los routers tengan la misma prioridad será active aquel con la IP más alta configurada en su interfaz de HSRP.

HSRP v2 añade las siguientes características:

- HSRPv2 amplía el número de grupos soportados a 4095 en lugar de 255 con HSRPv1.
- HSRP versión 2 utiliza la dirección de multidifusión IPv4 224.0.0.102 o la dirección IPv6 multicast FF02::66 para enviar paquetes hello en lugar de 224.0.0.2 utilizados por HSRPv1.
- HSRP v2 utiliza el rango de direcciones MAC de 0000.0C9F.F000 a 0000.0C9F.FFFF para IPv4 y 0005.73A0.0000 a 0005.73A0.0FFF para IPv6, en los tres últimos dígitos hexadecimales de la dirección MAC indican el número de grupo HSRP.
- HSRPv2 tiene soporte para autenticación MD5.

El proceso de configuración se inicia seleccionando un número de grupo HSRP dentro de un rango de 0 a 4095 y asignando un valor para la prioridad:

```text
Router(config-if)#standby grupo priority prioridad
```

Al configurar HSRP en una interfaz el router se mueve entre una serie de estados hasta alcanzar el estado final que dependerá de la prioridad y del estado del resto de los miembros del grupo. Los estados HSRP son los siguientes:

- **Disabled:** desactivado.
- **Init:** iniciándose.
- **Listen:** escuchando.
- **Speak:** hablando.
- **Standby:** en espera.
- **Active:** activo.

Los mensajes hello se envían cada 3 segundos. Un router en el estado de standby es el único que monitoriza los hello del router activo. Cuando el temporizador holdtime (3 veces el intervalo hello o 10 segundos) se inicia se presume que el router activo ha caído, el router en el estado standby pasará entonces al estado active y en caso de haber uno o más routers en el estado listen el de mayor prioridad pasará al estado standby.

Para cambiar los temporizadores de HSRP es necesario hacerlo en todos los routers del grupo, el holdtime debería ser siempre al menos 3 veces el intervalo hello. El comando para efectuar dicho cambio es el siguiente:

```text
Router(config-if)#standby group timers [msec] hello [msec] holdtime
```

Una vez que un router es elegido como activo mantendrá su estado incluso si otros routers con mayor prioridad son detectados. Es importante tener en cuenta para evitar que un router no deseado sea elegido como activo, iniciar la red encendiendo primero el router adecuado para cumplir el rol de activo. Este comportamiento es posible corregirlo de manera que el router con mayor prioridad sea siempre el activo, para esto se puede utilizar el siguiente comando:

```text
Router(config-if)#standby group preempt [delay [minimum seconds] [reload seconds]]
```

Por defecto después de aplicar este comando el router del grupo con mayor prioridad siempre será el activo y tomará su rol inmediatamente. La configuración del parámetro `delay minimum` puede efectuarse para esperar un tiempo determinado a partir de que la interfaz esté operativa antes de tomar el rol de activo y `reload`, se fuerza al router a esperar un tiempo determinado a partir del reinicio antes de tomar el rol de activo.

Además de la dirección IP única que cada router tiene configurada en las interfaces que ejecutan HSRP hay una dirección IP común, conocida como IP virtual o de HSRP. Los hosts entonces pueden apuntar a esa IP como su puerta de enlace, teniendo la certeza de que siempre habrá algún router respondiendo. Hay que tener en cuenta que tanto la IP real como la de HSRP han de pertenecer al mismo rango.

Para asignar la IP virtual se utiliza el siguiente comando:

```text
Router(config-if)#standby grupo ip ip-virtual

Norte(config)#interface vlan 50
Norte(config-if)#ip address 192.168.1.10 255.255.255.0
Norte(config-if)#standby 1 priority 200
Norte(config-if)#standby 1 preempt
Norte(config-if)#standby 1 ip 192.168.1.1
```

HSRP permite ser configurado con dos tipos diferentes de autenticación, todos los miembros del grupo deben coincidir en el tipo y clave. Los dos modos de autenticación HSRP son:

- **Texto plano:** los mensajes de HSRP son enviados con una cadena en texto plano de hasta ocho caracteres, esta cadena debe ser igual en todos los routers del grupo. El siguiente comando puede configurarlo:

```text
Switch(config-if)#standby group authentication string
```

- **MD5:** un cifrado del tipo MD5 (*Message Digest 5*) es computado en una porción de cada mensaje HSRP y en la clave secreta configurada en cada router del grupo. El hash MD5 es enviado junto con los mensajes HSRP. Cuando un mensaje es recibido el router recalcula el cifrado del mensaje y de su propia clave, en caso de coincidencia el mensaje será aceptado. Este tipo de autenticación es, obviamente, mucho más segura que en texto plano. Para configurarla se utiliza el siguiente comando:

```text
Switch(config-if)#standby group authentication md5 key-string [0 | 7] string
```

Por defecto la clave se pone en texto plano, una vez introducida aparecerá encriptada en la configuración. Para copiar y pegar dicha clave en otros routers es posible copiarla ya encriptada y especificar la opción `7` delante de la clave antes de pegarla.

Alternativamente se puede usar una cadena de claves que, aunque hace que la configuración sea más compleja, proporciona mayor flexibilidad. Los comandos son los siguientes:

```text
Switch(config)#key chain chain-name
Switch(config-keychain)#key key-number
Switch(config-keychain-key)#key-string [0 | 7] string
Switch(config)#interface type mod/num
Switch(config-if)#standby group authentication md5 key-chain chain-name
```

Para poder llevar a cabo el balanceo de carga en HSRP es necesario utilizar al menos 2 grupos, para el caso de tener dos switches, SW1 sería activo en un grupo y standby en el otro mientras que SW2 actuaría con el rol contrario a SW1 para esos mismos grupos. El conjunto de host que utilicen estas puertas de enlace deberá ser asignados mitad con una IP y mitad con otra IP.

La siguiente sintaxis corresponde al escenario de abajo. Catalyst Norte es activo para el grupo 1 con IP 192.168.1.1 y es standby del grupo 2 con IP 192.168.1.2. Catalyst Sur tiene una configuración similar, pero tomando el rol contrario para cada grupo.

```text
Cat_Norte(config)#interface vlan 50
Cat_Norte(config-if)#ip address 192.168.1.10 255.255.255.0
Cat_Norte(config-if)#standby 1 priority 200
Cat_Norte(config-if)#standby 1 preempt
Cat_Norte(config-if)#standby 1 ip 192.168.1.1
Cat_Norte(config-if)#standby 1 authentication CCna
Cat_Norte(config-if)#standby 2 priority 100
Cat_Norte(config-if)#standby 2 ip 192.168.1.2
Cat_Norte(config-if)#standby 2 authentication CCna

Cat_Sur(config)#interface vlan 50
Cat_Sur(config-if)#ip address 192.168.1.11 255.255.255.0
Cat_Sur(config-if)#standby 1 priority 100
Cat_Sur(config-if)#standby 1 ip 192.168.1.1
Cat_Sur(config-if)#standby 1 authentication CCna
Cat_Sur(config-if)#standby 2 priority 200
Cat_Sur(config-if)#standby 2 preempt
Cat_Sur(config-if)#standby 2 ip 192.168.1.2
Cat_Sur(config-if)#standby 2 authentication CCnP
```

Para ver el estado HSRP puede utilizarse el comando `show standby`.

```text
Router#show standby [brief] [vlan vlan-id | type mod/num]

Router#show standby
GigabitEthernet0/0 - Group 1 (version 2)
  State is Active
     9 state changes, last state change 00:14:51
  Virtual IP address is 192.168.1.1
  Active virtual MAC address is 0000.0C9F.F001
  Local virtual MAC address is 0000.0C9F.F001 (v2 default)
  Hello time 3 sec, hold time 10 sec
  Next hello sent in 1.479 secs
  Preemption disabled
  Active router is local
  Standby router is 192.168.1.10
  Priority 110 (default 100)
  Group name is hsrp-Gig0/0-1 (default)
```

Los siguientes ejemplos muestran la salida de este comando.

```text
Norte#show standby vlan 50 brief
  P indicates configured to preempt.
  |
Interface  Grp  Prio P State       Active addr  Standby addr  Group addr
Vl50       1    200  P Active      local        192.168.1.11   192.168.1.1
Vl50       2    100    Standby     192.168.1.11 local          192.168.1.2

Norte#show standby vlan 50
Vlan50 - Group 1
  Local state is Active, priority 200, may preempt
  Hellotime 3 sec, holdtime 10 sec
  Next hello sent in 2.248
  Virtual IP address is 192.168.1.1 configured
  Active router is local
  Standby router is 192.168.1.11 expires in 9.860
  Virtual mac address is 0000.0c07.ac01
  Authentication text "CCnA"
  2 state changes, last state change 00:11:58
  IP redundancy name is "hsrp-Vl50-1" (default)
Vlan50 - Group 2
  Local state is Standby, priority 100
  Hellotime 3 sec, holdtime 10 sec
  Next hello sent in 1.302
  Virtual IP address is 192.168.1.2 configured
  Active router is 192.168.1.11, priority 200 expires in 7.812
  Standby router is local
  Authentication text "CCnA"
  4 state changes, last state change 00:10:04
  IP redundancy name is "hsrp-Vl50-2" (default)

Sur#show standby vlan 50 brief
  P indicates configured to preempt.
  |
Interface  Grp  Prio P State       Active addr  Standby addr  Group addr
Vl50       1    100    Standby     192.168.1.10 local          192.168.1.1
Vl50       2    200  P Active      local        192.168.1.10   192.168.1.2

Sur#show standby vlan 50
Vlan50 - Group 1
  Local state is Standby, priority 100
  Hellotime 3 sec, holdtime 10 sec
  Next hello sent in 0.980
  Virtual IP address is 192.168.1.1 configured
  Active router is 192.168.1.10, priority 200 expires in 8.128
  Standby router is local
  Authentication text "CCnA"
  1 state changes, last state change 00:01:12
  IP redundancy name is "hsrp-Vl50-1" (default)
Vlan50 - Group 2
  Local state is Active, priority 200, may preempt
  Hellotime 3 sec, holdtime 10 sec
  Next hello sent in 2.888
  Virtual IP address is 192.168.1.2 configured
  Active router is local
  Standby router is 192.168.1.10 expires in 8.500
  Virtual mac address is 0000.0c07.ac02
  Authentication text "CCnA"
  1 state changes, last state change 00:01:16
```

!!! tip "RECUERDE"
    Causas habituales de fallo en HSRP:

    - Los routers HSRP no están conectados al mismo segmento de red, ya sea debido a un problema de la capa física o un problema de configuración VLAN.
    - Los routers HSRP no están configurados con direcciones IP de la misma subred, por lo tanto, un router de reserva no sabría cuándo el router activo falla.
    - Los routers HSRP no están configurados con la misma dirección IP virtual.
    - Los routers HSRP no están configurados con el mismo número de grupo HSRP.
    - Los dispositivos finales no están configurados con la dirección de puerta de enlace predeterminada correcta.

!!! note "NOTA"
    Los HSRP intercambian mensajes hello entre ellos para comprobar que todo está en orden de manera multicast a través de la dirección IP 224.0.0.2 puerto UDP 1985.

### VRRP

VRRP (*Virtual Router Redundancy Protocol*) es un protocolo estándar definido en la RFC 2338, con un funcionamiento y configuración similares a HSRP. Una comparación entre ambos es la siguiente:

- VRRP proporciona una IP redundante compartida entre un grupo de routers, de los cuales está el activo que recibe el nombre de master mientras que el resto se les conoce como backup. El master es aquel con mayor prioridad en el grupo.
- Los grupos pueden tomar un valor entre 0 y 255, mientras que la prioridad asignada a un router puede tomar valores entre 1 y 254 siendo 254 la más alta y 100 el valor por defecto.
- La dirección MAC virtual tiene el formato `0000.5e00.01xx`, donde `xx` es el número de grupo en formato hexadecimal.
- Los hello de VRRP son enviados cada 1 segundo.
- Por defecto los routers configurados con VRRP toman el rol de master en cualquier momento.
- VRRP no tiene un mecanismo para llevar un registro del estado de las interfaces de la manera que lo hace HSRP.

El proceso de configuración de VRRP se realiza mediante los siguientes comandos:

```text
! Asignación de la prioridad:
vrrp group priority level
! Cambio del intervalo del temporizador:
vrrp group timers advertise [msec] interval
! Para aprender el intervalo desde el router master:
vrrp group timers learn
! Deshabilita la función de automáticamente tomar el rol de master:
no vrrp group preempt
! Cambia el retraso en tomar el rol de master, por defecto es 0 segundos:
vrrp group preempt [delay seconds]
! Habilita la autenticación:
vrrp group authentication string
! Configura la IP virtual:
vrrp group ip ip-address [secondary]
```

La siguiente sintaxis es un ejemplo de configuración:

```text
Cat_Norte(config)#interface vlan 50
Cat_Norte(config-if)#ip address 192.168.1.10 255.255.255.0
Cat_Norte(config-if)#vrrp 1 priority 200
Cat_Norte(config-if)#vrrp 1 ip 192.168.1.1
Cat_Norte(config-if)#vrrp 2 priority 100
Cat_Norte(config-if)#no vrrp 2 preempt
Cat_Norte(config-if)#vrrp 2 ip 192.168.1.2

Cat_Sur(config)#interface vlan 50
Cat_Sur(config-if)#ip address 192.168.1.11 255.255.255.0
Cat_Sur(config-if)#vrrp 1 priority 100
Cat_Sur(config-if)#no vrrp 1 preempt
Cat_Sur(config-if)#vrrp 1 ip 192.168.1.1
Cat_Sur(config-if)#vrrp 2 priority 200
Cat_Sur(config-if)#vrrp 2 ip 192.168.1.2
```

La siguiente salida corresponde a los `show vrrp brief` y `show vrrp`:

```text
Cat_Norte#show vrrp brief
Interface  Grp  Pri  Time  Own  Pre State    Master addr   Group addr
Vlan50     1    200  3218  Y    Master      192.168.1.10  192.168.1.1
Vlan50     2    100  3609     Backup      192.168.1.11  192.168.1.2

Cat_Sur#show vrrp brief
Interface  Grp  Pri  Time  Own  Pre State    Master addr   Group addr
Vlan50     1    100  3609     Backup      192.168.1.10  192.168.1.1
Vlan50     2    200  3218  Y    Master      192.168.1.11  192.168.1.2

Cat_Norte#show vrrp
Vlan50 - Group 1
  State is Master
  Virtual IP address is 192.168.1.1
  Virtual MAC address is 0000.5e00.0101
  Advertisement interval is 1.000 sec
  Preemption is enabled
    min delay is 0.000 sec
  Priority is 200
  Authentication is enabled
  Master Router is 192.168.1.10 (local), priority is 200
  Master Advertisement interval is 1.000 sec
  Master Down interval is 3.218 sec
Vlan50 - Group 2
  State is Backup
  Virtual IP address is 192.168.1.2
  Virtual MAC address is 0000.5e00.0102
  Advertisement interval is 1.000 sec
  Preemption is disabled
  Priority is 100
  Authentication is enabled
  Master Router is 192.168.1.11, priority is 200
  Master Advertisement interval is 1.000 sec
  Master Down interval is 3.609 sec (expires in 2.977 sec)

Cat_Sur#show vrrp
Vlan50 - Group 1
  State is Backup
  Virtual IP address is 192.168.1.1
  Virtual MAC address is 0000.5e00.0101
  Advertisement interval is 1.000 sec
  Preemption is disabled
  Priority is 100
  Authentication is enabled
  Master Router is 192.168.1.10, priority is 200
  Master Advertisement interval is 1.000 sec
  Master Down interval is 3.609 sec (expires in 2.833 sec)
Vlan50 - Group 2
  State is Master
  Virtual IP address is 192.168.1.2
  Virtual MAC address is 0000.5e00.0102
  Advertisement interval is 1.000 sec
  Preemption is enabled
    min delay is 0.000 sec
  Priority is 200
  Authentication is enabled
  Master Router is 192.168.1.11 (local), priority is 200
  Master Advertisement interval is 1.000 sec
  Master Down interval is 3.218 sec
```

### GLBP

GLBP (*Gateway Load Balancing Protocol*) es un protocolo propietario de Cisco que sirve para añadir balanceo de carga sin la necesidad de utilizar múltiples grupos a la función de redundancia con HSRP o VRRP.

Múltiples routers o switches son asignados a un mismo grupo, pudiendo todos ellos participar en el envío de tráfico. La ventaja de GLBP es que los host clientes no han de dividirse y apuntar a diferentes puertas de enlace, todos pueden tener la misma. El balanceo de carga se lleva a cabo respondiendo a los clientes con diferentes direcciones MAC, de manera que, aunque todos apuntan a la misma IP la dirección MAC de destino es diferente, repartiendo de esta manera el tráfico entre los diferentes routers.

Uno de los routers del grupo GLBP es elegido como "puerta de enlace virtual activa" o AVG (*Active Virtual Gateway*), dicho router es el de mayor prioridad del grupo o en caso de no haberse configurado dicha prioridad, será el de IP más alta. El AVG responde a las peticiones ARP de los clientes y la MAC que enviará dependerá del algoritmo de balanceo de carga que se esté utilizando.

El AVG también asigna las MAC virtuales a cada uno de los routers del grupo, pudiéndose usar hasta 4 MAC virtuales por grupo. Cada uno de esos routers recibe el nombre de AVF (*Active Virtual Forwarder*) y se encarga de enviar el tráfico recibido en su MAC virtual. Otros routers en el grupo pueden funcionar como backup en caso de que el AVF falle.

La prioridad GLBP se configura con el siguiente comando:

```text
Switch(config-if)#glbp group priority level
```

El rango de números que pueden usarse para definir grupos asume valores entre 0 y 1023. El rango de prioridades es entre 1 y 255 siendo 255 la más alta y 100 la de por defecto.

Como ocurre en HSRP se tiene que habilitar la función `preempt` en caso de ser necesario, ya que por defecto no está permitido tomar el rol de AVG a no ser que éste falle. El siguiente comando lo configura:

```text
Switch(config-if)#glbp group preempt [delay minimum seconds]
```

Para monitorizar el estado de los routers AVG se envían hello cada 3 segundos y en caso de no recibir respuesta en el intervalo de holdtime de 10 segundos, se considera que el vecino está caído. Es posible modificar estos temporizadores con el siguiente comando:

```text
Switch(config-if)#glbp group timers [msec] hellotime [msec] holdtime
```

Para modificar los temporizadores se debe tener en cuenta que el holdtime debería ser al menos 3 veces mayor que el hello.

GLBP también usa mensajes hello para monitorizar los AVF (*Active Virtual Forwarder*). Cuando el AVG detecta que un AVF ha fallado asigna el rol a otro router, el cual podría ser o no otro AVF, teniendo entonces que enviar el tráfico destinado a 2 MAC virtuales.

Para solventar el problema de estar respondiendo a mensajes destinados a dos MAC virtuales se usan dos temporizadores:

- **Redirect:** determina cuándo el AVG dejará de usar la MAC del router que falló para respuestas ARP.
- **Timeout:** cuando expira la MAC y el AVF que había fallado son eliminados del grupo, asumiendo que ese AVF no se recuperará. Los clientes necesitan entonces renovar su memoria y obtener la nueva MAC.

El temporizador redirect es de 10 minutos por defecto, pudiendo configurarse hasta un máximo de 1 hora. El temporizador timeout es de 4 horas por defecto, pudiendo configurarse dentro del rango de 18 horas. Es posible ajustar estos valores usando el siguiente comando:

```text
Switch(config-if)#glbp group timers redirect redirect timeout
```

GLBP usa una función de "peso" para determinar qué router será el AVF para una MAC virtual dentro de un grupo. Cada router comienza con un peso máximo entre 1 y 255 siendo por defecto 100. Cuando una interfaz en particular falla, el peso es disminuido en el valor que esté configurado. GLBP usa umbrales para determinar si un router puede o no ser el AVF. Si el valor del peso está por debajo de ese umbral el router no puede asumir ese rol, pero si dicho valor volviera a superar el umbral entonces sí podría.

GLBP necesita tener conocimiento sobre qué interfaces utilizarán este mecanismo y cómo ajustar su peso. El siguiente comando especifica dicha interfaz:

```text
Switch(config)#track object-number interface type mod/num {line-protocol | ip routing}
```

El valor `object-number` simplemente referencia el objeto que se está monitorizando y puede tener un valor entre 1 y 500. Las condiciones a verificar pueden ser `line-protocol` o `ip-routing`. Seguidamente es necesario definir los umbrales del peso para lo cual se utiliza el siguiente comando:

```text
Switch(config-if)#glbp group weighting maximum [lower lower] [upper upper]
```

El parámetro `maximum` indica con qué valor se inicia y los valores `lower` y `upper` definen cuándo, o cuándo no, el router puede actuar como AVF.

Finalmente se debe indicar a GLBP qué objetos ha de monitorizar para aplicar los umbrales de "peso". Para ello se utiliza el siguiente comando:

```text
Switch(config-if)#glbp group weighting track object-number [decrement value]
```

El parámetro `value` indica el valor que se disminuirá cuando el objeto monitorizado falle. Por defecto es 10 y puede ser configurado con un valor entre 1 y 254.

El balanceo de carga AVG funciona enviando MAC virtuales a los clientes. Previamente estas MAC virtuales han sido asignadas a los AVF permitiendo hasta un máximo de 4 MAC virtuales por grupo.

Los siguientes algoritmos se utilizan para el balanceo de carga con GLBP:

- **Round Robin:** cada nueva petición ARP para la IP virtual recibe la siguiente MAC virtual disponible. La carga de tráfico se distribuye equitativamente entre todos los routers del grupo asumiendo que los clientes envían y reciben la misma cantidad de tráfico.
- **Weighted:** el valor del peso configurado en la interfaz perteneciente al grupo será la referencia para determinar la proporción de tráfico enviado a cada AVF.
- **Host dependent:** cada cliente que envía una petición ARP es respondido siempre con la misma MAC. Es útil para clientes que necesitan que la MAC de la puerta de enlace sea siempre la misma.

El método de balanceo de carga utilizado se selecciona con el siguiente comando:

```text
Switch(config-if)#glbp group load-balancing [round-robin | weighted | host-dependent]
```

En la siguiente figura existen 3 switches multicapa participando en un grupo común GLBP. Catalyst A es elegido como AVG y por lo tanto coordina el proceso. El AVG responde todas las peticiones de la puerta de enlace 192.168.1.1. Dicho router se identifica a sí mismo y a Catalyst B y Catalyst C como AVF del grupo.

Para habilitar GLBP se debe asignar una IP virtual al grupo mediante el siguiente comando:

```text
Switch(config-if)#glbp group ip [ip-address [secondary]]
```

Cuando en el comando la dirección IP no se configura será aprendida de otro router del grupo. Para el caso puntual de la configuración del posible AVG es necesario especificar la IP virtual para que los demás routers puedan conocerla.

```text
CatalystA(config)#interface vlan 50
CatalystA(config-if)#ip address 192.168.1.10 255.255.255.0
CatalystA(config-if)#glbp 1 priority 200
CatalystA(config-if)#glbp 1 preempt
CatalystA(config-if)#glbp 1 ip 192.168.1.1

CatalystB(config)#interface vlan 50
CatalystB(config-if)#ip address 192.168.1.11 255.255.255.0
CatalystB(config-if)#glbp 1 priority 150
CatalystB(config-if)#glbp 1 preempt
CatalystB(config-if)#glbp 1 ip 192.168.1.1

CatalystC(config)#interface vlan 50
CatalystC(config-if)#ip address 192.168.1.12 255.255.255.0
CatalystC(config-if)#glbp 1 priority 100
CatalystC(config-if)#glbp 1 ip 192.168.1.1
```

Utilizando el método de balanceo de carga round-robin, cada uno de los PC hace peticiones ARP de la puerta de enlace. Al iniciar los PC de izquierda a derecha el AVG va asignando la siguiente MAC virtual secuencialmente.

Para ver información acerca de la operación de GLBP se pueden utilizar los comandos `show glbp brief` o `show glbp`:

```text
CatalystA#show glbp brief
Interface  Grp  Fwd  Pri  State    Address          Active     Standby
Vl50       1    -    200  Active    192.168.1.1      local      192.168.1.11
Vl50       1    1    7    Active    0007.b400.0101   local
Vl50       1    2    7    Listen    0007.b400.0102   192.168.1.11
Vl50       1    3    7    Listen    0007.b400.0103   192.168.1.13

CatalystB#show glbp brief
Interface  Grp  Fwd  Pri  State    Address          Active     Standby
Vl50       1    1    7    Listen    0007.b400.0101   192.168.1.10
Vl50       1    2    7    Active    0007.b400.0102   local
Vl50       1    3    7    Listen    0007.b400.0103   192.168.1.13

CatalystC#show glbp brief
Interface  Grp  Fwd  Pri  State    Address          Active     Standby
Vl50       1    -    100  Listen    192.168.1.1      192.168.1.10  192.168.1.11
Vl50       1    1    7    Listen    0007.b400.0101   192.168.1.10  -
Vl50       1    2    7    Listen    0007.b400.0102   192.168.1.11  -
Vl50       1    3    7    Active    0007.b400.0103   local
```

```text
CatalystA#show glbp
Vlan50 - Group 1
  State is Active
  7 state changes, last state change 03:28:05
  Virtual IP address is 192.168.1.1
  Hello time 3 sec, hold time 10 sec
  Next hello sent in 1.672 secs
  Redirect time 600 sec, forwarder time-out 14400 sec
  Preemption enabled, min delay 0 sec
  Active is local
  Standby is 192.168.1.11, priority 150 (expires in 9.632 sec)
  Priority 200 (configured)
  Weighting 100 (default 100), thresholds: lower 1, upper 100
  Load balancing: round-robin
  There are 3 forwarders (1 active)
  Forwarder 1
    State is Active
      3 state changes, last state change 03:27:37
    MAC address is 0007.b400.0101 (default)
    Owner ID is 00d0.0229.b80a
  Redirection enabled
  Preemption enabled, min delay 30 sec
  Active is local, weighting 100
  Forwarder 2
    State is Listen
    MAC address is 0007.b400.0102 (learnt)
    Owner ID is 0007.b372.dc4a
    Redirection enabled, 598.308 sec remaining (maximum 600 sec)
    Time to live: 14398.308 sec (maximum 14400 sec)
  Preemption enabled, min delay 30 sec
    Active is 192.168.1.11 (primary), weighting 100 (expires in 8.308 sec)
  Forwarder 3
    State is Listen
    MAC address is 0007.b400.0103 (learnt)
    Owner ID is 00d0.ff8a.2c0a
    Redirection enabled, 599.892 sec remaining (maximum 600 sec)
    Time to live: 14399.892 sec (maximum 14400 sec)
  Preemption enabled, min delay 30 sec
    Active is 192.168.1.13 (primary), weighting 100 (expires in 9.892 sec)
```

## Caso práctico

En base a la topología se han realizado las siguientes tareas de configuración en el router CCNA:

- Usuario, contraseña y banner.
- Configuración de interfaces FastEthernet y Serial.
- Creación de una tabla de hosts.

### Configuración de usuario y contraseña

En el siguiente caso se han creado dos usuarios `Admin_Sur` con una contraseña `Ansur` y `Admin_Nort` con una contraseña `Anort`. Se configura a continuación la contraseña secret, el mensaje y la línea de consola:

```text
Router(config)#hostname CCNA
CCNA(config)#enable secret cisco
CCNA(config)#username Admin_Sur password Ansur
CCNA(config)#username Admin_Nort password Anort
CCNA(config)#banner motd * Usted intenta ingresar en un sistema protegido por las leyes vigentes*
CCNA(config)#line console 0
CCNA(config-line)#login local
```

Cuando el usuario Admin_Nort intente ingresar al router le será solicitado su usuario y contraseña, y luego la enable secret:

```text
Press RETURN to get started.
Usted intenta ingresar en un sistema protegido por las leyes vigentes
User Access Verification
Username: Admin_Nort
Password: *****
CCNA>enable
Password: *****
CCNA#
```

!!! note "NOTA"
    Las contraseñas sin encriptación aparecen en el `show running` debiendo tener especial cuidado ante la presencia de intrusos.

!!! tip "RECUERDE"
    El comando `service password-encryption` encriptará con un cifrado leve las contraseñas que no están cifradas por defecto como las de telnet, consola, auxiliar, etc. Una vez cifradas las contraseñas no se podrán volver a leer en texto plano.

### Configuración de una interfaz FastEthernet

La sintaxis muestra la configuración de una interfaz FastEthernet:

```text
CCNA>enable
Password: *******
CCNA#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
CCNA(config)#interface Fastethernet 0
CCNA(config-if)#ip address 192.168.1.1 255.255.255.0
CCNA(config-if)#speed 100
CCNA(config-if)#duplex full
CCNA(config-if)#no shutdown
CCNA(config-if)#description Conexion_Host
```

### Configuración de una interfaz Serie

El ejemplo muestra la configuración de un enlace serial como DCE:

```text
CCNA(config)#interface serial 0/0
CCNA(config-if)#ip address 220.220.10.2 255.255.255.252
CCNA(config-if)#clock rate 56000
CCNA(config-if)#bandwidth 100000
CCNA(config-if)#description Conexion_Wan
CCNA(config-if)#no shutdown
```

### Configuración de una tabla de host

A continuación se ha creado una tabla de host con el comando `ip host`:

```text
CCNA(config)#ip host SERVIDOR 204.200.1.2
CCNA(config)#ip host WAN 220.220.10.1
CCNA(config)#ip host HOST 192.168.1.2
CCNA(config)#exit

CCNA#show hosts
Host      Flags  Age Type Address(es)
SERVIDOR  (perm, OK)  0 IP  204.200.1.2
ROUTER    (perm, OK)  0 IP  220.220.10.1
HOST      (perm, OK)  0 IP  192.168.1.2
```

!!! tip "RECUERDE"
    En el caso que se muestra arriba si se deseara enviar un `ping` a la dirección IP 204.200.1.2 bastaría con ejecutar `ping SERVIDOR`. Por defecto las tablas de host están asociadas al puerto 23 (telnet); si solo se ejecutara `SERVIDOR` el router intentaría establecer una sesión de telnet con ese host, y solo tienen carácter local.

### Configuración dual-stack

En base a la topología se han realizado las siguientes tareas de configuración en el router CCNAv6 para que trabaje en dual-stack:

- Habilitación del enrutamiento IPv6.
- Configuración de las interfaces FastEthernet 0/0 y FastEthernet 0/1 con direccionamiento estático IPv4 e IPv6.
- Configuración de la interfaz Serial 0/2/0 con direccionamiento IPv6 EUI-64.
- Configuración de la interfaz FastEthernet 1/0 con direccionamiento dinámico IPv6.

Se realizan pruebas de conectividad desde el router CCNAv6 hacia Host A y Host B. En este último caso de dos formas diferentes.

```text
CCNAv6(config)#ipv6 unicast-routing
CCNAv6(config)#int fastEthernet 0/0
CCNAv6(config-if)#ipv6 address 2001:0:1AB:6:2222::2/64
CCNAv6(config-if)#ip address 192.168.1.1 255.255.255.0
CCNAv6(config-if)#no shutdown
CCNAv6(config-if)#exit
CCNAv6(config)#interface fastEthernet 0/1
CCNAv6(config-if)#ipv6 address 2001:0:1ab:5:1111::1/64
CCNAv6(config-if)#ip address 192.168.0.1 255.255.255.0
CCNAv6(config-if)#no shutdown
CCNAv6(config-if)#exit
CCNAv6(config)#interface serial 0/2/0
CCNAv6(config-if)#ipv6 address 2001:0:1AB:10::/64 eui-64
CCNAv6(config-if)#no shutdown
CCNAv6(config)#int fastEthernet 1/0
CCNAv6(config-if)#ipv6 address autoconfig
CCNAv6(config-if)#exit
CCNAv6(config)#exit

CCNAv6#show running-config
Building configuration...
Current configuration : 800 bytes
!
.......................
ipv6 unicast-routing
!
!
interface FastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:0:1AB:6:2222::2/64
!
interface FastEthernet0/1
 ip address 192.168.0.1 255.255.255.0
 duplex auto
 speed auto
 ipv6 address 2001:0:1AB:5:1111::1/64
!
interface Serial0/2/0
 no ip address
 ipv6 address 2001:0:1AB:10::/64 eui-64
!
interface FastEthernet1/0
 no ip address
 ipv6 address autoconfig
......................................
```

```text
CCNAv6#ping 192.168.1.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 49/59/63 ms

CCNAv6#ping 2001:0:1ab:5:1111::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2001:0:1ab:5:1111::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 62/74/125 ms

CCNAv6#ping ipv6 2001:0:1ab:5:1111::2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2001:0:1ab:5:1111::2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 49/59/63 ms
```

### Configuración dual-stack con túnel

En la siguiente práctica se ha creado un túnel IPv4 entre los routers Derecha e Izquierda por el que se enviará tráfico IPv6 intercambiado por las interfaces Tunnel0 de ambos routers.

- Habilitar el enrutamiento IPv6 en ambos routers.
- Configurar EIGRP 100 en su versión 6.
- Configurar las interfaces seriales con IPv4 en los dos routers.
- Crear las interfaces tunnel sobre IPv6 cuyo destino será la interfaz serie del router vecino.
- Configurar las interfaces GigabitEthernet.

```text
Router(config)#hostname Izquierda
Izquierda(config)#ipv6 unicast-routing
Izquierda(config)#interface Tunnel0
Izquierda(config-if)#ipv6 address 2001:0:1:5::1/64
Izquierda(config-if)#ipv6 eigrp 100
Izquierda(config-if)#tunnel source Serial0/0/0
Izquierda(config-if)#tunnel destination 192.168.7.1
Izquierda(config-if)#tunnel mode ipv6ip
Izquierda(config-if)#no shut
Izquierda(config-if)#exit
Izquierda(config)#interface GigabitEthernet0/0
Izquierda(config-if)#ipv6 address 2001:0:1:2::1/64
Izquierda(config-if)#ipv6 eigrp 100
Izquierda(config-if)#ipv6 enable
Izquierda(config-if)#no shut
Izquierda(config-if)#exit
Izquierda(config)#interface Serial0/0/0
Izquierda(config-if)#ip address 192.168.7.2 255.255.255.0
Izquierda(config-if)#ipv6 eigrp 100
Izquierda(config-if)#no shut
Izquierda(config)#ipv6 router eigrp 100
Izquierda(config-rtr)#no shutdown
```

```text
Router(config)#hostname Derecha
Derecha(config)#ipv6 unicast-routing
Derecha(config)#interface Tunnel0
Derecha(config-if)#ipv6 address 2001:0:1:5::2/64
Derecha(config-if)#ipv6 eigrp 100
Derecha(config-if)#tunnel source Serial0/0/0
Derecha(config-if)#tunnel destination 192.168.7.2
Derecha(config-if)#tunnel mode ipv6ip
Derecha(config-if)#no shut
Derecha(config-if)#exit
Derecha(config)#interface GigabitEthernet0/0
Derecha(config-if)#ipv6 address 2001:0:1:1::1/64
Derecha(config-if)#ipv6 eigrp 100
Derecha(config-if)#ipv6 enable
Derecha(config-if)#no shut
Derecha(config-if)#exit
Derecha(config)#interface Serial0/0/0
Derecha(config-if)#ip address 192.168.7.1 255.255.255.0
Derecha(config-if)#ipv6 eigrp 100
Derecha(config-if)#clock rate 72000
Derecha(config-if)#no shut
Derecha(config-if)#exit
Derecha(config)#ipv6 router eigrp 100
Derecha(config-rtr)#no shutdown
```

```text
Derecha#sh ipv6 route
IPv6 Routing Table - 6 entries
Codes: C - Connected, L - Local, S - Static, R - RIP, B - BGP
       U - Per-user Static route, M - MIPv6
       I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea, IS - ISIS summary
       O - OSPF intra, OI - OSPF inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2
       D - EIGRP, EX - EIGRP external
C   2001:0:1:1::/64 [0/0]
      via ::, GigabitEthernet0/0
L   2001:0:1:1::1/128 [0/0]
      via ::, GigabitEthernet0/0
D   2001:0:1:2::/64 [90/26880256]
      via FE80::260:3EFF:FE48:D6D2, Tunnel0
C   2001:0:1:5::/64 [0/0]
      via ::, Tunnel0
L   2001:0:1:5::2/128 [0/0]
      via ::, Tunnel0
L   FF00::/8 [0/0]
      via ::, Null0
```

La interfaz tunnel0 muestra el origen y el destino del túnel IPv4 configurado en el router.

```text
Derecha#sh int tunnel 0
Tunnel0 is up, line protocol is up (connected)
  Hardware is Tunnel
  MTU 17916 bytes, BW 100 Kbit/sec, DLY 50000 usec,
      reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation TUNNEL, loopback not set
  Keepalive not set
  Tunnel source 192.168.7.1 (Serial0/0/0), destination 192.168.7.2
  Tunnel protocol/transport IPv6/IP
  Key disabled, sequencing disabled
  Checksumming of packets disabled
  Tunnel TTL 255
  Fast tunneling enabled
  Tunnel transport MTU 1476 bytes
  Tunnel transmit bandwidth 8000 (kbps)
  Tunnel receive bandwidth 8000 (kbps)
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 1
  Queueing strategy: fifo
  Output queue: 0/0 (size/max)
  5 minute input rate 102 bits/sec, 0 packets/sec
  5 minute output rate 104 bits/sec, 0 packets/sec
     274 packets input, 16447 bytes, 0 no buffer
     Received 0 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 input packets with dribble condition detected
     270 packets output, 16220 bytes, 0 underruns
     0 output errors, 0 collisions, 0 interface resets
     0 unknown protocol drops
     0 output buffer failures, 0 output buffers swapped out
```

## Fundamentos para el examen

Este capítulo puede resultar muy extenso, familiarícese primero con la operatividad, la instalación y la configuración inicial del router hasta obtener un manejo fluido. Es imprescindible su dominio. Si no dispone de dispositivos reales puede utilizar simuladores.

- Recuerde los componentes principales del router, sus funciones e importancia dentro de su arquitectura.
- Estudie y relacione los estándares de WAN con el router.
- Memorice los parámetros de configuración del emulador de consola para ingresar por primera vez al router.
- Analice los pasos de arranque del router, estudie la secuencia y para qué sirve cada uno de los pasos.
- Familiarícese con todos los comandos básicos del router, tenga en cuenta que le servirán para el resto de las configuraciones más adelante.
- Recuerde los comandos `show` más usados, habitúese a su utilización para detectar y visualizar incidencias o configuraciones.
- Estudie y analice las propiedades de las distintas interfaces que puede contener el router, recuerde los pasos a seguir en el proceso de configuración de cada una de ellas.
- Recuerde los comandos necesarios para efectuar copias de seguridad, los requisitos mínimos y los pasos para cargar desde diferentes fuentes. Tenga en cuenta las diferencias entre `startup-config` y `running-config`.
- Memorice cómo se compone el nombre del Cisco IOS y cómo se obtienen las licencias para su utilización.
- Tenga en cuenta la importancia del comando `show version` y los diferentes valores que puede tomar el registro de configuración.
- Recuerde los pasos en el proceso de recuperación de contraseñas y para qué sirve cada uno de ellos. Tenga una idea clara de cuáles son los registros de configuración antes y después de la recuperación.
- Recuerde la función y comandos del CDP, qué muestran y para qué se utilizan.
- Compare y tenga en cuenta las diferencias entre LLDP y CDP.
- Configure una topología con DHCP, observe los resultados y analícelos.
- Ejercite todas las configuraciones en dispositivos reales o en simuladores.
- Ejecute pruebas de conectividad con los comandos `ping` y `traceroute`, saque conclusiones.
- Analice la funcionalidad de los protocolos de redundancia.
- Estudie los casos donde los FHRP pueden dar fallos.
