---
semana: 12
tema: API Gateway + Lambda — proyecto final serverless
estado: pendiente
---

# Semana 12 — API Gateway + Lambda: tu primera API en la nube

> Tiempo estimado: 6–8 horas
> Al terminar: `bash scripts/push.sh "semana-12 proyecto-serverless COMPLETADO"`

---

## ¿Que es API Gateway?

API Gateway expone tus Lambdas como endpoints HTTP accesibles desde internet. Es el puente entre el usuario y tu codigo Lambda.

```
Internet → API Gateway → Lambda → DynamoDB/S3
```

---

## Proyecto Final: API de Notas Personales

Crearemos una API serverless completa:
- `POST /notas` — crear una nota
- `GET /notas` — listar todas las notas
- `GET /notas/{id}` — ver una nota especifica
- `DELETE /notas/{id}` — eliminar una nota

Los datos se guardan en **DynamoDB** (BD NoSQL serverless — perfecta para Lambda).

---

## DynamoDB — BD sin servidor

```python
import boto3
import uuid
from datetime import datetime

dynamodb = boto3.resource("dynamodb", region_name="us-east-1")
tabla = dynamodb.Table("notas")

# Crear una nota
tabla.put_item(Item={
    "id": str(uuid.uuid4()),
    "titulo": "Mi primera nota",
    "contenido": "Esto es lo que aprendi esta semana",
    "fecha": datetime.now().isoformat()
})

# Obtener todas las notas
response = tabla.scan()
notas = response["Items"]

# Obtener una nota por ID
response = tabla.get_item(Key={"id": "uuid-aqui"})
nota = response.get("Item")
```

---

## Lambda handler completo

```python
import boto3
import json
import uuid
from datetime import datetime

dynamodb = boto3.resource("dynamodb")
tabla = dynamodb.Table("notas")

def handler(event, context):
    metodo = event["httpMethod"]
    path = event["path"]

    if metodo == "GET" and path == "/notas":
        return listar_notas()
    elif metodo == "POST" and path == "/notas":
        body = json.loads(event["body"])
        return crear_nota(body)
    elif metodo == "DELETE":
        nota_id = event["pathParameters"]["id"]
        return eliminar_nota(nota_id)
    else:
        return {"statusCode": 404, "body": json.dumps({"error": "No encontrado"})}

def listar_notas():
    response = tabla.scan()
    return {"statusCode": 200, "body": json.dumps(response["Items"])}

def crear_nota(datos):
    nota = {
        "id": str(uuid.uuid4()),
        "titulo": datos["titulo"],
        "contenido": datos.get("contenido", ""),
        "fecha": datetime.now().isoformat()
    }
    tabla.put_item(Item=nota)
    return {"statusCode": 201, "body": json.dumps(nota)}

def eliminar_nota(nota_id):
    tabla.delete_item(Key={"id": nota_id})
    return {"statusCode": 204, "body": ""}
```

---

## Crear la API Gateway desde consola

1. API Gateway → Create API → HTTP API
2. Integrations: Lambda → seleccionar tu Lambda
3. Routes:
   - `GET /notas`
   - `POST /notas`
   - `DELETE /notas/{id}`
4. Deploy → Stage: `dev`
5. AWS te da una URL: `https://abc123.execute-api.us-east-1.amazonaws.com/dev`

---

## Probar la API desde terminal

```bash
BASE_URL="https://tu-url.execute-api.us-east-1.amazonaws.com/dev"

# Crear nota
curl -X POST $BASE_URL/notas \
  -H "Content-Type: application/json" \
  -d '{"titulo": "Mi nota", "contenido": "Aprendi Lambda!"}'

# Listar notas
curl $BASE_URL/notas
```

---

## Reflexion final del Curso 2

**¿Que diferencias notas entre Python y Java para hacer APIs?**

_Tu respuesta:_

**¿Como se siente ejecutar codigo real en la nube de Amazon?**

_Tu respuesta:_

**¿Cuales aspectos de AWS te gustaron mas?**

_Tu respuesta:_

**¿Te interesaria explorar mas sobre seguridad en AWS (el Curso 3)?**

_Tu respuesta:_

---

> Felicidades — ya tienes una API real corriendo en AWS. Eso es lo que hacen los profesionales.
