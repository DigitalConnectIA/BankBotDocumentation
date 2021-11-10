# StateMaching
Esta maquina de estados es la encarga de dar el flujo de conversación de cada petición que se le hace al chatbot, consta de varias lambdas, estas mismas son adaptables según los requerimientos de la conversación 
El dato de entrada del la State Machine es el siguiente JSON. En donde sessionID es el identificador del chat ya sea el `ID` de la llamada de voz de Twilio o el `ID` del socket del chat
```json
{"sessionID": "di3Jae7vvHcCFfA=", "mensaje":"hola"}
```
El json de salida de la StateMachine es el siguiente, este formato es importante debido a que el Front-End ya esta configurado para recibir estos datos.
```json
{"respuesta": "hola", "sessionID": "di3Jae7vvHcCFfA=", "intent": "saludo"}
```
Gráficamente el funcionamiento de la StateMachine queda como se muestra en la siguiente figura.  
  
![Arquitectura StepFunction](https://referencias-documentacion-md.s3-us-west-2.amazonaws.com/StepFunction.jpg)

## Definición de State Machine
La estructura definida para la State Machine es el siguiente JSON. En este mismo se muestra que las entras y salidas de cada paso son las definidas dentro de las lambdas 

```json
{
    "Comment": "Prueba 01 de flujo de conversacion",
    "StartAt": "uno",
    "States": {
      "uno": {
        "Type": "Task",
        "Resource": "${SFPasoUnoArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "motores"
      },
      "motores": {
        "Type": "Choice",
        "Choices": [
          {
            "Variable": "$.estado",
            "StringEquals": "mensajex",
            "Next": "mensajex"
          },
          {
            "Variable": "$.estado",
            "StringEquals": "aclaracion",
            "Next": "aclaracion"
          },
          {
            "Variable": "$.estado",
            "StringEquals": "credito",
            "Next": "credito"
          },
          {
            "Variable": "$.estado",
            "StringEquals": "cuenta",
            "Next": "cuenta"
          },
          {
            "Variable": "$.estado",
            "StringEquals": "seguro",
            "Next": "seguro"
          }
        ]
      },
      "mensajex": {
        "Type": "Task",
        "Resource": "${SFMensajeXArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "tres"
      },
      "aclaracion": {
        "Type": "Task",
        "Resource": "${SFAclaracionesArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "tres"
      },
      "credito": {
        "Type": "Task",
        "Resource": "${SFCreditosArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "tres"
      },
      "cuenta": {
        "Type": "Task",
        "Resource": "${SFCuentasArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "tres"
      },
      "seguro": {
        "Type": "Task",
        "Resource": "${SFSegurosArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "Next": "tres"
      },
      "tres": {
        "Type": "Task",
        "Resource": "${SFPasoTresArn}",
        "InputPath": "$",
        "OutputPath": "$",
        "End": true
      }
    }
  }
```
