# Configuración de enrutamiento

## Enrutamiento estático

Para que un dispositivo de capa tres pueda determinar la ruta hacia un destino debe tener conocimiento de las diferentes rutas hacia él y cómo hacerlo. El aprendizaje y la determinación de estas rutas se lleva a cabo mediante un proceso de enrutamiento dinámico a través de cálculos y algoritmos que se ejecutan en la red, o enrutamiento estático ejecutado manualmente por el administrador, o incluso ambos métodos.

### Enrutamiento estático IPv4

La configuración de las rutas estáticas se realiza a través del comando de configuración global de IOS `ip route`. El comando utiliza varios parámetros, entre los que se incluyen la dirección de red y la máscara de red asociada, así como información acerca del lugar al que deberían enviarse los paquetes destinados para dicha red.

La información de destino puede adoptar una de las siguientes formas:

- Una dirección IP específica del siguiente router de la ruta.
- La dirección de red de otra ruta de la tabla de enrutamiento a la que deben reenviarse los paquetes.
- Una interfaz conectada directamente en la que se encuentra la red de destino.

```text
Router(config)# ip route [dirección IP de la red destino + máscara] [IP del primer salto/interfaz de salida] [distancia administrativa] [permanent]
```

Donde:

- **dirección IP de la red destino+máscara:** hace referencia a la red a la que se pretende tener acceso y su correspondiente máscara de red o subred. Si el destino es un host específico se debe identificar la red a la que pertenece dicho host.
- **IP del primer salto/interfaz de salida:** se debe elegir entre configurar la IP del próximo salto (hace referencia a la dirección IP de la interfaz del siguiente router) o el nombre de la interfaz del propio router por donde saldrán los paquetes hacia el destino. Por ejemplo, si el administrador no conoce o tiene dudas acerca del próximo salto utilizará su propia interfaz de salida, de lo contrario es conveniente hacerlo con la IP del próximo salto.
- **distancia administrativa:** parámetro opcional (de 1 a 255) que si no se configura será igual a 1. Este valor hará que si existen más rutas estáticas o protocolos de enrutamiento configurados en el router, cada uno de estos tendrá mayor o menor importancia según sea el valor de su distancia administrativa. Cuanto más baja, mayor importancia.

Las entradas creadas en la tabla de enrutamiento usando este procedimiento permanecerán en dicha tabla mientras la ruta siga activa. Con la opción `permanent`, la ruta seguirá en la tabla aunque la ruta en cuestión haya dejado de estar activa.

Las situaciones típicas donde se recomienda la utilización de las rutas estáticas pueden ser las siguientes:

- Cuando un circuito de datos es especialmente poco fiable y deja de funcionar constantemente. En estas circunstancias, un protocolo de enrutamiento dinámico podrá producir demasiada inestabilidad, mientras que las rutas estáticas no cambian.
- Cuando existe una sola conexión con un solo ISP. En lugar de conocer todas las rutas globales de Internet, se utiliza una sola ruta estática.
- Cuando solo se puede acceder a una red a través de una conexión de acceso telefónico. Dicha red no puede proporcionar las actualizaciones constantes que requieren un protocolo de enrutamiento dinámico.
- Cuando un cliente o cualquier otra red vinculada no desean intercambiar información de enrutamiento dinámico. Se puede utilizar una ruta estática para proporcionar información acerca de la disponibilidad de dicha red.

La sintaxis muestra una ruta estática que apunta a la red 172.16.0.0 hacia el próximo salto 200.200.10.1 con una distancia administrativa de 120.

```text
Router_B(config)# ip route 172.16.0.0 255.255.0.0 200.200.10.1 120
```

La sintaxis muestra una ruta estática que apunta a la red 172.16.0.0 saliendo por la interfaz serial 0 del propio router con una distancia administrativa de 120.

```text
Router_B(config)# ip route 172.16.0.0 255.255.0.0 serial 0 120
```

#### Rutas estáticas por defecto

Cuando el destino al que se pretende llegar son múltiples redes o no se conocen, se pueden crear rutas estáticas por defecto como lo muestra la siguiente sintaxis:

```text
Router(config)# ip route 0.0.0.0 0.0.0.0 [IP del primer salto/interfaz de salida] [distancia administrativa]
```

```text
Router_B(config)# ip route 0.0.0.0 0.0.0.0 serial 0
```

Observe que los parámetros de configuración, en lugar de una dirección de red específica de destino, se utilizan ceros en los octetos de red y máscara; el resto de los parámetros serán iguales a las rutas estáticas convencionales.

#### Red de último recurso

Cuando la información de enrutamiento dinámico no se intercambia con una entidad externa, como puede ser un ISP, la configuración de una red de último recurso suele ser la forma más fácil de generar una ruta predeterminada. Los protocolos de enrutamiento redistribuyen la información sobre la existencia de una red como ruta predeterminada.

El comando `ip default-network` es la forma más apropiada de designar una o varias rutas de red predeterminadas posibles.

La siguiente sintaxis muestra la configuración de una red por defecto o de último recurso:

```text
Router(config)# ip default-network [dirección IP de la red de último recurso]
```

Los routers que no intercambian información de enrutamiento dinámico o que se encuentran en conexiones de acceso telefónico, como RDSI o SVC de Frame-Relay, deben configurarse como una ruta predeterminada por defecto.

### Enrutamiento estático IPv6

Las rutas estáticas IPv6 siguen el mismo concepto de configuración que las IPv4. El router debe tener el enrutamiento IPv6 previamente habilitado, el comando `ipv6 route` inicia el proceso de configuración de la ruta estática.

La siguiente es la sintaxis del comando abreviado:

```text
Router(config)# ipv6 route [IPv6 de la red destino/prefijo] [IP del primer salto/interfaz de salida] [distancia administrativa]
```

La ruta estática apunta hacia la red 2001:0DB8::/32, saliendo por la interfaz giga0/1 y con una distancia administrativa de 120.

```text
Router(config)# ipv6 route 2001:0DB8::/32 gigabitethernet0/1 120
```

Al igual que las rutas estáticas IPv4 puede elegirse para la configuración la interfaz local de salida o la IPv6 del próximo salto. La RFC 2461, *Neighbor Discovery for IPv6*, especifica que un router debe ser capaz de identificar la dirección de enlace local de los routers vecinos, pero para rutas estáticas la dirección del próximo salto debe ser configurada como la dirección link-local del router vecino.

Las rutas por defecto se representan en el parámetro de la dirección de la siguiente manera `::/0`.

Un ejemplo de una ruta estática que sale por la interfaz Giga0/0 se configura de la siguiente manera:

```text
Router(config)# ipv6 route ::/0 GigabitEthernet0/0
```

!!! tip "RECUERDE"

    En las rutas estáticas el valor de la distancia administrativa por defecto es 1. Cuando se configuran como respaldo al enrutamiento dinámico la distancia administrativa debe ser mayor que la del protocolo.

## Enrutamiento dinámico

Si se diseñasen redes que utilizaran exclusivamente rutas estáticas sería tedioso administrarlas y no responderían bien a las interrupciones y a los cambios de topología que suelen suceder con cierta frecuencia. Para responder a estos problemas se desarrollaron los protocolos de enrutamiento dinámico.

Los protocolos de enrutamiento dinámico son algoritmos que permiten que los routers publiquen, o anuncien, la existencia de la información de ruta de red IP necesaria para crear la tabla de enrutamiento. Dichos algoritmos también determinan el criterio de selección de la ruta que sigue el paquete cuando se le presenta al router esperando una decisión de conmutar. Los objetivos del protocolo de enrutamiento consisten en proporcionar al usuario la posibilidad de seleccionar la ruta idónea en la red, reaccionar con rapidez a los cambios de la misma y realizar dichas tareas de la manera más sencilla y con la menor sobrecarga del router posible.

Los protocolos de enrutamiento dinámico se configuran en un router para poder describir y administrar dinámicamente las rutas disponibles en la red. Para habilitar un protocolo de enrutamiento dinámico, se han de realizar las siguientes tareas:

- Seleccionar un protocolo de enrutamiento.
- Seleccionar las redes IP que serán anunciadas.
- Asignar direcciones de red/subred y las máscaras de subred apropiadas a las distintas interfaces.

El enrutamiento dinámico utiliza difusiones y multidifusiones para comunicarse con otros routers.

El comando `router` es el encargado de iniciar el proceso de enrutamiento, posteriormente se asocian las redes con el comando `network`.

## RIP

RIP (*Routing Information Protocol*) es uno de los protocolos de enrutamiento más antiguos utilizados por dispositivos basados en IP. Su implementación original fue para el protocolo Xerox a principios de los ochenta. Ganó popularidad cuando se distribuyó con UNIX como protocolo de enrutamiento para esa implementación TCP/IP.

RIP es un protocolo vector de distancia que utiliza la cuenta de saltos del router como métrica. La cuenta de saltos máxima de RIP es 15. Cualquier ruta que exceda de los 15 saltos se etiqueta como inalcanzable al establecerse la cuenta de saltos en 16. En RIP la información de enrutamiento se propaga de un router a los otros vecinos por medio de una difusión de IP usando el protocolo UDP y el puerto 520.

El protocolo RIPv1 es un protocolo de enrutamiento con clase que no admite la publicación de la información de la máscara de red. El protocolo RIPv2 es un protocolo sin clase que admite CIDR, VLSM, resumen de rutas y seguridad mediante texto simple y autenticación MD5.

Algunas características comparativas entre RIPv1 y RIPv2 son las siguientes:

- RIP es un protocolo de enrutamiento basado en vectores distancia.
- RIP utiliza el número de saltos como métrica para la selección de rutas.
- El número máximo de saltos permitido en RIP es 15.
- RIP difunde actualizaciones de enrutamiento por medio de la tabla de enrutamiento completa cada 30 segundos, por omisión.
- RIP puede realizar equilibrado de carga en un máximo de seis rutas de igual coste (la especificación por omisión es de cuatro rutas).
- RIPv1 requiere que se use una sola máscara de red para cada número de red de clase principal que es anunciado. La máscara es una máscara de subred de longitud fija. El estándar RIPv1 no contempla actualizaciones desencadenadas.
- RIPv2 permite la utilización de VLSM. El estándar RIPv2 permite actualizaciones desencadenadas, a diferencia de RIPv1. La definición del número máximo de rutas paralelas permitidas en la tabla de enrutamiento faculta a RIP para llevar a cabo el equilibrado de carga.

El proceso de configuración de RIP es bastante simple, una vez iniciado el proceso de configuración se deben especificar las redes que participan en el enrutamiento. Si es necesario la versión y el balanceo de ruta.

```text
Router(config)# router rip
Router(config-router)# network dirección de red
Router(config-router)# version versión
Router(config-router)# maximum-paths número
```

Donde:

- **network:** especifica las redes directamente conectadas al router que serán anunciadas por RIP.
- **version:** adopta un valor de 1 o 2 para especificar la versión de RIP que se va a utilizar. Si no se especifica la versión, el software IOS adopta como opción predeterminada el envío de RIP versión 1, pero recibe actualizaciones de ambas versiones, 1 y 2.
- **maximum-paths (opcional):** habilita el equilibrado de carga.

Algunos de los comandos que se pueden utilizar para la verificación de RIP pueden ser:

- `show ip route`: muestra la tabla de enrutamiento donde las rutas aprendidas por RIP llevan la letra R.
- `show ip protocols`: muestra la información de los protocolos que se están ejecutando en el router.
- `debug ip rip`: muestra los procesos que ejecuta RIP.

!!! note "NOTA"

    RIP no lleva identificadores de proceso ni de sistema autónomo, por lo tanto no es posible hacer distinciones entre distintos dispositivos.

## RIPng

RIPng (*Routing Information Protocol new generation*) es la nueva generación de RIP para IPv6 y está basado en RIPv2. Tal como RIPv2, este protocolo es un protocolo de enrutamiento vector distancia que utiliza la cuenta de saltos como métrica, con un máximo de 15, y sus actualizaciones son multicast cada 30 segundos.

RIPng utiliza la dirección de multicast FF02::9, ésta es la dirección del grupo multicast de todos los routers que están ejecutando RIPng. RIP envía actualizaciones utilizando UDP puerto 521 dentro de los paquetes IPv6; éstas incluyen el prefijo IPv6 y la dirección del próximo salto de IPv6.

Los pasos para la configuración de RIPng conlleva habilitar el enrutamiento IPv6 de manera global, posteriormente configurar el nombre del proceso correspondiente y especificar las interfaces que participarán en RIPng. La siguiente sintaxis muestra un ejemplo donde el proceso RIPng se llama ccna.

```text
Router(config)# ipv6 unicast-routing
Router(config)# ipv6 router rip nombre
Router(config)# interface tipo número
Router(config-if)# ipv6 rip nombre enable
```

Ejemplo de configuración completa:

```text
Router# show running-config
ipv6 unicast-routing
!
interface FastEthernet0/0.1
ipv6 address 2012::1/64
ipv6 rip ccna enable
!
interface FastEthernet0/0.2
ipv6 address 2017::1/64
ipv6 rip ccna enable
!
interface FastEthernet0/1.18
ipv6 address 2018::1/64
ipv6 rip ccna enable
!
interface Serial0/0/0.3
ipv6 address 2013::1/64
ipv6 rip ccna enable
!
interface Serial0/0/0.5
ipv6 address 2015::1/64
ipv6 rip ccna enable
!
ipv6 router rip ccna
```

## EIGRP

EIGRPv4 (*Enhanced Interior Gateway Routing Protocol*) es un protocolo vector distancia desarrollado por Cisco, que usa el mismo sistema de métricas sofisticadas que su antecesor IGRP (*Interior Gateway Routing Protocol*) y que utiliza DUAL (*Diffusing Update Algorithm*) para crear las bases de datos topológicas. EIGRP utiliza principios de los protocolos de estado de enlace, es por ello que muchas veces se lo llame protocolo híbrido, aunque sería más correcto llamarlo protocolo de vector distancia avanzado. EIGRP es eficiente tanto en entornos IPv4 como IPv6, los fundamentos no cambian.

EIGRP surge para eliminar las limitaciones de IGRP, aunque sigue siendo sencillo de configurar, utiliza pocos recursos de CPU y memoria.

EIGRP envía actualizaciones confiables identificando sus paquetes con el protocolo IP número 88. Estas actualizaciones confiables significan que el destino tiene que enviar un acuse de recibo (ACK) al origen, es decir, que debe confirmar que ha recibido los datos.

EIGRP utiliza los siguientes tipos de paquetes IP durante las comunicaciones:

- **Hello:** se envían periódicamente usando una dirección multicast para descubrir y mantener relaciones de vecindad.
- **Update:** anuncian las rutas, se envían de manera multicast.
- **Ack:** se envían para confirmar la recepción de un update.
- **Query:** se usa como consulta de nuevas rutas cuando el mejor camino se ha perdido. Cuando el router que envía la consulta no recibe respuesta de alguno de sus vecinos volverá a enviarla, pero esta vez en unicast, y así sucesivamente hasta que reciba un reply o hasta un máximo de 16 envíos.
- **Reply:** es una respuesta a una query, con el camino alternativo o simplemente indicando que no tiene esa ruta.

Mediante los hellos el router descubre a los vecinos; los paquetes son enviados periódicamente para mantenerlos en una lista de vecindad. Cuando no se recibe un hello de un determinado vecino durante un tiempo establecido (*hold time*), se dará por finalizada la relación de vecindad y será necesario recalcular.

!!! note "NOTA"

    EIGRP combina las ventajas de los protocolos de estado de enlace con las de los protocolos de vector de distancia.

### Métrica

EIGRP utiliza una métrica de enrutamiento compuesta. La ruta que posea la métrica más baja será considerada la ruta más óptima. Las métricas de EIGRP están ponderadas mediante constantes desde K1 hasta K5 que convierten los vectores de métrica EIGRP en cantidades escalables.

La métrica utilizada por EIGRP se compone de:

- **K1 = Bandwidth (ancho de banda):** valor mínimo de ancho de banda en kbps en la ruta hacia el destino. Se define como 10 elevado a 7 dividido por el ancho de banda del enlace más lento de todo el camino.
- **K2 = Reliability (fiabilidad):** fiabilidad entre el origen y el destino, determinado por el intercambio de mensajes de actividad expresado en porcentajes. Significa lo confiable que puede ser la interfaz, en un rango expresado entre 255 como máximo y 1 como mínimo; normalmente esta constante no se utiliza.
- **K3 = Delay (retraso):** retraso de interfaz acumulado a lo largo de la ruta en microsegundos.
- **K4 = Carga:** carga de un enlace entre el origen y el destino. Medido en bits por segundo es el ancho de banda real de la ruta. Se expresa en un rango entre 255 como máximo y 1 como mínimo; normalmente esta constante no se utiliza.
- **K5 = MTU:** valor de la unidad máxima de transmisión de la ruta expresado en bytes.

La métrica EIGRP se calcula en base a las variables resultantes de las constantes K1 y K3. Se divide por 10^7 por el valor mínimo de ancho de banda, mientras que el retraso es la sumatoria de todos los retrasos de la ruta en microsegundos y todo multiplicado por 256.

!!! note "NOTA"

    La información de MTU se envía en los mensajes de actualización del protocolo, sin embargo no se utiliza en el cálculo de la métrica.

### DUAL

DUAL (*Diffusing Update Algorithm*) es el algoritmo empleado por EIGRP para encontrar caminos alternativos y libres de bucles, para que en el caso de que el camino principal falle usar una de estas rutas alternativas sin tener que recalcular o, lo que es lo mismo, sin tener que preguntar a los vecinos acerca de cómo llegar al destino.

La terminología empleada por DUAL se basa en los siguientes conceptos:

- **Advertised Distance (AD):** coste desde el router vecino hacia la ruta al destino.
- **Feasible Distance (FD):** mejor métrica desde el router vecino hasta el destino más la métrica que el router origen necesita para alcanzar a ese vecino.
- **Feasible Condition (FC):** es la condición que ha de cumplirse para añadir un posible camino a la tabla de topologías: la AD advertida por el vecino ha de ser menor que la FD.
- **Feasible Successor (FS):** es la forma de definir un router de respaldo o backup para el caso de que la ruta al vecino a través del cual se enruta tráfico se caiga. El FS se habilita sin necesidad de envíos de queries a los vecinos para tratar de averiguar otro posible camino hacia el destino.

DUAL utiliza las métricas para determinar la mejor o mejores rutas hacia un destino. Se pueden tener hasta 16 caminos diferentes hacia un mismo destino.

Hay tres tipos diferentes de caminos o rutas:

- **Internal:** rutas que están directamente configuradas en el router mediante el comando `network`.
- **Summary:** son rutas internas sumarizadas.
- **External:** rutas redistribuidas en EIGRP.

#### Queries

Cuando una ruta se cae y no existe un Feasible Successor en la tabla de topologías, se envían queries a los routers vecinos para determinar cuál de ellos puede alcanzar al destino. En el caso de que éstos no tengan conocimiento, preguntarán recursivamente a sus respectivos vecinos y así sucesivamente.

En el caso de que nadie resuelva la consulta, comienza un estado conocido como SIA (*Stuck In Active*) y el router dará tiempo vencido a la consulta. Este estado se puede evitar con un buen diseño de red.

EIGRP utiliza *Split Horizon* como mecanismo de prevención de bucles, evitando enviar actualizaciones de rutas en la misma interfaz por la que han sido recibidas.

Las queries se propagarán hasta que algún router responda o hasta que no queden más routers a los que preguntar. Cuando se envía una consulta el router entra en estado *active* y pone en marcha un contador de tiempo, por defecto 3 minutos. Cuando este tiempo expira y no ha recibido respuesta, el router entra en estado SIA. Generalmente el router entra en este estado cuando existe algún bucle o el alcance de las queries no está debidamente limitado y se va más allá del área.

Existen dos maneras de controlar las queries, la primera es mediante sumarización y la segunda es mediante *stub routing*. Ambos casos se verán más adelante.

#### Actualizaciones

EIGRP utiliza periódicamente paquetes hello para mantener la relación con sus vecinos, pero el caso de las actualizaciones de enrutamiento es diferente ya que solo se intercambian actualizaciones de ruta en el caso de que se pierda o añada una nueva ruta, y estas actualizaciones son incrementales. El único momento que EIGRP utiliza actualizaciones totales es cuando establece las relaciones iniciales con otros routers.

EIGRP utiliza RTP (*Reliable Transport Protocol*), que es un protocolo propietario de Cisco para controlar la comunicación entre paquetes EIGRP. Estos paquetes son enviados con un número de secuencia y deben ser confirmados en el destino. Los paquetes Hello y los ACK no necesitan ningún tipo de confirmación, mientras que los paquetes update, query y reply sí necesitan confirmación del destino.

Las actualizaciones son enviadas mediante el uso de multicast con la dirección 224.0.0.10. Cuando el vecino recibe un multicast confirma la recepción mediante un paquete unicast no confiable.

El uso del direccionamiento multicast demuestra la evolución de este protocolo siendo de esta forma más efectivo que los protocolos que utilizan broadcast, como por ejemplo RIPv1 o IGRP.

### Tablas

EIGRP mantiene tres tipos de tablas.

- **Tabla de vecindad:** EIGRP comienza a descubrir vecinos vía multicast, esperando confirmaciones vía unicast. La tabla de vecinos es creada y mantenida mediante el uso de paquetes hello. Estos paquetes son enviados en un principio para descubrir a los vecinos y luego se envían periódicamente para mantener información del estado de estos. Hello utiliza la dirección multicast 224.0.0.10. Cada protocolo de capa 3 soportado por EIGRP (IPv4, IPv6, IPX y AppleTalk) tiene su propia tabla de vecinos, esta información no es compartida entre estos protocolos. La tabla de vecinos sirve para verificar que cada uno de ellos responde a los hellos; en caso de que no responda se enviará una copia vía unicast, hasta un máximo de 16 veces.
- **Tabla de topologías:** en ella se listan todos los posibles caminos y todas las posibles redes. Después de que el router conoce quiénes son sus vecinos, es capaz de crear una tabla topológica y de esa manera asignar el *successor* y los *feasible successors* para cada una de las rutas. Además de los successors se agregan también las otras rutas que se llaman *possibilities*. La tabla de topología se encarga de seleccionar qué rutas serán añadidas a la tabla de enrutamiento.
- **Tabla de enrutamiento:** es donde constan la o las redes principales en el caso de tener balanceo de carga. La tabla de enrutamiento se construye a partir de la tabla de topología mediante el uso del algoritmo DUAL. La tabla de topología contiene toda la información de enrutamiento que el router conoce a través de EIGRP; por medio de esta información el router puede ejecutar DUAL y así determinar el sucesor y el *feasible successor*, el sucesor será el que finalmente se agregue a la tabla de enrutamiento.

### Equilibrado de carga desigual

EIGRP es el único protocolo de enrutamiento que proporciona la capacidad de hacer equilibrado de carga desigual; los demás protocolos permiten hacer balanceo de carga de forma equitativa a todos los enlaces en el caso de que el coste al destino sea el mismo. Sin embargo EIGRP, mediante el uso de la varianza, permite el balanceo de carga del tipo desigual.

El equilibrado se realiza multiplicando la FD por la varianza, que por defecto tiene un valor de uno. Si este último valor fuese, por ejemplo, 3, la FD se multiplicaría por 3, por lo tanto cualquier otra FD que tuviera un valor menor al producto resultante serviría de igual manera para transmitir datos. Ahora bien, EIGRP no transmitiría datos de forma equitativa por ambos canales sino que utilizaría las métricas para decidir qué porcentaje enviaría por cada enlace. Por ejemplo, si un enlace es de 3 Mbps y otro de 1 Mbps, enviaría tres veces más datos por el primero.

## Configuración de EIGRP

EIGRP es un protocolo de enrutamiento *classless* o sin clase, es decir, que en las actualizaciones envía tanto el prefijo de red como la máscara de subred. Los protocolos de enrutamiento sin clase son capaces de sumarizar. EIGRP permite sumarizar en cualquier tipo de interfaz y de ruta, algo sumamente importante a la hora de diseñar una red EIGRP escalable.

Para la configuración básica de EIGRP es necesario activar el protocolo con su correspondiente AS (*Autonomous System*) y las redes que participan en el proceso.

```text
Router(config)# router eigrp número de sistema autónomo
Router(config-router)# network dirección de red
```

A partir de esta configuración todas las interfaces relacionadas con el comando `network` comienzan a buscar routers vecinos dentro del mismo AS para establecer una relación de vecindad. Para el caso concreto de que dicha interfaz necesite ser advertida pero que no establezca una relación con el vecino se debe configurar dentro del protocolo de la siguiente manera:

```text
Router(config-router)# passive-interface número de interfaz
```

Con esto se evitará el envío de hello por la interfaz en cuestión.

El comando `network` puede individualizar una interfaz especificando una máscara comodín o *wildcard*:

```text
Router(config-router)# network dirección de red [wildcard]
```

```text
Router(config)# router eigrp 220
Router(config-router)# network 172.16.0.0 0.0.0.255
```

Para el caso que desee desactivar el resumen de ruta, por ejemplo al tener redes discontinuas, puede ejecutar el comando:

```text
Router(config-router)# no auto-summary
```

Para crear manualmente un resumen de ruta puede hacerlo indicando el AS (sistema autónomo EIGRP) y la red de resumen:

```text
Router(config-router)# ip summary-address eigrp sistema autónomo dirección de red-máscara
```

### Intervalos hello

Los intervalos de saludo y los tiempos de espera se configuran por interfaz y no tienen que coincidir con otros routers EIGRP para establecer adyacencias.

```text
Router(config-if)# ip hello-interval eigrp AS segundos
```

Si cambia el intervalo de saludo, asegúrese de cambiar también el tiempo de espera a un valor igual o superior al intervalo hello. De lo contrario, la adyacencia de vecinos se desactivará después de que haya terminado el tiempo de espera y antes del próximo intervalo de saludo.

```text
Router(config-if)# ip hold-time eigrp AS segundos
```

El valor en segundos para los intervalos de saludo y de tiempo de espera puede variar entre 1 y 65535.

### Filtrados de rutas

EIGRP permite el filtrado de rutas en las interfaces de manera entrante o saliente asociando listas de acceso al protocolo.

```text
Router(config)# router eigrp AS
Router(config-router)# distribute-list número ACL [in|out] interfaz
```

#### Redistribución estática

EIGRP redistribuye rutas aprendidas estáticamente dirigidas hacia un destino en particular o por defecto.

```text
Router(config)# ip route red destino [gateway|interfaz]
Router(config)# router eigrp AS
Router(config-router)# redistribute static
```

!!! note "NOTA"

    EIGRP se redistribuye automáticamente con otros sistemas autónomos EIGRP identificando las rutas como EIGRP externo y con IGRP si es el mismo número de sistema autónomo.

### Equilibrado de carga

El balanceo de carga en los routers con rutas de coste equivalente suele ser por defecto de un máximo de cuatro. El equilibrado puede modificarse hasta un máximo de seis rutas. EIGRP puede a su vez equilibrar tráfico por múltiples rutas con diferentes métricas utilizando un multiplicador de varianza, por defecto el valor de la varianza es uno, equilibrando la carga por costes equivalentes.

```text
Router(config)# router eigrp sistema autónomo
Router(config-router)# network dirección de red
Router(config-router)# maximum-paths número máximo
Router(config-router)# variance métrica multiplicador
```

### Router Stub

Los routers *stub* en EIGRP sirven para enviar una cantidad limitada de información entre ellos mismos y los routers de núcleo o *core*. De esta manera se ahorran recursos de memoria y CPU en los routers stub.

Los routers stub solamente tienen un vecino que acorde con buen diseño de red debería ser un router de distribución, de esta forma el router solo tiene una red que apunta hacia el router de distribución para alcanzar cualquier otro prefijo en la red.

Configurando un router como stub ayuda al buen funcionamiento de la red, las consultas se responden mucho más rápido. Estos routers responden a esas consultas con mensajes de inaccesibles limitando así el ámbito de dichas consultas.

La sintaxis de configuración de EIGRP stub es la siguiente:

```text
Router(config-router)# eigrp stub [receive-only|connected|redistributed|static|summary]
```

### Autenticación

La autenticación EIGRP comienza creando una cadena de claves, numerarla y asociarla con la clave correspondiente. Posteriormente se puede configurar un sistema seguro de encriptación como MD5 dentro de la interfaz y habilitar la autenticación dentro de la misma interfaz.

```text
Router(config)# key chain nombre
Router(config-keychain)# key número
Router(config-keychain-key)# key-string nombre
Router(config-keychain-key)# exit
Router(config-keychain)# exit
Router(config)# interface tipo número
Router(config-if)# ip authentication mode eigrp AS md5
Router(config-if)# ip authentication key-chain eigrp AS nombre de la cadena
```

### Verificación

Algunos comandos para la verificación y control EIGRP son:

- `show ip route`: muestra la tabla de enrutamiento.
- `show ip protocols`: muestra los parámetros de todos los protocolos.
- `show ip eigrp neighbors`: muestra la información de los vecinos EIGRP.
- `show ip eigrp topology`: muestra la tabla de topología EIGRP.
- `debug ip eigrp`: muestra la información de los paquetes.

```text
Router# show ip route eigrp
D 172.22.0.0/16 [90/2172416] via 172.25.2.1, 00:00:35, Serial0.1
172.25.0.0/16 is variably subnetted, 6 subnets, 4 masks
D 172.25.25.6/32 [90/2300416] via 172.25.2.1, 00:00:35, Serial0.1
D 172.25.25.1/32 [90/2297856] via 172.25.2.1, 00:00:35, Serial0.1
D 172.25.1.0/24 [90/2172416] via 172.25.2.1, 00:00:35, Serial0.1
D 172.25.0.0/16 is a summary, 00:03:10, Null0
D 10.0.0.0/8 [90/4357120] via 172.25.2.1, 00:00:35, Serial0.1
```

```text
Router# show ip protocols
Routing Protocol is "eigrp 100"
Outgoing update filter list for all interfaces is not set
Incoming update filter list for all interfaces is not set
Default networks flagged in outgoing updates
Default networks accepted from incoming updates
EIGRP metric weight K1=1, K2=0, K3=1, K4=0, K5=0
EIGRP maximum hopcount 100
EIGRP maximum metric variance 1
Redistributing: eigrp 55
Automatic network summarization is in effect
Automatic address summarization:
  192.168.20.0/24 for Loopback0, Serial0
  192.170.0.0/16 for Ethernet0
Summarizing with metric 128256
Maximum path: 4
Routing for Networks:
  172.30.0.0
  192.168.20.0
Routing Information Sources:
  Gateway          Distance      Last Update
  172.25.5.1       90            00:01:49
Distance: internal 90 external 170
```

## EIGRPv6

Este protocolo está basado en EIGRP para IPv4; tal como pasa con su antecesor es un protocolo vector-distancia avanzado diseñado por Cisco que utiliza una métrica compleja con actualizaciones confiables y el algoritmo DUAL para converger rápidamente. EIGRP para IPv6 se puede configurar a partir de la versión de IOS 12.4(6)T y posteriores.

EIGRPv6 lleva este nombre no solo porque sea la versión 6 del protocolo, sino porque además es el que se usa con IPv6.

Las siguientes son algunas diferencias entre EIGRP para IPv4 y EIGRP para IPv6:

- EIGRPv6 anuncia prefijos IPv6 junto con su longitud, mientras que la versión para IPv4 anuncia subredes y máscaras.
- EIGRPv6 utiliza la IP *local link* del vecino como siguiente salto. En EIGRP para IPv4 ese concepto no existe.
- EIGRPv6 encapsula los mensajes en paquetes IPv6 y no en paquetes IPv4.
- EIGRPv6 confía en IPv6 para la autenticación.
- EIGRPv6 no tiene concepto de redes *classful* por lo que no realiza ninguna sumarización automática, tal y como ocurre con EIGRP para IPv4.
- EIGRPv6 no requiere que los vecinos estén en la misma subred para que se establezca la adyacencia.

### Configuración

En general la mayoría de los comandos para EIGRPv6 son similares a EIGRPv4 añadiendo el parámetro `ipv6`.

Habilitar el enrutamiento IPv6 y el enrutamiento EIGRPv6 con los comandos de configuración global:

```text
Router(config)# ipv6 unicast-routing
Router(config)# ipv6 router eigrp AS
```

Configurar la dirección IPv6 en la interfaz correspondiente. Se puede utilizar cualquiera de estos comandos a nivel de interfaz:

```text
Router(config-if)# ipv6 address dirección/prefijo [eui-64]
Router(config-if)# ipv6 enable
```

Configurar EIGRPv6 en la interfaz con el comando `ipv6 eigrp AS`, donde el AS ha de ser el mismo utilizado en la configuración global.

Habilitar EIGRPv6 globalmente utilizando el comando `no shutdown` dentro de la configuración de EIGRP.

Dentro de la configuración del protocolo se puede configurar un ID con el comando:

```text
Router(config-rtr)# router-id ID
```

Hay que prestar especial atención a este último paso, ya que si no se configura un `router-id`, EIGRP intentará utilizar primeramente la IP loopback más alta; si no la encuentra intentará hacerlo con la interfaz física con la IP más alta configurada. En ambos casos refiriéndose a IPv4. Si no encuentra ninguna, el proceso no se iniciará.

El siguiente es un ejemplo de configuración:

```text
Router# show running-config
..................................
ipv6 unicast-routing
!
interface FastEthernet0/0.1
 ipv6 address 2012::1/64
 ipv6 eigrp 9
!
interface FastEthernet0/0.2
 ipv6 address 2017::1/64
 ipv6 eigrp 9
!
interface FastEthernet0/1.18
 ipv6 address 2018::1/64
 ipv6 eigrp 9
!
interface Serial0/0/0.3
 ipv6 address 2013::1/64
 ipv6 eigrp 9
!
ipv6 router eigrp 9
 no shutdown
 router eigrp 10.10.34.3
```

### Verificación

Existen varios comandos de verificación; en el siguiente ejemplo se pueden apreciar que son similares a los usados en EIGRP para IPv4, lo que cambia es la palabra `ipv6`:

- `show ipv6 route`: muestra la tabla de enrutamiento.
- `show ipv6 protocols`: muestra los parámetros de todos los protocolos.
- `show ipv6 eigrp neighbors`: muestra la información de los vecinos EIGRP.
- `show ipv6 eigrp topology`: muestra la tabla de topología EIGRP.
- `show ipv6 eigrp interfaces`: muestra la información de las interfaces que participan en el proceso EIGRP.

```text
Router# show ipv6 protocols
IPv6 Routing Protocol is "eigrp 9"
EIGRP metric weight K1=1, K2=0, K3=1, K4=0, K5=0
EIGRP maximum hopcount 100
EIGRP maximum metric variance 1
Interfaces:
 FastEthernet0/0
 Serial0/0/0.1
 Serial0/0/0.2
Redistribution:
 None
Maximum path: 16
Distance: internal 90 external 170
```

```text
Router# show ipv6 route 2099::/64
Routing entry for 2099::/64
  Known via "eigrp 9", distance 90, metric 2174976, type internal
  Route count is 2/2, share count 0
Routing paths:
  FE80::22FF:FE22:2222, Serial0/0/0.2
    Last updated 00:24:32 ago
  FE80::11FF:FE11:1111, Serial0/0/0.1
    Last updated 00:07:51 ago
```

```text
R3# show ipv6 route eigrp
IPv6 Routing Table - Default - 19 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
        B - BGP, M - MIPv6, R - RIP, I1 - ISIS L1 I2 - ISIS L2, IA -
        ISIS interarea, IS - ISIS summary, D - EIGRP
        EX - EIGRP external, O - OSPF Intra, OI - OSPF Inter, OE1 -
        OSPF ext 1, OE2 - OSPF ext 2, ON1 - OSPF NSSA ext 1, ON2 -
        OSPF NSSA ext 2
D 2005::/64 [90/2684416]
     via FE80::11FF:FE11:1111, Serial0/0/0.1
     via FE80::22FF:FE22:2222, Serial0/0/0.2
D 2012::/64 [90/2172416]
     via FE80::22FF:FE22:2222, Serial0/0/0.2
     via FE80::11FF:FE11:1111, Serial0/0/0.1
D 2014::/64 [90/2681856]
     via FE80::11FF:FE11:1111, Serial0/0/0.1
D 2015::/64 [90/2681856]
     via FE80::11FF:FE11:1111, Serial0/0/0.1
.....................................
D 2099::/64 [90/2174976]
     via FE80::22FF:FE22:2222, Serial0/0/0.2
     via FE80::11FF:FE11:1111, Serial0/0/0.1
```

## OSPF

OSPFv2 (*Open Shortest Path First*) fue creado a finales de los ochenta. Se diseñó para cubrir las necesidades de las grandes redes IP que otros protocolos como RIP no podían soportar, incluyendo VLSM, autenticación de origen de ruta, convergencia rápida, etiquetado de rutas conocidas mediante protocolos de enrutamiento externo y publicaciones de ruta de multidifusión. El protocolo OSPF versión 2 es la implementación más actualizada, aparece especificado en la RFC 2328.

OSPF funciona dividiendo una Intranet o un sistema autónomo en unidades jerárquicas de menor tamaño. Cada una de estas áreas se enlaza a un área backbone mediante un router fronterizo. Todos los paquetes enviados desde una dirección de una estación de trabajo de un área a otra de un área diferente atraviesan el área backbone, independientemente de la existencia de una conexión directa entre las dos áreas. Aunque es posible el funcionamiento de una red OSPF únicamente con el área backbone, OSPF escala bien cuando la red se subdivide en un número de áreas más pequeñas.

OSPF es un protocolo de enrutamiento por estado de enlace que, a diferencia de RIP e IGRP, que publican sus rutas solo a routers vecinos, los routers OSPF envían publicaciones del estado de enlace LSA (*Link-State Advertisment*) a todos los routers pertenecientes a la misma área jerárquica mediante una multidifusión de IP. La LSA contiene información sobre las interfaces conectadas, la métrica utilizada y otros datos adicionales necesarios para calcular las bases de datos de la ruta y la topología de red.

Los routers OSPF acumulan información sobre el estado de enlace y ejecutan el algoritmo SPF (*Shortest Path First*), también conocido con el nombre de su creador Dijkstra, para calcular la ruta más corta a cada nodo.

Para determinar qué interfaces reciben las publicaciones de estado de enlace, los routers ejecutan el protocolo OSPF Hello. Los routers vecinos intercambian mensajes hello para determinar qué otros routers existen en una determinada interfaz y sirven como mensajes de actividad que indican la accesibilidad de dichos routers.

Cuando se detecta un router vecino, se intercambia información de topología OSPF. Cuando los routers están sincronizados, se dice que han formado una adyacencia.

Las LSA se envían y reciben solo en adyacencias. La información de la LSA se transporta en paquetes mediante la capa de transporte OSPF que define un proceso fiable de publicación, acuse de recibo y petición para garantizar que la información de la LSA se distribuye adecuadamente a todos los routers de un área. Los tipos más comunes son los que publican información sobre los enlaces de red conectados de un router y los que publican las redes disponibles fuera de las áreas OSPF.

### Métrica

El coste es la métrica utilizada por OSPF. Un factor importante en el intercambio de las LSA es la relativa a la métrica. OSPF calcula el coste mediante la siguiente fórmula:

```text
                    100.000.000 bps
Coste = ---------------------------------
          VelocidadEnlace (bps)
```

Si existen varios caminos para llegar al destino con el mismo coste, OSPF efectúa por defecto un balanceo de carga hasta 4 rutas diferentes. Este valor admite hasta 16 rutas diferentes. OSPF calcula el coste de manera acumulativa tomando en cuenta el coste de la interfaz de salida de cada router.

### Tablas

Todas las operaciones OSPF se basan en tres tablas, que deben mantenerse actualizadas:

- **Tabla de vecinos:** contiene la información sobre los vecinos con los cuáles se realizan intercambios OSPF.
- **Tabla de topologías:** mantiene una base de datos de todas las LSA recibidas de toda la red.
- **Tabla de enrutamiento:** contiene la información necesaria para alcanzar una red de destino.

#### Mantenimiento de la base de datos

Los protocolos vector distancia anuncian rutas hacia los vecinos, pero los protocolos estado de enlace anuncian una lista de todas sus conexiones. Cuando un enlace se cae se envían LSA (*Link-State Advertisement*), que son compartidas por los vecinos, así como también una base topológica LSDB (*Link-State Database*).

Las LSA se identifican con un número de secuencia para reconocer las más recientes, en un rango de 0x8000 0001 al 0xFFFF FFFF. Cuando los routers convergen tienen la misma LSDB; a partir de ese momento SPF es capaz de determinar la mejor ruta hacia el destino. La tabla de topología es la visión que tiene el router de la red dentro del área en que se encuentra, incluyendo además todos los routers.

La tabla de topología se actualiza por cada una de las LSA que envían cada uno de los routers dentro de la misma área y que todos estos routers comparten la misma base de datos. Si existen inconsistencias en esta base de datos podrían generarse bucles; es el propio router el encargado de avisar que ha habido algún cambio e informar del mismo.

Algunas de éstas pueden ser:

- Pérdida de conexión física o link en algunas de sus interfaces.
- No se reciben los hello en el tiempo establecido por sus vecinos.
- Se recibe un LSA con información de cambios en la topología.

En cualquiera de los tres casos anteriores el router generará una LSA enviando a sus vecinos la siguiente información:

- Si la LSA es más reciente se añade a la base de datos. Se reenvían a todos los vecinos para que actualicen sus tablas y SPF comienza a funcionar.
- Si el número de secuencia es el mismo que el router ya tiene registrado en la base de datos, ignorará esta actualización.
- Si el número de secuencia es anterior al que está registrado, el router enviará la versión nueva al router que envió la anterior. De esta forma se asegura que todos los routers poseen la última versión.

```text
Router# show ip ospf database
OSPF Router with ID (172.18.6.1) (Process ID 87)

Router Link States (Area 10)

Link ID         ADV Router      Age   Seq#         Checksum Link count
172.18.6.1       172.18.6.1       108   0x80000005  0x008367  4
172.19.2.1       172.19.2.1       144   0x80000004  0x00C25B  1
192.168.2.3      192.168.2.3      109   0x80000006  0x001DDE  4
192.168.2.5      192.168.2.5      109   0x80000006  0x007CFD  3

Net Link States (Area 10)

Link ID         ADV Router      Age   Seq#         Checksum
172.18.5.3       172.19.2.1       144   0x80000003  0x001612
192.168.1.1      172.18.6.1       208   0x80000001  0x007CE5
192.168.2.1      172.18.6.1       208   0x80000001  0x0071EF

Summary Net Link States (Area 10)

Link ID         ADV Router      Age   Seq#         Checksum
0.0.0.0         172.19.2.1       978   0x80000001  0x00F288
2.2.2.2         172.19.2.1       973   0x80000001  0x0096DC
2.2.2.3         172.19.2.1       973   0x80000001  0x008CE5
2.2.2.4         172.19.2.1       973   0x80000001  0x0082EE
172.19.2.1       172.19.2.1       973   0x80000001  0x00298F
172.20.10.0      172.19.2.1       397   0x80000001  0x00472A
```

### Relación de vecindad

OSPF establece relaciones con otros routers mediante el intercambio de mensajes Hello. Luego del intercambio inicial de estos mensajes los routers elaboran sus tablas de vecinos, que lista todos los routers que están ejecutando OSPF y están directamente conectados. Los mensajes hello son enviados con la dirección multicast 224.0.0.5 con una frecuencia en redes tipo broadcast cada 10 segundos, mientras que en las redes nonbroadcast cada 30 segundos.

Una vez que los routers hayan intercambiado los paquetes hello, comienzan a intercambiar información acerca de la red y una vez que esa información haya sincronizado, los routers forman adyacencias.

Una vez lograda la adyacencia (estado Full), las tablas deben mantenerse actualizadas; las LSA son enviadas cuando exista algún cambio o cada 30 minutos como un tiempo de refresco.

La siguiente lista describe los estados de una relación de vecindad:

- **Down:** es el primer estado de OSPF y significa que no se ha escuchado ningún hello de este vecino.
- **Attempt:** este estado es únicamente para redes NBMA; durante este estado el router envía paquetes hello de tipo unicast hacia el vecino aunque no se hayan recibido hello de ese vecino.
- **Init:** se ha recibido un paquete hello de un vecino, pero el ID del router no está listado en ese paquete hello.
- **2-Way:** se ha establecido una comunicación bidireccional entre dos routers.
- **Exstart:** una vez elegidos el DR y el BDR, el verdadero proceso de intercambiar información del estado del enlace se hace entre los routers y sus DR y BDR.
- **Exchange:** en este estado los routers intercambian la información de la base de datos DBD.
- **Loading:** es en este estado cuando se produce el verdadero intercambio de la información de estado de enlace.
- **Full:** finalmente los routers son totalmente adyacentes, se intercambian las LSA y las bases de datos de los routers están sincronizadas.

Los mensajes hello se siguen enviando periódicamente para mantener las adyacencias; en el caso de que no se reciban se dará por perdida dicha adyacencia. Tan pronto como OSPF detecta un problema modifica las LSA correspondientes y envía actualizaciones a todos los vecinos. Este proceso mejora el tiempo de convergencia y reduce al mínimo la cantidad de información que se envía a la red.

### Router designado

Cuando varios routers están conectados a un segmento de red del tipo broadcast, uno de estos routers del segmento tomará el control y mantendrá las adyacencias entre todos los routers de ese segmento. Ese router toma el nombre de DR (*Designate Router*) y será elegido a través de la información que contienen los mensajes hello que se intercambian los routers. Para una eficaz redundancia también se elige un router designado de reserva o BDR.

Los DR son creados en enlaces multiacceso debido a que el número de adyacencias incrementaría de manera significativa el tráfico en la red; de esta forma el DR y el BDR establecen adyacencias reduciendo significativamente la cantidad de las mismas.

La elección de un router designado (DR) y un router designado de reserva (BDR) en una topología multiacceso con difusión cumple los siguientes requisitos:

- El router con el valor de prioridad más alto es el router designado DR.
- El router con el segundo valor es el router designado de reserva BDR.
- El valor predeterminado de la prioridad OSPF de la interfaz es 1. Un router con prioridad 0 no es elegible. En caso de empate se usa el ID de router.
- ID de router. Este número de 32 bits identifica únicamente al router dentro de un sistema autónomo. La dirección IP más alta de una interfaz activa se elige por defecto.

## Topologías OSPF

### Multiacceso con difusión

Dado que el enrutamiento OSPF depende del estado de enlace entre dos routers, los vecinos deben reconocerse entre sí para compartir información. Este proceso se hace por medio del protocolo Hello.

Los paquetes se envían cada 10 segundos (forma predeterminada) utilizando la dirección de multidifusión 224.0.0.5. Para declarar a un vecino caído el router espera cuatro veces el tiempo del intervalo Hello (intervalo Dead).

Los routers de un entorno multiacceso, como un entorno Ethernet, deben elegir un router designado (DR) y un router designado de reserva (BDR) para que representen a la red.

Un DR lleva a cabo tareas de envío y sincronización. El BDR solo actuará si el DR falla. Cada router debe establecer una adyacencia con el DR y el BDR. En redes con difusión se lleva a cabo la elección de DR y BDR.

!!! note "NOTA"

    Un router se ve a sí mismo listado en un paquete Hello que recibe de un vecino.

### NBMA

Las redes NBMA son aquellas que soportan más de dos routers pero que no tienen capacidad de difusión. Frame-Relay, ATM, X.25 son algunos ejemplos de redes NBMA. La selección del DR se convierte en un tema importante ya que el DR y el BDR deben tener conectividad física total con todos los routers de la red.

OSPF en redes NBM: debe existir conectividad entre todos los routers.

### Punto a punto

En redes punto a punto el router detecta dinámicamente a sus vecinos enviando paquetes Hello con la dirección de multidifusión 224.0.0.5. No se lleva a cabo elección y no existe concepto de DR o BDR.

Los intervalos Hello y Dead son de 10 y 40 segundos respectivamente.

OSPF en redes punto a punto: no hay elección de DR ni BDR.

## Configuración de OSPF en una sola área

Para iniciar el proceso de configuración OSPF se debe identificar el número de proceso. Este número tiene significado local y pueden existir varios procesos OSPF en un mismo router, aunque hay que tener en cuenta que cuantos más procesos más consumo de recursos.

```text
Router(config)# router ospf número de proceso
```

Una vez que el proceso OSPF es habilitado se debe identificar las interfaces que participarán en el mismo, debiendo tener especial cuidado con la utilización de la máscara comodín o *wildcard*.

```text
Router(config-router)# network dirección wildcard area número
```

El parámetro área asocia las interfaces en un área en particular. El formato del parámetro área es un campo de 32 bits en decimal simple o notación decimal de punto.

A partir de la identificación del área comienzan a intercambiarse los hello, se envían las LSA y el conjunto de los routers comienzan a participar en la red. Cuando el router tiene interfaces en diferentes áreas se llama ABR.

La *wildcard* permite especificar una red, una subred, una interfaz específica, un rango de interfaces o todas las interfaces que participarán en el proceso OSPF. Existen varias formas de utilizar el comando `network` aprovechando la flexibilidad de la wildcard:

- Configurando de manera global todas las interfaces.
- Configurando las redes a las que pertenecen las interfaces.
- Configurando las interfaces una a una.

Estas opciones pueden ser aplicables con mayor eficacia según sea el caso. La primera puede ser de rápida configuración, pero con el consiguiente riesgo de que alguna interfaz no deseada se filtre en el proceso OSPF. El tercer caso es más trabajoso para el administrador, pero más selectivo y seguro.

Observe el siguiente ejemplo:

**Configurando de manera global todas las interfaces:**

```text
Router(config-router)# network 0.0.0.0 255.255.255.255 area 0
```

**Configurando las redes a las que pertenecen las interfaces:**

```text
Router(config-router)# network 172.16.0.0 0.0.255.255 area 0
Router(config-router)# network 192.168.100.0 0.0.0.255 area 0
```

**Configurando las interfaces una a una:**

```text
Router(config-router)# network 192.168.1.1 0.0.0.0 area 0
Router(config-router)# network 192.168.2.1 0.0.0.0 area 0
Router(config-router)# network 192.168.3.1 0.0.0.0 area 0
Router(config-router)# network 172.16.0.1 0.0.0.0 area 0
Router(config-router)# network 172.16.1.3 0.0.0.0 area 0
```

### Elección del DR y BDR

La elección del DR y del BDR puede manipularse acorde a las necesidades existentes variando los valores de la prioridad dentro de la interfaz o subinterfaz que participe en el dominio OSPF (rango de 1 a 65535).

```text
Router# configure terminal
Router(config)# interface tipo número
Router(config-if)# ip ospf priority [1-65535]
```

Esta decisión puede aplicarse también con la creación de una interfaz de Loopback, cuyo valor se tendrá en cuenta como prioritario al momento de definir el ID del router.

```text
Router(config)# interface loopback número
Router(config-if)# ip address dirección IP máscara
```

!!! tip "RECUERDE"

    Para la configuración de OSPF, las interfaces que participan del proceso deben estar configuradas y activas previamente.

### Cálculo del coste del enlace

El Cisco IOS determina automáticamente el coste basándose en el ancho de banda de la interfaz expresado en bps.

```text
                       10^8 bps
Coste = ---------------------
            Bandwidth
```

Para modificar el ancho de banda sobre la interfaz utilice el comando `bandwidth`:

```text
Router(config)# interface serial 0/0
Router(config-if)# bandwidth 64
```

Use el siguiente comando de configuración de interfaz para cambiar el coste del enlace:

```text
Router(config-if)# ip ospf cost coste
```

El valor por defecto del coste se muestra en la siguiente tabla:

| Enlace | Coste |
| --- | --- |
| 56-kbps serial link | 1785 |
| T1 (1.544-Mbps serial link) | 64 |
| Ethernet | 10 |
| FastEthernet | 1 |
| GigabitEthernet | 1 |

### Autenticación OSPF

Para crear una contraseña de autenticación en texto simple utilice el siguiente comando dentro de la interfaz:

```text
Router(config-if)# ip ospf authentication-key contraseña
```

Para establecer un nivel de encriptación en la contraseña de autenticación puede utilizarse el siguiente comando dentro de la interfaz:

```text
Router(config-if)# ip ospf message-digest-key [identificador] md5 [tipo de encriptación]
```

```text
Router(config)# router ospf número de proceso
Router(config-router)# area número authentication
Router(config-router)# area número authentication message-digest
```

### Administración del protocolo Hello

De manera predeterminada, los paquetes de saludo OSPF (Hello) se envían cada 10 segundos en segmentos multiacceso y punto a punto, y cada 30 segundos en segmentos multiacceso sin broadcast (NBMA).

El intervalo muerto (Dead) es el período, expresado en segundos, que el router esperará para recibir un paquete de saludo antes de declarar al vecino desactivado. Cisco utiliza de forma predeterminada cuatro veces el intervalo de Hello. En el caso de los segmentos multiacceso y punto a punto, dicho período es de 40 segundos. En el caso de las redes NBMA, el intervalo muerto es de 120 segundos.

Para configurar los intervalos de Hello y de Dead en una interfaz se deben utilizar los siguientes comandos:

```text
Router(config-if)# ip ospf hello-interval segundos
Router(config-if)# ip ospf dead-interval segundos
```

## OSPF en múltiples áreas

La capacidad de OSPF de separar una gran red en diferentes áreas más pequeñas se denomina enrutamiento jerárquico. Esta red jerárquica permite dividir un AS (sistema autónomo) en redes más pequeñas llamadas áreas que se conectan al área 0 o área de backbone. Las actualizaciones de enrutamiento interno como el recálculo de la base de datos se producen dentro de cada área, es decir, que si por ejemplo una interfaz se torna inestable el recálculo se circunscribe a su área sin afectar al resto. Esta tarea hace que los cálculos SPF solo incluyan al área en cuestión sin que esto afecte a las demás áreas.

Las actualizaciones de estado de enlace LSU pueden publicar rutas resumidas entre áreas en lugar de una por red. La información de enrutamiento entre áreas puede ser filtrada haciendo más selectivo y eficaz el enrutamiento dinámico.

Si se consideran los problemas que pueden existir con el crecimiento de una red en OSPF con una sola área, hay varias cuestiones que se deben tener en cuenta:

- El algoritmo SPF es ejecutado con mayor frecuencia. Cuanto mayor sean las dimensiones de la red, mayor posibilidad de fallos en enlaces o cambios topológicos debiendo recalcular toda la tabla de topologías con el algoritmo SPF. El tiempo de convergencia es mayor cuanto mayor sea el área.
- Cuanto mayor sea el área, mayor será la tabla de enrutamiento. A pesar de que la tabla de enrutamiento no se envía por completo como en los protocolos vector distancia, cuanto más grande más tiempo se tardará en hacer una búsqueda en ella, con mayor gasto de recursos.
- En una red de grandes dimensiones la tabla de topología puede ser inmanejable, intercambiándose entre los routers cada 30 minutos.
- Finalmente, la base de datos se incrementa en tamaño y los cálculos aumentan en frecuencia; crece de manera considerable el uso de CPU y memoria afectando directamente a la latencia de la red. Todo esto se traduce en congestiones de red, paquetes perdidos, malos tiempos de convergencia, etc.

### Tipos de router

La división en áreas hace que el desempeño de la red mejore notablemente; parte de esta mejora incluye la tecnología empleada y el diseño de un modelo jerárquico eficiente. Los routers dentro de este modelo jerárquico tienen diferentes responsabilidades, a saber:

- **Internal router:** es el responsable de mantener una base de datos actualizada y precisa de cada una de las LSA dentro de cada una de las áreas. Al mismo tiempo envía datos hacia otras redes empleando la ruta más corta. Todas las interfaces de este router están dentro de la misma área.
- **Backbone router:** las normas de diseño de OSPF requieren que todas las áreas estén conectadas a un área de backbone o área 0. Un router dentro de esta área lleva este nombre.
- **Area Border Router (ABR):** este router se encarga de la conexión entre dos o más áreas, mantiene una base topológica de cada una de las áreas a que pertenece y envía actualizaciones LSA a cada una de dichas áreas.
- **Autonomous System Boundary Router (ASBR):** este router conecta hacia otros dominios de enrutamiento, normalmente ubicados dentro del área de backbone.

### Virtual Links

Para los casos en que el administrador deba configurar un área sin conectividad con el área 0 podrá utilizar los *virtual links*, creando un "puente" entre dos ABR para conectar de forma lógica el área remota con el área 0. De esta manera la información del área entre los dos ABR fluye a través del área intermedia o virtual. Desde el punto de vista de OSPF el ABR tiene una conexión directa con estas tres áreas.

Este escenario puede verse en varios casos:

- Una fusión o un fallo aísla un área del área 0.
- La existencia de dos áreas 0 debido a una fusión.
- Un área es crítica y se requiere configurar un link extra para mayor redundancia (pasando éste por otra área para llegar al área 0).

Aunque los virtual links son una herramienta que solventa este tipo de situaciones, no se debe pensar en ella desde un punto de vista de diseño; deben ser empleadas como soluciones temporales.

Hay que asegurarse de los siguientes puntos antes de implementarlos:

- Ambos routers deben compartir un área.
- El área de tránsito no puede ser *stub*.
- Uno de los routers ha de estar conectado al área 0.

### Verificación

Algunos comandos para la verificación y control OSPF son:

- `show ip route`: muestra la tabla de enrutamiento.
- `show ip protocols`: muestra los parámetros del protocolo.
- `show ip ospf neighbors`: muestra la información de los vecinos OSPF.
- `debug ip ospf events`: muestra adyacencias, DR, inundaciones, etc.
- `debug ip ospf packet`: muestra la información de los paquetes.
- `debug ip ospf hello`: muestra las actualizaciones Hello.

```text
Router# show ip protocols
Routing Protocol is "ospf 100"
Outgoing update filter list for all interfaces is not set
Incoming update filter list for all interfaces is not set
Router ID 200.200.10.10
It is an area border and autonomous system boundary router
Redistributing External Routes from
Number of areas in this router is 3. 3 normal 0 stub 0 nssa
Maximum path: 4
Routing for Networks:
  192.168.0.0  0.0.0.255 area 0
  192.170.0.0  0.0.0.255 area 0
  192.178.0.0  0.0.0.255 area 0
Routing Information Sources:
  Gateway          Distance      Last Update
  192.168.0.1      110            00:01:30
  192.170.0.26     110            16:44:07
  122.178.0.1      110            00:01:30
Distance: (default is 110)
```

```text
Router# show ip ospf neighbor
Neighbor ID     Pri   State       Dead Time   Address       Interface
192.168.0.3       1   FULL/DROTHER 00:00:33   192.168.0.3   Gi0/0
192.168.0.5       1   FULL/DROTHER 00:00:33   192.168.0.5   Gi0/0
192.168.0.4       1   FULL/BDR     00:00:33   192.168.0.4   Gi0/0
200.200.1.1       2   FULL/DR      00:00:39   192.168.0.2   Gi0/0
```

!!! note "NOTA"

    La configuración de OSPF en múltiples áreas puede ser muy extensa y complicada. OSPF multiarea se ve en su totalidad en el CCNP R&S.

## OSPFv3

OSPFv3 comparte muchas características de OSPFv2; sigue siendo un protocolo de estado de enlace que utiliza el algoritmo de Dijkstra SPF para seleccionar los mejores caminos a través de la red. Las rutas en OSPFv3 son organizadas en áreas con todas las rutas conectadas al área 0 o área de backbone.

Los routers OSPFv3 se comunican con sus vecinos intercambiando hello, LSA y también DBD, y ejecutan el algoritmo SPF contra la base de datos del estado de enlace acumulada (LSDB).

OSPFv3 utiliza el mismo tipo de paquetes que la versión 2, forma las relaciones de vecinos con el mismo mecanismo y borra las LSA de forma idéntica. Ambas versiones soportan redes NBMA, non-broadcast y punto a punto. OSPFv3 se ejecuta directamente dentro de los paquetes IPv6 y puede coexistir con OSPFv2.

Las direcciones de multicast de OSPFv2 son de 224.0.0.5 y 224.0.0.6; OSPFv6 utiliza las direcciones de multicast FF02::5 para todos los routers OSPF y FF02::6 para todos los DR y BDR. Los routers que ejecutan OSPFv3 pueden soportar varias direcciones por interfaz, incluyendo la dirección link-local, la dirección global, la dirección de multicast, las dos direcciones de OSPFv3, etc.

OSPFv2 construye las relaciones entre redes con términos tales como "red" o "subred", lo que implica una dirección IP específica en una interfaz. En cambio OSPFv3 solamente se ocupa de la conexión a través del enlace hacia su vecino, por lo tanto, en la terminología en OSPFv3 se habla de "*link*". La dirección link-local es el origen de las actualizaciones y no de la dirección local de unicast.

La autenticación no se incluye dentro de la versión 3. OSPFv3 confía en las capacidades de IPv6 para proporcionar autenticación y encriptación utilizando extensiones de cabecera.

OSPFv3 y OSPFv2 utilizan un conjunto de LSA similares, pero que no son del todo idénticas.

### Configuración

En general la mayoría de los comandos para OSPFv2 son similares a OSPFv3 añadiendo el parámetro `ipv6`. Asumiendo que IPv6 está habilitado y que las direcciones IPv6 están configuradas correctamente en las interfaces correspondientes, los comandos para habilitar OSPFv3 son los siguientes.

Habilitar el enrutamiento IPv6 y el enrutamiento OSPFv3 con los comandos de configuración global:

```text
Router(config)# ipv6 unicast-routing
Router(config)# ipv6 router ospf proceso
Router(config-rtr)# router-id número
```

Identificar el área en la que participa cada interfaz.

```text
Router(config-if)# ipv6 ospf proceso area número
Router(config-if)# ipv6 ospf priority priority
Router(config-if)# ipv6 ospf cost interface-cost
```

El router ID debe ser un número de 32 bits en formato de dirección decimal IPv4 y tiene que ser único; se puede utilizar para este valor una dirección IPv4 ya establecida en el router. La prioridad funciona de la misma manera que OSPFv2, el valor por defecto de la prioridad es 1. El router con mayor prioridad tiene más posibilidades de ser DR o BDR, mientras que 0 significa que el router no participará de dicha elección.

El coste permanece igual en ambas versiones, que por defecto es inversamente proporcional al ancho de banda de la interfaz. El coste se puede modificar con el comando `ipv6 ospf cost`.

Opcionalmente puede configurarse el comando `passive-interface` para evitar que los vecinos descubran la interfaz.

### Verificación

Para la verificación de OSPFv3 se pueden emplear muchos de los comandos de la versión 2 con el añadido del parámetro `ipv6`.

- `show ipv6 route`: muestra la tabla de enrutamiento IPv6.
- `show ipv6 protocols`: muestra los parámetros del protocolo.
- `show ipv6 ospf neighbors`: muestra la información de los vecinos OSPFv3. Añadir el parámetro `detail` sirve para mostrar detalles más específicos acerca de los vecinos OSPFv3.
- `debug ipv6 ospf events`: muestra adyacencias, DR, inundaciones, etc.

```text
RouterA# show ipv6 ospf
Routing Process "ospfv3 1" with ID 10.255.255.1
SPF schedule delay 5 secs, Hold time between two SPFs 10 secs
Minimum LSA interval 5 secs. Minimum LSA arrival 1 secs
LSA group pacing timer 240 secs
Interface flood pacing timer 33 msecs
Retransmission pacing timer 66 msecs
Number of external LSA 0. Checksum Sum 0x000000
Number of areas in this router is 2. 2 normal 0 stub 0 nssa
Area BACKBONE(0) (Inactive)
Number of interfaces in this area is 1
 SPF algorithm executed 1 times
Number of LSA 1. Checksum Sum 0x008A7A
Number of DCbitless LSA 0
Number of indication LSA 0
Number of DoNotAge LSA 0
Flood list length 0
Area 1
Number of interfaces in this area is 1
 SPF algorithm executed 9 times
Area ranges are
 2001:0:1::/80  Passive  Advertise
Number of LSA 9. Checksum Sum 0x05CCFF
Number of DCbitless LSA 0
Number of indication LSA 0
Number of DoNotAge LSA 0
Flood list length 0
```

```text
Router# show ipv6 ospf neighbor detail
Neighbor 172.16.3.3
  In the area 1 via interface FastEthernet0/0
  Neighbor: interface-id 3,
  link-local address FE80::205:5FFF:FED3:5808
Neighbor priority is 1, State is FULL, 6 state changes
  DR is 172.16.6.6 BDR is 172.16.3.3
  Options is 0x63F813E9
  Dead timer due in 00:00:33
  Neighbor is up for 00:09:00
  Index 1/1/2, retransmission queue length 0, number of retransmission 2
  First 0x0(0)/0x0(0)/0x0(0) Next 0x0(0)/0x0(0)/0x0(0)
  Last retransmission scan length is 1, maximum is 2
  Last retransmission scan time is 0 msec, maximum 0 msec
```

## BGP

BGP (*Border Gateway Protocol*) es un protocolo tipo *path-vector*, aunque mantiene muchas características comunes con los de vector-distancia, diseñado para ser escalable y poder utilizarse en grandes redes creando rutas estables entre las organizaciones. Las rutas son registradas de acuerdo con los sistemas autónomos por donde está pasando y los bucles son evitados rechazando aquellas rutas que tienen el mismo número de sistema autónomo al cual están llegando.

Soporta enrutamiento entre dominios. Los dispositivos, equipos y redes controlados por una organización son llamados sistemas autónomos, AS. Esto significa independencia, es decir, que cada organización es independiente de elegir la forma de conducir el tráfico y no se los puede forzar a cambiar dicho mecanismo. Por lo tanto, BGP comunica los AS con independencia de los sistemas que utilice cada organización.

Mientras que los IGP están buscando la última información y ajustando constantemente las rutas acordes con la nueva información que se recibe, BGP está diseñado para que las rutas sean estables y que no se estén advirtiendo e intercambiando constantemente. BGP pretende que las redes permanezcan despejadas de tráfico innecesario el mayor tiempo posible.

Existen dos tipos de BGP:

- **BGP externo (eBGP):** es el protocolo de enrutamiento utilizado entre diferentes sistemas autónomos.
- **BGP interno (iBGP):** es el protocolo de enrutamiento utilizado entre routers en el mismo AS.

Este libro se centra en conceptos básicos sobre eBGP.

Como protocolo de enrutamiento externo BGP es utilizado para conectar hacia y desde Internet y para enrutar tráfico dentro de Internet. Existen varias formas de conectar un AS a un ISP. Las principales son las siguientes:

- **Multi-homed:** conexión a Internet que utiliza enlaces redundantes hacia múltiples ISPs u otros AS. Es importante controlar cuánto tráfico de enrutamiento se quiere recibir desde Internet.
- **Single-homed:** este tipo de conexión a Internet utiliza un solo ISP o una única conexión a otro AS. El enrutamiento es muy sencillo teniendo en cuenta que solo existe un camino para alcanzar a cualquier destino de Internet.

La manera más fácil de conectarse a Internet son las rutas por defecto desde todos los proveedores, proporcionando una ruta redundante en caso de que la principal falle. Si solo se recibe una ruta de cada proveedor la utilización de memoria y CPU es muy baja. El punto negativo es que no siempre se elegirán los caminos más cortos, el tráfico se dirigirá simplemente hacia el router frontera más cercano. Si las necesidades de la organización no son exigentes, este tipo de conexión es la adecuada.

Existen tres formas de conectarse a Internet:

1. Aceptar solo rutas por defecto desde todos los ISP. En este caso los consumos de recursos serán muy bajos y la selección de rutas se hará utilizando el router BGP más cercano. Algunos de los problemas que pueden surgir es el enrutamiento subóptimo (menos adecuado).
2. Aceptar algunas rutas, más las rutas por defecto desde los ISP. En este caso el consumo de recursos de memoria y CPU será medio. El router seleccionará la ruta específica y si no la conoce lo hará a través del router BGP más cercano. Puede producirse enrutamiento sub-óptimo con las redes conectadas más allá del ISP.
3. Aceptar todas las rutas desde todos los ISP; en este caso el consumo de recursos es alto, pero en contra posición siempre se elegirá la ruta más directa.

La autenticación es una parte importante en BGP, sobre todo para proveedores de servicios. Sin autenticación estos ISP estarían expuestos a múltiples ataques desde Internet. La autenticación de BGP consiste en abordar una clave o contraseña entre los vecinos, de tal manera que se envíe un hash MD5 con cada paquete BGP.

### Configuración básica

BGP ha sido diseñado para conectar diferentes sistemas autónomos entre sí. Los pasos para habilitar BGP consisten en identificar el sistema autónomo local e identificar a los vecinos con su correspondiente sistema autónomo. La configuración también debe incluir las redes que se quieren anunciar.

Para iniciar el proceso BGP se utiliza la siguiente sintaxis:

```text
Router(config)# router bgp autonomous-system-number
```

A diferencia de muchos otros protocolos, BGP solo puede ejecutar un proceso en cada router. Al intentar configurar más de un proceso BGP el router mostrará el número de proceso que se está ejecutando actualmente.

BGP no se conecta a otros routers de manera automática, hay que predefinirlos. El comando `neighbor` es utilizado para definir cada uno de los vecinos y su correspondiente sistema autónomo. Si el AS del vecino es el mismo que el local, habrá una conexión iBGP (*Internal BGP*); si el vecino posee un AS diferente, la conexión es eBGP (*External BGP*). Una vez que los vecinos son definidos habrá más comandos dentro del comando `neighbor` que se utilizarán para definir las políticas del filtrado de rutas, etc.

La siguiente sintaxis muestra la configuración del comando `neighbor`:

```text
Router(config-router)# neighbor ip-address remote-as autonomous-system-number
```

El comando `network` configura las redes que van a ser originadas por este router. Hay una diferencia notable entre el uso del comando `network` en BGP y en otros protocolos de enrutamiento. Con este comando no se identifican las interfaces que van a ejecutar BGP, sino que se identifican las redes que se van a propagar. Se pueden utilizar múltiples comandos `network`, tantos como se requiera. El parámetro de la máscara es muy útil en BGP, puesto que puede funcionar con *subnetting* y *supernetting*. La sintaxis del comando es la siguiente:

```text
Router(config-router)# network network-number mask network-mask
```

Un *peer-group* es un grupo de vecinos que comparten la misma política de actualizaciones. Los routers son listados como miembros del mismo peer-group, de tal manera que las políticas asociadas con el grupo lo serán también del router. De esta forma las políticas son aplicadas a cada vecino, aunque también se pueden definir parámetros individuales personalizando a cada uno de los vecinos, además de aplicar una regla general propia del peer-group.

El comando `neighbor peer-group-name` es utilizado para crear el peer-group y asociar a los pares dentro de un sistema autónomo. Una vez que el peer-group ha sido definido, los miembros son configurados con el comando `neighbor peer-group`.

```text
Router(config-router)# neighbor peer-group-name peer-group
Router(config-router)# neighbor ip-address | peer-group-name remote-as autonomous-system-number
Router(config-router)# neighbor ip-address peer-group peer-group-name
```

La configuración de BGP puede resultar larga y tediosa y se trata mucho más en profundidad en el CCNP R&S. Estos son únicamente los conceptos básicos que entran en el temario del CCNA R&S.

### Verificación

Los comandos `show` para BGP brindan una información clara acerca de las sesiones de BGP y de las opciones de enrutamiento:

- `show ip bgp`: muestra la tabla de enrutamiento de BGP.

```text
Router# show ip bgp
BGP table version is 22, local router ID is 192.168.0.231
Status codes: s suppressed, d damped, h history, * valid, > best,
              i - internal, r RIB-failure
Origin codes: i - IGP, e - EGP, ? - incomplete
Network          Next Hop        Metric LocPrf Weight Path
*>i4.0.0.0         100.2.4.4         0     100      0    400 I
*>i5.0.0.0         100.2.3.2         0     100      0    300 I
*>i100.2.3.0/29    100.2.3.2         0     100      0    300 I
*>i100.2.4.0/29    100.2.4.4         0     100      0    400 I
*>i130.16.0.0      100.2.3.2         0     100      0    300 I
r>i167.55.0.0      167.55.191.3  281600     100      0    I
```

- `show ip bgp neighbors`: muestra la información de la conexión TCP hacia los vecinos, así como el tipo y número de mensajes BGP que están intercambiándose con cada vecino. Cuando la conexión se establece los vecinos intercambian actualizaciones.

```text
Router# show ip bgp neighbors
BGP neighbor is 10.1.1.1, remote AS 100, external
BGP version 4, remote router ID 172.31.2.3
BGP state = Established, up for 00:19:10
```

- `show processes cpu`: muestra los procesos activos y se usa para identificar los procesos que consumen demasiados recursos; pueden ordenarse por cantidad de recursos consumidos.
- `show ip bgp summary`: muestra el estado de las sesiones de BGP y también el número de prefijos aprendidos en cada sesión.

Otro comando de gran utilidad es el `debug`; como todos estos comandos debe utilizarse con la debida precaución. Mostrará la información real de los eventos que se están ejecutando:

```text
Router# debug ip bgp [dampening | events | keepalives | updates]
```

!!! note "NOTA"

    La configuración de BGP puede ser muy extensa y complicada. BGP no se ve en su totalidad en este libro.

## Caso práctico

### Configuración de EIGRP

La sintaxis muestra la configuración de un sistema autónomo 100 con EIGRP.

```text
Madrid(config)# router eigrp 100
Madrid(config-router)# network 172.16.128.0 0.0.15.255
Madrid(config-router)# network 172.16.64.0 0.0.15.255
Madrid(config-router)# eigrp log-neighbor-changes
Madrid(config)# interface serial 0/0
Madrid(config-if)# ip address 172.16.128.1 255.255.255.240
Madrid(config-if)# bandwidth 64
Madrid(config-if)# clock rate 250000
Madrid(config-if)# no shutdown
Madrid(config)# interface serial 0/1
Madrid(config-if)# ip address 172.16.64.1 255.255.255.240
Madrid(config-if)# bandwidth 64
Madrid(config-if)# clock rate 250000
Madrid(config-if)# no shutdown
```

```text
Madrid# show ip eigrp neighbors
IP-EIGRP neighbors for process 100
H  Address       Interface Hold Uptime   SRTT RTO  Q  Seq
                   (sec)         (ms) Cnt Num
0  172.16.128.2  Se0/0       12  00:09:12   40 1000  0   8
1  172.16.64.2   Se0/1       11  00:05:01   40 1000  0   6
```

```text
Madrid# show ip route
Codes: L-local, C-connected, S-static, R-RIP, M-mobile, B-BGP
       D-EIGRP, EX-EIGRP external, O-OSPF, IA-OSPF inter area
       N1-OSPF NSSA external type 1, N2-OSPF NSSA external type 2
       E1-OSPF external type 1, E2 OSPF external type 2, E-EGP
       i-IS-IS,L1-IS-IS level-1,L2-IS-IS level-2,ia-IS-IS inter area
       *-candidate default, U-per-user static route, o-ODR
       P-periodic downloaded static route

Gateway of last resort is not set

172.16.0.0/16 is variably subnetted, 4 subnets, 2 masks
C 172.16.64.0/28 is directly connected, Serial0/1
L 172.16.64.1/32 is directly connected, Serial0/1
C 172.16.128.0/28 is directly connected, Serial0/0
L 172.16.128.1/32 is directly connected, Serial0/0
D 192.168.10.0/24 [90/405122] via 172.16.128.2, 00:02:36, Serial0/0
D 204.10.20.0/24 [90/4051225] via 172.16.64.2, 00:00:11, Serial0/1
```

```text
Madrid# debug eigrp packets
EIGRP Packets debugging is on
 (UPDATE, REQUEST, QUERY, REPLY, HELLO, ACK )
Madrid#
EIGRP: Received HELLO on Serial0/1 nbr 172.16.64.2
  AS 100, Flags 0x0, Seq 9/0 idbQ 0/0
EIGRP: Received HELLO on Serial0/0 nbr 172.16.128.2
  AS 100, Flags 0x0, Seq 9/0 idbQ 0/0
EIGRP: Sending HELLO on Serial0/0
  AS 100, Flags 0x0, Seq 9/0 idbQ 0/0 iidbQ un/rely 0/0
EIGRP: Sending HELLO on Serial0/1
  AS 100, Flags 0x0, Seq 9/0 idbQ 0/0 iidbQ un/rely 0/0
EIGRP: Received HELLO on Serial0/1 nbr 172.16.64.2
  AS 100, Flags 0x0, Seq 9/0 idbQ 0/0
```

### Configuración de filtro de ruta

En el ejemplo que sigue se han creado dos listas de acceso estándar: la ACL 10 denegará cualquier información de enrutamiento de la red 192.168.20.0, mientras que la ACL 20 enviará información de enrutamiento EIGRP de la red 200.20.20.0. Ambas listas se asocian al protocolo de enrutamiento EIGRP 100.

```text
Router# configure terminal
Router(config)# access-list 10 deny 192.168.50.0 0.0.0.255
Router(config)# access-list 10 permit any
Router(config)# access-list 20 permit 200.20.20.0 0.0.0.255
Router(config)# router eigrp 100
Router(config-router)# distribute-list 10 in Serial 0/0
Router(config-router)# distribute-list 20 out Serial 0/1
Router(config-router)# network 172.16.0.0
Router(config-router)# network 192.168.10.0
```

### Configuración de redistribución estática

En el ejemplo se ilustra un router como única salida y entrada para el sistema autónomo 100. La distribución estática permite que todos los routers implicados en el mismo sistema conozcan la ruta estática como salida predeterminada.

```text
Borde(config)# ip route 192.168.0.0 255.255.255.0 220.20.20.1 120
Borde(config)# router eigrp 100
Borde(config-router)# network 192.168.1.0
Borde(config-router)# network 200.200.10.0
Borde(config-router)# redistribute static
Borde(config-router)# passive-interface serial 0
```

### Configuración de OSPF en una sola área

En el ejemplo se muestra la sintaxis de la configuración de OSPF 100 en un router (RouterDR).

```text
RouterDR(config)# router ospf 100
RouterDR(config-router)# network 192.168.0.0 0.0.0.255 area 0
RouterDR(config-router)# network 192.170.0.0 0.0.0.255 area 0
RouterDR(config-router)# network 192.178.0.0 0.0.0.255 area 0
RouterDR(config-router)# area 0 authentication
RouterDR(config-router)# area 0 authentication message-digest
RouterDR(config-router)# exit
RouterDR(config)# interface loopback 1
RouterDR(config-if)# ip address 200.200.10.10 255.255.255.0
RouterDR(config-if)# exit
RouterDR(config)# interface Giga 0/0
RouterDR(config-if)# ip address 192.168.0.2 255.255.255.0
RouterDR(config-if)# no shutdown
RouterDR(config-if)# ip ospf priority 2
RouterDR(config-if)# bandwidth 64
RouterDR(config-if)# ip ospf cost 10
RouterDR(config-if)# ip ospf message-digest-key 1 md5 AlaKran
RouterDR(config-if)# ip ospf hello-interval 20
RouterDR(config-if)# ip ospf dead-interval 60
RouterDR(config-if)# exit
```

```text
RouterDR# show ip ospf
Routing Process "ospf 100" with ID 200.200.10.10
 Supports only single TOS(TOS0) routes
 Supports opaque LSA
SPF schedule delay 5 secs, Hold time between two SPFs 10 secs
Minimum LSA interval 5 secs. Minimum LSA arrival 1 secs
Number of external LSA 0. Checksum Sum 0x000000
Number of opaque AS LSA 0. Checksum Sum 0x000000
Number of DCbitless external and opaque AS LSA 0
Number of DoNotAge external and opaque AS LSA 0
Number of areas in this router is 1. 1 normal 0 stub 0 nssa
External flood list length 0
Area BACKBONE(0)
Number of interfaces in this area is 1
Area has no authentication
 SPF algorithm executed 3 times
Area ranges are
Number of LSA 2. Checksum Sum 0x017580
Number of opaque link LSA 0. Checksum Sum 0x000000
Number of DCbitless LSA 0
Number of indication LSA 0
Number of DoNotAge LSA 0
Flood list length
```

El router se ve a sí mismo listado en la lista de vecinos; si se observa en el `show ip ospf neighbor` del router remoto, el RouterDR aparecerá como DR a partir del ID tomado de la interfaz de loopback.

```text
RouterDR# sh ip ospf neighbor
Neighbor ID     Pri   State       Dead Time   Address       Interface
192.168.0.3       1   FULL/DROTHER 00:00:33   192.168.0.3   Gi0/0
192.168.0.5       1   FULL/DROTHER 00:00:33   192.168.0.5   Gi0/0
192.168.0.4       1   FULL/BDR     00:00:33   192.168.0.4   Gi0/0
```

```text
Remoto# sh ip ospf neighbor
Neighbor ID     Pri   State       Dead Time   Address       Interface
192.168.0.3       1   FULL/DROTHER 00:00:39   192.168.0.3   Gi0/0
192.168.0.5       1   FULL/DROTHER 00:00:39   192.168.0.5   Gi0/0
200.200.10.10     2   FULL/DR      00:00:39   192.168.0.2   Gi0/0
```

### Configuración de OSPF en múltiples áreas

Muchas de las configuraciones y comandos detallados en los párrafos anteriores pueden aplicarse al siguiente ejemplo. La figura ilustra una topología OSPF de múltiples áreas y los comandos utilizados para su configuración.

```text
RouterA(config)# router ospf 220
RouterA(config-router)# network 122.100.17.128 0.0.0.15 area 3
RouterA(config-router)# network 122.100.17.192 0.0.0.15 area 2
RouterA(config-router)# network 122.100.32.0 0.0.0.255 area 0
RouterA(config-router)# network 10.10.10.33 0.0.0.0 area 0
RouterA(config-router)# area 0 range 172.16.20.128 255.255.255.192
RouterA(config-router)# area 3 virtual-link 10.10.10.30
RouterA(config-router)# area 2 stub
RouterA(config-router)# area 3 stub no-summary
RouterA(config-router)# area 3 default-cost 15
RouterA(config-router)# interface loopback 0
RouterA(config-if)# ip address 10.10.10.33 255.255.255.255
RouterA(config-if)# interface FastEthernet0/0
RouterA(config-if)# ip address 122.100.17.129 255.255.255.240
RouterA(config-if)# ip ospf priority 100
RouterA(config-if)# interface FastEthernet0/1
RouterA(config-if)# ip address 122.100.17.193 255.255.255.240
RouterA(config-if)# ip ospf cost 10
RouterA(config-if)# interface FastEthernet1/0
RouterA(config-if)# ip address 122.100.32.10 255.255.255.240
RouterA(config-if)# no keepalive
RouterA(config-if)# exit
```

```text
RouterM(config)# loopback interface 0
RouterM(config-if)# ip address 10.10.10.30 255.255.255.255
RouterM(config)# router ospf 220
RouterM(config-router)# network 172.16.20.32 0.0.0.7 area 5
RouterM(config-router)# network 10.10.10.30 0.0.0.0 area 0
RouterM(config-router)# area 3 virtual-link 10.10.10.33
```

### Configuración básica de OSPFv3

La configuración básica de OSPFv3 del router A se muestra en la siguiente sintaxis, mientras que el router B está configurado de una manera similar:

```text
RouterA# configure terminal
RouterA(config)# ipv6 unicast-routing
RouterA(config)# ipv6 cef
RouterA(config)# ipv6 router ospf 1
RouterA(config-rtr)# router-id 10.255.255.1
RouterA(config-rtr)# interface fastethernet0/0
RouterA(config-if)# description Local LAN
RouterA(config-if)# ipv6 address 2001:0:1:1::2/64
RouterA(config-if)# ipv6 ospf 1 area 1
RouterA(config-if)# ipv6 ospf cost 10
RouterA(config-if)# ipv6 ospf priority 20
RouterA(config-if)# interface serial 1/0
RouterA(config-if)# description multi-point line to Internet
RouterA(config-if)# ipv6 address 2001:0:1:5::1/64
RouterA(config-if)# ipv6 ospf 1 area 0
RouterA(config-if)# ipv6 ospf priority 20
```

!!! tip "RECUERDE"

    En principio, el router intentará utilizar un ID buscando interfaces virtuales o loopback; si no encuentra configuración de las mismas lo hará con la interfaz física con la dirección IP más alta.

    Los valores de los intervalos de Hello y de Dead deben coincidir en los router adyacentes para que OSPF funcione correctamente.

    Ante la posibilidad de flapping los routers esperan unos instantes antes de recalcular su tabla de enrutamiento.

!!! tip "RECUERDE"

    OSPF mantiene la información de enrutamiento siguiendo este orden:

    1. Un router advierte un cambio de estado de un enlace y hace una multidifusión de un paquete LSU (actualización de estado de enlace) con la IP 224.0.0.6.
    2. El DR acusa recepción e inunda la red con la LSU utilizando la dirección de multidifusión 224.0.0.5.
    3. Si se conecta un router con otra red, reenviará la LSU al DR de dicha red.
    4. Cuando un router recibe la LSU que incluye la LSA (publicación de estado de enlace) diferente, cambiará su base de datos.

!!! note "NOTA"

    Muchos de los comandos utilizados a lo largo de este capítulo poseen gran cantidad de parámetros opcionales; para facilitar el aprendizaje estos han sido simplificados.

### Configuración básica de BGP

El ejemplo que sigue muestra la configuración básica de los comandos requeridos para que BGP funcione entre sistemas autónomos. Según muestra la topología, el router A en el AS-200 está conectado a los routers en los AS-300, AS-400, AS-500 y AS-600.

```text
RouterA(config)# interface Serial0/0.1
RouterA(config-int)# ip address 190.55.5.201 255.255.255.252
!
RouterA(config)# interface Serial0/0.2
RouterA(config-int)# ip address 190.55.5.205 255.255.255.252
!
RouterA(config)# interface Serial0/0.3
RouterA(config-int)# ip address 190.55.5.209 255.255.255.252
!
RouterA(config)# interface Serial0/0.4
RouterA(config-int)# ip address 190.55.5.213 255.255.255.252
!
RouterA(config)# router bgp 200
RouterA(config-router)# neighbor 190.55.5.202 remote-as 300
RouterA(config-router)# neighbor 190.55.5.206 remote-as 400
RouterA(config-router)# neighbor 190.55.5.210 remote-as 500
RouterA(config-router)# neighbor 190.55.5.214 remote-as 600
RouterA(config-router)# network 190.10.35.8 255.255.255.252
RouterA(config-router)# network 190.10.27.0 255.255.255.0
RouterA(config-router)# network 190.10.100.0 255.255.255.0
```

## Fundamentos para el examen

- Recuerde las condiciones necesarias para la utilización de rutas estáticas.
- Analice las diferencias entre las rutas estáticas y las rutas estáticas por defecto, cuáles emplear en cada situación y los comandos para su configuración.
- Tenga en cuenta las directrices recomendables a la hora de configurar un enrutamiento estático.
- Recuerde conceptos aprendidos como métrica, distancia administrativa, sistema autónomo, IGP y EGP.
- Estudie el funcionamiento de RIPv1, RIPv2 y RIPng y compárelos.
- Recuerde los conceptos fundamentales sobre el tipo de protocolo que es EIGRP, su funcionamiento, tipos de tablas que utiliza y topologías.
- Analice el funcionamiento de DUAL y cómo descubre las rutas.
- Estudie las métricas utilizadas por EIGRP, cuáles son las constantes y cómo funcionan y las que lo hacen por defecto.
- Observe las diferencias entre EIGRPv4 y EIGRPv6.
- Estudie todos los comandos completos utilizados para la configuración de EIGRP, incluidos los de verificación de funcionamiento.
- Memorice los conceptos fundamentales sobre el tipo de protocolo que es OSPF, su funcionamiento y los tipos de tablas que utiliza.
- Recuerde las diferentes topologías sobre las que puede funcionar OSPF, en qué caso existe elección de DR y BDR y cómo se hace tal elección.
- Analice la métrica y elección de ruta de OSPF.
- Estudie todos los comandos completos utilizados para la configuración de OSPF, incluidos los de verificación de funcionamiento.
- Tenga un concepto claro del funcionamiento de OSPF en múltiples áreas.
- Observe las diferencias entre OSPFv2 y OSPFv3.
- Estudie los conceptos básicos de funcionamiento de BGP.
- Tenga en claro cuáles son las diferencias entre un iBGP y un eBGP.
- Practique las configuraciones en dispositivos reales o en simuladores.
