---
semana: 7
tema: FastAPI — tu primera API REST
estado: pendiente
---

# Semana 7 — FastAPI: API REST en Python

> Tiempo estimado: 5–6 horas (el salto a web — muy emocionante)
> Al terminar: `bash scripts/push.sh "semana-07 fastapi"`

---

## ¿Que es una API REST?

Una API es como un mesero: tu le pides algo (una peticion HTTP), el va a la cocina (backend), y te trae el resultado (la respuesta).

FastAPI es el framework de Python que Carlos usa en el Portal Personal. Con el crearemos nuestra primera API en minutos.

---

## Setup

```bash
# En tu carpeta codigo/semana-07/
python3 -m venv .venv
source .venv/bin/activate   # o .venv\Scripts\activate en Windows
pip install fastapi uvicorn
```

---

## Tu primera API

Crea `main.py`:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def inicio():
    return {"mensaje": "Hola desde mi API!"}

@app.get("/saludo/{nombre}")
def saludar(nombre: str):
    return {"mensaje": f"Hola, {nombre}!"}
```

Correrla:
```bash
uvicorn main:app --reload
```

Abre en el navegador: `http://localhost:8000`
Documentacion automatica: `http://localhost:8000/docs`

---

## Metodos HTTP

| Metodo | Para que | Ejemplo |
|--------|----------|---------|
| `GET` | Obtener datos | Ver una lista de productos |
| `POST` | Crear datos | Crear un producto nuevo |
| `PUT` | Actualizar completo | Actualizar todos los campos |
| `PATCH` | Actualizar parcial | Solo cambiar el precio |
| `DELETE` | Eliminar | Borrar un producto |

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

# Lista en memoria (sin BD por ahora)
tareas = []

class Tarea(BaseModel):
    titulo: str
    completada: bool = False

@app.get("/tareas")
def listar_tareas():
    return tareas

@app.post("/tareas")
def crear_tarea(tarea: Tarea):
    tareas.append(tarea)
    return {"mensaje": "Tarea creada", "tarea": tarea}

@app.delete("/tareas/{indice}")
def eliminar_tarea(indice: int):
    if 0 <= indice < len(tareas):
        eliminada = tareas.pop(indice)
        return {"eliminada": eliminada}
    return {"error": "Indice no valido"}
```

---

## Pydantic — validacion de datos

`BaseModel` de Pydantic valida automaticamente que los datos que lleguen sean del tipo correcto:

```python
from pydantic import BaseModel

class Producto(BaseModel):
    nombre: str
    precio: float
    stock: int = 0   # valor por defecto
```

Si alguien manda un `precio` que no es numero, FastAPI automaticamente devuelve un error 422 con el detalle del problema. Muy conveniente.

---

## Probar tu API con Swagger

FastAPI genera documentacion interactiva automaticamente en `/docs`. Desde ahi puedes:
- Ver todos los endpoints
- Probar cada uno sin necesidad de Postman
- Ver que parametros necesita cada endpoint

---

## A recordar

- `FastAPI()` crea la app
- `@app.get("/ruta")` registra un endpoint GET
- `uvicorn main:app --reload` corre el servidor con recarga automatica
- `BaseModel` de Pydantic valida los datos de entrada
- `/docs` — documentacion automatica interactiva

---

[[03_Practicas/semana-07]]
