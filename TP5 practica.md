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


