# Módulo 2: Resilient Distributed Datasets (RDDs)

## Introducción a RDDs

Los Resilient Distributed Datasets (RDDs) son la estructura de datos fundamental en Apache Spark. Un RDD es una colección inmutable y distribuida de objetos que se pueden procesar en paralelo. Los RDDs son una de las características clave que permiten a Spark manejar grandes volúmenes de datos de manera eficiente.

### Características de RDDs

- **Inmutabilidad**: Una vez creado, un RDD no puede ser modificado. En su lugar, se pueden crear nuevos RDDs a partir de operaciones en RDDs existentes.
- **Distribución**: Los RDDs se distribuyen automáticamente en un clúster de computadoras, lo que permite el procesamiento paralelo.
- **Resiliencia**: Los RDDs pueden recuperarse de fallos automáticamente, lo que los hace robustos para el procesamiento de grandes conjuntos de datos.

### Creación de RDDs

Hay varias formas de crear RDDs en Spark:

1. **Desde un archivo externo**: Puedes cargar datos desde un archivo de texto o CSV.
2. **A partir de una colección existente en memoria**: Puedes crear un RDD a partir de una lista o colección en memoria.
3. **A través de transformaciones de otro RDD**: Puedes aplicar operaciones a un RDD existente para crear un nuevo RDD.

#### Ejemplo de creación de RDDs

A continuación se presentan ejemplos de cómo crear RDDs en PySpark y Scala.

**Ejemplo en PySpark:**

```python
from pyspark import SparkContext

# Crear un contexto de Spark
sc = SparkContext("local", "Ejemplo RDD")

# Crear un RDD a partir de una lista
data = [1, 2, 3, 4, 5]
rdd = sc.parallelize(data)

# Crear un RDD a partir de un archivo
rdd_from_file = sc.textFile("ruta/al/archivo.txt")
```

**Ejemplo en Scala:**

```scala
import org.apache.spark.{SparkConf, SparkContext}

// Crear un contexto de Spark
val conf = new SparkConf().setAppName("Ejemplo RDD").setMaster("local")
val sc = new SparkContext(conf)

// Crear un RDD a partir de una lista
val data = List(1, 2, 3, 4, 5)
val rdd = sc.parallelize(data)

// Crear un RDD a partir de un archivo
val rddFromFile = sc.textFile("ruta/al/archivo.txt")
```

### Operaciones en RDDs

Las operaciones en RDDs se dividen en dos categorías:

1. **Transformaciones**: Operaciones que crean un nuevo RDD a partir de uno existente. Son perezosas, lo que significa que no se ejecutan hasta que se necesita el resultado. Ejemplos incluyen `map`, `filter`, y `flatMap`.

2. **Acciones**: Operaciones que devuelven un resultado al controlador o guardan datos en un sistema de almacenamiento externo. Ejemplos incluyen `count`, `collect`, y `saveAsTextFile`.

#### Ejemplo de operaciones

**Transformación:**

```python
# Filtrar los números pares
rdd_pares = rdd.filter(lambda x: x % 2 == 0)
```

**Acción:**

```python
# Contar los elementos en el RDD
count = rdd.count()
print(f"Número de elementos: {count}")
```

### Ejercicio Práctico

1. Crea un RDD a partir de un archivo de texto que contenga una lista de nombres.
2. Aplica una transformación para filtrar los nombres que comiencen con la letra "A".
3. Usa una acción para contar cuántos nombres cumplen con esta condición.

### Recursos Adicionales

- [Documentación oficial de Apache Spark](https://spark.apache.org/docs/latest/rdd-programming-guide.html)
- [Tutorial de PySpark en Databricks](https://docs.databricks.com/getting-started/quick-start.html)

---

En este módulo, has aprendido sobre RDDs, su creación y las operaciones básicas que se pueden realizar. En el siguiente módulo, exploraremos las operaciones específicas que se pueden llevar a cabo en RDDs, lo que te permitirá manipular datos de manera más efectiva en Spark.
