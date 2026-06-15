---
semana: 2
tema: Funciones y modulos
estado: pendiente
---

# Semana 2 — Funciones y Modulos en Python

> Tiempo estimado: 3 horas
> Al terminar: `bash scripts/push.sh "semana-02 funciones"`

---

## Funciones — mas simples que en Java

```python
# Java: public static int sumar(int a, int b) { return a + b; }
def sumar(a, b):
    return a + b

# Llamar la funcion
resultado = sumar(5, 3)
print(resultado)   # 8
```

- `def` en lugar de `public static <tipo>`
- Sin declarar el tipo de los parametros
- Sin declarar el tipo de retorno
- El `return` es igual

---

## Parametros con valor por defecto

```python
def saludar(nombre, saludo="Hola"):
    print(f"{saludo}, {nombre}!")

saludar("Jess")              # Hola, Jess!
saludar("Carlos", "Buenos dias")   # Buenos dias, Carlos!
```

Esto en Java no existe — Python lo hace muy facil.

---

## Funciones que devuelven multiples valores

```python
def dividir(a, b):
    cociente = a // b
    residuo = a % b
    return cociente, residuo   # devuelve dos valores a la vez!

c, r = dividir(10, 3)
print(f"Cociente: {c}, Residuo: {r}")   # Cociente: 3, Residuo: 1
```

---

## Modulos — importar codigo

Python tiene miles de modulos listos para usar. Se importan con `import`.

```python
import math

print(math.pi)          # 3.141592...
print(math.sqrt(16))    # 4.0
print(math.pow(2, 10))  # 1024.0

import random

numero = random.randint(1, 100)   # numero aleatorio entre 1 y 100
print(numero)
```

---

## Crear tu propio modulo

Cualquier archivo `.py` es un modulo. Si creas `utilidades.py`:

```python
# utilidades.py
def calcular_iva(precio):
    return precio * 0.16

def calcular_total(precio):
    return precio + calcular_iva(precio)
```

Lo importas en otro archivo:
```python
# main.py
import utilidades

total = utilidades.calcular_total(100)
print(total)   # 116.0

# O importar funciones especificas
from utilidades import calcular_total
print(calcular_total(200))   # 232.0
```

---

## A recordar

- `def nombre(params):` define una funcion
- Puedes poner valores por defecto en los parametros: `def f(x=10):`
- Una funcion puede devolver multiples valores con comas: `return a, b`
- `import modulo` importa un modulo completo
- `from modulo import funcion` importa solo una parte

---

[[03_Practicas/semana-02]]
