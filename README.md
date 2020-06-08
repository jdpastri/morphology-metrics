# Data Complexity Metrics Based on Morphology for Overlap and Imbalance: Snapshot, New Overlap Number of Balls Metrics and Singular Problems Prospect

Complementary material for the paper on morphology-based complexity metrics.

This repository is organised as follows:

1. Abstract
1. Overview of the State-of-the-art Data Complexity Metrics
1. Results

## Abstract

Data Science and Machine Learning have become fundamental assets for companies and research institutions alike. As one of its fields, supervised classification allows for class prediction of new samples, learning from given training data. However, some properties can cause datasets to be problematic to classify.

In order to evaluate a dataset a priori, data complexity metrics have been used extensively. They provide information regarding different intrinsic characteristics of the data, which serve to evaluate classifier compatibility and a course of action that improves performance. However, most complexity metrics focus on just one characteristic of the data, which can be insufficient to properly evaluate the dataset towards the classifiers' performance. In fact, class overlap, a very detrimental feature for the classification process (especially when imbalance among class labels is also present) is hard to assess.

This research work focuses on complexity metrics based on data morphology. In accordance to their nature, the premise is that they provide both good estimates for class overlap, and great correlations with the classification performance. For that purpose, a novel family of metrics have been developed. Being based on ball coverage by classes, they are named after Overlap Number of Balls. Finally, some prospects for the adaptation of the former family of metrics to singular (more complex) problems are discussed.

## Overview of the State-of-the-art Data Complexity Metrics

(Add a small intro)

<html>
<table>
 <caption><b>Table 1</b>: State-of-the-art data complexity metrics by focus, from (Lorena et al., 2019).</caption>
 <thead>
  <tr>
   <th scope="col">Type of metric</th>
   <th colspan="2">Metric name</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <th rowspan="3" scope="rowgroup">Neighbourhood</th>
   <td>N1</td>
   <td>N2</td>

  </tr>
  <tr>
   <td>N3</td>
   <td>N4</td>

  </tr>
  <tr>
   <td>T1</td>
   <td>LSC</td>

  </tr>
  
  <tr>
   <th rowspan="3" scope="rowgroup">Feature Overlap</th>
   <td>F1</td>
   <td>F1v</td>

  </tr>
  <tr>
   <td>F2</td>
   <td>F3</td>

  </tr>
  <tr>
   <td>F4</td>
   <td></td>

  </tr>
 <tr>
   <th rowspan="2" scope="rowgroup">Linearity</th>
   <td>L1</td>
   <td>L2</td>

  </tr>
  <tr>
   <td>L3</td>
   <td></td>
  </tr>

  <tr>
   <th rowspan="2" scope="rowgroup">Dimensionality</th>
   <td>T2</td>
   <td>T3</td>

  </tr>
  <tr>
   <td>T4</td>
   <td></td>

  </tr>
  <tr>
   <th scope="row">Class Balance</th>
   <td>C1</td>
   <td>C2</td>

  </tr>
  <tr>
   <th rowspan="2" scope="rowgroup">Network Properties</th>
   <td>Density</td>
   <td>ClsCoef</td>

  </tr>
  <tr>
   <td>Hubs</td>
   <td></td>

  </tr>
  
 </tbody>
</table>
</html>





### Neighbourhood metrics

These metrics aim to discern the boundaries between the classes or their structure, studying the neighbourhoods of the points. These six metrics are the most prevalent:

* N1: it is the Fraction of Borderline Points of the Minimum Spanning Tree, a tree graph generated using the instances (vertexes) and the distances between them to create and weigh the edges. The borderline points are those that have at least one edge that connects them to a point of a different class. N1 is the ratio of these points and the total number of points. Greater values indicate greater complexity. 


* N2: this is the Ratio of Intra/Extra-Class Nearest Neighbour Distance, which compares the distances inside a class with those between classes. For this, the division of the sum of the 1NN distances among the points from one class and the sum of the 1NN distances of points from that class to points of a different class is computed. N2 grows with that ratio, so the bigger N2, the closer the classes, which often signals greater complexity.


* N3: this is the Error Rate of the Nearest Neighbour Classifier, or the ratio of the misclassified points using a leave-one-out 1NN over all instances. The higher the value, the more complex the boundaries and the dataset will be.


* N4: it is the Non-Linearity of the Nearest Neighbour Classifier. For this metric, a set  of new points is generated by interpolation of pairs of points that share a class. These new points are then classified using nearest neighbours, where the initial data is the training set. N4 is the ratio of the misclassified interpolated points. Higher values indicate a more complex dataset.


* T1: this is the Fraction of Hyperspheres Covering Data, from \cite{ho_complexity_2002}. For this metric, hyperspheres are generated, centred on each data point. Their radii are the distances from those instances to their closest of a different class. Then, the hyperspheres that are completely contained within others are eliminated. T1 is the ratio between the number of the chosen hyperspheres and the total points. Higher values imply a harder coverage and a more complex dataset.


* LSC: this is the Local Set Average Cardinality, from \cite{leyva_set_2015}. The local set of an instance consists of the data points from its class that are closer than those of other classes. Its cardinality can indicate the closeness of that instance to the class boundaries, since points near them would have close neighbours from a different class, and their local set would thus hold few neighbours from their same class. LSC is derived from the ratio between the mean of those cardinalities and the total instances. Higher LSC indicates less complexity.


### Feature Overlap


This group of metrics assesses the capability of features for the discerning of the classes. If there is at least one feature with low overlap of different classes, the classification should be easier and, thus, obtain better results. The same works for combinations of features and areas of the n-dimensional space of each dataset.
Five different metrics can be enumerated:

* F1: this is the Maximum Fisher’s Discriminant Ratio, which measures the ease to separate the classes using the features (columns) of the data. It compares the dispersion inside each class and the dispersion of the classes. Higher values indicate less overlapping features and, thus, a less complex dataset.
* F1v: this is the Directional Vector Maximum Fisher’s Discriminant Ratio from \cite{orriols-puig_documentation_2010}. It complements F1, looking for the hyperplane, generated by a vector, that best discerns the classes instead of using the separate features. Greater values indicate a lower complexity.
* F2: this metric estimates the volume of the overlapping region, using the ratio between the value limits of each class for each feature and the full range of said feature, and multiplying them to get the ratio of volume overlap. Greater values indicate more overlap, which increases the complexity.
* F3: it is the Maximum Individual Feature Efficiency, which is the biggest ratio of points outside the overlapping region of a feature and the total number of points. Greater values indicate less complexity.
* F4: this is the Collective Feature Efficiency from \cite{orriols-puig_documentation_2010}. It is based on an iterative use of F3 over the dataset, each time
choosing the most efficient feature and setting aside the non-overlapped points of that feature, until there are no more points or features. F4 indicates the ratio of points that have been discerned over the total number of points, so greater values of F4 signal lower complexity.


### Linearity

These measures assess the ease of separability of the different classes by hyperplanes, which would lead to easier classification. There are three main metrics in this category:

* L1: it is a measure of the Sum of the Error Distance by Linear Programming. After using the linear classifier, the total error distance of the misclassified points to their closest hyperplane is computed and divided by the total number of points. The bigger this ratio, the bigger the L1 will be, indicating more complexity.
* L2: this is the Error Rate of the Linear Classifier, that is, the number of misclassified points divided by the total number of points.
The bigger the L2, the more complex a problem will be. 
* L3: it is the Non-Linearity of a Linear Classifier, from \cite{hoekstra_nonlinearity_1996}. For this metric, new points are generated using pairs of points sharing
a class, and they are classified using the initial data as the training set for the generation of the classification model. L3 is the ratio of the misclassified points from those interpolated. A higher value of L3 indicates more complex boundaries and 

### Dimensionality

This set of measures reflect the data sparsity that can appear from a high dimensionality. When a dataset has low-density or even void areas, the model might fail to correctly classify new data there. Three metrics stand out:

* T2: it is the Average Number of Features per Dimension, that is, the number of features of the dataset divided by the number of points. Greater values indicate less points per feature, which will cause sparsity and a higher complexity.
* T3: it is the Average number of PCA Dimensions per points. This is the division of the dimensionality of the PCA selected attributes over the number of points of the dataset. Greater values signal a higher complexity.
* T4: this is the Ratio of the PCA Dimension to the Original Dimension, which is the division of the dimensionality of the PCA selected attributes over the original dimensionality. Greater values indicate that more features are necessary to explain the data variability and, usually, higher complexity. 


### Class balance

These metrics measure the differences in the number of elements in each class, which could favour the classification of the predominant class. The two most common metrics are:

* C1: it is the Entropy of Class Proportions. The higher the value (closer to 1), the most balanced the dataset will be, which usually indicates lower complexity.

* C2: this is the Imbalance Ratio, using the multiclass modification in \cite{tanwani_classification_2010}. It has the value "0" for balanced problems, and higher values (up to 1) indicate more imbalance.

### Network properties

These metrics study graph properties of the data, after using the distances between data points to generate it. To this end, each point becomes a node and the instructions in \cite{morais_complex_2013}, \cite{garcia_effect_2015} and \cite{zhu_semi-supervised_2005-1} are followed in order to decide the edges, which only join close points that belong to the same class. The three basic metrics are the following: 


* Density: it is the Average Density of the Network, which is obtained from the ratio between the number of edges of the graph and the maximum possible amount of edges for that graph. The more edges, the lower the complexity.
* Clustering Coefficient: this metric is derived from the mean of the ratio of edges between each point and its neighbours and the maximum number of edges between them, for every point. It signals the tendency to create cliques. The higher the value, the most complex the dataset.
* Hubs: this is the Mean Hub Score of the graph. The hub score measures the importance of each node from both its connections and their hub scores, in an iterative way. The higher the value, the most complex the dataset.
