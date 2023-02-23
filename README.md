# Configuracion-Samba
En este repositorio se mostraran los pasos para crear un recurso samba y compartirlo con una maquina Debian

# 1- Instalación de Samba

```
sudo apt -y install samba
Verificamos que el servicio este correcto

sudo systemctl status smbd.service
```

2- Configurando Samba
Una vez instalado el servidor Samba, es hora de configurarlo. El archivo de configuración de samba es smb.conf y se encuentra en el directorio /etc/samba. En este archivo, especificamos la carpeta y las impresoras que queremos compartir junto con sus permisos y parámetros. Pero antes de hacer nada te recomiendo un backup del archivo

sudo cp /etc/samba/smb.conf ~/Documentos/smb.conf_backup
Ahora si lo editamos

sudo nano /etc/samba/smb.conf
Vamos a agregar al final del archivo lo siguiente

[samba-share]
comment = Samba en Debian
path = /samba
read-only = no
browsable = yes
Explicación

[samba-share] = nombre del recurso compartido de samba
comment = breve descripción de la acción
path= Ruta del directorio compartido.
read-only = Establecer directorio compartido como lectura
browsable = para incluir el recurso compartido en la lista de recursos compartidos o no.

## Step-02: PODs Demo
### Get Worker Nodes Status
- Verify if kubernetes worker nodes are ready. 
```
# Get Worker Node Status
kubectl get nodes

# Get Worker Node Status with wide option
kubectl get nodes -o wide
```

### Create a Pod
- Create a Pod
```
# Template
kubectl run <desired-pod-name> --image <Container-Image> --generator=run-pod/v1

# Replace Pod Name, Container Image
kubectl run my-first-pod --image stacksimplify/kubenginx:1.0.0 --generator=run-pod/v1
```
- **Important Note:** Without **--generator=run-pod/v1** it will create a pod with a deployment which is another core kubernetes concept which we will learn in next few minutes. 
- **Important Note:**
  - With **Kubernetes 1.18 version**, there is lot clean-up to **kubectl run** command.
  - The below will suffice to create a Pod as a pod without creating deployment. We dont need to add **--generator=run-pod/v1**
```
kubectl run my-first-pod --image stacksimplify/kubenginx:1.0.0
```  
