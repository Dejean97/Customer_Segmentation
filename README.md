# Customer_Segmentation

The aim of this project was to examine online sales data to determine the potential value of a set of customers, clustering them together which could be used to develop targeted marketing strategies to improve future sales. I'm particularly practicing this on a simple scenario as I plan to use it on an upcoming project involving a little more complexity.

Inspiration for this project came from the [The AI University](https://www.youtube.com/channel/UCv6Uw36LRbYnX4HDxKPguKg) Youtube channel.

The data used for this project is the online retail [dataset](http://archive.ics.uci.edu/ml/machine-learning-databases/00352/).

## Project Summary

Having downloaded the raw sales data, this was then read into pandas for exploration and data cleaning.

### Data Cleaning/Exploration

- Basic exploration of thTe data discovered of the 541,909 rows and 8 columns there were 25,900 unique transactions and 4,372 unique customers.
- When splitting the distinct count of customers by country, it was identified 3,950 customer were from the UK. All non-UK customer transactions were dropped from the dataset.
- There were missing values in item description and customer ID, any records containing these missing values were dropped. 
- The numeric fields of quantity and unit price were examined for their minimum value, any values below 0 were dropped from the dataset resulting a dataset of 354,345 rows.
- Finally, a new column was added simply multiplying order quantity and unit price, creating a total amount for each row. This resulting dataset was saved as a clean dataset ready for analysis.

### Recency, Frequency & Monetary (RFM) Modelling

RFM segmentation is a great method to identify groups of customers for special treatment. A detailed description and step by step methodology can be found on this Optimove [post](https://www.optimove.com/resources/learning-center/rfm-segmentation).

- The previously cleaned and reduced dataset was read in via pandas.
- A 'maximum' date was created as a benchmark for calcuating transaction recency.
- Values for Recency, Frequency and Monetary were then calculated for each customer:
    - Recency = Days since last transaction
    - Frequency = Total number of transactions
    - Monetary = Sum total amount of all transactions
 - This resulted in a new dataframe consisting of Customer ID, Recency value, Frequency value and Monetary value.
 - Standard descriptive statistics and distribution plots were generated for each, all three were right skewed and this will be addressed later.

![Recency Dist

 - Quantiles at 25%, 50% and 75% were created and these will be used to create a label for each customer with regards to which quartile (1, 2, 3 or 4) they reside within for each RFM attribute.
 - A function was then defined to assign these quartile labels based on the values, with 1-4 lower being better for recency and 4-1 with higher be better for monetary and frequency.
 - These labels were then combined to make a group (e.g. 441) and summed to create a score ranging from 3-12.
 - Customer tiers (bronze, silver, gold and platinum) were then created by generating for cuts of the final RFM score data (platinum having lowest scores and being most valuable customers, bronze having highest score and being least valuable customers).

Scatter graphs were plotted, showing the RFM attributes by customer tier:

- Frequency by Recency


![FreqxRec](https://github.com/Dejean97/Customer_Segmentation/blob/main/FreqxRec.png)

- Monetary by Frequency


![MonxFreq](https://github.com/Dejean97/Customer_Segmentation/blob/main/MonxFreq.png)

- Monetary by Recency


![MonxRec](https://github.com/Dejean97/Customer_Segmentation/blob/main/MonxRec.png)

The resulting dataset, to be used in the K-means clustering, consisted of the:
- Customer ID
- Recency value
- Frequency value
- Monetary value
- Recency quartile
- Frequency quartile
- Monetary quartile
- RFM group
- RFM score
- Customer tier

### K-Means Clustering

K-means clustering is a simple but popular algorithm, for grouping similar data points together (into clusters) and discover underlying patterns. A cluster refers to a collection of data points aggregated together because of certain similarities. In this scenario the algorithm is 'grouping' customers together based on online retail purchasing similarities.

Prior to carrying out the clustering, the RFM attributes underwent normalisation using log transform to ensure they met statistical assumptions. To ensure this worked correctly, a function was written to set any values, that were less than or equal to 0, to 1.


From here the elbow method was used to identify the optimal value for k, in this instance 3 clusters was optimal. More information on the Elbow method can be found in this Medium [post](https://medium.com/analytics-vidhya/elbow-method-of-k-means-clustering-algorithm-a0c916adc540), written by [S Joel Franklin](https://medium.com/@joel_34096).


### Roundup

This project allowed me to learn new skills in python as well as new analytical methods (RFM modelling and K-Means clustering). I believe customer segmentation is a very valuable and applicable skill,  I expect to utilise this in my next project which will be an end-to-end analytics consulting task.
