---
layout: post
title: Beginner's Guide to DBSCAN
bigimg: img/ML/brain.png
tags:
  - Machine Learning
  - Science
published: true
---

### Intro

### Supervised vs Unsupervised Machine Learning

<p align="center">
  <img src="/img/ML/mlclustering.png" />
</p>

###  Clustering Algorithms
<p align="center">
  <img src="/img/ML/kmeans_convergence.gif" />
</p>


<p align="left">
  <img src="/img/ML/KMEANS_example.png" />
</p>
<p align="right">
  <img src="/img/ML/DBSCAN_example.png" />
</p>

### DBSCAN
<p align="center">
  <img src="/img/ML/DBSCAN_cluster.png" />
</p>

```sh
import pandas as pd
import numpy as np


# initialize class
class DBSCAN:
"""
Density-Based Spatial Clustering of Applications with Noise
-----------------------------------------------------------

a clustering method for unsupervised learning

Parameters
----------
eps: (float, default=0.5)

epsilon; the distance threshold between two points in the same neighborhood

min_samples: (int, default=5)

the number of samples within a point's nighborhood required for it to be weighted as a core point for clustering

(these two parameters determine cluster density)
"""
def  __init__(self, eps=0.5, min_samples=5):

self.eps = eps

self.min_samples = min_samples

# self.data = None #the dataset

self.clusters = []  # list of cluster arrays containing point indeces

self.neighbors = {}  # hash dict of {"point": [neighbor1, neighbor2, ...]}

  

def  get_neighbors(self, X, y):

"""
finds a point's epsilon neighbors via calculating euclidian distance/L² norm

between the datapoints

returns a list of all neighboring points
"""

neighbors = np.where(np.linalg.norm(X[y] - X, axis=1) < self.eps)[0]

return np.array(neighbors)  #might need to remove np.array and just return neigbors

  

def  fit(self, X):
"""
perform clustering on the dataset

returns self

Parameters
----------

X: (array or array-like)

feature array of points to cluster
"""

C = 0  # cluster counter C

n_points = len(X)  # number of data points

self.clabels = np.zeros(n_points, dtype=int)  # define empty label list

for y in  range(n_points):  #for each point in our input data, do the following:

if  self.clabels[y] != 0:  # if it alraedy has a label, skip

continue

neighbors = self.get_neighbors(X, y)  #find neighbors

  

if  len(neighbors) < self.min_samples:  # if the number of neighboring points is less than min_samples (aka not densley surrounded)

self.clabels[y] = -1  # label that point as noise

continue

# when data point isnt noise

C += 1  # move onto the next cluster label

self.clabels[y] = C # assign new cluster label

  

# for each point not yes considerd:

# determine points and their unclaimed neighbors

i = 0

while i < len(neighbors):

  

neighbor_y = int(neighbors[i])  # creating a new cluster

  

if  self.clabels[neighbor_y] == -1:  # label new sparse points as noise

self.clabels[neighbor_y] = C

elif  self.clabels[neighbor_y] == 0:  # skip if already labelled/processed, otherwise add to cluster

self.clabels[neighbor_y] = C

new_neighbors = self.get_neighbors(X, neighbor_y)  # get neighbors of point

if  len(new_neighbors) >= self.min_samples:  # if the number of neighboring points is higher than min_samples (aka densley surrounded)

neighbors = np.append(neighbors, new_neighbors)  # exand the cluster with the newly found neighbors

  

i += 1  # iterate on for all remaining unconsidered points
```

<p align="left">
  <img src="/img/ML/scratch_DBSCAN.png" />
</p>
<p align="right">
  <img src="/img/ML/sklearn_DBSCAN.png" />
</p>

<p align="left">
  <img src="/img/ML/scratch_DBSCAN_blobs.png" />
</p>
<p align="right">
  <img src="/img/ML/sklearn_DBSCAN_blobs.png" />
</p>


### Conclusion 




--- 

**Sources:**


<b name="f1">1 - </b> Bock, Hans-Hermann.  “A Comprehensive Survey of Clustering Algorithms.” *Annals of Data Science* 2,no. 2 (2015): 165–93. https://doi.org/10.1007/s40745-015-0040-1. [↩](#a1)

<b name="f2">2 - </b>  Xu, Dongkuan, and Yingjie Tian. “Clustering Methods: A History of k-Means Algorithms.” *Selected Contributions in Data Analysis and Classification Studies in Classification, Data Analysis, and Knowledge Organization,* 2007, 161–72. https://doi.org/10.1007/978-3-540-73560-1_15.[↩](#a2)

<b name="f3">3 - </b> Mehle, Andraž, Boštjan Likar, and Dejan Tomaževič. "In-Line Recognition of Agglomerated Pharmaceutical Pellets with Density-Based Clustering and Convolutional Neural Network." *IPSJ Transactions on Computer Vision and Applications* 9, , no. 1 (2017). https://doi.org/10.1186/s41074-017-0019-2. [↩](#a3)

<b name="f4">4 - </b> Ester, Martin; Kriegel, Hans-Peter; Sander, Jörg; Xu, Xiaowei. 1996. "A density-based algorithm for discovering clusters in large spatial databases with noise." Proceedings of the Second International Conference on Knowledge Discovery and Data Mining (KDD-96). *AAAI Press*. pp. 226–231. https://doi/10.5555/3001460.3001507. [↩](#a4)

<b name="f5">5 - </b> Schubert, Erich, Jörg Sander, Martin Ester, Hans Peter Kriegel, and Xiaowei Xu. "DBSCAN Revisited, Revisited." *ACM Transactions on Database Systems* 42, no. 3 (2017): 1–21. https://doi.org/10.1145/3068335. [↩](#a5)


The jupyter notebook used to prepare and visualize the data and can accessed  [here](<https://github.com/maiali13//ML-Cookbook/blob/master/DBSCAN_Recipe.ipynb> "maiali13").
