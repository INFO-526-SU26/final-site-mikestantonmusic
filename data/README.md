## Dataset

Since 2023, Netflix has released regular Engagement Reports summarizing the number of hours that users have spent watching each show and movie in the last 6 months. This data set combines viewing data from late 2023 through the first half of 2025. The data was curated by Jen Richmond, RLadies-Sydney for the Tidy Tuesday challenge for the week of July 29, 2025 and can be found here:

https://github.com/rfordatascience/tidytuesday/blob/main/data/2025/2025-07-29/readme.md

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

Title: The title of the show

Available Globally: If the show is available globally

Release Date: When the show was released

Hours Viewed: Total number of hours the show was viewed by all audience members

Run Time: Length of the show

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
