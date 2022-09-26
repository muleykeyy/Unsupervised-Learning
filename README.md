# UNSUPERVISED LEARNING

# 1) K-Means Clustering

K-means clustering is an iterative process in which similar observations are grouped together. To do that, this algorithm starts by taking 2 random points known as centroids, and starts calculating the distance of each observation to the centroid, and assigning each cluster to the nearest centroid. After the first iteration every point belongs to a cluster.

Next, the number of centroids increases by one, and the centroid for each cluster are recalculated as the points with the average distance to all points in a given cluster. Then we keep repeating this process until no example is assigned to another cluster. 

And this process is repeated k-times, hence the name k-means. This algorithm converges when clusters do not move anymore.

We can also create multiple clusters, and we can have multiple solutions, by multiple solutions we mean that the clusters are not going to move anymore (they converged) but we can converge in different places where we no longer move those centroids.

## Advantages and Disadvantages of K-Means  

The main advantage of k-means algorithm is that it is easy to compute. One disadvantage is that this algorithm is sensitive to the choice of the initial points, so different initial configurations may yield different results. 

To overcome this, there is a smarter initialization of K-mean clusters called K-means ++, which helps to avoid getting stuck at local optima. This is the default implementation of the K-means.     

## Model Selection, Choosing K number of clusters

Sometimes you want to split your data into a predetermined number of groups or segments. Often, the number of clusters (K) is unclear, and you need an approach to select it.

A common metric is Inertia, defined as the sum of squares distance from each point to its cluster centroid.

Smaller values of Inertia correspond to tighter clusters, this means that we are penalizing spread out clusters and rewarding clusters that are tighter to their centroids.

The draw back of this metric is that its value sensitive to number of points in clusters. The more points you add, the more you will continue penalizing the inertia of a cluster, even if those points are relatively closer to the centroids than the existing points. 

Another metric is Distortion defined as the average of squared distance from each point to its cluster.

Smaller values of distortion corresponds to tighter clusters.

An advantage of distortion is that it doesn’t generally increase as more points are added (relative to inertia). This means that It doesn’t increase distortion, as closer points will actualyl decrease the average distance to the cluster centroid.

## Inertia VS Distortion 

Both Inertia and Distortion are measures of entropy per cluster.

Inertia will always increase as more members are added to each cluster, while this will not be the case with distortion. 

When the similarity of the points in the cluster are very relevant, you should use distortion and if you are more concerned that clusters should have a similar number of points, then you should use inertia.     

## Finding Right Cluster

To find the cluster with a low entopy metric, you can run a few k-means clustering models with different initial configurations, compare the results, and determine which one of the different initializations of configurations lead to the lowest inertia or distortion.

# Distance Metrics

Clustering methods rely very heavily on our definition of distance. Our choice of Distance Metric will be extremely important when discussing our clustering algorithms and to clustering success. 

Each metric has strengths and most appropriate use cases, but sometimes choosing a distance metric is also based on empirical evaluation to determine which metric works best to achieve our goals. 

These are the most common distance metrics:   

## Euclidean Distance

This one is the most intuitive distance metric, and that we use in K-means, another name for this is the L2 distance. You probably remember from your trigonometry classes.

We calculate (d) by taking the square root of the square of each of this changes (values). We can move this to higher dimensions for example 3 dimensions, 4 dimensions etc.  In general, for an n-dimensional space, the distance is: 

![image](https://user-images.githubusercontent.com/102208095/192229961-fa958098-2d69-44f1-b8f1-a1971a9d0f07.png)


## Manhattan Distance (L1 or City Block)

Another distance metric is the L1 distance or the Manhattan distance, and instead of squaring each term we are adding up the absolute value of each term. It will always be larger than the L2 distance, unless they lie on the same axis. We use this in business cases where there is very high dimensionality.  

As high dimensionality often leads to difficulty in distinguishing distances between one point and the other, the L1 score does better than the L2 score in distinguishing these different distances once we move into a higher dimensional space. 

## Cosine Distance

This is a bit less intuitive distance metric. What we really care about the Cosine Distance is the angle between 2 points, for example, for two given points A and B:

![image](https://user-images.githubusercontent.com/102208095/192230164-e33ff5b9-b133-4ec4-9fa6-738c51541878.png)

This metric gives us the cosine of the angle between the two vectors defined from the origin to two given points in a two-dimensional space. To translate this definition into higher dimensions, we take the dot product of the vectors and divide it by the norm of each point.

The key to the Cosine distance is that it will remain insensitive to the scaling with respect to the origin, which means that we can move some of the points along the same line and the distance will remain the same. So, any two points on that same array, passing through the origin will have a distance of zero from one another. 

### Euclidean VS Cosine distances

-          Euclidean distance is useful for coordinate based measurements.

-          Euclidean distance is more sensitive to curse of dimensionality

-          Cosine is better for data such as text where location of occurrence is less important. 

## Jaccard Distance

This distance is useful for texts and is often used to word occurrence. 

Consider the following example: 

![image](https://user-images.githubusercontent.com/102208095/192230338-36edda24-be45-496c-90f4-0494b18b132c.png)

# 2) Hierarchical Clustering

This clustering algorithm, will try to continuously split out and merge new clusters successively until it reaches a level of convergence. 

This algorithm identifies first the pair of points which has the minimal distance and it turns it into the first cluster, then the second pair of points with the second minimal distance will form the second cluster, and so on. As the algorithm continues doing this with all the pairs of closest points, we can turn our points into just one cluster, which is why HAC also needs a stopping criterion.

There are a few linkage types or methods to measure the distance between clusters. these are the most common:

**Single linkage:** minimum pairwise distance between clusters.

It takes the distance between specific points and declare that as the distance between 2 clusters and then it tries to find for all these pairwise linkages which one is the minimum and then we will combine those together as we move up to a higher hierarchy. 

Pros: It helps ensuring a clear separation between clusters.  

Cons: It won’t be able to separate out cleanly if there is some noise between 2 different clusters. 

**Complete linkage:** maximum pairwise distance between clusters. 

Instead of taking the minimum distance given the points within each cluster, it will take the maximum value. Then from those maximum distances it decides which one is the smallest and then we can move up that hierarchy. 

Pro: It would do a much better job of separating out the clusters if there’s a bit of noise or overlapping points of two different clusters.

Cons: Tends to break apart a larger existing cluster depending on where that maximum distance of those different points may end up lying  

**Average linkage:** Average pairwise distance between clusters. 

Takes the average of all the points for a given cluster and use those averages or clusters centroids to determine the distance between the different clusters. 

Pros: The same as the single and complete linkage. 

Cons: It also tends to break apart a larger existing cluster. 

**Ward linkage:** Cluster merge is based on inertia.

Computes the inertia for all pairs of points and picks the pair that will ultimately minimizes the value of inertia.

The pros and cons are the same as the average linkage. 
