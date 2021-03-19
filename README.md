<h2>Building a Recommender</h2><br>
To demonstrate how to build an analytic job with Mahout on EMR, we’ll build a movie recommender. We will start with ratings given to movie titles by users in the MovieLens data set, which was compiled by the GroupLens team, and will use the “recommenditembased” example to find most-recommended movies for each user.

<br>

In the CLI type bellow commands
<br>
<h3>Get the MovieLens data</h3>
<code>wget http://files.grouplens.org/datasets/movielens/ml-1m.zip

unzip ml-1m.zip</code>

<h5>Convert ratings.dat, trade “::” for “,”, and take only the first three columns:</h5>
<code>cat ml-1m/ratings.dat | sed 's/::/,/g' | cut -f1-3 -d, > ratings.csv</code>

<h5>Put ratings file into HDFS:</h5>
<code>hadoop fs -put ratings.csv /ratings.csv</code>

<h3>Run the recommender job:</h3>
<code>mahout recommenditembased --input /ratings.csv --output recommendations --numRecommendations 10 --outputPathForSimilarityMatrix similarity-matrix --similarityClassname SIMILARITY_COSINE</code>

<h3>Look for the results in the part-files containing the recommendations:</h3>
<code>hadoop fs -ls recommendations

hadoop fs -cat recommendations/part-r-00000 | head</code>

<h2>Building a Recommender</h2><br>

