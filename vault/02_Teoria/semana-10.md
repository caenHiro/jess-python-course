---
semana: 10
tema: AWS Lambda — serverless Python
estado: pendiente
---

# Semana 10 — AWS Lambda: codigo sin servidor

> Tiempo estimado: 5–6 horas
> Al terminar: `bash scripts/push.sh "semana-10 lambda"`

---

## ¿Que es una Lambda?

Una Lambda es una funcion que corre en la nube SIN que tu tengas que mantener un servidor. AWS se encarga de todo: escalado, disponibilidad, actualizaciones del SO.

Tu solo escribes la funcion y defines cuando debe ejecutarse.

**Precio:** pagas por invocacion (llamada) y por tiempo de ejecucion. El free tier es 1 millon de invocaciones/mes.

---

## Estructura de una Lambda Python

```python
# lambda_function.py
def handler(event, context):
    """
    event: los datos que llegan a la Lambda (JSON)
    context: informacion del entorno de ejecucion (rara vez se usa)
    """
    nombre = event.get("nombre", "Mundo")
    return {
        "statusCode": 200,
        "body": f"Hola, {nombre}!"
    }
```

Eso es todo — una funcion que recibe un evento y devuelve una respuesta.

---

## Crear tu primera Lambda desde la consola

1. Consola AWS → Lambda → Create Function
2. **Function name:** `mi-primera-lambda`
3. **Runtime:** Python 3.12
4. Copia el codigo de arriba en el editor
5. **Test** → crear evento de prueba: `{"nombre": "Jess"}`
6. Ejecutar → ver el resultado

---

## Usar boto3 — el SDK de Python para AWS

`boto3` es la libreria de Python para interactuar con todos los servicios AWS.

```python
import boto3
import json

def handler(event, context):
    # Crear cliente S3
    s3 = boto3.client("s3")

    # Listar los buckets
    response = s3.list_buckets()
    buckets = [b["Name"] for b in response["Buckets"]]

    return {
        "statusCode": 200,
        "body": json.dumps({"buckets": buckets})
    }
```

**Importante:** la Lambda necesita permisos (IAM Role) para poder acceder a S3. Sin el rol, falla con error de permisos.

---

## Variables de entorno en Lambda

En lugar de hardcodear datos sensibles, usa variables de entorno:

```python
import os

def handler(event, context):
    nombre_bd = os.environ.get("DB_NAME", "default")
    region = os.environ.get("AWS_REGION", "us-east-1")
    return {"bd": nombre_bd, "region": region}
```

Las variables se configuran en: Lambda → Configuration → Environment Variables.

---

## Deploy desde la terminal (AWS CLI)

```bash
# Empaquetar tu codigo en un zip
zip function.zip lambda_function.py

# Actualizar el codigo de la Lambda
aws lambda update-function-code \
    --function-name mi-primera-lambda \
    --zip-file fileb://function.zip

# Ver los logs en CloudWatch
aws logs tail /aws/lambda/mi-primera-lambda --follow
```

---

## A recordar

- Una Lambda = una funcion Python que AWS ejecuta on-demand
- `handler(event, context)` es el punto de entrada — siempre
- `event` = los datos de entrada (JSON)
- `boto3` = libreria para usar todos los servicios AWS desde Python
- Variables de entorno para datos sensibles — nunca hardcodear keys o passwords

---

[[03_Practicas/semana-10]]
