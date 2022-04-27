# Intancia WEBHOOK
Esta instancia es la encargada de recibir los mensajes de las redes sociales y enviarlos directamente al motor del bot, sus principales caracteristicas para que funcione son las siguiente:  
* **Detalles basicos**
* **Seguridad**
* **Conexion**  
## Detalles básicos
Son las configuraciones minimas requeridas
### Plataforma
Ubuntu (inferido)
### Detalles de la plataforma
Linux/UNIX
### Tipo de instancia
t2.micro
## Seguridad
Para la seguridad es necesario crear un grupo de seguridad con las siguientes caracteristicas:  
### Reglas de entrada

| Intervalo de puertos | Protocolo | Origen |
| --- | --- | --- |
| 22  | TCP | 0.0.0.0/0 |
| Todo | Todo | 0.0.0.0/0 |

### Reglas de salida

| Intervalo de puertos | Protocolo | Origen |
| --- | --- | --- |
| Todo | Todo | 0.0.0.0/0 |

## Conexion
Finalmente para la parte de la conexión la debemos de hacer mediante SSH con las siguientes instrucciones:  
### ID de la instancia  
i-xxxxxxxxxx (Name)
### Abra un cliente SSH.  
Localice el archivo de clave privada. La clave utilizada para lanzar esta instancia es name.pem
Ejecute este comando, si es necesario, para garantizar que la clave no se pueda ver públicamente.
#### linux 
```bash
chmod 400 name.pem
``` 
#### windows
```powershell
icacls .\name.pem /inheritance:r
icacls .\name.pem /grant:r "%username%":"(R)"
```
Conéctese a la instancia mediante su DNS público:
```ec2-xx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com```  
Ejemplo:
```bash
ssh -i "name.pem" ubuntu@ec2-xx-xxx-xxx-xxx.us-west-2.compute.amazonaws.com
```
#### Manejo de ventanas en consola
Para poder tener administrada las ejecuciones de los servidores Flask, los siguientes comandos son útiles para ejecutar uno o varios screen con sus respectivos servidores.
```bash
screen -list
Ctrl-a Ctrl-d   Desconectar y dejar la sesión en funcionamiento
screen -S xxx   crea el screen xxx
screen -r xxx   regresa a ese screen
```