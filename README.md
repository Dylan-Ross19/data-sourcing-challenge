# data-sourcing-challenge
## Pt. 1: Access the New York Times API
Dependancies and API url provided. However we put our API keys into the environment file.

Also Provided were the search parameters to build the URL with. Consulting instructions on the NYT website provided for in the module challenge page, we were able to build the URL in the correct order. Now we are able to retreive move reviews. The reviews are placed in batches, and a 12-second sleep interval is added to stay within Query Limits.

The code inside the try block attempts to execute a loop through the reviews obtained from the API response 
(reviews.json()["response"]["docs"]).
We then append each review to the reviews_list. but append wasn't working so by consulting the BCSlearning assistant I determined using extend was the correct approach

A KeyError might occur if the expected keys ("response" and "docs") are not present in the JSON structure obtained from the API response.
Inside the except block, the script prints a message indicating that there are no results from the current page (print(f"No results from page {page}")).

We then print the first 5 results in the JSON format with the indent=4.

The json_normalize function is used to flatten JSON data into a pandas DataFrame. In the dependencies section the appropriate function was not imported. So I added the from pandas import json_noramlize so that this cell could be accomplished.  json_normalize takes a nested JSON structure (which is common in API responses) and flattens it into a DataFrame. Each nested level in the JSON becomes a column in the DataFrame.

We then extracted "headline.main" using the lambda code provided for in the module challenge 6 page inside the apply function. 
The extract_keywords function is applied to each cell in the "keywords" column using the apply method. It transforms each list of dictionaries in the "keywords" column into a string of 'name: value' pairs.

We then created a list of titles to iterate through using the next dataframe from TMDB.

## Pt 2: Access Movie Database API

The script loops through a list of movie titles (title_list). For each title, it checks if a request sleep is needed (every 50 requests to avoid API rate limits). After the check is done and the is no Index Error it is appended to the 'tmdb_movies list'.
If the movie was not found it prints an error message. The output prints messages indicating which movies were found and which ones were not.

We print the frist 5 results in JSON format index=4.
Convert to pandas, not having to use json_normalize this time because there are no nested objects.

## Pt 3: Merge and CLean the Data for Export

We merged the teo DataFrames on the 'title' column using an inner join, combining info from both sources. We convert all unwanted characters in the "genre, spoken_languages, and prodcution_countries" columns. We converted the columns to strings and removed [] and ' from the strings.

We then drop the "byline.person" column and all duplictae rows from the merged_df DataFrame.

After all that we  export to CSV file and index set to false to prevent the index column being written into the csv file.

These last few steps are essential for sharing the data. It is now ready for further analysis.

