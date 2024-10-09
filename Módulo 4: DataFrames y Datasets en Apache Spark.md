# Módulo 4: DataFrames y Datasets en Apache Spark

## Introducción

En este módulo, exploraremos dos de las estructuras de datos más poderosas y utilizadas en Apache Spark: **DataFrames** y **Datasets**. Estas estructuras permiten trabajar con datos de una manera más eficiente y fácil, proporcionando un enfoque más estructurado que los RDDs. Al final de este módulo, deberías ser capaz de crear, manipular y realizar operaciones sobre DataFrames y Datasets.

### ¿Qué son los DataFrames?

Un DataFrame es una colección distribuida de datos organizados en columnas, similar a una tabla en una base de datos o a un DataFrame en pandas. Los DataFrames son ideales para trabajar con datos estructurados y semiestructurados, y permiten utilizar una amplia gama de operaciones de consulta, transformación y análisis.

#### Características de los DataFrames

- **Estructura de Tabla**: Los datos se organizan en filas y columnas, donde cada columna tiene un nombre y un tipo de dato.
- **Optimización**: Los DataFrames utilizan la optimización de consulta mediante el motor Catalyst, lo que mejora el rendimiento de las consultas.
- **Interoperabilidad**: Se puede trabajar con datos provenientes de diversas fuentes, como CSV, JSON, Parquet, bases de datos SQL, y más.

#### Creación de un DataFrame

Para crear un DataFrame, puedes usar el método `createDataFrame()` de una instancia de `SparkSession`. Aquí tienes un ejemplo:

```python
from pyspark.sql import SparkSession

# Crear una SparkSession
spark = SparkSession.builder.appName("Ejemplo DataFrame").getOrCreate()

# Crear un DataFrame a partir de una lista de tuplas
datos = [("Juan", 30), ("Ana", 25), ("Pedro", 35)]
columnas = ["Nombre", "Edad"]

df = spark.createDataFrame(datos, columnas)
df.show()
```

### Operaciones Comunes con DataFrames

1. **Mostrar Datos**: Usa `show()` para visualizar los datos.

   ```python
   df.show()
   ```

2. **Seleccionar Columnas**: Utiliza `select()` para elegir columnas específicas.

   ```python
   df.select("Nombre").show()
   ```

3. **Filtrar Filas**: Usa `filter()` para filtrar filas según condiciones.

   ```python
   df.filter(df.Edad > 30).show()  # Filtra personas mayores de 30 años
   ```

4. **Agregar una Nueva Columna**: Usa `withColumn()` para añadir nuevas columnas.

   ```python
   from pyspark.sql.functions import col

   df_con_nueva_columna = df.withColumn("Edad en meses", col("Edad") * 12)
   df_con_nueva_columna.show()
   ```

5. **Agrupar y Agregar**: Utiliza `groupBy()` y funciones de agregación para resumir datos.

   ```python
   df.groupBy("Nombre").agg({"Edad": "avg"}).show()  # Calcula la edad promedio por nombre
   ```

### ¿Qué son los Datasets?

Los Datasets son una extensión de los DataFrames que proporcionan un tipo de dato fuerte y son compatibles con la API de tipo seguro. Esto significa que puedes aprovechar la verificación de tipos en tiempo de compilación, lo que reduce los errores en el código.

#### Características de los Datasets

- **Tipos Fuertes**: Permiten trabajar con objetos de Scala o Java con tipos fuertes.
- **Optimización**: Al igual que los DataFrames, los Datasets se benefician de las optimizaciones del motor Catalyst.

#### Creación de un Dataset

Para crear un Dataset, necesitas tener una clase que represente el esquema del Dataset y luego puedes convertir un DataFrame en un Dataset:

```scala
case class Persona(nombre: String, edad: Int)

val datos = Seq(Persona("Juan", 30), Persona("Ana", 25), Persona("Pedro", 35))
val dataset = spark.createDataset(datos)
dataset.show()
```

### Comparación entre DataFrames y Datasets

| Característica        | DataFrames                              | Datasets                          |
|-----------------------|-----------------------------------------|-----------------------------------|
| Tipo de datos         | No tiene tipos fuertes                  | Tiene tipos fuertes               |
| Lenguaje              | Disponible en Python, R, Scala, Java   | Principalmente en Scala y Java    |
| Optimización          | Sí, usa Catalyst                        | Sí, usa Catalyst                  |
| Interfaz              | API basada en DataFrame                 | API basada en Dataset             |

### Ejercicio Práctico

1. Crea un DataFrame a partir de un archivo CSV que contenga datos de empleados (nombre, edad, salario).
2. Realiza las siguientes operaciones:
   - Muestra los primeros 10 registros.
   - Filtra los empleados que tienen un salario mayor a 50000.
   - Agrupa los datos por edad y calcula el salario promedio por edad.

**Ejemplo de Solución**:

```python
# Cargar un DataFrame desde un archivo CSV
df_empleados = spark.read.csv("ruta/al/empleados.csv", header=True, inferSchema=True)

# Mostrar los primeros 10 registros
df_empleados.show(10)

# Filtrar empleados con salario mayor a 50000
df_empleados.filter(df_empleados.Salario > 50000).show()

# Agrupar por edad y calcular el salario promedio
df_empleados.groupBy("Edad").agg({"Salario": "avg"}).show()
```

### Recursos Adicionales

- [Documentación de DataFrames y Datasets en Apache Spark](https://spark.apache.org/docs/latest/sql-programming-guide.html)
- [Curso de Apache Spark para Ciencia de Datos en Coursera](https://www.coursera.org/learn/spark-data-science)
- [Tutorial de DataFrames en Apache Spark en Medium](https://medium.com/@yourusername/spark-dataframes-tutorial)

---

En este módulo, has aprendido sobre DataFrames y Datasets en Apache Spark, incluidas sus características, cómo crearlos y realizar operaciones comunes. En el siguiente módulo, exploraremos las funciones SQL en Apache Spark y cómo se integran con DataFrames.
encias clave.
