# Redes de área amplia

## WAN

Una WAN (*Wide Area Networks*) define la forma en que los datos se desplazan a través de una zona geográficamente extensa. Las WAN interconectan diferentes LAN utilizando los servicios de un proveedor, que a diferencia del diseño de LAN se hace absolutamente necesario. Las tecnologías de señalización y transporte que utilizan los proveedores de servicios suelen ser transparentes para los usuarios finales y generalmente son tecnologías propietarias. Las operaciones de una WAN se centran principalmente en las capas 1 y 2 del modelo OSI.

### Topologías

Una WAN puede utilizar varios tipos de topologías, las siguientes son las más comunes:

- **Topología punto a punto:** emplea un circuito punto a punto entre dos puntos finales. Típicamente se relaciona con las conexiones de líneas alquiladas dedicadas.
- **Topología hub-and-spoke:** se utiliza cuando se necesita una conexión entre múltiples sitios. Una sola interfaz en el hub puede ser compartida por todos los circuitos de remotos.
- **Topología de malla completa:** cualquier sitio puede comunicarse directamente con cualquier otro sitio. Una desventaja puede ser el gran número de circuitos virtuales que necesitan ser configurados y mantenidos.
- **Topología dual-homed:** proporciona redundancia, pero es una topología muy costosa.

### Conectividad

Dentro de una nube WAN generalmente es posible observar varios tipos de conexiones.

- **Líneas alquiladas.** También denominada conexión punto a punto o línea dedicada. Ofrece una única opción de comunicación por un medio exclusivo para el cliente. Las líneas alquiladas eliminan los problemas de conexión/desconexión de llamada, brindando a su vez mayor privacidad y seguridad. Suelen emplearse en conexiones serie síncronas manteniendo constante la utilización del ancho de banda. Suelen ser las líneas más costosas.
- **Circuitos conmutados.** Es un método de conmutación donde solo se establece conexión entre el emisor y el receptor únicamente durante el tiempo que dure la transmisión. Las sucesivas conexiones pueden o no utilizar la misma ruta que la anterior. Las conexiones de circuito conmutado suelen emplearse para entornos que tengan uso esporádico, enlaces de respaldo o enlaces bajo demanda. Este tipo de servicios también pueden utilizar los servicios de telefonía básicos mediante una conexión asíncrona conectada a un módem. Un ejemplo es el de RDSI.
- **Paquetes conmutados.** Es un método de conmutación donde los dispositivos comparten un único enlace punto a punto o punto multipunto para transportar paquetes desde un origen hacia un destino a través de una internetwork portadora. Estas redes utilizan circuitos virtuales para ofrecer conectividad, de forma permanente o conmutada (PVC o SVC). El destino es identificado por las cabeceras y el ancho de banda es dedicado, sin embargo una vez entregada la trama el proveedor puede compartirlo con otros clientes. Un ejemplo es el de Frame-Relay.
- **Celdas conmutadas.** Es un método similar al de conmutación de paquetes, solo que en lugar de ser paquetes de longitud variable se utilizan celdas de longitud fija que se transporten sobre circuitos virtuales. Un ejemplo es el de ATM.

### Terminología

Los términos y servicios asociados con las tecnologías WAN son cuantiosos, sin embargo los más utilizados son los siguientes:

- **CPE (Customer Premises Equipment):** dispositivos ubicados físicamente en el cliente.
- **Demarcación:** punto en el que finaliza el CPE y comienza el bucle local.
- **Bucle local:** también llamada última milla, es el cableado desde la demarcación hasta la oficina central del proveedor.
- **CO:** oficina central donde se encuentra el switch CO, dentro de la red pueden existir varios tipos de CO.
- **ISP (Internet Services Provider):** proveedor de servicios o acceso de Internet.
- **Telco:** nombre genérico utilizado para designar a una empresa de telecomunicaciones.
- **Nube:** grupo de dispositivos y recursos que se encuentran dentro de la red de pago.

### Estándares de capa 1

Los dispositivos WAN soportan los siguientes estándares de capa física:

- EIA/TIA-232.
- EIA/TIA-449.
- V.35.
- X.21.
- EIA-530.
- HSSI.

El gráfico ilustra los diferentes tipos de conectores para las interfaces serie.

!!! note "NOTA"

    Las tarjetas WIC (WAN interface Card) utilizan interfaces SmartSerial, lo que reduce notablemente el tamaño de sus antecesoras manteniendo las mismas propiedades.

### Estándares de capa 2

Dependiendo de la tecnología WAN utilizada es necesario configurar el tipo de encapsulamiento adecuado. Entre los tipos de encapsulación WAN se detallan:

- **HDLC (High-Level Data Link Control):** es el tipo de encapsulación por defecto de los routers Cisco, es un protocolo de enlace de datos síncrono propietario.
- **PPP (Point-to-Point Protocol):** es un protocolo estándar que ofrece conexiones de router a router y de host a red. Utiliza enlaces síncronos y asíncronos. Utiliza mecanismos de autenticación como PAP y CHAP.
- **SLIP (Serial Link Internet Protocol):** antecesor de PPP ya casi en desuso.
- **Frame-Relay:** es un protocolo de enlace de datos conmutado y estándar que maneja varios circuitos virtuales para establecer las conexiones. Posee corrección de errores y control de flujo.
- **X.25/LAPB (Link Access Procedure Balanced):** antecesor de Frame-Relay menos fiable que este último.
- **ATM (Asynchonous Transfer Mode):** estándar para la transmisión de celdas de longitud fija. Se utiliza indistintamente para voz, vídeo y datos.

El comando `encapsulation` habilita el encapsulamiento para una interfaz serie.

```text
Router(config-if)#encapsulation serial número
```

El comando `show interfaces` muestra el tipo de encapsulación en una interfaz determinada.

```text
Router>show interfaces serial 0
Serial 0 is up, line protocol is up
Hardware is MCI Serial
Internet address is 131.108.156.98, subnet mask is 255.255.255.240
MTU 1500 bytes, BW 1544 Kbit, DLY 20000 usec, rely 255/255, load 1/255
Encapsulation HDLC, loopback not set, keepalive set (10 sec)
Last input 0:00:00, output 0:00:00, output hang never
Last clearing of "show interface" counters never
Output queue 0/40, 5762 drops; input queue 0/75, 301 drops
Five minute input rate 9000 bits/sec, 16 packets/sec
Five minute output rate 9000 bits/sec, 17 packets/sec
5780806 packets input,785841604 bytes, 0 no buffer
Received 757 broadcasts, 0 runts, 0 giants
```

### Interfaces

Las interfaces seriales WAN responden de forma diferente a las interfaces Ethernet. Es importante poder identificar fallos para resolver posibles incidencias. En muchos casos las interfaces serie tienen errores que no son locales, fallos en las conexiones remotas provocarán caídas inesperadas en dichas interfaces. Los comandos `show interfaces` y `show controllers` brindan soporte logístico para definir errores o conflictos.

```text
Router>show interfaces serial 0
Serial 0 is up, line protocol is up
Hardware is MCI Serial
Internet address is 131.108.156.98, subnet mask is 255.255.255.240
MTU 1500 bytes, BW 1544 Kbit, DLY 20000 usec, rely 255/255, load 1/255
Encapsulation HDLC, loopback not set, keepalive set (10 sec)
Last input 0:00:00, output 0:00:00, output hang never
Last clearing of "show interface" counters never
Output queue 0/40, 5762 drops; input queue 0/75, 301 drops
Five minute input rate 9000 bits/sec, 16 packets/sec
Five minute output rate 9000 bits/sec, 17 packets/sec
5780806 packets input,785841604 bytes, 0 no buffer
Received 757 broadcasts, 0 runts, 0 giants
146124 input errors, 87243 CRC, 58857 frame, 0 overrun, 0 ignored, 3 abort
5298821 packets output, 765669598 bytes, 0 underruns
0 output errors, 0 collisions, 2941 interface resets, 0 restarts
2 carrier transitions
```

En la sintaxis anterior se resalta el estado de la interfaz, errores en las tramas, paquetes descartados, etc. Las dos sintaxis que siguen corresponden a un router DCE y un router DTE, observe el detalle del sincronismo y tipo de conexión.

```text
RouterDCE# sh controllers serial 0/0
Interface Serial0/0
Hardware is PowerQUICC MPC860
DCE V.35, clock rate 56000
idb at 0x81081AC4, driver data structure at 0x81084AC0
SCC Registers:
General [GSMR]=0x2:0x00000000, Protocol-specific [PSMR]=0x8
Events [SCCE]=0x0000, Mask [SCCM]=0x0000, Status [SCCS]=0x00
Transmit on Demand [TODR]=0x0, Data Sync [DSR]=0x7E7E
Interrupt Registers:
Config [CICR]=0x00367F80, Pending [CIPR]=0x0000C000
Mask [CIMR]=0x00200000, In-srv [CISR]=0x00000000
--More--
```

```text
RouterDTE#sh controllers serial 0/0
Interface Serial0/0
Hardware is PowerQUICC MPC860
DTE V.35 TX and RX clocks detected
idb at 0x81081AC4, driver data structure at 0x81084AC0
SCC Registers:
General [GSMR]=0x2:0x00000000, Protocol-specific [PSMR]=0x8
Events [SCCE]=0x0000, Mask [SCCM]=0x0000, Status [SCCS]=0x00
Transmit on Demand [TODR]=0x0, Data Sync [DSR]=0x7E7E
Interrupt Registers:
Config [CICR]=0x00367F80, Pending [CIPR]=0x0000C000
Mask [CIMR]=0x00200000, In-srv [CISR]=0x00000000
--More--
```

!!! tip "RECUERDE"

    Las interfaces DCE deben tener configurado el *clock rate*, es decir el sincronismo o velocidad. Una interfaz local DTE puede presentar fallos si la interfaz remota DCE no tiene correctamente configurado el valor del *clock rate*. Los *keepalive* deben ser iguales en ambos extremos.

## PPP

PPP (*Point-to-Point Protocol*) es un protocolo WAN de enlace de datos. Se diseñó como un protocolo abierto para trabajar con varios protocolos de capa de red, como IP, IPX y Apple Talk.

Se puede considerar a PPP la versión no propietaria de HDLC (*High-Level Data Link Control*), aunque el protocolo subyacente es considerablemente diferente. PPP funciona tanto con encapsulación síncrona como asíncrona porque el protocolo usa un identificador para denotar el inicio o el final de una trama. Dicho indicador se utiliza en las encapsulaciones asíncronas para señalar el inicio o el final de una trama y se usa como una encapsulación síncrona orientada a bit. Dentro de la trama PPP el bit de entramado es el encargado de señalar el comienzo y el fin de la trama PPP. El campo de direccionamiento de la trama PPP es un broadcast debido a que PPP no identifica estaciones individuales.

PPP se basa en el protocolo de control de enlaces LCP (*Link Control Protocol*), que establece, configura y pone a prueba las conexiones de enlace de datos que utiliza PPP. El protocolo de control de red NCP (*Network Control Protocol*) es un conjunto de protocolos (uno por cada capa de red compatible con PPP) que establece y configura diferentes capas de red para que funcionen a través de PPP. Para IP, IPX y Apple Talk, las designaciones NCP son IPCP, IPXCP y ATALKCP, respectivamente.

PPP provee mecanismos de control de errores y soporta los siguientes tipos de interfaces físicas:

- Serie síncrona.
- Serie asíncrona.
- RDSI.
- HSSI.

### Establecimiento de la conexión

El establecimiento de una sesión PPP tiene tres fases:

1. **Establecimiento del enlace:** en esta fase cada dispositivo PPP envía paquetes LCP para configurar y verificar el enlace de datos.
2. **Autenticación:** fase opcional, una vez establecido el enlace es elegido el método de autenticación. Normalmente los métodos de autenticación son PAP y CHAP.
3. **Protocolo de capa de red:** en esta fase el router envía paquetes NCP para elegir y configurar uno o más protocolos de capa de red. A partir de esta fase es posible el envío de tráfico a través del enlace.

### Autenticación PAP

PAP (*Password Authentication Protocol*) proporciona un método de autenticación simple utilizando un intercambio de señales de dos vías. El proceso de autenticación solo se realiza durante el establecimiento inicial del enlace.

Una vez completada la fase de establecimiento PPP, el nodo remoto envía repetidas veces al router extremo su usuario y contraseña hasta que se acepta la autenticación o se corta la conexión.

!!! tip "RECUERDE"

    PAP no es un método de autenticación seguro, las contraseñas se envían en modo abierto y no existe protección contra el registro de las mismas o los ataques externos.

### Configuración PPP con PAP

Para activar la encapsulación PPP con autenticación PAP en una interfaz se debe cambiar la encapsulación en dicha interfaz serial, el tipo de autenticación y configurar la dirección IP.

```text
Router(config-if)#encapsulation PPP
Router(config-if)#ppp authentication pap
Router(config-if)#ip address dirección máscara
Router(config-if)#no shutdown
```

Defina el nombre de usuario y la contraseña que espera recibir del router remoto.

```text
Router(config)#username nombre del remoto password contraseña
```

### Autenticación CHAP

CHAP (*Challenge Handshake Authentication Protocol*) es un método de autenticación más seguro que PAP. Se emplea durante el establecimiento del enlace y posteriormente se verifica periódicamente para comprobar la identidad del router remoto utilizando un saludo de tres vías. La contraseña es encriptada utilizando MD5, una vez establecido el enlace el router agrega un mensaje desafío que es verificado por ambos routers, si ambos coinciden, se acepta la autenticación, de lo contrario la conexión se cierra inmediatamente.

!!! tip "RECUERDE"

    CHAP ofrece protección contra ataques externos mediante el uso de un valor de desafío variable que es único e indescifrable. Esta repetición de desafíos limita la posibilidad de ataques.

### Configuración PPP con CHAP

Defina el nombre de usuario y la contraseña que espera recibir del router remoto.

```text
Router(config)#username nombre del remoto password contraseña
```

Puede usar el mismo nombre de host en múltiples routers cuando quiera que el router remoto crea que está conectado a un solo router.

Para activar la encapsulación PPP con autenticación CHAP en una interfaz se debe cambiar la encapsulación en dicha interfaz serial, el tipo de autenticación y la dirección IP:

```text
Router(config-if)#encapsulation PPP
Router(config-if)#ppp authentication chap
Router(config-if)#ip address IP máscara
Router(config-if)#no shutdown
```

### Verificación

- `show interfaces`. Muestra el estado de las interfaces con su autenticación.
- `debug ppp authentication`. Muestra el proceso de autenticación.

```text
Router#show int bri0/0
BRI0 is standby mode, line protocol is down
Hardware is BRI
Internet address is 10.1.99.55/24
MTU 1500 bytes, BW 64 Kbit, DLY 20000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation PPP, loopback not set
Last input never, output never, output hang never
Last clearing of "show interface" counters never
Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
Queueing strategy: weighted fair
Output queue: 0/1000/64/0 (size/max total/threshold/drops)
Conversations 0/0/16 (active/max active/max total)
Reserved Conversations 0/0 (allocated/max allocated)
Available Bandwidth 48 kilobits/sec
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
0 packets input, 0 bytes, 0 no buffer
```

## PPPoE

PPPoE (*Point-to-Point Protocol over Ethernet*) está descrito en la RFC 2516, combina dos estándares ampliamente conocidos como Ethernet y PPP, pudiendo hacer uso de autenticación PAP o CHAP para añadir seguridad.

Los clientes PPPoE son típicamente ordenadores personales conectados a un ISP a través de una conexión de banda ancha, tales como DSL o cable. El ISP utiliza PPPoE porque es compatible con el acceso de banda ancha de alta velocidad utilizando en su infraestructura de acceso remoto y porque es más fácil de utilizar para los clientes.

PPPoE permite la asignación de direcciones IP autenticadas. En este tipo de aplicación, el cliente y el servidor PPPoE están interconectados mediante los protocolos de capa 2 que se ejecutan sobre un DSL u otra conexión de banda ancha.

Normalmente existen tres métodos de conectar al abonado a la red:

- **Ubicar un router con capacidades DSL en la casa del abonado.** Este router tendrá un módem DSL integrado y un cliente PPPoE. Esta opción evita la necesidad de instalar software PPPoE en los dispositivos del abonado que requieran de conexión. El router proporcionará al abonado DHCP, NAT/PAT y otros servicios como pueden ser DNS.
- **Ubicar un router sin capacidades DSL en la casa del abonado.** Esta opción requiere la instalación adicional de un módem externo en la parte del abonado para terminar la conexión DSL. El router debería tener software PPPoE para proporcionar una conexión constante. Además ejecutará DHCP, NAT/PAT y otros servicios como pueden ser DNS.
- **Ubicar un módem DSL externo en la casa del abonado.** Con esta opción es necesario instalar clientes PPPoE en todos los hosts del abonado que requieran el servicio.

La capa 1 DSL termina en el DSLAM y quien se encarga de enviar los datos a través del medio existente, ya sea fibra o cobre, hasta la red ATM. Desde el CPE hasta el router de agregación solamente se utilizan las capas 1 y 2 del modelo OSI. Una vez que se negocia la sesión PPP entre CPE y el router de agregación comienza la utilización de la capa 3. El direccionamiento IP que recibe el CPE es asignado por el proveedor usando DHCP. El aprovisionamiento de abonados se realiza por abonado y no por sitio. Para proporcionar conexiones punto a punto sobre Ethernet cada sesión PPP debe aprender la dirección MAC del par remoto y establecer una sesión única. Esto es realizado por un protocolo incluido en PPPoE que realiza este descubrimiento.

### Fases

El proceso de inicialización de PPPoE tiene dos fases adicionales:

- **Fase de descubrimiento.** Para iniciar la sesión PPP el CPE debe primero realizar un descubrimiento para identificar la MAC del dispositivo con el que va a establecer la vecindad con el par. El CPE descubre todos los recursos disponibles en el router de agregación y elige uno.
- **Fase de sesión PPP.** Una vez que la fase de sesión PPPoE comienza los datos PPP pueden ser transmitidos. Esta transmisión es enteramente unicast entre el CPE y el router de agregación.

### Tamaño MTU

Cliente especifica el tamaño de la MTU en la ventana TCP en el saludo de 3 vías. Se utiliza el tamaño máximo de la porción de datos que permite TCP MSS (*Maximum Segment Size*). Por defecto el tamaño del MSS es de 1460 bytes, cuando la MTU por defecto es de 1500 bytes.

La RFC 2516 establece que el tamaño de la carga útil negociada en PPPoE sea de 1492 bytes. La cabecera PPPoE es 6 bytes y hay que sumarle 2 bytes del campo `Protocol-ID`. Si se suman esas 3 cifras se obtiene un valor de 1500 bytes, que es el valor por defecto de la MTU en interfaces Ethernet.

La figura siguiente muestra la estructura de la trama PPPoE:

### Verificación

Para ver la dirección IP asignada por el ISP en la interfaz ejecute el siguiente comando.

```text
Router#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     unassigned      YES unset  adm down              down
GigabitEthernet0/1     unassigned      YES unset  up                    up
Serial0/0/0            unassigned      YES unset  adm down              down
Serial0/0/1            unassigned      YES unset  adm down              down
Dialer1                10.1.1.2        YES IPCP  up                    up
```

El comando `show running-config` muestra la encapsulación y la autenticación. Puede hacerse una búsqueda selectiva utilizando el parámetro `section`.

```text
Router#show run | section interface dialer1
interface Dialer1
 ip address negotiated
 encapsulation ppp
 dialer pool 1
 dialer-group 1
 no cdp enable
 ppp authentication pap chap callin
 ppp pap sent-username cisco password ccna
 ppp chap hostname cisco
 ppp chap password ccna
!
ip route 0.0.0.0 0.0.0.0 Dialer1
```

El comando `show interface dialer` muestra entre otros datos la MTU y la encapsulación en la interfaz.

```text
Router#show interfaces dialer 1
Dialer1 is up, line protocol is up (spoofing)
Hardware is Unknown
Internet address is 212.93.198.1/32
MTU 1500 bytes, BW 56 Kbit, DLY 20000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation PPP, loopback not set
DTR is pulsed for 1 seconds on reset
.....................................
```

El proceso de negociación puede verse con el comando `debug`, recuerde siempre terminar el proceso con un `undebug all`.

```text
Router#debug ppp negotiation
PPP protocol negotiation debugging is on
Router#
2w3d: Vi1 PPP: No remote authentication for call-out
2w3d: Vi1 PPP: Phase is ESTABLISHING
2w3d: Vi1 LCP: O CONFREQ [Open] id 146 len 10
2w3d: Vi1 LCP: MagicNumber 0x8CCF0E1E (0x05068CCF0E1E)
2w3d: Vi1 LCP: O CONFACK [Open] id 102 Len 15
2w3d: Vi1 LCP: AuthProto CHAP (0x0305C22305)
2w3d: Vi1 LCP: MagicNumber 0xD945AD0A (0x0506D945AD0A)
2w3d: Di1 IPCP: Remove route to 20.20.2.1
2w3d: Vi1 LCP: I CONFACK [ACKsent] id 146 Len 10
2w3d: Vi1 LCP: MagicNumber 0x8CCF0E1E (0x05068CCF0E1E)
2w3d: Vi1 LCP: State is Open
2w3d: Vi1 PPP: Phase is AUTHENTICATING, by the peer
2w3d: Vi1 CHAP: I CHALLENGE id 79 Len 33 from "6400-2-NRP-2"
2w3d: Vi1 CHAP: O RESPONSE id 79 Len 28 from "John"
2w3d: Vi1 CHAP: I SUCCESS id 79 Len 4
2w3d: Vi1 PPP: Phase is UP
2w3d: Vi1 IPCP: O CONFREQ [Closed] id 7 Len 10
2w3d: Vi1 IPCP: Address 0.0.0.0 (0x030600000000)
2w3d: Vi1 IPCP: I CONFREQ [REQsent] id 4 Len 10
2w3d: Vi1 IPCP: Address 20.20.2.1 (0x030614140201)
2w3d: Vi1 IPCP: O CONFACK [REQsent] id 4 Len 10
2w3d: Vi1 IPCP: Address 20.20.2.1 (0x030614140201)
2w3d: Vi1 IPCP: I CONFNAK [ACKsent] id 7 Len 10
2w3d: Vi1 IPCP: Address 40.1.1.2 (0x030628010102)
2w3d: Vi1 IPCP: O CONFREQ [ACKsent] id 8 Len 10
2w3d: Vi1 IPCP: Address 40.1.1.2 (0x030628010102)
2w3d: Vi1 IPCP: I CONFACK [ACKsent] id 8 Len 10
2w3d: Vi1 IPCP: Address 40.1.1.2 (0x030628010102)
2w3d: Vi1 IPCP: State is Open
2w3d: Di1 IPCP: Install negotiated IP interface address 40.1.1.2
2w3d: Di1 IPCP: Install route to 20.20.2.1
Router#undebug all
```

## MULTILINK PPP

Multilink PPP, se define en la RFC 1990, es una variante del PPP que se utiliza para agregar múltiples enlaces WAN en un solo canal lógico para el transporte de tráfico. Permite el equilibrio de carga de tráfico de diferentes enlaces y permite un cierto nivel de redundancia en de la línea en caso de fallo de un enlace. Proporciona además interoperabilidad entre varios proveedores.

Multilink PPP permite que los paquetes sean fragmentados y que los fragmentos se envíen al mismo tiempo a través de múltiples enlaces punto a punto con la misma dirección remota y que sean re-ensamblados en el destino. Multilink PPP proporciona un ancho de banda bajo demanda y reduce la latencia de transmisión a través de enlaces WAN. Multilink PPP puede trabajar sobre interfaces simples o múltiples síncronas y asíncronas que se han configurado para soportar tanto llamada bajo demanda como encapsulación PPP.

Multilink PPP trabaja con interfaces PPP totalmente funcionales. Un grupo Multilink PPP puede tener varios enlaces que conectan los dispositivos pares. Estos enlaces pueden ser enlaces serie o enlaces de banda ancha (Ethernet o ATM). Mientras cada enlace se comporta como una interfaz en serie estándar, todos los enlaces enlazados funcionan como una unidad.

### Configuración

El primer paso en la configuración de MLPPP es la configuración de la interfaz.

```text
Router(config)# interface multilink-bundle-number
Router(config-if)# ip address ip-address mask
```

Establecer políticas de QoS entrantes y salientes.

```text
Router(config-if)# service-policy output policy-map-name
Router(config-if)# service-policy input policy-map-name
```

Especifique un tamaño máximo en unidades de tiempo para fragmentos de paquetes y el intercalado de paquetes.

```text
Router(config-if)# ppp multilink fragment milliseconds[microseconds]
Router(config-if)# ppp multilink interleave
```

La interfaz MLPP debe estar asociada a una interfaz física con encapsulación PPP y habilitado el PPP multilink en dicha interface.

```text
Router(config)# interface serial slot/port:timeslot
Router(config-if)# encapsulation ppp
Router(config-if)# ppp multilink
```

Para designar la interfaz a un grupo específico, se utiliza el siguiente comando:

```text
Router(config-if)# ppp multilink group-number
```

Cuando se configura el comando `ppp multilink group` en un enlace, el comando aplica las siguientes restricciones en el enlace:

- El enlace no se le permite unirse a cualquier grupo que no sea la interfaz de grupo indicado.
- La sesión PPP debe terminarse si el dispositivo par intenta unirse a un grupo diferente.

### Verificación

Los comandos `show ppp multilink` y `show interfaces` permiten ver características de la configuración.

```text
Router# show ppp multilink
Multilink2, bundle name is 7206-2
Endpoint discriminator is 7206-2
Bundle up for 00:00:09, 1/255 load
Receive buffer limit 12000 bytes, frag timeout 1500 ms
0/0 fragments/bytes in reassembly list
0 lost fragments, 0 reordered
0/0 discarded fragments/bytes, 0 lost received
0x0 received sequence, 0x3 sent sequence
Member links:1 active, 1 inactive (max not set, min not set)
Se3/2, since 00:00:10, 240 weight, 232 frag size
Se3/3 (inactive)
```

## NAT

NAT (*Network Address Traslation*) permite acceder a Internet traduciendo las direcciones privadas en direcciones IP registradas. Incrementa la seguridad y la privacidad de la red local al traducir el direccionamiento interno a uno externo.

NAT tiene varias formas de trabajar según los requisitos y la flexibilidad de que se disponga, cualquiera de ellas es sumamente importante a la hora de controlar el tráfico hacia el exterior:

- **Estáticamente:** NAT permite la asignación de una a una entre las direcciones locales y las exteriores o globales.
- **Dinámicamente:** NAT permite asignar a una red IP interna a varias externas incluidas en un grupo o *pool* de direcciones.
- **PAT (Port Address Traslation):** es una forma de NAT dinámica, comúnmente llamada NAT sobrecargado, que asigna varias direcciones IP internas a una sola externa. PAT utiliza números de puertos de origen únicos en la dirección global interna para distinguir entre las diferentes traducciones.

### Terminología NAT

En NAT se utiliza comúnmente la siguiente terminología:

- **Dirección local interna:** es la dirección IP asignada a un host de la red interna.
- **Dirección global interna:** es la dirección IP asignada por el proveedor de servicio que representa a la dirección local ante el mundo.
- **Dirección local externa:** es la dirección IP de un host externo tal como lo ve la red interna.
- **Dirección global externa:** es una dirección IP asignada por el propietario a un host de la red externa.

### Configuración estática

Para configurar NAT estáticamente utilice el siguiente comando:

```text
Router(config)#ip nat inside source static ip-interna ip-global
```

Defina cuáles serán las interfaces de entrada y salida y su correspondiente dirección IP:

```text
Router(config)#interface tipo número
Router(config-if)#ip address ip-interna máscara
Router(config-if)#ip nat inside
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)# interface tipo número
Router(config-if)#ip address ip-global máscara
Router(config-if)#ip nat outside
Router(config-if)#no shutdown
Router(config-if)#exit
```

### Configuración dinámica

Para configurar NAT dinámicamente se debe crear un *pool* de direcciones, para ello utilice el siguiente comando:

```text
Router(config)#ip nat pool nombre ip-inicio ip-final netmask máscara
```

Defina una lista de acceso que permita solo a las direcciones que deban traducirse:

```text
Router(config)#access-list 1 permit ip-interna-permitida wildcard
```

Asocie la lista de acceso al *pool*:

```text
Router(config)#ip nat inside source list 1 pool nombre-del-pool
```

Defina las interfaces de entrada y salida:

```text
Router(config)#interface tipo número
Router(config-if)#ip address ip-interna máscara
Router(config-if)#ip nat inside
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)# interface tipo número
Router(config-if)#ip address ip-global máscara
Router(config-if)#ip nat outside
Router(config-if)#no shutdown
Router(config-if)#exit
```

### Configuración de PAT

PAT o NAT sobrecargado se configura definiendo una lista de acceso que permita solo a las direcciones que deban traducirse:

```text
Router(config)#access-list 1 permit ip-interna-permitida wildcard
```

Asocie dicha lista a la interfaz de salida agregando al final el comando `overload`:

```text
Router(config)#ip nat inside source list 1 interface tipo número overload
```

Defina las interfaces de entrada y salida:

```text
Router(config)#interface tipo número
Router(config-if)#ip address ip-interna máscara
Router(config-if)#ip nat inside
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)# interface tipo número
Router(config-if)#ip address ip-global máscara
Router(config-if)#ip nat outside
Router(config-if)#no shutdown
Router(config-if)#exit
```

### Verificación

- `show ip nat translations`. Muestra las traslaciones de direcciones IP.
- `show ip nat statistics`. Muestra las estadísticas NAT.
- `debug ip nat`. Muestra los procesos de traslación de dirección.

```text
Router# show ip nat translations
Pro  Inside global      Inside local       Outside local      Outside global
TCP  171.16.233.209    192.168.1.95      ---                 ---
UDP  171.16.233.210    192.168.1.89      ---                 ---
```

```text
Router# show ip nat statistics
Total translations: 2 (0 static, 2 dynamic; 0 extended)
Outside interfaces: Serial0
Inside interfaces: Ethernet1
Hits: 135 Misses: 5
Expired translations: 2

Dynamic mappings:
-- Inside Source
access-list 1 pool CCNA refcount 2
 pool CCNA: netmask 255.255.255.240
        start 172.16.233.208 end 172.16.233.221
        type generic, total addresses 14, allocated 2 (14%), misses 0
```

## VPN

Una VPN (*Virtual Private Networks*) se utiliza principalmente para conectar dos redes privadas a través de la red pública de datos. Sin embargo puede tener varias aplicaciones más. Un túnel es básicamente un método para encapsular un protocolo en otro. La existencia de protocolos no enrutables hacen que el uso de las VPN sea imprescindible para enviar el tráfico que utiliza este tipo de protocolos. Incluso para otros tipos de protocolos enrutables cuya dificultad de enrutamiento es elevada, se hace más sencillo cuando este se envía por un túnel.

Otra buena razón para la utilización de túneles es evitar los problemas que suelen dar los protocolos de enrutamiento en redes extremadamente grandes debido a que muchas veces su arquitectura no coincide en tipos de protocolos o entre áreas.

Los túneles son sumamente útiles en laboratorios o ambientes de prueba donde se intenta emular las topologías de red más complejas.

Existen muchas variaciones diferentes para la configuración de las VPN, aun para las más comunes. En el caso de este libro se utilizará como ejemplo de configuración la de túneles GRE (*Generic Routing Encapsulation*) que es una norma abierta. Existen varias versiones de GRE, la versión 0 es la común, la versión 1 también llamada PPTP (*Point to Point Tunneling Protocol*) incluye una capa intermedia PPP, mientras que GRE soporta directamente protocolos de capa 3 como IP e IPX. GRE no utiliza TCP ni UDP, trabaja directamente con IP, identificado con el número 47. Posee características propias de entrega, verificación e integridad.

### Funcionamiento

Los routers encapsulan los paquetes IP con la etiqueta GRE y los envían por la red al router de destino al final del túnel, el router remoto desencapsula los paquetes quitándoles la etiqueta GRE dejándolos listos para enrutarlos localmente. El paquete GRE pudo haber cruzado una gran cantidad de router para alcanzar su destino, sin embargo para este, solo ha efectuado un único salto hacia el destino. Esto significa que en el encabezado IP el tiempo de vida del paquete TTL (*Time To Live*) se ha incrementado una vez.

La utilización de las VPN obliga muchas veces a los routers a segmentar los paquetes para enviarlos a través del túnel debido a que su tamaño excede la MTU que estos pueden soportar. En ciertos casos pueden existir dificultades con las aplicaciones que ven las cabeceras de los paquetes IP duplicadas, sin embargo, esto ocurre en raros casos. Cuando el router no puede segmentar el paquete debe descartarlos, en estos casos envía mensajes ICMP al dispositivo origen para que regule el tamaño de los paquetes. Como resultado final de este proceso es que para el uso eficaz de las VPN el tamaño de las MTU debe reducirse.

!!! note "NOTA"

    El término "túnel VPN" implica que el paquete encapsulado se ha cifrado, mientras que el término "túnel" se refiere al mecanismo de enviar paquetes de un protocolo encapsulados dentro de otro.

### IPSec

IPSec (*Internet Protocol Security*) es un conjunto de protocolos y algoritmos de seguridad diseñados para la protección del tráfico de red para trabajar con IPv4 e IPv6 de modo transparente o modo túnel que soporta una gran variedad de encriptaciones y autenticaciones. El principio básico de funcionamiento de IPSec es la independencia algorítmica que le permite efectuar cambios de algoritmos si alguien descubre un fallo crítico o si existe otro más eficaz.

IPSec está diseñado para proporcionar seguridad sobre la capa de red IP, por lo tanto, puede ser utilizado eficazmente sobre protocolos como TCP, UDP, ICMP y otros. Esto es muy importante porque significa que se puede usar IPSec con protocolos o aplicaciones inseguras logrando un excelente nivel de seguridad global.

IPSec se introdujo para proporcionar servicios de seguridad tales como:

- **Confidencialidad:** el tráfico se encripta de manera segura para que no pueda ser leído por nadie más que las partes a las que está dirigido.
- **Integridad:** certificar la integridad de los datos, asegurando que el tráfico no ha sido modificado a lo largo de su trayecto.
- **Autenticación:** autenticar a los extremos reconociendo el tráfico que proviene de un extremo seguro y validado.
- **Anti-repetición:** evita que una copia ilegitima de los paquetes se intente utilizar luego para parecer un usuario legítimo.

IPSec utiliza dos protocolos importantes de seguridad:

- **AH (Authentication Header)** que le permite asegurar que los datos no se han manipulado de forma alguna, y que realmente viene del dispositivo de la fuente correcta. AH no encripta directamente los datos.
- **ESP (Encapsulating Security Payload)** proporciona encriptación a la carga útil del paquete para el envío seguro de los datos.

La autenticación y la encriptación se utilizan en funciones completamente diferentes pero absolutamente complementarias. Al usar IPSec, es sumamente recomendable el uso de ambos protocolos.

IPSec tiene dos modos principales de funcionamiento:

- **Modo túnel:** todo el paquete IP (datos más cabeceras del mensaje) es cifrado y/o autenticado. Debe ser entonces encapsulado en un nuevo paquete IP para que funcione el enrutamiento. El modo túnel se utiliza para comunicaciones red a red, VPN.
- **Modo transporte:** solo la carga útil (los datos que se transfieren) del paquete IP es cifrada y/o autenticada. El enrutamiento permanece intacto, ya que no se modifica ni se cifra la cabecera IP. Este método se usa para comunicaciones de ordenador a ordenador.

### SSL VPN

SSL VPN (*Secure Sockets Layer VPN*) es una tecnología emergente que proporciona acceso remoto con las mismas capacidades que una de VPN, sumando la función de SSL que viene integrado en los navegadores Web modernos.

SSL VPN permite a los usuarios remotos autorizados desde cualquier lugar con conexión a Internet utilizar un navegador web para establecer conexiones VPN de acceso remoto, generando mejoras en la productividad y disponibilidad.

SSL VPN tiene algunas características únicas en comparación con otras tecnologías VPN existentes. La más notable es que SSL VPN utiliza el protocolo SSL y su sucesor, TLS (*Transport Layer Security*), para proporcionar una conexión segura entre usuarios remotos y los recursos de la red interna. Actualmente esta función SSL/TLS está incorporada en todos los navegadores web.

A diferencia de la tecnología tradicional IPsec VPN, que requiere la instalación de software cliente IPSec antes de que se pueda establecer una conexión, los usuarios no necesitan instalar ningún software cliente para utilizar SSL VPN. Como consecuencia de este resultado, SSL VPN también se conoce como *clientless VPN* o *Web VPN*.

### Túnel GRE

Los túneles GRE (*Generic Routing Encapsulation*) permiten encapsular cualquier tipo de tráfico. En un principio se utilizaban para encapsular tráfico no IP dentro de las redes IP, pero también permiten la encapsulación de tráfico IP. Funcionan encapsulando la cabecera IP original dentro de la cabecera GRE.

Algunas ventajas y desventajas de los túneles GRE son las siguientes:

- Es similar a un túnel IPsec en el sentido de que ambos encapsulan la cabecera original IP.
- No ofrece mecanismos de control de flujo.
- GRE añade un mínimo de 24 bytes a la cabecera, en los que se incluye la nueva cabecera IP.
- Permiten tunelizar cualquier protocolo de capa 3.
- Permite que los protocolos de enrutamiento viajen a través del túnel.
- A diferencia de los túneles IPsec los túneles GRE no coordinan parámetros antes de enviar tráfico. Mientras el otro extremo del túnel sea alcanzable permite enviar tráfico, sin proporcionar confiabilidad o mirar los números de secuencia. GRE deja estas tareas para protocolos de capas superiores.
- GRE ofrece una seguridad limitada mucho más débil que la de IPsec. Cuenta con un proceso de encriptación pero la clave viaja junto con los paquetes, dejándola expuesta a que sea robada.
- A diferencia de IPsec los túneles GRE permiten que el tráfico de los protocolos de enrutamiento viaje a través de ellos. Con IPsec se limita al uso de rutas estáticas, haciendo que la escalabilidad sea un problema.

La combinación de GRE junto con IPsec se denomina *GRE over IPsec* y permite que estos dos mecanismos de tunelización se complementen entre sí.

### Configuración de túnel GRE

En la actualidad los túneles GRE se utilizan normalmente para transportar tráfico IP en una red IP o sobre un túnel IPsec. El origen del túnel GRE en un extremo ha de ser el final del túnel en el otro y viceversa. Esta validación es llevada a cabo inicialmente cuando se establece el túnel. Es necesario configurar una subred apropiada y común para el túnel.

La configuración del túnel GRE incluye:

- Crear la interfaz túnel.
- Origen del túnel. Interfaz o dirección IP local del router.
- Destino del túnel. Dirección IP en el extremo remoto.
- Modo del túnel. Por defecto GRE/IP.
- Tráfico del túnel. Datos que viajan a través del túnel y por lo tanto van encapsulados en GRE.

```text
Router(config)#interface tunnel número
Router(config-if)#ip address dirección máscara
Router(config-if)#tunnel source interfaz-oigen
Router(config-if)#tunnel destination ip-destino
Router(config-if)#tunnel mode [gre|ipv6ip] ip
```

## OTRAS TECNOLOGÍAS DE ACCESO WAN

### Metro Ethernet

La tecnología Metro Ethernet es un servicio ofrecido por los proveedores de telecomunicaciones para interconectar redes LAN ubicadas a grandes distancias, ejecutando un transporte WAN. Esta tecnología se basada en el estándar Ethernet, y puede cubrir un área metropolitana. Es comúnmente usada como una red de acceso para conectar a las empresas con los abonados y hacia Internet.

Ethernet es la tecnología de red más utilizada por las empresas, por lo que el acceso basado en Ethernet puede ser fácilmente implementado en la red del cliente. Estas características permiten a una empresa conectar sus sucursales en una sola intranet mediante Metro Ethernet.

Las redes Metro Ethernet, están soportadas principalmente por medios de transmisión como cobre y fibra óptica, existiendo también soluciones de radio frecuencia.

Los beneficios que ofrece Metro Ethernet son los siguientes:

- **Fiabilidad**, los enlaces pueden constituirse por múltiples conexiones de cobre y/o fibra.
- **Fácil administración**, interconectando con Ethernet se simplifica las operaciones de red, administración, manejo y actualización.
- **Fácil implementación**, se emplean interfaces Ethernet que son las más difundidas para las soluciones de red.
- **Ancho de banda**, los servicios Metro Ethernet permiten a los usuarios acceder a conexiones de banda ancha a menor costo.
- **Flexibilidad**, Metro Ethernet también es una red multiservicio que soporta una amplia gama de aplicaciones, contando con mecanismos donde se incluye soporte como puede ser telefonía IP y vídeo.

### DMVPN

DMVPN (*Dynamic Multipoint VPN*) es una solución de software de Cisco para escenarios en los que múltiples sitios remotos necesitan comunicarse entre sí evitando pasar por un sitio central. Este recurso permite crear y eliminar múltiples redes privadas virtuales de una manera fácil, dinámica y escalable.

Las topologías DMVPN pueden utilizar:

- Túneles hub-to-spoke.
- Túneles hub-to-spoke y spoke-to-spoke.

Para que DMVPN funcione son necesarias las siguientes tecnologías:

- NHRP (*Next Hop Resolution Protocol*).
- Túneles mGRE (*Multipoint Generic Routing Encapsulation*).
- IPsec (*IP Security*).

La siguiente figura muestra una topología hub-and-spoke en la que la oficina central actúa como el hub. Cuando por ejemplo los sitios remotos B y C necesitan comunicarse entre ellos un nuevo túnel DMVPN es creado entre dichos sitios.

### MPLS

MPLS (*Multiprotocol Label Switching*) es una tecnología WAN que está definida en la RFC 3031. MPLS proporciona un mecanismo por el cual los paquetes son etiquetados sin la necesidad de examinar la cabecera de capa 3. En lugar de mirar en la cabecera de capa 3 los dispositivos MPLS sencillamente miran en las etiquetas haciéndolos independientes de los protocolos de capa 3. La etiqueta de un paquete de entrada es examinada y comparada con la base de datos de etiquetas. Basándose en la información contenida en dicha tabla se le asigna una nueva etiqueta para ser asociada al paquete y que sea enviado fuera de la interfaz correspondiente.

MPLS es un mecanismo de conmutación que ejecuta un proceso de conmutar paquetes MPLS incluyendo el análisis de la etiqueta. Esta etiqueta contiene la información de envío necesaria para poder conmutar el paquete dentro del switch MPLS llamado LSR que no necesita ejecutar enrutamiento de capa 3.

Las etiquetas normalmente corresponden a redes de destino aunque también podrían corresponder a otro tipo de variables como son VPN de capa 3, circuitos virtuales de capa 2, calidad de servicio, etc. Estas opciones son configurables en cada uno de los dispositivos. Por esta razón MPLS no fue diseñado únicamente para enviar paquetes IP.

Los principios básicos de enrutamiento también se aplican a MPLS, esencialmente la elección del dispositivo del siguiente salto sin importar la naturaleza del proceso de enrutamiento que se está ejecutando.

La red MPLS aunque es propiedad del ISP no deja de ser una extensión de la red de la empresa.

Las redes MPLS convergen de manera dinámica, soportan múltiples protocolos de enrutamiento y pueden utilizar políticas de calidad de servicio.

El mecanismo de MPLS en los routers Cisco está basado en CEF (*Cisco Express Forwarding*) y es un mecanismo necesario para el funcionamiento de las mismas.

### DSL

Las líneas DSL (*Digital Suscriber Line*) son soluciones comunes de acceso que cuentan con la ventaja añadida de que se pueden utilizar sobre la infraestructura telefónica existente, lo que hace innecesario desplegar un nuevo cable para su implementación.

La transmisión múltiple de señales a través de un cable se realiza por medio de la modulación de la señal. La modulación es la adición de información a una señal portadora electrónica u óptica. La voz utiliza solamente una pequeña parte de la frecuencias disponibles en los cables de par trenzado.

La implementación de esta tecnología es económica gracias al uso del cableado existente pero guarda ciertas limitaciones como:

- La distancia del proveedor al cliente.
- Interferencias de radiofrecuencia.
- No puede ser implementada sobre fibra óptica.
- Atenuación y degradación de la señal en largas distancias.

Existen dos variantes de DSL:

- **ADSL**, DSL Asimétrica. Las velocidades de subida y bajada son diferentes. Es la más popular para uso doméstico o pequeñas oficinas.
- **SDSL**, ASL Simétrica. Las velocidades de subida y bajada son idénticas.

## CASO PRÁCTICO

### Configuración PPP con CHAP

Las siguientes sintaxis muestran las configuraciones básicas de una conexión serie punto a punto utilizando una encapsulación PPP y una autenticación CHAP:

Router Local:

```text
Router(config)#hostname Local
Local(config)#username Remoto password cisco
Local(config)#interface serial 0/1
Local(config-if)#encapsulation PPP
Local(config-if)#ppp authentication chap
Local(config-if)#ip address 203.24.33.1 255.255.255.0
Local(config-if)#no shutdown
Local(config-if)#exit
Local(config)#interface ethernet 0/1
Local(config-if)#ip address 192.168.0.1 255.255.255.0
Local(config-if)#no shutdown
Local(config-if)#exit
Local(config)#router ospf 100
Local(config-router)#network 192.168.0.0 0.0.0.255 area 0
Local(config-router)#network 203.24.33.0 0.0.0.255 area 0
```

Router Remoto:

```text
Router(config)#hostname Remoto
Remoto(config)#username Local password cisco
Remoto(config)#interface serial 0/0
Remoto(config-if)#clockrate 56000
Remoto(config-if)#encapsulation PPP
Remoto(config-if)#ppp authentication chap
Remoto(config-if)#ip address 203.24.33.2 255.255.255.0
Remoto(config-if)#no shutdown
Remoto(config)#interface ethernet 0/0
Remoto(config-if)#ip address 198.170.0.1 255.255.255.0
Remoto(config-if)#no shutdown
Remoto(config-if)#exit
Remoto(config)#router ospf 100
Remoto(config-router)#network 198.170.0.0 0.0.0.255 area 0
Remoto(config-router)#network 203.24.33.0 0.0.0.255 area 0
```

Verificación en el router Local:

```text
Local#sh int serial 0/0
Serial0/0 is up, line protocol is up (connected)
Hardware is HD64570
Internet address is 203.24.33.1/24
MTU 1500 bytes, BW 1544 Kbit, DLY 20000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation PPP, loopback not set, keepalive set (10 sec)
LCP Open
Open: IPCP, CDPCP
Last input never, output never, output hang never
```

### Configuración de NAT dinámico

El ejemplo muestra la configuración de un router con NAT dinámico donde se ha creado un *pool* de direcciones IP llamado INTERNET, la interfaz entrante es la ethernet 0/0 y la saliente la interfaz serial 0/1:

```text
Router(config)#ip nat pool INTERNET 20.20.10.20 20.20.10.30 netmask 255.255.255.0
Router(config)#access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)#ip nat inside source list 1 pool INTERNET
Router(config)#interface ethernet 0/0
Router(config-if)#ip address 192.168.1.25 255.255.255.0
Router(config-if)#ip nat inside
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)# interface serial 0/1
Router(config-if)#ip address 20.20.10.11 255.255.255.0
Router(config-if)#ip nat outside
Router(config-if)#no shutdown
Router(config-if)#exit
Router#show ip nat translations
Pro  Inside global      Inside local       Outside local      Outside global
tcp  20.20.10.22:1025   192.168.1.3:1025   20.20.10.12:23     20.20.10.12:23
icmp 20.20.10.22:33     192.168.1.2:33     20.20.10.12:33     20.20.10.12:33
icmp 20.20.10.22:34     192.168.1.3:34     20.20.10.12:34     20.20.10.12:34
```

!!! tip "RECUERDE"

    Las listas de acceso asociadas a NAT deben permitir solo el acceso a las redes que se van a convertir, sea específico y no utilice el `permit any`.

### Configuración de una VPN de router a router

Se describe a continuación la configuración de un túnel GRE en una VPN de router a router según la siguiente topología.

Configuración del router remoto:

```text
Router#configure terminal
Router(config)#hostname remoto
remoto(config)#interface Tunnel 0
remoto(config-if)#ip address 192.168.1.1 255.255.255.252
remoto(config-if)#tunnel source serial 0/0/0
remoto(config-if)#tunnel destination 172.16.2.1
remoto(config-if)#no shut
remoto(config-if)#exit
remoto(config)#interface Serial 0/0/0
remoto(config-if)#ip address 172.16.2.2 255.255.255.0
remoto(config-if)#no shutdown
remoto(config-if)#exit
remoto(config)#interface gigabitEthernet 0/0
remoto(config-if)#ip address 192.168.16.1 255.255.255.0
remoto(config-if)#no shutdown
remoto(config-if)#exit
remoto(config)#ip route 192.168.15.0 255.255.255.0 192.168.1.2
remoto(config)#end
```

Configuración del router central:

```text
Router#configure terminal
Router(config)#hostname central
central(config)#interface Tunnel1
central(config-if)#ip address 192.168.1.2 255.255.255.252
central(config-if)#tunnel source serial 0/0/0
central(config-if)#tunnel destination 172.16.1.1
central(config-if)#no shut
central(config-if)#exit
central(config)#interface Serial 0/0/0
central(config-if)#ip address 172.16.2.1 255.255.255.0
central(config-if)#no shutdown
central(config-if)#exit
central(config)#interface gigabitEthernet 0/0
central(config-if)#ip address 192.168.15.1 255.255.255.0
central(config-if)#no shutdown
central(config-if)#exit
central(config)#ip route 192.168.16.0 255.255.255.0 192.168.1.1
central(config)#end
central#sh int tunnel 1
Tunnel1 is up, line protocol is up (connected)
Hardware is Tunnel
Internet address is 192.168.1.2/30
MTU 17916 bytes, BW 100 Kbit/sec, DLY 50000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation TUNNEL, loopback not set
Keepalive not set
Tunnel source 172.16.2.1 (Serial0/0/0), destination 172.16.2.2
Tunnel protocol/transport GRE/IP
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
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
...................................
```

```text
remoto#sh ip route
Codes: L-local, C - connected, S - static, R - RIP, M - mobile, B - BGP
      D-EIGRP, EX-EIGRP external, O-OSPF, IA-OSPF inter area
      N1-OSPF NSSA external type 1, N2-OSPF NSSA external type 2
      E1-OSPF external type 1, E2-OSPF external type 2, E-EGP
      i-IS-IS, L1-IS-IS level-1,L2-IS-IS level-2,ia-IS-IS interarea
      *-candidate default, U - per-user static route, o-ODR
      P-periodic downloaded static route

Gateway of last resort is not set

     172.16.0.0/16 is variably subnetted, 2 subnets, 2 masks
C       172.16.2.0/24 is directly connected, Serial0/0/0
L       172.16.2.2/32 is directly connected, Serial0/0/0
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/30 is directly connected, Tunnel0
L       192.168.1.1/32 is directly connected, Tunnel0
S       192.168.15.0/24 [1/0] via 192.168.1.2
     192.168.16.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.16.0/24 is directly connected, GigabitEthernet0/0
L       192.168.16.1/32 is directly connected, GigabitEthernet0/0
```

```text
central#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.15.1    YES manual up                    up
Serial0/0/0            172.16.2.1      YES manual up                    up
Tunnel1                192.168.1.2     YES manual up                    up
```

## FUNDAMENTOS PARA EL EXAMEN

- Estudie las terminologías, estándares y conexiones utilizadas en las redes WAN.
- Recuerde los tipos de encapsulación de capa 2 de las redes WAN.
- Memorice los conceptos sobre PPP y los pasos en el establecimiento de una sesión PPP.
- Tenga en cuenta los tipos de autenticaciones PPP y sus diferencias fundamentales.
- Analice las diferencias entre PPP, PPPoE y MLPPP.
- Estudie los fundamentos sobre NAT, los diferentes tipos de traducciones y para qué se utilizan en cada caso.
- Recuerde las terminologías empleadas en la tarea de configuración de NAT.
- Analice el proceso de traslación de una dirección IP a otra.
- Estudie los fundamentos y funciones de una VPN.
- Analice la seguridad que debe proporcionar una VPN y el funcionamiento de IPsec.
- Estudie, analice y ejercite en dispositivos reales o en simuladores todos los comandos necesarios para las configuraciones de PPP y NAT y todos los comandos para su verificación.
- Recuerde que otros tipos de tecnologías de acceso WAN existen, analice para qué emplearía cada una.
- Ejercite todas las configuraciones en dispositivos reales o en simuladores.
