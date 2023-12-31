# HMK 5: Reading and tidying data

# Data import

## Q1:

I previously made a data directory within my class directory so I don’t
have to do that again. If I needed to though, I would open the terminal
and do this. `pwd` to see what directory I am in. The result of that
should look like `/Users/cassidycatrett/Documents/micr_575`. If that’s
the case, `mkdir data` will create a new directory in my class
directory. Once that’s one, `cd data` will move me into that directory.

Now that I have a `data` directory and have navigated to it, I will use
this to store raw data for this class. To download the `students` data
set, I used the `wget` command to download it to my `data` directory.

`wget https://raw.githubusercontent.com/hadley/r4ds/main/data/students.csv`

Once my data set has been downloaded it, I want to open it in R studio.

Loading packages

``` r
library(tidyverse)
```

Loading data

``` r
students <- read_csv("../data/students.csv")
View(students)
```

Now that I have uploaded and viewed my data set, I want to clean it up.
First, I notice that some columns are empty and are interpreted as NA
values in R but there are also responses stated as “N/A”. I want all of
those to be interpreted in the same manner so I’m going to re-read in my
data set to do that.

``` r
students <- read_csv("../data/students.csv", 
                     na = c("N/A", ""))
```

Now that all NA values have been interpreted in the same way, I want to
rename my columns so they are all in the same format.

``` r
# install.packages("janitor")
library(janitor)
students <- students |> clean_names()
```

Now, all my column names are in the same format. If I had wanted to
change a couple column names, I could’ve done this.

``` r
# students |> 
  # rename(
    # student_id = `Student ID`,
   #  full_name = `Full Name`
  # )
```

Now, I want to look at what type of variables I have using `glimpse`.

`glimpse(students)`

I see here that student_id is a dbl and all other columns are chr. I
need to change some of these so that I can better run analyses and
visualize my data.

``` r
students <- students |> 
  mutate(meal_plan = factor(meal_plan), 
         age = parse_number(if_else(age == "five", "5", age)))
```

Here, I changed meal_plan to be a factor since this is a categorical
variable, meaning there are only so many values this column can be. I
also reformatted the age column to be a dbl and all the values are now
written as numbers whereas, previously, there was once value written as
“five”.

## Q2

Find (or make) a data file of your own, in text format. Read it into a
well-formatted data frame.

Here, I have a subset of dam age records for a group of Simmental
heifers. To make this subset, I used `sample_n(size = 20)` to randomly
select 20 records from my full data set. To export this data set, I use
`write_delim` as follows.

``` r
# write_delim(afc, "~/Documents/micr_575/data/afc.txt", delim = ",", col_names = TRUE)
```

Now, I want to read it in to this session.

``` r
age <- read_csv("../data/afc.txt")
```

The first column shows animal identification numbers. The second column
shows the contemporary group for that animal. The third column shows the
age at first calving in days for these heifers. The comma separated text
file is
[here](https://github.com/cassidycatrett/micr_575/blob/main/data/afc.txt).

# Tidying

Download the data set available at
<https://tiny.utk.edu/MICR_575_hmk_05>, and save it to your `data`
folder. **This is a real data set:** it is the output from the
evaluation forms for student colloquium speakers in the Microbiology
department. I have eliminated a few columns, changed some of the scores,
and edited comments, to protect student privacy, but the output is real.

To download this file, I used the same `wget` command from before.

`wget https://tiny.utk.edu/MICR_575_hmk_05`

## Q3a

Next, use `read_csv()` to read the data into a data frame. Note that
you’ll need to make use of some of the optional arguments. Use
`?read_csv` to see what they are.

``` r
eval <- read_csv("../data/MICR_575_hmk_05",
                 col_names = c("start_time", "end_time", "status", "progress", "duration", "finished", "recorded_date", "response_id", "last_name", "first_name", "email", "external_reference", "latitude", "longitude", "distribution_channel", "language", "q4", "q5", "q6", "q7", "q8", "q9", "q10", "q11", "comments"),
                 skip = 5) |> 
  filter(!is.na(start_time))
```

Notes for these steps while reading in my data file.

`col_names` creating names for columns since the ones in my data file
aren’t useful

`skip` the first 5 lines do not contain any data so I want to ignore
those I then piped this command to the

`filter` function so that rows that did not have a start_time would be
removed, leaving me with responses from the 16 students in the study.

Now, I want to reshape my data frame to be more useful.

``` r
new_eval <- eval |> 
  pivot_longer(cols = starts_with("q"), 
               names_to = "question", 
               values_to = "response") |> 
   mutate(question = parse_number(question))
```

I made my data frame longer and put all of the question responses in to
one column.

`mutate` was used to remove the “q” from the beginning of each question
number

## Q3b

Finally, calculate this student’s average score for each of questions
7-10.

``` r
new_eval |> 
  filter(question >= 7, 
         question < 11) |>
  group_by(question) |> 
  summarise(mean(response))
```

    # A tibble: 4 × 2
      question `mean(response)`
         <dbl>            <dbl>
    1        7             4.5 
    2        8             4.62
    3        9             4.31
    4       10             4.44

`filter` was used to subset the data file to only include questions 7-10

The average response for questions 7-10 is in the tibble above.
