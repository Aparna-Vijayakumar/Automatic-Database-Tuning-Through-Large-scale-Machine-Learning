# Automatic-Database-Tuning-Through-Large-scale-Machine-Learning

### Overview:
Since DBMSes have hundreds of knobs, tuning them to minimize latency is particularly hard. The paper uses an automated approach that using ML to recommend configurations 
of DBMS knobs for current workload based on the workloads it has seen in the past. This work is based on https://www.cs.cmu.edu/~dvanaken/papers/ottertune-sigmod17.pdf, with an
extension.

### Preprocessing and Pruning Metrics
The notebook "pruning_metrics.ipynb" contains the code to prune the dataset. Running the notebook yields pruned metrics in output CSVs. The KMeans output is saved in "kmeans_pruned.csv"
and Mean Shift output is saved in "mean_shift_pruned.csv".

The stages in the computation are
<ol>
<li> Loading the input data </li>
<li> Factor Analysis for dimensionality reduction </li>
<li> Cluster the factors obtained in step 2 </li>
	<li> Using K Means (as per the paper) </li>
	<li> Using Mean Shift Clustering (Extension) </li>
<li> Visualizing the clusters </li>
<li> Selecting the points in each cluster closest to the respective centroids. </li>
<li> Selecting the metrics associated with those points and rejecting the rest (Pruning) </li>
<li> Save the knob configuration along with pruned metrics in the output CSV </li>
</ol>

### Latency Prediction via Workload Mapping

The workload mapping, GPR and Random Forest code is in the form of a single python notebook called "prediction.ipynb" and clicking run all will execute everything in the following order:
<ol>
<li> Initialising the data </li>
<li> Normalising the metrics </li>
<li> Workload mapping </li>
<li> Splitting the data into train test and dev </li>
<li> GPR as per pyGPs </li>
<li> GPR as per sklearn </li>
<li> Latency Prediction </li>
<li> Random Forest extension </li>
</ol>

