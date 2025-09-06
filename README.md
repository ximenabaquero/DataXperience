# Análisis de Cobertura Celular y Condiciones Socioeconómicas en Colombia

## Descripción del Proyecto

Este proyecto realiza un análisis integral de la cobertura de telecomunicaciones móviles en Colombia y su relación con las condiciones socioeconómicas territoriales. Combina datos geográficos oficiales del DANE, información de cobertura móvil de operadores, y indicadores socioeconómicos para proporcionar insights sobre la brecha digital y equidad territorial en Colombia.

## Objetivos

### Objetivo Principal
Analizar la distribución territorial de la cobertura móvil en Colombia y su correlación con indicadores socioeconómicos para identificar brechas de conectividad y oportunidades de mejora en equidad digital.

### Objetivos Específicos
- Procesar y limpiar datos geográficos oficiales del DANE
- Analizar patrones de cobertura por operador móvil a nivel municipal
- Evaluar condiciones socioeconómicas territoriales
- Integrar datasets para análisis multidimensional
- Identificar municipios con brechas críticas de conectividad
- Desarrollar insights para políticas de inclusión digital

## Estructura del Proyecto

```
proyecto/
├── notebooks/
│   ├── 01_analisis_dane.ipynb           # Análisis datos geográficos DANE
│   ├── 02_analisis_psdata.ipynb         # Análisis cobertura móvil
│   ├── 03_analisis_socioeconomico.ipynb # Análisis condiciones de vida
│   └── 04_integracion_final.ipynb       # Análisis conjunto
├── data/
│   ├── raw/                             # Datos originales
│   │   ├── MGN2018_MPIO_POLITICO/       # Shapefile DANE
│   │   └── Condiciones de vida del hogar y tenencia de bienes/
│   └── processed/                       # Datos procesados
│       ├── municipios_dane_divipola_limpio.csv
│       ├── psdata_cobertura_agregado_municipios.csv
│       └── datos_socioeconomicos_agregado_municipios.csv
├── src/                                 # Código fuente reutilizable
├── results/                             # Resultados y visualizaciones
└── docs/                               # Documentación
```

## Datasets Utilizados

### 1. Datos Geográficos - DANE
- **Fuente**: Shapefile MGN_MPIO_POLITICO - DANE 2018
- **Descripción**: División político-administrativa de Colombia
- **Registros**: 1,122 municipios únicos (después de limpieza)
- **Variables clave**: Códigos DIVIPOLA, nombres de municipios y departamentos, áreas

### 2. Cobertura Móvil - PSData
- **Fuente**: API PSData Colombia
- **Descripción**: Datos de cobertura por operador móvil
- **Operadores**: Claro, Movistar, Tigo, WOM
- **Variables clave**: Área de cobertura por operador, índices agregados

### 3. Condiciones Socioeconómicas
- **Fuente**: Encuesta de condiciones de vida del hogar y tenencia de bienes
- **Registros**: 86,405 registros procesados
- **Dimensiones**: Vivienda, bienes, educación, salud, tecnología, demografía, economía

## Metodología

### Fase 1: Procesamiento Individual de Datasets

#### DANE - Datos Geográficos
1. **Carga y exploración** de shapefiles
2. **Limpieza** de códigos DIVIPOLA y nombres geográficos
3. **Resolución de duplicados** (60 códigos duplicados identificados y corregidos)
4. **Estandarización** de nombres para integración
5. **Validación** de integridad territorial

#### PSData - Cobertura Móvil
1. **Descarga automatizada** vía API con paginación
2. **Limpieza** de variables de cobertura (conversión a valores numéricos)
3. **Análisis por operador** y métricas comparativas
4. **Agregación por municipio** para análisis territorial
5. **Detección de outliers** y validación de datos

#### Datos Socioeconómicos
1. **Identificación automática** de variables por categorías:
   - Geográficas, demográficas, económicas
   - Vivienda, educación, salud, tecnología, bienes
2. **Limpieza y conversión** de tipos de datos
3. **Creación de índices** compuestos (bienes, económico)
4. **Agregación municipal** con promedios ponderados

### Fase 2: Integración y Análisis Conjunto
1. **Merge por municipio** usando nombres estandarizados
2. **Análisis de correlaciones** entre variables
3. **Identificación de brechas** territoriales
4. **Modelado predictivo** (en desarrollo)

## Archivos de Datos Procesados

### municipios_dane_divipola_limpio.csv
- **Descripción**: Base territorial limpia y validada
- **Registros**: 1,122 municipios
- **Uso**: Referencia geográfica oficial para todos los análisis

### psdata_cobertura_agregado_municipios.csv
- **Descripción**: Datos de cobertura móvil agregados por municipio
- **Variables**: Cobertura por operador, índices de conectividad
- **Uso**: Análisis de brecha digital territorial

### datos_socioeconomicos_agregado_municipios.csv
- **Descripción**: Indicadores socioeconómicos municipales
- **Variables**: Índices de bienes, condiciones de vivienda, acceso a servicios
- **Uso**: Análisis de equidad territorial y desarrollo

## Principales Hallazgos

### Calidad de Datos
- **DANE**: Excelente calidad (100% completitud post-limpieza)
- **PSData**: Buena calidad (>85% completitud promedio)
- **Socioeconómicos**: Buena calidad (>80% completitud variables clave)

### Cobertura Territorial
- **Total municipios con datos**: Más de 1,000 municipios analizados
- **Operadores analizados**: 4 operadores principales
- **Brechas identificadas**: Diferencias significativas entre operadores y regiones

### Análisis Socioeconómico
- **Variables categorizadas**: 8 dimensiones socioeconómicas
- **Índices creados**: Índice de bienes, índice económico compuesto
- **Disparidades territoriales**: Identificadas entre municipios y regiones

## Tecnologías Utilizadas

### Librerías Python
- **Procesamiento**: pandas, numpy, geopandas
- **Visualización**: matplotlib, seaborn, plotly
- **Análisis estadístico**: scipy, scikit-learn
- **APIs**: requests para descarga PSData

### Herramientas
- **Jupyter Notebooks**: Análisis interactivo
- **Git**: Control de versiones
- **APIs REST**: Integración con PSData

## Instrucciones de Uso

### Requisitos
```bash
pip install pandas numpy matplotlib seaborn geopandas scipy requests plotly scikit-learn
```

### Ejecución
1. **Clonar repositorio** y configurar estructura de carpetas
2. **Descargar datos DANE** en `data/raw/MGN2018_MPIO_POLITICO/`
3. **Ejecutar notebooks en orden**:
   - `01_analisis_dane.ipynb`
   - `02_analisis_psdata.ipynb`
   - `03_analisis_socioeconomico.ipynb`
   - `04_integracion_final.ipynb` (próximamente)

### Configuración de Rutas
Actualizar rutas en los notebooks según tu sistema:
```python
# Ejemplo de configuración
ruta_shapefile = "C:/ruta/a/tus/datos/MGN_MPIO_POLITICO.shp"
ruta_socioeconomicos = "C:/ruta/a/condiciones-vida/"
```

## Resultados y Outputs

### Archivos Generados
- Datasets limpios y procesados en `data/processed/`
- Visualizaciones en `results/`
- Reportes de calidad de datos
- Matrices de correlación y análisis estadísticos

### Métricas de Calidad
- **Score de completitud**: >85% promedio
- **Consistencia territorial**: 100% (sin duplicados)
- **Validación cruzada**: Exitosa entre datasets

## Próximos Pasos

### Análisis Pendientes
1. **Notebook de integración final**: Combinar los 3 datasets
2. **Modelado predictivo**: Predicción de cobertura basada en variables socioeconómicas
3. **Análisis de clustering**: Segmentación de municipios por perfiles
4. **Dashboard interactivo**: Visualización web de resultados

### Mejoras Técnicas
1. **Automatización**: Pipeline completo de procesamiento
2. **Validación temporal**: Análisis de series de tiempo
3. **Geolocalización avanzada**: Mapas interactivos
4. **API propia**: Servicio de consulta de datos procesados

## Limitaciones y Consideraciones

### Limitaciones de Datos
- **Temporalidad**: Datos de diferentes períodos
- **Granularidad**: Análisis a nivel municipal (no inframunicipal)
- **Cobertura rural**: Posible subrepresentación de áreas rurales

### Consideraciones Metodológicas
- **Agregación**: Promedios municipales pueden ocultar variabilidad interna
- **Correlación vs causalidad**: Análisis principalmente correlacional
- **Datos faltantes**: Manejados con técnicas de imputación y exclusión

## Autores y Contribuciones

- **Edwin, Ximena**: Desarrollo principal, análisis de datos
- **Institución**: EAN - DataXperience
- **Fecha**: 2024

## Licencia y Uso

Este proyecto se desarrolla con fines académicos y de investigación. Los datos utilizados provienen de fuentes públicas oficiales (DANE, PSData) y se procesan siguiendo mejores prácticas de ciencia de datos.

## Referencias

- **DANE**: Departamento Administrativo Nacional de Estadística
- **PSData**: Portal de Datos Abiertos del Gobierno de Colombia
- **Metodología**: Basada en estándares de ciencia de datos y análisis territorial

---

**Nota**: Este proyecto está en desarrollo activo. Para preguntas o colaboraciones, contactar a los autores.
