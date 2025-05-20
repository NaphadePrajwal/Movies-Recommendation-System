# Movies-Recommendation-System

🔁 Project Flow
This section outlines the step-by-step pipeline of how the AI-Based Movie Recommendation System is built and executed — from raw data to intelligent suggestions.

📌 1. Recommendation Type
Content-Based Filtering: Recommends movies similar to a given movie based on metadata (genre, overview, keywords, cast, crew).
Collaborative Filtering: (Mentioned but not implemented) Recommends based on what similar users liked.
Hybrid Filtering: A combination of both methods — future enhancement.

📌 2. Data Collection
Datasets Used:
movies.csv — contains movie metadata like title, overview, genres, etc.
credits.csv — contains detailed info about cast and crew.

📌 3. Data Preprocessing
Used Pandas to load and manipulate datasets.
Merged the two CSV files on the movie title.
Removed:
    Duplicate values
    Null or irrelevant columns
Selected only important columns:
    movie_id, title, overview, genres, keywords, cast, crew
    
These columns were combined into a new feature called "tags".

📌 4. Feature Engineering
Converted column values from string to list using ast.literal_eval (for genres, keywords, cast, crew).
Merged 5 columns into 1 unified "tags" column.
Cleaned and preprocessed text for NLP.

📌 5. Text Preprocessing with NLP
Used the NLTK library:
Removed spaces and converted to lowercase.
Applied stemming using PorterStemmer to reduce words to root form.
Example: "dancing" → "dance"

📌 6. Vectorization
Used CountVectorizer to convert text into numerical vectors.
Created a vector space model from the "tags" column.
Applied cosine similarity to compute distances between all movies.

📌 7. Model Building
Created a recommend() function that:
Takes a movie title as input
Finds the top 5 most similar movies based on cosine distance
Returns both titles and movie IDs

📌 8. Model Serialization
Used Pickle to save:
movie_dict.pkl: contains the movie DataFrame
similarity.pkl: precomputed similarity matrix
Ensures faster loading and reuse in the frontend.

📌 9. Frontend Interface (Streamlit)
Built a web-based GUI using Streamlit.

Features:
Dropdown to select movie
Button to generate recommendations
5 columns for displaying recommended movies

📌 10. API Integration (TMDb)
Used the TMDb API to fetch movie posters:
Each movie ID is used to call the API and retrieve the poster image path.

Constructed image URLs with:
https://image.tmdb.org/t/p/w500/<poster_path>

📌 11. Final Deployment
The app is run locally using: streamlit run app.py

Can be hosted online using platforms like Streamlit Cloud, Heroku, or Render.

✅ Summary Workflow

Data Collection
     ↓
Data Preprocessing (Merge, Clean, Tag Creation)
     ↓
Text Processing (NLTK + Stemming)
     ↓
Vectorization (CountVectorizer)
     ↓
Similarity Matrix (Cosine Similarity)
     ↓
Model Save (Pickle)
     ↓
Frontend (Streamlit)
     ↓
API Poster Fetching (TMDb)
     ↓
Top 5 Movie Recommendations

