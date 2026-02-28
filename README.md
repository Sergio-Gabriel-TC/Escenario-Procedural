# Escenario-Procedural
Paso 1: Instalación de Blender
Para empezar, necesitamos el motor de renderizado. Blender es de código abierto, lo cual es genial para nosotros los desarrolladores.

Descarga: Ve al sitio oficial blender.org y descarga la versión estable más reciente para tu sistema operativo (Windows, macOS o Linux).

<img width="740" height="182" alt="image" src="https://github.com/user-attachments/assets/2d873c7d-e971-457f-8c66-ca3988bb8c61" />

<img width="1326" height="657" alt="image" src="https://github.com/user-attachments/assets/62bc6ac6-8050-44fd-807a-57b3e22fb867" />

<img width="1013" height="297" alt="image" src="https://github.com/user-attachments/assets/68b306e2-b0fe-4e84-8c58-20b402ca002c" />

Instalación: Ejecuta el instalador. En Windows, es el típico "Siguiente, Siguiente".


# Primer Inicio: Al abrirlo, te pedirá configurar el idioma y el teclado. Te recomiendo dejarlo en Inglés, ya que la mayoría de la documentación de la API bpy (Blender Python) está en ese idioma.

Paso 1: Localización del Editor de Texto
Blender no es solo un software de diseño; tiene un IDE de Python integrado.

Abre Blender (si ya tienes algo en la escena, no importa, el código lo borrará).

En la parte superior de la ventana, verás varias pestañas (Layout, Modeling, Sculpting, etc.). Haz clic en la que dice Scripting.

Tip: Si no la ves, dale al botón + al final de las pestañas, elige General y luego Scripting.

La interfaz cambiará. El área más grande en el centro es tu Editor de Texto.

Haz clic en el botón central que dice + New. Esto creará un archivo virtual llamado Text.py.

<img width="1576" height="972" alt="image" src="https://github.com/user-attachments/assets/b0242dc4-5809-45c1-93d2-0000aabcd644" />

<img width="1581" height="1029" alt="image" src="https://github.com/user-attachments/assets/3a744b19-5686-45ad-92d3-714b40727f89" />


# Paso 2: Colocación del Código Completo
Copia el siguiente bloque de código íntegro y pégalo en ese espacio en blanco que acabas de crear. Asegúrate de que la primera línea sea import bpy.

    import bpy
    import random

    def crear_material(nombre, color_rgb):
        # Crea un material básico con un color específico
        mat = bpy.data.materials.new(name=nombre)
        mat.diffuse_color = (*color_rgb, 1.0) # RGBA
        return mat

    def generar_escenario():
        # 1. Limpiar la escena previa
        bpy.ops.object.select_all(action='SELECT')
        bpy.ops.object.delete()

        # 2. Definir materiales (Basado en modelos de color RGB)
        mat_pared_a = crear_material("ParedOscura", (0.1, 0.1, 0.1))
        mat_pared_b = crear_material("ParedDetalle", (0.8, 0.2, 0.0)) # Un naranja rojizo

        # 3. Parámetros del escenario
        largo_pasillo = 10
        ancho_pasillo = 4

        # 4. Ciclo para construir paredes (Transformación: Traslación)
        for i in range(largo_pasillo):
            # Pared Izquierda
            bpy.ops.mesh.primitive_cube_add(location=(-ancho_pasillo, i * 2, 1))
            pared_izq = bpy.context.active_object

            # Aplicar material de forma alternada (Lógica de programación)
            if i % 2 == 0:
                pared_izq.data.materials.append(mat_pared_a)
            else:
                pared_izq.data.materials.append(mat_pared_b)
                 # Escalamiento para darle variedad visual
                pared_izq.scale.z = 1.5

            # Pared Derecha
            bpy.ops.mesh.primitive_cube_add(location=(ancho_pasillo, i * 2, 1))
            pared_der = bpy.context.active_object
            pared_der.data.materials.append(mat_pared_a)

        # 5. Agregar un suelo (Escalamiento y Posicionamiento)
        bpy.ops.mesh.primitive_plane_add(size=1, location=(0, (largo_pasillo - 1), 0))
        suelo = bpy.context.active_object
        suelo.scale.x = ancho_pasillo + 1
        suelo.scale.y = largo_pasillo + 1

generar_escenario()

generar_escenario()
# Paso 3: Ejecución y Validación
Dale Play: En la barra de herramientas del editor de texto, verás un icono de flecha hacia la derecha o el botón que dice Run Script. Presiónalo.

<img width="1570" height="971" alt="image" src="https://github.com/user-attachments/assets/ae137a43-e97b-418e-a4af-e70ee15ee1d5" />

Verificación Visual: Mira la ventana de la Vista 3D (arriba a la derecha). Debería aparecer el pasillo.

<img width="589" height="515" alt="image" src="https://github.com/user-attachments/assets/665fb514-18db-4f44-b565-09e90529d613" />




