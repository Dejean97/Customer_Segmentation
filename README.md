# Customer_Segmentation

The aim of this project was to examine online sales data to determine the potential value of a set of customers, clustering them together which could be used to develop targeted marketing strategies to improve future sales.

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


### K-Means Clustering

Elbow method Medium [post](https://medium.com/analytics-vidhya/elbow-method-of-k-means-clustering-algorithm-a0c916adc540), written by [S Joel Franklin](https://medium.com/@joel_34096).


### Roundup

This project allowed me to learn new skills in python as well as new analytical methods (RFM modelling and K-Means clustering). I believe customer segmentation is a very valuable and applicable skill,  I expect to utilise this in my next project which will be an end-to-end analytics consulting task.
