# INFORME

*Trabajo prensentado por:*

*Ayala Daniel*

*Bello Cristian*

*Chaves Samuel*

*Guevara Kevin* 


# Conexion guiada mediante el ping 192.168.0.2 > Traza.txt y wifi 802.11ac

- Pasos que seguimos para la implementación:
  
  1. Conectamos los pc por medio del cable LAN (ethernet)
     
  2. Conectamos las 2 pc a la misma red wifi (IEEE 802.11ac)
     
  3. Nos aseguramos que ambos pc tengan la dirección IP en el mismo rango que en este caso es (192.168.0.2)
     
  4. Desde mi pc se crea el ping para la otra pc, eso lo hicimos mediante el codigo:
  ```
      ping 192.168.0.2 > traza.txt
  ```
   - Este codigo envia paquetes ICMP (protocolo de mensajes de control de internet) a la dirección IP 192.168.0.2 y guarda la salida en un archivo llamado traza.txt. Los paquetes ICMP son para verificar si un 
     host esta activo y medir el tiempo de ida y vuelta (RTT, Round-Trip Time).
     
  5. Creamos un bucle para que se manden paquetes ICMP cada segundo y asi poder medir el tiempo de respuesta entre cada paquete, asi mismo vemos si hay paquetes perdidos, el codigo para hacer esto es el siguiente:
  ```
     ping -i 1 192.168.0.2 | tee traza.txt & sleep 30m; kill $!
  ```
   - Este codigo esta hecho de esa forma para que se envien paquetes 1 segundo entre cada uno, aparte de eso muestra la salida en tiempo real en traza.txt y por ultimo detiene el bucle pasados los 30mn
 
  6. Ahora mandamos el archivo traza.txt a la otra pc, esto lo hacemos de la siguiente manera:
  ```
     scp traza.txt samuel@192.168.0.2:/home/samuel/Conexion/    
  ```
  7. Por ultimo vemos la informacion en el otro pc, la cual se veria algo asi:
```
   PING 192.168.0.2 (192.168.0.2) 56(84) bytes of data.
   64 bytes from 192.168.0.2: icmp_seq=1 ttl=64 time=1.23 ms
   64 bytes from 192.168.0.2: icmp_seq=2 ttl=64 time=1.45 ms
   64 bytes from 192.168.0.2: icmp_seq=3 ttl=64 time=1.12 ms
   64 bytes from 192.168.0.2: icmp_seq=4 ttl=64 time=1.67 ms
   64 bytes from 192.168.0.2: icmp_seq=5 ttl=64 time=1.09 ms
   Request timeout for icmp_seq 6
   64 bytes from 192.168.0.2: icmp_seq=7 ttl=64 time=1.34 ms
   64 bytes from 192.168.0.2: icmp_seq=8 ttl=64 time=1.56 ms
   64 bytes from 192.168.0.2: icmp_seq=9 ttl=64 time=1.22 ms
   64 bytes from 192.168.0.2: icmp_seq=10 ttl=64 time=1.45 ms
   64 bytes from 192.168.0.2: icmp_seq=11 ttl=64 time=1.33 ms
   64 bytes from 192.168.0.2: icmp_seq=12 ttl=64 time=1.28 ms
   64 bytes from 192.168.0.2: icmp_seq=13 ttl=64 time=1.41 ms
   64 bytes from 192.168.0.2: icmp_seq=14 ttl=64 time=1.19 ms
   64 bytes from 192.168.0.2: icmp_seq=15 ttl=64 time=1.37 ms
   Request timeout for icmp_seq 16
   64 bytes from 192.168.0.2: icmp_seq=17 ttl=64 time=1.25 ms
   64 bytes from 192.168.0.2: icmp_seq=18 ttl=64 time=1.48 ms
   64 bytes from 192.168.0.2: icmp_seq=19 ttl=64 time=1.31 ms
   64 bytes from 192.168.0.2: icmp_seq=20 ttl=64 time=1.22 ms
   ...
   64 bytes from 192.168.0.2: icmp_seq=1798 ttl=64 time=1.33 ms
   64 bytes from 192.168.0.2: icmp_seq=1799 ttl=64 time=1.28 ms
   64 bytes from 192.168.0.2: icmp_seq=1800 ttl=64 time=1.41 ms

   --- 192.168.0.2 ping statistics ---
   1800 packets transmitted, 1795 received, 0.27% packet loss, time 1800000ms
   rtt min/avg/max/mdev = 1.09/1.34/2.45/0.12 ms
```










  
