# Guía de Ejecución y Pruebas del Proyecto (Robot RRR en Plano XY)

Este documento explica los pasos necesarios para compilar y probar el espacio de trabajo de ROS 2 en un sistema Ubuntu.

## 1. Compilar el espacio de trabajo (Workspace)
Primero, abre una terminal, navega hacia la carpeta `robot_ws` que está dentro de la carpeta `ros`, y compila los paquetes de ROS 2.

Ejecuta los siguientes comandos:
```bash
# Navega hasta el espacio de trabajo 
cd ros/robot_ws/

# Compila el código del robot
colcon build
```

## 2. Cargar el entorno ("Sourcear")
Una vez que termine la compilación sin errores, necesitas indicarle a la terminal dónde están los nuevos archivos ejecutables del robot.

En la misma terminal (asegurándote de seguir en la carpeta `robot_ws`), ejecuta:
```bash
source install/setup.bash
```

## 3. Lanzar la Simulación y RViz
Ahora, iniciarás todos los nodos necesarios (el modelo del robot, la interfaz visual y el código de cinemática). Esto se hace ejecutando el archivo `launch` previamente configurado.

Ejecuta:
```bash
ros2 launch robot_bringup trajectory_bringup.launch.py
```
*(Al hacer esto, RViz se abrirá automáticamente mostrando la cuadrícula virtual y el robot en el centro).*

## 4. ¿Cómo ver la animación por click?
Una vez que tengas la ventana de RViz abierta con el robot a la vista:

1. En la barra superior de herramientas de RViz, busca un botón que dice **"Publish Point"** (suele tener el icono de una cruz o un pin).
2. Haz clic en el botón **Publish Point**.
3. Ahora, haz clic en cualquier lugar sobre el **suelo cuadriculado (Plano XY)** en RViz.
4. ¡Listo! El nodo de cinemática detectará las coordenadas (X, Y) de tu clic, calculará la cinemática inversa animada y enviará los ángulos a las juntas para mover el efector final (la punta del brazo) hasta ese punto.

*Nota: Cada vez que quieras mover el brazo a una nueva ubicación, debes volver a seleccionar la herramienta "Publish Point" en la barra superior y hacer clic en el nuevo destino.*
