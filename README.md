1. Importación de Librerías y LimpiezaEn esta parte, preparamos el entorno de trabajo.
```python
Pythonimport bpy
import math

# Limpiar escena

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```
- import bpy: Importa la librería de Blender para poder crear objetos, moverlos, etc.import math: Necesaria para usar funciones matemáticas como el seno (sin), coseno (cos) y la conversión a radianes.
- Limpieza: Estas líneas seleccionan todo lo que haya en la escena actual y lo borran para que el script empiece desde cero cada vez que lo ejecutes.

2. Configuración de Parámetros
Aquí definimos las "reglas" de nuestra figura.
```Python
radio = 3
- angulo_actual = 0
paso_angular = 30 # Define la separación entre cada círculo
```
- radio: El tamaño de los círculos.
- paso_angular: Es el ángulo que saltamos para poner el siguiente círculo. Si pones 60°, obtendrás 6 círculos alrededor; con 30° como está aquí, obtendrás 12.3.

3. El Círculo Central y los Primeros Pasos
Antes de automatizar, el código coloca el centro y los primeros dos pétalos manualmente.

```Python
# 1. Círculo Central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

# Círculo 1 (Manual)
x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)
```
Trigonometría: Para saber dónde poner el círculo, usamos las fórmulas:
- x = radio*cos(0)
- y = radio sin(0)
- math.radians: Es vital porque las funciones cos y sin no entienden "grados" (0-360), sino "radianes".

4. Automatización con el Ciclo while

Esta es la parte más eficiente. En lugar de escribir el código 12 veces, le pedimos a la computadora que lo repita hasta dar la vuelta completa (360°).
```Python 
while angulo_actual < 360:
    x = radio * math.cos(math.radians(angulo_actual)) 
    y = radio * math.sin(math.radians(angulo_actual))
    bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x, y, 0), vertices=64)
    
    # Incremento: ¡Súper importante para no crear un bucle infinito!
    angulo_actual += paso_angular
```
- while angulo_actual < 360: "Mientras no hayamos completado el círculo, sigue haciendo esto".
- angulo_actual += paso_angular: En cada vuelta del ciclo, sumamos 30 grados a la posición. Así, el siguiente círculo se moverá un poco más en la circunferencia.
