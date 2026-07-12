# Web Scraping: ENDES 2004–2025 <a id='a'></a>

Este proyecto en **Stata** proporciona una solución automatizada para descargar, organizar y procesar la **Encuesta Demográfica y de Salud Familiar (ENDES)** del Perú a partir del portal [**Microdatos**](https://proyectos.inei.gob.pe/microdatos/) del **Instituto Nacional de Estadística e Informática (INEI)**. El script permite obtener la información disponible para todos los años comprendidos entre **2004 y 2025**.

El objetivo principal es automatizar la descarga de todos los módulos de la encuesta directamente desde los servidores oficiales del INEI. Además, el script descomprime automáticamente los archivos en formato **`.zip`**, lo que permite construir un flujo de trabajo eficiente, reproducible y fácilmente actualizable para el procesamiento de los microdatos. En aquellos casos en que los archivos comprimidos presenten errores o inconsistencias, el script conserva el archivo descargado y notifica al usuario que la extracción deberá realizarse manualmente.

El proceso sigue una estructura jerárquica de iteración, recorriendo primero los **años de la encuesta** (identificados mediante el **Código de Encuesta**) y, posteriormente, los **módulos** (identificados mediante el **Código de Módulo**). Esta estructura facilita la descarga masiva de la información y permite personalizar fácilmente los años o módulos que se desean procesar.

Con el propósito de garantizar la reproducibilidad, la trazabilidad y el mantenimiento del proyecto, el código se gestiona mediante **Git** y se encuentra alojado en **GitHub**, lo que facilita el control de versiones, la documentación de los cambios y la colaboración con otros usuarios.

## Contenido
1. [**Requisitos**](#1)
2. [**Instalación y uso**](#2)
3. [**Módulos disponibles**](#4)
4. [**Funcionamiento del script**](#5)
5. [**Resultado**](#6)
6. [**Observaciones**](#7)
___

## 1. Requisitos ⚙️ <a id='1'></a>
Para ejecutar este proyecto únicamente se requiere:
- **Stata 16** o superior.
- Permisos de escritura en el directorio donde se almacenarán los archivos descargados.
- **Git** (opcional), para clonar el repositorio.

## 2. Instalación y uso 🚀 <a id='2'></a>

### 2.1. Clonar el repositorio

1. Abrir una terminal o línea de comandos Git Bash.

2. Ejecutar el siguiente comando para clonar el repositorio en tu máquina local:
```bash
git clone https://github.com/CarloEduardo/02-Web-Scraping-ENDES-2004-2025.git
```
3. Establecer como directorio de trabajo la carpeta clonada.
```
cd \E:\07. GitHub\02-Web-Scraping-ENDES-2004-2025\
```

### 2.1. Uso

1. Abrir el archivo 
```bash
Download-ENDES-2004-2025.do
```

2. Modificar la ruta donde se almacenarán los archivos descargados.
```stata
global Path = "E:\07. GitHub\02-Web-Scraping-ENDES-2004-2025"
```

3. Si lo deseas, modificar el rango de años:
```stata
local y_start = 4
local y_end   = 25
```

4. Seleccionar los módulos que deseas descargar:
```stata
foreach j in 1 2 3 4 5 {
```

5. Ejecutar el script.

## 3. Módulos disponibles <a id="3"></a>
___
<table>
<thead><tr>
<th><strong>Nro</strong></th>
<th><strong>Módulo</strong></th>
<th><strong>Descripción</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>Módulo 1629</td>
<td>Caracteristicas del Hogar</td>
</tr>
<tr>
<td>2</td>
<td>Módulo 1630</td>
<td>Caracteristicas de la Vivienda</td>
</tr>
<tr>
<td>3</td>
<td>Módulo 1631</td>
<td>Datos Basicos de MEF	</td>
</tr>
<tr>
<td>4</td>
<td>Módulo 1632</td>
<td>Historia de Nacimiento - Tabla de Conocimiento de Metodo</td>
</tr>
<tr>
<td>5</td>
<td>Módulo 1633</td>
<td>Embarazo, Parto, Puerperio y Lactancia</td>
</tr>
<tr>
<td>6</td>
<td>Módulo 1634</td>
<td>Inmunización y Salud</td>
</tr>
<tr>
<td>7</td>
<td>Módulo 1635</td>
<td>Nupcialidad - Fecundidad - Cónyugue y Mujer</td>
</tr>
<tr>
<td>8</td>
<td>Módulo 1636</td>
<td>Conocimiento de Sida y uso del condón</td>
</tr>
<tr>
<td>9</td>
<td>Módulo 1637</td>
<td>Mortalidad Materna - Violencia Familiar</td>
</tr>
<tr>
<td>10</td>
<td>Módulo 1638</td>
<td>Peso y talla - Anemia</td>
</tr>
<tr>
<td>11</td>
<td>Módulo 1639</td>
<td>Disciplina Infantil</td>
</tr>
<tr>
<td>12</td>
<td>Módulo 1640</td>
<td>Encuesta de salud</td>
</tr>
<tr>
<td>13</td>
<td>Módulo 1641</td>
<td>Programas Sociales</td>
</tr>
</tbody>
</table>

## 4. Funcionamiento del script <a id="4"></a>
El script realiza automáticamente las siguientes tareas:

1. Crea la estructura de carpetas del proyecto.
2. Recorre los años seleccionados.
3. Obtiene el Código de Encuesta correspondiente a cada año.
4. Recorre los módulos seleccionados.
5. Descarga cada archivo ZIP desde el portal oficial del INEI.
6. Descomprime automáticamente cada archivo.
7. Conserva el archivo ZIP cuando ocurre un error durante la extracción.

El proceso completo puede resumirse mediante el siguiente flujo:


El siguiente diagrama resume el flujo de ejecución del script para descargar y extraer automáticamente los módulos de la **Encuesta Demográfica y de Salud Familiar (ENDES)**:

```mermaid
---
title: Flujo del proceso de descarga y extracción de la ENDES (2004–2025)
---
flowchart TD

A([Inicio]) --> B[Definir directorio de trabajo]
B --> C[Crear carpeta principal ENDES]
C --> D{{Iterar por años<br/>2004–2025}}
D --> E[Obtener Código de Encuesta]
E --> F{{Iterar por módulos}}
F --> G[Construir URL de descarga]
G --> H[Descargar archivo ZIP]
H --> I[Descomprimir archivo ZIP]
I --> J{¿Extracción exitosa?}
J -- Sí --> K[Continuar con el siguiente módulo]
J -- No --> L[Conservar archivo ZIP<br/>Mostrar mensaje de extracción manual]
L --> K
K --> M{¿Quedan módulos?}
M -- Sí --> F
M -- No --> N{¿Quedan años?}
N -- Sí --> D
N -- No --> O([Fin])
```

*Elaboración propia.* <br>
***Nota:** El diagrama muestra el flujo de ejecución del script, incluyendo la iteración por años y módulos, la construcción de la URL de descarga, la obtención de los archivos desde el portal oficial del INEI y su extracción automática. En caso de que un archivo comprimido presente inconsistencias, el script conserva el archivo `.zip` y notifica al usuario que la extracción debe realizarse manualmente.*

## 5. Resultado 📂<a id="5"></a>
Al finalizar la ejecución se obtiene una estructura similar a la siguiente:

```text
ENDES/
│
├──2004/
│   ├── enaho01-2004.dta
│   ├── enaho02-2004.dta
│   └── ...
│
├──2005/
│
├──...
│
└──2025/
```
Cada carpeta contiene todos los módulos descargados y extraídos para el año correspondiente.

## 6. Observaciones ⚠️<a id="6"></a>
En algunos años, determinados archivos ZIP publicados por el INEI presentan inconsistencias que impiden su extracción automática mediante Stata.
Cuando esto ocurre, el script muestra un mensaje indicando que el archivo debe descomprimirse manualmente. El archivo ZIP descargado se conserva para facilitar este proceso.

## Licencia <a id="9"></a>
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](/LICENSE) para más detalles.

## Autor 👨‍💻<a id="10"></a>

**Carlos Eduardo Torres García**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/carlo4-eduardo-torres-garcia/)
[![X Twitter](https://img.shields.io/badge/Twitter-000000?style=flat&logo=x&logoColor=white)](https://x.com/Carlo4_Eduardo)

[**⬆ Volver al inicio**](#a)
