---
semana: 4
tema: POO en Python
estado: pendiente
---

# Semana 4 — POO en Python

> Tiempo estimado: 4 horas
> Al terminar: `bash scripts/push.sh "semana-04 clases-python"`

---

## Clases en Python vs Java

```python
# Java:
# public class Persona {
#     private String nombre;
#     public Persona(String nombre) { this.nombre = nombre; }
#     public void saludar() { ... }
# }

# Python:
class Persona:
    def __init__(self, nombre, edad):   # __init__ es el constructor
        self.nombre = nombre            # self es como "this" en Java
        self.edad = edad

    def saludar(self):
        print(f"Hola, soy {self.nombre}, tengo {self.edad} años")

    def es_mayor_de_edad(self):
        return self.edad >= 18
```

Diferencias clave:
- `def __init__(self, ...)` es el constructor (se llama `__init__`)
- `self` es como `this` — siempre es el primer parametro de cada metodo
- No hay `public`/`private` declarado — en Python todo es "publico" por convencion

---

## Crear objetos

```python
jess = Persona("Jess", 22)
carlos = Persona("Carlos", 30)

jess.saludar()         # Hola, soy Jess, tengo 22 años
print(carlos.nombre)   # Carlos
print(jess.es_mayor_de_edad())   # True
```

---

## Herencia en Python

```python
class Animal:
    def __init__(self, nombre):
        self.nombre = nombre

    def hacer_sonido(self):
        print("...")

class Perro(Animal):               # extends Animal
    def __init__(self, nombre, raza):
        super().__init__(nombre)   # llama al constructor del padre
        self.raza = raza

    def hacer_sonido(self):        # override
        print(f"{self.nombre}: ¡Guau!")

    def buscar_pelota(self):
        print(f"{self.nombre} busca la pelota")
```

```python
rex = Perro("Rex", "Labrador")
rex.hacer_sonido()     # Rex: ¡Guau!
rex.buscar_pelota()    # Rex busca la pelota
```

---

## Atributos "privados" — convencion con _

En Python no hay `private` real. La convencion es usar `_`:

```python
class CuentaBancaria:
    def __init__(self, titular, saldo):
        self.titular = titular
        self._saldo = saldo     # _ indica "no acceder directamente"

    def depositar(self, cantidad):
        if cantidad > 0:
            self._saldo += cantidad

    def get_saldo(self):
        return self._saldo
```

---

## dataclass — clases de datos simples

Python moderno tiene `@dataclass` que elimina mucho codigo repetitivo:

```python
from dataclasses import dataclass

@dataclass
class Producto:
    nombre: str
    precio: float
    stock: int = 0   # valor por defecto

p = Producto("Laptop", 15000.0, 5)
print(p)   # Producto(nombre='Laptop', precio=15000.0, stock=5)
```

Esto genera automaticamente `__init__`, `__repr__` y mas.

---

## A recordar

- `class NombreClase:` — sin `public`, sin `{}`
- `def __init__(self, ...)` — constructor
- `self` = `this` en Java (siempre primer parametro)
- `class Hijo(Padre):` — herencia
- `super().__init__(...)` — llamar al constructor del padre
- `_atributo` — convencion de "privado" (no real)

---

[[03_Practicas/semana-04]]
