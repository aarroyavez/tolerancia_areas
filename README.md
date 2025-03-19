# Validador de Áreas de Tolerancia

Este script valida las diferencias entre el Área Geográfica y el Área Registral de predios, calcula porcentajes de diferencia, límites de tolerancia y determina si las diferencias están dentro de los rangos permitidos.

---

## Requisitos

- **Python 3.6 o superior**: El script está escrito en Python, por lo que necesitas tener Python instalado en tu sistema.
- **Bibliotecas necesarias**: El script utiliza las bibliotecas `pandas` y `numpy`.

---

## Instalación

### 1. Instalar Python

Si no tienes Python instalado, sigue estos pasos:

#### En Windows:
1. Descarga Python desde [python.org](https://www.python.org/downloads/).
2. Ejecuta el instalador y asegúrate de marcar la opción **"Add Python to PATH"** antes de hacer clic en "Install Now".
3. Verifica la instalación abriendo una terminal (`cmd` o `PowerShell`) y ejecutando:
   ```bash
   python --version

4. Instala la librería pandas

         pip install pandas
   
Ejecución del Script


1. Preparación del Archivo de Datos
Asegúrate de tener el archivo datos_predio.csv en el mismo directorio donde se encuentra el script. Este archivo debe contener los datos de los predios con las columnas Area Geografica y Area Registral.

2. Guardar el Script
Abre en un editor de código el archivo .py llamado validacion_tolerancia_areas_v6.py

3. Ejecutar el Script

Abre una terminal y navega al directorio donde guardaste el script y el archivo datos_predio.csv.

Ejecuta el script con el siguiente comando:

      python validacion_tolerancia_areas_v6.py


Resultados


1. El script generará un archivo CSV llamado datos_predio_con_diferencias_porcentajes_limites_y_validaciones_v6.csv en el mismo directorio.
2. Este archivo contendrá las columnas adicionales con los resultados de los cálculos.
3. El script también mostrará el DataFrame resultante en la consola.


Ejemplo de Uso


Si tienes un archivo datos_predio.csv con las columnas Area Geografica y Area Registral, el script calculará:

1. Diferencias absolutas.
2. Porcentajes de diferencia.
3.Límites de tolerancia.
4. Validación de tolerancia.

El archivo generado contendrá todas estas columnas adicionales.

Este archivo `README.md` está listo para ser usado en tu repositorio. ¡Espero que te sea útil! 😊

