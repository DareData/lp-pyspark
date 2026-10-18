# Final Project

Welcome to the Final Project of this Learning Pod! ✴️

This project brings together everything covered in the previous modules. It is split over **two weeks**. The goal is to practise PySpark and learn from a real public dataset together.

## The brief

We will use four raw CSV files from the MovieLens Small dataset as material for hands-on learning. Over two weeks, we will:

- **Week 1** — explore the raw files, practise cleaning and joining data, and create a curated dataset.
- **Week 2** — practise advanced PySpark techniques, answer three open questions about the dataset, and explain your findings.

## The dataset

We use the **MovieLens small** dataset, published by the [GroupLens](https://grouplens.org/datasets/movielens/) research group at the University of Minnesota. It contains **100.836 ratings** and **3.683 tags** applied to **9.742 movies** by **610 users**, between March 1996 and September 2018.

| File | Columns | Description |
| --- | --- | --- |
| `ratings.csv` | `userId`, `movieId`, `rating`, `timestamp` | One row per rating. Ratings go from 0.5 to 5.0 stars, in 0.5 increments |
| `movies.csv` | `movieId`, `title`, `genres` | One row per movie. The title ends with the release year and the genres are pipe separated |
| `tags.csv` | `userId`, `movieId`, `tag`, `timestamp` | Free text tags applied by users to movies |
| `links.csv` | `movieId`, `imdbId`, `tmdbId` | Identifiers of the same movie on IMDb and TMDB |

**You do not need to download anything by hand.** The first cells of the Week 1 notebook download and unzip the dataset (~1 MB) into `movielens-data/`. If your network blocks the download, get *ml-latest-small.zip* manually from [grouplens.org/datasets/movielens](https://grouplens.org/datasets/movielens/) and unzip it into that folder.


## Structure

```
04_final_project/
├── README.md                        <- you are here
├── 04_01_data_foundations/
│   ├── project.ipynb                <- Week 1, the notebook you work on
│   └── project-solution.ipynb       <- Week 1, the solution
├── 04_02_advanced_insights/
│   ├── project.ipynb                <- Week 2, the notebook you work on
│   └── project-solution.ipynb       <- Week 2, the solution
├── movielens-data/                  <- created by the notebooks, raw dataset
└── curated/                         <- created by you in Week 1, the hand off between weeks
```

Work on `project.ipynb` and only open `project-solution.ipynb` once you are done, or when you are truly stuck. The point of the project is the struggle, not the answer.

### Week 1 — From raw files to a curated dataset

Modules **01 - Spark Introduction** and **02 - PySpark DataFrames**.

1. Download the raw dataset
2. Explore `movies.csv` with **RDDs**: parse it by hand, count movies per genre, and see lazy evaluation and caching in action
3. Load the four files into **DataFrames** with explicit `StructType` schemas
4. Run **data quality checks**: duplicates, nulls, value ranges
5. **Clean and enrich**: extract the release year from the title, convert unix timestamps into dates, normalise the tags
6. **Join** the four datasets together
7. Explore questions about the dataset with `groupBy`, aggregations and **Spark SQL**
8. Write the **curated dataset** to `curated/` as Parquet

**Learning outcome:** a `curated/` folder with the `movies`, `ratings` and `tags` datasets, plus practice explaining findings from the analysis.

### Week 2 — Advanced analytics and insights

Module **03 - PySpark Advanced**.

**Part A, the toolbox.** Guided questions, one expected answer each:

- **Complex data types**: turn the genres into an array, collect the tags of a movie into another one, build a movie profile `struct`, `explode` the genres to get per genre statistics, build a `map` from genre to average rating
- **Window functions**: top 3 movies per genre, the rating timeline of each user, moving and cumulative averages, year over year genre growth
- **UDFs**: implement a weighted rating with built-in functions, with a UDF and with a Pandas UDF, compare the three, and then write a UDF for something that built-in functions cannot do

**Part B, putting it all together.** Three open questions, with no step-by-step instructions: you choose the approach and write the PySpark code. Between them they need a window function, a UDF and an operation on a complex data type:

- **Question 19**: do users become harsher or more generous as they rate more movies?
- **Question 20**: do blockbusters and long tail movies get systematically different ratings?
- **Question 21**: which tags are associated with the best and the worst rated movies?

Each answer is followed by a short markdown cell where you explain your findings in your own words.

**Learning outcome:** practise the Part A techniques, answer the three Part B questions and explain what the numbers mean, focusing on what the data shows rather than on the code.

> If you did not finish Week 1, do not worry: the first cells of the Week 2 notebook rebuild the curated dataset automatically, so you can start Week 2 anyway.

## What you will practice

| Module | Where it shows up |
| --- | --- |
| 01 - RDDs, lazy evaluation, caching | Week 1, section 2 |
| 02 - Schemas, cleaning, joins, aggregations, Spark SQL | Week 1, sections 3 to 7 |
| 03 - Arrays, structs and maps | Week 2, section 2 |
| 03 - Window functions | Week 2, section 3 |
| 03 - UDFs and Pandas UDFs | Week 2, section 4 |
| 03 - All topics together | Week 2, section 5 |

## Running the notebooks

The notebooks run locally, exactly like the ones of the previous modules. You need Java 8 or newer and the following Python packages:

```bash
pip install pyspark pandas pyarrow seaborn matplotlib ipykernel
```

`pyarrow` is required by the Pandas UDFs of Week 2, and `seaborn` by the performance comparison chart.

Paths inside the notebooks are relative to the notebook folder, so open them from their own directory and do not move them around.

---

Happy Learning!
