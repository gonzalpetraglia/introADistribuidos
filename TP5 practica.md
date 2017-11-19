Practica
--------

#Ejercicio 1

##Configuraciones

###r1
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

#r2

```
conf t
int atm2/0
no shu
int atm2/0.25 point-to-point
ip address 192.168.25.2 255.255.255.0
pvc 0/201
encapsulation aal5snap 
```

#r3


```
conf t
int atm2/0
no shu
int atm2/0.25 point-to-point
ip address 192.168.25.3 255.255.255.0
pvc 0/301
encapsulation aal5snap 

```


