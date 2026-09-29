# Seguridad

## Principios de seguridad

Mantener una red protegida garantiza la seguridad de la red y de los usuarios y salvaguarda los intereses comerciales de la empresa. Esto requiere vigilancia de parte de los profesionales de seguridad en redes, quienes deberán estar constantemente al tanto de las nuevas y evolucionadas amenazas y ataques a las redes, así como también de las vulnerabilidades de los dispositivos y aplicaciones. La mayor motivación de la seguridad en redes es el esfuerzo por mantenerse un paso más adelante de los intereses malintencionados.

Además de encargarse de las amenazas que provienen de fuera de la red, los profesionales de redes deben también estar preparados para amenazas que provengan desde dentro de la misma. Las amenazas internas, ya sean intencionales o accidentales, pueden causar aún más daño que las amenazas externas, por el acceso directo y conocimiento de la red y datos corporativos.

Las principales vulnerabilidades de los dispositivos finales son los ataques de virus, gusanos y troyanos.

### Virus

Un virus informático es un programa que tiene por objeto alterar el normal funcionamiento del ordenador sin el permiso o el conocimiento del usuario. Los virus, habitualmente, reemplazan archivos ejecutables por otros infectados con el código de este. Los virus pueden destruir, de manera intencionada, los datos almacenados en un ordenador, aunque también existen otros más inofensivos, que solo se caracterizan por ser molestos.

Los virus informáticos tienen, básicamente, la función de propagarse a través de un software, no se replican a sí mismos, son muy nocivos y algunos contienen además una carga dañina con distintos objetivos, desde una simple broma hasta realizar daños importantes en los sistemas o bloquear las redes informáticas generando tráfico inútil.

El funcionamiento de un virus informático es conceptualmente simple. Se ejecuta un programa que está infectado, en la mayoría de las ocasiones por desconocimiento del usuario. El código del virus queda alojado en el ordenador, aun cuando el programa que lo contenía haya terminado de ejecutarse. El virus toma entonces el control de los servicios básicos del sistema operativo, infectando, de manera posterior, archivos ejecutables que sean llamados para su ejecución. Finalmente, se añade el código del virus al programa infectado y se graba en el disco duro, con lo cual el proceso de replicado se completa.

### Gusanos

Un gusano (*Worm*) es un programa que tiene la propiedad de duplicarse a sí mismo. Los gusanos utilizan las partes automáticas de un sistema operativo que generalmente son invisibles al usuario.

A diferencia de un virus, un gusano no precisa alterar los archivos de programas, sino que reside en la memoria y se duplica a sí mismo. Los gusanos casi siempre causan problemas en la red (aunque sea simplemente consumiendo ancho de banda), mientras que los virus siempre infectan o corrompen los archivos del ordenador que atacan. Mientras que los virus requieren un programa huésped para ejecutarse, los gusanos pueden ejecutarse solos.

Es algo usual detectar la presencia de gusanos en un sistema cuando, debido a su incontrolada replicación, los recursos del sistema se consumen hasta el punto de que las tareas ordinarias del mismo son excesivamente lentas o simplemente no pueden ejecutarse.

Los gusanos se basan en una red de ordenadores para enviar copias de sí mismos a otros terminales en la red y son capaces de llevar esto a cabo sin intervención del usuario, propagándose utilizando Internet, basándose en diversos métodos, como SMTP, IRC o P2P, entre otros.

### Troyanos

En informática se denomina troyano a un programa malicioso que se presenta al usuario como un software aparentemente legítimo e inofensivo, pero que al ejecutarlo ocasiona daños.

Los troyanos pueden realizar diferentes tareas, pero en la mayoría de los casos crean una puerta trasera que permite la administración remota a un usuario no autorizado. Un troyano no es estrictamente un virus informático y la principal diferencia es que los troyanos no propagan la infección a otros sistemas por sí mismos.

Los troyanos están diseñados para permitir a un individuo el acceso remoto a un sistema. Una vez ejecutado el troyano, el individuo puede acceder al sistema de forma remota y realizar diferentes acciones sin necesitar permiso. Las acciones que el individuo puede realizar en el equipo remoto dependen de los privilegios que tenga el usuario en el ordenador remoto y de las características del troyano.

### Mitigación de virus, gusanos y troyanos

El principal recurso para la mitigación de ataques de virus y troyanos es el software antivirus. El software antivirus y los programas antimalware ayudan a prevenir que los hosts sean infectados y así poder diseminar código malicioso. Requiere mucho más tiempo limpiar ordenadores infectados que mantener al software antivirus actualizado en los propios terminales.

Concienciar y capacitar a los usuarios finales para que sean conscientes de la necesidad de la confidencialidad de los datos personales y corporativos. Deben estar entrenados para actuar ante posibles amenazas con procedimientos y políticas de seguridad ante la pérdida de datos. Esto también implica que la empresa debe desarrollar y publicar políticas de seguridad formales para que sigan sus empleados, usuarios y socios comerciales.

La mayoría de las vulnerabilidades descubiertas en el software tienen relación con el desbordamiento del buffer. Un buffer es un área de la memoria utilizada por los procesos para almacenar datos temporariamente. Un desbordamiento en el buffer ocurre cuando un buffer de longitud fija llena su capacidad y un proceso intenta almacenar datos más allá de ese límite máximo. Esto puede dar por resultado que los datos extra sobrescriban localizaciones de memoria adyacentes o causen otros comportamientos inesperados. Los desbordamientos de buffer son generalmente el conducto principal a través del cual los virus, gusanos y troyanos hacen daño.

Los gusanos dependen más de la red que los virus. La mitigación de gusanos requiere diligencia y coordinación por parte de los profesionales de la seguridad en redes. La respuesta a una infección de un gusano puede separarse en cuatro fases:

- **Fase de contención:** consiste en limitar la difusión de la infección del gusano de áreas de la red que ya están infectadas. La contención requiere el uso de ACL y firewalls.
- **Fase de inoculación:** durante la fase de inoculación todos los sistemas no infectados reciben un parche del vendedor apropiado para la vulnerabilidad.
- **Fase de cuarentena:** incluye el rastreo y la identificación de máquinas infectadas dentro de las áreas contenidas y su desconexión, bloqueo o eliminación.
- **Fase de tratamiento:** consiste en terminar el proceso del gusano, eliminar archivos modificados o configuraciones del sistema que el gusano haya introducido e instalar un parche para la vulnerabilidad que el gusano usaba para explotar el sistema.

Los virus, gusanos y troyanos pueden hacer lentas a las redes o detenerlas completamente y corromper o destruir datos. Hay opciones de hardware y software disponibles para mitigar estas amenazas.

## Seguridad en la red

Una de las principales premisas a tomar en cuenta en la protección de una red son las ubicaciones de infraestructura, como armarios de red y centros de datos, que deben permanecer bloqueadas de forma segura. El acceso con credenciales a ubicaciones confidenciales es una solución escalable que ofrece una pista de auditoría de identidades y marcas de tiempo cuando se otorga el acceso. Actualmente las credenciales biométricas elevan los mecanismos de acceso aún más lejos al proporcionar un factor que representa al usuario en "algo que es". El fundamento es utilizar algún atributo físico del cuerpo de un usuario para identificar de manera única a esa persona. Por ejemplo, la huella digital se puede escanear y usar como factor de autenticación.

La mayoría de las amenazas desde dentro de la red revelan los protocolos y tecnologías utilizados en la red de área local o la infraestructura conmutada. Estas amenazas internas caen, básicamente, en dos categorías: falsificación y DoS.

- **Ataques de falsificación:** son ataques en los que un dispositivo intenta hacerse pasar por otro falsificando datos. Por ejemplo, la falsificación de direcciones MAC ocurre cuando un ordenador envía paquetes de datos cuya dirección MAC corresponde a otro ordenador. Como este, existen otros tipos de ataques de falsificación.
- **Ataques de DoS** (*Denial of Service*): hacen que los recursos de un ordenador no estén disponibles para los usuarios a los que estaban destinados. Los hackers usan varios métodos para lanzar ataques de DoS.

Además de prevenir y denegar tráfico malicioso, la seguridad en redes también requiere que los datos se mantengan protegidos. La criptografía, el estudio y práctica de ocultar información, es ampliamente utilizada en la seguridad de las redes modernas. Hoy en día, cada tipo de comunicación de red tiene un protocolo o tecnología correspondiente, diseñado para ocultar esa comunicación de cualquier otro que no sea el usuario al que está destinada. Los datos inalámbricos pueden ser cifrados utilizando varias aplicaciones de criptografía. Se puede cifrar una conversación entre dos usuarios de teléfonos IP y también pueden ocultarse con criptografía los archivos de un ordenador. La criptografía puede ser utilizada en casi cualquier comunicación de datos. De hecho, la tendencia apunta a que todas las comunicaciones sean cifradas.

Los tres objetivos principales de la seguridad de la red son:

- Confidencialidad
- Integridad
- Disponibilidad

La criptografía asegura la confidencialidad de los datos. La seguridad de la información comprende la protección de la información y de los sistemas de información de acceso, uso, revelación, interrupción, modificación o destrucción no autorizados. El cifrado provee confidencialidad al ocultar los datos que van en texto plano.

Algunos ejemplos para proporcionar confidencialidad a la red pueden ser:

- Utilizar los mecanismos de seguridad de red como por ejemplo, los firewalls y las listas de control de acceso.
- Exigir credenciales apropiadas por ejemplo, nombres de usuario y contraseñas, para acceder a los recursos de red específicos.
- Cifrar todo el tráfico de manera que un atacante no pueda descifrar el tráfico que se apropió de la red.

La integridad de datos asegura que estos no han sido modificados en tránsito. La integridad de datos podría realizar la autenticación de origen para verificar que el tráfico se origina en la fuente que realmente lo envió. Algunos ejemplos de violaciones de integridad incluyen:

- Modificar la apariencia de una página web corporativa.
- Interceptar y alterar una transacción de comercio electrónico.
- Modificación de los registros financieros almacenados electrónicamente.

La disponibilidad de datos es una forma de medición de la accesibilidad a los datos o recursos. Por ejemplo, si un servidor no está disponible cinco minutos al año, tendría una disponibilidad del 99,999 %. Algunos ejemplos de cómo un atacante podría intentar poner en peligro la disponibilidad de una red son:

- Enviar incorrectamente datos formateados a un dispositivo conectado en red, dando como resultado un error de excepción no controlada.
- Inundar un sistema de red con una cantidad excesiva de tráfico o de solicitudes. Esto consumiría los recursos del sistema de procesamiento y evitaría que el sistema respondiese a las solicitudes legítimas (ataque de denegación de servicio DoS).

Hay varios tipos diferentes de ataques de red que no son virus, gusanos o troyanos. Para mitigar los ataques es útil tener a los diferentes tipos de ataques categorizados. Al categorizarlos es posible abordar tipos de ataques en lugar de ataques individuales. No hay un estándar sobre cómo categorizar los ataques de red. El método utilizado en este caso clasifica los ataques en tres categorías principales.

### Ataques de reconocimiento

Los ataques de reconocimiento consisten en el descubrimiento y mapeo de sistemas, servicios o vulnerabilidades sin autorización. Los ataques de reconocimiento muchas veces emplean el uso de sniffers de paquetes y escáneres de puertos, los cuales están ampliamente disponibles para su descarga gratuita en Internet. El reconocimiento es análogo a un ladrón vigilando un vecindario en busca de casas vulnerables para robar, como una residencia sin ocupantes o una casa con puertas o ventanas fáciles de abrir.

Los ataques de reconocimiento son generalmente precursores de ataques posteriores con la intención de ganar acceso no autorizado a una red o interrumpir el funcionamiento de la misma.

Los ataques de reconocimiento utilizan varias herramientas para ganar acceso a una red:

- **Sniffers de paquetes:** es una aplicación de software que utiliza una tarjeta de red en modo promiscuo para capturar todos los paquetes de red que se transmitan a través de una LAN.
- **Barridos de ping:** es una técnica de escaneo de redes básica que determina qué rango de direcciones IP corresponde a los hosts activos.
- **Escaneo de puertos:** escaneo de un rango de números de puerto TCP o UDP en un host para detectar servicios abiertos.
- **Búsquedas de información en Internet:** pueden revelar información sobre quién es el dueño de un dominio particular y qué direcciones han sido asignadas a ese dominio.

### Ataques de acceso

Los ataques de acceso explotan vulnerabilidades conocidas en servicios de autenticación, FTP y web, para ganar acceso a cuentas web, bases de datos confidenciales y otra información sensible. Un ataque de acceso puede efectuarse de varias maneras. Un ataque de acceso generalmente emplea un ataque de diccionario para adivinar las contraseñas del sistema. También hay diccionarios especializados para diferentes idiomas.

Hay cinco tipos de ataques de acceso:

1. **Ataques de contraseña:** el atacante intenta adivinar las contraseñas del sistema. Un ejemplo común es un ataque de diccionario.
2. **Explotación de la confianza:** el atacante usa privilegios otorgados a un sistema en una forma no autorizada, posiblemente causando que el objetivo se vea comprometido.
3. **Redirección de puerto:** se usa un sistema ya comprometido como punto de partida para ataques contra otros objetivos. Se instala una herramienta de intrusión en el sistema comprometido para la redirección de sesiones.
4. **Ataque Man in the Middle:** el atacante se ubica en medio de una comunicación entre dos entidades legítimas para leer o modificar los datos que pasan entre las dos partes.
5. **Desbordamiento de buffer:** el programa escribe datos más allá de la memoria de buffer. Un resultado del desbordamiento es que los datos válidos se sobreescriben o explotan para permitir la ejecución de código malicioso.

### Ataques de denegación de servicio

Los ataques de denegación de servicio (DoS) envían un número extremadamente grande de solicitudes en una red o Internet. Estas solicitudes excesivas hacen que la calidad de funcionamiento del dispositivo víctima sea inferior. Como consecuencia, el dispositivo atacado no está disponible para acceso y uso legítimo. Al ejecutar explotaciones o combinaciones de explotaciones, los ataques de DoS desaceleran o colapsan aplicaciones y procesos. Un ataque distribuido de denegación de servicio (DDoS) es similar en intención al ataque de DoS, excepto en que el ataque DDoS se origina en varias fuentes coordinadas.

Los ataques de DoS más comunes son:

- **Ping de la muerte:** se trata de una solicitud de eco en un paquete IP más grande que el tamaño de paquete máximo de 65535 bytes. Enviar un ping de este tamaño puede colapsar el nodo objetivo. Una variante de este ataque es colapsar el sistema enviando fragmentos ICMP, que llenan los buffers de reensamblado de paquetes en el objetivo.
- **Ataque Smurf:** el atacante envía un gran número de solicitudes ICMP a direcciones broadcast, todos con direcciones de origen falsificadas de la misma red que la víctima. Si el dispositivo de enrutamiento que envía el tráfico a esas direcciones de broadcast reenvía los broadcasts, todos los host de la red destino enviarán respuestas ICMP, multiplicando el tráfico por el número de hosts en las redes. En una red broadcast multiacceso cientos de máquinas podrían responder a cada paquete.
- **Inundación TCP/SYN:** se envía una inundación de paquetes SYN TCP, generalmente con una dirección de origen falsa. Cada paquete se maneja como una solicitud de conexión, causando que el servidor genere una conexión a medio abrir devolviendo un paquete SYN-ACK TCP y esperando un paquete de respuesta de la dirección del remitente. Sin embargo, como la dirección del remitente es falsa, la respuesta nunca llega. Estas conexiones a medio abrir saturan el número de conexiones disponibles que el servidor puede atender, haciendo que no pueda responder a solicitudes legítimas hasta después de que el ataque haya finalizado.

### Mitigación de ataques de red

Los ataques de inundación reconocimiento pueden ser mitigados de varias maneras. Utilizar una autenticación fuerte es una primera opción para la defensa contra sniffers de paquetes. El cifrado también es efectivo en la mitigación de estos. Si el tráfico está cifrado, es prácticamente irrelevante si un sniffer de paquetes está siendo utilizado, ya que los datos capturados no son legibles.

El software antisniffer y las herramientas de hardware detectan cambios en el tiempo de respuesta de los hosts para determinar si los hosts están procesando más tráfico del que sus propias cargas de tráfico indicarían. Una infraestructura conmutada es la norma hoy en día, lo cual dificulta la captura de datos que no sean los del dominio de colisión inmediato, que probablemente contenga solo un host.

Es imposible mitigar el escaneo de puertos. Sin embargo, el uso de un IPS (*Intrusion Prevention System*) y un firewall puede limitar la información que puede ser descubierta con un escáner de puerto, y los barridos de ping pueden ser detenidos si se deshabilitan el eco y la respuesta al eco ICMP en los routers de borde. Los IPS basados en red y los basados en host pueden notificar al administrador cuando está tomando lugar un ataque de reconocimiento. Esta advertencia permite al administrador prepararse mejor para el ataque o notificar al ISP sobre el lugar desde donde se está lanzando el reconocimiento.

Un número sorprendente de ataques de acceso se lleva a cabo a través de simples averiguaciones de contraseñas o ataques de diccionario de fuerza bruta contra las contraseñas. El uso de protocolos de autenticación cifrados o de hash, en conjunción con una política de contraseñas fuerte, reduce enormemente la probabilidad de ataques de acceso exitosos.

Hay prácticas específicas que ayudan a asegurar una política de contraseñas fuerte:

- Deshabilitar cuentas luego de un número específico de autenticaciones fallidas.
- Usar una contraseña de una sola vez (OTP) o una contraseña cifrada.
- Usar contraseñas fuertes. Las contraseñas fuertes tienen por lo menos seis caracteres y contienen letras mayúsculas y minúsculas, números y caracteres especiales.

La criptografía es un componente crítico de una red segura. Se recomienda utilizar cifrado para el acceso remoto a una red. Además, el tráfico del protocolo de enrutamiento también debería estar cifrado. Cuanto más cifrado esté el tráfico, menos oportunidad tendrán los hackers de interceptar datos con ataques Man in the Middle.

Un ataque de DoS puede ser truncado usando tecnologías antifalsificación (*anti-spoofing*) en routers y firewalls de perímetro. Hoy en día, muchos ataques de DoS son ataques distribuidos de DoS llevados a cabo por hosts comprometidos en varias redes. Mitigar los ataques DDoS requiere diagnóstico y planeamiento cuidadoso, así como también cooperación de los ISP.

También, y aunque la calidad de servicio (QoS) no ha sido diseñada como una tecnología de seguridad, una de sus aplicaciones, la implementación de políticas de tráfico (*traffic policing*), puede ser utilizada para limitar el tráfico ingresante de cualquier cliente dado en un router borde.

Los routers y switches Cisco soportan algunas tecnologías antifalsificación como seguridad de puerto, snooping de DHCP, IP Source Guard, inspección de ARP dinámico y ACL. Las ACL permiten realizar el filtrado de paquetes para controlar qué paquetes se mueven a través de la red y a dónde se les permite ir, clasificar el tráfico, controlar el ancho de banda, etc.

El tráfico del plano de datos consiste sobre todo en el tráfico generado por los usuarios y los paquetes que se reenvían a través del router a través del plano de datos. La seguridad del plano de datos se puede implementar con el uso de ACL, mecanismos antispoofing y funciones de seguridad de nivel 2.

Los switches Cisco Catalyst pueden utilizar las funciones integradas para proteger a nivel de la capa 2. Las siguientes son las herramientas de seguridad de nivel 2 integradas en los switches Cisco Catalyst:

- **Port security:** evita la suplantación de direcciones MAC y los ataques de inundaciones de direcciones MAC
- **DHCP snooping:** previene los ataques de cliente en el servidor DHCP y en el router
- **Dynamic ARP Inspection (DAI):** añade seguridad a ARP mediante el uso de la tabla DHCP snooping para minimizar el impacto del envenenamiento ARP y los ataques de suplantación
- **IP Source Guard:** evita la suplantación de direcciones IP mediante el uso de la tabla DHCP snooping

!!! tip "RECUERDE"
    Buenas prácticas generales de seguridad:

    1. Mantener parches actualizados, instalándolos cada semana o día si fuera posible, para prevenir los ataques de desbordamiento de buffer y la escalada de privilegios.
    2. Cerrar los puertos innecesarios y deshabilitar los servicios no utilizados.
    3. Utilizar contraseñas fuertes y cambiarlas seguido.
    4. Controlar el acceso físico a los sistemas.
    5. Evitar ingresos innecesarios en páginas web.
    6. Realizar copias de resguardo y probar los archivos resguardados regularmente.
    7. Educar a los empleados en cuanto a los riesgos de la ingeniería social y desarrollar estrategias para validar las entidades a través del teléfono, del correo electrónico y en persona.
    8. Cifrar y poner una contraseña a datos sensibles.
    9. Implementar hardware y software de seguridad como firewalls, IPS, dispositivos de red privada virtual, software antivirus y filtrado de contenidos y UPS para suministro eléctrico.
    10. Desarrollar una política de seguridad escrita para la compañía.

## Firewalls

El firewall es un dispositivo, sistema o grupo de sistemas que aplica una política definida y restrictiva en el control de acceso en las redes, monitoriza el tráfico entrante y saliente y decide si debe permitir o bloquear un tráfico específico según dicha política. Un firewall puede ser hardware, software o ambos a la vez.

Al principio, los firewalls inspeccionaban los paquetes coincidentes con grupos de reglas preestablecidas, con la opción de reenviar o descartar esos paquetes. Este tipo de filtrado de paquetes, llamado *stateless*, funciona sin importar si el paquete es parte de un flujo de datos existente. Cada paquete se filtra de manera similar a una ACL, basándose exclusivamente en los valores de los parámetros contenidos en el encabezado del paquete. Los firewalls sin estados no son dispositivos autónomos, la funcionalidad de firewall es proporcionada por los routers o servidores de la red.

Los firewalls con estados filtran los paquetes basándose en la información extraída de los datos que fluyen y se almacenan en él. Este tipo de firewall *stateful* es capaz de determinar si un paquete pertenece a un flujo de datos existente. Las reglas estáticas, como las de los firewalls stateless, son suplementadas por reglas dinámicas creadas en tiempo real para definir estos flujos activos. Los firewalls con estados ayudan a mitigar ataques de DoS que explotan conexiones activas a través de dispositivos de red.

!!! tip "RECUERDE"
    Los firewalls son la primera línea de defensa en seguridad de la red. Establecen una barrera entre las redes internas seguras, controladas y fiables y las redes externas poco fiables.

### Características de los firewalls

Algunos de los beneficios del uso del firewall en una red pueden ser:

- Previenen la exposición de los hosts y las aplicaciones sensibles a usuarios no confiables.
- Examinan el flujo de datos de los protocolos, previniendo la explotación de fallos en los mismos.
- Puede bloquearse el acceso de datos maliciosos a servidores y clientes.
- Hace que la aplicación de una política de seguridad se torne simple, escalable y robusta.
- Mejora la administración de la seguridad de la red al reducir el control de acceso a la misma.

Los firewalls también tienen limitaciones:

- Si está mal configurado, el firewall puede tener consecuencias serias.
- Muchas aplicaciones no pueden pasar a través del firewall en forma segura.
- Los usuarios pueden intentar buscar maneras de sortear el firewall para recibir material bloqueado, exponiendo la red a potenciales ataques.
- El rendimiento de la red puede disminuir.
- Puede hacerse tunneling de tráfico no autorizado o puede disfrazárselo como tráfico legítimo.

### Diseño de redes con firewalls

La seguridad en redes consiste en crear y mantener una política de seguridad, incluyendo una política de seguridad de firewall. Las siguientes recomendaciones sirven como punto de inicio para implementar una política de seguridad con firewall.

- Instalar los firewalls en las fronteras de seguridad clave.
- Los firewalls son el principal dispositivo de seguridad, pero no es aconsejable depender exclusivamente de ellos para la seguridad de una red.
- Denegar todo el tráfico por defecto y permitir solo los servicios necesarios.
- Asegurar que el acceso físico al firewall esté controlado.
- Monitorizar regularmente los registros del firewall.
- Administrar y controlar regularmente la configuración en el firewall.
- Los firewalls protegen principalmente contra ataques técnicos que se originan fuera de la red. Los ataques internos tienden a no ser de naturaleza técnica.

Algunos diseños son tan simples como la designación de una red externa y una interna, determinadas por dos interfaces en un firewall. La red externa no es confiable, mientras que la interna sí lo es. El tráfico proveniente de la red interna, pasa a través del firewall hacia afuera con pocas o ninguna restricción. El tráfico que se origina fuera generalmente es bloqueado o permitido muy selectivamente. Al tráfico de retorno que proviene de la red externa, asociado con tráfico de origen interno, se le permite pasar de la interfaz no confiable a la confiable.

Un diseño más complicado puede involucrar tres o más interfaces en el firewall. En este caso, generalmente se trata de una interfaz externa, una interna y una DMZ (*Demilitarized Zone*). En la seguridad de las redes, a menudo se hace referencia a una zona desmilitarizada como una porción de red conectada con un firewall donde es común permitir tipos específicos de tráfico desde fuera.

Las características de este diseño se resumen en:

- El flujo de tráfico circula libremente de la interfaz interna a la externa y la DMZ.
- Se permite libremente el paso del tráfico que proviene de la DMZ por la interfaz externa.
- El tráfico de la interfaz externa generalmente se bloquea salvo que esté asociado con tráfico de origen interno o de la DMZ.
- En interfaz DMZ es común permitir tráfico desde fuera, siempre que sea el tipo de tráfico correcto y que su destino sea la DMZ (por ejemplo, correo electrónico, DNS, HTTP o HTTPS).

En un escenario de defensa por capas, los firewalls proporcionan seguridad perimetral de toda la red y de los segmentos de red internos en el núcleo. La defensa por capas usa diferentes tipos de firewalls que se combinan para agregar profundidad a la seguridad de la organización. El tráfico sigue la siguiente secuencia:

1. El tráfico que ingresa de la red no confiable se topa con un filtro de paquetes inicial en el router más externo
2. El tráfico se dirige a un potente firewall dentro de la DMZ donde se aplican más reglas al tráfico y se descartan paquetes sospechosos
3. El tráfico apunta ahora al router interior, donde se moverá al host de destino interno solo si ha superado con éxito el filtrado entre el router externo y la red interna

Las recomendaciones finales en el diseño de una red con firewalls pueden ser las siguientes.

- Un número importante de las intrusiones proviene de hosts dentro de la red.
- Los firewalls no ofrecen protección contra instalaciones de módems no autorizadas.
- El firewall no puede reemplazar a los administradores y usuarios informados.
- Una defensa profunda debe incluir almacenamiento externo para resguardo y recuperación de desastres y una topología de hardware redundante.

### Tipos de firewall

Antes de adoptar alguna de las varias opciones de solución de firewall, es importante llevar a cabo un análisis de coste contra los posibles riesgos. No siempre la solución más costosa es la más adecuada. Cualquiera que sea la decisión que se tome en la adquisición de una solución de firewall, es crítico contar con un diseño de red apropiado para el desarrollo exitoso del firewall. Hay varios tipos de firewalls de filtrado, incluyendo los siguientes.

- **Firewall de filtrado de paquetes:** trabajan principalmente en la capa de Red del modelo OSI y generalmente se los considera dispositivos de capa 3. Sin embargo, analizan tráfico basándose en información de capa 4 como protocolo y números de puerto de origen y destino. El filtrado de paquetes utiliza las ACL para determinar si permite o deniega tráfico basándose en direcciones IP de origen y destino, protocolo, tipo de paquete y números de puerto origen y destino. Los firewalls de filtrado de paquetes generalmente son parte de un router con funcionalidad de firewall.
- **Stateful firewall:** los firewalls con estados son la tecnología de firewall más versátil y común, están clasificados como de capa de Red. Proporcionan filtrado de paquetes con estados utilizando la información de conexiones establecidas, almacenadas en una tabla de estados. Los firewalls Stateful usan dicha tabla para monitorizar el proceso de comunicación. El dispositivo examina la información en los encabezados de paquetes de capa 3, aunque, para algunas aplicaciones, también puede analizar tráfico de capas 4 y 5. Cada vez que se accede a un servicio externo, el firewall stateful retiene ciertos detalles de la solicitud y guarda el estado de la solicitud en la tabla de estados. Dicha tabla contiene las direcciones de origen y destino, los números de puertos, información de secuencias TCP y etiquetas adicionales por cada conexión TCP o UDP asociada con esa sesión particular. Cuando el sistema externo responde a una solicitud, el firewall compara los paquetes recibidos con el estado previamente almacenado para permitir o denegar el acceso a la red. El firewall permite la entrada de datos solo si existe una conexión apropiada que justifique su paso.
- **Proxy firewall:** filtra según información de las capas 3, 4, 5 y 7 del modelo de referencia OSI. La mayoría del control y filtrado del firewall se hace por software. Los servidores proxy pueden aportar otras funciones como contenido de caché y seguridad, ya que evitan conexiones directas desde fuera de la red. Sin embargo, esto puede afectar a otras funciones y a las aplicaciones que respaldan.
- **Firewall para gestión unificada de amenazas (UTM):** es un dispositivo UTM que combina de forma independiente las funciones de un stateful firewall, con prevención de intrusiones y antivirus. También puede incluir otros servicios como la gestión en la nube. Este firewall se centra en la sencillez y en la facilidad de uso.

## NGFW

Firewall de última generación (NGFW) son los Cisco Firepower, son evoluciones de todos los firewalls anteriores, no solamente filtran paquetes, sino que pueden detener amenazas como malware avanzado y ataques en la capa de aplicación. Las ventajas incluyen un firewall de última generación pueden ser:

- Funciones estándar de firewall como la inspección de estados.
- Prevención de intrusiones integrada.
- Detección de aplicaciones y control para visualizar y bloquear aplicaciones que puedan generar riesgos.
- Actualizar rutas para añadir futuras fuentes de información.
- Técnicas que permitan hacer frente a los cambios en las amenazas para la seguridad.

NGFW centrado en las amenazas es un tipo de firewall que cuenta con las funciones de un firewall de última generación tradicional pero también ofrece detección y solución de amenazas avanzadas. Las ventajas incluyen un NGFW centrado en las amenazas de última generación pueden ser:

- Reconoce los sectores que corren más riesgo, gracias a su completa visibilidad del contexto.
- Reaccionar rápidamente a los ataques a través de la automatización de una seguridad inteligente que establece políticas y refuerza sus defensas de manera dinámica.
- Detecta de manera más efectiva las actividades evasivas o sospechosas gracias a la vinculación de la red y el evento del terminal.
- Reduce de manera significativa el tiempo entre la detección y la limpieza a través de una seguridad retrospectiva que monitoriza de manera continua para buscar actividades y comportamientos sospechosos incluso después de una inspección inicia.
- Simplifica la gestión y reduce la complejidad gracias a políticas unificadas que aportan protección durante todo el ciclo del ataque.

!!! note "NOTA"
    Otros tipos de firewalls pueden ser:

    - Firewall de traducción de direcciones (NAT).
    - Host-based firewall.
    - Transparent firewall.
    - Hybrid firewall

## IPS

Un IPS (*Intrusion Prevention System*) monitoriza el tráfico de capas 3 y 4 y analiza los contenidos y la carga de los paquetes en búsqueda de ataques sofisticados insertos en ellos, que pueden incluir datos maliciosos pertenecientes a las capas 2 a 7. Las plataformas IPS de Cisco utilizan una mezcla de tecnologías de detección, incluyendo detecciones de intrusiones basadas en firma, basadas en perfil y de análisis de protocolo. Este análisis, más profundo, permite al IPS identificar, detener y bloquear ataques que pasarían a través de un dispositivo firewall tradicional. Cuando un paquete pasa a través de una interfaz en un IPS, no es enviado a la interfaz de salida o confiable hasta haber sido analizado previamente.

Los sistemas de detección de intrusiones IDS (*Intrusion Detection Systems*) fueron implementados para monitorizar de manera pasiva el tráfico de la red. Un IDS copia el tráfico de red y lo analiza en lugar de reenviar los paquetes reales. Compara el tráfico capturado con firmas maliciosas conocidas de manera offline del mismo modo que el software que busca virus. Esta implementación offline de IDS se conoce como "modo promiscuo". Al operar con una copia del tráfico el IDS no tiene efectos negativos sobre el flujo real de paquetes del tráfico reenviado; sin embargo, no puede evitar que el tráfico malicioso de ataques de un solo paquete alcance el sistema objetivo antes de aplicar una respuesta para detener el ataque.

El sistema de prevención de intrusiones IPS se apoya en la tecnología IDS ya existente. A diferencia del IDS, un dispositivo IPS se implementa en modo en línea y no permite el paso de tráfico malicioso respondiendo inmediatamente. Esto significa que todo el tráfico de entrada y de salida debe fluir a través de él para ser procesado. El IPS no permite que los paquetes ingresen al lado confiable de la red sin ser analizados primero. Puede detectar, calificar y tratar inmediatamente un problema según corresponda.

Las tecnologías IDS e IPS pueden complementarse entre sí basándose en las soluciones de cada una de ellas y en los objetivos de seguridad de la organización. Las tecnologías IDS e IPS se despliegan como sensores, que pueden ser cualquiera de los siguientes dispositivos:

- Un router configurado con software IPS Cisco IOS.
- Un dispositivo diseñado específicamente para proporcionar servicios IDS o IPS dedicados.
- Un módulo de red instalado en un dispositivo de seguridad adaptable, switch o router.

Las características del IDS en modo promiscuo son las siguientes:

- No tiene impacto sobre la red, no crea latencia ni genera jitter.
- La acción de respuestas no puede detectar los paquetes disparadores.
- No tiene impacto sobre la red si el sensor falla o se sobrecarga.
- Se requieren ajustes correctos para las acciones de respuesta.
- Se necesita una política de seguridad bien definida.
- Son más vulnerables a técnicas de evasión.

Las características del IPS en modo en línea son las siguientes:

- Detiene los paquetes disparadores.
- Puede tener algún impacto sobre la red, al crear latencia o jitter.
- Los posibles problemas de los sensores afectan al tráfico de la red.
- Puede utilizar técnicas de normalización de flujo.
- Se necesita una política de seguridad bien definida.

### Firmas IPS

Las firmas IPS, son paquetes criptográficos que se añaden a la IOS del Router que funciona como firewall. Estos paquetes de firmas se instalan en la memoria flash del router o en una memoria USB conectada permanentemente al dispositivo.

Cuando los sensores escanean los paquetes de la red, utilizan las firmas para detectar algún tipo de actividad intrusiva, como ataques de DoS, y responder con acciones predefinidas. Estas firmas identifican puntualmente gusanos, virus, anomalías en los protocolos o tráfico malicioso específico.

Cuando un sensor encuentra una coincidencia entre una firma y un flujo de datos, realiza una acción, como dejar constancia del evento en el registro o enviar una alarma al software de administración del IDS o IPS.

Las firmas se dividen en tres partes bien definidas:

- Tipo
- Alarma
- Acción

Las actualizaciones de firma requieren una suscripción y una llave de la licencia válidas de los Servicios de Cisco para IPS.

## NGIPS

La nueva generación de IPS Cisco (NGIPS) son sistemas dedicados modulares y escalables de protección contra amenazas y ciberataques. Un NGIPS recibe nuevas reglas sobre normas y firmas cada dos horas, para que el sistema de seguridad esté constantemente actualizado. El Firepower NGIPS se integra a la red sin necesidad de grandes cambios de hardware.

A través del Firepower Management Center, pueden visualizarse más datos contextuales de la red y ajustar su seguridad en tiempo real. Monitoriza aplicaciones, señales de peligro, perfiles de host, trayectorias de archivos, sandboxing, información de vulnerabilidades y visualiza sistemas operativos de los dispositivos. Estos datos son utilizados para optimizar la seguridad de la red.

!!! note "NOTA"
    Sandboxing es una técnica de seguridad que ejecuta procesos en un espacio virtual controlado y supervisado.

Algunas de las características de los NGIPS pueden ser:

- **Detección de intrusiones:** para evitar vulnerabilidades, el NGIPS puede marcar los archivos sospechosos y analizarlos en busca de amenazas no identificadas.
- **Nube pública:** puede aplicarse en nubes públicas y privadas para gestionar las amenazas. Los NGIPS están basados en la arquitectura abierta de Cisco y admite Azure, AWS, VMware y más hipervisores.
- **Segmentación interna de redes:** se ajusta fácilmente a la planificación de la red con un mecanismo de implementación que utiliza los requisitos de varias organizaciones internas.
- **Vulnerabilidad y gestión de parches:** la información de los NGIPS puede utilizarse para solucionar las vulnerabilidades más importantes en menos tiempo y con menos recursos.

## AAA

Los dispositivos Cisco ofrecen varios niveles de seguridad. La forma más simple de autenticación son las contraseñas. Los inicios de sesión de solo contraseña son muy vulnerables a ataques de fuerza bruta. Este método no ofrece registros de auditoría de ningún tipo. Cualquiera que tenga la contraseña puede ganar acceso al dispositivo y alterar la configuración.

AAA (*Authentication, Authorization, Accounting*) provee una mejor solución al hacer que todos los dispositivos accedan a la misma base de datos de usuarios y contraseñas en un servidor central. Cada una de las partes se detalla a continuación:

- **Authentication.** El proceso de autenticación se encarga de verificar que el usuario es quien dice ser, por ejemplo mediante el uso de un nombre de usuario y contraseña. La autenticación AAA local utiliza una base de datos local para la autenticación. Este método almacena los nombres de usuario y sus correspondientes contraseñas localmente y los usuarios se autentican en la base de datos local. Este método no es muy seguro y puede mejorarse con la autenticación basada en servidor.
- **Authorization.** El proceso de autorización determina a qué recursos tiene acceso el usuario una vez que se ha autenticado. En general, la autorización se implementa usando una solución de AAA basada en servidor.
- **Accounting.** El proceso de auditoría se encarga de registrar la actividad realizada por el usuario una vez que haya sido autenticado. Los servidores AAA mantienen un registro detallado de absolutamente todo lo que hace el usuario una vez autenticado en el dispositivo.

### RADIUS y TACACS+

RADIUS (*Remote Authentication Dial-In User Service*) está definido en la RFC 2865 y TACACS+ (*Terminal Access Control Access Control Server Plus*) en la RFC 1492. Ambos protocolos se encargan de proporcionar servicios AAA. RADIUS utiliza UDP, puerto 1645 o el 1812 para la autenticación y el puerto UDP 1646 o el 1813 para los registros de auditoría, mientras que TACACS+ utiliza TCP puerto 49.

Tanto TACACS+ como RADIUS son protocolos de administración, pero cada uno soporta diferentes capacidades y funcionalidades. La elección de uno sobre otro depende de las necesidades de la organización. Las diferencias entre ambos se enumeran a continuación:

1. RADIUS fue desarrollado por Livingston Enterprises; es un protocolo AAA abierto de estándar IETF con aplicaciones en acceso a las redes y movilidad IP.
2. TACACS+ es una mejora de Cisco del protocolo TACACS original, es un protocolo enteramente nuevo que es incompatible con todas las versiones anteriores de TACACS.
3. El protocolo RADIUS esconde las contraseñas durante la transmisión, el resto del paquete se envía en texto plano.
4. RADIUS combina autenticación y autorización en un solo proceso.
5. RADIUS es muy popular entre los proveedores de servicio VoIP.
6. RADIUS no permite especificar qué comandos puede utilizar el usuario después de iniciar una sesión en el router, simplemente permite o deniega el acceso al equipo.
7. TACACS+ tiene dos métodos de autorizar el uso de comandos en el router:
    - Especificando en el servidor TACACS+ los comandos que se permite usar a un determinado usuario o grupo.
    - Confiando en los niveles de privilegio. Se lanza una consulta al servidor TACACS+ para ver si el usuario o grupo puede usar un determinado comando en un determinado nivel de privilegio.
8. El protocolo DIAMETER es el reemplazo programado para RADIUS. DIAMETER usa un nuevo protocolo de transporte llamado SCTP (*Stream Control Transmission Protocol*) y TCP en lugar de UDP.
9. RADIUS no soporta los siguientes protocolos:
    - AppleTalk Remote Access (ARA) protocol.
    - NetBIOS Frames Protocol Control protocol.
    - Novell Asynchronous Services Interface (NASI).
    - X.25 PAD connection.
10. TACACS+ ofrece soporte multiprotocolo, como IP y AppleTalk.
11. TACACS+ proporciona servicios AAA separados.
12. Las extensiones al protocolo TACACS+ proporcionan más tipos de códigos de solicitud y respuesta de autenticación que los que estaban en la especificación TACACS original.
13. TACACS+ separa completamente los procesos de autenticación y autorización y soporta más protocolos que RADIUS, mientras que RADIUS los unifica.

### Configuración AAA local y basada en servidor

El comando `aaa new-model` sirve para habilitar AAA. Si se utiliza la forma `no` delante quedará deshabilitado. Defina una lista nombrada de los métodos de autenticación y luego aplíquela a las interfaces con el comando `aaa authentication login`.

```text
Router(config)# aaa new-model
Router(config)# aaa authentication login {default | list-name} method1 [method2...]
```

AAA basado en servidor debe identificar los servidores TACACS+ y RADIUS que el servicio AAA debe consultar al autenticar y autorizar usuarios. Una vez habilitado AAA en el dispositivo debe indicar el servidor que se utilizará.

El comando `radius-server host` se utiliza para indicar el servidor RADIUS.

```text
Router(config)# radius-server host {hostname | ip-address} [auth-port port-number] [acct-port port-number] [timeout seconds] [retransmit retries] [key string] [alias {hostname | ip-address}]
```

El comando `tacacs-server host`, se utiliza para indicar el servidor TACACS.

```text
tacacs-server host {hostname | ip-address} [key string] [nat] [port [integer]] [single-connection] [timeout [integer]]
no tacacs-server host {host-name | host-ip-address}
```

Los siguientes comandos son adicionales a la configuración de AAA basada en servidor:

Ambos comandos cumplen la misma función de configuración de la clave de autenticación para la comunicación entre el router y el servidor.

```text
[no] radius-server key {0 string | 7 string | string}
[no] tacacs-server key {0 string | 7 string | string}
```

No es un comando específico de AAA. Sirve para especificar un usuario y contraseña.

```text
username root password
```

Especifica los métodos de autenticación para usar en interfaces seriales PPP.

```text
[no] aaa authentication ppp {default | list-name} method1 [method2...]
```

Permite definir el grado de acceso de los usuarios.

```text
[no] aaa authorization {network | exec | commands level | reverse-access} {default | listname} [method1 [method2...]]
```

Permite guardar un registro con los comandos que ha utilizado cada usuario.

```text
[no] aaa accounting {auth-proxy | system | network | exec | connection | commands level} {default | list-name} [vrf vrf-name] {start-stop | stop-only | none} [broadcast] group group-name
```

### Verificación AAA

Para ver los atributos recolectados en una sesión AAA, utilice el siguiente comando:

```text
Router# show aaa user {all | unique id}
```

Es posible obtener información de todos los usuarios bloqueados, con el comando:

```text
Router# show aaa local user lockout
```

Este último comando no proporciona información sobre todos los usuarios que ingresan a un dispositivo, sino sobre aquellos que han sido autenticados o autorizados usando AAA o cuyas sesiones están siendo monitorizadas por el módulo de registro de auditoría de AAA.

Existen varios comandos `debug` que se pueden utilizar para este propósito, que como siempre que se utilicen con comandos `debug` ha de hacerse con cuidado y con la plena seguridad de no saturar el procesador. La siguiente tabla muestra los principales comandos `debug`:

| Comando | Descripción |
| --- | --- |
| `debug aaa authentication` | Muestra información sobre los eventos de autenticación. |
| `debug aaa authorization` | Muestra información sobre los eventos de autorización. |
| `debug aaa accounting` | Muestra información sobre los eventos de auditoría. |
| `debug radius` | Muestra información relativa a RADIUS. |
| `debug tacacs` | Muestra información relativa a TACACS+. |

!!! tip "RECUERDE"
    Ejecutar un proceso `debug` desmedido puede saturar al router o al switch hasta hacerlo inoperable. Termine el proceso `debug` con el comando `no debug all` o `undebug all`.

## DHCP snooping

Los usuarios maliciosos intentan enviar información falsa a los switches o host intentando utilizar mecanismos de burla falseando las puertas de enlace. El objetivo del atacante es interceptar el tráfico enviando paquetes al afectado como si éste fuera la puerta de enlace o el router. El atacante puede obtener información del tráfico de paquetes antes de que lleguen a su verdadero destino. El atacante está en el medio del camino, el cliente nunca se da cuenta de ello, acción conocida como *man-in-the-middle*.

Un servidor DHCP proporciona la información que un cliente necesita para operar dentro de una red. Un atacante puede activar un servidor DHCP falso en el mismo segmento en que se encuentra el cliente; cuando el cliente hace la petición DHCP el falso servidor podría enviar el DHCP reply con su propia dirección IP sustituyendo a la verdadera puerta de enlace. Los paquetes destinados hacia fuera de la red local serían enviados al servidor del atacante que podrá enviarlos a la dirección correcta pero primero podrá examinar cada paquete que va interceptando.

Los switches Catalyst poseen la característica DHCP Snooping para prevenir este tipo de ataque. Cuando está configurado, los puertos están categorizados como confiables o no confiables. Los servidores DHCP legítimos pueden encontrarse en puertos confiables, mientras que todos los demás host están detrás de los puertos no confiables. Un switch intercepta todas las peticiones DHCP que vienen de los puertos no confiables antes de pasarlas a la VLAN correspondiente. Cualquier respuesta DHCP *reply* viniendo desde un puerto no confiable se descarta, además el puerto pasará al estado *errdisable*.

DHCP Snooping mantiene un registro de todos los enlaces de los DHCP completados, lo que significa que posee conocimiento de las direcciones MAC, direcciones IP, tiempo de alquiler, etc. del cliente. El siguiente comando configura DHCP Snooping en el switch:

```text
Switch(config)#ip dhcp snooping
```

El siguiente paso consiste en identificar la VLAN donde DHCP Snooping se implementará:

```text
Switch(config)#ip dhcp snooping vlan vlan-id [vlan-id]
```

Posteriormente se configuran los puertos confiables donde están localizados los servidores DHCP reales:

```text
Switch(config)#interface type mod/num
Switch(config-if)#ip dhcp snooping trust
```

Para los puertos no confiables se permite un número ilimitado de peticiones DHCP, para limitarlo se puede utilizar el siguiente comando:

```text
Switch(config)#interface type mod/num
Switch(config-if)#ip dhcp snooping limit rate rate
```

El parámetro `rate` tiene un rango de 1 a 2048 paquetes DHCP por segundo.

Puede, además, configurarse el switch para que use la opción DHCP 82 descrita en la RFC 3046. Añadiendo la opción 82 la información acerca del cliente que ha generado la petición DHCP es más amplia. Además, la respuesta DHCP (en caso de que la hubiera) traerá contenida la información de la opción 82. El switch intercepta la respuesta y compara los datos de la opción 82 para confirmar que la respuesta viene de un puerto válido en el mismo. Esta característica está habilitada por defecto; no obstante, para habilitar la opción 82 se utiliza el siguiente comando:

```text
Switch(config)# ip dhcp snooping information option
```

El estado del DHCP Snooping puede verse con el siguiente comando:

```text
Switch#show ip dhcp snooping [binding]
```

El parámetro `binding` se utiliza para mostrar todas las relaciones conocidas de DHCP que han sido recibidas.

En el siguiente ejemplo se observa la configuración de DHCP Snooping, las interfaces FastEthernet 0/5 a la 0/16 son consideradas no confiables, la cantidad de peticiones están limitadas a 3 por segundo. El servidor DHCP conocido está localizado en la interfaz GigaEthernet 0/1:

```text
Switch(config)#ip dhcp snooping
Switch(config)#ip dhcp snooping vlan 104
Switch(config)#interface range fastethernet 0/5 - 16
Switch(config-if)#ip dhcp snooping limit rate 3
Switch(config-if)#interface gigabitethernet 0/1
Switch(config-if)#ip dhcp snooping trust
Switch#show ip dhcp snooping
Switch DHCP snooping is enabled
DHCP snooping is configured on following VLANs:
 104
Insertion of option 82 is enabled

Interface          Trusted  Rate limit (pps)
-----------------  -------  ----------------
FastEthernet0/35   no       3
FastEthernet0/36   no       3
GigabitEthernet0/1  yes      unlimited
```

En algunos entornos es necesario utilizar ordenadores o dispositivos específicos en la red para capturar flujos de tráfico y examinar los paquetes. De esta manera se sondea dentro de las cabeceras de capa 2, 3 y 4 para ver como dichos paquetes son tratados en la red.

Si hay uno varios switches entre los segmentos los dominios de colisión se separarán y no se enviarán las tramas en cuestión al puerto donde se encuentre conectado el analizador de tráfico.

## Seguridad de puertos

Los switches Catalyst poseen una característica llamada *port-security* que controla las direcciones MAC asignadas a cada puerto. Para iniciar la configuración de seguridad de puertos en un switch se comienza con el siguiente comando:

```text
Switch(config-if)#switchport port-security
```

Posteriormente se deben identificar un conjunto de direcciones MAC permitidas en ese puerto. Estas direcciones pueden ser configuradas explícitamente o de forma dinámica a través del tráfico entrante por ese puerto, en cada interfaz que utiliza port-security se debe especificar un número máximo de direcciones MAC que serán permitidas:

```text
Switch(config-if)#switchport port-security maximum max-addr
```

La siguiente sintaxis muestra la configuración de direcciones MAC para un puerto a un máximo de 5:

```text
Switch(config-if)#switchport port-security maximum 5
```

También se puede definir estáticamente una o más direcciones MAC en una interfaz, cualquiera de las direcciones configuradas tendrá permitido el acceso a la red a través de ese puerto:

```text
Switch(config-if)#switchport port-security mac-address mac-addr
```

El rango de MAC permitidas va desde 1 a 1024. Cada interfaz configurada con port-security aprende dinámicamente las direcciones MAC por defecto y espera que esas direcciones aparezcan en esa interfaz en el futuro. Este proceso se llama **sticky MAC addresses**. Las direcciones MAC se aprenden cuando las tramas de los hosts pasan a través de la interfaz, que aprende hasta el número máximo de direcciones que tiene permitidas. Las direcciones aprendidas también son eliminadas si los hosts conectados no transmiten en un período determinado.

Si el número de direcciones estáticas dado es menor que el número máximo de direcciones que puede aprender dinámicamente, el resto de las direcciones se aprenderán dinámicamente. Por lo tanto, se debe tener un control apropiado sobre cuantas direcciones se deben permitir.

Finalmente se debe definir cómo una interfaz con seguridad de puerto debería reaccionar si ocurre un intento de violación, para eso se utiliza el siguiente comando:

```text
Switch(config-if)# switchport port-security violation {shutdown | restrict | protect}
```

Cuando más del número máximo de direcciones MAC permitidas o una dirección MAC desconocida se detecta se interpreta como una violación. El puerto del switch toma algunas de las siguientes acciones cuando ocurre una violación:

- **Shutdown**, el puerto automáticamente se pone en el estado *errdisable*, lo que hace dejarlo inoperable y tendrá que ser habilitado manualmente o utilizando la recuperación de errdisable.
- **Restrict**, el puerto permanece activo pero los paquetes desde las direcciones MAC que están violando la restricción son eliminados. El switch continúa ejecutando el temporizador de los paquetes que están violando la condición y puede enviar un trap de SNMP a un servidor Syslog para alertar de lo que está ocurriendo.
- **Protect**, el puerto sigue habilitado pero los paquetes de las direcciones que están violando la condición son eliminados, no queda ninguna constancia de lo que está aconteciendo en el puerto.

Un ejemplo del modo restrict se detalla en la siguiente sintaxis:

```text
interface GigabitEthernet0/11
 switchport access vlan 991
 switchport mode access
 switchport port-security
 switchport port-security violation restrict
 spanning-tree portfast
```

Cuando el número máximo de direcciones MAC se excede se guarda un log cuya sintaxis se muestra a continuación:

```text
Jun  3 17:18:41.888 EDT: %PORT_SECURITY-2-PSECURE_VIOLATION: Security violation occurred, caused by MAC address 0000.5e00.0101 on port GigabitEthernet0/11.
```

En caso de que se cumpla la condición restrict o protect se deberían eliminar las direcciones MAC que no son permitidas con el siguiente comando:

```text
Switch#clear port-security dynamic [address mac-addr | interface type mod/num]
```

En el modo shutdown la acción de port-security es mucho más drástica. Cuando el número máximo de direcciones MAC es sobrepasado el siguiente mensaje log indica que el puerto ha sido puesto en modo errdisable:

```text
Jun  3 17:14:19.018 EDT: %PM-4-ERR_DISABLE: psecure-violation error detected on Gi0/11, putting Gi0/11 in err-disable state
Jun  3 17:14:19.022 EDT: %PORT_SECURITY-2-PSECURE_VIOLATION: Security violation occurred, caused by MAC address 0003.a089.efc5 on port GigabitEthernet0/11.
Jun  3 17:14:20.022 EDT: %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/11, changed state to down
Jun  3 17:14:21.023 EDT: %LINK-3-UPDOWN: Interface GigabitEthernet0/11, changed state to down
```

El estado de un puerto puede verse con el comando `show port-security interface`:

```text
Switch#show port-security interface gigabitethernet 0/11
Port Security              : Enabled
Port Status                : Secure-shutdown
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 0
Configured MAC Addresses  : 0
Sticky MAC Addresses       : 0
Last Source Address        : 0003.a089.efc5
Security Violation Count   : 1
```

Para ver un resumen rápido del estado del puerto puede utilizarse el siguiente comando:

```text
Switch#show interfaces status err-disabled
Port Name               Status    Reason
Gi0/11        Test port  err-disabled  psecure-violation
```

Hay que recordar que cuando un puerto está en el estado errdisable se debe recuperar manualmente o de manera automática. La secuencia de comandos para la recuperación manual es la siguiente:

```text
Switch(config)#interface type mod/num
Switch(config-if)#shutdown
Switch(config-if)#no shutdown
```

Finalmente, se puede ver un resumen del estado de port-security con el siguiente comando:

```text
Switch#show port-security
Secure Port  MaxSecureAddr  CurrentAddr  SecurityViolation  Security Action
     (Count)     (Count)      (Count)
-------------------------------------------------------------
Gi0/11           5             1              0             Restrict
Gi0/12           1             0              0             Shutdown
-------------------------------------------------------------
Total Addresses in System (excluding one mac per port) : 0
Max Addresses limit in System (excluding one mac per port) : 6176
```

## Autenticación basada en puerto

Los switches Catalyst pueden soportar autenticación basada en puerto que resulta una combinación de autenticación AAA (*Authentication, Authorization, Accounting*) y de port-security. Esta característica se basa en el estándar IEEE 802.1X, cuando está habilitado un puerto del switch no pasará tráfico hasta que el usuario se autentique con el switch. Si la autenticación es satisfactoria el usuario podrá utilizar el puerto con normalidad.

En la autenticación basada en puerto tanto el switch (autenticador) como el PC del usuario (suplicante) tienen que soportar el estándar 802.1X usando EAPOL (*Extensible Authentication Protocol over LAN*). Dicho estándar es un protocolo que se ejecuta entre el cliente y el switch que está brindando el servicio de red. Si el cliente del PC está configurado para utilizar 802.1X pero el switch no lo soporta, el PC abandona el protocolo y se comunica normalmente; pero a la inversa, es decir, si el switch está configurado con autenticación y el PC no lo soporta, el puerto del switch permanecerá en estado "no autorizado" de manera que no enviará tráfico a ese cliente.

Un puerto del switch con 802.1X comienza en el estado no autorizado, de tal manera que solamente el único tipo de datos que permite pasar es del propio protocolo 802.1X. Tanto el cliente como el switch pueden comenzar la sesión 802.1X. El estado autorizado del puerto finaliza cuando el usuario del puerto termina la sesión causando que el cliente 802.1X informe al switch que regrese al estado no autorizado. El switch puede finalizar la sesión del usuario cuando lo crea necesario; en caso de que así ocurra, el cliente tiene que reautenticarse para continuar utilizando el puerto.

### Configuración de 802.1X

La autenticación basada en puerto puede ser administrada por uno o más servidores RADIUS (*Remote Authentication Dial-In User Service*). Aunque muchos switches Cisco soportan otros métodos de autenticación solo RADIUS soporta el estándar 802.1X.

El método de autenticación real de RADIUS tiene que ser configurado inicialmente y luego el 802.1X. Los siguientes pasos muestran dicha configuración:

1. **Habilitación de AAA en el switch.** Por defecto AAA está deshabilitado; para habilitarlo se utiliza el siguiente comando:

    ```text
    Switch(config)#aaa new-model
    ```

    El parámetro `new-model` hace referencia al método de listas que se van a utilizar para la autenticación.

2. **Definición de los servidores RADIUS externos.** En primer lugar se define cada servidor junto con la clave compartida; esta cadena solamente es conocida por el switch y el servidor y proporciona una clave de encriptación para la autenticación del usuario.

    ```text
    Switch(config)#radius-server host {hostname | ip-address} [key string]
    ```

    Este comando debe repetirse según tantos servidores existan en la red.

3. **Definición del método de autenticación 802.1X.** Con el siguiente comando los servidores de autenticación RADIUS que se han definido en el switch utilizarán la autenticación 802.1X:

    ```text
    Switch(config)#aaa authentication dot1x default group radius
    ```

4. **Habilitación de 802.1x en el switch.**

    ```text
    Switch(config)#dot1x system-auth-control
    ```

5. **Configuración de los puertos del switch con 802.1X.**

    ```text
    Switch(config)#dot1x system-auth-control
    Switch(config)# interface type mod/num
    Switch(config-if)#dot1x port-control {force-authorized | force-unauthorized | auto}
    ```

    Donde:

    - `force-authorized`: el puerto es forzado para que siempre autorice cualquier conexión de cliente, no es necesario la autenticación; este es el estado por defecto para todos los puertos cuando 802.1X está habilitado.
    - `force-unauthorized`: el puerto es forzado para no autorizar nunca la conexión de un cliente, como resultado ese puerto no pasará al estado autorizado.
    - `auto`: el puerto utiliza un intercambio de 802.1X para moverse desde el estado *unauthorized* hacia el estado *authorized* cuando la autenticación resulte satisfactoria. Esto requiere una aplicación capaz de soportar dicho estándar en el PC del cliente.

    Por defecto, todos los puertos del switch están en el estado `force-authorized` pero si el objetivo es la utilización de 802.1X los puertos deben estar configurados en `auto`, de tal manera que se emplee dicho mecanismo de autenticación.

6. **Permitir múltiples host en un puerto del switch.** El estándar 802.1X soporta casos en los cuales múltiples host están conectados a un simple puerto del switch ya sea a través de un hub o de otros switch de acceso. En este caso se debe configurar el puerto con el siguiente comando:

    ```text
    Switch(config-if)#dot1x host-mode multi-host
    ```

El comando `show dot1x all` se utiliza para verificar las operaciones de 802.1X en cada puerto del switch donde está configurado.

El siguiente es un ejemplo de autenticación basada en 802.1X, donde hay configurados dos servidores RADIUS y varios puertos del switch están utilizando 802.1X para autenticación y asociación con la VLAN 100:

```text
Switch(config)#aaa new-model
Switch(config)#radius-server host 100.30.1.1 key PruebaCCNP
Switch(config)#radius-server host 100.30.1.2 key OtraCCNP
Switch(config)#aaa authentication dot1x default group radius
Switch(config)#dot1x system-auth-control
Switch(config)#interface range FastEthernet0/1 - 40
Switch(config-if)#switchport access vlan 100
Switch(config-if)#switchport mode access
Switch(config-if)#dot1x port-control auto
```

## Listas de acceso

Desde la primera vez que se conectaron varios sistemas para formar una red, ha existido una necesidad de restringir el acceso a determinados sistemas o partes de la red por motivos de seguridad, privacidad y otros. Mediante la utilización de las funciones de filtrado de paquetes del software IOS, un administrador de red puede restringir el acceso a determinados sistemas, segmentos de red, rangos de direcciones y servicios, basándose en una serie de criterios. La capacidad de restringir el acceso cobra mayor importancia cuando la red de una empresa se conecta con otras redes externas, como otras empresas asociadas o Internet.

Los routers se sirven de las ACL (*Access Control List*) para identificar el tráfico. Esta identificación puede usarse posteriormente para filtrarlo y conseguir una mejor administración y rendimiento del tráfico global de la red. Las listas de acceso constituyen una eficaz herramienta para el control de la red, añaden la flexibilidad necesaria para filtrar el flujo de paquetes que entra y sale de las diferentes interfaces del router.

Las ACL trabajan utilizando entradas de control de acceso, ACE (*Access Control Entries*), en un listado secuencial de condiciones de permiso o prohibición que se aplican a direcciones IP o a protocolos IP de capa superior.

Las listas de acceso identifican el tráfico que ha de ser filtrado en su tránsito por el router, pero no pueden filtrar el tráfico originado por el propio router. Las listas de acceso pueden aplicarse también a los puertos de líneas de terminal virtual para permitir y denegar tráfico Telnet entrante o saliente, no es posible bloquear el acceso Telnet desde el mismo router.

Se pueden usar listas de acceso IP para establecer un control más fino o la hora de separar el tráfico en diferentes colas de prioridades y personalizadas. Una lista de acceso también puede utilizarse para identificar el tráfico "interesante" que sirve para activar las llamadas del enrutamiento por llamada telefónica bajo demanda (DDR). Las listas de acceso son mecanismos opcionales del software Cisco IOS que pueden ser configurados para filtrar o verificar paquetes con el fin de determinar si deben ser retransmitidos hacia su destino, o bien descartados.

Cuando un paquete llega a una interfaz, el router comprueba si el paquete puede ser retransmitido verificando su tabla de enrutamiento. Si no existe ninguna ruta hasta la dirección de destino, el paquete es descartado. A continuación, el router comprueba si la interfaz de destino está agrupada en alguna lista de acceso. De no ser así, el paquete puede ser enviado al búfer de salida. Si el paquete de salida está destinado a un puerto, que no ha sido agrupado a ninguna lista de acceso de salida, dicho paquete será enviado directamente al puerto destinado. Si el paquete de salida está destinado a un puerto que ha sido agrupado en una lista de acceso saliente, antes de que el paquete pueda ser enviado al puerto destinado será verificado por una serie de instrucciones de la lista de acceso asociada con dicha interfaz.

Dependiendo del resultado de estas pruebas, el paquete será admitido o denegado.

- Para las listas salientes, un `permit` significa enviar al búfer de salida, mientras que `deny` se traduce en descartar el paquete.
- Para las listas entrantes un `permit` significa continuar el procesamiento del paquete tras su recepción en una interfaz, mientras que `deny` significa descartar el paquete.

Cuando se descarta un paquete IP, ICMP devuelve un paquete especial notificando al remitente que el destino ha sido inalcanzable.

### Prueba de las condiciones de una ACL

Las instrucciones de una lista de acceso operan en un orden lógico secuencial. Evalúan los paquetes de principio a fin, instrucción a instrucción. Si la cabecera de un paquete se ajusta a una instrucción de la lista de acceso, el resto de las instrucciones de la lista serán omitidas, y el paquete será permitido o denegado según se especifique en la instrucción competente.

Si la cabecera de un paquete no se ajusta a una instrucción de la lista de acceso, la prueba continúa con la siguiente instrucción de la lista. El proceso de comparación sigue hasta llegar al final de la lista, cuando el paquete será denegado implícitamente.

Una vez que se produce una coincidencia, se aplica la opción de permiso o denegación y se pone fin a las pruebas de dicho paquete. Esto significa que una condición que deniega un paquete en una instrucción no puede ser afinada en otra instrucción posterior.

La implicación de este modo de comportamiento es que el orden en que figuran las instrucciones en la lista de acceso es esencial. Hay una instrucción final que se aplica a todos los paquetes que no han pasado ninguna de las pruebas anteriores. Esta condición final se aplica a todos esos paquetes y se traduce en una condición de denegación del paquete. En lugar de salir por alguna interfaz, todos los paquetes que no satisfacen las instrucciones de la lista de acceso son descartados.

Esta instrucción final se conoce como la **denegación implícita de todo**, al final de cada lista de acceso. Aunque esta instrucción no aparece en la configuración del router, siempre está activa. Debido a dicha condición, es necesario que en toda lista de acceso exista al menos una instrucción `permit`, en caso contrario la lista de acceso bloquearía todo el tráfico.

## Tipos de listas de acceso

### Listas de acceso estándar

Las listas de acceso estándar solo comprueban las direcciones de origen de los paquetes que solicitan enrutamiento. El resultado es el permiso o la denegación de la salida del paquete por parte del protocolo, basándose en la dirección IP de la red-subred-host de origen.

### Listas de acceso extendidas

Las listas de acceso extendidas comprueban tanto la dirección de origen como la de destino de cada paquete. También pueden verificar protocolos especificados, números de puerto y otros parámetros.

### Listas de acceso con nombre

Permiten asignar nombres en lugar de un rango numérico en las listas de acceso estándar y extendidas.

!!! note "NOTA"
    El estudio de este libro se basa en las listas de acceso IP.

## Aplicación de las ACL

Las listas de acceso expresan el conjunto de reglas que proporcionan un control añadido para los paquetes que entran en interfaces de entrada, paquetes que se trasmiten por el router y paquetes que salen de las interfaces de salida del router.

Una vez creada, una ACL debe asociarse a una o varias interfaces de forma que analice todos los paquetes que pasen por estas ya sea de manera entrante o saliente según corresponda el caso. La manera de determinar cuál de los casos es el que corresponde es pensar si los paquetes van hacia la red en cuestión (saliente) o si vienen de ella (entrante).

Las ACL deben ubicarse donde más repercutan sobre la eficacia. Las reglas básicas son:

- Ubicar las ACL extendidas lo más cerca posible del origen del tráfico denegado. De esta manera, el tráfico no deseado se filtra sin atravesar la infraestructura de red.
- Como las ACL estándar no especifican las direcciones de destino, colóquelas lo más cerca del destino posible.

### ACL para tráfico entrante

Los paquetes entrantes son procesados antes de ser enrutados a una interfaz de salida, si el paquete pasa las pruebas de filtrado, será procesado para su enrutamiento (evita la sobrecarga asociada a las búsquedas en las tablas de enrutamiento si el paquete ha de ser descartado por las pruebas de filtrado). El paquete entrante es filtrado antes de su enrutamiento.

### ACL para tráfico saliente

Los paquetes entrantes son enrutados a la interfaz de salida y después son procesados por medio de la lista de acceso de salida antes de su transmisión. El paquete saliente debe ser enrutado antes de su respectivo filtrado.

!!! tip "RECUERDE"
    Las listas de acceso no actúan sobre paquetes originados en el propio router, como las actualizaciones de enrutamiento o las sesiones telnet salientes.

## Máscara comodín

Puede ser necesario probar condiciones para un grupo o rango de direcciones IP, o bien para una dirección IP individual. La comparación de direcciones tiene lugar usando máscaras que actúan a modo de comodines en las direcciones de la lista de acceso, para identificar los bits de la dirección IP que han de coincidir explícitamente y cuáles pueden ser ignorados. El enmascaramiento wildcard para los bits de direcciones IP utiliza los números 1 y 0 para referirse a los bits de la dirección. Teniendo en cuenta que:

- Un bit de máscara wildcard `0` significa "comprobar el valor correspondiente".
- Un bit de máscara wildcard `1` significa "No comprobar (ignorar) el valor del bit correspondiente".

Para los casos más frecuentes de enmascaramiento wildcard se pueden utilizar abreviaturas.

- `Host` = máscara comodín 0.0.0.0, utilizada para un host específico.
- `Any` = 0.0.0.0 255.255.255.255, utilizado para definir a cualquier host, red o subred.

En el caso de permitir o denegar redes o subredes enteras se deben ignorar todos los hosts pertenecientes a dicha dirección de red o subred. Cualquier dirección de host será leída como dirección de red o subred.

Por ejemplo, el siguiente caso de una dirección IP clase B:

```text
172.16.32.0 255.255.224.0
```

| Concepto | Octeto 1 | Octeto 2 | Octeto 3 | Octeto 4 |
| --- | --- | --- | --- | --- |
| Dirección IP | 172 | 16 | 32 | 0 |
| En binarios | 10101100 | 00010000 | 00100000 | 00000000 |
| Máscara | 255 | 255 | 224 | 0 |
| En binarios | 11111111 | 11111111 | 11100000 | 00000000 |
| Wildcard | 00000000 | 00000000 | 00011111 | 11111111 |
| Resultado | Se tienen en cuenta 8 bits | Se tienen en cuenta 8 bits | Se tienen en cuenta 3 bits, se ignoran 5 | Ignorados |

**Wildcard: 0.0.31.255**

Cálculo rápido: reste la máscara de subred 255.255.224.0 al valor 255.255.255.255:

```text
  255.255.255.255
- 255.255.224.000
= 000.000.031.255
```

El resultado es la máscara wildcard 0.0.31.255.

## Proceso de configuración de las ACL numeradas

El proceso de creación de una ACL se lleva a cabo creando la lista y posteriormente asociándola a una interfaz entrante o saliente.

Las ACL numeradas llevan un número identificativo que las identifica según sus características. La siguiente tabla muestra los rangos de listas de acceso numeradas:

| ACL | Rango | Rango extendido |
| --- | --- | --- |
| IP estándar | 1-99 | 1300-1999 |
| IP extendida | 100-199 | 2000-2699 |
| Prot, type code | 200-299 | |
| DECnet | 300-399 | |
| XNS estándar | 400-499 | |
| XNS extendida | 500-599 | |
| Apple Talk | 600-699 | |
| Ethernet | 700-799 | |
| IPX estándar | 800-899 | |
| IPX extendida | 900-999 | |
| Filtros Sap | 1000-1099 | |

### Configuración de ACL estándar

Las listas de acceso IP estándar verifican solo la dirección de origen en la cabecera del paquete IP (capa 3).

```text
Router(config)#access-list {1-99} {permit|deny} {dirección de origen} {máscara comodín}
```

Donde:

- **1-99:** identifica el rango y número de lista.
- **Permit|deny:** indica si esta entrada permitirá o bloqueará el tráfico a partir de la dirección origen.
- **Dirección de origen:** identifica la dirección IP de origen.
- **Máscara comodín (wildcard):** identifica los bits del campo de la dirección que serán comprobados.

!!! note "NOTA"
    La máscara predeterminada es 0.0.0.0 (coincidencia de todos los bits).

Una vez configurada asocie la ACL estándar a la interfaz a través del siguiente comando dentro del modo de dicha interfaz.

```text
Router(config-if)#ip access-group {Nº de ACL} {in|out}
```

Donde:

- **Número de lista de acceso:** indica el número de lista de acceso que será aplicada a esa interfaz.
- **In|out:** selecciona si la lista de acceso se aplicará como filtro de entrada o de salida.

### Configuración de ACL extendida

Las listas de acceso IP extendidas pueden verificar otros muchos elementos, incluidas opciones de la cabecera del segmento (capa 4), como los números de puerto. Direcciones IP de origen y destino, protocolos específicos. Números de puerto TCP y UDP.

El proceso de configuración de una ACL IP extendida es el siguiente:

```text
Router(config)#access-list {100-199} {permit|deny} {protocolo} {dirección de origen} {máscara comodín} {dirección de destino} {máscara comodín} {puerto} {established} {log}
```

- **100-199:** identifica el rango y número de lista.
- **Permit|deny:** indica si la entrada permitirá o bloqueará el tráfico desde la dirección origen hacia el destino.
- **Protocolo:** como por ejemplo IP, TCP, UDP, ICMP.
- **Dirección origen, dirección destino:** identifican direcciones IP de origen y destino.
- **Máscara comodín:** son las máscaras wildcard. Identifica los bits del campo de la dirección que serán comprobados.
- **Puerto (opcional):** puede ser, por ejemplo, `lt` (menor que), `gt` (mayor que), `eq` (igual a), o `neq` (distinto que) y un número de puerto de protocolo correspondiente.
- **Established (opcional):** se usa solo para TCP de entrada. Esto permite que el tráfico TCP pase si el paquete utiliza una conexión ya establecida (por ejemplo, posee un conjunto de bits ACK).
- **Log (opcional):** envía un mensaje de registro a la consola a un servidor syslog determinado.

Algunos de los números de puerto más conocidos, se detallan con mayor profundidad más adelante:

| Puerto | Servicio | Puerto | Servicio |
| --- | --- | --- | --- |
| 21 | FTP | 69 | tftp |
| 23 | Telnet | 53 | dns |
| 25 | smtp | 80 | http |
| | | 109 | pop 2 |

La asociación de las ACL a una interfaz en particular se realiza en el modo de interfaz aplicando el siguiente comando.

```text
Router(config-if)#ip access-group {Nº de ACL} {in|out}
```

Donde:

- **Número de lista de acceso:** indica el número de lista de acceso que será aplicada a esa interfaz.
- **In|out:** selecciona si la lista de acceso se aplicará como filtro de entrada o de salida.

### Configuración de una ACL en la línea de telnet

Para evitar intrusiones no deseadas en las conexiones de telnet se puede crear una lista de acceso estándar y asociarla a la Line VTY. El proceso de creación se lleva a cabo como una ACL estándar denegando o permitiendo un origen hacia esa interfaz. El modo de asociar la ACL a la Línea de telnet es el siguiente:

```text
router(config)#line vty 0 4
router(config-line)#access-class {Nº de ACL} {in|out}
```

### Mensajes de registro en las ACL

Al final de una sentencia ACL, el administrador tiene la opción de configurar el parámetro `log`. Cuando este parámetro se configura, se comparan los paquetes en búsqueda de una coincidencia con la sentencia. El dispositivo registra en una función de registro habilitada, como la consola, el buffer interno del router o un servidor syslog. Los mensajes de registro se generan en la primera coincidencia de paquete y luego en intervalos de cinco minutos.

La habilitación del parámetro `log` en una ACL puede afectar seriamente al rendimiento del dispositivo. Cuando se habilita el registro, los paquetes son transmitidos por conmutación de proceso o por conmutación rápida. El parámetro `log` debe ser usado solamente si la red está bajo ataque y el administrador está intentando determinar quién es el atacante. En este punto, el administrador debe habilitar el registro por el tiempo que sea necesario para reunir la información suficiente y luego deshabilitarlo.

El siguiente ejemplo muestra los mensajes emergentes de una ACL extendida configurada con el parámetro `log`.

```text
01:24:23:%SEC-6-IPACCESSLOGDP:list ext1 permitted icmp 10.1.1.15 -> 10.1.1.61 (0/0), 1 packet
01:25:14:%SEC-6-IPACCESSLOGDP:list ext1 permitted icmp 10.1.1.15 -> 10.1.1.61 (0/0), 7 packets
01:26:12:%SEC-6-IPACCESSLOGP:list ext1 denied udp 0.0.0.0(0) -> 255.255.255.255(0), 1 packet
01:31:33:%SEC-6-IPACCESSLOGP:list ext1 denied udp 0.0.0.0(0) -> 255.255.255.255(0), 8 packets
```

### Comentarios en las ACL

Las ACL permiten agregar comentarios para facilitar su comprensión o funcionamiento. El comando `remark` no actúa sobre las sentencias de las ACL pero brindan a los técnicos la posibilidad de una visión rápida sobre la actividad de las listas.

Los comentarios pueden agregarse tanto a las ACL nombradas como también a las numeradas, la clave reside en agregar los comentarios antes de la configuración de los permisos o denegaciones.

La sintaxis muestra una ACL nombrada con el comando `remark`:

```text
Router(config)#ip access-list {standard|extended} nombre
Router(config-std-nacl)#remark comentario
```

La sintaxis muestra una ACL numerada con el comando `remark`:

```text
Router(config)#ip access-list {número} remark comentario
```

## Listas de acceso IP con nombre

Con listas de acceso IP numeradas, para modificar una lista tendría que borrar primero la lista de acceso y volver a introducirla de nuevo con las correcciones necesarias. En una lista de acceso numerada no es posible borrar instrucciones individuales. Las listas de acceso IP con nombre permiten eliminar entradas individuales de una lista específica. El borrado de entradas individuales permite modificar las listas de acceso sin tener que eliminarlas y volver a configurarlas desde el principio. Sin embargo, no es posible insertar elementos selectivamente en una lista.

### Configuración de una lista de acceso nombrada

Básicamente, la configuración de una ACL nombrada es igual a las extendidas o estándar numeradas. Si se agrega un elemento a la lista, este se coloca al final de la misma. No es posible usar el mismo nombre para varias listas de acceso. Las listas de acceso de diferentes tipos tampoco pueden compartir nombre.

```text
Router(config)#ip access-list {standard|extended} nombre
Router(config-std-nacl)#{permit|deny} {condiciones de prueba}
Router(config)#Interfaz asociación de la ACL
Router(config-if)#ip access-group nombre {in|out}
```

Para eliminar una instrucción individual, anteponga `no` a la condición de prueba.

```text
Router(config-std-nacl)#no {permit|deny} {condiciones de prueba}
```

## Eliminación de las ACL

Una ACL puede ser modificada sin necesidad de desasociarla de la interfaz si luego mantiene el mismo número o nombre. Para eliminar una ACL anteponga el parámetro `no` a los comandos de configuración y vuelva a crear la ACL:

```text
Router(config)#no access-list {Nº de lista de acceso}
Router(config)#no ip access-list {standard|extended} nombre
```

Si fuese necesario eliminarla completamente siga el siguiente orden de configuración:

1. Desde el modo interfaz donde se aplicó la lista desasociar dicha ACL anteponiendo un `no` al comando. Tenga en cuenta que en una interfaz puede tener asociadas varias ACL.
2. Posteriormente desde el modo global elimine la ACL.

## Listas de acceso IPv6

El desempeño de las ACL estándar IPv6 es idéntico a las ACL IPv4. A partir de las IOS versión 12.0(23)S y 12.2(13)T o versiones posteriores esto se amplía también a las ACL extendidas. Para configurar una ACL IPv6, en primer lugar se debe entrar en el modo de configuración de ACL IPv6.

```text
Router(config)# ipv6 access-list nombre
```

A continuación, configurar cada entrada de la lista de acceso para permitir o denegar tráfico específico.

```text
Router(config-ipv6-acl)# {permit | deny} protocol {source-ipv6-prefix/prefix-length | any | host source-ipv6-address | auth} [operator port] {destination-ipv6-prefix/prefix-length | any | host destination-ipv6-address | auth} [operator port]
```

Una vez creada la ACL se debe aplicar a una interfaz específica de entrada o salida.

```text
Router(config-if)# ipv6 traffic-filter nombre {in | out}
```

La denegación implícita al final de cada ACL también está presente en las ACL IPv6, pero además hay algunos hechos adicionales a tener en cuenta.

- Cada ACL IPv6 contiene normas implícitas para permitir el descubrimiento de vecinos de IPv6. El proceso de descubrimiento de vecinos se sirve de la capa de red IPv6.
- Las ACL IPv6, por defecto, permiten enviar y recibir paquetes IPv6 en una interfaz.
- Las listas de acceso IPv6 niegan implícitamente todos los servicios que no estén específicamente permitidos.
- Las reglas sobre el descubrimiento de vecinos IPv6 funcionan de manera similar a como lo hace ARP en IPv4. Estas reglas no se modifican aún cuando se aplica una ACL a una interfaz.

Las sentencias implícitas que se agregan al final de cada ACL IPv6 son las siguientes:

```text
permit icmp any any nd-na
permit icmp any any nd-ns
deny ipv6 any any
```

Donde:

- **nd-na** (*Neighbor Discovery-Neighbor Advertisement*): esta instrucción permite enviar los mensajes na que sirven para descubrir las direcciones de capa 2 de otros nodos.
- **nd-ns** (*Neighbor Discovery-Neighbor Solicitation*): esta instrucción permite recibir los mensajes ns que llegan como respuesta al mensaje na enviado previamente.

Estas reglas de descubrimiento de vecinos pueden ser modificadas anteponiendo la instrucción explícita `deny ipv6 any any`. En el caso de añadir una denegación explícita como esta, tendrá prioridad sobre los permisos implícitos sobre el descubrimiento de vecinos.

La siguiente sintaxis es un ejemplo de una configuración básica de una ACL IPv6 nombrada "CCNA". En letras resaltadas en gris se detallan las sentencias implícitas.

```text
Switch(config)# ipv6 access-list CCNA
Switch(config-ipv6-acl)# deny tcp any any gt 5000
Switch(config-ipv6-acl)# deny ::/0 lt 5000 ::/0 log
Switch(config-ipv6-acl)# permit icmp any any
Switch(config-ipv6-acl)# permit any any
Switch(config-ipv6-acl)# permit icmp any any nd-na
Switch(config-ipv6-acl)# permit icmp any any nd-ns
Switch(config-ipv6-acl)# deny ipv6 any any
Switch(config-ipv6-acl)# exit
Switch(config)# interface gigabitethernet 1/0/3
Switch(config-if)# no switchport
Switch(config-if)# ipv6 address 2001::/64 eui-64
Switch(config-if)# ipv6 traffic-filter CCNA out
```

## Otros tipos de listas de acceso

### Listas de acceso dinámicas

Este tipo de ACL depende de telnet a partir de la autenticación de los usuarios que quieran atravesar el router y que han sido previamente bloqueados por una ACL extendida. Una ACL dinámica añadida a la ACL extendida existente permitirá tráfico a los usuarios que son autenticados en una sesión de telnet por un período de tiempo en particular.

### Listas de acceso reflexivas

Permiten el filtrado de paquetes IP en función de la información de la sesión de capa superior. Mayormente se utilizan para permitir el tráfico saliente y para limitar el entrante en respuesta a las sesiones originadas dentro del router.

### Listas de acceso basadas en tiempo

Este tipo de ACL permite la configuración para poner en actividad el filtrado de paquetes solo en períodos de tiempo determinados por el administrador. En algunos casos puede ser muy útil la utilización de ACL en algunos momentos del día o particularmente en solo algunos días de la semana.

## Puertos y protocolos más utilizados en las ACL

### Puertos TCP

| Número de puerto | Comando | Protocolo |
| --- | --- | --- |
| 7 | echo | Echo |
| 9 | discard | Discard |
| 13 | daytime | Daytime |
| 19 | chargen | Character Generator |
| 20 | ftp-data | FTP Data Connections |
| 21 | ftp | File Transfer Protocol |
| 23 | telnet | Telnet |
| 25 | smtp | Simple Mail Transport Protocol |
| 37 | time | Time |
| 53 | domain | Domain Name Service |
| 43 | whois | Nicname |
| 49 | tacacs | TAC Access Control System |
| 70 | gopher | Gopher |
| 79 | finger | Finger |
| 80 | www-http | World Wide Web |
| 101 | hostname | NIC Hostname Server |
| 109 | pop2 | Post Office Protocol v2 |
| 110 | pop3 | Post Office Protocol v3 |
| 111 | sunrpc | Sun Remote Procedure Call |
| 113 | ident | Ident Protocol |
| 119 | nntp | Network News Transport Protocol |
| 179 | bgp | Border Gateway Protocol |
| 194 | irc | Internet Relay Chat |
| 496 | pim-auto-rp | PIM Auto-RP |
| 512 | exec | Exec |
| 513 | login | Login |
| 514 | cmd | Remote commands |
| 515 | lpd | Printer service |
| 517 | talk | Talk |
| 540 | uucp | Unix-to-Unix Copy Program |

### Puertos UDP

| Número de puerto | Comando | Protocolo |
| --- | --- | --- |
| 7 | echo | Echo |
| 9 | discard | Discard |
| 37 | time | Time |
| 42 | nameserver | IEN116 name service |
| 49 | tacacs | TAC Access Control System |
| 53 | domain | Domain Name Service |
| 67 | bootps | Bootstrap Protocol server |
| 68 | bootpc | Bootstrap Protocol client |
| 69 | tftp | Trivial File Transfer Protocol |
| 111 | sunrpc | Sun Remote Procedure Call |
| 123 | ntp | Network Time Protocol |
| 137 | netbios-ns | NetBios name service |
| 138 | netbios-dgm | NetBios datagram service |
| 139 | netbios-ss | NetBios Session Service |
| 161 | snmp | Simple Network Management Protocol |
| 162 | snmptrap | SNMP Traps |
| 177 | xdmcp | X Display Manager Control Protocol |
| 195 | dnsix | DNSIX Security Protocol Auditing |
| 434 | mobile-ip | Mobile IP Registration |
| 496 | pim-auto-rp | PIM Auto-RP |
| 500 | isakmp | Internet Security Association and Key Management Protocol |
| 512 | biff | Biff |
| 513 | who | Who Service |
| 514 | syslog | System Logger |
| 517 | talk | Talk |
| 520 | rip | Routing Information Protocol |

### Protocolos

| Comando | Descripción |
| --- | --- |
| `eigrp` | Cisco EIGRP routing protocol |
| `gre` | Cisco GRE tunneling |
| `icmp` | Internet Control Message Protocol |
| `igmp` | Internet Gateway Message Protocol |
| `ip` | Any Internet Protocol |
| `ospf` | OSPF routing protocol |
| `pcp` | Payload Compression Protocol |
| `tcp` | Transmission Control Protocol |
| `udp` | User Datagram Protocol |

El esquema muestra la jerarquía de los protocolos más utilizados en las listas de acceso.

## Verificación de las ACL

Verifica si una lista de acceso está asociada a una interfaz:

```text
Router#show ip interface tipo número
```

Muestra información de la interfaz IP:

```text
Router#show access-list
```

Muestra información general de las ACL y de las interfaces asociadas:

```text
Router#running-config
```

Muestra contenido de todas las listas de acceso:

```text
Router#show access-lists
```

```text
Standard IP access list 10
 deny 192.168.1.0
Extended IP access list 120
 deny tcp host 204.204.10.1 any eq 80
 permit ip any any
Extended IP access list INTRANET
 deny tcp any any eq 21 log
 permit ip any any
```

```text
Router#show [protocolo] access-list [número|nombre]
```

Muestra los eventos de log:

```text
Router# show logging
Syslog logging: enabled (0 messages dropped, 0 flushes, 0 overruns)
Console logging: level debugging, 37 messages logged
Monitor logging: level debugging, 0 messages logged
Buffer logging: level debugging, 37 messages logged
File logging: disabled
Trap logging: level debugging, 39 message lines logged
Log Buffer (4096 bytes):00:00:48: NTP: authentication delay calculation problems
00:09:34:%SEC-6-IPACCESSLOGS:list stan1 permitted 0.0.0.0 1 packet
00:09:59:%SEC-6-IPACCESSLOGS:list stan1 denied 10.1.1.15 1 packet
00:10:11:%SEC-6-IPACCESSLOGS:list stan1 permitted 0.0.0.0 1 packet
```

!!! tip "RECUERDE"
    Las listas de acceso extendidas deben colocarse normalmente lo más cerca posible del origen del tráfico que será denegado, mientras que las estándar, lo más cerca posible del destino.

!!! tip "RECUERDE"
    - Una lista de acceso puede ser aplicada a múltiples interfaces.
    - Solo puede haber una lista de acceso por protocolo, por dirección y por interfaz.
    - Es posible tener varias listas para una interfaz, pero cada una debe pertenecer a un protocolo diferente.
    - Organice las listas de acceso de modo que las referencias más específicas a una red o subred aparezcan delante de las más generales.
    - Coloque las condiciones de cumplimiento más frecuentes antes de las menos habituales.
    - Las adiciones a las listas se agregan siempre al final de estas, pero siempre delante de la condición de denegación implícita.
    - No es posible agregar ni eliminar selectivamente instrucciones de una lista cuando se usan listas de acceso numeradas, pero sí cuando se usan listas de acceso IP con nombre.
    - A menos que termine una lista de acceso con una condición de permiso implícito de todo, se denegará todo el tráfico que no cumpla ninguna de las condiciones establecidas en la lista al existir un `deny` implícito al final de cada lista.
    - Toda lista de acceso debe incluir al menos una instrucción `permit`. En caso contrario, todo el tráfico será denegado.
    - Cree una lista de acceso antes de aplicarla a la interfaz. Una interfaz con una lista de acceso inexistente o indefinida aplicada al mismo permitirá todo el tráfico.
    - Las listas de acceso permiten filtrar solo el tráfico que pasa por el router. No pueden hacer de filtro para el tráfico originado por el propio router.

!!! tip "RECUERDE"
    El orden en el que aparecen las instrucciones en la lista de acceso es fundamental para un filtrado correcto. La práctica recomendada consiste en crear las listas de acceso usando un editor de texto y descargarlas después en un router vía TFTP o copiando y pegando el texto.

    Las listas de acceso se procesan de arriba a abajo. Si coloca las pruebas más específicas y las que se verificarán con más frecuencia al comienzo de la lista de acceso, se reducirá la carga de procesamiento. Solo las listas de acceso con nombre permiten la supresión, aunque no la alteración del orden de instrucciones individuales en la lista. Si desea reordenar las instrucciones de una lista de acceso, deberá eliminar la lista completa y volver a crearla en el orden apropiado o con las instrucciones correctas.

## Caso práctico

### Cálculo de wildcard

Las wildcard también permiten identificar rangos simplificando la cantidad de comandos a introducir, en este ejemplo la wildcard debe identificar el rango de subredes entre la 172.16.16.0/24 y la 172.16.31.0/24.

Al ser una red clase B con máscara de clase C, se debe trabajar en el tercer octeto en el rango entre 16 y 31, por lo tanto, la wildcard será: `0.0.15.255`.

### Configuración de una ACL estándar

Se ha denegado en el router remoto la red 192.168.1.0 y luego se ha permitido a cualquier origen, posteriormente se asoció la ACL a la interfaz Serial 0/0 como saliente.

```text
Router#configure terminal
Router(config)#access-list 10 deny 192.168.1.0 0.0.0.0
Router(config)#access-list 10 permit any
Router(config)#access-list 10 remark ACL estandar
Router(config)#interface serial 0/0
Router(config-if)#ip access-group 10 out
```

### Configuración de una ACL extendida

Se ha denegado al host A, 204.204.10.1 (identificándolo con la abreviatura "host") hacia el puerto 80 de cualquier red de destino (usando el término `any`). Posteriormente se permite todo tráfico IP. Esta ACL se asoció a la interfaz ethernet 0/1 como entrante.

```text
Router(config)#access-list 120 deny tcp host 204.204.10.1 any eq 80
Router(config)#access-list 120 permit ip any any
Router(config)#access-list 120 remark ACL extendida
Router(config)#interface ethernet 0/1
Router(config-if)#ip access-group 120 in
```

### Configuración de una ACL con subred

En el siguiente caso la subred 200.20.10.64/29 tiene denegado el acceso de todos sus hosts en el protocolo UDP, mientras que los restantes protocolos y otras subredes tienen libre acceso. La ACL es asociada a la ethernet 0/0 como entrante. Observe la wildcard utilizada en este caso.

```text
Router(config)#access-list 100 deny udp 200.20.10.64 0.0.0.7 any
Router(config)#access-list 100 permit ip any any
Router(config)#interface ethernet 0/0
Router(config-if)#ip access-group 100 in
```

Procedimiento para hallar la máscara comodín de la subred:

```text
200.20.10.64/29 es lo mismo que 200.20.10.64 255.255.255.248
  255.255.255.255
- 255.255.255.248
= 000.000.000.007
Wildcard: 0.0.0.7
```

### Configuración de una ACL nombrada

Se creó una ACL con el nombre INTRANET que deniega todo tráfico de cualquier origen a cualquier destino hacia el puerto 21, luego se permite cualquier otro tráfico IP. Se usó el comando `log` (opcional) para enviar información de la ACL a un servidor. Se asocia a la interfaz ethernet 1 como saliente.

```text
Router(config)#ip access-list extended INTRANET
Router(config-ext-nacl)#deny tcp any any eq 21 log
Router(config-ext-nacl)#permit ip any any
Router(config-ext-nacl)#exit
Router(config)#interface ethernet 1
Router(config-if)#ip access-group INTRANET out
```

!!! tip "RECUERDE"
    Al final de cada ACL existe una negación implícita. Debe existir al menos un `permit`.

### Modificación de una ACL IPv6

En el siguiente escenario un técnico principiante ha instalado una ACL en la interfaz Gi0/0 en R1 denegando cierto tráfico en la dirección 2001:db8:a:b::7. PC2 es el único terminal que puede realizar telnet hacia al servidor DHCP, pero no puede.

En primer lugar se debe verificar si al ACL está asociada a la interfaz correcta y de qué manera, si entrante o saliente. Se ejecuta el comando `show ipv6 interface`.

```text
R1# show ipv6 interface gigabitEthernet 0/0
GigabitEthernet0/0 is up, line protocol is up
  IPv6 is enabled, link-local address is FE80::C808:3FF:FE78:8
  No Virtual link-local address(es):
  Global unicast address(es):
    2001:DB8:A:A::1, subnet is 2001:DB8:A:A::/64
  Joined group address(es):
    FF02::1
    FF02::2
    FF02::1:2
    FF02::1:FF00:1
    FF02::1:FF78:8
  MTU is 1500 bytes
  ICMP error messages limited to one every 100 milliseconds
  ICMP redirects are enabled
  ICMP unreachables are sent
  Input features: Access List
    Inbound access list CCNA
  ND DAD is enabled, number of DAD attempts: 1
  ND reachable time is 30000 milliseconds (using 30000)
  ND RAs are suppressed (all)
  Hosts use stateless autoconfig for addresses.
  Hosts use DHCP to obtain other configuration.
```

En la interfaz Gi0/0 en R1 se ve claramente que existe una ACL IPv6 nombrada CCNA asociada de manera entrante a la interfaz. Ahora lo que necesita es verificar la configuración de la ACL IPv6 nombrada CCNA.

```text
R1# show ipv6 access-list CCNA
IPv6 access list CCNA
 deny tcp any host 2001:DB8:A:B::7 eq telnet (6 matches) sequence 10
 permit tcp host 2001:DB8:A:A::20 host 2001:DB8:A:B::7 eq telnet sequence 20
 permit tcp host 2001:DB8:A:A::20 host 2001:DB8:D::1 eq www sequence 30
 permit ipv6 2001:DB8:A:A::/64 any (67 matches) sequence 40
```

Analizando la ACL se observa que la secuencia 10 es una sentencia negando a todos los dispositivos realizar telnet hacia la 2001:db8:a:b::7, la secuencia 20 es un permiso de PC2 para realizar telnet en la 2001:db8:a:b::7. Recuerde que las ACL IPv6 se procesan de arriba hacia abajo, y una vez que se encuentra una coincidencia, se ejecuta inmediatamente. Una entrada más general denegando telnet está colocada antes de una entrada más específica que permite a PC2.

Para resolver el problema, en R1, desde el modo de configuración para la ACL IPv6 nombrada CCNA, quite la secuencia 20 y añada la misma entrada con un número de secuencia inferior para ubicarla antes de la secuencia 10, por ejemplo, 5.

```text
R1# config t
Enter configuration commands, one per line. End with CNTL/Z.
R1(config)# ipv6 access-list CCNA
R1(config-ipv6-acl)# no sequence 20
R1(config-ipv6-acl)# seq 5 permit tcp host 2001:DB8:A:A::20 host 2001:DB8:A:B::7 eq telnet
```

Verifique la nueva configuración de la ACL IPv6 nombrada CCNA.

```text
R1# show ipv6 access-list CCNA
IPv6 access list CCNA
 permit tcp host 2001:DB8:A:A::20 host 2001:DB8:A:B::7 eq telnet sequence 5
 deny tcp any host 2001:DB8:A:B::7 eq telnet (6 matches) sequence 10
 permit tcp host 2001:DB8:A:A::20 host 2001:DB8:D::1 eq www sequence 30
 permit ipv6 2001:DB8:A:A::/64 any (67 matches) sequence 40
```

Después de aplicar los cambios en R1, PC2 realiza telnet con éxito.

## Fundamentos para el examen

- Tenga claro cuáles son las amenazas, ataques y vulnerabilidades de una red corporativa y como mitigarlos.
- Recuerde cuales son los objetivos principales de la seguridad de la red.
- Estudie las características de cada tipo de firewall y de los NGFW.
- Entienda el concepto de DMZ.
- Estudie las características de los IPS y de los NGIPS.
- Analice el funcionamiento de las firmas IPS.
- Analice el funcionamiento de un firewall basado en zonas y cómo responden las interfaces en cada una de las zonas.
- Estudie que es y cómo funciona AAA, RADIUS y TACACS, compárelos.
- Recuerde cómo funciona la característica DHCP Snooping.
- Estudie la configuración y la teoría de como asegurar un puerto.
- Recuerde los fundamentos para el filtrado y administración del tráfico IP.
- Memorice las pruebas de condiciones que efectúa el router y cuáles son los resultados en cada caso.
- Estudie los tipos de ACL, su asociación con las interfaces del router y cuál es la manera más adecuada para aplicarlas.
- Estudie y analice la función de las máscaras comodín y su efecto en las ACL.
- Memorice los rangos de las ACL numeradas.
- Memorize los números de puertos básicos empleados en la configuración de las ACL.
- Recuerde que existen otros tipos de ACL, sepa cuáles son.
- Compare las diferencias entre las ACL IPv4 y ACL IPv6.
- Memorice los comandos para las configuraciones de todas las ACL, teniendo en cuenta las condiciones fundamentales para su correcto funcionamiento, incluidos los comandos para su visualización.
- Recuerde que existe un tipo especial de ACL para telnet.
- Ejercite todo lo que pueda con las wildcard.
- Ejercite todas las configuraciones en dispositivos reales o en simuladores.
