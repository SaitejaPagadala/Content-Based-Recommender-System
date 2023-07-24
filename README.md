# Content-Based-Recommender-System
This repo will have content-based recommender system project files

# Building a Content-Based Movie Recommendation System in Python

Dataset Link: https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata?select=tmdb_5000_movies.csv

Recommendation systems are an important part of many online platforms. In this post, I'll walk through building a simple content-based movie recommendation system in Python. 

Content-based recommendation relies on item metadata and descriptions to find similarities and make suggestions. This is in contrast to collaborative filtering systems which use historical user behavior and ratings data to make recommendations.

## Data Collection and Cleaning

I collected movie metadata like cast, crew, plot keywords, genres from TMDB and performed some transformations:

- Merged movie data with credits data
- Extracted relevant textual columns 
- Used ast.literal_eval to convert string lists into Python lists
- Wrote functions to clean and transform text data into a consistent format

The key here is getting all the meaningful text data associated with each movie consolidated for the next step.

## Feature Extraction with NLP

To extract features, I treated each movie's metadata as a document. I concatenated the plot, genres, keywords, cast, etc into a single string per movie. This represented the textual "content" of the movie.

I then used CountVectorizer to convert these documents into a matrix of token counts. This effectively models the presence/absence of words in each movie, giving us numerical features to work with.

Transforming text into a numeric matrix is a common process in natural language processing and information retrieval. It allows us to apply various algorithms to understand relationships between documents.

## Calculate Similarity with Cosine Similarity 

Using the count matrix as input features, I calculated a cosine similarity matrix using sklearn. Cosine similarity is a great way to quantify similarity for these high-dimensional text feature vectors. 

The similarity scores represent how close two movies are based on the words that appear in their concatenated document vectors. The closer to 1, the more similar the movies based on their content.

## Make Recommendations

To generate recommendations, I wrote a function that finds the 5 movies most similar to a given movie title based on the cosine similarity matrix.

And that's it for a basic content-based recommendation system! The key strengths are that it only relies on item metadata, doesn't need historical user data, and can recommend niche items. However, it can only make recommendations based on existing movies - a collaborative filtering system may discover more novel connections.
