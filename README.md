====================================================

Machine Learning Using NumPy – From Scratch

====================================================



Project Name   : NUMPYproject

Notebook File : Numpy-Ml-From-Scratch.ipynb



----------------------------------------------------

Project Overview

----------------------------------------------------

This project explains how Machine Learning algorithms work internally by

building them completely from scratch using only NumPy and Matplotlib.



• No ML libraries like scikit-learn, pandas, TensorFlow, or PyTorch are used

• Focus is on understanding logic, formulas, and learning process

• Everything is implemented inside a single Jupyter Notebook

• Step-by-step implementation with comments, formulas, examples, and graphs

• Visualizations are used to clearly show how learning happens



----------------------------------------------------

1\. Linear Regression

----------------------------------------------------

Definition:

Linear Regression is used to find a straight line that best represents the

relationship between input data and output values.



Simple Explanation:

• Used when the output is a number

• Tries to draw a line close to all data points



Examples:

• Predict marks from study hours

• Predict house price from house size



Formula:

Prediction = weight × input + bias



Meaning:

• weight → controls the slope of the line

• bias  → shifts the line up or down

• input → data value



Learning Process:

• Predict output using the line

• Calculate error with actual value

• Update weight and bias to reduce error



----------------------------------------------------

2\. Logistic Regression

----------------------------------------------------

Definition:

Logistic Regression is used for classification problems where output is

0 or 1 (Yes or No).



Simple Explanation:

• Used to decide between two classes

• Works using probability



Examples:

• Pass or Fail

• Spam or Not Spam



Formula:

Sigmoid = 1 / (1 + e⁻ˣ)



Meaning:

• Converts values into range 0 to 1

• Near 1 → Yes

• Near 0 → No



Decision Rule:

• Value ≥ 0.5 → Class 1

• Value < 0.5 → Class 0



----------------------------------------------------

3\. K Nearest Neighbors (KNN)

----------------------------------------------------

Definition:

KNN makes predictions based on the closest data points.



Simple Explanation:

• Looks at nearby points to decide

• No training phase required



Examples:

• Movie recommendation

• Friend suggestion



Distance Formula:

Distance = √\[(x₂ − x₁)² + (y₂ − y₁)²]



Meaning:

• Measures how close two points are

• Smaller distance means closer points



Decision Process:

• Select K nearest neighbors

• Choose the most common class



----------------------------------------------------

4\. K-Means Clustering

----------------------------------------------------

Definition:

K-Means is an unsupervised algorithm used to group data into clusters

without predefined labels.



Simple Explanation:

• Groups data based on similarity

• No output labels are given



Examples:

• Customer segmentation

• Market analysis



Center Formula:

Center = Average of all points in a cluster



Working Steps:

• Choose random cluster centers

• Assign points to nearest center

• Update center positions

• Repeat until centers stop moving



----------------------------------------------------

5\. Principal Component Analysis (PCA)

----------------------------------------------------

Definition:

PCA is used to reduce data dimensions while keeping important information.



Simple Explanation:

• Removes unnecessary features

• Keeps the most useful data



Examples:

• Image compression

• Faster data processing



Main Idea:

• Find direction with maximum data spread



Variance:

• Shows how much the data is spread



Result:

• Data is reduced to fewer dimensions



----------------------------------------------------

Conclusion

----------------------------------------------------

This project is ideal for:

• Beginners and students

• Interview preparation

• Resume and portfolio showcase



It demonstrates:

• Strong Machine Learning fundamentals

• Mathematical understanding

• Clean visualization

• Pure NumPy-based implementation

----------------------------------------------------



