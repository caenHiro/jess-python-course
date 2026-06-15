---
semana: 6
tema: Entornos virtuales, decoradores y excepciones
estado: pendiente
---

# Semana 6 — Entornos virtuales, Decoradores y Excepciones

> Tiempo estimado: 4 horas
> Al terminar: `bash scripts/push.sh "semana-06 venv-decoradores"`

---

## Entornos virtuales (venv) — fundamental en Python

En Java usabas Maven para manejar dependencias (librerias externas). En Python se usa `pip` + `venv`.

Un **entorno virtual** aisla las dependencias de cada proyecto. Sin esto, todas las librerias se mezclan en tu sistema.

```bash
# Crear un entorno virtual
python3 -m venv .venv

# Activarlo (Linux/Mac)
source .venv/bin/activate

# Activarlo (Windows)
.venv\Scripts\activate

# Instalar una libreria
pip install requests

# Ver que esta instalado
pip list

# Guardar las dependencias del proyecto
pip freeze > requirements.txt

# Instalar desde requirements.txt (cuando alguien clona tu proyecto)
pip install -r requirements.txt

# Desactivar el entorno
deactivate
```

**Regla:** siempre crea un `.venv` antes de instalar paquetes. El `.venv/` va en `.gitignore`.

---

## Excepciones en Python

```python
# try/except en lugar de try/catch
try:
    numero = int(input("Ingresa un numero: "))
    resultado = 10 / numero
    print(f"Resultado: {resultado}")
except ValueError:
    print("Eso no es un numero")
except ZeroDivisionError:
    print("No puedes dividir entre 0")
except Exception as e:
    print(f"Error inesperado: {e}")
finally:
    print("Esto siempre se ejecuta")
```

Tipos comunes:
- `ValueError` — conversion fallida (`int("hola")`)
- `ZeroDivisionError` — division entre 0
- `FileNotFoundError` — archivo no encontrado
- `KeyError` — clave no existe en diccionario
- `IndexError` — indice fuera de rango en lista

---

## Lanzar tu propia excepcion

```python
def dividir(a, b):
    if b == 0:
        raise ValueError("No se puede dividir entre 0")
    return a / b

try:
    print(dividir(10, 0))
except ValueError as e:
    print(f"Error: {e}")
```

---

## Decoradores — funciones que modifican funciones

Un decorador es una funcion que envuelve a otra funcion para agregarle comportamiento. Los veras mucho en FastAPI (`@router.get`, `@router.post`, etc.).

```python
def mi_decorador(funcion):
    def envolvente():
        print("Antes de ejecutar")
        funcion()
        print("Despues de ejecutar")
    return envolvente

@mi_decorador
def saludar():
    print("Hola!")

saludar()
# Antes de ejecutar
# Hola!
# Despues de ejecutar
```

En FastAPI lo veras asi:
```python
@router.get("/usuarios")         # decorador que registra la ruta
def obtener_usuarios():
    return [{"id": 1, "nombre": "Jess"}]
```

No necesitas crear decoradores propios — basta con entender que `@algo` modifica la funcion de abajo.

---

## A recordar

- `venv` = entorno aislado por proyecto (como `pom.xml` en Maven pero para el entorno)
- `pip install` instala paquetes, `pip freeze > requirements.txt` los guarda
- `try/except` en lugar de `try/catch` en Java
- Decoradores `@nombre` modifican el comportamiento de una funcion

---

[[03_Practicas/semana-06]]
