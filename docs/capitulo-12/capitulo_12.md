# Administración y gestión

## SNMP

SNMP (*Simple Network Management Protocol*) fue desarrollado para administrar nodos, servidores, estaciones de trabajo, routers, switches y dispositivos de seguridad, en una red IP. SNMP es un protocolo de capa de aplicación que facilita el intercambio de información de administración entre dispositivos de red. SNMP es parte de la suite del protocolo TCP/IP.

SNMPv3 es un protocolo interoperable basado en estándares para administración de redes. La versión actual de SNMPv3 resuelve las vulnerabilidades de las versiones anteriores, incluyendo tres nuevas características de seguridad.

- **Integridad del mensaje:** asegura que el paquete no ha sido manipulado en su tránsito por la red.
- **Autenticación:** determina que el mensaje proviene de un origen válido.
- **Cifrado:** encripta los contenidos de un paquete para evitar que pueda ser visualizado por una fuente no autorizada.

SNMP está basado en administradores NMS (*Network Management Systems*), agentes que son los nodos administrados, y las MIB (*Management Information Bases*) que son las bases de información de administración. El administrador SNMP puede obtener y cambiar información del agente y cambiar variables de configuración o iniciar acciones determinadas en los dispositivos.

Los agentes SNMP aceptan comandos y solicitudes de los sistemas de administración SNMP solo si estos forman parte de una comunidad SNMP (*community string*):

- **RO:** proporcionan acceso de solo lectura.
- **RW:** proporcionan acceso de lectura-escritura.

Por defecto, la mayoría de los sistemas SNMP utiliza `public` como *community string*, por lo tanto, cualquiera que tenga un sistema SNMP podrá leer la MIB del router.

Para configurar la comunidad SNMP por CLI se utiliza el siguiente comando:

```text
Router(config)# snmp-server community nombre [ro | rw]
```

### Configuración

La configuración de SNMPv3 es un poco más complicado que las versiones 1 o 2C, debido principalmente a las características de seguridad adicionales. Estos son los pasos para configurar SNMPv3 en un dispositivo:

1. Se pueden limitar los hosts que pueden acceder al switch a través de SNMP mediante la definición de una ACL nombrada o numerada. Las direcciones permitidas obtendrán acceso SNMPv3.

    ```text
    Router(config)# ip access-list standard acl-name
    Router(config-std-nacl)# permit source_net
    Router(config)# access-list access-list-number permit ip-addr
    ```

2. Se puede utilizar el comando `snmp-server view` para definir una vista específica para los usuarios. Si no se configura ninguna vista, todas las variables MIB son visibles para los usuarios.

    ```text
    Switch(config)# snmp-server view view-name oid-tree {included | excluded}
    ```

3. Se utiliza el comando `snmp-server group` para configurar un nombre de grupo que establecerá el nivel de seguridad de las políticas para usuarios SNMPv3 que están asignados al grupo. El nivel de seguridad se define con las siguientes opciones:

    - `noauth`: sin autenticación o cifrado de paquetes.
    - `auth`: autenticación de paquetes, pero no cifrado.
    - `priv`: paquetes autenticados y cifrados.

    Solo la política de seguridad se define en el grupo; todavía no se requieren contraseñas ni llaves.

    Si se ha configurado una vista, se pueden usar las opciones `read`, `write` y `notify` para limitar el acceso a operaciones de lectura, escritura o notificación. Si se ha configurado una ACL, se puede aplicar al grupo con la opción `access`.

    ```text
    Router(config)# snmp-server group group-name v3 { noauth | auth | priv }
        [ read read-view ] [ write write-view ] [ notify notify-view ]
        [ access accesslist]
    ```

4. Se define un nombre de usuario para ser usado por el SNMP manager para comunicarse con el dispositivo. Se utiliza el comando `snmp-server user` para definir el nombre y asociarlo con el grupo SNMPv3. La opción `v3` configura el usuario para utilizar SNMPv3.

    El usuario SNMPv3 también debe tener algunos detalles añadidos a su política de seguridad. La opción `auth` permite definir autenticación de tipo MD5 o SHA. La opción `priv` define el método de cifrado.

    ```text
    Router(config)# snmp-server user user-name group-name v3
        auth {md5 | sha} auth-password priv { des | 3des | aes { 128 | 192 | 256 } }
        priv-password [ access-list-number ]
    ```

    El mismo nombre de usuario SNMPv3, método de autenticación y contraseña, y método de cifrado y la contraseña, deben ser definidos en el SNMP manager para que se pueda comunicar con el router o switch.

5. Se puede utilizar el comando `snmp-server host` para identificar el SNMP manager que recibirá las *traps* o los *informs*. El dispositivo puede utilizar SNMPv3 para enviar *traps* o *informs*, utilizando los parámetros de seguridad que se definen en el nombre de usuario SNMPv3:

    ```text
    Router(config)# snmp-server host host-address [ informs ]
        version 3 { noauth | auth | priv } username [ trap-type ]
    ```

En el siguiente ejemplo un router está configurado con SNMPv3. La ACL 10 permite acceso SNMP únicamente a las estaciones de gestión 192.168.3.99 y 192.168.100.4. El acceso SNMPv3 está definido para un grupo llamado gsnmp utilizando el nivel de seguridad priv, es decir autenticación y cifrado. Se crea un usuario SNMPv3 llamado monitor; la estación gestión de red usará ese nombre de usuario cuando proceda a sondear el dispositivo para obtener información. El nombre de usuario requerirá autenticación de paquetes SHA y cifrado AES-128, usando las contraseñas ccnp3rote5 y tsh5ccnp2, respectivamente.

Por último, los mensajes *inform* SNMPv3 serán utilizados para enviar alertas a la estación de gestión 192.168.3.99 usando el nivel de seguridad priv y el usuario monitor.

```text
Router(config)# access-list 10 permit 192.168.3.99
Router(config)# access-list 10 permit 192.168.100.4
Router(config)# snmp-server group gsnmp v3 priv
Router(config)# snmp-server user monitor gsnmp v3 auth sha ccnp3rote5 priv aes 128 tsh5ccnp2
Router(config)# snmp-server host 192.168.3.99 informs version 3 priv monitor
```

#### Verificación

El comando `show snmp group` se utiliza para mostrar información acerca de cada grupo SNMP en la red.

```text
Router# show snmp group
groupname: V1 security model:v1
readview : v1default writeview: <no writeview specified>
notifyview: <no notifyview specified>
row status: active

groupname: ILMI security model:v1
readview : *ilmi writeview: *ilmi
notifyview: <no notifyview specified>
row status: active

groupname: ILMI security model:v2c
readview : *ilmi writeview: *ilmi
notifyview: <no notifyview specified>
row status: active

groupname: group1 security model:v1
readview : v1default writeview: <no writeview specified>
notifyview: <no notifyview specified>
row status: active
```

El comando `show snmp community` muestra las comunidades configuradas para permitir el acceso SNMP.

```text
Router# show snmp community
Community name: ILMI
Community Index: ILMI
Community SecurityName: ILMI
storage-type: read-only active

Community name: private
Community Index: private
Community SecurityName: private
storage-type: nonvolatile active

Community name: private@1
Community Index: private@1
Community SecurityName: private
storage-type: read-only active

Community name: public
Community Index: public
Community SecurityName: public
storage-type: nonvolatile active
```

El comando `show snmp user` se utiliza para mostrar información sobre los usuarios configurados para SNMP. Cuando no se especifica un nombre de usuario el comando muestra a todos los usuarios configurados.

```text
Router# show snmp user authuser
User name: authuser
Engine ID: 00000009020000000C025808
storage-type: nonvolatile       active access-list: 10
Rowstatus: active
Authentication Protocol: MD5
Privacy protocol: DES
Group name: VacmGroupName
```

## SYSLOG

Los routers Cisco pueden registrar información en relación a los cambios de configuración, violaciones de las ACL, el estado de las interfaces y muchos otros tipos de eventos. Además, pueden enviar mensajes de registro a muchos destinos diferentes. El router puede estar configurado para enviar mensajes de registro a uno o más de los siguientes destinos:

- **Consola:** los mensajes se registran en la consola y pueden ser visualizados cuando se modifica o se prueba el router usando software de emulación de terminal. El registro de consola está habilitado por defecto. Este tipo de registro no se almacena en el router.
- **Líneas de terminal:** las sesiones pueden ser configuradas para recibir mensajes de registro en cualquiera de las líneas de terminal. Este tipo de registro no se almacena en el router.
- **Registro de buffer:** el registro de buffer es un poco más útil como herramienta de seguridad porque los mensajes quedan almacenados en la memoria del router por un cierto tiempo.
- **SNMP traps:** los eventos de los routers, como la superación de un umbral, pueden ser procesados por el router y reenviados como traps SNMP a un servidor SNMP externo. Las traps SNMP son una herramienta de registro de seguridad viable, pero requieren la configuración y mantenimiento de un sistema SNMP.
- **Syslog:** los routers Cisco pueden ser configurados para reenviar mensajes de registro a un servicio syslog externo. Este servicio puede residir en uno o muchos servidores o estaciones de trabajo.

Syslog es el estándar para registrar eventos del sistema. Syslog es la herramienta de registro de mensajes más popular, ya que proporciona capacidades de almacenamiento de registro de largo plazo y una ubicación central para todos los mensajes del router.

Las implementaciones syslog contienen dos tipos de sistemas:

- **Servidores syslog:** también conocidos como hosts de registro, estos sistemas aceptan y procesan mensajes de registro de clientes syslog.
- **Clientes syslog:** routers u otros tipos de dispositivos que generan y reenvían mensajes de registro a servidores syslog.

| Nivel | Aviso | Descripción | Definición |
| --- | --- | --- | --- |
| 0 | emergencies | El sistema es inoperable. | LOG_EMERG |
| 1 | alerts | Se requiere una acción inmediata. | LOG_ALERT |
| 2 | critical | Existen condiciones críticas. | LOG_CRIT |
| 3 | errors | Existen condiciones de error. | LOG_ERR |
| 4 | warnings | Existen condiciones de advertencia. | LOG_WARNING |
| 5 | notification | Notificaciones significativas. | LOG_NOTICE |
| 6 | informational | Mensajes informativos. | LOG_INFO |
| 7 | debugging | Mensajes de depuración. | LOG_DEBUG |

### Configuración de logging

Los siguientes pasos configuran el registro del sistema:

1. Configuración del host de registro de destino utilizando el comando `logging host`.
2. Establecer el nivel de severidad del trap con el comando `logging trap level` (este paso es opcional).
3. Configurar la interfaz de origen con el comando `logging source-interface`. Esto especifica que los paquetes syslog contengan la dirección IPv4 o IPv6 de una interfaz particular, sin importar qué interfaz usa el paquete para salir del router.
4. Habilitar el registro utilizando el comando `logging on`. Puede habilitar o deshabilitar el registro para estos destinos individualmente usando los comandos `logging buffered`, `logging monitor` y `logging` de configuración global. Sin embargo, si el comando `logging on` está deshabilitado, no se envían mensajes a estos destinos. Solo la consola recibe mensajes.

```text
Router(config)# logging host 192.168.1.23
Router(config)# logging trap critical
Router(config)# logging source-interface fastethernet0/2
Router(config)# logging on
```

Los mensajes emergentes de logging aparecen a medida que los eventos ocurren, también es posible visualizarlos con el comando `show logging`. Los mensajes llevan implícitos los datos correspondientes a la fecha, nivel de severidad y un mensaje de texto que indica detalles del mensaje.

```text
00:00:46:%LINK-3-UPDOWN:Interface Port-channel1, changed state to up
00:00:47:%LINK-3-UPDOWN:Interface Ethernet0/1, changed state to up
00:00:47:%LINK-3-UPDOWN:Interface Ethernet0/2, changed state to up
```

```text
Router> show logging
Syslog logging:enabled (2 messages dropped, 0 flushes, 0 overruns)
Console logging:disabled
Monitor logging:level debugging, 0 messages logged
Buffer logging:level debugging, 4104 messages logged
Trap logging:level debugging, 4119 message lines logged
Logging to 216.231.111.14, 4119 message lines logged
Log Buffer (262144 bytes):
Jul 11 12:17:49 EDT:%BGP-4-MAXPFX:No. of prefix received from 209.165.200.225 (afi 0)
reaches 24, max 24
! THE FOLLOWING LINE IS A DEBUG MESSAGE FROM NTP.
! NOTE THAT IT IS NOT PRECEEDED BY THE % SYMBOL.
Jul 11 12:17:48 EDT: NTP: Maxslew = 213866
Jul 11 15:15:41 EDT:%SYS-5-CONFIG:Configured from tftp://host.com/addc5505-rsm.nyiix
.Jul 11 15:30:28 EDT:%BGP-5-ADJCHANGE:neighbor 209.165.200.226 Up
.Jul 11 15:31:34 EDT:%BGP-3-MAXPFXEXCEED:No. of prefix received from
209.165.200.226 (afi 0):16444 exceed limit 375
.Jul 11 15:31:34 EDT:%BGP-5-ADJCHANGE:neighbor 209.165.200.226 Down BGP
Notification sent
.Jul 11 15:31:34 EDT:%BGP-3-NOTIFICATION:sent to neighbor 209.165.200.226 3/1 (update
malformed) 0 bytes
```

## NOMBRE DEL CISCO IOS

A partir de la versión IOS 12.3 (*Internetwork Operating System*) Cisco ha puesto en funcionamiento un nuevo método de categorización y nomenclatura para las imágenes IOS denominado "IOS Packaging".

Anteriormente era necesario diferenciar las imágenes IOS para las distintas familias de routers debido a las incompatibilidades de hardware. El objetivo principal es reducir la cantidad y variedad de versiones de IOS disponibles para cada dispositivo a solamente 8.

- **IP Base:** licencia básica por defecto.
- **IP Voice:** añade al IP Base Telefonía IP, VoIP, VoFR.
- **SP Services:** añade al IP Voice NetFlow, SSH, ATM, VoATM, MPLS.
- **Advanced Security:** añade al IP Base Cisco IOS FW, IDS, SSH, IPsec VPN, 3DES.
- **Enterprise Base:** añade al IP Base soporte multi-protocolo y soporte IBM.
- **Enterprise Services:** añade a Enterprise Base soporte completo IBM, Service Provider Services.
- **Advanced IP Services:** añade a SP Services IPv6, Seguridad avanzada.
- **Advanced Enterprise Services:** versión completa del Cisco IOS Software.

Cisco presentaba importantes revisiones de imágenes del IOS para cada nueva versión de software llamándolas "versions" y utilizaba los cambios menores con las llamadas "release". Sin embargo, Cisco no había utilizado hasta ahora un modelo en el que se instala el IOS como un archivo y, a continuación, añadir correcciones de errores como un archivo separado. Esta nueva modalidad de presentación llamada "universal image" reemplaza el antiguo método de imágenes por paquetes.

Para los routers ISR G2 (*Integrated Service Routers Generation 2*), el software Cisco IOS se entrega con una única imagen universal del software Cisco IOS por plataforma para cada versión. En el pasado, había disponibles 44 imágenes diferentes del software Cisco IOS, según cada plataforma y cada versión, con el fin de cubrir todas las combinaciones de conjuntos de funciones del software. El usuario debía asegurarse de comprar la licencia de funciones correcta para cada dispositivo de la red y dedicar bastante tiempo a verificar que estaba utilizando la imagen correcta en cada plataforma. Con la imagen universal solo se debe seleccionar la versión de software Cisco IOS que se necesita para la propia red.

La característica principal de esta nueva nomenclatura es que para una misma versión de IOS y para idéntico hardware hay una única imagen del sistema operativo que contiene todas las características disponibles.

Sin embargo el acceso a todas estas características está limitado por un sistema de licencias que comprenden cuatro modalidades básicas.

- **IP Base.** Es la licencia por defecto que viene con todos los dispositivos, incorpora BGP, OSPF, EIGRP, ISIS.
- **Security.** Firewall IOS, IPS, IPSec, 3DES, VPN.
- **Unified Communications.** VoIP, telefonía IP.
- **Data.** MPLS, ATM, soporte multiprotocolo.

Existen licencias específicas como: SNAsw, SSL VPN, IOS IPS y Gatekeeper que dependen de un paquete de Tecnología concreto y solamente pueden ser activados si éste se encuentra instalado y activo previamente.

Con estas nuevas peculiaridades no será necesario comprar un nuevo dispositivo que cumpla ciertos requisitos, bastará con ampliar las funcionalidades de la IOS habilitando la licencia correspondiente.

### Activación y licencias del IOS

La imagen de IOS 15 es una única imagen universal que solo está limitada por licencia. En consecuencia, no es necesario descargar una nueva imagen de sistema operativo sino activar las características correspondientes actualizando la clave de actualización que habilita la licencia correspondiente.

Las licencias pueden ser:

- **Permanente:** una licencia permanente no tiene vencimiento. Cuando se instala una licencia permanente en un sistema, dicha licencia es válida para ese conjunto de funciones en particular durante toda la vida útil del router.
- **Temporal:** también llamada licencia de prueba, es válida durante un período limitado. Todos los nuevos routers ISR incluyen un juego completo de licencias temporales por 60 días para los conjuntos de funciones de datos, de comunicaciones unificadas y de seguridad.
- **Por cantidad:** hace referencia al recuento de utilidades determinadas que pueden sumar varias o múltiples licencias.
- **Suscripción:** permite acceder a una función o capacidad por un período limitado, a menos que se renueve la suscripción. Las licencias por suscripción generalmente están relacionadas con actualizaciones periódicas del servicio de un tercero.

Con la presentación de los nuevos routers, Cisco está cambiando la manera en que se disponen los paquetes del software Cisco IOS. Con anterioridad, cada plataforma y versión incluía entre 7 y 11 imágenes diferentes, con diversas funciones y capacidades en cada imagen. Cisco Software Activation crea un método mucho más práctico para los nuevos routers, todas las funciones están incluidas en una única imagen universal de Cisco IOS. Las funciones superiores respecto de las incluidas en el paquete predeterminado IP Base generalmente se agrupan en tres paquetes principales de tecnología: datos, seguridad y comunicaciones unificadas. Estos tres paquetes representan la amplia mayoría de funciones disponibles en el software Cisco IOS.

Además de los tres paquetes principales de tecnología, existen licencias de funciones adicionales para funciones superiores que requieren servicios de suscripción o solicitud de cantidades.

Cisco Software Activation es el mecanismo que se utiliza para activar las funciones y componentes del software de los routers ISR de segunda generación. Genera una clave de licencia única para un conjunto de funciones de un dispositivo específico y activa ese conjunto de funciones en el router.

El primer paso es obtener el código de activación PAK (*Product Activation Key*) para cada licencia. El PAK se proporciona al comprar o adquirir el derecho de uso de un conjunto de características para una plataforma en particular.

Obtener el número del identificador UDI (*Unique Device Identifier*), con el comando `show license udi`. Este comando muestra además el ID del producto y el número de serie.

```text
Router#show license udi
Device#   PID                SN              UDI
-------------------------------------------------------------
*0      CISCO2911/K9   FTX152410Y6   CISCO2911/K9:FTX152410Y6
```

Para obtener la licencia apropiada, ingrese los datos UDI obtenidos con el comando `show license udi` y el código de activación PAK en el portal de Registros de Productos de Cisco en `http://www.cisco.com/go/license`.

!!! note "NOTA"

    La Licencia IP Base es un prerrequisito para la instalación de las demás licencias.

## IP SLA

Cisco IOS IP SLA (*IP Service Level Agreement*) permite medir el rendimiento y disponibilidad de la red generando tráfico simulado de manera continua y fiable de forma predecible. Los datos que se pueden obtener varían mucho en función de cómo se configura. Se puede obtener información acerca de la pérdida de paquetes, latencia en un solo sentido, tiempos de respuesta, jitter, disponibilidad de los recursos de red, rendimiento de aplicaciones, tiempos de respuesta del servidor, e incluso calidad de voz.

Es posible realizar múltiples operaciones con ellas, entre las que se encuentran:

- ICMP (echo, jitter).
- RTP (VoIP).
- TCP (establishes TCP connections).
- UDP (echo, jitter).
- DNS.
- DHCP.
- HTTP.
- FTP.

IP SLA consiste en un origen que envía las sondas y un destino, el que responde, conocido como *responder* que envía respuestas a las sondas, aunque no siempre son necesarios ambos. Solo la fuente IP SLA, es decir el origen, es siempre necesario. El *responder* es necesario únicamente cuando se necesitan recopilar estadísticas de alta precisión para servicios que no son ofrecidas por cualquier dispositivo de red destino. El *responder* tiene la capacidad de responder a la fuente con mediciones precisas tomando en cuenta su propio tiempo de procesamiento de la sonda.

### Configuración

Para comprender el funcionamiento de las SLAs se tomará como ejemplo la operación ICMP, los pasos a seguir para su configuración serán:

1. Creación de la operación IP SLA y la asignación del número correspondiente, con el comando:

    ```text
    ip sla sla-ops-number
    ```

2. Definir el tipo de operación y los parámetros. Para este caso, ICMP *echo*, se utiliza IP o nombre destino y opcionalmente el de origen. Se utiliza el subcomando:

    ```text
    icmp-echo {destination-ipaddress | destination-hostname}
        [source-ip {ip-address | hostname} | source-interface interface-name]
    ```

3. De manera opcional se determina la frecuencia con la que se debe ejecutar la operación. Se utiliza el subcomando:

    ```text
    frequency seconds
    ```

4. Definir cuando ha de ejecutarse la operación con el comando:

    ```text
    ip sla schedule sla-ops-number [life {forever | seconds}]
        [start-time {hh:mm[:ss] [month day | day month] | pending | now | after hh:mm:ss}]
        [ageout seconds] [recurring]
    ```

#### Verificación

Para verificar que las operaciones están soportadas en la plataforma, además de la cantidad de operaciones configuradas y cuantas están actualmente activas, se utiliza el comando `show ip sla application`.

```text
R1# show ip sla application
IP Service Level Agreements
Version: Round Trip Time MIB 2.2.0, Infrastructure Engine-III
Supported Operation Types:
  icmpEcho, path-echo, path-jitter, udpEcho, tcpConnect, http
  dns, udpJitter, dhcp, ftp, lsp Group, lspPing, lspTrace
  802.1agEcho VLAN, EVC, Port, 802.1agJitter VLAN, EVC, Port
  pseudowirePing, udpApp, wspApp
Supported Features:
  IPSLAs Event Publisher
IP SLAs low memory water mark: 30919230
Estimated system max number of entries: 22645
Estimated number of configurable operations: 22643
Number of Entries configured : 2
Number of active Entries : 2
Number of pending Entries : 0
Number of inactive Entries : 0
Time of last change in whole IP SLAs: 09:29:04.789 UTC Sat Jul 26 2014
```

Para verificar los valores de configuración para cada instancia IP SLA, así como los valores por defecto que no se han modificado se utiliza el comando `show ip sla configuration`.

```text
R1# show ip sla configuration
IP SLAs Infrastructure Engine-III
Entry number: 1
Owner:
Tag:
Operation timeout (milliseconds): 5000
Type of operation to perform: udp-jitter
Target address/Source address: 10.1.34.4/192.168.1.11
Target port/Source port: 65051/0
Type Of Service parameter: 0x0
Request size (ARR data portion): 160
Packet Interval (milliseconds)/Number of packets: 20/20
Verify data: No
Vrf Name:
Control Packets: enabled
Schedule:
Operation frequency (seconds): 30 (not considered if randomly scheduled)
Next Scheduled Start Time: Start Time already passed
Group Scheduled : FALSE
Randomly Scheduled : FALSE
Life (seconds): Forever
Entry Ageout (seconds): never
Recurring (Starting Everyday): FALSE
Status of entry (SNMP RowStatus): Active
Threshold (milliseconds): 5000
Distribution Statistics:
Number of statistic hours kept: 2
Number of statistic distribution buckets kept: 1
Statistic distribution interval (milliseconds): 20
Enhanced History:
```

Los siguientes son comandos adicionales para la resolución de problemas en Cisco IOS IP SLA.

- `show ip sla statistics`, muestra los resultados de las operaciones de IP SLA y las estadísticas recogidas.
- `show ip sla responder`, se utiliza para verificar el funcionamiento del IP SLA responder.
- `debug ip sla`, muestra la salida en tiempo real de una operación SLA.

## SPAN

En algunos entornos es necesario utilizar ordenadores o dispositivos específicos en la red para capturar flujos de tráfico y examinar los paquetes. De esta manera se sondea dentro de las cabeceras de capa 2, 3 y 4 para ver como dichos paquetes son tratados en la red.

Si hay uno varios switches entre los segmentos los dominios de colisión se separarán y no se enviarán las tramas en cuestión al puerto donde se encuentre conectado el analizador de tráfico.

Para resolver este problema del análisis de tráfico entre switches Cisco incorpora una funcionalidad llamada SPAN (*Switched Port Analyzer*), cuyo funcionamiento básico es copiar todas las tramas que pasan por un puerto determinado a otro donde estará conectado el capturador de paquetes.

La siguiente sintaxis muestra un ejemplo de configuración:

```text
Switch# conf term
Enter configuration commands, one per line. End with CNTL/Z.
Cat3550(config)# monitor session 1 source interface gig 0/1
Cat3550(config)# monitor session 1 destination interface gig 0/3
Cat3550(config)# end
Switch# show monitor
Session 1
------------
Type : Local Session
Source Ports :
Both : Gi0/1
Destination Ports : Gi0/3
Encapsulation : Native
Ingress : Disabled
```

En entornos de grandes redes puede darse el caso de que un dispositivo de captura de paquetes esté conectado a un switch y sea necesario capturar paquetes desde otros switches. Para estos casos existe la herramienta RSPAN (*Remote SPAN*). El funcionamiento se basa en una VLAN especial que se encarga de transportar ese tráfico entre los switches.

El siguiente es un ejemplo que muestra un diagrama de red y la configuración asociada en cada switch:

```text
Switch_1# conf term
Switch_1(config)# vlan 10
Switch_1(config-vlan)# name CCNA_SPAN
Switch_1(config-vlan)# remote-span
Switch_1(config-vlan)# exit
Switch_1(config)# monitor session 1 source interface gig 0/1
Switch_1(config)# monitor session 1 destination remote vlan 10 reflector-port gig 0/3
Switch_1(config)# end
Switch_1#show monitor
Session 1
------------
Type : Remote Source Session
Source Ports :
Both : Gi0/1
Reflector Port : Gi0/3
Dest RSPAN VLAN : 20
```

```text
Switch_2# conf term
Switch_2(config)# vlan 10
Switch_2(config-vlan)# name CCNA_SPAN
Switch_2(config-vlan)# remote-span
Switch_2(config-vlan)# exit
Switch_2(config)# monitor session 2 source remote vlan 10
Switch_2(config)# monitor session 2 destination interface fa 5/2
Switch_2(config)# end
Switch_2# show monitor
Session 2
------------
Type : Remote Destination Session
Source RSPAN VLAN : 20
Destination Ports : Fa5/2
```

## SERVICIOS EN LA NUBE

Los llamados servicios en la nube o Cloud services son servidores en Internet soportados por empresas privadas encargados de atender las peticiones y requerimientos de los usuarios en cualquier momento. Se puede tener acceso a su información o servicio, mediante una conexión a internet desde cualquier dispositivo móvil o fijo ubicado en cualquier lugar. Sirven a sus usuarios desde varios proveedores de alojamiento repartidos frecuentemente por todo el mundo. Esta medida reduce los costes, garantiza un mejor tiempo de actividad y que los sitios web estén debidamente protegidos.

A diferencia de un Data Center donde los datos son administrados por un departamento específico de la empresa y alojados dentro de la propia empresa o fuera en instalaciones arrendadas, los servicios en la nube ofrecen acceso bajo demanda a un conjunto compartido de recursos informáticos configurables. Estos recursos se pueden aprovisionar rápidamente y liberados con mínimo esfuerzo de gestión.

Los servicios en la nube están disponibles en una variedad de opciones, adaptadas a las necesidades del cliente. Los tres principales servicios en la nube definidos por el Instituto Nacional de Estándares y Tecnología (NIST) son las siguientes:

- **Software como servicio, SaaS (Software as a Service).** El proveedor de la nube es responsable de acceso a los servicios, como el correo electrónico, la comunicación y la Oficina 365 que se entregan a través de Internet. Los usuarios solo tienen que proporcionar sus datos. Las aplicaciones que suministran este modelo de servicio son accesibles a través de un navegador web o de cualquier aplicación diseñada para tal efecto y el usuario no tiene control sobre ellas, aunque en algunos casos se le permite realizar algunas configuraciones. Esto elimina la necesidad al cliente de instalar aplicaciones en sus propios ordenadores, evitando asumir los costos de soporte y el mantenimiento de hardware y software.
- **Plataforma como servicio, PaaS (Platform as a Service).** El proveedor de la nube es responsable del acceso a las herramientas y servicios de desarrollo utilizados para entregar las aplicaciones. Las ofertas de PaaS pueden dar servicio a todas las fases del ciclo de desarrollo y pruebas del software, o pueden estar especializadas en cualquier área en particular, tal como la administración del contenido. En este modelo de servicio se le ofrece al usuario la plataforma de desarrollo y las herramientas de programación por lo que puede desarrollar aplicaciones propias y controlar la aplicación, pero no controla la infraestructura.
- **Infraestructura como servicio, IaaS (Infrastructure as a Service).** El proveedor de la nube es responsable del acceso a los equipos de red, servicios de red virtualizados y el apoyo a la infraestructura de red. Es un medio de entregar almacenamiento básico y capacidades de cómputo como servicios estandarizados en la red. Servidores, sistemas de almacenamiento, conexiones, enrutadores, y otros sistemas se concentran (por ejemplo, a través de la tecnología de virtualización) para manejar tipos específicos de cargas de trabajo.

### Modelos de nubes

Existen cuatro modelos de nubes:

- **Nubes públicas:** las aplicaciones basadas en la nube y los servicios ofrecidos en una nube pública se ponen a disposición de la población en general. Los servicios pueden ser libres o en un modelo de pago por uso.
- **Nubes privadas:** las aplicaciones basadas en la nube y los servicios ofrecidos en una nube privada se destinan a una organización o entidad específica, como por ejemplo el gobierno. También puede ser administrado por una organización externa con la seguridad de acceso estricto.
- **Nubes híbridas:** este modelo se compone de dos o más nubes (parte privada y parte pública por ejemplo), donde cada parte sigue siendo un objeto distintivo. Ambos están conectados mediante una única arquitectura.
- **Nubes personalizadas:** son nubes construidas para satisfacer las necesidades de una industria específica, como la salud o multimedia. Las nubes personalizadas pueden ser privadas o públicas.

## VIRTUALIZACIÓN

Los servicios en la nube y la virtualización se utilizan generalmente como sinónimos sin embargo, significan cosas diferentes. Mientras que los servicios en la nube separan la aplicación del hardware, la virtualización separa el sistema operativo (OS) del hardware.

La virtualización es el fundamento del funcionamiento en la nube. Varios proveedores ofrecen servicios en la nube virtual que puede aprovisionar servidores dinámicamente según sea necesario. Un servidor físico, Host, tiene un alto poder de procesamiento. Un Host puede almacenar varias máquinas virtuales VM (*Virtual Machine*).

Históricamente, los servidores de la empresa consistían en un sistema operativo de servidor como Windows Server o Servidor Linux, instalado en un hardware específico. El principal problema de esta configuración es que cuando un componente falla, el servicio que es proporcionado por este servidor no está disponible. Esto es un único punto de fallo. La virtualización de servidores aprovecha los recursos ociosos y consolida el número de servidores necesarios. Permite a múltiples sistemas operativos coexistir en una única plataforma de hardware.

Una de las principales ventajas de la virtualización es que se reduce el costo general:

- Se requiere menos equipo.
- Se consume menos energía.
- Se requiere menos espacio.

Estos son beneficios adicionales de virtualización:

- Creación de prototipos más simple.
- Suministro de servidores más rápido.
- Máximo aprovechamiento de la actividad del servidor.
- Rápida recuperación ante desastres.
- Compatibilidad con sistemas existentes.

### Hypervisor

Un hypervisor es un software que crea y ejecuta instancias de máquina virtual. Funciona entre el firmware y el sistema operativo. El hypervisor puede soportar múltiples instancias de sistemas operativos. Para que la virtualización del servidor funcione, cada servidor físico debe utilizar un hipervisor.

El hipervisor gestiona y asigna el hardware del Host (servidor) como la CPU, RAM, etc. a cada VM en función de su configuración. Cada VM se ejecuta como si se ejecutara en un servidor físico autónomo, con un número específico de CPU y NIC virtuales y una cantidad establecida de RAM y almacenamiento.

Un hypervisor de tipo 2 está instalado en los sistemas operativos existentes, como Mac OS X, Windows o Linux. El equipo en el que un hypervisor está apoyando una o más máquinas virtuales es una máquina host.

Un hypervisor de tipo 1 se instala directamente en el servidor o hardware de red, por lo tanto, tiene acceso directo a los recursos de hardware. Requiere una consola de administración para gestionarlo. Se utiliza un software de gestión para gestionar múltiples servidores que utilizan el mismo hypervisor.

Algunos ejemplos de hypervisor pueden ser:

- VMware.
- Oracle VM VirtualBox.
- Red Hat KVM.
- Mac OS X Parallels.
- Citrix XenServer.
- Microsoft Hyper-V.

La virtualización de servidores oculta los recursos del servidor. Esta práctica puede crear problemas si el centro de datos utiliza arquitecturas de red tradicionales. Por ejemplo, las VLANs utilizadas por las máquinas virtuales deben ser asignadas al mismo puerto del switch como el servidor físico que ejecuta el hypervisor. Otro problema es que los flujos de tráfico difieren sustancialmente del modelo tradicional de cliente-servidor. Estos flujos cambian de ubicación e intensidad con el tiempo, lo que requiere un enfoque flexible para la gestión de recursos de red. Las infraestructuras de red existentes pueden responder a las necesidades cambiantes relacionadas con la gestión de los flujos de tráfico mediante el uso de QoS (*Quality of Service*).

#### Virtualización de la red

Las dos principales arquitecturas de red desarrolladas para soportar la virtualización de la red son las siguientes:

- **SDN (Software Defined Networking)** una arquitectura de red que permite virtualizar la red.
- **ACI (Cisco Application Centric Infrastructure)** una solución de hardware especialmente diseñado para integrar los procesos en nube y la gestión del centro de datos.

Las siguientes son otras tecnologías de virtualización de red, algunos de los cuales están incluidos como componentes en SDN y ACI:

- **OpenFlow**, desarrollado en la Universidad de Stanford para gestionar el tráfico entre los routers, switches, puntos de acceso inalámbrico y un controlador.
- **OpenStack**, utilizado comúnmente por Cisco ACI. Es el proceso de automatizar el aprovisionamiento de componentes de red.

## CASO PRÁCTICO

### Activación de licencia

Requisitos previos para obtener una licencia son los siguientes:

- Obtener el PAK necesario, es un identificador de 11 dígitos que se puede entregar por correo o electrónicamente.
- Poseer nombre de usuario y contraseña válido en Cisco.
- Obtener los datos del número de serie, el PID y el UDI con el comando `show license udi` o del código de barras de la etiqueta del router.

```text
Router#show license udi
Device#   PID                SN              UDI
-------------------------------------------------------------
*0      C3900-SPE100/K9   FHH13030044  C3900-SPE100/K9:FHH13030044
Router#
```

El comando `show license feature` muestra un listado resumido de las licencias habilitadas en el router.

```text
Router#show license feature
Feature name         Enforcement   Evaluation   Subscription   Enabled   RightToUse
ipbasek9                       no           no             no       yes            no
securityk9                    yes          yes             no        no           yes
uck9                          yes          yes             no        no           yes
datak9                        yes          yes             no        no           yes
gatekeeper
SSL_VPN
ios-ips-update
SNASw
hseck9
.......
```

El comando `show license detail` muestra un listado más completo de las licencias habilitadas en el router.

```text
Router#show license detail
Index 1 Feature: ipbasek9
    Period left: Life time
    License Type: Permanent
    License State: Active, In Use
    License Count: Non-Counted
    License Priority: Medium

Index 2 Feature: securityk9
    Period left: Not Activated
    Period Used: 0 minute 0 second
    License Type: Evaluation
    License State: Not in Use, EULA not accepted
    License Count: Non-Counted
    License Priority: None

Index 3 Feature: uck9
    Period left: Not Activated
    Period Used: 0 minute 0 second
    License Type: Evaluation
    License State: Not in Use, EULA not accepted
    License Count: Non-Counted
    License Priority: None

Index 4 Feature: datak9
    Period left: Not Activated
    Period Used: 0 minute 0 second
    License Type: Evaluation
    License State: Not in Use, EULA not accepted
    License Count: Non-Counted
    License Priority: None

Index 5 Feature: gatekeeper
    Period left: Not Activated
    Period Used: 0 minute 0 second
    License Type: Evaluation
    License State: Not in Use, EULA not accepted
    License Count: Non-Counted
    License Priority: None

Index 6......
```

Desde el portal de activación de licencias de Cisco se pueden obtener licencias de los productos y realizar otras operaciones relacionadas con las licencias, `http://www.cisco.com/go/license`.

1. Tenga disponibles el PAK y el UDI.
2. Inicie sesión en el portal de licencias de Cisco con nombre de usuario y contraseña.
3. Escriba y verifique la información necesaria y presentar el registro de la licencia.
4. La generación del registro y licencia se ha completado. Descargue la licencia o bien desde el sitio web haciendo clic en el botón "Descargar Licencia" o desde el archivo adjunto del correo electrónico enviado desde Cisco.
5. Copie la licencia en la memoria flash, en este caso desde un servidor TFTP de la red.

    ```text
    Router#copy tftp flash0:
    Address or name of remote host []? 192.168.1.3
    Source filename []?
    /tftpboot/lmxiang/FHH1216P07R_20090528163510702.lic
    Destination filename [FHH1216P07R_20090528163510702.lic]?
    Accessing
    tftp://192.168.1.3//tftpboot/lmxiang/FHH1216P07R_20090528163510702.lic...
    Loading /tftpboot/lmxiang/FHH1216P07R_20090528163510702.lic from 192.168.1.3
    (via GigabitEthernet0/0): !
    [OK - 1149 bytes]
    1149 bytes copied in 0.548 secs (2097 bytes/sec)
    ```

6. Instale la licencia con el comando `license install`, en este caso desde la memoria flash.

    ```text
    Router#license install flash0:FHH1216P07R_20090528163510702.lic
    Installing licenses from "flash0:FHH1216P07R_20090528163510702.lic"
    Installing...Feature:securityk9...Successful:Supported
    1/1 licenses were successfully installed
    0/1 licenses were existing licenses
    0/1 licenses were failed to install
    Router#
    *May 28 16:27:28.861 PDT: %LICENSE-6-INSTALL: Feature securityk9 1.0
    was installed in this device. UDI=CISCO2951:FHH1216P07R; StoreIndex=2:Primary
    License Storage
    ```

7. Verifique el estado de la licencia.

    ```text
    Router#show license detail
    Index 1 Feature: ipbasek9
        Period left: Life time
        License Type: Permanent
        License State: Active, In Use
        License Count: Non-Counted
        License Priority: Medium

    Index 2 Feature: securityk9
        Period left: Life time
        License Type: Permanent
        License State: Active, In Use
        License Count: Non-Counted
        License Priority: Medium

    Index 3 Feature: uck9
        Period left: Not Activated
        Period Used: 0 minute 0 second
        License Type: Evaluation
        License State: Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None

    Index 4 Feature: datak9
        Period left: Not Activated
        Period Used: 0 minute 0 second
        License Type: Evaluation
        License State: Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None

    Index 5 Feature: gatekeeper
        Period left: Not Activated
        Period Used: 0 minute 0 second
        License Type: Evaluation
        License State: Not in Use, EULA not accepted
        License Count: Non-Counted
        License Priority: None

    Index 6......
    ```

#### Configuración de IP SLA

En este ejemplo, R1 se configura como una fuente de IP SLA. La sonda que está enviando es un mensaje ICMP echo (ping) a 10.1.100.100, utilizando la dirección IP de origen 192.168.1.11. Esta sonda se envía cada 15 segundos y no expira nunca.

La sintaxis que sigue muestra la configuración basada en la figura.

```text
R1# show run | section sla
ip sla 2
 icmp-echo 10.1.100.100 source-ip 192.168.1.11
 frequency 15
ip sla schedule 2 life forever start-time now
```

En este otro ejemplo, R1 se configura como una fuente de IP SLA. La sonda que está enviando es para probar el jitter UDP desde la dirección de origen 192.168.1.11 a 10.1.34.4 utilizando el puerto 65051. Se enviarán 20 paquetes de sondeo para cada test, con un tamaño de 160 bytes cada uno, y se repetirá cada 30 segundos. La sonda se inicia y nunca expira. Para obtener mediciones relacionadas con jitter, es necesario tener un dispositivo destino que puede procesar las sondas y responder a ellas. Por lo tanto, el dispositivo destino debe ser capaz de soportar Cisco IOS IP SLA y ser configurado como *responder*. R2 está configurado como *responder* IP SLA.

La siguiente salida muestra una configuración basada en la figura.

```text
R1# show run | section sla
ip sla 1
 udp-jitter 10.1.34.4 65051 source-ip 192.168.1.11 num-packets 20
  request-data-size 160
 frequency 30
ip sla schedule 1 life forever start-time now
```

```text
R2# show run | section sla
ip sla responder
```

## FUNDAMENTOS PARA EL EXAMEN

- Evalue las características de SNMP y compárelo con SNMPv3.
- Tenga una idea clara del funcionamiento de las comunidades SNMP.
- Piense en la utilidad de una implementación de Syslog y para que se registran los eventos.
- Sepa como reconocer los nombres del Cisco IOS y como administrar sus licencias.
- Estudie el comportamiento de IP SLA y SPAN, compárelos.
- Analice los modelos de Cloud services y las ventajas que ofrecen.
- Recuerde las ventajas de la virtualización, y como funciona.
- Estudie los tipos de virtualizaciones utilizadas en la red.
- Ejercite todas las configuraciones en dispositivos reales o en simuladores.
