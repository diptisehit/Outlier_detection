# What are Outliers?

an Outlier is an observation in a given dataset that lies far from the rest of the observations. 

An outlier may occur due to the variability in the data(not an error), or due to experimental error/human error. The trade-off is between the loss of accuracy if we throw away “good” observations, and the bias of our estimates if we keep “bad” ones.

Mean’ is the only measure of central tendency that is affected by the outlier treatment which in turn impacts Standard deviation.

# Detecting Outliers or anomaly detection:

Below are some of the techniques of detecting outliers

1. Boxplots : For visualizing outliers
   
   plt.boxplot(sample, vert=False)
   
   ![image](https://github.com/user-attachments/assets/0d404254-913d-468d-b211-046c05cac83c)


   IQR = Q3-Q1
   
2. Z-score :

   Any data point whose Z-score falls out of 3rd standard deviation is an outlier treatment.

   ![image](https://github.com/user-attachments/assets/34851566-9cbf-4315-bda7-f664c27f6847)


   - loop through all the data points and compute the Z-score using the formula (Xi-mean)/std.
   - define a threshold value of 3 and mark the datapoints whose absolute value of Z-score is greater than the threshold as outliers.
     
3. Inter Quantile Range(IQR) : Data points that lie 1.5 times of IQR above Q3 and below Q1 are outliers.

  ![image](https://github.com/user-attachments/assets/8a48d9a4-286b-48f7-a591-143e41e97354)


   positive outliers : Q3 + (1.5*IQR)

   negative outlier : Q1 - (1.5*IQR)


# How to Handle Outliers?

1. Trimming/Remove the outliers by stakeholders confirmation.Although it is not a good practice to follow.
 
2. Quantile Based Flooring and Capping /  Winsorization
  
tenth_percentile = np.percentile(sample, 10)  # Computing 10th, 90th percentiles and replacing the outlier treatment in python

ninetieth_percentile = np.percentile(sample, 90) 

print(tenth_percentile, ninetieth_percentile)

b = np.where(sample<tenth_percentile, tenth_percentile, sample)

b = np.where(b>ninetieth_percentile, ninetieth_percentile, b)

print("New array:",b)

3. Transformation : Transform the variable to induce normality. Use QQ plots (quantile-quantile plots) to visually check if the transformed data is closer to a normal distribution.
   - Log transformation : Log transformations are effective for right-skewed data, compressing the range and making outliers less extreme. 
   - squareroot transformation : Square root transformations are useful for count data and moderate skewness. 
   - cuberoot transformation : Cube root transformations are beneficial when dealing with negative values.

4. Regularisation : using lasso,ridge or elasticnet

5. Employing algorithms that are less sensitive to outliers, such as tree-based models .
