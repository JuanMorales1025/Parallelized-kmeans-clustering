# Parallelized K-means Clustering

Este proyecto implementa el algoritmo de K-means de manera paralelizada utilizando un modelo maestro-esclavo para distribuir el trabajo entre varios procesos. 

## Estructura del proyecto

El proyecto se divide en varios archivos:

- `master.py`: Contiene la clase `Master`, que coordina las operaciones y distribuye tareas a los esclavos.
- `slave.py`: Contiene la clase `Slave`, que recibe tareas del maestro, las ejecuta y envía los resultados de vuelta.
- `utils.py`: Contiene funciones auxiliares como la inicialización de centroides, asignación de clusters, actualización de centroides y visualización de resultados.
- `main.py`: Punto de entrada del programa, donde se especifica si el nodo actual es un maestro o un esclavo.

## Instalación

1. Clona este repositorio:

    ```bash
    git clone https://github.com/JuanMorales1025/parallelized-kmeans-clustering.git
    cd parallelized-kmeans-clustering
    ```

2. Instala las dependencias necesarias:

    ```bash
    pip install numpy pandas matplotlib scikit-learn
    ```

## Ejecución del proyecto

1. Asegúrate de tener un archivo de datos en `input_data/Online_Retail.xlsx`. Este archivo se utiliza para realizar el clustering.

2. Ejecuta el código principal dos veces: una vez para el maestro y una vez para cada esclavo. Por ejemplo, si tienes un maestro y un esclavo, ejecuta:

    ```bash
    python main.py master
    python main.py slave
    ```

    Puedes ajustar el número de esclavos en el código según sea necesario.

## Descripción de las funciones clave

- `Master`: Clase que coordina la operación, distribuye datos a los esclavos y reúne resultados.
- `Slave`: Clase que recibe tareas del maestro, realiza computaciones y envía resultados de vuelta.
- `initCentroids(X, K)`: Inicializa los centroides usando K-means++.
- `assignClusters(X, Centroids, K)`: Asigna cada punto de datos al cluster más cercano.
- `updateCentroids(X, Centroids, K, cluster_assignation)`: Actualiza los centroides basándose en la asignación de clusters.
- `plot_output(Output, Centroids, K)`: Visualiza los resultados del clustering.

## Ejemplo de uso

El algoritmo se ejecuta en paralelo, distribuyendo los datos entre los esclavos para asignar clusters y actualizando los centroides en cada iteración. Al final, los resultados se visualizan utilizando `matplotlib`.

1. **Inicialización de centroides**:
    ```python
    data_to_broadcast = initCentroids(df_values, K)
    ```

2. **Asignación de clusters en paralelo**:
    ```python
    cluster_assignation = master.runSlaves(data_to_scatter, data_to_broadcast, assignClusters, K)
    ```

3. **Actualización de centroides**:
    ```python
    Output, data_to_broadcast = updateCentroids(df_values, data_to_broadcast, K, cluster_assignation)
    ```

4. **Visualización**:
    ```python
    plot_output(Output, Centroids, K)
    ```

## Contribuciones

Las contribuciones son bienvenidas. Si deseas contribuir, por favor haz un fork del repositorio y envía un pull request con tus cambios.

## Licencia

Este proyecto está licenciado bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.
