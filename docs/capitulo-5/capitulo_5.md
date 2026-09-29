# Conceptos de enrutamiento

## Determinación de rutas IP

Para que un dispositivo de capa tres pueda determinar la ruta hacia un destino debe tener conocimiento de las diferentes rutas hacia él y cómo hacerlo. El aprendizaje y la determinación de estas rutas se lleva a cabo mediante un proceso de enrutamiento dinámico a través de cálculos y algoritmos que se ejecutan en la red o enrutamiento estático ejecutado manualmente por el administrador o incluso ambos métodos.

La información de enrutamiento que el router aprende desde sus fuentes se coloca en su propia tabla de enrutamiento. El router se vale de esta tabla para determinar los puertos de salida que debe utilizar para retransmitir un paquete hasta su destino.

La tabla de enrutamiento es la fuente principal de información del router acerca de las redes. Si la red de destino está conectada directamente, el router sabrá de antemano el puerto que debe usar para reenviar paquetes. Si las redes de destino no están conectadas directamente, el router debe aprender y calcular la ruta óptima a usar para reenviar paquetes a dichas redes. La tabla de enrutamiento se construye mediante uno de estos dos métodos o ambos:

- **Rutas estáticas:** aprendidas por el router a través del administrador, que establece dicha ruta manualmente, quien también debe actualizar cuando tenga lugar un cambio en la topología.
- **Rutas dinámicas:** rutas aprendidas automáticamente por el router a través de la información enviada por otros routers, una vez que el administrador ha configurado un protocolo de enrutamiento que permite el aprendizaje dinámico de rutas.

Para poder enrutar paquetes de información un router debe conocer lo siguiente:

- **Dirección de destino:** dirección a donde han de ser enviados los paquetes.
- **Fuentes de información:** fuente (otros routers) de donde el router aprende las rutas hasta los destinos especificados.
- **Descubrir las posibles rutas hacia el destino:** rutas iniciales posibles hasta los destinos deseados.
- **Seleccionar las mejores rutas:** determinar cuál es la mejor ruta hasta el destino especificado.
- **Mantener las tablas de enrutamiento actualizadas:** mantener conocimiento actualizado de las rutas al destino.

### Distancia administrativa

Los routers son multiprotocolo, lo que quiere decir que pueden utilizar al mismo tiempo diferentes protocolos incluidas rutas estáticas. Si varios protocolos proporcionan la misma información de enrutamiento se les debe otorgar un valor administrativo. La distancia administrativa permite que un protocolo tenga mayor prioridad sobre otro si su distancia administrativa es menor. Este valor viene por defecto, sin embargo el administrador puede configurar un valor diferente si así lo determina.

El rango de las distancias administrativas varía de 1 a 255 y se especifica en la siguiente tabla:

| Origen de la ruta | Distancia administrativa |
| --- | --- |
| Interfaz física | 0 |
| Ruta estática | 1 |
| Ruta sumarizada EIGRP | 5 |
| BGP externo | 20 |
| EIGRP interno | 90 |
| IGRP | 100 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| EIGRP externo | 170 |
| BGP interno | 200 |
| Inalcanzable | 255 |

#### Métricas

Las métricas utilizadas habitualmente por los protocolos de enrutamiento pueden calcularse basándose en una sola o en múltiples características de la ruta. Existen diferentes protocolos de enrutamiento y cada uno utiliza métricas diferentes.

- **Número de saltos:** número de routers por los que pasará un paquete.
- **Tic tac (Novell):** retraso en un enlace de datos usando pulsos de reloj de PC IBM (msg).
- **Coste:** valor arbitrario, basado generalmente en el ancho de banda, el coste económico u otra medida, que puede ser asignado por un administrador de red.
- **Ancho de banda:** capacidad de datos de un enlace. Por ejemplo, un enlace Ethernet de 10Mb será preferible normalmente a una línea dedicada de 64Kb.
- **Retraso:** tiempo en mover un paquete de un origen a un destino.
- **Carga:** cantidad de actividad existente en un recurso de red, como un router o un enlace.
- **Fiabilidad:** normalmente, se refiere al valor de errores de bits de cada enlace de red.
- **MTU (*Maximum Transmission Unit*):** longitud máxima de trama en octetos que puede ser aceptada por todos los enlaces de la ruta.

Los valores de la métrica y de la distancia administrativa pueden verse en la tabla de enrutamiento encerrado entre corchetes. El ejemplo se basa en una topología OSPF, donde el primero de los valores corresponde a la DA (110) y el segundo a la métrica.

```text
Router#show ip route
Gateway of last resort is not set
172.16.0.0/16 is variably subnetted, 3 subnets, 2 masks
O E2   172.16.20.128/29 [110/20] via 172.16.20.9, 00:00:29, Serial1
O IA  172.16.20.128/26 [110/74] via 172.16.20.9, 00:01:29, Serial1
C      172.16.20.8/29 is directly connected, Serial1
O E2   192.168.0.0/24 [110/20] via 172.16.20.9, 00:01:29, Serial1
```

## Enrutamiento estático

Las rutas estáticas se definen administrativamente y establecen rutas específicas que han de seguir los paquetes para pasar de un puerto de origen hasta un puerto de destino. Se establece un control preciso del enrutamiento según los parámetros del administrador.

Las rutas estáticas por defecto (default) especifican una puerta de enlace (gateway) de último recurso, a la que el router debe enviar un paquete destinado a una red que no aparece en su tabla de enrutamiento, es decir, que desconoce.

Las rutas estáticas se utilizan habitualmente en enrutamientos desde una red hasta una red de conexión única, ya que no existe más que una ruta de entrada y salida en una red de conexión única, evitando de este modo la sobrecarga de tráfico que genera un protocolo de enrutamiento.

La ruta estática se configura para conseguir conectividad con un enlace de datos que no esté directamente conectado al router. Para conectividad de extremo a extremo, es necesario configurar la ruta en ambas direcciones. Las rutas estáticas permiten la construcción manual de la tabla de enrutamiento.

El comando `ip route` configura una ruta estática, los parámetros siguientes al comando definen la ruta estática.

Una ruta estática se representa con una "S" en la tabla de enrutamiento:

```text
Router#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP,
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area,
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2,
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP,
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1,
       L2 - IS-IS level-2, ia - IS-IS inter area, * - candidate default,
       U - per-user static route, o - ODR, P - periodic downloaded static route

Gateway of last resort is not set
161.44.0.0/24 is subnetted, 1 subnets
C       161.44.192.0 is directly connected, Ethernet0
131.108.0.0/24 is subnetted, 1 subnets
C       131.108.99.0 is directly connected, Serial0
S       198.10.1.0/24 [1/0] via 161.44.192.2
```

!!! note "NOTA"
    Es necesario configurar una ruta estática en sentido inverso para conseguir una comunicación en ambas direcciones.

### Rutas estáticas por defecto

Una ruta estática por defecto (default), predeterminada o de último recurso es un tipo especial de ruta estática que se utiliza cuando no se conoce una ruta hasta un destino determinado, o cuando no es posible almacenar en la tabla de enrutamiento la información relativa a todas las rutas posibles.

```text
Router_B(config)#ip route 0.0.0.0 0.0.0.0 Serial 0
```

El gráfico ilustra un ejemplo de utilización de una ruta estática por default, el router B tiene configurada la ruta por defecto hacia el exterior como única salida/entrada del sistema autónomo 100, los demás routers aprenderán ese camino gracias a la redistribución que el protocolo hará dentro del sistema autónomo.

Una ruta estática por defecto se representa con una "S*" en la tabla de enrutamiento.

```text
Router#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP,
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area,
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2,
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP,
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1,
       L2 - IS-IS level-2, ia - IS-IS inter area, * - candidate default,
       U - per-user static route, o - ODR, P - periodic downloaded static route

Gateway of last resort is 161.44.192.2 to network 198.10.1.0
161.44.0.0/24 is subnetted, 1 subnets
C       161.44.192.0 is directly connected, Ethernet0
131.108.0.0/24 is subnetted, 1 subnets
C       131.108.99.0 is directly connected, Serial0
S*      198.10.1.0/24 [1/0] via 161.44.192.2
```

### Rutas estáticas flotantes

Una ruta estática flotante es una ruta estática que el router utiliza para respaldar una ruta dinámica. Debe configurar una ruta estática flotante con una distancia administrativa más alta que la ruta dinámica a la que hará de respaldo.

Recuerde que el router basa su decisión en el concepto de distancia administrativa (AD). La ruta que tenga una distancia administrativa más baja será la que se escoja como primera opción para alcanzar la red de destino y la otra quedará como respaldo. En este caso, el router escogerá la ruta dinámica ante una ruta estática flotante. Se puede utilizar una ruta estática flotante. Por lo tanto, una ruta estática se puede utilizar como una ruta estática flotante con una distancia administrativa más alta que la ruta dinámica como alternativa si se pierde la ruta aprendida por el protocolo de enrutamiento.

### Rutas locales

En las nuevas versiones de Cisco aparecen en la tabla de enrutamiento rutas identificadas como "L". Las rutas locales de IPv6 han existido siempre, mientras que las rutas locales o rutas de host IPv4 fueron añadidas a partir de la característica de enrutamiento Multi-topología (MTR).

Las rutas de host permiten ver en la tabla de enrutamiento la dirección IP de la interfaz del router, mientras que con las versiones anteriores la "C" únicamente identificaba a la red directamente conectada.

Hay tres maneras de crear una ruta de host:

- Automáticamente, Cisco IOS instala una ruta de host cuando una dirección de interfaz está configurada en el router.
- Manualmente, como una ruta estática configurada para dirigir el tráfico a un dispositivo de destino específico.
- Una ruta de host se obtiene de forma automática a través de otros métodos.

En el siguiente ejemplo las direcciones IP asignadas a Ethernet0/0 son 10.1.1.1/30 para IPv4 y 2001:db8::1/64 para el IPv6. Ningunas son rutas de host. Recuerde que una ruta host para el IPv4 tiene la máscara /32, y una ruta de host para el IPv6 tiene la máscara /128.

Para cada direccionamiento IPv4 y IPv6, Cisco IOS instala las rutas de host en las tablas de enrutamiento respectivas. Las rutas locales se identifican con una "L" en la salida del comando `show ip route`. Ahora las direcciones 10.1.1.1/32 y 2001:db8::1/128 aparecen como rutas de host local respectivamente. La ruta FF00::/8 es también una ruta local, pero esta ruta es necesaria para el enrutamiento multicast:

```text
Router#show ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP,
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area,
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2,
       E1 - OSPF external type 1, E2 - OSPF external type 2, i - IS-IS,
       su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2,
       ia - IS-IS inter area, * - candidate default, U - per-user static route,
       o - ODR, P - periodic downloaded static route, H - NHRP,
       + - replicated route, % - next hop override

Gateway of last resort is not set
C       10.1.1.0/30 is directly connected, Ethernet0/0
L       10.1.1.1/32 is directly connected, Ethernet0/0

Router#show ipv6 route
IPv6 Routing Table - default - 3 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route,
       B - BGP, R - RIP, I1 - ISIS L1, I2 - ISIS L2, IA - ISIS interarea,
       IS - ISIS summary, D - EIGRP, EX - EIGRP external, ND - Neighbor Discovery,
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2,
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2
C       2001:DB8::/64 [0/0]
        via Ethernet0/0, directly connected
L       2001:DB8::1/128 [0/0]
        via Ethernet0/0, receive
L       FF00::/8 [0/0]
        via Null0, receive
```

Las rutas locales tienen la distancia administrativa de 0, que es la misma distancia administrativa que las rutas directamente conectadas "C". Sin embargo, cuando se configura la redistribución, se redistribuyen únicamente las rutas directamente conectadas, pero las rutas locales no.

El comando `show ipv6 route local` se utiliza para verificar solamente las rutas locales IPv6.

## Enrutamiento dinámico

Los cambios que una red puede experimentar hacen poco factible la utilización de rutas estáticas, el administrador se vería forzado a reconfigurar los routers ante cada cambio. El enrutamiento dinámico permite que los routers actualicen conocimientos ante posibles cambios sin tener que recurrir a nuevas configuraciones. Un protocolo de enrutamiento permite determinar dinámicamente las rutas y mantener actualizadas sus tablas.

Es importante diferenciar los protocolos enrutados y los de enrutamiento. Un protocolo enrutado lleva una completa información de capa tres, como TCP/IP, IPX, APPLE TALK, Net BEUI. Un protocolo de enrutamiento es el utilizado por los routers para mantener tablas de enrutamiento y así poder elegir la mejor ruta hacia un destino.

Existen dos grandes núcleos de protocolos de enrutamiento:

- **Protocolos de gateway interior (IGP):** se usan para intercambiar información de enrutamiento dentro de un sistema autónomo (RIP, EIGRP, OSPF).
- **Protocolos de gateway exterior (EGP):** se usan para intercambiar información de enrutamiento entre sistemas autónomos (BGP).

### Clases de protocolos de enrutamiento

Todos los protocolos de enrutamiento cumplen las mismas funciones, aprendiendo y determinando cuál es la mejor ruta hacia un destino.

Existen dos clases de protocolos de enrutamiento:

- **Vector distancia:** este tipo de protocolo determina la dirección y la distancia a cualquier red.
- **Estado de enlace:** estos protocolos poseen una idea exacta de la topología de la red y no efectúan actualizaciones a menos que ocurra un cambio en la topología.

Un tercer caso de protocolo de enrutamiento sería un método híbrido como es el caso de EIGRP, diseñado por Cisco, que combina aspectos de los dos casos anteriores.

Un protocolo de enrutamiento también puede clasificarse como classful (con clase) o classless (sin clase), es decir, que pueden no reconocer las máscaras de subred como en el caso de los classfull o sí pueden hacerlo en el caso de los classless.

Los routers que no pasan la información de las subredes son con clase, porque el router solo codifica la clase de red IP para la información de enrutamiento. En cuanto el direccionamiento IP fue adaptándose a las necesidades de crecimiento los protocolos se hicieron más sofisticados, pudiendo manipular máscaras de subred, estos protocolos son los llamados sin clase.

Un administrador puede habilitar el comando `ip classless` para el caso que se reciba un paquete hacia una subred desconocida, el router enviará ese paquete a la ruta predeterminada para enviar la trama al siguiente salto.

### Sistema autónomo

Un sistema autónomo (AS) es un conjunto de redes bajo un dominio administrativo común. El uso de números de sistema autónomos asignados por entidades (IANA, ARIN, RIPE) solo es necesario si el sistema utiliza algún BGP, o una red pública como Internet.

Los sistemas autónomos intercambian información a través de protocolos de gateway exterior como BGP.

## Enrutamiento vector distancia

Los algoritmos de enrutamiento basados en vectores pasan copias periódicas de una tabla de enrutamiento de un router a otro y acumulan vectores de distancia. Distancia es una medida de longitud, mientras que vector significa una dirección. Las actualizaciones regulares entre routers comunican los cambios en la topología. Cada protocolo de enrutamiento basado en vectores de distancia utiliza un algoritmo distinto para determinar la ruta óptima. El algoritmo genera un número, denominado métrica de ruta, para cada ruta existente a través de la red. Normalmente cuanto menor es este valor, mejor es la ruta.

Los dos ejemplos típicos de protocolos por vector distancia son:

- **RIP (*Routing Information Protocol*):** protocolo suministrado con los sistemas UNIX. Es el protocolo de gateway interior (IGP) más comúnmente utilizado. RIP utiliza el número de saltos como métrica de enrutamiento. Existen dos versiones, RIP v1 como protocolo tipo classfull y RIP v2, más completo que su antecesor, como protocolo classless.
- **IGRP (*Interior Gateway Routing Protocol*):** protocolo desarrollado por Cisco para tratar los problemas asociados con el enrutamiento en redes de gran envergadura. IGRP es un protocolo tipo classfull.

## Bucles de enrutamiento

El proceso de mantener la información de enrutamiento puede generar errores si no existe una convergencia rápida y precisa entre los routers. En los diseños de redes complejas pueden producirse bucles o loops de enrutamiento. Los routers transmiten a sus vecinos actualizaciones constantes, si un router A recibe de B una actualización de una red que ha caído, este transmitirá dicha información a todos sus vecinos incluido el router B, quien primeramente le informó de la novedad, a su vez el router B volverá a comunicar que la red se ha caído al router A formándose un bucle interminable.

### Solución a los bucles de enrutamiento

Los protocolos vector distancia poseen diferentes métodos para evitar los bucles de enrutamiento, generalmente estas herramientas funcionan por sí mismas (por defecto); sin embargo, en algunos casos pueden desactivarse con el consiguiente riesgo que pudiera generar un bucle de red.

#### Horizonte dividido

Resulta sin sentido volver a enviar información acerca de una ruta a la dirección de donde ha venido la actualización original. A menos que el router conozca otra ruta viable al destino, horizonte dividido o *split horizon* no devolverá información por la interfaz donde la recibió.

#### Métrica máxima

Un protocolo de enrutamiento permite la repetición del bucle de enrutamiento hasta que la métrica exceda del valor máximo permitido. Los routers agregan a la información de enrutamiento la cantidad de saltos transcurridos desde el origen a medida que los paquetes son enrutados. En el caso de RIP el bucle solo estará permitido hasta que la métrica llegue a 16 saltos, cuando el paquete sume 16 saltos será descartado por RIP.

#### Envenenamiento de rutas

El router crea una entrada en la tabla donde guarda el estado coherente de la red en tanto que otros routers convergen gradualmente y de forma correcta después de un cambio en la topología. La actualización inversa es una operación complementaria del horizonte dividido. El objetivo es asegurarse de que todos los routers del segmento hayan recibido información acerca de la ruta envenenada. El router agrega a la información de enrutamiento la cantidad máxima de saltos, el envenenamiento utiliza la métrica máxima para indicar que se trata de una ruta inalcanzable.

#### Temporizadores de espera

Los temporizadores hacen que los routers no apliquen ningún cambio que pudiera afectar a las rutas durante un período de tiempo determinado. Si llega una actualización con una métrica mejor a la red inaccesible, el router se actualiza y elimina el temporizador. Si no recibe cambios óptimos dará por caída la red al transcurrir el tiempo de espera.

!!! tip "RECUERDE"
    Los protocolos vector distancia inundan la red con broadcast de actualizaciones de enrutamiento.

## Enrutamiento estado de enlace

Los protocolos de estado de enlace construyen tablas de enrutamiento basándose en una base de datos de la topología. Esta base de datos se elabora a partir de paquetes de estado de enlace que se pasan entre todos los routers para describir el estado de una red.

El algoritmo SPF (*Shortest Path First*) usa una base de datos para construir la tabla de enrutamiento. El enrutamiento por estado de enlace utiliza la información resultante del árbol SPF, a partir de los paquetes de estado de enlace (LSP) creando una tabla de enrutamiento con las rutas y puertos de toda la red.

Los protocolos de enrutamiento por estado de enlace recopilan la información necesaria de todos los routers de la red, cada uno de los routers calcula de forma independiente su mejor ruta hacia un destino. De esta manera se producen muy pocos errores al tener una visión independiente de la red por cada router.

Estos protocolos prácticamente no tienen limitaciones de saltos. Cuando se produce un fallo en la red el router que detecta el error utiliza una dirección multicast para enviar una tabla LSA, cada router recibe y la reenvía a sus vecinos. La métrica utilizada se basa en el coste, que surge a partir del algoritmo de Dijkstra y se basa en la velocidad del enlace.

Los protocolos de estado de enlace son protocolos de enrutamiento de gateway interior, se utilizan dentro de un mismo AS (*Autonomous System*), el que puede dividirse en sectores más pequeños como divisiones lógicas llamadas áreas. El área 0 es el área principal del AS. Este área también es conocida como área de *backbone*.

Los dos ejemplos típicos de protocolos de estado de enlace son:

- **IS-IS (*Intermediate System to Intermediate System*):** protocolo de enrutamiento jerárquico de estado de enlace casi en desuso hoy en día.
- **OSPF (*Open Shortest Path First*):** protocolo de enrutamiento por estado de enlace jerárquico, que se ha propuesto como sucesor de RIP en la comunidad de Internet. Entre las características de OSPF se incluyen el enrutamiento de menor coste, el enrutamiento de múltiples rutas y el balanceo de carga.

### Vector distancia Vs Estado de enlace

Los protocolos de estado de enlace son más rápidos y más escalables que los de vector distancia, algunas razones podrían ser:

- Los protocolos de estado de enlace solo envían actualizaciones cuando hay cambios en la topología.
- Las actualizaciones periódicas son menos frecuentes que en los protocolos por vector de distancia.
- Las redes que ejecutan protocolos de enrutamiento por estado de enlace soportan direccionamiento sin clase.
- Las redes con protocolos de enrutamiento por estado de enlace soportan resúmenes de ruta.
- Las redes que ejecutan protocolos de enrutamiento por estado de enlace pueden ser segmentadas en distintas áreas jerárquicamente organizadas, limitando así el alcance de los cambios de rutas.

!!! note "NOTA"
    El término convergencia hace referencia a la capacidad de los routers de poseer la misma información de enrutamiento actualizada. Las siglas VLSM son las de máscara de subred de longitud variable.

**La siguiente tabla compara las características de los protocolos de enrutamiento:**

| Característica | RIP | RIPv2 | IGRP | EIGRP | IS-IS | OSPF |
| --- | :---: | :---: | :---: | :---: | :---: | :---: |
| Vector distancia | X | X | X | X | | |
| Estado de enlace | | | | | X | X |
| Resumen automático de ruta | X | X | X | X | X | |
| Resumen manual de ruta | X | X | X | X | X | X |
| Soporte VLSM | | X | | X | X | X |
| Diseñado por Cisco | | | X | X | | |
| Convergencia | Lento | Lento | Lento | Muy rápido | Muy rápido | Muy rápido |
| Distancia administrativa | 120 | 120 | 100 | 90 | 115 | 110 |
| Tiempo de actualización | 30 | 30 | 90 | | | |
| Métrica | Saltos | Saltos | Compuesta | Compuesta | Coste | Coste |

!!! tip "RECUERDE"
    Mientras los campos IP se mantienen intactos a lo largo de la ruta, las tramas cambian en cada salto con la MAC correspondiente al salto siguiente.

## Fundamentos para el examen

- Tome en cuenta las diferencias entre enrutamiento estático y dinámico, aprendizaje de direcciones y cuál es la manera más adecuada para aplicarlas.
- Analice las condiciones básicas necesarias para la aplicación de rutas estáticas y rutas estáticas por defecto y cuáles son los parámetros de configuración de cada una de ellas.
- Recuerde qué es y para qué sirve un sistema autónomo.
- Recuerde qué es la distancia administrativa, cómo funciona en los procesos de enrutamiento y sus diferentes valores.
- Analice y assimile el funcionamiento de los protocolos de enrutamiento.
- Estudie cómo funciona un protocolo vector distancia, cuáles son y sus respectivas métricas.
- Analice la problemática de los bucles de enrutamiento y sus posibles soluciones razonando el funcionamiento de cada una de ellas.
- Recuerde para qué se utilizan los IGP y los EGP.
- Piense en qué consiste una ruta estática de respaldo o flotante.
- Estudie cómo funciona un protocolo de estado de enlace, cuáles son, sus jerarquías y compárelos con los de vector distancia.
- Recuerde la diferencia entre protocolos enrutables y de enrutamiento.
