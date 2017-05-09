---
layout: post
title: 🤔✍️Recommendation systems with Apache Spark🌳🌿
---
data: [Amazon product data](http://jmcauley.ucsd.edu/data/amazon/)
techniques: big data, collaborative filtering, ALS, Spark

---
Spring has sprung in NYC and it's time for gardening! But how to buy the right hose when you're a total gardening newbie?

This is a short step-by-step tutorial on collaborative filtering based recommendation systems on <a href="http://jmcauley.ucsd.edu/data/amazon/">Amazon product data</a>. Detailed instructions are included in the Jupyter Notebook (GardeningToolsRecommender.ipynb), so please check it out. Below, I included materials I found super useful to learn about recommendation systems & Apache Spark (which is used to paralelize alternative least squares at the end of the notebook).

For instructional purposes, the code is not optimized for speed. 

![recommendation_systems]({{ site.baseurl }}/images/recommendation_systems.jpg)

Source of the image (I added scribbles myself;): _"Recommendation systems: Principles, methods and evaluation"_ by Isinkayea, Folajimib and Ojokohc, http://doi.org/10.1016/j.eij.2015.06.005

# Resources:

## Data:
[Amazon's data](http://jmcauley.ucsd.edu/data/amazon/) set contains reviews and metadata spanning from 1996 to 2014 and is an excellent source if you want to practice recommendation algorithms. As you might suspect, it's huge, but Julian McAuley from UCSD also shared smaller subsets. I decided to use one of the 5-core datasets which contain entries from users who reviewed at least 5 products and products which were reviewed at least 5 times, which drastically limits the size of it allowing to run costly algorithms (such as ALS) on a personal laptop within a reasonable time (it took me few minutes).


## Readings:

Blog posts about collaborative filtering and Alternative Least Squares: 

Andrew Ng's awesome [intro to recommender systems](https://www.coursera.org/learn/machine-learning/home/week/9) (part of his ML coursera series, so pretty basic)

Ethan Rosenthal's excellent blog post about [collaborative filtering](http://blog.ethanrosenthal.com/2015/11/02/intro-to-collaborative-filtering/) and [matrix factorization](http://blog.ethanrosenthal.com/2016/01/09/explicit-matrix-factorization-sgd-als/) (a bit more advanced).

Alex Abate on [collaborative filtering](http://alexabate.github.io/2016/11/05/movie-lens.html) - I heavily borrowed from her prediction rating code, which demonstrates step-by-step how it works.

bugra on [Alternating Least Squares](ttp://bugra.github.io/work/notes/2014-04-19/alternating-least-squares-method-for-collaborative-filtering/).

## Apache Spark

Using Apache Spark makes a lot of sense when we're using iterative algorithms (such as gradient descent or alternative least squares) as it leverages its capacity for *caching* / *persisting* (taking a snapshot of the data and iterating only over steps which are unique across iterations).

### Running Apache Spark with Jupyter Notebook:

It's not hard at all, actually! Make sure SSH is enabled on your machine, your Java is up to date, and [download](http://spark.apache.org/downloads.html) + install Spark. In my case, in order to run it I need to execute in the Terminal:
<pre>
    $ export PATH=$PATH:/usr/local/spark/bin:/usr/local/spark/sbin
</pre>
followed by:
<pre>
    $ start-all.sh
</pre>
and to lanch Jupyter Notebook with Spark:
<pre>
    $ PYSPARK_DRIVER_PYTHON=ipython PYSPARK_DRIVER_PYTHON_OPTS="notebook --no-browser --ip="*"" pyspark --master local[*]
</pre>

Then, Jupyter Notebook will run on <code>localhost:8888</code>, your Spark cluster UI on <code>localhost:8080</code> and Spark Jobs on <code>localhost:4040</code>. 
Those tips come from **Austin Ouyang** who wrote a great step-by-step [intro](http://blog.insightdatalabs.com/jupyter-on-apache-spark-step-by-step/) and gave a two day workshop at Insight Labs that I attended (and you can sign up for too:).

### Machine learning and collaborative filtering with Spark: 

http://spark.apache.org/docs/latest/mllib-guide.html

https://spark.apache.org/docs/latest/mllib-collaborative-filtering.html

A great tutorial on recommendations systems and Spark with MovieLens data: https://databricks-training.s3.amazonaws.com/movie-recommendation-with-mllib.html

# Requirements:

1. <a href="https://www.python.org/"> Python</a> (2.7)
2. <a href="http://jupyter.org/">Jupyter Notebook</a>
3. <a href="http://www.numpy.org/">NumPy</a>
4. <a href="http://www.scipy.org/">SciPy</a>
5. <a href="http://matplotlib.org/">matplotlib</a>
6. <a href="http://pandas.pydata.org">Pandas</a>
7. <a href="http://scikit-learn.org/stable/">scikit learn</a>

To install all of them (except Python) using pip run:
<pre>
 pip install -r requirements.txt
</pre>




