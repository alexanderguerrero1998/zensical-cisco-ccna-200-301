# Redes inalámbricas

## Redes WLAN

Una red Ethernet tradicional está definida en los estándares IEEE 802.3. Cada conexión Ethernet tiene que operar bajo unas condiciones controladas, especialmente en lo que se refiere al enlace físico. Tanto el estado, la velocidad y el modo de Duplex deben operar tal como lo describe el estándar.

Las redes inalámbricas están constituidas de una manera similar, pero definidas en el estándar IEEE 802.11. Los dispositivos Ethernet cableados tienen que recibir y transmitir tramas Ethernet acordes al protocolo CSMA/CD (*Carrier Sense Multiple Access/Collision Detect*) en un segmento de red compartido donde los host se comunican de modo Half Duplex: cada host puede hablar libremente y posteriormente escuchar si hay colisiones con otros dispositivos que también están intentando hablar.

Los enlaces Ethernet Full Duplex o conmutados no sufren colisiones ni compiten por el uso del ancho de banda, aunque siguen las mismas normas que Half Duplex. Aunque las redes inalámbricas se basan en el mismo mecanismo, el medio wireless es más difícil de controlar.

Cuando un PC comparte un segmento de red, lo hace con un número conocido de host; cuando el mismo PC utiliza una red wireless utiliza la atmósfera como medio en la capa de acceso, al igual que otros usuarios que son libres de utilizarla.

Una WLAN (*Wireless LAN*) utiliza un medio compartido donde un número indeterminado de host puede competir por el medio en cualquier momento. Las colisiones son un hecho constante en una WLAN porque funciona en modo Half Duplex y siempre dentro de la misma frecuencia. Sólo una estación puede transmitir en un determinado momento de tiempo.

!!! note "NOTA"
    Para lograr el modo Full Duplex todas las estaciones que transmiten y las que reciben deberían hacerlo en frecuencias diferentes. Operación no permitida en IEEE 802.11.

Las tramas ACK sirven como un medio rudimentario para la detección de colisiones, pero no logra prevenirlas. El estándar IEEE 802.11 utiliza un método preventivo llamado CSMA/CA (*Carrier Sense Multiple Access Collision Avoidance*). Mientras que las redes cableadas detectan las colisiones, las redes inalámbricas intentan evitarlas. Todas las estaciones deben escuchar antes de poder transmitir una trama.

Cuando una estación necesita enviar una trama pueden cumplirse estas dos condiciones:

- **Ningún otro dispositivo está transmitiendo.** La estación puede transmitir su trama de inmediato. La estación receptora debe enviar una trama ACK para confirmar que la trama original llegó bien y libre de colisiones.
- **Otro dispositivo está en ese momento transmitiendo una trama.** La estación tiene que esperar hasta que la trama en progreso se haya completado. La estación espera un período aleatorio de tiempo para transmitir su propia trama.

### Topologías WLAN

Una red wireless básica no comprende ningún tipo de organización; un PC con capacidad wireless puede conectarse en cualquier parte y en cualquier momento. Naturalmente debe existir algo más que permita enviar o recibir sobre el medio inalámbrico antes de que el PC pueda comunicarse.

En la terminología 802.11 un grupo de dispositivos wireless se llama SSID (*Service Set Identifier*), que es una cadena de texto incluida en cada trama que se envía. Si hay coincidencia entre receptor y emisor se produce el intercambio. El PC se convierte en cliente de la red wireless y para esto debe poseer un adaptador inalámbrico y un software que interactúen con los protocolos wireless.

El estándar 802.11 permite que dos clientes wireless se comuniquen entre sí sin necesidad de otros medios de red, conocido como red *ad-hoc* o IBSS (*Independent Basic Service Set*).

!!! note "NOTA"
    No existe control incorporado sobre la cantidad de dispositivos que pueden transmitir y recibir tramas sobre un medio wireless. También dependerá de la posibilidad de que agentes externos permitan transmitir a otras estaciones sin dificultad, lo que hace que proporcionar un medio adecuado wireless sea difícil.

**BSS** (*Basic Service Set*) centraliza el acceso y controla sobre el grupo de dispositivos inalámbricos utilizando un AP (*Access Point*) como un concentrador de la red. Cualquier cliente wireless intentando usar la red tiene que completar una condición de membresía con el AP. El AP o punto de acceso lleva a cabo ciertas consideraciones antes de permitir transmitir a la estación:

- El SSID debe concordar.
- Una tasa de transferencia de datos compatible.
- Las mismas credenciales de autenticación.

La membresía con el AP se llama **asociación**, el cliente debe enviar un mensaje de petición de asociación. El AP utiliza un identificador BSS único llamado BSSID que se basa en la propia dirección MAC de radio del AP. El AP permite o deniega la asociación enviando un mensaje de respuesta de asociación. Una vez asociadas todas las comunicaciones desde y hacia el cliente pasarán por el AP. Los clientes ahora no pueden comunicarse directamente con otros sin la intervención del AP.

Un AP puede funcionar como un sistema autónomo y a su vez ser un punto de conexión hacia una red Ethernet tradicional porque dispone de capacidad inalámbrica y de cableado. Los AP situados en sitios diferentes pueden estar conectados entre ellos con una infraestructura de switching. Esta topología recibe el nombre en el estándar 802.11 ESS (*Extended Service Set*).

!!! tip "RECUERDE"
    En ESS un cliente puede asociarse con un AP, pero si el cliente se mueve a una localización diferente puede intercambiarse con otro AP más cercano.

### Funcionamiento de un AP

La función primaria del AP es puentear datos wireless del aire hasta una red tradicional cableada o hacia otra red inalámbrica a través un WGB (*Workgroup Bridge*) o ambas conexiones a la vez. Un AP puede soportar múltiples SSID y aceptar conexiones de un número de clientes wireless de tal manera que éstos se convierten en miembros de la LAN como si fueran conexiones cableadas.

Un AP también puede actuar como un bridge formando un enlace inalámbrico desde una LAN hacia otra en largas distancias. Los enlaces entre los AP son utilizados normalmente para conectividad entre edificios. Los AP conectados con antenas direccionales pueden brindar conectividad en grandes distancias.

Los AP actúan como un punto central controlando el acceso de los clientes a la red LAN. Cualquier intento de acceso a la WLAN debe establecer inicialmente conexión con el AP, quien permitirá un acceso abierto o restringido según las credenciales de autenticación. Los clientes deben efectuar un saludo de dos vías antes de asociarse. El AP puede solicitar más condiciones antes de la asociación, y antes de permitir el acceso al cliente, como credenciales específicas o volumen de datos.

El AP puede compararse con un mecanismo de traducción donde las tramas de un medio son enviadas a otro en capa 2; también asocia el SSID a una o múltiples VLAN.

Cuando la capacidad del enlace inalámbrico no está presente en algún dispositivo, pero sí es posible conectar el dispositivo a una conexión Ethernet, puede utilizarse un tipo de adaptador WGB (*Workgroup Bridge*) para conectar el dispositivo a una red WLAN. Por ejemplo, una impresora que solo tiene una conexión RJ45 el WGB actúa como un adaptador de red inalámbrico externo para ese dispositivo que no tiene ninguno.

### Celdas WLAN

Un AP puede proporcionar conectividad WLAN solamente a los clientes dentro de su cobertura, la señal está definida por la emisión que pueda tener la antena. En un espacio abierto podría describirse como una forma circular alrededor de la antena omnidireccional. El patrón de ondas emitidas tiene tres dimensiones, afectando también a los pisos superiores e inferiores de un edificio.

La ubicación de los AP tiene que estar cuidadosamente planificada para proporcionar cobertura en toda el área necesaria. El hecho de que los clientes sean móviles hace que la cobertura de los AP sea diferente a lo que se espera debido a los objetos que puedan interponerse entre ellos y las antenas.

El área de cobertura del AP se denomina **celda**. Los clientes dentro de una celda pueden asociarse con el AP y utilizar libremente la WLAN.

La celda está limitando la capacidad de operación de los clientes a su radio de cobertura. Para expandir el área total de la cobertura WLAN pueden sumarse más celdas en zonas cercanas simplemente distribuyendo los AP en dichas zonas basándose en estándar 802.11 ESS (*Extended Service Set*). La idea es que la suma de las celdas pueda cubrir cada una de las áreas donde un cliente esté localizado.

Los clientes pueden moverse desde una celda AP a otra y sus asociaciones se van pasando de un AP a otro, mecanismo llamado **roaming**. Los datos que se están confiando en un AP una vez que el cliente se mueve de celda deben ser confiados por el nuevo AP. Esto minimiza la posibilidad de pérdidas de datos durante el proceso de roaming.

Un buen diseño de una red WLAN intenta aprovechar al máximo la cobertura de un AP minimizando la cantidad de puntos de acceso necesarios para cubrir una zona determinada reduciendo a su vez el coste de la instalación. También es importante recordar que el medio es Half Duplex y que a mayor cantidad de usuarios menor ancho de banda disponible.

Para entornos seguros el tamaño de la celda se reduce en microceldas o picoceldas bajando la potencia del AP.

### Radiofrecuencia en WLAN

Las comunicaciones por RF (*Radiofrecuencia*) comienzan con una oscilación transmitida desde un dispositivo que será recibida en uno o varios dispositivos. Esta oscilación de la señal se basa en una constante llamada frecuencia. El transmisor y el receptor deben estar en la misma frecuencia para transmitir la misma señal. Tanto la estación transmisora como la receptora tienen un dispositivo transmisor unido a una antena que permite recibir y transmitir la señal.

Una señal de RF puede ser medida en función de su potencia o energía en unidades de Watts (W) o miliwatt, que es una milésima parte de un Watt. Por ejemplo, un teléfono móvil puede tener una potencia aproximada de 200 mW y un punto de acceso WLAN entre 1 y 100 mW.

Un rango de frecuencias se llama **banda**, como el utilizado en estaciones de radio de AM (*Amplitud Modulada*) o FM (*Frecuencia Modulada*).

Muchas comunicaciones de WLAN ocurren dentro de la banda de 2,4 GHz comprendido en un rango de 2,412 a 2,484 GHz; mientras que otras utilizan una banda de 5 GHz en un rango de 5,150 a 5,825 GHz. La banda de 5 GHz contiene cuatro bandas separadas y distintas:

- de 5.150 a 5.250 GHz
- de 5.250 a 5.350 GHz
- de 5.470 a 5.725 GHz
- de 5.725 a 5.825 GHz

La señal emitida por una estación wireless se llama **portadora** (*carrier*), es una señal constante a una determinada frecuencia. Una estación de radio que sólo transmite la portadora no está emitiendo datos de ningún tipo. Para agregar información, el transmisor debe modular la portadora para insertar la información que desea transmitir. Las estaciones receptoras deben revertir el proceso demodulando la portadora para recuperar la información original.

Los métodos de modulación pueden ser diferentes según hagan variar la frecuencia o la amplitud de la señal portadora. Las WLAN utilizan unas técnicas de modulación más complejas porque sus volúmenes de datos son mayores que los de audio.

El principio de la modulación WLAN es empaquetar tantos datos como sean posibles dentro de una señal y de esa manera minimizar las posibles pérdidas por interferencias o ruidos. Cuando los datos se pierden deben ser retransmitidos utilizando más recursos.

Aunque el receptor espera encontrar la portadora en una frecuencia fija, la modulación hace que la portadora varíe cada cierto tiempo. Esta variación de la frecuencia de la portadora se llama **canal**, a la que se hace referencia con un tipo de numeración. Los canales WLAN están definidos en el estándar 802.11.

### Estándares WLAN

Todos los estándares WLAN están incluidos en las series IEEE 802.11. Definen la operación de capa 1 y de capa 2, que incluye las frecuencias, los canales wireless, el rendimiento, la seguridad, la movilidad, etc.

La frecuencia de las WLAN utiliza una banda que no tiene licencias lo que permite a cualquiera utilizarla sin ningún permiso. Pero existe una regulación que establece reglas sobre qué frecuencias están disponibles y qué potencias se pueden utilizar.

Algunas de las agencias reguladoras pueden ser:

- Federal Communications Commission (FCC)
- Electrical and Electronics Engineers (IEEE)
- European Telecommunications Standard Institute (ETSI)
- La alianza Wi-Fi
- La alianza Wireless Ethernet Compatibility (WECA).
- La asociación WLANA

Los estándares IEEE 802.11 están contenidos en la siguiente tabla:

| Estándar | 2,4GHz | 5GHz | Velocidad | Fecha |
| --- | --- | --- | --- | --- |
| 802.11 | Si | No | 2 Mbps | 1997 |
| 802.11b | Si | No | 11 Mbps | 1999 |
| 802.11a | No | Si | 54 Mbps | 1999 |
| 802.11g | Si | No | 54 Mbps | 2003 |
| 802.11n | Si | Si | 600 Mbps | 2009 |
| 802.11ac | No | Si | 6.93 Gbps | 2003 |
| 802.11ax | Si | Si | 4x802.11ac | 2019 |

Los clientes inalámbricos y los AP pueden ser compatibles con uno o más estándares, sin embargo, un cliente y un AP solo pueden comunicarse si ambos soportan y aceptan usar el mismo tipo de normativa.

## Arquitectura WLAN

Tradicionalmente la arquitectura WLAN se centra en los AP. Cada uno de los AP funciona como un concentrador de su propio BSS dentro de la celda donde los clientes se localizan para obtener la correspondiente asociación con el AP. El tráfico desde y hacia cada cliente debe pasar por el AP.

Cada AP debe ser configurado individualmente, aunque puede darse el caso de que varios utilicen las mismas políticas. Cada AP opera de manera independiente utilizando su propio canal de RF, la asociación con los clientes y la seguridad. En síntesis, cada AP es autónomo. Por este último motivo la gestión de la seguridad en una red wireless puede ser difícil. Cada AP autónomo maneja sus propias políticas de seguridad, no existe un lugar común para monitorizar la seguridad, detección de intrusos, políticas de ancho de banda, etc.

Gestionar las operaciones de RF de varios AP autónomos puede ser también bastante difícil. Cuestiones como las interferencias, la selección de canales, la potencia de salida, cobertura, solapamientos y zonas negras pueden ser partes conflictivas para la configuración de los AP autónomos.

### Cisco Wireless Architectures

A medida que la red inalámbrica crece se hace más difícil configurar y administrar cada AP. Cisco ofrece plataformas de gestión como Cisco Prime Infrastructure o Cisco DNA Center de donde desde una ubicación especifica dentro de la empresa es posible administrar la red wireless.

Esta arquitectura *cloud-based* AP envía y almacena toda la gestión de los AP en la nube. Esta arquitectura ofrece las siguientes capacidades centralizadas de tal manera que los dispositivos de la red inalámbrica las reciben independientemente de donde se encuentren:

- Seguridad
- Desarrollo
- Configuración y Administración
- Control y monitorización

Los AP Cisco Meraki están basados en la nube, una vez que se enciendan y se registren en la nube, se autoconfigurarán. A partir de ese momento se puede administrar el AP desde el panel de control de la nube Meraki.

Los procesos de tiempo real involucran enviar y recibir las tramas 802.11, las señales de los AP y los mensajes *probe* con información de la red. La encriptación de los datos también se maneja por paquete y en tiempo real. El AP debe interactuar con los clientes wireless a nivel de capa 2 desde la subcapa MAC, estas funciones son parte del hardware del AP. Las tareas de gestión no son integrales al manejo de tramas sobre señales RF, de esta forma estas funciones pueden dividirse, facilitando la administración centralizadamente.

!!! note "NOTA"
    Los mensajes *probe* contienen información sobre la red, se envían periódicamente y sirven para anuncia la presencia de una WLAN y para sincronizar a los miembros del conjunto de servicios.

Por lo tanto, cuando las funciones del AP se dividen, se puede elegir un AP determinado para llevar a cabo solamente la operación 802.11 en tiempo real en cuyo caso el AP se llama LAP (*Lightweight Access Point*). Los LAP reciben su nombre porque realizan menor cantidad de tareas que un AP tradicional autónomo. Mientras que las funciones de gestión se llevan a cabo en el WLC (*Wireless LAN Controller*) que es común a varios AP. Las funciones del WLC son la autenticación de usuarios, políticas de seguridad, administración de canales, niveles de potencia de salida, etc.

Esta división de tareas se conoce como arquitectura **split-MAC**, donde las operaciones normales de MAC son separadas en dos ubicaciones distintas, esto ocurre por cada LAP en la red. Cada uno tiene que unirse a sí mismo con un WLC de manera que pueda encender y soportar a los clientes wireless. El WLC se convierte en el concentrador que soporta un número variado de LAP en la red conmutada.

El proceso de asociación del LAP con el WLC se produce a través de un túnel para pasar los mensajes relativos a 802.11 y los datos de los clientes. Los LAP y el WLC pueden estar localizados en la misma subred o VLAN, pero no tiene que ser siempre así. El túnel hace posible el encapsulado de los datos entre ambos AP dentro de nuevos paquetes IP. Los datos tunelizados pueden ser conmutados o enrutados a través de la red del campus.

El LAP y el WLC utilizan para intercambiar mensajes a través del túnel el **CAPWAP** (*Control and Provisioning of Wireless Access Points*) y lo hacen de dos modos diferentes:

- **Mensajes de control CAPWAP**, son mensajes utilizados para la configuración del LAP y gestionan la operación. Estos mensajes están autenticados y encriptados de tal manera que el LAP es controlado de manera segura solamente por el WLC.
- **Datos CAPWAP**, los paquetes hacia y desde los clientes wireless son asociados con el LAP. Los datos son encapsulados dentro de LWAPP pero por defecto no están encriptados entre el AP y el WLC. Cuando se habilita la encriptación de los datos en un AP, los paquetes se protegen con el protocolo DTLS (*Datagram Transport Layer Security*).

!!! tip "RECUERDE"
    CAPWAP está basado en el LWAPP (*Lightweight Access Point Protocol*) y está definido en las RFCs 5415, 5416, 541 y 5418.

### Funciones de los WLC y LAP

Una vez que los túneles CAPWAP se construyen desde el WLC a uno o más LAP, el WLC puede comenzar a ofrecer una cantidad de funciones adicionales:

- **Asignación de canales dinámicos:** el WLC elige la configuración de los canales de RF que usará cada LAP basándose en otros AP activos en el área.
- **Optimización potencia de transmisión:** el WLC configura la potencia de transmisión para cada LAP en función de la cobertura de área necesaria y se ajusta automáticamente de manera periódica.
- **Solución de fallos en la cobertura:** si un LPA deja de funcionar, el hueco que deja la falta de cobertura es solucionado aumentando el poder de transmisión en los LAP que hay alrededor de manera automática.
- **Roaming flexible:** los clientes pueden moverse libremente en capa 2 o en capa 3 con un tiempo de roaming muy rápido.
- **Balanceo de carga dinámico:** cuando 2 o más LAP están posicionados para cubrir la misma área geográfica el WLC puede asociar los clientes con el LAP menos usado distribuyendo la carga de clientes entre los LAP.
- **Monitorización de RF:** el WLC gestiona cada LAP de manera que pueda buscar los canales y monitorizar el uso de la RF. Escuchando en un canal el WLC puede conseguir información sobre interferencias, ruido, señales de diversos tipos.
- **Gestión de la seguridad:** el WLC puede requerir a los clientes wireless que obtengan una dirección IP de un servidor DHCP confiable antes de permitirles su asociación con la WLAN.

Para manejar un gran número de LAP se pueden desplegar varios WLC de manera redundante. La gestión de varios WLC puede requerir un esfuerzo significativo, debido a que el número de AP y clientes para ser monitorizados y gestionados puede ser elevado.

El LAP lleva una configuración muy básica, normalmente está en modo local cuando proporciona BSS y permite que los dispositivos del cliente se asocien a WLAN. Para funcionar en otros modos el AP debe tener una configuración inicial para encontrar un WLC y recibir la configuración completa de tal manera que nunca necesite ser configurado por el puerto de consola. Los siguientes pasos detallan el proceso de inicio que el LAP tiene que completar antes de entrar en actividad:

1. Se obtiene una dirección desde un servidor DHCP. El servidor DHCP debe estar configurado con la opción DHCP 43.
2. Obtenida la IP, el LAP efectúa un broadcast con un mensaje de petición esperando encontrar un WLC en la misma subred. Esta función sólo es posible si existe adyacencia de capa 2.
3. El LAP aprende la dirección IP de los WLC disponibles.
4. Envía una petición de unión al primer WLC que encuentra en la lista de direcciones. Si el primero no responde se intenta con el siguiente. Cuando el WLC acepta al LAP envía una respuesta para hacer efectiva la unión.
5. El WLC compara el código de imagen del LAP con el código que tiene localmente almacenado, el LAP descarga la imagen y se reinicia.
6. El WLC y el LAP construyen un túnel seguro CAPWAP para tráfico de gestión y otro similar no seguro para los datos del cliente.

La mayoría de los AP de Cisco pueden funcionar como autónomos o como LAP, dependiendo de la imagen que tenga cargada. Desde el WLC, también puede configurar un LAP para operar en modos especiales extras, añadiendo más y mejores funcionalidades.

## Diseño de WLAN

A partir de un sistema autónomo que puede implementarse en una red hogareña o en una pequeña oficina SOHO (*Small Office Home Office*), el diseño puede variar según las necesidades de la empresa o la escalabilidad necesaria.

En entornos de pequeña escala, como ubicaciones de sucursales pequeñas o medianas es posible que no sea necesario el uso de WLC dedicados. En este caso, la función WLC se puede ubicar junto con un AP instalado en el sitio de la sucursal. Esto se conoce como implementación de WLC **Cisco Mobility Express**. Un WLC Mobility Express puede soportar hasta **100 AP**.

Para campus pequeños o ubicaciones de sucursales distribuidas, donde el número de AP es relativamente pequeño en cada uno, el WLC puede ubicarse conjuntamente con los switchs instalados en cada sucursal, como se muestra en la Figura 27-10. Esto se conoce como una implementación **embedded WLC** porque el WLC está integrado dentro del hardware de conmutación. Esta implementación de Cisco puede soportar hasta **200 AP**. Los AP no necesariamente tienen que estar conectados a los switchs que alojan el WLC, pueden estar en otras ubicaciones y unirse al WLC.

Un WLC también puede ubicarse en una posición central en la red, dentro de un centro de datos en una nube privada. Esto se conoce como un despliegue **cloud-based WLC**, donde el WLC existe como una máquina virtual en lugar de un dispositivo físico. Si la plataforma de informática en la nube ya existe, entonces implementar un WLC basado en la nube se vuelve sencillo. Este tipo de controlador puede admitir hasta **3000 AP**.

Otro enfoque es instalar el WLC en una ubicación central para que pueda maximizar el número de AP unidos a él. Esto se llama implementación unificada o **centralized WLC**, que tiende a seguir el concepto de concentrar todos los recursos que los usuarios necesitan alcanzar en una ubicación central, como un centro de datos o Internet. El tráfico hacia y desde los usuarios inalámbricos viajaría por los túneles CAPWAP. La estabilidad y la implementación de políticas de seguridad aplicables a los usuarios inalámbricos son algunos de los factores más importantes en el diseño unificado. Un WLC centralizado puede soportar un máximo de **6000 AP**.

El WLC puede conectarse a uno o varios puertos de un switch, ya sea en modo de acceso, troncal o LAG (*Link Aggregation Group*). LAG se configura como un mismo grupo lógico como un EtherChannel de modo que los puertos se agrupan para actuar como un enlace más grande. Si falla un puerto individual, el tráfico se redirigirá a los puertos de trabajo restantes.

!!! note "NOTA"
    Los WLC de Cisco no admiten ningún protocolo de negociación LAG, como LACP o PaGP. Por lo tanto, debe configurar los puertos del switch en modo *on* de manera que los puertos que forman el EtherChannel estén siempre activos.

## Seguridad WLAN

Como concentrador central de BSS (*Basic Service Set*) un AP gestiona las WLAN de los clientes dentro de su rango. Todo el tráfico desde y hacia un cliente pasa a través del AP para alcanzar otros clientes en la BSS o clientes cableados localizados en cualquier otro sitio. Los clientes inalámbricos no se pueden comunicar directamente entre sí.

El AP es el dispositivo donde se implementarán varias formas de seguridad, por ejemplo, el control de los miembros WLAN autenticando a los clientes: en caso de un fallo de autenticación no le será permitido el uso de la red wireless. También el AP y sus clientes pueden trabajar juntos para asegurar los datos que fluyen entre ellos.

Cuando un cliente intenta establecer una conexión wireless primero tiene que buscar un AP que sea alcanzable y presentar sus credenciales. El cliente tiene que negociar su admisión y las medidas de seguridad en la siguiente secuencia:

1. Usar un SSID que concuerde con el AP.
2. Autenticarse con el AP.
3. Utilizar un método (opcional) de encriptación de paquetes (privacidad de datos).
4. Utilizar un método (opcional) de autenticación de paquetes (integridad de datos).
5. Construir una asociación con el AP.

En las redes 802.11 los clientes pueden autenticarse con un AP utilizando alguno de los siguientes métodos:

1. **Autenticación abierta**, en este método no utiliza ningún tipo de autenticación, simplemente ofrece un acceso abierto al AP.
2. **Pre-Phared Key (PSK)**, se define una clave secreta en el cliente y en el AP. Si la clave concuerda se le concede el acceso al cliente.

El proceso de autenticación en estos dos métodos se termina cuando el AP admite el acceso. El AP posee suficiente información en sí mismo para de manera independiente determinar si el cliente puede o no tener acceso. La autenticación abierta y PSK son considerados métodos antiguos, no escalables y poco seguros. En el caso de la autenticación abierta sólo el SSID es solicitado y aunque hace que la configuración sea extremadamente fácil, no proporciona ningún tipo de medida de seguridad.

### WEP

La autenticación compartida (PSK) utiliza una clave conocida como WEP (*Wireless Equivalence Protocol*) que se guarda en el cliente y en el AP. Cuando un cliente intenta unirse a la WLAN el AP presenta un desafío al cliente quien exhibe su clave WEP para hacer un cómputo y enviar de vuelta la clave y el desafío al AP, si los valores son idénticos el cliente es finalmente autenticado.

La clave WEP también sirve para autenticar cada paquete cuando se envía por la WLAN, sus contenidos son procesados por un mecanismo criptográfico. Cuando los paquetes son recibidos en el otro extremo el contenido se desencripta utilizando la misma clave WEP. Este método de autenticación es, obviamente, más seguro que la autenticación abierta pero aun así tiene su lado negativo:

- No se escala bien porque el uso de una cadena de claves tiene que estar configurada en cada dispositivo.
- No es del todo seguro.
- Las claves permanecen hasta su reconfiguración manual.
- Las claves pueden ser desencriptadas.

### Métodos de seguridad EAP

EAP (*Extensible Authentication Protocol*) es el mecanismo básico de seguridad de muchas redes wireless. EAP está definido en la RFC 3748 y fue diseñado para manejar las autenticaciones de usuario vía PPP. Debido a que es extensible permite una variedad de métodos de entornos de seguridad. La RFC 4017 cubre las variantes de EAP que pueden ser utilizadas en WLAN tales como:

- **LEAP** (*Lightweight EAP*), desarrollado por Cisco. Se utiliza un servidor RADIUS externo para manejar la autenticación de los clientes.
- **EAP-TLS**, definido en la RFC 2716 y utiliza TLS (*Transport Layer Security*) para autenticar a los clientes de manera segura. Basado en SSL (*Secure Socket Layer*), utilizado para acceder a sesiones Web seguras. Cada AP tiene que tener un certificado generado por una autoridad certificadora. Cada vez que el cliente intenta autenticarse el servidor crea una clave nueva y será única para cada cliente.
- **PEAP** (*Protected EAP* o EAP-PEAP), es similar al EAP-TLS. Requiere un certificado digital sólo en el servidor de autenticación de tal manera que el mismo puede autenticar a los clientes. Cada vez que el cliente intenta autenticarse el servidor crea una clave nueva y será única para cada cliente. Pueden utilizarse cualquiera de estos dos métodos:
    - MS-CHAPv2 (*Microsoft Challenge Handshake Authentication Protocol V2*)
    - GTS (*Generic Token Card*), es un dispositivo de hardware que genera contraseñas de un solo uso para el usuario o una contraseña generada manualmente
- **EAP-FAST** (*EAP Flexible Authentication via Secure Tunneling*), es un método de seguridad wireless desarrollado por Cisco. Su nombre indica flexibilidad reduciendo la complejidad de la configuración. No se utilizan certificados digitales. Construye un túnel seguro entre el cliente y el servidor utilizando PAC (*Protected Access Credential*) como única credencial para construir el túnel.

### WPA

El estándar IEEE 802.11i se centra en resolver los problemas de seguridad en las WLAN, incluso abarca más allá que la autenticación del cliente utilizando claves WEP. WPA (*Wi-Fi Protected Access*) utiliza varios de los componentes del estándar 802.11 proporcionando las siguientes medidas de seguridad:

- Autenticación de cliente utilizando 802.1x o llave precompartida.
- Autenticación mutua entre cliente y servidor.
- Privacidad de los datos con TKIP (*Temporal Key Integrity Protocol*).
- Integridad de los datos utilizando MIC (*Message Integrity Check*).

TKIP acentúa la encriptación WEP en hardware dentro de los clientes wireless y el AP. El proceso de encriptación WEP permanece, pero las llaves son generadas más frecuentemente que con los métodos EAP. TKIP genera nuevas llaves por cada paquete. Se crea una llave inicial cuando el cliente se autentica por algún método AEP, la llave se genera con una mezcla de la dirección MAC del transmisor con un número de secuencia. Cada vez que un paquete es enviado la llave WEP se actualiza incrementalmente.

WPA puede utilizar llaves precompartidas para autenticación si no se utilizan servidores de autenticación externos. Para estos casos la llave precompartida se utiliza sólo para la autenticación mutua entre el cliente y el AP. La privacidad de datos y la encriptación no utilizan la llave precompartida. TKIP se encarga de la encriptación de la llave para la posterior encriptación WEP.

El proceso MIC (*Message Integrity Check*) se utiliza para generar una huella digital por cada paquete que se envía en la WLAN comparándolo con los contenidos al recibir el paquete. De esta manera se consigue la integridad de los datos para que no puedan modificarse y poder compararlos con la huella enviada. Por cada paquete MIC se genera una llave con un cálculo complejo que solamente pude ser generado en una sola dirección. Para desencriptarlo es necesario conocer la dirección MAC del destino para efectuar los cálculos necesarios.

### WPA2

WPA2 (*Wi-Fi Protected Access V2*) está basado en el estándar 802.11i. Se extiende mucho más en las medidas de seguridad que WPA. Para la encriptación de los datos se utiliza AES-CCMP (*Advanced Encryption Standard-Counter/CBC-MAC Protocol*) que es un método robusto y escalable adoptado para utilizarlo por muchas organizaciones gubernamentales. Soporta TKIP para la encriptación de los datos y compatibilidad con WPA.

Con WPA o con autenticación EAP un cliente wireless tiene que autenticar al AP que visita, si el cliente se está moviendo de un AP a otro el continuo proceso de autenticación puede llegar a ser tedioso. WPA2 resuelve este problema utilizando PKC (*Proactive Key Caching*) donde un cliente se autentica sólo una vez en el primer AP que se encuentra. Si el resto de los AP soportan WPA2 y están configurados como un grupo lógico, la autenticación se pasa automáticamente de un AP a otro.

### WPA3

WPA3 nace como reemplazo futuro para WPA2, agregando varios mecanismos de seguridad importantes y superiores que solventan las vulnerabilidades de la versión 2. WPA3 utiliza un cifrado más fuerte con AES-GCMP (*Advanced Encryption Standard-Galois/Counter Mode Protocol*). También utiliza PMF (*Protected Management Frames*) para evitar actividades maliciosas que puedan suplantar o alterar la operación entre AP y los clientes de un BSS. La clave no se envía, y el intercambio es tal que un observador que capture los paquetes enviados, no puede averiguar ni la clave original ni la clave maestra generada.

WPA3 puede utilizarse en dos modos diferentes:

- WPA3-personal
- WPA3-enterprise, posee niveles de seguridad más elevados para entornos en los que se requiere mayor seguridad (gobierno, aplicaciones militares, etc.)

!!! tip "RECUERDE"
    Tipo de autenticación y encriptación en WPA, WPA2 y WPA3:

    | Tipo de autenticación y encriptación | WPA | WPA2 | WPA3 |
    | --- | --- | --- | --- |
    | Autenticación con Pre-Shared Keys | Sí | Sí | Sí |
    | Autenticación con 802.1x | Sí | Sí | Sí |
    | Encriptación y MIC con TKIP | Sí | No | No |
    | Encriptación y MIC con AES y CCMP | Sí | Sí | No |
    | Encriptación y MIC con AES y GCMP | No | No | Sí |

## Caso práctico

### Configuración de una WLAN

La configuración inicial de un AP de Cisco debe realizarse a través de un cable de consola conectado al puerto serie de un PC. Una vez que el AP tiene una dirección IP y está conectado a la red también puede usar Telnet o SSH para conectarse a su CLI a través de la red cableada. Los AP autónomos admiten sesiones de administración basadas en navegador a través de HTTP y HTTPS. Los LAP pueden administrarse desde una sesión de navegador al WLC.

Un puerto de un switch que posee una conexión por cable a un AP puede configurarse en modo acceso o troncal. En el modo troncal, la encapsulación 802.1Q etiqueta cada trama de acuerdo con el número de VLAN del que proviene. El lado inalámbrico de un AP inherentemente conecta las tramas 802.11 al marcarlas con el BSSID de la WLAN a la que pertenecen. Todas las VLAN cableadas configuradas en el WLC pueden asignarse a las WLAN configuradas en el LAP, estas VLAN se transportan a través del túnel CAPWAP entre los dos dispositivos.

Una vez que el WLC tenga una configuración inicial y una dirección IP puede abrir un navegador web en la dirección de administración del WLC con HTTP o HTTPS. La interfaz gráfica de usuario GUI (*Graphical User Interface*) proporciona una manera amigable y efectiva de configurar, administrar, monitorizar y solucionar problemas en la red wireless.

Comience la configuración básica en el administrador del sistema, iniciando una sesión de emulación de terminal con las opciones ya conocidas:

- 9600 baudios
- 8 bits de datos
- 1 bit de detención
- Ninguna paridad
- Sin control del flujo de hardware

```text
Welcome to the Cisco Wizard Configuration Tool
. . . . . . . . . . . . . . . . . . . . . . . .
Enter Administrative User Name (24 characters max): admin
Enter Administrative Password (24 characters max): *****
Service Interface IP Address Configuration [none][DHCP]: none
Enable Link Aggregation (LAG) [yes][NO]: No
Management Interface IP Address: 192.168.60.10
Management Interface Netmask: 255.255.255.0
Management Interface Default Router: 192.168.60.1
Management Interface VLAN Identifier (0 = untagged): 10
. . . . . . . . . . . . . . . . . . . . . . . .
```

Tanto la GUI basada en la web como la CLI requieren que los administradores inicien sesión. Los usuarios pueden autenticarse localmente o con un servidor AAA (*Authentication, Authorization, Accounting*), como TACACS+ o RADIUS.

!!! note "NOTA"
    Siguiendo los objetivos del examen de certificación CCNA 200-301 se ha configurado un WLC utilizando la interfaz GUI en un escenario de pruebas, sobre un direccionamiento privado clase C. Las capturas de pantalla muestran los pasos a seguir. Cada paso de configuración se realiza mediante una sesión de navegador web que está conectada a la dirección IP de administración del WLC.

El primer paso es definir una WLAN en el controlador, de esta forma el WLC vinculará los AP a la interfaz correspondiente, los clientes comenzarán entonces a recibir tramas con la información correspondiente a su WLAN y podrán unirse al BSS. Las WLAN pueden estar asociadas a una VLAN, por lo tanto el tráfico de una VLAN hacia otra, solo será posible mediante los servicios de un router a través de la infraestructura de la red cableada.

De forma predeterminada, un WLC tiene una configuración mínima, por lo que no se definen WLAN. Antes de crear una nueva WLAN, hay que tener en cuenta las siguientes cuestiones:

- Los WLC admiten un máximo de 512 WLAN, pero solo 16 de pueden configurarse activamente en un AP
- Será necesario configurar un SSID
- Definir una interfaz del controlador y número de VLAN
- Tipo de seguridad inalámbrica
- Anunciar cada WLAN a los clientes inalámbricos potenciales consume recursos

Seleccione **WLAN** en la barra de menú superior, para crear una WLAN nueva haga clic en el botón **Go**. En la siguiente pantalla configure el nombre y el SSID, en nuestro caso se ha utilizado el mismo nombre para ambos, `Desarrollo005` (estos no tienen por qué ser idénticos).

Una vez aplicados los cambios pueden seguir añadiéndose configuraciones tales como seguridad, QoS, elección de la RF utilizada, también se muestra el estado de la WLAN y su vinculación con el SSID. Observe que, aunque la página General muestra una política de seguridad predeterminada para la WLAN la WPA2 con 802.1x, puede realizar cambios a través de la pestaña Security.

!!! tip "RECUERDE"
    La casilla **Broadcast SSID** permite a los AP transmitir el nombre del SSID automáticamente. Desmarcar esta casilla para que el nombre del SSID no se difunda no contribuye en nada sustancial a la seguridad de WLAN.

Defina un servidor RADIUS para comenzar a configurar la seguridad de su nueva WLAN. Si se definen varios servidores, el controlador los probará en orden secuencial. En la captura aparecen dos servidores configurados, 192.168.0.33 y 192.168.0.34.

Para añadir un nuevo servidor, ingrese la dirección IP, la clave secreta compartida y el número de puerto. Como el WLC ya tenía dos servidores RADIUS configurados, el servidor en 192.168.0.35 será por orden el número 3. En **server status** active el servidor para que el controlador pueda comenzar a usarlo. En la parte inferior de la página, puede seleccionar el tipo de usuario que se autenticará con el servidor:

- Network User, para autenticar clientes inalámbricos
- Management, para autenticar administradores inalámbricos

Finalice haciendo clic en **Apply**.

Para crear una nueva interfaz dinámica, acceda a **Controlador/Interfaces**, en este caso ya existen dos interfaces llamadas "Administrador" y "Backup". Haga clic en **Nuevo** para definir una nueva interfaz. Ingrese un nombre para dicha interfaz y el número de VLAN al que estará vinculado, en este caso "Prueba" y VLAN10. Finalice con el botón **Aplicar**.

Luego, configure la dirección IP, la máscara y la dirección de la puerta de enlace para la interfaz. En nuestro ejemplo 192.168.0.12 255.255.255.0. También debe definir las direcciones del servidor DHCP primario y secundario que usará el controlador para las solicitudes DHCP de los clientes vinculados a la interfaz, en este caso 192.168.0.101 y 102. Haga clic en el botón **Aplicar** para completar la configuración de la interfaz y volver a la lista de interfaces.

El siguiente paso es configurar los ajustes de la seguridad, desde la pestaña **Security**. Seleccione los ajustes apropiados según las exigencias de la red a nivel de capa 2, salvo que se especifique lo contrario intente configurar las opciones de seguridad más fuertes y fiables.

En la siguiente imagen se ha seleccionado **WPA+WPA2** en el menú desplegable y dentro de los parámetros la encriptación WPA2 y AES. En lo que respecta a las claves de autenticación se ha seleccionado **PSK**. La WLAN `Desarrollo005` solo permitirá autenticación WPA2-Personal con clave precompartida PSK (*pre-shared key*).

Para usar WPA2-Enterprise, marque la opción **802.1X**. En ese caso, se usarían 802.1x y EAP para autenticar clientes inalámbricos en uno o más servidores RADIUS. El controlador usaría servidores de la lista que ha definido previamente. Para especificar los servidores que puede usar la WLAN, debe seleccionar la pestaña **Security** y luego la pestaña **AAA Servers**. Al lado de cada servidor, seleccione una dirección IP específica del servidor en el menú desplegable de servidores definidos globalmente, en este caso 192.168.0.33, 192.168.0.34 y 192.168.0.35 respectivamente. Los servidores se prueban en orden secuencial hasta que uno de ellos responde (puede configurar hasta seis).

A continuación, siguiendo las exigencias del examen de certificación CCNA, configure la calidad de servicio para la WLAN. Seleccione la pestaña **QoS**, luego en el menú desplegable *Quality of Service* marque la que usted necesite de las siguientes opciones:

- Platinum (voice)
- Gold (vídeo)
- Silver (best effort)
- Bronze (background)

Por defecto, el controlador funciona en *best effort*.

Finalmente, para que la configuración tenga efecto haga clic en el botón **Apply**, se creará la nueva WLAN y se agregará la nueva configuración al WLC.

De manera predeterminada, y como medida de seguridad, un controlador no permitirá el tráfico de administración desde una WLAN. Esto significa que no se puede acceder a la GUI o CLI del controlador desde un dispositivo inalámbrico que esté asociado a la WLAN. Sin embargo, siempre se puede acceder a través de sus interfaces cableadas. Este comportamiento se puede modificar globalmente para todas la WLAN, de manera que sea accesible la administración desde cualquier WLAN. Seleccione la pestaña **Management** y luego en la barra lateral **Logs/Mgmt Via Wireless**.

!!! note "NOTA"
    Para este caso práctico se ha tomado como referencia un dispositivo Cisco 5520 WLC.

## Fundamentos para el examen

- Analice el principio del funcionamiento de una WLAN, compárelo con una LAN tradicional y los respectivos métodos para evitar o detectar colisiones.
- Recuerde cuales son los dispositivos necesarios para el funcionamiento de una WLAN, tanto en un medio pequeño como en una red empresarial.
- Recuerde que es SSID, BSS, BSSID.
- Compare el funcionamiento de un AP autónomo y una arquitectura centralizada.
- Recuerde los conceptos básicos de radiofrecuencia.
- Estudie los estándares WLAN y compárelos.
- Recuerde las funciones de los WLC y LAP.
- Entienda y analice como construyen los túneles CAPWAP.
- Estudie los métodos de seguridad, autenticación y encriptación compárelos entre sí.
