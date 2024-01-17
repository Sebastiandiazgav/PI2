


** Rol a Desarrollar:

El rol asignado implica liderar y ejecutar un proyecto integral de análisis de datos para el Observatorio de Movilidad y Seguridad Vial (OMSV). El OMSV, en su función de recopilación y análisis de información, se basa principalmente en datos policiales, conforme a los estándares internacionales. Las estadísticas elaboradas se derivan de los sumarios proporcionados por la Policía de la Ciudad.

En el periodo comprendido entre 2010 y 2016, la información fue recopilada por la Comisión General de Comisarías. A partir de 2018, la Policía de la Ciudad, dependiente del Ministerio de Justicia y Seguridad del Gobierno de la Ciudad Autónoma de Buenos Aires (GCBA), comenzó a operar y se convirtió en la principal fuente de información para el Observatorio. Esto se debe a que abarca la totalidad del territorio y, por ende, proporciona una visión más integral de la movilidad y la seguridad vial en la ciudad.

La tarea específica solicitada consiste en desarrollar un proyecto de análisis de datos utilizando un dataset que contiene información sobre homicidios y siniestros viales ocurridos en la Ciudad de Buenos Aires durante el periodo 2016-2021. El objetivo primordial de este proyecto es generar información relevante que permita a las autoridades locales tomar medidas concretas para reducir la cantidad de víctimas fatales en los incidentes viales. Este análisis se realizará con un enfoque proactivo, buscando identificar patrones, tendencias y factores que contribuyan a la comprensión de los eventos y, en última instancia, faciliten la implementación de estrategias efectivas de prevención y seguridad vial.


# Proyecto de Análisis de Homicidios

Este proyecto tiene como objetivo realizar un análisis exploratorio de datos relacionados con homicidios. Inicialmente, se accedió a la información de homicidios, la cual se encontraba en un archivo en formato xlsx. Para facilitar el proceso, se abrió el archivo en Excel y se realizaron ajustes en algunos datos para asegurar una transición sin problemas al formato CSV.

A continuación, se llevó a cabo un proceso de ETL (Extract, Transform, Load) para transformar los datos y obtener una estructura limpia que facilitara el análisis. Los archivos xlsx fueron cargados y convertidos a formato CSV, creando dos archivos denominados "hechos.csv" y "victimas.csv". Se procedió a visualizar los datos para comprender la información contenida.

Posteriormente, se realizó una operación de fusión (merge) entre los dos conjuntos de datos utilizando las columnas relacionadas 'ID' y 'ID_hechos', generando un nuevo DataFrame denominado "df_combinado".

Se llevaron a cabo las siguientes operaciones de limpieza en el DataFrame resultante:
- Eliminación de las columnas: 'HORA', 'Calle', 'Altura', 'Cruce', 'XY (CABA)', 'Dirección Normalizada', 'ID_hecho', 'FECHA_y', 'AAAA_y', 'MM_y', 'DD_y', 'VICTIMA_y', 'FECHA_FALLECIMIENTO'.
- Cambio de tipos de datos para las columnas: 'N_VICTIMAS' a tipo 'int', 'FECHA_x' a tipo 'datatime', 'AAAA_x', 'MM_x', DD_x, 'HH', 'COMUNA', 'EDAD' a tipo 'int'.
- Conversión de las columnas 'pos x' y 'pos y' a tipo 'float'.

Se realizaron validaciones para detectar valores nulos, eliminando registros que contenían <NA>, 'MOTO-SD', 'SD-SD', 'AUTO-SD', 'PEATON-SD', 'SD-CARGAS', 'SD-AUTO', 'SD-MOTO', 'PASAJEROS-SD', 'SD', y 'nan'.

Finalmente, con los datos limpios y preparados, se exportó el nuevo DataFrame a un archivo CSV llamado "homicidio_df.csv" para su posterior uso en el análisis exploratorio.




## EDA (Exploratory Data Analysis)

En el proceso de análisis exploratorio de datos, se ha empleado la librería Pandas para cargar el nuevo DataFrame desde el archivo 'homicidios_df.csv'. Además, se ha  integrado la librería 'ydata_profiling' para realizar un análisis detallado de la base  base de datos en cuestion. 

Adicionalmente, con el objetivo de enriquecer el  análisis exploratorio de datos, se incorporado la librería 'dtale'. Se Invoca esta librería para proporcionarnos información adicional sobre los datos, puede acceder al documento en este apartado [EDA](https://drive.google.com/file/d/1jChuQuY1Ee_7ykh52j-mQUoChNRkPzdA/view?usp=sharing)




Si eres un desarrollador y deseas visualizar e interactuar con los datos, te recomendamos realizar un fork de este repositorio en GitHub. Posteriormente, clónalo y desde la terminal podrás explorar la información utilizando diversos notebooks. También hemos incluido un archivo 'requirements.txt' para que descargues las librerías necesarias para la visualización. de igual forma se deja este link que permite acceder directo a la carpeta de notbooks

En el eda se evidencia claramente que no hay valores faltantes, nulos, se evidencia la cantidad de datos a trabajar se muestran graficas con los datos relevantes para el analisis que se va a realizar se muestran los años, los dias, las horas con mas siniestros, los generos involucrados, tipos de calles con mas accidentalidad, las comunas con mayores victimas, el tipo de victima y acusado, la edad, la concentracion  de personas por edad año y por ultimo un glosario para tener claridad de los datos que se mencionan 



## Power Bi

Este dashboard utiliza la herramienta Power BI para analizar los accidentes mortales  en la Ciudad Autónoma de Buenos Aires (CABA). El objetivo es evaluar la evolución de la siniestralidad en los últimos años y determinar las medidas necesarias para reducirla.

El primer paso fue abrir la aplicación Power BI y cargar la base de datos en formato CSV. La base de datos contiene información sobre los accidentes mortales desde el año 2016 al 2021

Antes de cargar los datos, se verificó que los datos fueran del tipo adecuado al que se necesitaban. Para ello, se utilizaron las funciones de Power BI para validar los datos y corregir cualquier error.

Una vez que los datos se cargaron correctamente, se crearon las medidas y los gráficos necesarios para realizar el análisis.

*** Medidas Creadas

- **% Hombres:** `DIVIDE([Cantidad Hombres], [Número de Acusados Únicos por Categoría]) * 100`

- **% Mujeres:** `DIVIDE([Cantidad Mujeres], [Número de Acusados Únicos por Categoría]) * 100`

- **Actual:** `DIVIDE(SUM(homicidio_df[N_VICTIMAS]), [Poblacion]) * 100000`

- **Anterior:** `DIVIDE(CALCULATE(SUM(homicidio_df[N_VICTIMAS]), DATEADD(homicidio_df[FECHA_x], -6, MONTH)), [Poblacion]) * 100000`

- **Cantidad Hombres:** `CALCULATE([Número de Acusados Únicos por Categoría], homicidio_df[SEXO] = "MASCULINO")`

- **Cantidad Mujeres:** `CALCULATE([Número de Acusados Únicos por Categoría], homicidio_df[SEXO] = "FEMENINO")`

- **Moto Actual:** `SUMX(FILTER(homicidio_df, YEAR(homicidio_df[AAAA_x]) = YEAR(TODAY())), homicidio_df[VictimasEnMoto])`

- **Moto Anterior:**
  ```md
  CALCULATE(
      SUMX(
          FILTER(homicidio_df, homicidio_df[VICTIMA_x] = "MOTO"),
          DATEVALUE(homicidio_df[FECHA_x])
      ),
      SAMEPERIODLASTYEAR(homicidio_df[FECHA_x])
  )



- Número de acusados únicos por categoría = COUNTROWS(FILTER(homicidio_df, NOT(ISBLANK(homicidio_df[ACUSADO]))))


- Número de víctimas fatales = SUM(homicidio_df[N_VICTIMAS])


- Poblacion = 3120021 * (1 - 0.015)



- Reduccion10Porciento = DIVIDE([Anterior] - [Actual], [Anterior])


- Reduccion7Porciento = ([MotoAnterior] - [MotoActual]) / [MotoAnterior] * 100


- Tasa de homicidios en siniestros viales = (homicidio_df[Número de víctimas fatales] / [Poblacion]) * 100.000


- TasaSiniestrosVialesAnterior = 
CALCULATE(
    SUM(homicidio_df[N_VICTIMAS]),
    DATEADD(homicidio_df[FECHA_x], -6, MONTH)
) / 
(3120021 * (1 - 0.015)) * 100000
                                   

- VictimasEnMoto = CALCULATE(SUM(homicidio_df[N_VICTIMAS]), homicidio_df[VICTIMA_x] = "MOTO")


se crean las columnas
Q1,Q2,Q3,Q4




El objetivo de este proyecto es elaborar un dashboard que permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales en siniestros viales.
Número total de víctimas: El número total de víctimas fatales en siniestros viales en el período de análisis.
Cantidad de acusados: La cantidad de acusados por siniestros viales en el período de análisis.
Cantidad de acusados por género: La cantidad de acusados hombres y mujeres por siniestros viales en el período de análisis.
Porcentaje de acusados por género: El porcentaje de acusados hombres y mujeres por siniestros viales en el período de análisis.
Número de víctimas por calle: El número de víctimas fatales en siniestros viales por calle en el período de análisis.
Número de víctimas por hora: El número de víctimas fatales en siniestros viales por hora en el período de análisis.
Número de víctimas por comuna: El número de víctimas fatales en siniestros viales por comuna en el período de análisis.
Cantidad de acusados por categoría: La cantidad de acusados por categoría de vehículo en los siniestros viales en el período de análisis.
La imagen de porcentajes por género se ha creado utilizando Figma. La imagen muestra los porcentajes de acusados hombres y mujeres por siniestros viales en el período de análisis




## kpis


1- Reducir en un 10% la tasa de homicidios en siniestros viales de los últimos seis meses, en CABA, en comparación con la tasa de homicidios en siniestros viales del semestre anterior.

Definimos a la tasa de homicidios en siniestros viales como el número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica durante un período de tiempo específico. Su fórmula es: (Número de homicidios en siniestros viales / Población total) * 100,000


a- se tiene en cuenta el numero de victimas
b- la tasa de homicidios a lo cual se elaboro las siguiente formula
 Tasa de homicidios en siniestros viales = (homicidio_df[Número de víctimas fatales] / [Poblacion]) * 100.000
c- se crea una medida llamada actual  
Actual = DIVIDE(SUM(homicidio_df[N_VICTIMAS]), [Poblacion]) * 100000
d- se crea una medida anterior
Anterior = DIVIDE(CALCULATE(SUM(homicidio_df[N_VICTIMAS]), DATEADD(homicidio_df[FECHA_x], -6, MONTH)), [Poblacion]) * 100000
e- generamos indicador
Reduccion10Porciento = DIVIDE([Anterior] - [Actual], [Anterior])




2- Reducir en un 7% la cantidad de accidentes mortales de motociclistas en el último año, en CABA, respecto al año anterior.

Definimos a la cantidad de accidentes mortales de motociclistas en siniestros viales como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas que viajaban en moto en un determinado periodo temporal. Su fórmula para medir la evolución de los accidentes mortales con víctimas en moto es: (Número de accidentes mortales con víctimas en moto en el año anterior - Número de accidentes mortales con víctimas en moto en el año actual) / (Número de accidentes mortales con víctimas en moto en el año anterior) * 100


a- en la columna que contiene las victimas en la categoria moto se suman todos los valores que sean = 'moto'
VictimasEnMoto = CALCULATE(SUM(homicidio_df[N_VICTIMAS]), homicidio_df[VICTIMA_x] = "MOTO")
b- se crea una medidad para que tenga en cuenta el dato actual
MotoActual = SUMX(FILTER(homicidio_df, YEAR(homicidio_df[AAAA_x]) = YEAR(TODAY())), homicidio_df[VictimasEnMoto]
c- se crea una medida para que tenga el dato anterir 
MotoAnterior = 
CALCULATE(
    SUMX(
        FILTER(homicidio_df, homicidio_df[VICTIMA_x] = "MOTO"),
        DATEVALUE(homicidio_df[FECHA_x])
    ),
    SAMEPERIODLASTYEAR(homicidio_df[FECHA_x])
)
d- se crea el indicador 
Reduccion7Porciento = ([MotoAnterior] - [MotoActual]) / [MotoAnterior] * 100




## Conclusiones 

 

1. Las horas con mayor incidencia de accidentes son entre las 5, 6 y 7 de la mañana, así como entre las 14 y las 20 horas. 

  

2. En cuanto al tipo de calle, las avenidas lideran con un 64% de los accidentes. 

  

3. Las comunas con los mayores índices de accidentalidad son la 1, 4, 7, 8 y 9, que incluyen los siguientes barrios: 

   - Comuna 1: Retiro, San Nicolás, Monserrat, San Telmo, Puerto Madero, Constitución. 

   - Comuna 4: Parque Patricios, Nueva Pompeya, Barracas. 

   - Comuna 7: Flores. 

   - Comuna 8: Villa Lugano, Villa Riachuelo, Villa Soldati. 

   - Comuna 9: Liniers, Mataderos. 

  

4. Las principales víctimas/acusados son peatones y pasajeros, seguidos por accidentes que involucran motocicletas, automóviles, motocargas y peatones con automóviles. 

  

5. Las principales víctimas son motociclistas y peatones, mientras que los principales acusados son automovilistas y pasajeros. 

  

6. El género más frecuentemente involucrado en acusaciones es el masculino. 

  

7. La franja de edad con mayor incidencia de siniestros se encuentra entre los 20 y 40 años. 



## Recomendaciones

Objetivo:

Disminuir la cantidad de víctimas fatales en siniestros viales en las comunas 1, 2, 3 y 4 de la Ciudad Autónoma de Buenos Aires.


Población objetivo:

Hombres con edad entre los 20 y los 40 años.


Estrategias:

Concientización:
Campañas de educación vial en las avenidas de las comunas objetivo.
Difusión de información sobre seguridad vial en medios de comunicación y redes sociales.
Control de tránsito:
Aumento de la presencia de agentes de tránsito en las avenidas.
Aplicación de sanciones a los conductores que infrinjan las normas de tránsito.
