# School District Analysis - Berkeley DA
Yae Jin Park\
Module 4: PyCitySchools with Pandas

## Assignment Overview
The main objective of this assignment was to become familiar with the Pandas library by doing a thorough analysis on school and student data. I was provided with two csv data sheets - one for students, and one for schools, but there are "tampered" data within Thomas High School's ninth graders' grades. In terms of code, my goal is to demonstrate that I can repeat the process the whole module walked me through after cleaning up the invalid data.

## Cleaning Invalid Data - Deliverable 1
In order to clear Thomas High School's 9th graders' grades, I used the loc method on the student data dataframe (created with pandas'read_csv method for loading the csv data files). Logical operators specified within the loc method allowed me to select all 9th graders' grade in THS and make them equal to NaN with np.nan, as shown in the following screenshot. This process was done twice, first for removing math grades and second for removing reading grades.

* ![Replacing grades with NaN.](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d1_1.PNG)

There are two logical operators within each loc methods - the first operator looks for students that are in 9th grade and the second looks for students in THS. The two are connected with an AND, meaning both have to be satisfied in order to indicate that the selected rows indeed represent data from THS 9th graders.

I stored the resulting dataframe in a variable, 'ths_student_data_df', and checked if all 9th graders' grades shown as NaN.

* ![Seems like that worked.](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d1_2.PNG)

## School District Analysis - Deliverable 2
Merging the two data sets was required in order to do a full analysis of the school and student data, as the two sets contain different columns of data. This was simply done by pandas' merge method, as in line In[40].

Since the THS 9th graders' data are removed, for accurate average calculation, I had to calculate the new total number of students in the students data set, which was decreased from 39170 to 38709, as there are 461 9th graders in THS.

Then I got every school's count of students that are passing in math, reading, or both. This was done by selecting rows of data where desired scores are over 70 with a logical operator and counted unique student names (in hindsight, I should have counted student ID's instead of names since there can be more than one person with the same name. Luckily, that wasn't the case for me, looking at the results shown in later parts of this README.). This procedure is demonstrated in In[44].

Getting the count of students allowed me to get the percentage of the passing grades for math, reading, or both as the next step, which can be shown in the district summary dataframe below (Out[47]).

* ![District Summary DataFrame](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d2_1.PNG)

Now, I move on to get THS' summary on student performance and budget. This process is not too different from the process of getting the district summary, as almost same logical operators and pandas methods were used to count valid rows for calculations. I was able to get every school's summary (Out[50]), then singled out THS' row as per the requirement (Out[51]). The THS' row grades have been manually changed by the new grade calculations that don't count the invalid data from the 9th graders (In[57] - In[87]).

* ![All Schools Summary DataFrame](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d2_2.PNG)

* ![THS Summary DataFrame](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d2_3.PNG)

* ![Manually changing THS Summary](https://github.com/yaejinpark/school-district-analysis/blob/main/resources/screenshot/d2_4.PNG)

Interestingly, THS' passing math, reading, and overall percentages have boosted after manually correcting the data, but not much change in the actual scores. Maybe this indicates that the instructor who witnessed the academic dishonesty among 9th graders gave them failing grades regardless of the scores.

Remaining tasks and their results can be found at:
* Top 5 performing schools, Out[62]
* Bottom 5 performing schools, Out[64]
* Average math score for each grade level from each school, Out[131]
* Average reading score for each grade level from each school, Out[133]
* The scores by school spending per student, Out[108]
* The score by school size, Out[113]
* The score by school type, Out[116]

### Summary - The Four Changes
Manually changing THS students' grades have brought changes to the results.

* Math and reading scores - Interestingly, there isn't much change in the actual average scores. Maybe this indicates that the instructor who witnessed the academic dishonesty among 9th graders gave them failing grades regardless of the scores. In the outputs of the Jupyter Notebook where it shows the average scores for each grade level from each school, all 9th graders' columns are shown as NaN.
* Scores by school size - THS' size is categorized under 'Medium.' Just eyeballing the scores by school spending DF, other scores under the same category have quite high passing rates, all above 90%. If the manual change hadn't happened, THS would have been the outlier for medium sized schools.
* Scores by school spending - THS' spending range is in $630-644, which the range itself has passing scores ranging from 60 to 80 percent. THS' student performance are way above these averages, indicating that the manual fix would have boosted this range's performance.
* Scores by school type - THS is one of the charter schools, and their student performances averaged in the 90's for the passing rates. Manually fixing the data most likely boosted the charter schools' students' average performance, and it seems that THS' performance are right around the new average.