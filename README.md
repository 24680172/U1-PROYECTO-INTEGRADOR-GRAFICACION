# Pasillo Procedural Curvo en Blender

Generador procedural de un pasillo 3D curvo con animación automática usando Python en Blender.
Este proyecto demuestra cómo crear entornos 3D automáticamente mediante código, sin modelado manual.

---

## Descripción

El script crea de forma automática:

* Paredes con variación procedural
* Materiales generados por código
* Suelo continuo
* Cámara animada
* Escena lista para render

Todo el entorno se genera al ejecutar el script.

---

## Requisitos

* Blender 3.x o superior
* Python (incluido en Blender)

---

## Instalación

1. Clonar el repositorio:

```bash
git clone https://github.com/tu_usuario/pasillo-procedural-blender.git
```

2. Abrir Blender
3. Ir a la pestaña Scripting
4. Abrir el archivo:

```bash
src/pasillo_procedural.py
```

5. Ejecutar el script
6. Presionar Play para ver la animación

---

## Explicación del código

### 1. Importación de librerías

```python
import bpy
import math
```

* `bpy` permite controlar Blender desde Python.
* `math` se usa para funciones trigonométricas y generación de curvas.

---

### 2. Creación de materiales

La función:

```python
def crear_material(nombre, color_rgb):
```

Se encarga de:

* Crear materiales automáticamente.
* Ajustar el color base.
* Evitar duplicación de código.

Esto permite modificar la apariencia del entorno de forma rápida.

---

### 3. Limpieza de la escena

Antes de generar el pasillo, el script elimina todos los objetos:

```python
bpy.ops.object.select_all(action="SELECT")
bpy.ops.object.delete()
```

Esto asegura que la escena esté limpia si el script se ejecuta varias veces.

---

### 4. Parámetros principales

```python
ancho = 3.0
paso = 3.0
total_bloques = 60
altura_pared = 3.0
grosor_pared = 1.0
```

Estos valores controlan:

* El tamaño del pasillo.
* Su longitud.
* La escala general.

Se pueden modificar fácilmente para generar distintos entornos.

---

### 5. Curvatura procedural

La función:

```python
def offset_x(i):
```

Desplaza cada bloque del pasillo lateralmente.
Se utiliza una función coseno para crear curvas suaves, evitando cambios bruscos de dirección.

Esto mejora:

* La continuidad visual.
* El realismo.
* La calidad de la animación.

---

### 6. Orientación del pasillo

```python
def angulo_tangente(i):
```

Calcula el ángulo de cada sección usando la tangente de la curva.
Esto permite:

* Rotar correctamente las paredes.
* Mantener la coherencia de la geometría.
* Orientar la cámara.

---

### 7. Creación de paredes

El script crea cubos para cada sección:

* Escala los objetos.
* Los rota según la curva.
* Alterna materiales para mejorar el detalle.

Esto genera un entorno más variado.

---

### 8. Suelo procedural

En lugar de utilizar cubos, el suelo se crea como una malla continua:

```python
mesh.from_pydata(verts, [], faces)
```

Ventajas:

* Mejor rendimiento.
* Superficie continua.
* Mayor control.

---

### 9. Animación de la cámara

El script:

* Crea una cámara.
* Inserta keyframes automáticamente.
* Suaviza la interpolación.

Esto genera un recorrido automático por el pasillo.

---

### 10. Configuración de render

Se configuran:

* FPS
* Resolución
* Duración de la animación.

Esto permite obtener una previsualización rápida.

---

## Personalización

Puedes modificar:

| Parámetro     | Descripción             |
| ------------- | ----------------------- |
| ancho         | Ancho del pasillo       |
| paso          | Distancia entre bloques |
| total_bloques | Longitud                |
| altura_pared  | Altura                  |
| grosor_pared  | Grosor                  |

---

