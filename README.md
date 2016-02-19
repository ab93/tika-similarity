[Apache Tika](http://tika.apache.org/) File Similarity based on Jaccard distance, Edit distance & Cosine distance
===

This project demonstrates using the [Tika-Python](http://github.com/chrismattmann/tika-python) package (Python port of Apache Tika) to compute file similarity based on Metadata features.

The script can iterate over all files in the current directory or given files by command line and derives their metadata features, then computes the union of all features. The union of all features become the "golden feature set" that all document features are compared to via intersect. The length of that intersect per file divided by the length of the unioned set becomes the similarity score.

Scores are sorted in reverse (descending) order which can be shown in three different Data-Driven document visualizaions.

Pre-requisite
===
0. Install [Tika-Python](http://github.com/chrismattmann/tika-python)

Installation
===
```
pip install editdistance
git clone https://github.com/chrismattmann/tika-img-similarity
```
You can also check out [ETLlib](https://github.com/chrismattmann/etllib/tree/master/etl/imagesimilarity.py)

How to use
===

Optional: Compute similarity only on specific IANA MIME Type(s) inside a directory using **--accept**

Key-based comparison
--------------------
This compares metadata feature names as a golden feature set
```python
#!/usr/bin/env python2.7
python similarity.py -f [directory of files] [--accept [jpeg pdf etc...]]
or 
python similarity.py -c [file1 file2 file3 ...]
```
Value-based comparison
----------------------
This compares metadata feature names together with its value as a golden feature set
```python
#!/usr/bin/env python2.7
python value-similarity.py -f [directory of files] [--accept [jpeg pdf etc...]]
or 
python value-similarity.py -c [file1 file2 file3 ...]
```

Edit Distance comparison on Metadata Values
-------------------------------------------
- This computes pairwise similarity scores based on Edit Distance Similarity.
- **Similarity Score of 1 implies an identical pair of documents.**
- **Clustering & Visualization is Pending.**

```python
#!/usr/bin/env python2.7
python edit-value-similarity.py [-h] --inputDir INPUTDIR --outCSV OUTCSV [--accept [png pdf etc...]] [--allKeys]

--inputDir INPUTDIR  path to directory containing files

--outCSV OUTCSV      path to directory for storing the output CSV File, containing pair-wise Similarity Scores based on Edit distance

--accept [ACCEPT]    Optional: compute similarity only on specified IANA MIME Type(s)

--allKeys            Optional: compute edit distance across all metadata keys of 2 documents, else default to only intersection of metadata keys

```
```python
Eg: python edit-value-similarity.py --inputDir /path/to/files --outCSV /path/to/output.csv --accept png pdf gif
```

Cosine Distance comparison on Metadata Values
---------------------------------------------
- This computes pairwise similarity scores based on Cosine Distance Similarity.
- **Similarity Score of 1 implies an identical pair of documents.**
- **Clustering & Visualization is Pending.**

```python
#!/usr/bin/env python2.7
python cosine_similarity.py [-h] --inputDir INPUTDIR --outCSV OUTCSV [--accept [png pdf etc...]]

--inputDir INPUTDIR  path to directory containing files

--outCSV OUTCSV      path to directory for storing the output CSV File, containing pair-wise Similarity Scores based on Cosine distance

--accept [ACCEPT]    Optional: compute similarity only on specified IANA MIME Type(s)

```


D3 visualization
----------------

### cluster viz 
```
* python cluster-scores.py [-t threshold_value] (for generating cluster viz)
* open cluster-d3.html(or dynamic-cluster.html for interactive viz) in your browser
```
Default **threshold** value is 0.01.

<img src="https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/cluster.png" width = "200px" height = "200px" style = "float:left">
<img src="https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/interactive-cluster.png" width = "200px" height = "200px" style = "float:right">

###circlepacking viz
```
* python circle-packing.py (for generating circlepacking viz)
* open circlepacking.html(or dynamic-circlepacking.html for interactive viz) in your browser
```
<img src="https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/circlepacking.png" width = "200px" height = "200px" style = "float:left">
<img src="https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/interactive-circlepacking.png" width = "200px" height = "200px" style = "float:right">

###composite viz
This is a combination of cluster viz and circle packing viz.
The deeper color, the more the same attributes in the cluster.
```
* open compositeViz.html in your browser
```
![Image of composite viz](https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/composite.png)

###Big data way
if you are dealing with big data, you can use it this way:
```
* python generateLevelCluster.py (for generating level cluster viz)
* open levelCluster-d3.html in your browser
```
You can set max number for each node **_maxNumNode**(default _maxNumNode = 10) in generateLevelCluster.py
![Image of level composite viz](https://github.com/dongnizh/tika-img-similarity/blob/refactor/snapshots/level-composite.png)

Questions, comments?
===================
Send them to [Chris A. Mattmann](mailto:chris.a.mattmann@jpl.nasa.gov).

Contributors
============
* Chris A. Mattmann, JPL
* Dongni Zhao, USC
* Harshavardhan Manjunatha, USC
* Thamme Gowda, USC
* Ayberk Yılmaz, USC


License
===

This project is licensed under the [Apache License, version 2.0](http://www.apache.org/licenses/LICENSE-2.0).







