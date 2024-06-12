# Parallelized K-means Clustering

This project implements the K-means algorithm in a parallelized manner using a master-slave model to distribute the workload among multiple processes.

## Project Structure

The project is divided into several files:

- `master.py`: Contains the `Master` class, which coordinates operations and distributes tasks to the slaves.
- `slave.py`: Contains the `Slave` class, which receives tasks from the master, executes them, and sends the results back.
- `utils.py`: Contains helper functions such as centroid initialization, cluster assignment, centroid update, and result visualization.
- `main.py`: Entry point of the program, where the current node is specified as either a master or a slave.

## Installation

1. Clone this repository:

    ```bash
    git clone https://github.com/JuanMorales1025/parallelized-kmeans-clustering.git
    cd parallelized-kmeans-clustering
    ```

2. Install the required dependencies:

    ```bash
    pip install numpy pandas matplotlib scikit-learn
    ```

## Running the Project

1. Ensure you have a data file at `input_data/Online_Retail.xlsx`. This file is used for clustering.

2. Run the main code twice: once for the master and once for each slave. For example, if you have one master and one slave, run:

    ```bash
    python main.py master
    python main.py slave
    ```

    You can adjust the number of slaves in the code as needed.

## Description of Key Functions

- `Master`: Class that coordinates the operation, distributes data to slaves, and gathers results.
- `Slave`: Class that receives tasks from the master, performs computations, and sends results back.
- `initCentroids(X, K)`: Initializes centroids using K-means++.
- `assignClusters(X, Centroids, K)`: Assigns each data point to the nearest cluster.
- `updateCentroids(X, Centroids, K, cluster_assignation)`: Updates the centroids based on cluster assignment.
- `plot_output(Output, Centroids, K)`: Visualizes the clustering results.

## Example Usage

The algorithm runs in parallel, distributing data among slaves to assign clusters and updating the centroids in each iteration. In the end, the results are visualized using `matplotlib`.

1. **Centroid Initialization**:
    ```python
    data_to_broadcast = initCentroids(df_values, K)
    ```

2. **Cluster Assignment in Parallel**:
    ```python
    cluster_assignation = master.runSlaves(data_to_scatter, data_to_broadcast, assignClusters, K)
    ```

3. **Centroid Update**:
    ```python
    Output, data_to_broadcast = updateCentroids(df_values, data_to_broadcast, K, cluster_assignation)
    ```

4. **Visualization**:
    ```python
    plot_output(Output, Centroids, K)
    ```

## Contributions

Contributions are welcome. If you wish to contribute, please fork the repository and submit a pull request with your changes.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.
