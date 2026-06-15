---
semana: 1
tema: Python basico — traduccion desde Java
estado: pendiente
---

# Semana 1 — Python: mismo concepto, diferente sintaxis

> Tiempo estimado: 2–3 horas (ya sabes programar — esto es mas rapido)
> Al terminar: `bash scripts/push.sh "semana-01 python basico"`

---

## La gran diferencia

En Java escuchabas: `public static void main(String[] args)`. En Python ese mismo concepto es:
```python
# No hay nada que escribir — el archivo ya ES el programa
print("Hola Mundo")
```

Python tiene menos "ceremonia". No necesitas declarar la clase, ni el tipo de las variables, ni los puntos y coma.

---

## Variables en Python

```python
# Java: int edad = 25;
edad = 25              # Python: sin tipo, sin ;

# Java: double precio = 99.50;
precio = 99.50

# Java: String nombre = "Jess";
nombre = "Jess"

# Java: boolean activo = true;
activo = True          # en Python es True/False (con mayuscula)
```

Python deduce el tipo automaticamente. A esto se le llama **tipado dinamico**.

---

## Imprimir con print()

```python
nombre = "Jess"
edad = 22

# Concatenar (como en Java con +)
print("Me llamo " + nombre)

# Forma Python idiomatica: f-strings (mas comodo)
print(f"Me llamo {nombre} y tengo {edad} años")

# Con coma (agrega espacio automatico)
print("Hola", nombre, "tienes", edad, "años")
```

Los **f-strings** (`f"texto {variable}"`) son la forma moderna en Python. Muy facil.

---

## Entrada del usuario

```python
# Java: Scanner sc = new Scanner(System.in); String nombre = sc.nextLine();
nombre = input("¿Como te llamas? ")    # Python: una sola linea

# Para numeros hay que convertir (igual que en Java con parseInt)
edad = int(input("¿Cuantos años tienes? "))
precio = float(input("¿Cual es el precio? "))
```

---

## Operadores — identicos a Java

```python
a = 10
b = 3

print(a + b)   # 13
print(a - b)   # 7
print(a * b)   # 30
print(a / b)   # 3.333...  (siempre da decimales en Python!)
print(a // b)  # 3  (division entera — necesitas // para esto)
print(a % b)   # 1
print(a ** b)  # 1000  (potencia — en Java era Math.pow)
```

---

## Condicionales — sin parentesis, con dos puntos

```python
edad = 20

# Java: if (edad >= 18) { ... }
if edad >= 18:
    print("Mayor de edad")    # la indentacion reemplaza a las llaves {}
elif edad >= 15:
    print("Adolescente")
else:
    print("Menor de edad")

# NO SE NECESITAN parentesis ni llaves — la indentacion define el bloque
```

---

## Ciclos

```python
# for — recorre un rango
for i in range(1, 6):     # 1, 2, 3, 4, 5
    print(i)

# for — recorre una lista
frutas = ["manzana", "pera", "uva"]
for fruta in frutas:
    print(fruta)

# while — identico a Java
n = 0
while n < 5:
    print(n)
    n += 1
```

---

## Tabla de equivalencias Java → Python

| Java | Python |
|------|--------|
| `int x = 5;` | `x = 5` |
| `System.out.println("hola")` | `print("hola")` |
| `Scanner + nextLine()` | `input()` |
| `if (condicion) { }` | `if condicion:` + indentacion |
| `for (int i=0; i<10; i++)` | `for i in range(10):` |
| `true / false` | `True / False` |
| `// comentario` | `# comentario` |
| `/* bloque */` | `""" bloque """` |

---

## A recordar

- Sin punto y coma al final de las lineas
- Sin llaves `{}` — la indentacion (espacios) define los bloques
- Sin declarar el tipo de las variables
- `True/False` con mayuscula
- `f"texto {variable}"` para strings con variables
- `/` siempre da decimales, `//` es division entera

---

[[03_Practicas/semana-01]]
