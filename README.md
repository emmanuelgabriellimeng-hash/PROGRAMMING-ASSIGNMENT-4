# PA 4 – Data Wrangling and Data Visualization  

## Overview  
This programming assignment demonstrates how to use **Pandas** for data wrangling and **Matplotlib** for visualization. The program works on a dataset of ECE Board Exam results and applies filtering, computation of averages, and visual analysis. 

---

## Directory  
Problem Item 1:  
* 

Problem Item 2:  
* 

Program Link:  
* https://github.com/emmanuelgabriellimeng-hash/PROGRAMMING-ASSIGNMENT-4/blob/main/LIM_2ECEB_Experiment_4.ipynb

Download Excel File:  
* https://github.com/emmanuelgabriellimeng-hash/PROGRAMMING-ASSIGNMENT-4/blob/main/board2.xlsx

---


## ECE BOARD EXAM PROBLEM:

Using data wrangling and data visualization technique with storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.
1. Crea|te the following data frames based on the format provided:
        Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas

   <img width="609" height="107" alt="image" src="https://github.com/user-attachments/assets/d86bf4d8-3965-4e1f-86b2-251d8e0f9f19" />


a. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon

---

**Explanation:**  

1. Import the Pandas library.  
```python
import pandas as pd
````

2. Load the dataset `board2.csv` into a DataFrame.

```python
df = pd.read_csv("board2.csv")
```

3. Apply filtering conditions using `&`: Track is Instrumentation, Hometown is Luzon, and Electronics > 70.

```python
Instru = df[(df["Track"] == "Instrumentation") & 
            (df["Hometown"] == "Luzon") & 
            (df["Electronics"] > 70)][["Name", "GEAS", "Electronics"]]
```

4. Display the resulting DataFrame.

```python
Instru
```

**Example Output**

<img width="275" height="170" alt="image" src="https://github.com/user-attachments/assets/8496a5bc-58ba-4448-a6d4-e48b9f8ca22e" />

---

b. Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female

---

**Explanation:**

1. Compute the average score from Math, Electronics, GEAS, and Communication.

```python
df["Average"] = df[["Math","Electronics","GEAS","Communication"]].mean(axis=1)
```

2. Apply filtering conditions: Hometown is Mindanao, Gender is Female, and Average ≥ 55.

```python
Mindy = df[(df["Hometown"] == "Mindanao") & 
           (df["Gender"] == "Female") & 
           (df["Average"] >= 55)][["Name", "Track", "Electronics", "Average"]]
```

3. Display the resulting DataFrame.

```python
Mindy
```

**Example Output**

<img width="442" height="242" alt="image" src="https://github.com/user-attachments/assets/367f75a2-1c43-4600-8ff8-c7435a9cca77" />


---

2. Create a visualization that shows how the different features contributes to average grade. Does
chosen track in college, gender, or hometown contributes to a higher average score?

---

**Explanation:**

1. Group the dataset by Track, Gender, and Hometown, computing the mean of Average for each group.

```python
avg_by_track = df.groupby("Track")["Average"].mean()
avg_by_gender = df.groupby("Gender")["Average"].mean()
avg_by_hometown = df.groupby("Hometown")["Average"].mean()
```

2. Create a figure with three subplots to compare Track, Gender, and Hometown.

```python
fig, axes = plt.subplots(1, 3, figsize=(18,5))
```

3. Plot bar charts for each factor separately to compare their effect on averages.

```python
axes[0].bar(avg_by_track.index, avg_by_track.values, color="skyblue")
axes[0].set_title("Track vs Average")
axes[0].set_ylabel("Average Grade")
```

* For Track vs Average,

```python
axes[1].bar(avg_by_gender.index, avg_by_gender.values, color="lightgreen")
axes[1].set_title("Gender vs Average")
```

* For Gender vs Average,

```python
axes[2].bar(avg_by_hometown.index, avg_by_hometown.values, color="salmon")
axes[2].set_title("Hometown vs Average")
```

* For Hometown vs Average,.

4. Adjust layout and display the visualization.

```python
plt.tight_layout()
plt.show()
```

**Example Output:**

<img width="1493" height="408" alt="image" src="https://github.com/user-attachments/assets/174863e9-365e-4b16-9288-d26d41b4c252" />

* The results show that track, gender, and hometown have a slight effect on average scores. Differences between groups are minimal, with slight variations in track and hometown, and almost no difference between male and female students.
