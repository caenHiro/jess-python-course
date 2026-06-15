---
semana: 8
tema: FastAPI + PostgreSQL
estado: pendiente
---

# Semana 8 — FastAPI + PostgreSQL: el stack completo

> Tiempo estimado: 5–6 horas
> Prerequisito: Docker corriendo con PostgreSQL (ver guia instalacion)
> Al terminar: `bash scripts/push.sh "semana-08 fastapi-bd"`

---

## Conectar FastAPI a PostgreSQL

```bash
pip install psycopg2-binary sqlalchemy
```

---

## SQLAlchemy — ORM de Python

Un ORM (Object Relational Mapper) te permite trabajar con la BD usando clases Python en lugar de SQL puro.

```python
# database.py
from sqlalchemy import create_engine, Column, Integer, String, Float
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "postgresql://alumno:alumno123@localhost:5432/mi_escuela"

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(bind=engine)
Base = declarative_base()
```

---

## Definir una tabla como clase Python

```python
# models.py
from database import Base
from sqlalchemy import Column, Integer, String, Float

class Estudiante(Base):
    __tablename__ = "estudiantes"

    id = Column(Integer, primary_key=True, index=True)
    nombre = Column(String, nullable=False)
    edad = Column(Integer)
    promedio = Column(Float)
```

---

## Endpoints CRUD completo

```python
# main.py
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session
from database import SessionLocal, engine
from models import Estudiante, Base
from pydantic import BaseModel

Base.metadata.create_all(bind=engine)   # crea las tablas si no existen
app = FastAPI()

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

class EstudianteIn(BaseModel):
    nombre: str
    edad: int
    promedio: float

@app.get("/estudiantes")
def listar(db: Session = Depends(get_db)):
    return db.query(Estudiante).all()

@app.post("/estudiantes", status_code=201)
def crear(datos: EstudianteIn, db: Session = Depends(get_db)):
    nuevo = Estudiante(**datos.model_dump())
    db.add(nuevo)
    db.commit()
    db.refresh(nuevo)
    return nuevo

@app.delete("/estudiantes/{id}", status_code=204)
def eliminar(id: int, db: Session = Depends(get_db)):
    est = db.query(Estudiante).filter(Estudiante.id == id).first()
    if est:
        db.delete(est)
        db.commit()
```

---

## ¿Suena familiar?

Si ves el Portal Personal de Carlos, hace exactamente esto pero mas grande:
- FastAPI con endpoints REST
- PostgreSQL como base de datos
- SQLAlchemy o consultas directas
- Pydantic para validacion

Lo que tu haces esta semana es el 80% de como funciona el Portal.

---

## A recordar

- SQLAlchemy = ORM de Python (como JPA/Hibernate en Java)
- `Base.metadata.create_all()` crea las tablas automaticamente desde las clases
- `Depends(get_db)` inyecta la sesion de BD en cada endpoint
- `db.add()` → `db.commit()` → `db.refresh()` para crear registros

---

[[03_Practicas/semana-08]]
