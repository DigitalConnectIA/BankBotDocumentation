# LAMBDAS
Este readme sirve para testear el funcionamiento de las lambas
## /conversations
La integración de esta ruta está compuesta por la lambda `ConversationService`. La configuracion de esta lambda solo requiere de las siguientes variables de entorno:
```
cluster_arn_aurora = "ARN del cluster"
secret_arn_aurora = "aquí Jose Luis"
```
La peticion a esta ruta es por el método `POST` y puede recibir cualquiera de los siguientes JSON.  
Definicion de creacion de una conversacion, ```idClient``` -> referencia al ID de cliente
```json
{
    "operation": "create",
    "payload": {
        "Item": {
          "transcription": {
            "messageIn": "data",
            ...
          },
          "states": {},
          "idClient": null, 
          "intent": null,
          "lastState": null,
          "lasQuestion": null,
        }
    }
}
```
Definicion de getItem para la conversacion
```json
{
    "operation": "getItem",
    "payload": {
        "Item": {
            "sessionId": "cb00463f-7166-11eb-9998-c727838c173"
        }
    }
}
```
Definicion de update para la conversacion, ```sessionId``` -> requerido, ```idClient``` -> referencia al ID del cliente
```json
{
    "operation": "update",
    "payload": {
        "Item": {
          "sessionId": "cb00463f-7166-11eb-9998-c727838c1732",
          "transcription": {
            "messageIn": "data",
            ...
          },
          "states": {},
          "idClient": null,
          "intent": null,
          "lastState": null,
          "lasQuestion": null,
        }
    }
}
```
Definicion de delete para la conversación
```json
{
    "operation": "delete",
    "payload": {
        "Item": {
            "sessionId": "cb00463f-7166-11eb-9998-c727838c173"
        }
    }
}
```
