### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 07-08-26
### AIM: 
To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.

### Program:
```
# Visitor segmentation based on characteristics

# Read the data
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

df = pd.read_csv("/content/clustervisitor.csv")

# Display dataset
print(df)

# Select characteristics for clustering (Age)
data = df[['Age']].values

# Number of clusters
k = 3

# Initialize cluster centers randomly
np.random.seed(42)
centers = data[np.random.choice(len(data), k, replace=False)]

# Repeat clustering process
for i in range(10):

    # Assign data points to nearest center
    clusters = []

    for point in data:
        distance = [abs(point[0] - center[0]) for center in centers]
        clusters.append(distance.index(min(distance)))

    clusters = np.array(clusters)

    # Update cluster centers
    for j in range(k):
        if len(data[clusters == j]) > 0:
            centers[j] = np.mean(data[clusters == j], axis=0)

# Add cluster labels
df['Segment'] = clusters

# Display segmented visitors
print("\nVisitor Segmentation:")
print(df)

# Scatter plot
plt.figure(figsize=(8,6))

plt.scatter(df['Age'], df['Segment'], s=100)

plt.xlabel("Age")
plt.ylabel("Segment")
plt.title("Visitor Segmentation using Clustering")

plt.grid(True)
plt.show()
```
### Output:
<img width="620" height="652" alt="image" src="https://github.com/user-attachments/assets/c56eb57d-f647-4734-9a0e-a5976d0b1bd3" />

<img width="655" height="678" alt="image" src="https://github.com/user-attachments/assets/f936bba0-bc28-4ab8-84d4-948273a822a5" />

<img width="1060" height="628" alt="image" src="https://github.com/user-attachments/assets/7e4fc460-1e76-406b-af57-e0301833a77c" />




### Visualization:
```
# Create a list to store counts of visitors in each age group
visitor_counts = []

# Count visitors in each age group
age_groups = {
    "Young": df[df['Age'] <= 30],
    "Middle": df[(df['Age'] > 30) & (df['Age'] <= 50)],
    "Old": df[df['Age'] > 50]
}

for group, visitors in age_groups.items():
    visitor_counts.append(len(visitors))

# Define age group labels and plot a bar chart
age_group_labels = list(age_groups.keys())

plt.figure(figsize=(8, 6))
plt.bar(age_group_labels, visitor_counts, color='skyblue')
plt.xlabel('Age Groups')
plt.ylabel('Number of Visitors')
plt.title('Visitor Distribution Across Age Groups')
plt.show()
```
### Output:

<img width="972" height="623" alt="image" src="https://github.com/user-attachments/assets/93c1567d-3493-43c8-822e-b5d34acb4f89" />

### Result:
Thus,the cluster and visitor segmentation for navigation patterns was implemented successfully in python.
