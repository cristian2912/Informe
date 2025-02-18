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
     
  5.Creamos un bucle para que se manden paquetes ICMP cada segundo y asi poder medir el tiempo de respuesta entre cada paquete, asi mismo vemos si hay paquetes perdidos, el codigo para hacer esto es el siguiente:
  ```
     ping -i 1 192.168.0.2 | tee traza.txt & sleep 30m; kill $!
  ```
   - Este codigo esta hecho de esa forma para que se envien paquetes 1 segundo entre cada uno, aparte de eso muestra la salida en tiempo real en traza.txt y por ultimo detiene el bucle pasados los 30mn
 
     
