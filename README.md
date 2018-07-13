>Henry Nguyen
<br>December 4 2017</br>

# Extreme Programming: Distributed Programming and Cluster Computing with Big Data

## Details of Implementation and Design Choices

- The code used to implement the algorithms are in separate text files and are accordingly named. The code is written in an open source programming language called ‘R’. Copy and pasting the code into the R software (can be retrieved from https://www.r-project.org/) will execute the instructions directly since it is an interpreted language. The dataset used in this project is from Kaggle and contains data regarding to diamonds (https://www.kaggle.com/shivam2503/diamonds/data) :
- A data frame with 53940 rows and 10 variables:
  - price price in US dollars (\$326--\$18,823)
  - carat weight of the diamond (0.2--5.01)
  - cut quality of the cut (Fair, Good, Very Good, Premium, Ideal)
  - color diamond colour, from J (worst) to D (best)
  - clarity a measurement of how clear the diamond is (I1 (worst), SI2, SI1, VS2, VS1, VVS2, VVS1, IF (best))
  - x length in mm (0--10.74)
  - y width in mm (0--58.9)
  - z depth in mm (0--31.8)
  - depth total depth percentage = z / mean(x, y) = 2 * z / (x + y) (43--79)
  - table width of top of diamond relative to widest point (43--95)
## Linear Regression
- Linear regression is used to describe the relationship between the dependent variable and the independent variable.
- For linear regression, I first use the read.csv() function to read in the dataset. I then assign it to a variable named “diamonds”.
- Use the attach() function to attach the .csv file. I put diamonds in the parameter.
- Use linear regression using the lm() function to model the relationship between the dependent variable “price”, and the independent variable “carat”. I assign the function to a variable called “linmod”.
- The “price” variable is measured in US dollars and the “carat” variable is the weight of the diamond.
- Calling linmod gives use the coefficients, in which the intercept is -2256 and carat is 7756. This tells us the constant value -2256 is the intercept, and the slope for carat is 7756, meaning that for every increase of 1 for carat, the price increases by $7756.
- Use the plot() function to create a scatterplot, using the arguments: price and carat.
- Use the abline() function to create a regression line, using linmod as the argument. This produces a graph shown in the last page.
- You can also call the summary() function to get residuals and coefficients. 

## K-means Clustering
- K-means clustering to find a small pattern in the data (between price and carat)
- As above, I first use the read.csv() function to read in the dataset. I then assign it to a variable named “diamonds”.
- Use the attach() function to attach the .csv file. I put diamonds in the parameter.
- Create a subset by assigning the indexes that I want, in this case, 2 (carat) and 8 (price) using the concatenation function c() and diamond[] vector. I assign it to the variable “subset”
- Set the seed value to 10 using the seed function set.seed().
- Calculate kmeans by using the kmeans() function, and passing the arguments: subset, 2, nstart=10. The parameter arguments, from left to right, stands for data, number of clusters, and are number of random sets. I assign this to a variable named Kcluster.
- Create a plot showing the two clusters by using the plot() function. The arguments passed are: subset, col=(Kcluster$cluster +1), main=”K-means result with 2 clusters”). The arguments, from left to right, are data, column where “cluster” is a built-in column (by R) of “Kcluster” and the “+1” changes cluster colors to red and green (default is black and red), and “main” is the title of the graph.
- This gives us 2 clusters that tell us that each cluster represents a different price range, where one (red) represents approximately above $7000, and one (green) below the $7000 range. The graph is in the last page.

## Hierarchical Clustering
- As above, I first use the read.csv() function to read in the dataset. I then assign it to a variable named “diamonds”.
- Use the attach() function to attach the .csv file. I put diamonds in the parameter.
- Create a subset from diamonds by using the sample() function. I then assign it the vector “mySample”.
- Create a distance matrix by using the dist() function and as.matrix() function. I pass mySample with the columns carat (2) and price (8) via c() function. I then assign it to the vector “distanceMatrix”.
- Create an hierarchical cluster by using the hclust() function, passing distanceMatrix in the parameter. I then assign it the variable “hc”.
- Call the plot() function and pass hc as the argument. This gives us a dendogram, in which we can decide which value of the height as a means to cluster. For example, cutting at height 10000 gives us two distinct clusters as shown in the graph (in the last page). 
- A cutree() function with the arguments hc and 3 is assigned to a variable called “clusterCut”, where hc is the hierarchical cluster, and 3 is the number of distinct clusters. 
- table() function is called to see the number of values for each carat column is in which cluster. It takes the arguments: clusterCut and mySample$carat.

## Problems encountered
- Printing out values from the dataset results in enormous amount of outputted values. 
- Graphs are full of data points because of the enormous sets.
  - These two problems could be resolve by taking a small random sample.
- Regression line is hard to see.
- Creating the distance matrix, it can take a long time to process if the file size is too big. In my case, I had to subset to 50 samples, and even then, it took a while.
- Producing the hierarchical cluster using the hclust() function, passing an argument can either be rejected by the R software as being too big or it will take a long time to process. In my case, I had to create a subset or else it gives a message telling me the vector size is 10.8 Gb.

## Evaluation
<br> Assuming the user using the code is somewhat knowledgeable in R, they should be able to implement the code(s) with easy understanding; some adjustments such as reading in a different data set or being able to interpret the results should make this project a simple solution or example for programmers. These implementations use the entire dataset, so the programmer would need to either read in a smaller set or create subsets (as shown in the K-means clustering implementation). The dataset is massive and I did little to shorten it, so it can be overwhelming (even when I reduced it to a sample size of 50 in the hierarchical clustering implementation). </br>

## Conclusion
<br> The linear regression model produces a graph that shows a relationship between x and y, and a summary that includes residuals and coefficients. The K-means clustering produces a graph the colors and separates data points based on the cluster. The Hierarchical clustering algorithm produces a dendrogram. All implementation essentially works, in which some details can be added, for example, hierarchical clustering could use better cluster cutting for character variables instead of numeric. Although none of these implementations used any library packages (other than the default built-in functions), there are many packages on the Internet that can be imported and are likely better than the code I provided. </br> 


## Graphs
 
![Scatterplot](/output/scatterplot.png  "Scatterplot")
![K-means Clustering](/output/KMC.png  "K-means Clustering")
![Cluster Dendogram](/output/ClusterDendogram.png  "Cluster Dendogram")
 
 
