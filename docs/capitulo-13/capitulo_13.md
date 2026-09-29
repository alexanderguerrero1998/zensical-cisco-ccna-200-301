# Automatización de la red

## SDN

Las redes definidas por software SDN (*Software Defined Networking*) permiten a las organizaciones acelerar la implementación y la distribución de aplicaciones reduciendo drásticamente los costes mediante la automatización del flujo de trabajo basada en políticas. La tecnología SDN habilita arquitecturas de nube mediante distribución y movilidad de aplicaciones de manera automatizada, a pedido y a escala. Las SDN incrementan los beneficios de la virtualización del centro de datos, ya que aumentan la flexibilidad y la utilización de recursos y reducen los gastos generales y los costos de infraestructura.

### Arquitectura SDN

Un dispositivo de red está dividido en dos planos diferentes, por ejemplo el procesador de un router se encarga de enrutar o enviar la mayoría del tráfico que le llega con destino diferente al propio router, mecanismo conocido como el *data plane*. Mientras que determinados tipos de tráfico, como por ejemplo actualizaciones de enrutamiento, tráfico de gestión, *keepalives*, etc. que están destinados al propio router, esto es conocido como plano de control o *Control Plane*.

Básicamente las funciones de cada plano son las siguientes:

- **Control Plane:**
    - Toma decisiones acerca de dónde se envía el tráfico.
    - Los paquetes del plano de control están destinados localmente o son originados por el propio router.
    - Incluyen la configuración del sistema, la gestión y el intercambio de información de la tabla de enrutamiento.
    - Contiene mecanismos de envío de capa 2 y capa 3, tales como tablas de adyacencias IPv4 e IPv6, tablas de topologías, tablas ARP y STP.
- **Data plane:**
    - También conocido como el plano de reenvío.
    - Reenvía el tráfico al siguiente salto en el camino hacia la red de destino seleccionada de acuerdo a la lógica del plano de control.
    - Los paquetes del plano de datos pasan por el router o por el switch.
    - Los routers y switches lo utilizan para enviar flujos de tráfico.

!!! note "NOTA"
    Cisco Express Forwarding (CEF) es una tecnología de conmutación de capa 3 avanzada que permite el envío de paquetes del plano de datos sin consultar el plano de control.

### Arquitectura SDN

En la arquitectura tradicional de un router o un switch las funciones del plano de control y del plano de datos se producen en el mismo dispositivo. Una red definida por software (SDN) mueve el plano de control de cada dispositivo de red a una entidad central de administración y control denominado SDN *controller*.

Para convertir el concepto de SDN en una aplicación práctica, se deben cumplir dos requisitos. En primer lugar, tiene que haber una arquitectura lógica común en todos los switches, routers y otros dispositivos de red que será gestionado por un controlador SDN. Esta arquitectura lógica puede implementarse de diferentes maneras en diferentes equipos de proveedores y en diferentes tipos de dispositivos de red, siempre que el controlador SDN interprete una función lógica uniforme entre todos ellos. En segundo lugar, se necesita un protocolo estándar, seguro entre el controlador SDN y el dispositivo de red.

Ambas exigencias las trata OpenFlow, que es a la vez un protocolo entre los controladores SDN y dispositivos de red, así como una especificación de la estructura lógica de la red.

Las funciones de un controlador SDN pueden resumirse en las siguientes:

- Define los flujos de datos que se producen en el plano de datos SDN. Un flujo de datos es una secuencia de paquetes que atraviesan una red y que comparten un conjunto de valores de los campos de cabecera.
- Todas las funciones complejas son realizadas por el controlador.
- El controlador completa y gestiona las tablas de flujo de los switches.
- El controlador SDN se comunica con dispositivos compatibles con OpenFlow utilizando el protocolo OpenFlow.
- Utiliza Transport Layer Security (TLS) para enviar de forma segura las comunicaciones del plano de control sobre la red.
- Cada switch OpenFlow se conecta a otros switches OpenFlow.

Para el switch, un flujo es una secuencia de paquetes que coincide con una entrada específica en una tabla de flujo. Las tablas tienen los objetivos siguientes:

- Una tabla de flujo compara los paquetes de entrada de un flujo particular y especifica las funciones que se van a realizar en los paquetes.
- Un medidor de tabla desencadena una serie de acciones relacionadas con el rendimiento en un flujo.
- Una tabla de flujo puede dirigir un flujo a una tabla de grupo, que puede accionar una variedad de acciones que afectan a uno o más flujos.

### Tipos de SDN

Existen tres tipos de modelos de SDN:

- **Device-based SDN:** los dispositivos son programables por aplicaciones que se ejecutan en el propio dispositivo o en un servidor en la red. Cisco OnePK es un ejemplo de un SDN basado en dispositivo. Se permite crear aplicaciones utilizando C, Java y Python, integrar e interactuar con los dispositivos de Cisco.
- **Controller-based SDN:** utiliza un controlador centralizado que tiene conocimiento de todos los dispositivos en la red. Las aplicaciones pueden interactuar con el controlador responsable de la gestión de dispositivos y manipular los flujos de tráfico en toda la red. Cisco Open SDN Controller es una distribución comercial de OpenDaylight.
- **Policy-based SDN:** similar al Controller-based SDN donde un controlador centralizado tiene una vista de todos los dispositivos en la red. SDN basado en políticas incluye una capa adicional donde la política funciona a un nivel más alto de abstracción. Utiliza aplicaciones integradas que automatizan las tareas de configuración avanzada a través de un flujo de trabajo guiado y de interfaz gráfica de usuario fácil de usar sin conocimientos de programación necesarios. Cisco APIC-EM es un ejemplo de este tipo de SDN.

### Southbound y Northbound API

En una arquitectura SDN, las *Southbound API* (*Application Program Interfaces*) se utilizan para comunicar el SDN Controller y los routers y switches de la red. Puede ser una solución abierta o propietaria. Las *Southbound API* proporcionan un control más eficiente sobre la red y permiten que el controlador SDN realice cambios de forma dinámica de acuerdo a las demandas y las necesidades en tiempo real.

OpenFlow es la primera y probablemente la más conocida interfaz *Southbound API*. Es un estándar desarrollado por ONF (*Open Networking Foundation*) que define la forma en que el controlador SDN debe interactuar con el plano de datos para realizar ajustes en la red para adaptarse a las necesidades cambiantes. El protocolo OpenFlow permite al controlador SDN administrar la estructura lógica de un switch, sin tener en cuenta los detalles de cómo el switch implementa la arquitectura lógica OpenFlow.

Con OpenFlow, las entradas en las tablas de flujo de los routers y switches se pueden agregar y quitar para hacer que la red responda mejor a las demandas de tráfico en tiempo real. Además de OpenFlow, Cisco OpFlex es también una *Southbound API* conocida.

En una arquitectura SDN, las *Northbound API* (*Application Program Interfaces*) se utilizan para comunicar el SDN Controller y los servicios y aplicaciones que se ejecutan en la red. Las *Northbound API* facilitan la innovación y permiten la organización, gestión y automatización de la red para ajustarse a las necesidades de las diferentes aplicaciones a través de la arquitectura SDN.

Las *Northbound API* son, posiblemente, las API más críticas en el medio SDN, ya que la importancia de la SDN está ligada a las aplicaciones que potencialmente pueden soportar y permitir. Debido a que son tan críticas, las *Northbound API* deben ser compatibles con una amplia variedad de aplicaciones, por lo que es posible que no quepan todas. Esto es posiblemente por qué las *Northbound API* sean el componente más complejo en un entorno SDN, debido a que existe una variedad de posibles interfaces en diferentes lugares de la pila para controlar diferentes tipos de aplicaciones a través de un controlador de SDN.

Las *Northbound API* también se utilizan para integrar el controlador SDN con herramientas de automatización remota, como Puppet, Chef, SaltStack, Ansible y CFEngine, así como plataformas de gestión, como OpenStack, VMware's vCloud-Director y de código abierto CloudStack. El objetivo es aislar el funcionamiento interno de la red, de modo que los desarrolladores de aplicaciones puedan hacer cambios para adaptarse a las necesidades de la aplicación sin tener necesidad de saber cómo funciona la red.

!!! tip "RECUERDE"
    La interfaz de programación de aplicaciones (API) es un mecanismo que permite que los componentes de software se comuniquen entre sí.

## Cisco SDA

Cisco SDA (*Software-Defined Access*) utiliza el modelo definido por software y varias API. Establece una forma completamente diferente de construir las redes de campus en comparación con los métodos tradicionales.

La arquitectura de SDA se compone básicamente de routers, switches, terminales, una interfaz gráfica (GUI) para los usuarios y un controlador DNA Center. SDA brinda un enfoque diferente a las redes WLAN y LAN y de cómo los terminales o puntos finales acceden a la red.

El modelo SDA se compone de tres partes o espacios necesarios:

- **Overlay:** es donde se crean los túneles VxLAN entre los switches SDA y que luego se utilizan para transportar el tráfico de un punto final a otro.
- **Underlay:** es la parte que contiene los dispositivos y conexiones para proporcionar conectividad IP a todos los nodos en la estructura, con el objetivo de admitir el descubrimiento dinámico de todos los dispositivos y puntos finales SDA como parte del proceso para crear túneles VxLAN superpuestos.
- **Fabric:** la combinación de overlay y underlay, que en conjunto proporcionan todas las características para entregar datos a través de la red con las características y atributos deseados.

Fabric, underlay y overlay se ubican del lado *southbound API*. Por diseño, en implementaciones SDN, la mayoría de las nuevas capacidades ocurren en el lado *northbound*.

Underlay proporciona conectividad entre los nodos en el entorno SDA con el fin de admitir túneles VxLAN en la red overlay. Para hacer eso, underlay incluye los switches, routers, cables y enlaces inalámbricos utilizados para crear la red física. También incluye la configuración y el funcionamiento de underlay para que pueda soportar el trabajo de la red overlay. Esto que parece un juego de palabras es muy fácil de comprender. Piense en capas, sin las capacidades de underlay, overlay no podría existir.

SDA se puede agregar a una LAN de campus existente, o crear una red SDA desde cero dentro de la red empresarial. La primera opción tiene algunos riesgos y restricciones, como interrupciones de tráfico que puedan afectar a la producción durante el proceso de migración.

Para elegir los dispositivos compatibles con SDA tiene que pensar en los roles que desempeñará cada uno:

- **Fabric edge node:** un switch que se conecta a dispositivos finales como los switches de acceso tradicionales.
- **Fabric border node:** un switch que se conecta a dispositivos fuera del control de SDA, por ejemplo, switches que se conectan a los routers WAN o a un centro de datos ACI.
- **Fabric control node:** un switch que realiza funciones especiales en el plano de control para LISP, este dispositivo requiere más CPU y memoria.

La secuencia de funcionamiento de SDA overlay es la siguiente. Primero, un punto final envía una trama que se entregará a través de la red SDA. El primer nodo SDA que recibe la trama la encapsula en un nuevo mensaje, utilizando un encabezado de túnel VxLAN, y reenvía la trama a través del túnel VxLAN, los otros nodos SDA que forman underlay reenvían la trama en función de cómo ha sido creado el túnel VxLAN. El último nodo SDA elimina el encabezado VxLAN, deja la trama original y la reenvía hacia el punto final de destino.

Todo este trabajo ocurre en modo ASIC de cada switch por lo que no hay penalización de rendimiento.

!!! note "NOTA"
    ASIC (*Application Specific Integrated Circuit*) es un circuito especializado de hardware diseñado para realizar una operación particular de manera altamente eficiente.

### Túneles VxLAN

SDA tiene muchas capacidades adicionales más allá de la simple entrega de mensajes, estas nuevas capacidades le permiten proporcionar funciones mejoradas. Con ese fin, SDA no solo enruta los paquetes IP o conmuta las tramas de Ethernet. Además, encapsula las tramas de enlace de datos entrantes a través de la red SDA con una tecnología de túnel llamada VxLAN (*Virtual Extensible LAN*). Algunas de las características de los túneles VxLAN pueden ser las siguientes:

- La encapsulación y desencapsulación en el túnel VxLAN debe ser realizada vía ASIC (*Application Specific Integrated Circuit*) en cada switch para que no haya penalización de rendimiento. Por lo tanto los switches deben tener necesariamente esa compatibilidad de hardware.
- La encapsulación VxLAN debe proporcionar los campos de encabezado que SDA necesita para sus características, por lo que el protocolo de tunelización debe ser flexible y extensible, a la vez que compatible con el hardware específico del switch.
- El proceso de tunelización necesita encapsular toda la trama de enlace de datos en lugar de encapsular el paquete IP. Eso permite que SDA admita funciones de reenvío de capa 2, así como funciones de reenvío de capa 3.

Estos objetivos se consiguen por medio del protocolo VxLAN que crea los túneles dentro de la red SDA encapsulando las tramas desde un terminal para ser enviadas a través del túnel. Para soportar el encapsulamiento VxLAN, underlay utiliza un direccionamiento IP diferente al de la red empresarial, sin embargo los túneles mantienen el mismo direccionamiento que el de la red de la empresa.

En la figura, la red empresarial tiene un direccionamiento `192.0.2.0/24`, mientras que los dispositivos underlay utilizan la `172.16.0.0/16`. El túnel overlay creado a través de los dos terminales fabric están dentro del mismo espacio de direccionamiento IP.

### LISP

LISP (*Locator/ID Separation Protocol*) se diseñó originalmente para disminuir las tablas de enrutamiento en internet. LISP está definido en la RFC 6830. Los switches de capa 2 aprenden los destinos de las tramas almacenando las direcciones MAC en tablas. Cuando llegan nuevas tramas el *Control Plane* del switch examina la tabla MAC en busca de coincidencias, agilizando la conmutación de capa 2. Los routers aprenden las direcciones IP de destino utilizando protocolos de enrutamiento y almacenando las rutas en tablas. Cuando llegan nuevos paquetes, el *Control Plane* de capa 3 intenta hacer coincidir la dirección IP de destino con alguna entrada en la tabla de enrutamiento IP.

LISP separa la ubicación y la identificación reemplazando las direcciones IP con RLOC (*Routing Locators*) y EID (*Endpoint Identifiers*). Los RLOC se asignan a los routers en función de la región para que puedan agregarse topológicamente. Los EID se asignan a puntos finales y no necesitan ser asignados topológicamente. Solo se puede acceder a los EID a través del RLOC en la frontera LISP donde se ubican. A diferencia del enrutamiento IP típico, los prefijos EID no se instalan en la tabla de enrutamiento. En cambio, LISP usa una base de datos EID-RLOC para localizar los EID y entregar los paquetes.

Los nodos frontera Fabric (por lo general switches) aprenden la ubicación de los posibles puntos finales utilizando los medios tradicionales, en función de su dirección MAC, dirección IP individual y por subred, identificando cada punto final con un EID. Estos reconocen el hecho de que pueden alcanzar un punto final (EID) consultando en una base de datos contenida en el servidor de tablas LISP. El servidor LISP mantiene la relación de los EID con los RLOC que identifican el nodo de borde fabric que puede alcanzar el EID. En adelante, cuando el *Data Plane* fabric necesite reenviar un mensaje, buscará y encontrará el destino en la base de datos del servidor de mapas LISP.

Básicamente el proceso LISP se describe en la siguiente figura:

PC1 envía una trama Ethernet al nodo borde SW1 con destino a PC2 pero el switch desconoce dónde reenviar la trama. SW1 consulta al servidor LISP por si conoce la dirección IP de PC2. El servidor consulta su tabla y encuentra una entrada creada anteriormente que mapea el EID con el RLOC de SW2. El servidor LISP contacta con SW2 para confirmar que la entrada en la tabla es correcta. SW2 completa el proceso informando a SW1 de que él puede llegar a PC2.

Ahora que SW1 sabe cómo llegar a PC2, encapsula la trama en un paquete IP y añade el encabezado VxLAN para ser enviado a través del túnel VxLAN.

!!! tip "RECUERDE"
    LISP funciona a nivel de *Control Plane*, mientras que VxLAN lo hace a nivel de *Data Plane*.

## Cisco DNA Center

Cisco DNA Center (*Digital Network Architecture*) es una aplicación que Cisco ofrece preinstalada en los dispositivos Cisco DNA Center Appliance. Funciona como controlador en una red SDA o como plataforma de administración para dispositivos de red tradicionales. DNA Center admite varias *southbound API* para que el controlador pueda comunicarse con los dispositivos que administra. Requiere varios protocolos para poder comunicarse con una amplia gama de dispositivos, por ejemplo: Telnet, SSH, SNMP o versiones más modernas como NETCONF, RESTCONF. También incluye una potente y robusta *northbound REST API*.

El modelo de seguridad basado en grupos SDA resuelve la problemática y los desafíos operativos con las ACL tradicionales. SDA y Cisco DNA logran esta característica particular al vincular la seguridad a grupos de usuarios, a los que se les asigna una etiqueta SGT (*Scalable Group Tag*). Luego, el administrador configura una política que identifica a los SGT que pueden enviar paquetes a otros SGT. Por lo tanto, una política de control de acceso basada en grupos tiene dos componentes principales:

- **Grupos escalables:** los SGT que comprenden una agrupación de usuarios, dispositivos terminales o recursos que comparten los mismos requisitos de control de acceso. Un grupo escalable puede contener tan solo un elemento (un usuario, un dispositivo de punto final o un recurso).
- **Reglas de acceso:** es un componente básico común que se utiliza tanto en las políticas de control de acceso basadas en IP como en grupos. Define las reglas que componen las políticas de control de acceso. Estas reglas especifican las acciones (permitir o denegar) realizadas cuando el tráfico coincide con un puerto o protocolo específico y las acciones implícitas (permitir o denegar) realizadas cuando ninguna otra regla coincide.

Los problemas con la administración de las ACL en cada dispositivo ya no representan complejidad con el modelo de seguridad grupal de SDA. Por ejemplo:

- El administrador puede considerar cada nuevo requisito de seguridad por separado, sin analizar una ACL existente generalmente larga y compleja.
- Cada nuevo requisito se puede considerar sin buscar todas las ACL en las rutas probables entre los puntos finales y analizar cada una de las ACL.
- DNA Center mantiene las políticas separadas, con espacio para guardar notas sobre el motivo de la política.
- Cada política puede eliminarse sin que afecte a la lógica de las otras políticas.

Para entender el funcionamiento de esta nueva característica de seguridad, piense cuando un terminal intenta enviar su primer paquete a un nuevo destino. El nodo SDA de ingreso inicia un proceso enviando mensajes al DNA Center. Luego, DNA Center trabaja con herramientas de seguridad en la red, como por ejemplo ISE (*Identity Services Engine*), para identificar a los usuarios y luego vincularlos con sus respectivos SGT. A continuación, DNA Center verifica la lógica configurada y si existe una acción de permiso entre el par de SGT de origen y destino, DNA Center dirige los nodos borde para crear el túnel VxLAN. Si en cambio las políticas de seguridad establecen que no se debe permitir el tráfico, DNA Center no dirige la estructura para crear el túnel y los paquetes se descartan.

!!! tip "RECUERDE"
    Cisco ISE (*Identity Services Engine*) es una plataforma que proporciona los servicios AAA necesarios para la autenticación, autorización y auditoría.

Un ejemplo típico de utilización de DNA Center como plataforma de gestión de red es el Cisco Prime Infrastructure. Una plataforma de gestión centralizada ofrece mejoras a la hora de administrar una red en comparación con la forma tradicional, dispositivo por dispositivo. Algunas de las ventajas y características de una gestión centralizada pueden ser:

- Permite administrar tanto la LAN cableada como la inalámbrica desde la misma plataforma de administración.
- Descubre dispositivos de red, crea un inventario y los organiza según la topología.
- Brinda soporte para las funciones tradicionales de administración de LAN, WAN y centros de datos empresariales.
- Utiliza SNMP, SSH y Telnet, así como CDP y LLDP, para descubrir y aprender información sobre los dispositivos en la red.
- Admite diferentes tareas para instalar un nuevo dispositivo, configurarlo para que funcione en producción y realiza seguimiento y monitorización continua y puede realizar cambios en cualquier momento.
- Administra imágenes de software y automatiza actualizaciones.
- Simplifica la implementación de la configuración de QoS en cada dispositivo.
- Utiliza funciones Plug-and-Play para la instalación inicial de nuevos dispositivos de red después de instalar físicamente el nuevo dispositivo, conectar un cable de red y encender.

### REST

Para automatizar y programar redes de forma centralizada, los softwares de automatización deben realizar varias tareas. El software analiza los datos en forma de variables, toma decisiones basadas en ese análisis y luego puede tomar medidas para cambiar la configuración de los dispositivos de red o informar sobre el estado de la red.

Las diferentes funciones de automatización residen en diferentes dispositivos: el terminal del administrador, un servidor, un controlador y los distintos dispositivos de red. Para que estos procesos de automatización interrelacionados funcionen correctamente, necesitan convenciones de software bien definidas para permitir una comunicación ágil entre los componentes de software.

Típicamente las API (*Application Programming Interface*) crean una forma para que las aplicaciones de software se comuniquen entre sí. Los requisitos del examen CCNA se basan en un tipo de API, las API REST (*REpresentational State Transfer*) por ser una de las más populares y utilizadas para la automatización de redes. Por otro lado, JSON (*JavaScript Object Notation*) es la convención estándar para el intercambio de variables de datos a través de API.

En definitiva, REST proporciona un método estándar para que dos programas de automatización puedan comunicarse a través de una red y JSON define cómo comunicar las variables utilizadas por esos programas.

Las API REST siguen un conjunto de reglas fundamentales sobre qué pueden hacer o no. Básicamente estas reglas se corresponden con las siguientes características:

- **Cliente-servidor:** esta condición mantiene al cliente y al servidor mínimamente vinculados. Esto quiere decir que el cliente no necesita conocer los detalles de implementación del servidor y el servidor se despreocupa de cómo son usados los datos que envía al cliente.
- **Sin estado (Stateless):** cada petición que recibe el servidor debería ser independiente, es decir, no es necesario mantener sesiones.
- **Cacheable:** debe admitir un sistema de almacenamiento en caché. La infraestructura de red debe soportar una caché de varios niveles. Este almacenamiento evitará repetir varias conexiones entre el servidor y el cliente para recuperar un mismo recurso.
- **Interfaz uniforme:** define una interfaz genérica para administrar cada interacción que se produzca entre el cliente y el servidor de manera uniforme, lo cual simplifica y separa la arquitectura. Esta restricción indica que cada recurso del servicio REST debe tener una única dirección URI (*Uniform Resource Identifier*).
- **Sistema de capas:** el servidor puede disponer de varias capas para su implementación. Esto ayuda a mejorar la escalabilidad, el rendimiento y la seguridad.

A menudo las siglas URI y URL se utilizan como sinónimos, sin embargo son términos diferentes. Una URL (*Uniform Resource Locator*) se utiliza principalmente para apuntar a una dirección de internet, a un componente de una página web o a un programa en una página web a través de algún protocolo como HTTP, FTP, SSH, FILE, etc., para acceder a la ubicación del recurso. Por otro lado, URI (*Uniform Resource Identifier*) se utiliza para distinguir un recurso de otro independientemente del método utilizado.

Los diseñadores de las API basadas en REST a menudo eligen HTTP (*Hypertext Transfer Protocol*) porque la lógica de HTTP coincide con algunos de los conceptos definidos de manera general para las API REST. HTTP utiliza los mismos principios que REST: funciona con un modelo cliente-servidor; utiliza un modelo operacional sin estado; e incluye encabezados que marcan claramente los objetos como almacenables en caché o no almacenables. También incluye verbos que coinciden con el funcionamiento de las aplicaciones.

Los verbos en HTTP (*HTTP verbs*) definen la acción que se quiere realizar sobre el recurso:

- **Get:** solicita una representación de un recurso específico.
- **Head:** solicita una respuesta idéntica a la de una petición GET, pero sin el cuerpo de la respuesta.
- **Post:** se utiliza para enviar una entidad a un recurso en específico, causando a menudo un cambio en el estado o efectos secundarios en el servidor.
- **Put:** reemplaza todas las representaciones actuales del recurso de destino con la carga útil de la petición.
- **Connect:** establece un túnel hacia el servidor identificado por el recurso.
- **Options:** se utiliza para describir las opciones de comunicación para el recurso de destino.
- **Trace:** realiza una prueba de bucle de retorno de mensaje a lo largo de la ruta al recurso de destino.
- **Patch:** es utilizado para aplicar modificaciones parciales a un recurso.
- **Delete:** borra un recurso en específico.

Además de utilizar los verbos HTTP para realizar las funciones CRUD (*Create, Read, Update, Delete*), REST usa las URI para identificar en qué recurso actúa la solicitud HTTP. Para las API REST, el recurso puede ser cualquiera de los muchos recursos definidos por la API.

El acrónimo CRUD (*Create, Read, Update, Delete*) identifica las cuatro acciones principales realizadas por una aplicación:

- **Create:** permite al cliente crear algunas instancias nuevas de variables y estructuras de datos en el servidor e inicializar sus valores tal como se mantienen en el servidor.
- **Read:** permite al cliente recuperar el valor actual de las variables que existen en el servidor, almacenando una copia de las variables, estructuras y valores en el cliente.
- **Update:** permite al cliente cambiar o actualizar el valor de las variables que existen en el servidor.
- **Delete:** permite al cliente eliminar del servidor diferentes instancias de variables de datos.

Cada recurso contiene un conjunto de variables relacionadas, definidas por la API e identificadas por una URI. La estructura URI para una solicitud REST GET consta de tres componentes. Por ejemplo, el URI solicita al Cisco DNA Center una lista de todos los dispositivos conocidos, y Cisco DNA Center devuelve un diccionario de valores para cada dispositivo.

- **Protocolo:** el término antes de `://` identifica el protocolo, en este caso, HTTPS.
- **Nombre de host o dirección IP:** este valor se encuentra entre la doble barra y la siguiente simple (`//` y `/`), e identifica el host; si usa un nombre de host, el cliente REST debe realizar una resolución de nombre para conocer la dirección IP del servidor REST.
- **Ruta o Recurso:** este valor se encuentra después de la primera barra simple (`/`) y termina al final del URI o antes de cualquier campo adicional (como un campo de consulta de parámetros). HTTP llama a este campo la ruta, pero para su uso con REST, el campo identifica de forma exclusiva el recurso tal como lo define la API.

Muchos de los mensajes de solicitud HTTP necesitan pasar información al servidor REST más allá de la API. Algunos de esos datos se pueden pasar en campos de encabezado; por ejemplo, las API REST usan campos de encabezado HTTP para codificar gran parte de la información de autenticación para las llamadas REST. Además, los parámetros relacionados con una llamada REST se pueden pasar como parámetros como parte del URI.

Siguiendo el ejemplo de la URI anterior, es posible que se requiera ese diccionario de valores para un solo dispositivo. La API de Cisco DNA Center lo permite añadiendo el parámetro al final del URI.

!!! note "NOTA"
    Para información más detallada sobre las API REST puede consultar la página de su creador Roy Fielding en <https://restfulapi.net>.

La interfaz de programación API es un mecanismo de software que puede resultar muy complejo y tedioso. De manera personal considero que es materia de estudio para desarrolladores de software y no para un técnico administrador de redes CCNA, sin embargo es una exigencia para los administradores actuales y es, además, tema de examen, por lo que hay que darle la importancia necesaria. Para los estudiantes que quieran profundizar en las API, existe una aplicación llamada Postman que es gratuita y se puede descargar desde su web en <https://www.postman.co>. Tenga en cuenta que Cisco hace un uso extensivo de Postman (por ejemplo Cisco DevNet) en sus laboratorios y ejemplos.

### JSON

JSON (*JavaScript Object Notation*) está incluido en el temario de la certificación CCNA 200-301, los siguientes párrafos describen el funcionamiento de este formato para intercambio de datos.

Los lenguajes de serialización de datos brindan una forma de representar variables con texto en lugar de en la representación interna utilizada por cualquier lenguaje de programación en particular.

Cada lenguaje de serialización de datos permite que los servidores API devuelvan datos para que el cliente API pueda replicar los mismos nombres de variables, así como las estructuras de datos que se encuentran en el servidor API.

Para describir las estructuras de datos, los lenguajes de serialización de datos incluyen caracteres especiales y convenciones que comunican ideas sobre variables de lista, variables de diccionario y otras estructuras de datos más complejas.

Los lenguajes de serialización de datos permiten superar estos problemas, ofreciendo a las aplicaciones un método estándar para representar variables para la transmisión y el almacenamiento de esas variables fuera del programa.

El flujo del proceso de serialización de datos es el siguiente:

1. El servidor recopila los datos representados internamente y los entrega al código API.
2. La API convierte la representación interna en un modelo de datos que representa esas variables (con JSON, por ejemplo).
3. El servidor envía el modelo de datos en formato JSON a través de mensajes a través de la red.
4. El cliente REST toma los datos recibidos y convierte los datos con formato JSON en variables en el formato nativo de la aplicación cliente.

El siguiente cuadro describe algunos lenguajes de serialización:

| Acrónimo | Nombre | Referencia | Propósito | Utilización |
| --- | --- | --- | --- | --- |
| JSON | JavaScript Object Notation | JavaScript (JS) language; RFC 8259 | Modelado general de datos y serialización | REST API |
| XML | eXtensible Markup Language | World Wide Web Consortium (W3C.org) | Lenguaje de marcado de propósito general | REST API, Páginas Web |
| YAML | YAML Ain't Markup Language | YAML.org | Modelado general de datos | Ansible |

Básicamente JSON es un fichero de texto guardado con la extensión `.json` que luego será utilizado por alguna aplicación para el intercambio de datos. Leerlo y escribirlo es simple para humanos, mientras que para las máquinas es simple interpretarlo y generarlo. JSON es un formato de texto que es completamente independiente del lenguaje pero utiliza convenciones que son ampliamente conocidas por los programadores. Estas propiedades hacen que JSON sea un lenguaje ideal para el intercambio de datos.

Las reglas sintácticas de JSON son bastante sencillas:

- **matrices (arrays):** son listas de valores separados por comas. Las matrices se escriben entre corchetes `[ ]`.

    ```text
    [1, "router", "CPD_Norte"]
    ```

- **objetos (objects):** son listas de parejas nombre-valor. El nombre y el valor están separados por dos puntos `:` y las parejas están separadas por comas. Los objetos se escriben entre llaves `{ }` y los nombres de las parejas se escriben siempre entre comillas dobles `"texto"`. Si el valor es numérico no se escribe entre comillas.

    ```text
    {"nombre": "CPD_Norte", "rack": 12, "administrable": true}
    ```

Los valores (tanto en los objetos como en las matrices) pueden ser:

- **números:** enteros, decimales o en notación exponencial. El separador decimal es el punto.
- **cadenas:** se escriben entre comillas dobles. Los caracteres especiales y los valores *unicode* se escriben con una contra barra `\` delante, por ejemplo las comillas se escriben `\"`.
- **booleanos y nulos:** los valores booleanos `true`, `false` y los tipos de datos `null` se escriben sin comillas.

Dentro de los objetos y matrices puede haber tanto objetos como matrices o ambos, sin límites.

Los ficheros JSON no pueden contener comentarios. Los espacios en blanco y los saltos de línea no son significativos, es decir, puede haber cualquier número de espacios en blanco o saltos de línea separando cualquier elemento o símbolo del documento. El siguiente ejemplo muestra una matriz con dos objetos.

### Herramientas de gestión

En capítulos anteriores se ha visto, expuesto e incluso se han dado casos prácticos de cómo configurar dispositivos de red, sin embargo en una red de producción las configuraciones manuales pueden ser un desafío. A medida que una empresa crece, migran dispositivos o cambia de administrador, los cambios de configuración son mayores, por lo tanto la gestión manual se convierte en un problema.

El proceso de configuración manual no registra el historial de cambios:

- qué líneas cambiaron
- qué cambió en cada línea
- qué configuración anterior se eliminó
- quién cambió la configuración
- cuándo se realizó cada cambio

Algunos sistemas externos de gestión de sistemas, como la emisión de tickets de problemas y el software de gestión de cambios, pueden registrar detalles, pero únicamente para los dispositivos que se encuentran dentro de su gestión. Sin embargo, los dispositivos que se encuentran fuera de esa gestión y requieren un análisis para descubrir qué cambios han sufrido, también dependen de los administradores para seguir los procesos operativos de manera consistente y correcta.

Con un sistema de control centralizado un equipo de red puede hacer un trabajo mucho más efectivo para rastrear los cambios y responder a quién, qué y cuándo cambió la configuración de cada dispositivo. Con este nuevo modelo, los administradores deben realizar cambios editando los archivos de configuración, lo que presenta otros desafíos que pueden resolverse mejor utilizando alguna herramienta de administración de configuración automatizada.

Por ejemplo, una empresa puede tener muchos routers cumpliendo funciones similares con una configuración casi idéntica. Las herramientas de administración de configuración pueden separar los componentes de una configuración en las partes en común para todos los dispositivos en ese rol (la plantilla) frente a las partes exclusivas de cualquier dispositivo (las variables).

```text
hostname Norte
!
interface GigabitEthernet0/1
 ip address 10.99.170.10 255.255.255.0
!
interface GigabitEthernet0/2
 ip address 10.99.170.11 255.255.255.0
!
ntp server 10.99.52.23
```

La siguiente plantilla imita la configuración anterior, excepto por colocar nombres de variables dentro de las llaves dobles.

```text
hostname {{nombre}}
!
interface GigabitEthernet0/1
 ip address {{direccion_1}} {{mascara_1}}
!
interface GigabitEthernet0/2
 ip address {{direccion_2}} {{mascara_2}}
!
ntp server {{ntp_server}}
```

El sistema de gestión de la configuración procesa una plantilla más todas las variables relacionadas para producir la configuración prevista para un dispositivo. El administrador crea y edita posteriormente un archivo de plantilla y luego un archivo con las variables para cada router.

```yaml
hostname: Norte
direccion_1: 10.99.170.10
mascara_1: 255.255.255.0
direccion_2: 10.99.170.11
mascara_2: 255.255.255.0
ntp_server: 10.99.52.23
```

Puede parecer un trabajo añadido separar las configuraciones en una plantilla y luego cargar las variables, sin embargo las plantillas aumentan el enfoque al tener una configuración estándar para cada rol. Los nuevos dispositivos con un rol existente se pueden implementar fácilmente simplemente copiando un archivo variable existente por dispositivo y cambiando los valores.

Ansible, Puppet y Chef son diferentes paquetes de software con opciones gratuitas que le permiten descargar y aprender sobre las herramientas. También puede comprar cada herramienta, que incluyen variaciones más específicas sobre las funcionalidades de cada una.

Para usar **Ansible**, puede instalarse en algún ordenador: Mac, Linux o en una máquina virtual de Linux en un PC con Windows. Puede usar la versión gratuita de código abierto o la versión de pago Ansible Tower.

Una vez que está instalado, crea varios archivos de texto, como los siguientes:

- **Playbooks:** estos archivos proporcionan acciones y lógica sobre lo que debe hacer Ansible.
- **Inventario:** estos archivos proporcionan nombres de host del dispositivo junto con información sobre cada dispositivo, como roles de dispositivo, por lo que Ansible puede realizar funciones para subconjuntos del inventario.
- **Plantillas:** con el lenguaje Jinja2, las plantillas representan la configuración de un dispositivo pero con variables.
- **Variables:** con YAML, un archivo puede enumerar variables que Ansible sustituirá en plantillas.

Ansible no depende de ningún código o agente que se ejecute en el dispositivo de red. En cambio, Ansible se basa en las características típicas de los dispositivos de red, como SSH o NETCONF, para realizar cambios y extraer información. Cuando se usa SSH, el nodo de control Ansible realmente realiza cambios en el dispositivo como lo haría cualquier otro usuario SSH, pero haciendo el trabajo con el código Ansible.

!!! note "NOTA"
    Jinja es un motor de plantillas web para el lenguaje de programación Python.

Para usar **Puppet**, comienza instalándolo en un host Linux. Puede instalarlo en su propio host, pero para fines de producción, normalmente se instala en un servidor Linux llamado Puppet Master. Al igual que con Ansible, puede usar la versión gratuita de código abierto pero también existen versiones de pago.

Una vez instalado, Puppet también utiliza varios archivos de texto importantes con diferentes componentes, como los siguientes:

- **Manifiesto:** este es un archivo de texto legible para humanos en Puppet Master, que utiliza un lenguaje definido por Puppet, y que se utiliza para definir el estado de configuración deseado de un dispositivo.
- **Módulo, recurso, clase:** estos términos se refieren a elementos del manifiesto, el módulo es el componente más grande compuesto por clases más pequeñas, que a su vez están compuestas de recursos.
- **Plantillas:** al usar un lenguaje específico de dominio de Puppet, estos archivos le permiten a Puppet generar manifiestos (y módulos, clases y recursos) mediante la sustitución de variables en la plantilla.

Una forma de pensar sobre las diferencias entre el enfoque de Ansible y el de Puppet es que los Playbooks de Ansible usan un lenguaje imperativo, mientras que Puppet usa un lenguaje declarativo. Es decir, con Ansible, los Playbooks enumerarán tareas y elecciones basadas en esos resultados, mientras que los manifiestos de Puppet declaran el estado final que debe tener un dispositivo. Por ejemplo, el mecanismo de Ansible sería "configurar todos los routers, en todos los edificios, si se producen errores realice las acciones que correspondan". Puppet en cambio declara "el router debe tener este estado de configuración".

No todos los sistemas operativos de Cisco son compatibles con los agentes Puppet, por lo que Puppet resuelve ese problema utilizando un agente *proxy* que se ejecuta en algún host externo. El agente externo luego usa SSH para comunicarse con el dispositivo de red.

Para usar **Chef**, al igual que Ansible y Puppet, es un paquete de software que se instala y ejecuta. Chef Automate es el producto al que la mayoría de la gente se refiere simplemente como Chef. Al igual que con Puppet, en producción probablemente se ejecute en modo servidor-cliente con un servidor y con varias estaciones de trabajo. Sin embargo, también puede ejecutar Chef Zero en modo independiente, lo cual es útil cuando recién comienza y aprende en el laboratorio.

Una vez que Chef está instalado, crea varios archivos de texto con diferentes componentes, como los siguientes:

- **Recurso:** los objetos de configuración cuyo estado es administrado por Chef, análogo a los ingredientes en una receta en un libro de cocina.
- **Receta:** la lógica del Chef se aplica a los recursos para determinar cuándo, cómo y si actuar contra los recursos, de forma análoga a una receta en un libro de cocina.
- **Cookbooks:** un conjunto de recetas sobre los mismos tipos de trabajo, agrupados para facilitar la gestión y el intercambio.
- **Runlist:** una lista ordenada de recetas que se deben ejecutar en un dispositivo determinado.

Chef usa una arquitectura similar a Puppet. Para los dispositivos de red, cada cliente Chef ejecuta un agente. El agente realiza la supervisión de la configuración en el sentido de que el cliente extrae recetas y recursos del servidor Chef y luego ajusta su configuración para mantenerse sincronizado con los detalles en esas recetas y listas de ejecución. Sin embargo, tenga en cuenta que muchos dispositivos Cisco no son compatibles con un cliente Chef, por lo que es probable que vea un mayor uso de Ansible y Puppet para la administración de la configuración de un dispositivo Cisco.

Ansible puede describirse como el uso de un modelo *push* en lugar de un modelo *pull* como Puppet y Chef. *Push* significa que un "servidor maestro" se conecta a través de SSH a los nodos que quiere administrar y hace lo que se presume que debe hacer. Muchas veces este método resulta un cuello de botella si existen muchos nodos simultáneos que intentan conectarse al servidor. Por otro lado, en las redes donde no es posible este tipo de despliegue por estar altamente protegidas, se utiliza el modo *pull*, donde un nodo se conecta a un servidor maestro para obtener instrucciones sobre qué hacer.

!!! note "NOTA"
    Para mayor información puede consultar las webs de los fabricantes en <https://www.ansible.com>, <https://www.puppet.com> y <https://www.chef.io>.

## Cisco ACI

Cisco ha desarrollado ACI (*Application Centric Infrastructure*) para ayudar a las organizaciones que no tienen necesidad o la habilidad para programar el uso de herramientas SDN, para automatizar la red. Cisco ACI es una solución de hardware especialmente diseñada para integrar los servicios en la nube y la gestión del centro de datos. La política de la red se elimina del plano de datos, simplificando la forma de crear y administrar las redes de datos.

La implementación de Cisco ACI puede desarrollarse en una topología de dos niveles tipo *spine-leaf* (también llamada *Clos network*) de la siguiente manera:

- En una topología spine-leaf Cisco ACI se compone del APIC (*Cisco Application Policy Infrastructure Control*) y de switches de la serie Cisco Nexus 9000.
- Los switches de la capa *leaf* se conectan con los de la capa *spine*, pero nunca entre ellos.
- Del mismo modo los switches de la capa *spine* se conectan con los de la capa *leaf*, pero nunca entre ellos.
- En esta topología de dos niveles los dispositivos están a un salto de los demás.
- Los puntos finales se conectan solo a los switches de capa *leaf*.
- Los puntos finales pueden ser también conexiones a routers que se comunican con dispositivos fuera del centro de datos. Por necesidad y volumen, la mayoría de los puntos finales serán servidores físicos que ejecutan un sistema operativo nativo o servidores que ejecutan software de virtualización con un número de máquinas virtuales y contenedores.

## Cisco APIC-EM

Cisco APIC-EM (*Cisco Application Policy Infrastructure Control Enterprise Module*) es un SDN basado en políticas, brinda una solución más robusta, que prevé un mecanismo simple para controlar y gestionar las políticas en toda la red.

APIC-EM ofrece SDN a las redes corporativas, WAN, redes de campus y de acceso. APIC-EM proporciona la automatización centralizada de perfiles de aplicación basados en políticas. A través de programación y control de red automatizada ayuda a responder rápidamente a gestiones de red.

Cisco APIC-EM ofrece las siguientes características:

- Descubrimiento de dispositivos.
- Inventario de dispositivos.
- Inventario de hosts.
- Topología.
- Políticas.
- Análisis de políticas.

### Análisis de ACL con APIC-EM

Con APIC-EM es posible examinar las ACL en los dispositivos en busca de redundancias, conflictos o contradicciones como por ejemplo entradas mal ubicadas o en un orden incorrecto que permitan un host y que luego lo denieguen (*shadowed*). Permite inspeccionar y analizar las ACL a través de toda la red, dejando al descubierto los problemas y conflictos. Examina ACL específicas en la ruta entre dos nodos finales, descubriendo los posibles problemas.

## Fundamentos para el examen

Este capítulo puede resultar bastante abstracto si no se tienen dispositivos para realizar pruebas de laboratorio. Piense en la tendencia de las empresas en la utilización de un sistema de gestión centralizada, donde cientos de dispositivos se gestionan y administran remotamente. Por ejemplo, un router con una configuración mínima se conecta a la red y obtiene la configuración completa automáticamente y se pone en producción casi al instante.

- Recuerde las diferencias entre el plano de control y el plano de datos.
- Analice para qué sirven y para qué se utilizan las *Southbound API* y *Northbound API*.
- Compare la administración tradicional de una red de campus con una administración centralizada.
- Estudie las partes que componen el modelo SDA y cómo se forman los túneles VxLAN.
- Analice cómo aprenden las ubicaciones de los dispositivos los nodos frontera.
- Piense y analice las ventajas que ofrece Cisco DNA Center.
- Analice el mecanismo que emplean las API para comunicarse entre sí y cómo se definen las variables que utilizan.
- Tenga en claro las diferencias entre URL y URI.
- Realice prácticas a través de la web <https://www.postman.co>.
- Aprenda qué son y cómo funcionan los lenguajes de serialización.
- Estudie las demás opciones de gestión centralizada de red.
