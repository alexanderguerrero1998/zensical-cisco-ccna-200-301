# Calidad de servicio

## Convergencia de red

Actualmente las redes soportan diferentes tipos de aplicaciones tales como voz, vídeo y datos sobre una infraestructura común. La convergencia de todos estos tipos de aplicaciones conjuntas representa un reto para el personal administrador encargado de ello.

Muchas aplicaciones de datos están basadas en protocolos orientados a la conexión como TCP; cuando pierden un segmento es retransmitido otro, mientras que las aplicaciones de voz o vídeo tienen una tolerancia mínima hacia las pérdidas de datos. Debido a esto es necesario implementar mecanismos que prioricen determinados tipos de tráfico cuando exista congestión en la red. Los fallos en la red afectan a todas las aplicaciones, mientras que la red converge después de un fallo, quienes más sufren el desperfecto son los usuarios que estén usando aplicaciones interactivas de voz o vídeo, pudiendo incluso perder la llamada.

Existen cuatro cuestiones importantes a tener en cuenta en redes convergentes:

- Ancho de banda disponible.
- Retraso de extremo a extremo.
- Jitter o fluctuación en el retraso.
- Pérdida de paquetes.

### Ancho de banda disponible

Los paquetes normalmente fluyen usando el camino con mejor ancho de banda. El mejor ancho de banda disponible en la ruta es el del enlace con menor ancho de banda. En la siguiente figura se observa que la ruta a través de los router R1-R2-R3-R4 es el mejor camino del cliente al servidor y 10 Mbps es el máximo ancho de banda del camino.

La falta de ancho de banda hace que las aplicaciones se degraden debido al retraso y a la pérdida de paquetes. Esto es detectado de forma inmediata por los usuarios de aplicaciones de voz o vídeo.

Es posible resolver los problemas de ancho de banda con algunos de los siguientes recursos:

- **Incrementar el ancho de banda:** lo cual es efectivo pero costoso, aunque dependiendo del escenario en algunos casos es recomendable.
- **Usar mecanismos de QoS** (*Quality of Service*) de clasificación y marcado, así como mecanismos de encolamiento apropiados. De esta manera se enviarán primero los paquetes más importantes.
- **Usar técnicas de compresión:** compresión a capa 2, compresión de cabeceras TCP, cRTP (*RTP header compression*), etc. Siempre es preferible compresión en hardware en vez de en software, ya que el mecanismo en sí usa muchos recursos de CPU.

### Retraso de extremo a extremo

Hay diferentes tipos de retraso desde origen a destino. El retraso de extremo a extremo es la suma de estos cuatro tipos de retraso:

- **Retraso de procesamiento:** es el tiempo que un dispositivo de capa 3 tarda en mover un paquete desde la interfaz de entrada a la de salida. El tipo de CPU así como la arquitectura de hardware influyen en esto.
- **Retraso de encolamiento:** es el tiempo que un paquete pasa en la cola de salida de una interfaz. Dependerá de lo ocupado que esté el router, del número de paquetes esperando, del tipo de cola y del ancho de banda de la interfaz.
- **Retraso de serialización:** es el tiempo empleado en poner en el medio físico todos los bits de una trama.
- **Retraso de propagación:** es el tiempo que se tarda en transmitir en el medio físico los bits correspondientes a una trama. Depende del tipo de medio físico.

### Variación del retraso

Las fluctuaciones en el retraso reciben el nombre de *jitter*. Se produce cuando los paquetes llegan al destino a velocidades diferentes a las que se emitieron desde el origen.

Para paquetes de VoIP o vídeo es esencial que la aplicación sea capaz de liberarlos en el destino a la misma velocidad y en el mismo orden que fueron emitidos en un principio. Esto lo hace sirviéndose del *buffer*, que es donde se van almacenando a medida que llegan, y de RTP (*Real-Time Transport Protocol*), que sella los paquetes para que sean entregados en orden.

Algunas de las claves para ayudar a reducir el jitter son las siguientes:

- Incrementar el ancho de banda.
- Priorizar los paquetes sensitivos.
- Usar técnicas de compresión de capa 2.
- Usar técnicas de compresión de cabeceras.

### Pérdida de paquetes

La pérdida de paquetes ocurre cuando un router no tiene más espacio libre en el buffer de memoria de la interfaz de salida para almacenar los nuevos paquetes que le llegan, debiendo descartarlos.

TCP reenvía los paquetes descartados, a la vez que reduce el tamaño de ventana. Aplicaciones UDP como TFTP por ejemplo pueden generar más tráfico en la red al tener que retransmitir un archivo completo en caso de pérdida de paquetes. Para llamadas de VoIP la pérdida de paquetes resulta en conversaciones entrecortadas, mientras que para vídeo la imagen parece congelarse. Con los mecanismos de QoS adecuados es posible evitar estas situaciones.

A través del comando `show interface` es posible obtener información cuando existan pérdidas de paquetes o congestión:

- **Output drop:** número de paquetes descartados, debido a que la cola de salida de la interfaz está llena.
- **Input queue drop:** si la CPU está sobrecargada el router podría tener problemas al procesar paquetes entrantes, incrementando este contador.
- **Ignore:** número de tramas ignoradas debido a falta de espacio en el buffer.
- **Overrun:** cuando la CPU está sobrecargada podría no proporcionar espacio en el buffer lo suficientemente rápido, haciendo que se descarten paquetes.
- **Frame error:** incluye las tramas con CRC no válido, las que son más pequeñas que el estándar (*runts*) y las gigantes (*giants*).

```text
Switch# show interfaces gigabitEthernet 9/1
GigabitEthernet9/1 is up, line protocol is up (connected)
Hardware is Gigabit Ethernet Port, address is 84b2.61f3.4d60 (bia 84b2.61f3.4d60)
Description: USUARIOS
MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation ARPA, loopback not set
Keepalive set (10 sec)
Full-duplex, 100Mb/s, link type is auto, media type is 10/100/1000-TX
input flow-control is on, output flow-control is on
Auto-MDIX on (operational: on)
ARP type: ARPA, ARP Timeout 04:00:00
Last input 00:00:14, output never, output hang never
Last clearing of "show interface" counters never
Input queue: 0/2000/0/0 (size/max/drops/flushes); Total output drops: 0
Queueing strategy: fifo
Output queue: 0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 11000 bits/sec, 11 packets/sec
4553059 packets input, 866005355 bytes, 0 no buffer
Received 147281 broadcasts (138296 multicasts)
0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
0 input packets with dribble condition detected
27569591 packets output, 5138649237 bytes, 0 underruns
0 output errors, 0 collisions, 3 interface resets
0 unknown protocol drops
0 babbles, 0 late collision, 0 deferred
0 lost carrier, 0 no carrier
0 output buffer failures, 0 output buffers swapped out
```

Los siguientes métodos pueden utilizarse para reducir o evitar la pérdida de paquetes:

- Incrementar el ancho de banda.
- Incrementar el tamaño del buffer, modificando los valores por defecto.
- Proporcionar un ancho de banda garantizado, usando herramientas de QoS tales como CBWFQ (*Class Based Weighted Fair Queuing*) o LLQ (*Low Latency Queuing*).
- Evitar la congestión, descartando aleatoriamente paquetes antes de que las colas se llenen. Para esto existen métodos como RED (*Random Early Detection*) y WRED (*Weighted Random Early Detection*).

### Comparativa del tipo de tráfico

Una red puede contener tres tipos de tráfico:

**1. Tráfico de voz:**

- Es predecible y constante.
- Es muy sensible a los retrasos y a la pérdida de paquetes y no puede ser retransmitido en caso de pérdida.
- El tráfico de voz debe recibir una prioridad más alta que UDP.
- Puede tolerar una cierta cantidad de latencia, jitter y pérdida, sin que sea perceptible.

**2. Tráfico de vídeo:**

- Tiende a ser impredecible, inconsistente, y por ráfagas.
- Es más sensible a la pérdida de paquetes y tiene un mayor volumen de datos.
- Al igual que el tráfico de voz puede tolerar una cierta cantidad de latencia, jitter y pérdida, sin que sea perceptible.

**3. Tráfico de datos:**

- Las aplicaciones que no tienen tolerancia a la pérdida de paquetes de datos, tales como correo electrónico y páginas web, utilizan TCP para garantizar que, si se pierden paquetes serán reenviados.
- Puede ser constante o por ráfagas.
- Algunas aplicaciones TCP pueden consumir gran parte de la capacidad de la red. FTP consumirá tanto ancho de banda como pueda conseguir cuando se descarga un archivo de gran tamaño, como una película o un juego.
- Es relativamente insensible a pérdidas y retrasos en comparación con el tráfico de voz y vídeo.

El administrador de la red debe tener en cuenta la calidad y la experiencia del usuario, QoE (*Quality of Experience*) y qué tipo de aplicaciones utiliza.

## Administración de la congestión

La congestión ocurre cuando el ritmo con el que llegan los paquetes al router es mayor que el ritmo con el que salen. Esto puede ser causado principalmente cuando la o las interfaces de salida tiene menos capacidad o son más lentas que la interfaz de entrada, como por ejemplo si los paquetes llegan en un enlace de Giga y han de salir por un enlace Ethernet. También podría ocurrir que el tráfico llegase por dos o más interfaces y solamente pudiera salir por una, que tiene menos ancho de banda que las de entrada.

Los dispositivos de red pueden reaccionar de diferentes maneras ante una congestión. Para situaciones en que la congestión sea permanente habría que pensar en un incremento del ancho de banda, pero para situaciones donde la congestión es temporal es posible implementar diferentes técnicas de encolamiento, que se pueden elegir dependiendo del objetivo que se busque.

Si una cola está llena y le llegan nuevos paquetes, se produce un fenómeno conocido como *tail drop* donde los paquetes son descartados directamente. Dicho fenómeno hace que mientras la cola esté llena los paquetes entrantes sean descartados a medida que llegan. Para evitar la caída o el *tail drop* ciertos paquetes que están en la cola se descartan para evitar que todos los nuevos paquetes entrantes sean descartados. La elección de qué paquetes serán descartados dependerá del tipo de cola. Generalmente las interfaces usan un sistema llamado FIFO (*First In, First Out*).

La arquitectura de encolamiento en una interfaz está compuesta por dos componentes: la cola de software y la cola de hardware (TxQ). Si la cola de hardware no se llena, no habrá paquetes en la cola de software. Pero si la cola de hardware estuviera congestionada o llena, entonces los paquetes se almacenarían en la cola de software y serían procesados por el mecanismo de encolamiento que se hubiera implementado (FIFO, PQ, CQ, RR, LLQ, etc.) para posteriormente ser pasados a la cola de hardware, que siempre usa un mecanismo FIFO.

El mecanismo de encolamiento por software normalmente cuenta con un determinado número de colas, cada una perteneciente a una clase de tráfico, donde los paquetes son asignados una vez que llegan a la interfaz. En caso de que la cola esté llena los paquetes son descartados directamente (*tail drop*).

Si no existieran las colas de software todo el tráfico sería encolado a través de la cola de hardware que siempre es FIFO, de manera que ciertas aplicaciones sufrirían más que otras y no habría manera de dar un trato adecuado al tráfico. En caso de configurar la cola de hardware con un valor demasiado grande se obtendría un resultado similar al mencionado anteriormente; mientras que si la cola de hardware es demasiado pequeña se llenará pronto y los nuevos paquetes serán asignados más rápidamente a la cola de software, que dependiendo de su configuración les dará un trato u otro.

Se recomienda no cambiar la configuración de la cola de hardware a no ser que sea necesario; el comando `tx-ring-limit` modifica el modo de configuración de la cola en la interfaz.

El comando `show controllers` muestra el tamaño de la cola de hardware.

```text
Router# show controllers
Interface EOBC0
Hardware is DEC21143
dec21140_ds=0x6107CA20, registers=0x3C018000, ib=0x78A7380
rx ring entries=128, tx ring entries=256, af setup failed=0
rxring=0x78A7480, rxr shadow=0x6107CC0C, rx_head=6, rx_tail=0
txring=0x78A7CC0, txr shadow=0x6107CE38, tx_head=18, tx_tail=18,
tx_count=0
PHY link up
CSR0=0xF8024882, CSR1=0xFFFFFFFF, CSR2=0xFFFFFFFF, CSR3=0x78A7480
CSR4=0x78A7CC0, CSR5=0xF0660000, CSR6=0x320CA002, CSR7=0xF3FFA261
CSR8=0xE0000000, CSR9=0xFFFDC3FF, CSR10=0xFFFFFFFF, CSR11=0x0
CSR12=0xC6, CSR13=0xFFFF0000, CSR14=0xFFFFFFFF, CSR15=0x8FF80000
DEC21143 PCI registers:
bus_no=0, device_no=6
CFID=0x00191011, CFCS=0x02800006, CFRV=0x02000041, CFLT=0x0000FF00
CBIO=0x01124401, CBMA=0x48018000, CFIT=0x28140100, CFDD=0x00000400
MII registers:
Register 0x00: FFFF FFFF FFFF FFFF FFFF FFFF FFFF FFFF
Register 0x08: FFFF FFFF FFFF FFFF FFFF FFFF FFFF FFFF
Register 0x10: FFFF FFFF FFFF FFFF FFFF FFFF FFFF FFFF
Register 0x18: FFFF FFFF FFFF FFFF FFFF FFFF FFFF FFFF
throttled=0, enabled=0, disabled=0
rx_fifo_overflow=0, rx_no_enp=0, rx_discard=0
tx_underrun_err=0, tx_jabber_timeout=0, tx_carrier_loss=0
tx_no_carrier=0, tx_late_collision=0, tx_excess_coll=0
tx_collision_cnt=26, tx_deferred=0, fatal_tx_err=0, tbl_overflow=0
HW addr filter: 0x78D10E0, ISL Disabled
Entry= 0: Addr=0000.0000.0000
Entry= 1: Addr=0000.0000.0000
Entry= 2: Addr=0000.0000.0000
Entry= 3: Addr=0000.0000.0000
Entry= 4: Addr=0000.0000.0000
Entry= 5: Addr=0000.0000.0000
Entry= 6: Addr=0000.0000.0000
Entry= 7: Addr=0000.0000.0000
```

### FIFO

FIFO (*First In First Out*) es el mecanismo con que la cola de hardware siempre procesa los paquetes. La configuración no es compleja, un sólo comando basta para habilitarla, y los paquetes simplemente llegan, se ponen en la cola y esperan a ser enviados; el primero en llegar será el primero en salir. La clase de paquete o la prioridad no importan, simplemente importa quién llega primero.

Esto puede ocasionar un problema debido a que algunas aplicaciones de descarga como FTP pueden saturar el enlace evitando el paso de paquetes de VoIP o dejando pasar solamente algunos, causando que las llamadas suenen entrecortadas o que incluso se caigan.

### WFQ

WFQ (*Weighted Fair Queuing*) es un algoritmo basado en flujos; los paquetes llegan y son categorizados en diferentes tipos de flujos asignados a diferentes colas FIFO. WFQ elimina los problemas de retraso y jitter.

Los flujos pueden ser identificados según a lo siguiente:

- Dirección IP de origen.
- Dirección IP de destino.
- Número de protocolo.
- Campo ToS (*Type of Service*).
- Número de puerto de origen TCP/UDP.
- Número de puerto de destino TCP/UDP.

WFQ realiza las siguientes funciones:

- Divide el tráfico en flujos.
- Proporciona una cantidad de ancho de banda justo a los flujos activos.
- Hace que los flujos con poco volumen de tráfico sean despachados más rápido.
- Proporciona más ancho de banda a los flujos con más prioridad.

WFQ tiene las siguientes ventajas y desventajas:

**Ventajas:**

- La configuración es simple y no hace falta clasificar previamente.
- Se garantiza que todas las colas podrán enviar paquetes.
- Se descartan paquetes en flujos de tráfico agresivos y se agiliza los no agresivos.
- Es un protocolo estándar.

**Desventajas:**

- El sistema de clasificación y la programación de la salida de los paquetes de la cola no puede ser modificada.
- Solamente es soportado en enlaces lentos (hasta 2,048 Mbps).
- No se garantiza prevención del retraso o un ancho de banda mínimo para ningún flujo.
- Podría darse el caso de que múltiples flujos fueran asignados a la misma cola.

### CBWFQ

CBWFQ (*Class Based Weighted Fair Queuing*) permite la definición manual de clases, cada una de las cuales es asignada a su propia cola. Dichas clases se definen mediante el uso de *class maps*. Cada una de las colas tiene definido un mínimo de ancho de banda que puede utilizar, pero como su propio nombre indica, es un mínimo; en caso de haber más ancho de banda libre podría emplearlo.

CBWFQ permite la creación de hasta 64 colas, cada una de las cuales es del tipo FIFO, con un ancho de banda garantizado y un límite máximo de paquetes, que en caso de ser alcanzado produciría un *tail drop*, aunque podría evitarse con métodos avanzados como WRED.

CBWFQ tiene los siguientes beneficios:

- Permite la definición de clases de tráfico mediante el uso de *class maps*.
- Permite la reserva de ancho de banda por cada clase de tráfico basándose en ciertos criterios.
- Proporciona granularidad al permitir definir hasta 64 clases diferentes de flujos de tráfico.

La desventaja de CBWFQ es que no incorpora ningún mecanismo para favorecer el tráfico en tiempo real de aplicaciones como VoIP o vídeo.

### LLQ

Hasta ahora no se ha tratado ningún mecanismo de encolamiento que cubriera las necesidades que tienen las aplicaciones en tiempo real. LLQ (*Low Latency Queuing*) cuenta con una cola de prioridad estricta que se utiliza para aplicaciones en tiempo real que son sensitivas al retraso y al jitter. Esta cola está limitada, impidiendo así que anule a las demás, pero limitando su uso. En caso de que haya congestión LLQ sólo usará el ancho de banda que se le ha asignado, permitiendo así que las demás colas también puedan enviar.

Este sistema es similar a CBWFQ pero difiere en la adición de colas de prioridad estricta con el uso del comando `strict-priority`. Se debe tener en cuenta que son posibles más de una cola de prioridad estricta, siendo dos usadas en muchos casos para VoIP y vídeo.

LLQ ofrece todos los beneficios de CBWFQ y además proporciona una o más colas de prioridad estricta que garantizarán ancho de banda a aplicaciones sensitivas al retraso y al jitter. Dichas colas no evitarán que el resto puedan seguir transmitiendo durante períodos de congestión ya que estarán limitadas.

La configuración es casi idéntica a la de CBWFQ con la variación del parámetro `priority` en vez de `bandwidth`.

## QoS

En una red normal con poca utilización un switch envía los paquetes tan pronto como le llegan, pero si la red está congestionada los paquetes no pueden ser entregados en un tiempo razonable. Tradicionalmente la disponibilidad de la red se incrementa aumentando el ancho de banda de los enlaces o el hardware de los switch. QoS (*Quality of Service*) ofrece técnicas utilizadas en la red para priorizar un tráfico determinado respecto a otros.

QoS se define como la habilidad de la red para proporcionar un mejor o especial servicio a un conjunto de usuarios o aplicaciones en detrimento de otros usuarios o aplicaciones.

Para implementar QoS hay que llevar a cabo tres pasos:

- Identificar tipos de tráfico y sus requerimientos.
- Clasificación del tráfico basándose en los requerimientos identificados.
- Definir las políticas para cada clase.

### Identificación del tráfico y sus requerimientos

Es el punto de partida en cualquier implementación de QoS y conlleva los siguientes apartados:

- **Llevar a cabo una auditoría de red.** Es aconsejable tomar estos datos durante los momentos en que la red esté más ocupada así como durante otros períodos.
- **Determinar la importancia de cada aplicación.** El modelo de negocio determinará la importancia de cada aplicación. Se pueden definir clases de tráfico y los requerimientos para cada clase.
- **Definir niveles de servicio para cada clase de tráfico.** Cada clase identificada previamente ha de tener un nivel de servicio que constará de características como ancho de banda garantizado, retraso, preferencia a la hora de que se descarte, etc.

### Clasificación del tráfico

Es posible clasificar desde unas pocas a cientos de variaciones de tráfico dentro de diferentes clases. Las clases definidas han de ir de acuerdo a las necesidades y objetivos de negocio. Las siguientes clases son el resultado de varios estudios y está demostrado que si no todas, alguna de ellas aparecerá en cualquier red empresarial:

- **Clase de VoIP:** como su propio nombre indica corresponde al tráfico de VoIP.
- **Clase de aplicaciones de misión crítica:** corresponde a aplicaciones de alta importancia.
- **Clase de tráfico de señalización:** pertenece al tráfico de señalización de VoIP, vídeo, etc.
- **Clase de tráfico de aplicaciones de transacción:** son aplicaciones del tipo de bases de datos interactivas, etc.
- **Clase Best-effort:** esta clase engloba el tráfico no estipulado en las anteriores y se le proporciona el ancho de banda que sobre.
- **Clase sin importancia:** corresponde a servicios o aplicaciones que se consideran inferiores a las Best-effort. Podrían ser e-mail personal, aplicaciones P2P, juegos online, etc.

### Definición de políticas para cada clase

Este paso conlleva el completar las siguientes tareas:

- Especificar un ancho de banda máximo.
- Especificar un ancho de banda mínimo garantizado.
- Asignar niveles de prioridad.
- Usar herramientas que sean adecuadas para la congestión, gestionándola, eliminándola, etc.

La tabla siguiente muestra un ejemplo de una política de QoS.

| Clase | Prioridad | Tipo de cola | Ancho de banda Mín/Máx | Herramienta |
| --- | --- | --- | --- | --- |
| Voice | 5 | Prioridad | 1 Mbps Mín / 1 Mbps Máx | Prioridad de cola |
| Business mission critical | 4 | CBWFQ | 1 Mbps Mín | CBWFQ |
| Signaling | 3 | CBWFQ | 400 Kbps Mín | CBWFQ |
| Transactional | 2 | CBWFQ | 1 Mbps Mín | CBWFQ |
| Best-effort | 1 | CBWFQ | 500 Kbps Máx | CBWFQ / CB-Policing |
| Scavenger | 0 | CBWFQ | Máx 100 Kbps | CBWFQ / CB-Policing / WRED |

## Modelos de QoS

### Best-effort

Este modelo significa que no hay QoS aplicado, de manera que todos los paquetes dentro de la red independientemente del tipo que sean reciben el mismo trato. Como beneficio de este sistema está la facilidad de implementación, ya que no hay que hacer nada para ponerlo en funcionamiento, pero tiene como desventaja que no es posible garantizar ningún tipo de servicio a ninguna aplicación.

### IntServ

Se trata del primer modelo que proporcionó QoS de extremo a extremo, basado en la señalización explícita y reserva de recursos de red para aquellas aplicaciones que los necesitan. El protocolo usado para la señalización es el RSVP (*Resource Reservation Protocol*).

Cuando una aplicación tiene un requerimiento de ancho de banda, RSVP va salto por salto a lo largo del camino intentando hacer la reserva solicitada en cada uno de los routers que se encuentra en la ruta. Si la reserva se puede hacer la aplicación podrá operar; pero si algún elemento en el camino no tiene los recursos suficientes la aplicación tendrá que esperar.

Para implementar Servicios Integrados de manera satisfactoria, además de RSVP debería habilitarse lo siguiente:

- **Control de Admisión:** en caso de que los recursos no puedan proporcionarse sin afectar a las aplicaciones actualmente en uso se deberían denegar.
- **Clasificación:** el tráfico perteneciente a una aplicación que ha solicitado una reserva se debería clasificar y ser reconocido por los routers en el camino.
- **Políticas:** es necesario tomar acciones cuando las aplicaciones excedan la utilización de los recursos acordados.
- **Encolamiento:** es importante que los dispositivos puedan almacenar los paquetes mientras se envían los que estaban primero.
- **Programación:** funciona junto con el encolamiento y hace referencia al caso en el que existan varias colas y qué cantidad de datos podrían transmitir cada una en cada ciclo.

Los beneficios de Servicios Integrados son el control de admisión de recursos de extremo a extremo, políticas de control de admisión por petición y señalización de números de puerto dinámicos. Como desventajas mencionar que cada flujo activo necesita señalización continua, usando así recursos extra y haciendo que no sea un modelo altamente escalable.

### DiffServ

Este modelo es el más actual de los tres y ha sido desarrollado para suplir las deficiencias de sus predecesores. Está explicado detalladamente en las RFC 2474 y 2475. Servicios diferenciados usa PHB (*Per-Hop Behavior*), que hace referencia al comportamiento por salto. Esto significa que cada salto en el camino está programado para proporcionar un nivel de servicio específico a cada clase de tráfico.

Con este modelo, el tráfico es en principio clasificado y marcado. A medida que fluye en la red va recibiendo distinto trato dependiendo de su marca.

En los servicios diferenciados hay que tener en cuenta que:

- El tráfico es clasificado.
- Las políticas de QoS son aplicadas dependiendo de la clase.
- Se debe elegir el nivel de servicio para cada tipo de clase que corresponderá a unas necesidades determinadas.

Como ventajas principales mencionar la escalabilidad y habilidad para soportar muchos tipos de niveles de servicio. Como puntos negativos, el servicio no es absolutamente garantizado y es más complejo de implementar.

## Clasificación y marcado de tráfico

Clasificar es el proceso de identificar y categorizar tipos de tráfico en clases. La categorización se ha hecho tradicionalmente basándose en ACL, pero además es posible utilizar descriptores de tráfico como:

- Interfaz de entrada.
- Valor del CoS (*Class of Service*).
- Dirección IP de origen o destino.
- Valor de IP Precedence o DSCP en la cabecera IP.
- Valor EXP en la cabecera MPLS.
- Tipo de aplicación.

Siempre se debe intentar clasificar y marcar el tráfico tan cerca del origen como sea posible, siendo la capa de acceso de la red el lugar ideal. Marcar es el proceso de etiquetar tráfico basándose en su categoría. Los campos usados para el marcado dependen de si es en capa 2 (CoS, EXP, DE, CLP) o capa 3 (IP Precedence, DSCP).

### Marcado en capa 2

802.1q es un modelo de enlace troncal de capa 2 estandarizado definido por la IEEE. Dentro de la cabecera existe un campo de 3 bits llamado PRI (*Priority*) o CoS (*Class of Service*) 802.1p, utilizado para propósitos de QoS y que puede tener 8 posibles valores.

La siguiente tabla describe los valores de los bits CoS 802.1p dentro de la cabecera:

| CoS (bits) | CoS (Decimal) | IETF RFC791 | Aplicación |
| --- | --- | --- | --- |
| 000 | 0 | Routine | Datos |
| 001 | 1 | Priority | Datos de media prioridad |
| 010 | 2 | Immediate | Datos de alta prioridad |
| 011 | 3 | Flash | Señal de llamada |
| 100 | 4 | Flash-Override | Videoconferencia |
| 101 | 5 | Critical | Voz |
| 110 | 6 | Internet | Reservado (inter-network control) |
| 111 | 7 | Network | Reservado (network control) |

La siguiente figura muestra la cabecera de 4 bytes 802.1q.

### Marcado de capa 3

IPv4 e IPv6 especifican un campo de 8 bits en sus cabeceras para marcar paquetes. Este campo recibe el nombre de:

- **IPv4:** Tipo de servicio
- **IPv6:** Clase de tráfico

Se utilizan los 3 bits más significativos (más a la izquierda) del campo ToS (*Type of Service*), los cuales reciben el nombre de IP Precedence, y dan un total de 8 posibles combinaciones; cuanto más alto el número, mayor prioridad.

La siguiente figura muestra una cabecera IP y detalla el campo ToS mostrando los posibles valores de IP Precedence.

Los valores 6 y 7 de la tabla anterior son usados por diferentes protocolos en su tráfico de gestión y no está permitido que se configuren para aplicaciones.

La redefinición del byte ToS dio lugar al campo DiffServ, usando los 6 bits más significativos (más a la izquierda), lo que aumenta la flexibilidad y las opciones. Los 2 bits menos significativos son llamados ECN (*Explicit Congestion Notification*) y se usan para control del flujo. DSCP (*Differentiated Services Code Point*) es compatible con IP Precedence, lo que hace que la migración sea más fácil.

En la terminología Diffserv, el comportamiento de reenvío asignado a un DSCP se denomina PHB (*Per-hop Behavior*). El PHB define la precedencia de reenvío que un paquete marcado en relación con otro tráfico del sistema con Diffserv. Esta precedencia determina si el sistema con IP QoS o Diffserv reenvía o descarta dicho paquete. Para un paquete reenviado, cada enrutador Diffserv que el paquete encuentra en la ruta hasta su destino aplica el mismo PHB. La excepción ocurre si otro sistema Diffserv cambia el DSCP.

Existen cuatro tipos de PHB con los valores del DSCP:

- **Call Selector:** poniendo a cero los 3 bits menos significativos del DSCP `xxx000`, se obtiene compatibilidad con IP Precedence.
- **Por defecto:** con los 3 bits más significativos del IP Precedence/DSCP `000xxx`, se obtiene un resultado de Best-effort.
- **Assured Forwarding (AF):** con los 3 bits más significativos del DSCP puestos a `001xxx`, `010xxx`, `011xxx` o `100xxx` (AF1, AF2, AF3, AF4) se usa para garantizar ancho de banda.
- **Expedite Forwarding (EF):** con los 3 bits más significativos del DSCP puestos a `101xxx` (el campo DSCP sería 101110 equivalente a 46 en decimal) se usa para proporcionar un servicio de bajo retardo.

## Fronteras de confianza

Los dispositivos finales como pueden ser PC, teléfonos IP, switches y routers localizados en diferentes niveles de la jerarquía de la red podrían marcar los paquetes IP o las tramas 802.1Q/P. Una medida importante en el diseño es decidir dónde localizar las fronteras de confianza. Dichas fronteras formarán un perímetro, dentro del cual los diferentes dispositivos respetarán y confiarán en las marcas de QoS realizadas dentro de ese perímetro. Las marcas hechas por dispositivos fuera de ese perímetro son eliminadas o chequeadas.

A la hora de decidir dónde colocar la frontera de confianza hay que tener en cuenta que los dispositivos confiables deberían estar dentro de nuestro control administrativo y que dependiendo del dispositivo tendrá capacidad para realizar unas tareas u otras. Con esto en consideración la frontera de confianza puede ser implementada en una de las siguientes capas:

- Sistema final.
- Capa de Acceso.
- Capa de Distribución.

## WRED

Las herramientas para evitar la congestión del tráfico de red son simples. Siguen de cerca las cargas de tráfico en un esfuerzo para anticipar y evitar la congestión en la red y los cuellos de botella antes de que se conviertan en un problema.

Estas técnicas proporcionan un tratamiento preferencial cuando hay congestión para el tráfico premium (según su prioridad), mientras que al mismo tiempo maximizan el rendimiento y la capacidad de la red al reducir al mínimo la pérdida de paquetes y el retardo.

El algoritmo WRED (*Weighted Random Early Detection*) permite evitar la congestión en interfaces de red, proporcionando gestión de memoria intermedia y permitiendo disminuir o desacelerar el tráfico TCP, antes de que se agoten los buffers de memoria.

WRED es un mecanismo que previene el *tail drop* descartando paquetes de manera aleatoria antes de que éste se produzca, con la capacidad añadida de poder decidir qué tráfico descartar en caso de que fuera necesario. La cantidad de paquetes que son descartados crece a medida que va creciendo el tamaño de la cola de la interfaz.

Con WRED es posible configurar diferentes perfiles (umbral mínimo, máximo y MPD) para dar más prioridad a unos flujos de tráfico que a otros. La prioridad se basa en los valores IP Precedence o DSCP.

WRED considera el tráfico RSVP sensitivo a los descartes, de manera que el tráfico que no sea RSVP es descartado primero. Por otra parte, los flujos de tráfico no IP son considerados menos importantes que los IP y se empiezan a descartar antes.

!!! note "NOTA"

    WRED no debe aplicarse a colas de tráfico VoIP, ya que dicho tráfico es extremadamente sensitivo a los descartes de paquetes y daría lugar a conversaciones entrecortadas, además de tratarse de tráfico UDP.

## Acuerdos de nivel de servicio

Un SLA (*Service Level Agreements*) es un acuerdo contractual entre dos partes, normalmente identificados como la empresa y el proveedor de servicios. Dichos servicios pueden ser líneas dedicadas punto a punto, acceso a Internet, etc. Es recomendable monitorizar dicho SLA para que ambas partes cumplan con lo acordado.

Los parámetros que se suelen negociar en relación a QoS son:

- Retraso.
- Jitter.
- Pérdida de paquetes.
- Rendimiento.
- Disponibilidad del servicio.

El desarrollo de la telefonía IP y aplicaciones interactivas han hecho que cada vez sean más importantes los SLA relativos a QoS.

Tradicionalmente las empresas han usado Circuitos Virtuales (VC) ya sean permanentes o temporales (PVC o SVC) para proporcionar conectividad entre sitios remotos. En este tipo de servicios no es posible negociar un SLA relativo a QoS, ya que el servicio que se presta es de capa 1 y 2.

El SLA se centra en parámetros como velocidad media de transferencia (CIR), ráfaga de tráfico alcanzable transmitiendo a la velocidad media (Bc, *committed burst*), ráfaga en exceso (Be, *excess burst*) y velocidad máxima de transferencia. Cuando los enlaces WAN se congestionan hay que aplicar técnicas de QoS tales como *traffic shaping*, compresión de cabeceras, LLQ, etc.

Actualmente hay muchos proveedores que ofrecen servicios de capa 3 mediante el uso de MPLS VPN, lo que proporciona muchas más ventajas que los servicios de capa 1 o 2 tradicionales. Escalabilidad, facilidad de provisión y flexibilidad del servicio son sinónimos de las MPLS VPN. Al trabajar en capa 3 se pueden, ahora sí, establecer SLA relativos a QoS.

## Control y manipulación del tráfico

Existen dos mecanismos para amoldar el tráfico a las necesidades de la red. Ambos miden la cantidad de tráfico y lo comparan con una política o un acuerdo de nivel de servicio (SLA). SLA es utilizado normalmente por las empresas o ISP en lo que respecta al manejo de ancho de banda, tráfico, disponibilidad, fiabilidad, etc. Cuando dicho SLA se sobrepasa y hay un exceso en el tráfico enviado, se pueden utilizar métodos para su regulación:

- **Shaping:** utiliza buffers para retardar el envío de dicho tráfico. Es aplicado en dirección de salida.
- **Policing:** descarta ese tráfico o en algunos casos lo remarca. Puede aplicarse tanto en salida como en entrada.

La utilización de *shaping* es recomendable en los siguientes casos:

- **Para frenar la velocidad a la que el tráfico es enviado a través de una red WAN.** En caso de que el sitio remoto o la red del proveedor tengan problemas de congestión, el dispositivo que envía puede ser notificado, usando por ejemplo BECN en Frame-Relay, almacenando tráfico y bajando la cantidad enviada hasta que las condiciones de la red mejoren. Dos casos comunes son cuando un sitio remoto tiene una conexión al proveedor a menor velocidad que la del sitio que envía, y cuando al sitio remoto le están llegando datos de múltiples sitios, saturando así su conexión.
- **Para cumplir con la velocidad de suscripción.** Dependiendo del SLA que exista con el proveedor habrá que aplicar *shaping* para los enlaces WAN o MetroEthernet.
- **Para enviar diferentes clases de tráfico a diferentes velocidades.** Si en el SLA se especifica una velocidad máxima para una clase de tráfico en particular, el dispositivo que envía tendrá que aplicar *shaping* basado en clase.

La utilización de *policing* es recomendable en los siguientes casos:

- **Para limitar la velocidad a un valor menor que la velocidad del medio o interfaz física.** Suele darse el caso cuando un proveedor ofrece un servicio de acceso a su red a través de una interfaz que puede proporcionar una velocidad mayor a la del SLA acordado.
- **Para limitar la velocidad del tráfico en cada clase.** Esto ocurre cuando el SLA pactado incluye diferentes velocidades por clase de tráfico.
- **Para remarcar tráfico.** Normalmente se remarca el tráfico si excede el SLA para que, posteriormente, otros dispositivos puedan tomar alguna acción.

## Fundamentos para el examen

- Recuerde los fundamentos para una correcta convergencia de una red.
- Estudie todas las posibilidades para garantizar el mayor ancho de banda posible.
- Recuerde la importancia del jitter.
- Diferencie los tipos de tráfico y compárelos.
- Respecto a la congestión recuerde cuáles pueden ser los mecanismos para evitarla.
- Identifique y estudie los diferentes tipos de tráfico.
- Estudie los modelos de QoS.
- Recuerde términos como SLA, WRED, CoS, CBWFQ, FIFO.
