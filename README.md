# tunnelssh
Con la ayuda de este repo puedes crear un servicio en systemd que mantiene en ejecucion permanente un tunel reverso ssh.

Se puede utilizar cuando quieres tener acceso ssh a un equipo que esta dentro de una red que no te permite redireccionar puertos a tu ip local dentro de esa red.

El equipo al que quieres tener acceso se conecta a un servidor remoto, y atiende peticiones hechas al servidor remoto como si fuesen peticiones hechas a el mismo.


#### EJEMPLO REVERSE SSH TUNNEL



En el archivo **tunnel.service** se deben cambiar lo siguiente:

* La ruta absoluta donde se encuentra la llave que se utiliza para autenticarse en el servidor remoto:

  **/home/your_linux_user/path_to_key/key_server.pem**

* El nombre del usuario en el servidor remoto a acceder:

  **ubuntu**

* El nombre del usuario local de linux:

  **your_linux_user**
  
* Puerto local y puerto del servidor:

  **8080:localhost:22**
  
  Donde 8080 es un puerto que tiene que estar abierto en el servidor remoto y localhost:22 es el puerto del servicio ssh.
  (Se puede configurar un puerto distinto al 22 en el archivo de configuracion del servicio ssh, esto ayuda con algunos firewall)
  
 El archivo **tunnel.service** se debe poner en la ruta: **/etc/systemd/system**
 
 Se debe configurar **GatewayPorts yes** en el servicio ssh del servidor remoto
 
 Luego ejecutar **sudo systemctl enable tunnel.service** para habilitar el servicio
 
 Para iniciar, parar y mostrar estatus se puede ejecutar:
 
 **systemctl start tunnel.service**
 
 **systemctl stop tunnel.service**
 
 **systemctl status tunnel.service**
 
