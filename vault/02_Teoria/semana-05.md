---
semana: 5
tema: Archivos y JSON
estado: pendiente
---

# Semana 5 — Archivos, JSON y manejo de datos

> Tiempo estimado: 4 horas
> Al terminar: `bash scripts/push.sh "semana-05 archivos-json"`

---

## Leer y escribir archivos de texto

```python
# Escribir un archivo
with open("mi_archivo.txt", "w") as f:
    f.write("Hola Mundo\n")
    f.write("Segunda linea\n")

# Leer un archivo (todas las lineas)
with open("mi_archivo.txt", "r") as f:
    contenido = f.read()
    print(contenido)

# Leer linea por linea
with open("mi_archivo.txt", "r") as f:
    for linea in f:
        print(linea.strip())   # strip() quita el salto de linea

# Agregar al final (append)
with open("mi_archivo.txt", "a") as f:
    f.write("Tercera linea\n")
```

El `with` cierra el archivo automaticamente al terminar el bloque.

---

## CSV — datos en tabla

```python
import csv

# Escribir CSV
with open("estudiantes.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["nombre", "edad", "promedio"])   # encabezado
    writer.writerow(["Jess", 22, 9.5])
    writer.writerow(["Carlos", 30, 8.8])

# Leer CSV
with open("estudiantes.csv", "r") as f:
    reader = csv.DictReader(f)   # cada fila es un diccionario
    for fila in reader:
        print(fila["nombre"], fila["promedio"])
```

---

## JSON — el formato de las APIs web

JSON es el formato que usan todas las APIs web para enviar y recibir datos. Veras JSON constantemente cuando trabajes con FastAPI y AWS.

```python
import json

# Python dict → JSON string
persona = {"nombre": "Jess", "edad": 22, "activa": True}
json_texto = json.dumps(persona)
print(json_texto)   # '{"nombre": "Jess", "edad": 22, "activa": true}'

# JSON string → Python dict
texto = '{"nombre": "Carlos", "edad": 30}'
persona2 = json.loads(texto)
print(persona2["nombre"])   # Carlos

# Guardar en archivo .json
with open("persona.json", "w") as f:
    json.dump(persona, f, indent=2)   # indent=2 lo hace legible

# Leer desde archivo .json
with open("persona.json", "r") as f:
    datos = json.load(f)
print(datos)
```

---

## Manejo de errores con archivos

```python
try:
    with open("archivo_que_no_existe.txt", "r") as f:
        contenido = f.read()
except FileNotFoundError:
    print("El archivo no existe")
except PermissionError:
    print("Sin permisos para leer el archivo")
```

---

## A recordar

- `with open("archivo", modo) as f:` — modo: `"r"` leer, `"w"` escribir, `"a"` agregar
- `with` cierra el archivo automaticamente
- `json.dumps()` — Python a JSON string
- `json.loads()` — JSON string a Python
- `json.dump()` / `json.load()` — leer/escribir archivos JSON

---

[[03_Practicas/semana-05]]
