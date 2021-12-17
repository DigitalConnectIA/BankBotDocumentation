# API's
Estas API's son usadas en el Front-End de Amplify, cada una será especificada y detalla para conocer su funcionamiento, hasta el momento se tienen solo dos y son
* **PointAccess**
* **Socket_user**
* **Socket_agente**

## PointAccess
Esta API es la central, su configuración en el Template SAM ya incluye la activación de cors y el método de respuesta de cada una de las siguientes rutas.
* /reports
* /user
* /{folder}/{item}
* /trainer

### /reports
La integración que tiene esta ruta es con la lambda `ReportsService`. La configuracion de esta lambda solo requiere de las siguientes variables de entorno:
```
cluster_arn_aurora = "ARN del cluster"
secret_arn_aurora = "aquí Jose Luis"
```
La peticion a esta ruta es por el método `POST` y puede recibir cualquiera de los siguientes JSON  
Definicion de creacion de reporte, todos los campos son requeridos
```json
{
    "operation": "create",
    "payload": {
        "Item": {
            "agent": "Jose Luis",
            "comment": "No le han llamado para su cotizacion",
            "priorityAttention": true,
            "processStatus": "pendiente"
        }
    }
}
```
Definicion de fullGet para extraer todos los reportes
```json
{
    "operation": "fullGet",
    "payload": {
        "Item": {}
    }
}
```
Definicion de la obtencion de reportes por rango de fechas. Fechas requeridas
```json
{
    "operation": "getReportByDate",
    "payload": {
        "Item": {
            "dateStart": "2021-06-15 00:00:00",
            "dateEnd": "2021-06-15 23:59:59"
        }
    }
}
```
Definicion de la obtencion de reportes por status del reporte
```json
{
    "operation": "getReportByStatus",
    "payload": {
        "Item": {
            "status": "activo"
        }
    }
}
```
Definicion de la obtencion de reportes por agente
```json
{
    "operation": "getReportByAgent",
    "payload": {
        "Item": {
            "agent": "activo"
        }
    }
}
```
Definicion para la actualiacion del reporte. reportId requerido
```json
{
  "operation": "update",
  "payload": {
      "Item": {
          "reportId": "85cdc38ade",
          "agent": "sandoval",
          "comment": "No le han llamado para su cotizacion. Llamada realizada",
          "priorityAttention": true,
          "processStatus": "solucionado"
      }
  }
}
```
Definicion para eliminar el reporte. reportId requerido
```json
{
    "operation": "delete",
    "payload": {
        "Item": {
            "reportId": "85cdc38ade"
        }
    }
}
```




### /user
La integración que tiene esta ruta es con la lambda `UserService`. La configuracion de esta lambda solo requiere de las siguientes variables de entorno:
```
cluster_arn_aurora = "ARN del cluster"
secret_arn_aurora = "aquí Jose Luis"
```
La peticion a esta ruta es por el método `POST` o `GET` y puede recibir cualquiera de los siguientes JSON  
Definicion de creacion de usuario, ```email``` -> requerido, ```password``` -> requerido
```json
{
    "operation": "create",
    "payload": {
        "Item": {
            "name": "Jose Luis",
            "lastName": "Palillero Huerta",
            "email": "test@digitialconnect.com.mx",
            "phone": "1234567890",
            "rol": "soporte",
            "lastState": "activo",
            "position": "asesor",
            "password": "1234",
            "Dashboard": false,
            "Chat": false,
            "Reportes": false,
            "Respuestas": false,
            "MiCuenta": false,
            "RecuperarPsswrd": false,
            "Consultar": false,
            "Nuevo": false,
            "sessionId": ""
        }
    }
}
```
Definicion de getItem para los usuarios, ```email``` -> requerido
```json
{
    "operation": "get",
    "payload": {
        "Item": {
            "email": "jlpalillero1@digitialconnect.com.mx"
        }
    }
}
```
Definicion de login para usuarios
```json
{
    "operation": "login",
    "payload": {
        "Item": {
            "email": "jlpalillero1@digitialconnect.com.mx",
            "password": "1234"
        }
    }
} 
```
Definicion de update para usuarios
```json
{
    "operation": "update",
    "payload": {
        "Item": {
            "id": 13,
            "email": "test@digitialconnect.com.mx",
            "lastName": "Palillero Huerta",
            "name": "Jose Luis",
            "phone": "0987654321",
            "rol": "portal",
            "lastState": "activo",
            "position": "asesor",
            "password":"81dc9bdb52d04dc20036dbd8313ed055",
            "Dashboard": false,
            "Chat": false,
            "Respuestas": true,
            "Reportes": false,
            "MiCuenta": false,
            "RecuperarPsswrd": false,
            "Consultar": false,
            "Nuevo": false
        }
    }
}
```
Definicion de delete para usuarios
```json
{
    "operation": "delete",
    "payload": {
        "Item": {
            "email": "jlpalillero@digitialconnect.com.mx"
        }
    }
}
```
Para recuperar contraseña
```json
{
    "operation": "recoverPasswd",
    "payload": {
        "Item": {
            "email": "juan.sandoval@digitalconnect.com.mx"
        }
    }
}
```
Para obtener usuarios por rol:
```json
{
    "operation": "getUsersByRol",
    "payload": {
        "Item": {
            "rol": "servicio"
        }
    }
}
```
Para obtener usuarios por nombre y apellido:
```json
{
    "operation": "getByNameLast",
    "payload": {
        "Item": {
            "name": "juan",
            "lastName": "sandoval"
        }
    }
}
```
Para obtener usuarios por estado:
```json
{
    "operation": "getUsersByState",
    "payload": {
        "Item": {
            "lastState": "alta"
        }
    }
}
```
Para obtener todos los usuarios:
```json
{
    "operation": "fullGet",
    "payload": {
        "Item":{}
    }
}
```

### /{folder}/{item}
La integración de esta ruta es con el servicio de `s3` y se encarga de realizar el almacenamiento de un archivo dentro de un bucket ya existente. Su método es `PUT` y el body donde va el archivo debe ser ```application/octet-stream``` un ejemplo de ruta es ```https://17ralen7pg.execute-api.us-west-2.amazonaws.com/dev/datoslex/lex.zip``` donde ```datoslex``` es el nombre del bucket existente y ```lex.zip``` es el nombre con el que se guardar el archivo en el body de la petición

### /trainer
Esta es la api que muestra los datos de entrenamiento y tambien recibe nuevos datos para re entrenar los motores, el json para obtener los datos es el siguiente:  
```json
{
    "operation": "getData",
    "payload": {}
}
```
Es indispensable que no falte ningun campo a pesar de de ir vacio. Para re entrenar el motor se requiere del siguiente json:  
```json
{
    "operation":"trainer",
    "payload":{
        "intent": [
            {
                "name": "despedida",
                "slots": [
                    "credito"
                ],
                "examples": [
                    "hasta luego espero su llamada para el [credito](prestamo)",
                    "hasta luego espero su correo"
                ],
                "response": "Un placer atenderte",
                "lexemas": []
            }
        ],
        "entity": [
            {
                "name":"credito",
                "values":[
                    "prestamo",
                    "interes",
                    "cat"
                ]
            }
        ]
    }
}
```
Para que el entrenamiento sea correcto se debe respetar la sintaxis de payload y de las entity dentro de los examples y slots
## Socket_user
Esta API consta de tres rutas `$connect`, `$disconnect` y `mensaje`. Cada una cuenta con su respectiva lambda con los siguientes nombres `SocketConnectUser`, `SocketDisconnectUser` y `SocketMensajeUser`
### SocketConnectUser
Esta lambda por el momento solo muestra en CloudWatch los datos de conexión
### SocketDisconnectUser
Al momento de desconectarse del socket, esta genera un delete mediante rds-data para la tabla conversations donde elimina la conversación del sessionId en curso
### SocketMensajeUser
Aquí se reciben los mensajes por parte del usuario. En esta primera parte se verifica si esta hablando con el bot o con un agente.  
```python
query=QueryConversation(event['requestContext']['connectionId'])
print(query)
if 'idSocket' in query:
```
En el caso de hablar con el bot invoca la Step Function, si el resultado es hablar con un agente, se le transfiere, sino solo se envía el resultado del bot.  
```python
sf_data = "{\"sessionID\":\""+event['requestContext']['connectionId']+"\",\"mensaje\":\""+json.loads(event['body'])['message']+"\"}"
sf_respuesta = sf.start_sync_execution(stateMachineArn=os.environ['STATE_MACHINE'],input=str(sf_data))
mensajeBot=json.loads(sf_respuesta['output'])
if json.loads(sf_respuesta['output'])['intent'] == 'agentehabla':
```
## socket_agente
Esta API consta de tres rutas `$connect`, `$disconnect` y `mensaje`. Cada una cuenta con su respectiva lambda con los siguientes nombres `SocketConnectAgent`, `SocketDisconnectAgent` y `SocketMensajeAgent`
### SocketConnectAgent
Esta lambda es la encarga de consultar que agente esta disponible para atender el chat, lo hace mediante consultas a la tabla Users
### SocketDisconnectAgent
Se encarga de modificar el status del agente dentro de la tabla Users, para notificar que no está conectado
### SocketMensajeAgent
Aquí se reciben los mensajes por parte del agente. En caso de tener asigando un usuario, redirige los mensajes a el, en caso contrario solo notifica que no tiene usuario asignado