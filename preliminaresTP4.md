Practica 1
----------
Bloqueo: En este estado se pueden recibir BPDU's pero no las enviará. Las tramas de datos se descartan y no se actualizan las tablas de direcciones MAC (mac-address-table). Los switch comienzan en este estado ya que si realizan envíos (forwarding) podrían estar generando un loop o bucle.
Escucha: A este estado se llega desde Bloqueo. En este estado, los switches determinan si existe alguna otra ruta hacia el puente raíz. En el caso que la nueva ruta tenga un coste mayor, se vuelve al estado de Bloqueo. Las tramas de datos se descartan y no se actualiza la tabla de direcciones MAC (mac-address-table). Se procesan las BPDU.
Aprendizaje: A este estado se llega desde Escucha. Las tramas de datos se descartan pero ya se actualizan las tablas de direcciones MAC (aquí es donde se aprenden por primera vez). Se procesan las BPDU.
Envío: A este estado se llega desde Aprendizaje, en este estado el puerto puede enviar y recibir datos. Las tramas de datos se envían y se actualizan las tablas de direcciones MAC (mac-address-table). Se procesan las BPDU.
Desactivado: A este estado se llega desde cualquier otro. Se produce cuando un administrador deshabilita el puerto o éste falla. No se procesan las BPDU.

3. Ejercicio
a) El Bridge ID esta formado por ......la prioridad del bridge.... y .....la MAC Address del Bridge, concatenados en ese orden.......
b) Si un puerto que es root port deja de recibir BPDUs, despu´es de un tiempo pasar´a al
estado ...blocking......
c) Cuando un puerto pasa al estado Learning ya puede aprender ....las rutas hacia las direcciones MAC.... de 
los frames que recibe.
d) Un switch recibe BPDUs a traves de dos puertos distintos, contieniendo el mismo Bridge
ID. Entonces, el puerto con menor ...Port Id... se convertira en el ....Root Port.....
e) Cada segmento de red debe tener un ´unico ...Designated port....



a) Verdadero, ya que son los unicos puertos habilitados, ademas del root port obviamente.
b) Falso, debe enviarlo a traves del root port y de los demas designated ports.
c) Falso, si el frame esta destinado a un host en otro segmento que tenga como designated port a un puerto de ese mismo bridge, este debera fordwardearla a traves de dicho puerto-
