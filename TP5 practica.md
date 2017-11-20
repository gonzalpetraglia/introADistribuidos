Practica
--------

# Ejercicio 1

## Configuraciones

### r1
```
conf t
int atm2/0
no shu
int atm2/0.25 multipoint
ip address 192.168.25.1 255.255.255.0
pvc 0/102
encapsulation aal5snap
protocol ip 192.168.25.2 broadcast
pvc 0/103
encapsulation aal5snap
protocol ip 192.168.25.3 broadcast
```

### r2

```
conf t
int atm2/0
no shu
int atm2/0.25 point-to-point
ip address 192.168.25.2 255.255.255.0
pvc 0/201
encapsulation aal5snap 
```

### r3


```
conf t
int atm2/0
no shu
int atm2/0.25 point-to-point
ip address 192.168.25.3 255.255.255.0
pvc 0/301
encapsulation aal5snap 

```

## Respuestas 

1. Ambos pings tuvieron respuesta.
2. 
  Para el caso del traceroute a R1, solo se ve la IP de R1, lo cual se explica porque R3 y R1 estan conectados directamente a la vista de IP, ya que ATM pertenece a capas inferiores.
  Por otro lado, cuando ejecutamos un traceroute a R2 aparece primero R1 y luego R2, esto se da porque las rutas de ATM que tenemos configuradas son R1-R2 y R1-R3, por lo que si bien a nivel fisico la conexion de R3 con R2 es la misma que R3 con R1, necesitaremos pasar por R1 para conectar a R2 con R3.
  
3.
4. 
### Configuración r4


```
conf t
int atm2/0
no shu
int atm2/0.25 point-to-point
ip address 192.168.25.4 255.255.255.0
pvc 0/403
encapsulation aal5snap 

```
5. 

La configuración utilizada en R3 fue:
```
conf t
int atm2/0
no shu
int atm2/0.25 multipoint
ip address 192.168.25.3 255.255.255.0
pvc 0/301
encapsulation aal5snap
protocol ip 192.168.25.1 broadcast
pvc 0/301
encapsulation aal5snap
protocol ip 192.168.25.2 broadcast
pvc 0/304
encapsulation aal5snap
protocol ip 192.168.25.4 broadcast
```

6. 
  Los pings realizados desde R3 dan todos resultados positivos. Por otro lado, si los pings se realizan desde R4 el unico con resultado positivos es a R3, puesto que si bien la ruta de R4 a cualquier router esta configurada, desde R1 y R2 no se puede llegar a R4, dando como resultado que los pings a R1 y R2 no tengan respuesta. Para que esto no suceda deberiamos agregar los siguientes comandos a la configuracion  de R1:

```
pvc 0/103
encapsulation aal5snap
protocol ip 192.168.25.4 broadcast
```

  Una vez agregado la configuración anterior, todos los traceroute ejecutados en R4 llegan satisfactoriamente a cada uno de los routers destinos, mostrando cada uno de  los nodos intermedios. 
  Para el caso de R3 se ve solo R3.
  Para el caso de R1 se ve R3 y R1.
  Para el caso de R2 se ve R3, R1 y R4.

# Ejercicio  2

  1. En los routers P se pueden ver las siguientes configuraciones adicionales:
  * El rango de labels mediante el comando *mpls label range n m*
  * La definicion de que cada una de las interfaces es apta para utilizar MPL mediante la sentencia *mpls ip* en cada una de ellas.
  
  
  2. En los routers PE se puede ver las siguientes configuraciones adicionales:
  * El rango de labels mediante el comando *mpls label range n m*
  * La declaracion de que el TTL no sea transmitido fuera de la red que admite MPLS  mediante el comando *no mpls ip propagate-ttl*
  * En las interfaces internas se define esto con la sentencia *mpls ip*
  
  3. MPLS utiliza un sistema de circuitos virtuales donde cada paquete al entrar a la red, si es posible, se le agrega un header de MPLS(entre el header de IP y el de Ethernet, si estos fueran los protocolos usados) y luego hasta que el paquete egresa de esta se utiliza dicho header para routear al paquete. La informacion de como routear estos labels se hace mediante LDP (o TDP para Cisco).
  5. LDP utiliza 646. Sin embargo, el equivalente de Cisco, TDP, utiliza el puerto 711, por lo que este es el que se puede observar mediante el mencionado comando.
  7. No hay rutas a las redes externas a la Service Provider Network, es decir por fuera del dominio de MPLS.
  8. 
  9.
  
