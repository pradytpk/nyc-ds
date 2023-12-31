# Exploring NYC Public School Test Result Scores

![New York City schoolbus](schoolbus.jpg)

Photo by [Jannis Lucas](https://unsplash.com/@jannis_lucas) on [Unsplash](https://unsplash.com).
<br>

Every year, American high school students take SATs, which are standardized tests intended to measure literacy, numeracy, and writing skills. There are three sections - reading, math, and writing, each with a maximum score of 800 points. These tests are extremely important for students and colleges, as they play a pivotal role in the admissions process.

Analyzing the performance of schools is important for a variety of stakeholders, including policy and education professionals, researchers, government, and even parents considering which school their children should attend.

You have been provided with a dataset called `schools.csv`, which is previewed below.

You have been tasked with answering three key questions about New York City (NYC) public school SAT performance.

```python
# Re-run this cell
import pandas as pd

# Read in the data
schools = pd.read_csv("schools.csv")

# Preview the data
schools.head()

# Start coding here...
# Add as many cells as you like...
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>borough</th>
      <th>building_code</th>
      <th>average_math</th>
      <th>average_reading</th>
      <th>average_writing</th>
      <th>percent_tested</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>New Explorations into Science, Technology and ...</td>
      <td>Manhattan</td>
      <td>M022</td>
      <td>657</td>
      <td>601</td>
      <td>601</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Essex Street Academy</td>
      <td>Manhattan</td>
      <td>M445</td>
      <td>395</td>
      <td>411</td>
      <td>387</td>
      <td>78.9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lower Manhattan Arts Academy</td>
      <td>Manhattan</td>
      <td>M445</td>
      <td>418</td>
      <td>428</td>
      <td>415</td>
      <td>65.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>High School for Dual Language and Asian Studies</td>
      <td>Manhattan</td>
      <td>M445</td>
      <td>613</td>
      <td>453</td>
      <td>463</td>
      <td>95.9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Henry Street School for International Studies</td>
      <td>Manhattan</td>
      <td>M056</td>
      <td>410</td>
      <td>406</td>
      <td>381</td>
      <td>59.7</td>
    </tr>
  </tbody>
</table>
</div>

Create a pandas DataFrame called best_math_schools containing the "school_name" and "average_math" score for all schools where the results are at least 80% of the maximum possible score, sorted by "average_math" in descending order.

```python
best_math_schools = schools[schools["average_math"] >= 640][["school_name", "average_math"]].sort_values("average_math", ascending=False)
best_math_schools
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>average_math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>88</th>
      <td>Stuyvesant High School</td>
      <td>754</td>
    </tr>
    <tr>
      <th>170</th>
      <td>Bronx High School of Science</td>
      <td>714</td>
    </tr>
    <tr>
      <th>93</th>
      <td>Staten Island Technical High School</td>
      <td>711</td>
    </tr>
    <tr>
      <th>365</th>
      <td>Queens High School for the Sciences at York Co...</td>
      <td>701</td>
    </tr>
    <tr>
      <th>68</th>
      <td>High School for Mathematics, Science, and Engi...</td>
      <td>683</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Brooklyn Technical High School</td>
      <td>682</td>
    </tr>
    <tr>
      <th>333</th>
      <td>Townsend Harris High School</td>
      <td>680</td>
    </tr>
    <tr>
      <th>174</th>
      <td>High School of American Studies at Lehman College</td>
      <td>669</td>
    </tr>
    <tr>
      <th>0</th>
      <td>New Explorations into Science, Technology and ...</td>
      <td>657</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Eleanor Roosevelt High School</td>
      <td>641</td>
    </tr>
  </tbody>
</table>
</div>

Identify the top 10 performing schools based on scores across the three SAT sections, storing as a pandas DataFrame called top_10_schools containing the school name and a column named "total_SAT", with results sorted by total_SAT in descending order.

```python
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]
top_10_schools = schools.groupby("school_name", as_index=False)["total_SAT"].mean().sort_values("total_SAT", ascending=False).head(10)
top_10_schools
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>total_SAT</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>325</th>
      <td>Stuyvesant High School</td>
      <td>2144.0</td>
    </tr>
    <tr>
      <th>324</th>
      <td>Staten Island Technical High School</td>
      <td>2041.0</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Bronx High School of Science</td>
      <td>2041.0</td>
    </tr>
    <tr>
      <th>188</th>
      <td>High School of American Studies at Lehman College</td>
      <td>2013.0</td>
    </tr>
    <tr>
      <th>334</th>
      <td>Townsend Harris High School</td>
      <td>1981.0</td>
    </tr>
    <tr>
      <th>293</th>
      <td>Queens High School for the Sciences at York Co...</td>
      <td>1947.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Bard High School Early College</td>
      <td>1914.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>Brooklyn Technical High School</td>
      <td>1896.0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>Eleanor Roosevelt High School</td>
      <td>1889.0</td>
    </tr>
    <tr>
      <th>180</th>
      <td>High School for Mathematics, Science, and Engi...</td>
      <td>1889.0</td>
    </tr>
  </tbody>
</table>
</div>

Locate the NYC borough with the largest standard deviation for "total_SAT", storing as a DataFrame called largest_std_dev with "borough" as the index and three columns: "num_schools" for the number of schools in the borough, "average_SAT" for the mean of "total_SAT", and "std_SAT" for the standard deviation of "total_SAT". Round all numeric values to two decimal places.

```python
boroughs = schools.groupby("borough")["total_SAT"].agg(["count", "mean", "std"]).round(2)
largest_std_dev = boroughs[boroughs["std"] == boroughs["std"].max()]
largest_std_dev = largest_std_dev.rename(columns={"count": "num_schools", "mean": "average_SAT", "std": "std_SAT"})
largest_std_dev
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_schools</th>
      <th>average_SAT</th>
      <th>std_SAT</th>
    </tr>
    <tr>
      <th>borough</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Manhattan</th>
      <td>89</td>
      <td>1340.13</td>
      <td>230.29</td>
    </tr>
  </tbody>
</table>
</div>
