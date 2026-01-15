# POO - Programación Orientada a Objetos

## ¿Qué es la Programación Orientada a Objetos?

La **Programación Orientada a Objetos (POO)** es un paradigma de programación que organiza el diseño de software alrededor de **objetos** en lugar de funciones y lógica. Un objeto es una entidad que combina datos (atributos) y comportamientos (métodos) relacionados en una sola unidad.

En lugar de pensar en un programa como una secuencia de instrucciones, la POO nos permite pensar en términos de objetos que interactúan entre sí, similar a cómo funcionan los objetos en el mundo real.

## Los Cuatro Pilares de la POO

### 1. **Encapsulamiento** 🔒

El encapsulamiento es el principio de ocultar los detalles internos de un objeto y exponer solo lo necesario. Esto se logra mediante:

- **Atributos privados**: Datos internos protegidos del acceso directo
- **Métodos públicos**: Interfaz para interactuar con el objeto

**Ejemplo en Python:**
```python
class CuentaBancaria:
    def __init__(self, titular, saldo_inicial):
        self.titular = titular
        self.__saldo = saldo_inicial  # Atributo privado
    
    def depositar(self, cantidad):
        if cantidad > 0:
            self.__saldo += cantidad
            return True
        return False
    
    def obtener_saldo(self):
        return self.__saldo

# Uso
cuenta = CuentaBancaria("María", 1000)
cuenta.depositar(500)
print(f"Saldo: ${cuenta.obtener_saldo()}")  # Saldo: $1500
```

**Beneficios:**
- Protege la integridad de los datos
- Facilita el mantenimiento del código
- Reduce el acoplamiento entre componentes

### 2. **Herencia** 👨‍👩‍👧‍👦

La herencia permite crear nuevas clases basadas en clases existentes, heredando sus atributos y métodos. Esto promueve la reutilización de código.

**Ejemplo en Python:**
```python
class Animal:
    def __init__(self, nombre):
        self.nombre = nombre
    
    def hacer_sonido(self):
        pass

class Perro(Animal):  # Perro hereda de Animal
    def hacer_sonido(self):
        return "¡Guau guau!"

class Gato(Animal):  # Gato hereda de Animal
    def hacer_sonido(self):
        return "¡Miau!"

# Uso
mi_perro = Perro("Toby")
mi_gato = Gato("Whiskers")
print(f"{mi_perro.nombre} dice: {mi_perro.hacer_sonido()}")
print(f"{mi_gato.nombre} dice: {mi_gato.hacer_sonido()}")
```

**Beneficios:**
- Reutilización de código
- Jerarquía natural de clases
- Facilita la extensibilidad

### 3. **Polimorfismo** 🎭

El polimorfismo permite que objetos de diferentes clases sean tratados como objetos de una clase común. Un mismo método puede comportarse de manera diferente según el objeto que lo invoque.

**Ejemplo en Python:**
```python
import math

class Figura:
    def area(self):
        pass

class Circulo(Figura):
    def __init__(self, radio):
        self.radio = radio
    
    def area(self):
        return math.pi * self.radio ** 2

class Rectangulo(Figura):
    def __init__(self, base, altura):
        self.base = base
        self.altura = altura
    
    def area(self):
        return self.base * self.altura

# Polimorfismo en acción
figuras = [Circulo(5), Rectangulo(4, 6), Circulo(3)]

for figura in figuras:
    print(f"Área: {figura.area():.2f}")
```

**Beneficios:**
- Código más flexible y extensible
- Interfaces consistentes
- Facilita el diseño de sistemas modulares

### 4. **Abstracción** 🎨

La abstracción consiste en modelar las características esenciales de un objeto, ignorando los detalles irrelevantes. Se enfoca en **qué hace** un objeto, no en **cómo lo hace**.

**Ejemplo en Python:**
```python
# ABC (Abstract Base Class) permite crear clases abstractas
# abstractmethod marca métodos que deben ser implementados por las subclases
from abc import ABC, abstractmethod

class Vehiculo(ABC):  # Clase abstracta
    @abstractmethod
    def arrancar(self):
        pass
    
    @abstractmethod
    def detener(self):
        pass

class Coche(Vehiculo):
    def arrancar(self):
        return "El coche arranca con llave"
    
    def detener(self):
        return "El coche se detiene con el freno"

class Bicicleta(Vehiculo):
    def arrancar(self):
        return "La bicicleta arranca pedaleando"
    
    def detener(self):
        return "La bicicleta se detiene con los frenos de mano"

# Uso
vehiculos = [Coche(), Bicicleta()]
for v in vehiculos:
    print(v.arrancar())
    print(v.detener())
```

**Beneficios:**
- Simplifica la complejidad
- Enfoque en lo esencial
- Mejora la comprensión del código

## Ventajas de la POO

1. **Modularidad**: El código se organiza en unidades independientes (objetos)
2. **Reutilización**: Las clases pueden usarse en diferentes partes del programa
3. **Mantenibilidad**: Es más fácil encontrar y corregir errores
4. **Escalabilidad**: Facilita la expansión del sistema
5. **Modelado natural**: Representa mejor situaciones del mundo real
6. **Colaboración**: Equipos pueden trabajar en diferentes clases simultáneamente

## Ejemplos del Mundo Real

### Sistema de Biblioteca
```python
class Libro:
    def __init__(self, titulo, autor, isbn):
        self.titulo = titulo
        self.autor = autor
        self.isbn = isbn
        self.disponible = True
    
    def prestar(self):
        if self.disponible:
            self.disponible = False
            return True
        return False
    
    def devolver(self):
        self.disponible = True

class Usuario:
    def __init__(self, nombre, id_usuario):
        self.nombre = nombre
        self.id_usuario = id_usuario
        self.libros_prestados = []
    
    def tomar_prestado(self, libro):
        if libro.prestar():
            self.libros_prestados.append(libro)
            return f"{self.nombre} ha tomado prestado '{libro.titulo}'"
        return f"'{libro.titulo}' no está disponible"

# Uso del sistema
libro1 = Libro("Cien Años de Soledad", "Gabriel García Márquez", "978-0307474728")
usuario1 = Usuario("Carlos", "U001")
print(usuario1.tomar_prestado(libro1))
```

### Sistema de Tienda Online
```python
class Producto:
    def __init__(self, nombre, precio, stock):
        self.nombre = nombre
        self.precio = precio
        self.stock = stock
    
    def esta_disponible(self, cantidad):
        return self.stock >= cantidad

class CarritoCompras:
    def __init__(self):
        self.items = []
    
    def agregar_producto(self, producto, cantidad):
        if producto.esta_disponible(cantidad):
            self.items.append({'producto': producto, 'cantidad': cantidad})
            return True
        return False
    
    def calcular_total(self):
        total = 0
        for item in self.items:
            total += item['producto'].precio * item['cantidad']
        return total

# Uso
laptop = Producto("Laptop Dell", 899.99, 5)
carrito = CarritoCompras()
carrito.agregar_producto(laptop, 1)
print(f"Total a pagar: ${carrito.calcular_total()}")
```

## Conceptos Importantes

### Clases vs Objetos

- **Clase**: Es el plano o plantilla que define las características y comportamientos
- **Objeto**: Es una instancia concreta de una clase

```python
# Clase: El plano
class Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad

# Objetos: Instancias concretas
persona1 = Persona("Ana", 25)
persona2 = Persona("Luis", 30)
```

### Constructor

El constructor (`__init__` en Python) es un método especial que se ejecuta automáticamente cuando se crea un objeto.

```python
class Coche:
    def __init__(self, marca, modelo, año):
        # Este código se ejecuta al crear el objeto
        self.marca = marca
        self.modelo = modelo
        self.año = año
        print(f"Coche creado: {marca} {modelo}")

# Al crear el objeto, el constructor se ejecuta automáticamente
mi_coche = Coche("Toyota", "Corolla", 2024)
# Salida: Coche creado: Toyota Corolla
```

### Métodos

Son funciones definidas dentro de una clase que determinan el comportamiento de los objetos.

## Lenguajes que Soportan POO

- **Python** 🐍
- **Java** ☕
- **C++** 
- **C#** 
- **Ruby** 💎
- **JavaScript** 
- **PHP** 
- **Swift** 
- **Kotlin**

## Conclusión

La Programación Orientada a Objetos es un paradigma poderoso que ayuda a:

- ✅ Escribir código más organizado y mantenible
- ✅ Modelar problemas del mundo real de manera natural
- ✅ Reutilizar código eficientemente
- ✅ Trabajar en equipo de manera más efectiva
- ✅ Crear aplicaciones escalables y robustas

La POO no es solo una técnica de programación, es una forma de **pensar y diseñar soluciones** que refleja cómo entendemos el mundo que nos rodea.

---

**¿Listo para empezar a programar con POO?** 🚀

Comienza practicando con pequeños proyectos, identificando objetos del mundo real y modelándolos en código. ¡La práctica hace al maestro!