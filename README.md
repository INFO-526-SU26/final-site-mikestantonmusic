[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/7LgAUKoA) \# project-final

Final Project repo for INFO 526 - Summer 2024.

#### Disclosure:

Derived from the original course by Mine Çetinkaya-Rundel \@ Duke University

#### **Dataset**

Since 2023, Netflix has released regular Engagement Reports summarizing the number of hours that users have spent watching each show and movie in the last 6 months. This data set combines viewing data from late 2023 through the first half of 2025. The data was curated by Jen Richmond, RLadies-Sydney for the Tidy Tuesday challenge for the week of July 29, 2025 and can be found here:

<https://github.com/rfordatascience/tidytuesday/blob/main/data/2025/2025-07-29/readme.md>

The data set is separated into "movies", and "shows", with a separate pair of data sets for each 6 month time frame (8 csv files in total).

For movies, the data set for each time frame contains the following columns:

Source: The full name of the data source

Report: Which 6 month time frame this data is referring to

Title: The title of the movie

Available Globally: If the movie is available globally

Release Date: When the movie was released

Hours Viewed: Total number of hours the movie was viewed by all audience members

Run Time: Length of the movie

Views: The number of views

To load and view the data:

```{r}
#| label: load-dataset
#| message: false

movies_data <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2025/2025-07-29/movies.csv")
print("Movies Dataset (from first half of 2025:")
head(movies_data)
```

```{r}
#| label: view-dimensions
#| message: false

print("Data Types")
spec(movies_data)
print("Number of Rows, Columns:")
dim(movies_data)
```

```         
  source = col_character(),   
  report = col_character(),   
  title = col_character(),   
  available_globally = col_character(),   
  release_date = col_date(format = ""),   
  hours_viewed = col_double(),   
  runtime = col_character(),   
  views = col_double()
  
  "Number of Rows, Columns:"
  36121     8
```

For Shows, the data set for each time frame contains the following columns:

Source: The full name of the data source

Report: Which 6 month time frame this data is referring to

Title: The title of the show, including the season (for shows each show is separated by season)

Available Globally: If the show is available globally

Release Date: When the show was released

Hours Viewed: Total number of hours the show was viewed by all audience members

Run Time: Length of the show (the total runtime of the season)

Views: The number of views

To load and view the data:

```{r}
#| label: load-dataset2
#| message: false

shows_data <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2025/2025-07-29/shows.csv")
print("Shows Dataset (from first half of 2025:")
head(shows_data)
```

```{r}
#| label: view-dimensions2
#| message: false

print("Data Types: ")
spec(shows_data)
print("Number of Rows, Columns: ")
dim(shows_data)
```

```         
  source = col_character(),   
  report = col_character(),   
  title = col_character(),   
  available_globally = col_character(),   
  release_date = col_date(format = ""),   
  hours_viewed = col_double(),   
  runtime = col_character(),   
  views = col_double()
  
  "Number of Rows, Columns:"
  27803     8
  
```

This data set was chosen because it has a variety of opportunities to explore both numerical (hours viewed, views, run time), categorical (type, global availability) and temporal (6 month timeframe, release data) data for answering research questions. Understanding this data can help businesses to better understand how to engage with their audiences.

#### **Questions**

Question 1: What patterns and trends do we see between lasting popularity (number of views, as well as hours viewed) of content and the release date? In other words, does a specific era have an association with lasting popularity. For this we can look at not only how popular a movie or TV show is but also the decay or lack thereof over time. Release date can be grouped into buckets and treated as a categorical variable in different ways, or it could be analyzed as a continuous variable.

Question 2: What patterns and trends do we see between lasting popularity (number of views) of content and the run time, both for shows and for movies? Does content of a specific length have any association with lasting popularity? For this we should account for whether the content is a show or a movie. Do movies with different lengths have stronger lasting popularity? What about shows with different lengths or different numbers of episodes? Run time could also be grouped into buckets and treated as a categorical variable, or analyzed as a continuous variable.

#### **Analysis plan**

Question 1:

Calculate an "Age of Content" variable (Numeric) by subtracting the Release Date from the report time-frame date. Create "Release Era" buckets (Categorical) based on data distribution (e.g., Pre-2010, 2010–2015, 2016–2020, 2021–2024, New Releases 2025+). Group the data by age bucket. Create columns for "Average Views" and "Average Hours Viewed", as well as "Title Count" for each age bucket.

Create faceted line charts to show the trend of views across the weeks represented in the data, with each line representing an "age bucket". A grouped bar chart could also potentially be layered onto the visual to show the volumes of each age bucket for added context. Interactive buttons can be added to switch between viewing the number of views vs the number of hours viewed on the Y axis. On the X axis could be simply the week of the movie/show, or it could be the age in weeks since the title's release. (this might make it easier to compare "staying power" by having all of the lines decay together.)

Question 2:

Create a clean Content Type column from the relative data source file (movie vs show, Categorical). Create "Length Buckets" (Categorical). For Movies: Short (\<90 mins), Standard (90–130 mins), Epic (\>130 mins). For Shows: Bin them by total run time hours to approximate short vs. long seasons. Group the data by run-time bucket and by type (show vs movie). Add a new column for average number of views as well as "Title Count".

Created faceted line charts to show the trend of views across the weeks represented in the data, with each line representing a duration/ run time bucket. On the X axis will be simply the week, and on the Y axis will be the average number of views. A grouped bar chart could also be potentially layered onto the visual to show the volumes of each "run time bucket" for added context. Interactive buttons can be added to switch between viewing shows vs movies.

#### **Weekly plan of attack:**

Week 1: Data Ingestion & Environmental Setup

Set up repository and working environment, choose data set, and ingest the dataset via the GitHub URL. Run initial glimpse(), dim(), and summary() checks. Identify missing values (NA values), specifically in the Release Date or Run Time columns, and decide how to handle them (e.g., filtering them out or looking up missing pieces).

Week 2: Feature Engineering & Data Cleaning

Create categorical era buckets and content length buckets. Merge data and flag data into "Movies" vs. "TV Shows". Calculate the content age/decay metrics. Print out small table summaries using count() to make sure custom categories have a healthy balance of rows.

Week 3: Exploratory Data Analysis (EDA) & Summary Statistics

Calculate standard numeric summaries (mean, median, standard deviation) of Views and Hours Viewed across different categorical buckets. Look at the skewness of viewership data. Because streaming hits have massive outliers, decide if it is necessary to apply a log transformation to numeric axes for upcoming charts.

Week 4: Data Visualization (Drafting the Core Plots)

Develop Question 1 plots: The scatter plot tracking popularity decay over time, and the box plots comparing release eras. Develop Question 2 plots: The faceted scatter plots breaking down runtime trends by Movie vs. Show. Apply clean axis labels, custom scales, and clear legends.

Week 5: Statistical Interpretation & Narrative Writing

Draft the written sections in Quarto document beneath code chunks. Interpret the charts: Does an older era hold a surprising amount of nostalgia/lasting popularity? Is there an optimal movie runtime that maximizes views? Use print statements within code to dynamically display key takeaway numbers directly inside report text.

Week 6: Quarto Polishing, Code Review, and Formatting

Render and double check all content. Finalize repository and record presentation.
