# Kmeans-Clustering
Implemented Kmeans clustering Llyods Algorithm and Kmeans plus plus algorithm from scratch

Dataset
The dataset contains information on patients with diabetes who were admitted to 130 hospitals in
the United States between 1999 and 2008. The primary purpose of the dataset is to explore features
that affect readmission rates for diabetic patients.The dataset can be used for various purposes,
including exploring the relationship between various features like patient
condition,labtest,medications and readmission rates, developing predictive models for readmission,
and evaluating the quality of care provided by hospitals. The dataset can be used to identify the
relationship between various parameters and can be used by Doctors, researchers to identify the
mistakes or areas of improvements or what better could have been done , so that patient is not
readmitted. Also, identify some pattern or cluster in the data given all the features or identify the
main features affecting the readmission. The different data types that the dataset includes are integer
and object data. The dataset’s features include patient demographics, admission type and source,
diagnosis and procedure codes, lab tests, medications, length of stay,etc. The target variable is
whether or not the patient was readmitted to the hospital within 30 days of discharge. Overall there
are 101766 entries of data and 50 features/columns including the target variable.


Exploratory Data Analysis

Handling Missing Data
There are no null entries as such in data. But some of the columns contains ? Replacing
question mark with NAN. After doing that we can see the results and now this missing data
needs to be handled. ′race′,′ weight′,′ payercode′,′ medicalspecialty′,′ diag1′ ,′ diag′2,′ diag′3
Columns contains null data. Dropping the columns where the count of null data is almost
around 50 percent as they dont provide significant information.

Creating Histograms
The histogram plot of the age feature suggests that the data is skewed towards higher age, while
the histogram plot of the num lab procedures feature suggests that the data is skewed and
bimodal. Furthermore, the histogram plot of the num medication feature indicates that the
data is normally distributed and right-tailed.

Scatterplots
The scatter plot of time in hospital and num medications shows a positive relationship between
the two variables, which is also supported by the correlation matrix. The scatter plot also suggests that the
readmitted variable does not have a strong relationship with either variable.
Similarly, the scatter plot of num medications and num lab procedures shows a weak positive
relationship between the two variables, which is also supported by the correlation matrix. The scatter plot
also suggests that the readmitted variable does not have a strong relationship with either variable.

Implementation

Kmeans Llyod Algorithm

Stopping condition and convergence criterion

The k-means algorithm is a popular clustering
algorithm that aims to minimize the sum of squared distances between data points and their assigned
centroids. However, it may converge to a local minimum rather than the global minimum due to its
greedy nature. There can be various other reasons for the same such as noise or outliers in data or
high dimensionality in data or poor centroid initialization. Yes, bound on the iterate must be
included to have a balance between computational efficiency and convergence accuracy. The
algorithm should stop sometime and not continue indefinitely. To perform the clustering, the
algorithm assigns each data point to the closest cluster centroid and recalculates the centroids based
on the new assignments. The stopping condition can be the maximum number of iterations or when
error becomes constant and same centroids are generated. In our example it is τ , when the scalar
product between clusters is less than τ , the k means stops or the stopping conditon is met.The
choice of the stopping criterion is very important and is determined by user i.e it is a user defined
parameter. Various factors can be considered while deciding the value of stopping condition such as
time to run the code, computational limitations, expected accuracy,etc. The k-means algorithm is
sensitive to the initial choice of centroids, and different initializations may result in different local
optima. Therefore, it is recommended to run the algorithm multiple times with different
initializations and choose the best clustering based on the stopping criterion and any domain
knowledge about the expected number of cluster or stopping condition.

Time Complexity 

The time complexity is O(n ∗ d ∗ k ∗ i)

Here

n: the number of data points

d: the number of dimensions

k: the number of clusters

i: the number of iterations till stopping condition is met


Initialization of Centroids

Initializing the centroids marks the first step. There can be multiple ways to initialize the centroids such as
Random selection from the overall search space. Random selection from the domain of the data. We have
initialized the centroids by using domain approach. We have randomly selected the cluster centroid from
the domain. Value of eachco ordinate of the centroid is taken randomly from the domain of that feature
which contributes to that feature. For example if the domain values of a feature is between 1 and 100, we
have randomly chosen a value between 1 and 100. This helps in initializing the centroid co ordinate value
whihc is close to the actual dataset.

Maintaining k Centroids

In kmeans we need to maintain the k centroids at each and every iteration.There are many reasons we may
get an empty cluster.Various affecting factors are: Sometimes due to the random initialization of clusters
Quality of Data Choice of number of clusters It is possible that in a particular iteration, no data point is
mapped to a cluster. We may lose out on that cluster. So to avoid that we have used the co ordinates of
previous iteration to maintain same number of clusters throughout. But if this continues in many iterations
than it can be an indication of merging the nearest clusters with empty cluter or changing the number of
cluster i.e k value whihc is decided in the start.


Deciding Ties

K means is distance based greedy algorithm. It calculates the distance between each data point and
various clusters. The minimum distance is selected, but there is high chance that there is tie between
minimum distance of cluster and datapoints. There could be various techniques to handle such scenario,
which include: Random tie breaking - Any cluster out of the cluters at same distance is selected randomly.
Least assigned Cluster- In case 2 cluster are into tie break, we can check the datapoints assigned to each
clusters, and whichever has low data points that can be selected. This helps in removing imbalance
between clusters Highest assigned cluster- This is opposite of least assigned cluster method, here the
cluster which is assigned more datapoints is selected. As from the previous iteration, it has high
probability to get selected to maintain the number of points assigned. Selection of both the techniques
highly depends upon use case, domain knowledge and expected results.

Stopping Criteria

Deciding the stopping criteria is an important step in kmeans algorithm. There are various approaches to
stop kmeans, which includes: 1) Maximum iterations are reached 2) The cluster centroids are not changing
3) Convergence or global minima is reached 4) The sum of square error becomes constant over the
iterations 5) The magnitude of clusters (scalar product) becomes less than a threshold (τ ). We have used
the last approach. Here the distance between current centroid and previous centroid for consequtive
iterations is calculated , squared. This is done for all the clusters and the distance is added and finally
divided by k. When this value becomes less than threshold i.e τ the k means algorithm stops.

I have implemented the kmeans llyod algorithm for number of clusters ranging from 2 to 5. The method
involves initializing k centroids randomly. Then assigning clusters to each datapoint. Centroid is calculated
by taking mean if datapoints and this serve as new centroids. Have handled scenarios to maintain k centroids
always and handling ties,etc. After each iteration, calculated the tao i.e magnitude of scalar product between
the new cluster and old cluster. If the tao is below certain threshold, then the algorithm converges and these
are the final sets of centroids. Here the data for diabetes and new york comments had a target variable each
having two target classes. So to calculate the error we need to merge the classes. Have merged the clusters
into 2 as per the class of target variable by calculating distance metric. Whichever distance is minimum,that
distance from cluster to target variable is selected for merging clusters such that 2 classes are remaining.
Have ran this algorithm for diabetes data set and new york dataset of comments. Have performed required
EDA on datasets.

Evaluation Metric

From the line plot below for error and sum of square error with number of clusters it can be seen that error
graph balances out with increase in the number of clusters i.e from 2 to 5. The error is decreasing with increase 
in number of clusters. Even the sum of square error shows a decrease with increase in the number of
clusters. From the box plot for error wrt number of clusters, shows the median error for each cluster shows
a gradual decrease. The box plot of runtime shows that with increase in number of clusters the median run
time also increases with increase in number of clusters.

![image](https://user-images.githubusercontent.com/37649277/236167677-65f74dbc-c263-4434-89c2-f8e4782fd471.png)
![image](https://user-images.githubusercontent.com/37649277/236167692-ebb0833f-dffe-4aeb-b523-407d9a59841d.png)
![image](https://user-images.githubusercontent.com/37649277/236167716-92bd3f3e-67ce-43ca-9631-6b3c87fa800e.png)


Kmeans Llyod Algorithm with SSE convergence

I have implemented the kmeans llyod algorithm with sse convergence for number of clusters ranging from
2 to 5. The method is similar to kmeans llyod with different convergence criteria. Here sum of square
error (SSE) is used at the stopping criteria. When the SSE becomes constant or the new iteration reduces
the SSE by certain threshold, then the algorithm stops. The threshold of SSE reduction percentage is user
defined.Rest all the functions are similar to kmeans Llyods. According to me, SSE convergence can be a
better metric to evaluate the quality of clusters. Improving the cohesion among the datapoints assigned to
same cluster and when it reaches a certain threshold the algorithm converges. Have ran this algorithm for
diabetes data set and new york dataset sample of comments. Have performed required EDA on datasets.

Evaluation Metric

From the line plot below for error and sum of square error with number of clusters it can be seen that error
graph balances out with increase in the number of clusters i.e from 2 to 5. The error is decreasing with
increase in number of clusters. Firstly there is a small increase and then the error deceases with increase
in clusters.The sum of square error shows a decrease with increase in the number of clusters. From the box
plot for error wrt number of clusters, shows the median error for each cluster shows a gradual decrease after
a small rise initially. The box plot of runtime shows that with increase in number of clusters the median
run time also increases with increase in number of clusters. When the runtime of kmeans llyos is compared
to runtime of kmeans with sse convergence it can be seen that for less number of clusters the median run
time of kmeans llyod is more that that of kmeans with SSE convergence i.e it takes more time to converge.
But when number of clusters increases i.e becomes 5, the median time to converge for kmeans with sse
convergence is more than that of kmeans llyod. When number of clusters become more run time of kmeans
lyods is less than that of sse converged kmeans

![image](https://user-images.githubusercontent.com/37649277/236168140-5620bc4a-393d-4c94-937a-269b48d94796.png)
![image](https://user-images.githubusercontent.com/37649277/236168202-53f2802e-b478-451c-91c8-f53176dc0d2c.png)
![image](https://user-images.githubusercontent.com/37649277/236168232-04c0333a-88c9-40a1-a6cf-a577abbb77f3.png)
![image](https://user-images.githubusercontent.com/37649277/236168246-bb94f810-dd25-424c-beb5-6f5877a84cc1.png)



kmeans plus plus algorithm

I have implemented the kmeans plus plus algorithm for number of clusters ranging from 2 to 5. The method
is similar to kmeans llyod with different centroid initialization. Here the first centroid is chosen randomly
from the domain of data. For rest k-1 centroids, we follow a different iterative approach. The second cluster is
initialized based on the first centroid. The third centroid requires data of first two centroids. The methodolgy
includes,selecting the first centroid randomly from domain of data. Then second cluster is at the farthest
distance from that cluster. In this way iteratively we initialize k centroids. As the centroid initialization is
not random, it is expected that the inter cluster distance will be more and intra cluster distance bewteen
points and centroid will be less.
The K-means++ algorithm selects the centroids in following way
Step1: Choosing the first centroid at random from the data points.
Step2: For each remaining data point, computing its distance to the nearest centroid that has already been
chosen.
Step3: Selecting the next centroid randomly from the remaining data points, with probability proportional
to the squared distance to the nearest centroid. Repeating steps 2-3 until all K centroids have been chosen.
The main idea behind K-means++ initialization is to select centroids that are well spread out across the data
points. By selecting the next centroid from the remaining data points with a probability that is proportional
to the squared distance to the nearest centroid, K-means++ initialization ensures that data points that are
far away from existing centroids are more likely to be selected as new centroids. Hence the sum of square
error is expected to be less. Rest the stopping conditions and other steps are similar to that of kmeans llyods
Have ran this algorithm for diabetes data set and new york dataset sample of comments. Have performed
required EDA on datasets.

Evaluation Metrics

From the line plot below for error and sum of square error with number of clusters it can be seen that error
graph balances out with increase in the number of clusters i.e from 2 to 5. The error is decreasing with
increase in number of clusters. At end there is slight increase in the error.The sum of square error shows
an initial small increase with increase in the number of clusters and then decreases with increase in clusters.
From the box plot for error wrt number of clusters, shows the median error for each cluster shows a gradual
decrease . The box plot of runtime shows that with increase in number of clusters the median run time also
increases with increase in number of clusters.
When the runtime of kmeans plus plus is compared to runtime of kmeans with sse convergence and kmeans
llyod it can be seen that kmeans plus plus have more median running time than other two variations.

![image](https://user-images.githubusercontent.com/37649277/236168511-318626b0-fd83-4749-96ac-93e1d1bf6aa9.png)
![image](https://user-images.githubusercontent.com/37649277/236168531-3d4547a5-c2e4-4db9-86f5-63305b88fa66.png)
![image](https://user-images.githubusercontent.com/37649277/236168543-12f69012-d1fb-454a-8882-dbf0d244fb83.png)
![image](https://user-images.githubusercontent.com/37649277/236168562-fa539577-5d00-43f3-82c4-d05dc413f352.png)
 
The code is also executed on other datasets.
Please refer the codes and the report to get more details
