---
semana: 11
tema: S3 + Lambda + boto3
estado: pendiente
---

# Semana 11 — S3 + Lambda: guardar archivos en la nube

> Tiempo estimado: 5 horas
> Al terminar: `bash scripts/push.sh "semana-11 s3-lambda"`

---

## ¿Que es S3?

Amazon S3 (Simple Storage Service) es como un disco duro enorme en la nube. Guardas "objetos" (archivos) en "buckets" (carpetas). Carlos lo usa en INE/PREP para guardar imagenes y reportes.

---

## Crear un bucket S3

Desde la consola AWS:
1. S3 → Create Bucket
2. Nombre unico global: `jess-practica-2026` (los nombres son globales en AWS)
3. Region: `us-east-1`
4. Bloquear acceso publico: ON (por seguridad)
5. Create Bucket

Desde CLI:
```bash
aws s3 mb s3://jess-practica-2026 --region us-east-1
```

---

## Operaciones basicas con boto3

```python
import boto3

s3 = boto3.client("s3", region_name="us-east-1")
BUCKET = "jess-practica-2026"

# Subir un archivo
s3.upload_file("mi_archivo.txt", BUCKET, "carpeta/mi_archivo.txt")

# Listar objetos
response = s3.list_objects_v2(Bucket=BUCKET)
for obj in response.get("Contents", []):
    print(obj["Key"], obj["Size"])

# Descargar un archivo
s3.download_file(BUCKET, "carpeta/mi_archivo.txt", "descargado.txt")

# Leer contenido sin descargar
response = s3.get_object(Bucket=BUCKET, Key="carpeta/mi_archivo.txt")
contenido = response["Body"].read().decode("utf-8")
print(contenido)

# Eliminar
s3.delete_object(Bucket=BUCKET, Key="carpeta/mi_archivo.txt")

# URL pre-firmada (acceso temporal)
url = s3.generate_presigned_url(
    "get_object",
    Params={"Bucket": BUCKET, "Key": "archivo.txt"},
    ExpiresIn=3600   # expira en 1 hora
)
```

---

## Lambda que se activa cuando llega un archivo a S3

```python
def handler(event, context):
    # Cuando S3 llama a esta Lambda, el evento contiene los archivos nuevos
    for registro in event["Records"]:
        bucket = registro["s3"]["bucket"]["name"]
        clave = registro["s3"]["object"]["key"]
        print(f"Nuevo archivo: {clave} en {bucket}")

        # Procesar el archivo...
        s3 = boto3.client("s3")
        response = s3.get_object(Bucket=bucket, Key=clave)
        contenido = response["Body"].read().decode("utf-8")
        print(f"Contenido: {contenido[:100]}")
```

Para conectar S3 con Lambda:
Lambda → Add Trigger → S3 → seleccionar bucket → Event type: PUT

---

## Permisos IAM para la Lambda

La Lambda necesita un rol con permisos para acceder a S3. Ejemplo de policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:PutObject", "s3:DeleteObject"],
      "Resource": "arn:aws:s3:::jess-practica-2026/*"
    }
  ]
}
```

---

## A recordar

- S3 = almacenamiento de archivos en la nube (no BD relacional)
- Los archivos se llaman "objetos", las carpetas se llaman "buckets"
- `boto3.client("s3")` crea el cliente
- Las Lambdas necesitan permisos IAM para acceder a S3

---

[[03_Practicas/semana-11]]
