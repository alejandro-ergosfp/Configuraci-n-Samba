# Configuracion-Samba
En este repositorio se mostraran los pasos para crear un recurso samba y compartirlo con una maquina Debian

## 1 Instalación de Samba

```
# Actualizamos los paquetes
apt update

# Instalamos el paquete que contiene el servicio samba
sudo apt -y install samba

#Verificamos que el servicio este correcto
sudo systemctl status smbd.service
```

## 2 Configurando Samba
- Una vez instalado el servidor Samba, es hora de configurarlo. El archivo de configuración de samba es smb.conf y se encuentra en el directorio /etc/samba. En este archivo, especificamos la carpeta y las impresoras que queremos compartir junto con sus permisos y parámetros.

- Abrimos el archivo de configuración
```
sudo nano /etc/samba/smb.conf
```
- Nos vamos al final del archivo y creamos la siguiente configuración
```
[Nombre_Recurso]
comment = Comentario sobre el recurso
path = /home/usuario/carpeta_compartida
read-only = no
browsable = yes
```

[![Image from Gyazo](https://i.gyazo.com/d26e00ad81f43ca978da81f7365fdddc.png)](https://gyazo.com/d26e00ad81f43ca978da81f7365fdddc)

- Definición de los recursos que acabamos de configurar
```
[Nombre_Recurso] = nombre del recurso compartido de samba
comment = breve descripción de la acción
path= Ruta del directorio compartido.
read-only = Establecer directorio compartido como lectura
browsable = para incluir el recurso compartido en la lista de recursos compartidos o no.
```

## 3 Configuración de la cuenta de usuario
- Ahora necesitaremos la cuenta de usuario de configuración para samba. El usuario de Samba debe ser el usuario del sistema y, por lo tanto, debe existir en el archivo /etc/passwd. En mi caso el usuario es "domin"
```
# Utilizando el comando tail /etc/passwd podemos ver el nombre de nuestro usuario
tail /etc/passwd
```
[![Image from Gyazo](https://i.gyazo.com/0447fb80bb347ec752bd5f1a5eb9b9a8.png)](https://gyazo.com/0447fb80bb347ec752bd5f1a5eb9b9a8)
```
# Con el siguiente comando vamos a crear el usuario "domin" en el servicio samba
sudo smbpasswd -a domin (Nombre del usuario para acceder al curso)
```

[![Image from Gyazo](https://i.gyazo.com/64e09de3dc0ebe0a58d4662f600d823c.png)](https://gyazo.com/64e09de3dc0ebe0a58d4662f600d823c)

## 4 Reiniciar el servicio Samba

- Una vez que hayamos terminado con todas las configuraciones y la configuración del usuario, reiniciamos el servicio Samba ejecutando el siguiente comando
```
sudo systemctl restart smbd
```

## 5 Usando la línea de comando
- Para conectar el recurso compartido de samba desde la línea de comandos de Linux, deberá instalar el cliente de Samba. Ayudará a conectar los recursos compartidos de samba desde la línea de comandos.

```
sudo apt install smbclient
````

- Para poder acceder al recurso deberemos entrar en Lugares -> Otras Ubicaciones
- Escribimos la siguiente ruta **smb://dirección_ip/Nombre_del_recurso**

[![Image from Gyazo](https://i.gyazo.com/c2c47bc60c7a8b724275ce218add204d.png)](https://gyazo.com/c2c47bc60c7a8b724275ce218add204d)

- Luego escribimos el usuario que configuramos anteriormente y su contraseña asociada


