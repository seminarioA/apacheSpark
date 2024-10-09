# Módulo 3: Transformaciones y Acciones en RDDs

## Introducción

En Apache Spark, las transformaciones y acciones son operaciones fundamentales que se pueden realizar en los Resilient Distributed Datasets (RDDs). Comprender cómo funcionan estas operaciones es crucial para manipular y procesar datos de manera eficiente en Spark. Este módulo se enfocará en explicar en detalle las transformaciones y acciones, con ejemplos y ejercicios prácticos.

### Transformaciones

Las transformaciones son operaciones que crean un nuevo RDD a partir de uno existente. Estas operaciones son **perezosas**, lo que significa que no se ejecutan inmediatamente. En su lugar, Spark construye un DAG (Directed Acyclic Graph) de las operaciones y las ejecuta solo cuando se realiza una acción. Esto permite optimizar el rendimiento y la utilización de recursos en el clúster.

#### Tipos Comunes de Transformaciones

1. **map(función)**:
   - **Descripción**: Aplica una función a cada elemento del RDD y devuelve un nuevo RDD que contiene los resultados.
   - **Ejemplo**:

     ```python
     rdd = sc.parallelize([1, 2, 3, 4, 5])
     rdd_mapeado = rdd.map(lambda x: x * 2)  # Devuelve [2, 4, 6, 8, 10]
     ```

2. **filter(función)**:
   - **Descripción**: Filtra los elementos del RDD que cumplen con una condición definida por una función.
   - **Ejemplo**:

     ```python
     rdd_pares = rdd.filter(lambda x: x % 2 == 0)  # Devuelve [2, 4]
     ```

3. **flatMap(función)**:
   - **Descripción**: Similar a `map`, pero cada entrada puede devolver múltiples salidas (es decir, aplanar la salida).
   - **Ejemplo**:

     ```python
     rdd_texto = sc.parallelize(["hola mundo", "adiós mundo"])
     rdd_flat = rdd_texto.flatMap(lambda x: x.split(" "))  # Devuelve ['hola', 'mundo', 'adiós', 'mundo']
     ```

4. **reduceByKey(función)**:
   - **Descripción**: Agrupa los valores por clave y aplica una función de reducción.
   - **Ejemplo**:

     ```python
     rdd_claves = sc.parallelize([("a", 1), ("b", 1), ("a", 2)])
     rdd_reducido = rdd_claves.reduceByKey(lambda x, y: x + y)  # Devuelve [('a', 3), ('b', 1)]
     ```

5. **union(otro RDD)**:
   - **Descripción**: Combina dos RDDs en uno nuevo que contiene todos los elementos de ambos RDDs.
   - **Ejemplo**:

     ```python
     rdd1 = sc.parallelize([1, 2, 3])
     rdd2 = sc.parallelize([4, 5, 6])
     rdd_union = rdd1.union(rdd2)  # Devuelve [1, 2, 3, 4, 5, 6]
     ```

### Acciones

Las acciones son operaciones que devuelven un resultado al controlador o almacenan datos en un sistema de almacenamiento externo. A diferencia de las transformaciones, las acciones desencadenan la ejecución del DAG y pueden llevar a cabo cálculos reales.

#### Tipos Comunes de Acciones

1. **collect()**:
   - **Descripción**: Devuelve todos los elementos del RDD al controlador como una lista. Útil para conjuntos de datos pequeños.
   - **Ejemplo**:

     ```python
     resultados = rdd.collect()  # Devuelve [1, 2, 3, 4, 5]
     print(resultados)
     ```

2. **count()**:
   - **Descripción**: Devuelve el número de elementos en el RDD.
   - **Ejemplo**:

     ```python
     cantidad = rdd.count()  # Devuelve 5
     print(f"Número de elementos: {cantidad}")
     ```

3. **first()**:
   - **Descripción**: Devuelve el primer elemento del RDD.
   - **Ejemplo**:

     ```python
     primer_elemento = rdd.first()  # Devuelve 1
     print(f"Primer elemento: {primer_elemento}")
     ```

4. **take(n)**:
   - **Descripción**: Devuelve los primeros `n` elementos del RDD.
   - **Ejemplo**:

     ```python
     primeros_tres = rdd.take(3)  # Devuelve [1, 2, 3]
     print(primeros_tres)
     ```

5. **saveAsTextFile(ruta)**:
   - **Descripción**: Guarda el contenido del RDD en un archivo de texto en el sistema de archivos.
   - **Ejemplo**:

     ```python
     rdd.saveAsTextFile("ruta/al/archivo_salida.txt")
     ```

### Ejercicio Práctico

1. Crea un RDD a partir de una lista de números del 1 al 20.
2. Aplica una transformación para filtrar los números impares.
3. Usa `map` para elevar al cuadrado cada número filtrado.
4. Realiza una acción para contar cuántos números impares se han elevado al cuadrado y muestra el resultado.

**Ejemplo de Solución**:

```python
# Crear un RDD con números del 1 al 20
rdd_numeros = sc.parallelize(range(1, 21))

# Filtrar los números impares
rdd_impares = rdd_numeros.filter(lambda x: x % 2 != 0)

# Elevar al cuadrado cada número impar
rdd_cuadrados = rdd_impares.map(lambda x: x ** 2)

# Contar los números impares elevados al cuadrado
cantidad_cuadrados = rdd_cuadrados.count()
print(f"Número de impares elevados al cuadrado: {cantidad_cuadrados}")
```

### Recursos Adicionales

- [Documentación de Transformaciones y Acciones en Apache Spark](https://spark.apache.org/docs/latest/rdd-programming-guide.html#transformations)
- [Curso de Introducción a Apache Spark en Coursera](https://www.coursera.org/learn/spark)
- [Tutorial de Spark para Principiantes en Medium](https://medium.com/@yourusername/spark-beginners-guide)

---

En este módulo, has aprendido sobre las transformaciones y acciones en RDDs, así como ejemplos prácticos de cómo utilizarlas. Has visto cómo las transformaciones permiten crear nuevos RDDs y cómo las acciones desencadenan el procesamiento de datos. En el siguiente módulo, exploraremos las estructuras de datos más avanzadas en Spark, como DataFrames y Datasets.
