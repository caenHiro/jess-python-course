---
semana: 3
tema: Listas, diccionarios y tuplas
estado: pendiente
---

# Semana 3 — Listas, Diccionarios y Tuplas

> Tiempo estimado: 4 horas
> Al terminar: `bash scripts/push.sh "semana-03 colecciones"`

---

## Listas — el ArrayList de Python

```python
# Java: ArrayList<String> frutas = new ArrayList<>();
frutas = ["manzana", "pera", "uva", "mango"]

# Acceder por indice (igual que en Java)
print(frutas[0])    # manzana
print(frutas[-1])   # mango  (ultimo elemento — truco Python!)

# Agregar
frutas.append("fresa")       # al final
frutas.insert(1, "kiwi")     # en posicion especifica

# Eliminar
frutas.remove("pera")        # por valor
frutas.pop(0)                # por indice

# Cuantos elementos
print(len(frutas))           # Java: frutas.size()

# Recorrer
for fruta in frutas:
    print(fruta)
```

### List comprehension — Python idiomatico

```python
numeros = [1, 2, 3, 4, 5]

# Java: for cada numero, si es par, agregalo al cuadrado a la lista
cuadrados_pares = [n**2 for n in numeros if n % 2 == 0]
print(cuadrados_pares)   # [4, 16]
```

Esto no existe en Java — es una de las cosas mas poderosas de Python.

---

## Diccionarios — el HashMap de Python

```python
# Java: HashMap<String, Integer> edades = new HashMap<>();
persona = {
    "nombre": "Jess",
    "edad": 22,
    "ciudad": "CDMX"
}

# Acceder
print(persona["nombre"])         # Jess
print(persona.get("email", "sin email"))  # sin email (valor por defecto)

# Agregar o modificar
persona["email"] = "jess@email.com"

# Eliminar
del persona["ciudad"]

# Recorrer
for clave, valor in persona.items():
    print(f"{clave}: {valor}")

# Solo claves o solo valores
print(persona.keys())
print(persona.values())
```

---

## Tuplas — arrays inmutables

```python
# Una tupla es como una lista pero no se puede modificar
coordenadas = (19.4326, -99.1332)   # latitud y longitud CDMX

x, y = coordenadas   # "desempacar" la tupla
print(x)   # 19.4326

# Util para devolver multiples valores de una funcion
def obtener_nombre_y_edad():
    return "Jess", 22   # internamente es una tupla

nombre, edad = obtener_nombre_y_edad()
```

---

## Slicing — cortar listas

```python
numeros = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numeros[2:5])    # [2, 3, 4]    — del indice 2 al 4
print(numeros[:3])     # [0, 1, 2]    — los primeros 3
print(numeros[7:])     # [7, 8, 9]    — desde el 7 hasta el final
print(numeros[::2])    # [0, 2, 4, 6, 8]  — cada 2 elementos
print(numeros[::-1])   # [9, 8, 7, ...0]  — al reves
```

---

## A recordar

- `lista = [a, b, c]` — lista mutable (se puede modificar)
- `diccionario = {"clave": "valor"}` — pares clave-valor (como HashMap)
- `tupla = (a, b, c)` — inmutable (no se puede modificar)
- `len()` en lugar de `.size()` o `.length`
- List comprehension: `[expresion for x in lista if condicion]`

---

[[03_Practicas/semana-03]]
