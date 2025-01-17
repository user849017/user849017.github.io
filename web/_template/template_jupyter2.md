---
layout: template2
comments: false
output:
    html_document:
        toc: true
        toc_float: true
        toc_depth: 3
---

# Introduction

(expliquer ce sur quoi porte cette article)
In this article, ...

 we are looking at the SAT scores of high schoolers in the US along with other information. The SAT (Scholastic Aptitude Test) is a test that high schoolers take in the US before applying to college. Colleges take the test scores into account when making admissions decisions, so it is fairly important. The test is divided into 3 sections, each of which is scored out of 800 points. The total score is out of 2400...
High schools are often ranked by their average SAT scores, and high SAT scores are considered a sign of how good a school district is.

There have been allegations about the SAT being unfair to certain racial groups in the US. Doing this analysis on New York City data will help shed some light on the fairness of the SAT.


```python
import pandas as pd
import numpy as np
```

# Data description


```python
data = {}
```

## SAT scores by school
The most recent school level results for New York City on the SAT. Results are available at the school level for the graduating seniors of 2012. Records contain 2012 College-bound seniors mean SAT scores taken during SY 2012.


```python
data["sat_results"] = pd.read_csv("../Data/us_sat/{0}.csv".format("SAT_Results"))
data["sat_results"].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DBN</th>
      <th>SCHOOL NAME</th>
      <th>Num of SAT Test Takers</th>
      <th>SAT Critical Reading Avg. Score</th>
      <th>SAT Math Avg. Score</th>
      <th>SAT Writing Avg. Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01M292</td>
      <td>HENRY STREET SCHOOL FOR INTERNATIONAL STUDIES</td>
      <td>29</td>
      <td>355</td>
      <td>404</td>
      <td>363</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01M448</td>
      <td>UNIVERSITY NEIGHBORHOOD HIGH SCHOOL</td>
      <td>91</td>
      <td>383</td>
      <td>423</td>
      <td>366</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01M450</td>
      <td>EAST SIDE COMMUNITY SCHOOL</td>
      <td>70</td>
      <td>377</td>
      <td>402</td>
      <td>370</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01M458</td>
      <td>FORSYTH SATELLITE ACADEMY</td>
      <td>7</td>
      <td>414</td>
      <td>401</td>
      <td>359</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01M509</td>
      <td>MARTA VALLE HIGH SCHOOL</td>
      <td>44</td>
      <td>390</td>
      <td>433</td>
      <td>384</td>
    </tr>
  </tbody>
</table>
</div>



## 2010-2011 Class Size - School-level detail
Average class sizes for each school, by grade and program type (General Education, Self-Contained Special Education, Collaborative Team Teaching (CTT)) for grades K-9 (where grade 9 is not reported by subject area), and for grades 5-9 (where available) and 9-12, aggregated by program type (General Education, CTT, and Self-Contained Special Education) and core course (e.g. English 9, Integrated Algebra, US History, etc.).

Class size data is based on January 28, 2011 data.

*Grade 9 Official Class data is included for 0K-09 schools. Core Course information for these sections is not reported.

link to the data: https://data.cityofnewyork.us/Education/2010-2011-Class-Size-School-level-detail/urz7-pzb3


```python

```


```python
data["class_size"] = pd.read_csv("../Data/us_sat/{0}.csv".format("Class_Size_-_School-level_detail"))
data["class_size"].head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CSD</th>
      <th>BOROUGH</th>
      <th>SCHOOL CODE</th>
      <th>SCHOOL NAME</th>
      <th>GRADE</th>
      <th>PROGRAM TYPE</th>
      <th>CORE SUBJECT (MS CORE and 9-12 ONLY)</th>
      <th>CORE COURSE (MS CORE and 9-12 ONLY)</th>
      <th>SERVICE CATEGORY(K-9* ONLY)</th>
      <th>NUMBER OF STUDENTS / SEATS FILLED</th>
      <th>NUMBER OF SECTIONS</th>
      <th>AVERAGE CLASS SIZE</th>
      <th>SIZE OF SMALLEST CLASS</th>
      <th>SIZE OF LARGEST CLASS</th>
      <th>DATA SOURCE</th>
      <th>SCHOOLWIDE PUPIL-TEACHER RATIO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>M</td>
      <td>M015</td>
      <td>P.S. 015 Roberto Clemente</td>
      <td>0K</td>
      <td>GEN ED</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>19.0</td>
      <td>1.0</td>
      <td>19.0</td>
      <td>19.0</td>
      <td>19.0</td>
      <td>ATS</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>M</td>
      <td>M015</td>
      <td>P.S. 015 Roberto Clemente</td>
      <td>0K</td>
      <td>CTT</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>21.0</td>
      <td>1.0</td>
      <td>21.0</td>
      <td>21.0</td>
      <td>21.0</td>
      <td>ATS</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>M</td>
      <td>M015</td>
      <td>P.S. 015 Roberto Clemente</td>
      <td>01</td>
      <td>GEN ED</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>17.0</td>
      <td>17.0</td>
      <td>17.0</td>
      <td>ATS</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>M</td>
      <td>M015</td>
      <td>P.S. 015 Roberto Clemente</td>
      <td>01</td>
      <td>CTT</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>17.0</td>
      <td>1.0</td>
      <td>17.0</td>
      <td>17.0</td>
      <td>17.0</td>
      <td>ATS</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>M</td>
      <td>M015</td>
      <td>P.S. 015 Roberto Clemente</td>
      <td>02</td>
      <td>GEN ED</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>15.0</td>
      <td>1.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>ATS</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## School Demographics and Accountability Snapshot 2006-2012
Annual school accounts of NYC public school student populations served by grade, special programs, ethnicity, gender and Title I funded programs.





```python
data["school_demographics"] = pd.read_csv("../Data/us_sat/{0}.csv".format("School_Demographics_and_Accountability"))
data["school_demographics"].head()

```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DBN</th>
      <th>Name</th>
      <th>schoolyear</th>
      <th>fl_percent</th>
      <th>frl_percent</th>
      <th>total_enrollment</th>
      <th>prek</th>
      <th>k</th>
      <th>grade1</th>
      <th>grade2</th>
      <th>...</th>
      <th>black_num</th>
      <th>black_per</th>
      <th>hispanic_num</th>
      <th>hispanic_per</th>
      <th>white_num</th>
      <th>white_per</th>
      <th>male_num</th>
      <th>male_per</th>
      <th>female_num</th>
      <th>female_per</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01M015</td>
      <td>P.S. 015 ROBERTO CLEMENTE</td>
      <td>20052006</td>
      <td>89.4</td>
      <td>NaN</td>
      <td>281</td>
      <td>15</td>
      <td>36</td>
      <td>40</td>
      <td>33</td>
      <td>...</td>
      <td>74</td>
      <td>26.3</td>
      <td>189</td>
      <td>67.3</td>
      <td>5</td>
      <td>1.8</td>
      <td>158.0</td>
      <td>56.2</td>
      <td>123.0</td>
      <td>43.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01M015</td>
      <td>P.S. 015 ROBERTO CLEMENTE</td>
      <td>20062007</td>
      <td>89.4</td>
      <td>NaN</td>
      <td>243</td>
      <td>15</td>
      <td>29</td>
      <td>39</td>
      <td>38</td>
      <td>...</td>
      <td>68</td>
      <td>28.0</td>
      <td>153</td>
      <td>63.0</td>
      <td>4</td>
      <td>1.6</td>
      <td>140.0</td>
      <td>57.6</td>
      <td>103.0</td>
      <td>42.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01M015</td>
      <td>P.S. 015 ROBERTO CLEMENTE</td>
      <td>20072008</td>
      <td>89.4</td>
      <td>NaN</td>
      <td>261</td>
      <td>18</td>
      <td>43</td>
      <td>39</td>
      <td>36</td>
      <td>...</td>
      <td>77</td>
      <td>29.5</td>
      <td>157</td>
      <td>60.2</td>
      <td>7</td>
      <td>2.7</td>
      <td>143.0</td>
      <td>54.8</td>
      <td>118.0</td>
      <td>45.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01M015</td>
      <td>P.S. 015 ROBERTO CLEMENTE</td>
      <td>20082009</td>
      <td>89.4</td>
      <td>NaN</td>
      <td>252</td>
      <td>17</td>
      <td>37</td>
      <td>44</td>
      <td>32</td>
      <td>...</td>
      <td>75</td>
      <td>29.8</td>
      <td>149</td>
      <td>59.1</td>
      <td>7</td>
      <td>2.8</td>
      <td>149.0</td>
      <td>59.1</td>
      <td>103.0</td>
      <td>40.9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01M015</td>
      <td>P.S. 015 ROBERTO CLEMENTE</td>
      <td>20092010</td>
      <td></td>
      <td>96.5</td>
      <td>208</td>
      <td>16</td>
      <td>40</td>
      <td>28</td>
      <td>32</td>
      <td>...</td>
      <td>67</td>
      <td>32.2</td>
      <td>118</td>
      <td>56.7</td>
      <td>6</td>
      <td>2.9</td>
      <td>124.0</td>
      <td>59.6</td>
      <td>84.0</td>
      <td>40.4</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 38 columns</p>
</div>



# Analysis process description
(some text)

In order to work with the data more easily, we’ll need to unify all the individual datasets into a single one. This will enable us to quickly compare columns across datasets. In order to do this, we’ll first need to find a common column to unify them on. Looking at the output above, it appears that DBN might be that common column, as it appears in multiple datasets.

DBN is a unique code for each school

class_size, and hs_directory, don’t have a DBN field. In the hs_directory data, it’s just named dbn, so we can just rename the column, or copy it over into a new column called DBN. In the class_size data, we’ll need to try a different approach.

...
If we take a look at some of the datasets, including class_size, we’ll immediately see a problem:

There are several rows for each high school (as you can see by the repeated DBN and SCHOOL NAME fields). However, if we take a look at the sat_results dataset, it only has one row per high school

## Data cleaning
Data cleaning and exploration is critical before working on the meat of the project. Having a good, consistent dataset will help you do your analysis more quickly.

# Outlooks

Adding in the surveys

One of the most potentially interesting datasets to look at is the dataset on student, parent, and teacher surveys about the quality of schools. These surveys include information about the perceived safety of each school, academic standards, and more. Before we combine our datasets, let’s add in the survey data. In real-world data science projects, you’ll often come across interesting data when you’re midway through your analysis, and will want to incorporate it. Working with a flexible tool like Jupyter notebook will allow you to quickly add some additional code, and re-run your analysis.


```python

```
