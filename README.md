# Práctica 2 – Generación de patrón tipo Flor de Vida en Blender

## Objetivo
Generar un patrón circular utilizando scripting en Blender y explorar cómo la modificación de variables afecta el resultado geométrico.

---

# Primera versión – Distribución básica de círculos

## Descripción

En la primera versión se utilizó un paso fijo de 60 grados, lo que genera 6 círculos distribuidos uniformemente alrededor de un círculo central.

## Código utilizado

```python
import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

radio = 2
angulo_actual = 0
paso = 60  # separación fija de 60°

# Círculo central
bpy.ops.mesh.primitive_circle_add(
    radius=radio,
    location=(0, 0, 0)
)

while angulo_actual < 360:
    
    angulo_rad = math.radians(angulo_actual)
    
    x = radio * math.cos(angulo_rad)
    y = radio * math.sin(angulo_rad)
    
    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0)
    )
    
    angulo_actual += paso
```

## Resultado

Se generan 6 círculos alrededor del círculo central, formando una estructura simétrica básica.

<img width="1112" height="674" alt="image" src="https://github.com/user-attachments/assets/cc06b008-685d-4a24-aa7c-d9e3cafa85ef" />


---

# Segunda versión – Mayor cantidad de círculos

## Mejora aplicada

En la segunda versión se modificaron las variables para permitir una mayor cantidad de círculos distribuidos uniformemente.

Se añadió la variable `cantidad` y el paso se calculó automáticamente:

```python
radio = 5
cantidad = 27
paso = 360 / cantidad
```

Esto permite generar tantos círculos como se desee sin cambiar manualmente el ángulo.

## Código utilizado

```python
import bpy
import math

# --- Paso 1: Limpiar la escena ---
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete(use_global=False)

# --- Paso 2: Definición de variables ---
radio = 5          # Aumenté un poco el radio para que no se amontonen
cantidad = 27      # El número de círculos que quieres
paso = 360 / cantidad 

# --- Paso 3: Círculo base en el origen (Opcional) ---
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0))

# --- Paso 4: Ciclo para los círculos periféricos ---
angulo_actual = 0
while angulo_actual < 360:
    
    # Convertir ángulo a radianes
    angulo_rad = math.radians(angulo_actual)
    
    # Coordenadas cartesianas
    x = radio * math.cos(angulo_rad)
    y = radio * math.sin(angulo_rad)
    
    # Crear círculo en la nueva posición
    bpy.ops.mesh.primitive_circle_add(
        radius=radio, 
        location=(x, y, 0)
    )
    
    # Incrementar el ángulo
    angulo_actual += paso
```

## Resultado mejorado

Al aumentar la cantidad de círculos, el patrón se vuelve más complejo y visualmente más cercano a una Flor de Vida extendida.

<img width="1105" height="606" alt="image" src="https://github.com/user-attachments/assets/df4ef702-af37-486f-b570-8507abe2190f" />

---

## Conclusión

Este ejercicio demuestra cómo la modificación de parámetros en un script permite generar patrones geométricos más complejos de manera automática.

El uso de trigonometría y ciclos facilita la creación de estructuras repetitivas con control total sobre su distribución.
