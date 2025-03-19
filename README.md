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

2. Instalar las Bibliotecas
El script requiere las bibliotecas pandas y numpy. Para instalarlas, sigue estos pasos:

Abre una terminal (cmd, PowerShell, bash, etc.).

Ejecuta el siguiente comando para instalar las bibliotecas:
pip install pandas numpy

Ejecución del Script

1. Preparación del Archivo de Datos
Asegúrate de tener el archivo datos_predio.csv en el mismo directorio donde se encuentra el script. Este archivo debe contener los datos de los predios con las columnas Area Geografica y Area Registral.

2. Guardar el Script
Copia el siguiente código y guárdalo en un archivo con extensión .py, por ejemplo, validador_areas.py:

import pandas as pd
import numpy as np  # Para usar NaN

# Leer el archivo CSV con el delimitador correcto
df = pd.read_csv('datos_predio.csv', delimiter=';', encoding='latin1')

# Filtrar los predios donde 'Area Geografica' sea mayor a 0
df = df[df['Area Geografica'] > 0]

# Función para calcular la diferencia entre las áreas
def calcular_diferencia(row):
    area_geografica = row['Area Geografica']
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver NaN (o un mensaje)
    if area_registral == 0:
        return np.nan  # O puedes usar "Área Registral inválida"
    
    # Calcular la diferencia absoluta entre las áreas
    diferencia = abs(area_geografica - area_registral)
    
    return round(diferencia, 2)  # Redondear a 2 decimales

# Función para calcular el porcentaje de diferencia usando Área Geográfica como referencia
def calcular_porcentaje_diferencia_geografica(row):
    area_geografica = row['Area Geografica']
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver NaN (o un mensaje)
    if area_registral == 0:
        return np.nan  # O puedes usar "Área Registral inválida"
    
    # Calcular la diferencia absoluta y el porcentaje
    diferencia = abs(area_geografica - area_registral)
    porcentaje_diferencia = (diferencia / area_geografica) * 100
    
    return round(porcentaje_diferencia, 2)  # Redondear a 2 decimales

# Función para calcular el porcentaje de diferencia usando Área Registral como referencia
def calcular_porcentaje_diferencia_registral(row):
    area_geografica = row['Area Geografica']
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver NaN (o un mensaje)
    if area_registral == 0:
        return np.nan  # O puedes usar "Área Registral inválida"
    
    # Calcular la diferencia absoluta y el porcentaje
    diferencia = abs(area_registral - area_geografica)
    porcentaje_diferencia = (diferencia / area_registral) * 100
    
    return round(porcentaje_diferencia, 2)  # Redondear a 2 decimales

# Función para calcular el límite de tolerancia usando Área Geográfica como referencia
def calcular_limite_tolerancia_geografica(row):
    area_geografica = row['Area Geografica']
    
    # Determinar el porcentaje de tolerancia según el rango del Área Geográfica
    if 2000 < area_geografica <= 10000:
        tolerancia = 0.09
    elif 10000 < area_geografica <= 100000:
        tolerancia = 0.07
    elif 100000 < area_geografica <= 500000:
        tolerancia = 0.04
    elif area_geografica > 500000:
        tolerancia = 0.02
    else:
        return np.nan  # Para áreas menores o iguales a 2000 m2
    
    # Calcular el límite de tolerancia permitido
    limite_tolerancia = area_geografica * tolerancia
    
    return round(limite_tolerancia, 2)  # Redondear a 2 decimales

# Función para calcular el límite de tolerancia usando Área Registral como referencia
def calcular_limite_tolerancia_registral(row):
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver NaN (o un mensaje)
    if area_registral == 0:
        return np.nan  # O puedes usar "Área Registral inválida"
    
    # Determinar el porcentaje de tolerancia según el rango del Área Registral
    if 2000 < area_registral <= 10000:
        tolerancia = 0.09
    elif 10000 < area_registral <= 100000:
        tolerancia = 0.07
    elif 100000 < area_registral <= 500000:
        tolerancia = 0.04
    elif area_registral > 500000:
        tolerancia = 0.02
    else:
        return np.nan  # Para áreas menores o iguales a 2000 m2
    
    # Calcular el límite de tolerancia permitido
    limite_tolerancia = area_registral * tolerancia
    
    return round(limite_tolerancia, 2)  # Redondear a 2 decimales

# Función para validar la tolerancia usando Área Geográfica como referencia
def validar_tolerancia_geografica(row):
    area_geografica = row['Area Geografica']
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver un mensaje especial
    if area_registral == 0:
        return "Area Registral igual a 0"
    
    # Calcular la diferencia absoluta entre las áreas
    diferencia = abs(area_geografica - area_registral)
    
    # Determinar el porcentaje de tolerancia según el rango del Área Geográfica
    if 2000 < area_geografica <= 10000:
        tolerancia = 0.09
    elif 10000 < area_geografica <= 100000:
        tolerancia = 0.07
    elif 100000 < area_geografica <= 500000:
        tolerancia = 0.04
    elif area_geografica > 500000:
        tolerancia = 0.02
    else:
        return "Fuera de rango"  # Para áreas menores o iguales a 2000 m2
    
    # Calcular el límite de tolerancia permitido
    limite_tolerancia = area_geografica * tolerancia
    
    # Validar si la diferencia está dentro del límite de tolerancia
    if diferencia <= limite_tolerancia:
        return "Dentro de tolerancia"
    else:
        return "Fuera de tolerancia"

# Función para validar la tolerancia usando Área Registral como referencia
def validar_tolerancia_registral(row):
    area_geografica = row['Area Geografica']
    area_registral = row['Area Registral']
    
    # Si el Área Registral es 0, devolver un mensaje especial
    if area_registral == 0:
        return "Area Registral igual a 0"
    
    # Calcular la diferencia absoluta entre las áreas
    diferencia = abs(area_registral - area_geografica)
    
    # Determinar el porcentaje de tolerancia según el rango del Área Registral
    if 2000 < area_registral <= 10000:
        tolerancia = 0.09
    elif 10000 < area_registral <= 100000:
        tolerancia = 0.07
    elif 100000 < area_registral <= 500000:
        tolerancia = 0.04
    elif area_registral > 500000:
        tolerancia = 0.02
    else:
        return "Fuera de rango"  # Para áreas menores o iguales a 2000 m2
    
    # Calcular el límite de tolerancia permitido
    limite_tolerancia = area_registral * tolerancia
    
    # Validar si la diferencia está dentro del límite de tolerancia
    if diferencia <= limite_tolerancia:
        return "Dentro de tolerancia"
    else:
        return "Fuera de tolerancia"

# Aplicar las funciones para calcular la diferencia, porcentajes, límites y validar la tolerancia
df['Diferencia'] = df.apply(calcular_diferencia, axis=1)
df['Porcentaje Diferencia (Area Geografica)'] = df.apply(calcular_porcentaje_diferencia_geografica, axis=1)
df['Porcentaje Diferencia (Area Registral)'] = df.apply(calcular_porcentaje_diferencia_registral, axis=1)
df['Limite Tolerancia (Area Geografica)'] = df.apply(calcular_limite_tolerancia_geografica, axis=1)
df['Limite Tolerancia (Area Registral)'] = df.apply(calcular_limite_tolerancia_registral, axis=1)
df['Validador Tolerancia (Area Geografica)'] = df.apply(validar_tolerancia_geografica, axis=1)
df['Validador Tolerancia (Area Registral)'] = df.apply(validar_tolerancia_registral, axis=1)

# Guardar el DataFrame con las nuevas columnas en un nuevo archivo CSV (opcional)
df.to_csv('datos_predio_con_diferencias_porcentajes_limites_y_validaciones_v6.csv', index=False)

# Mostrar el DataFrame resultante
print(df)

3. Ejecutar el Script
Abre una terminal y navega al directorio donde guardaste el script y el archivo datos_predio.csv.

Ejecuta el script con el siguiente comando:
python validador_areas.py

Resultados
El script generará un archivo CSV llamado datos_predio_con_diferencias_porcentajes_limites_y_validaciones_v6.csv en el mismo directorio.

Este archivo contendrá las columnas adicionales con los resultados de los cálculos.

El script también mostrará el DataFrame resultante en la consola.

Ejemplo de Uso
Si tienes un archivo datos_predio.csv con las columnas Area Geografica y Area Registral, el script calculará:

Diferencias absolutas.

Porcentajes de diferencia.

Límites de tolerancia.

Validación de tolerancia.

El archivo generado contendrá todas estas columnas adicionales.

¡Listo! Con esta guía, cualquier usuario podrá instalar y ejecutar el script sin problemas. 😊

