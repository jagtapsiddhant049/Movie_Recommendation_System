# Movie Recommendation System

A movie discovery app with a Streamlit interface and a FastAPI backend. Search for movies using The Movie Database (TMDB), browse movie categories, view details, and get recommendations based on TF-IDF similarity and genre.

## Features

- Browse trending, popular, top-rated, now-playing, and upcoming movies.
- Search movies by title and open matching results.
- View movie details, posters, release dates, genres, and summaries.
- Get similar-movie recommendations from a local TF-IDF model and genre recommendations from TMDB.

## Tech stack

- Python 3.11
- Streamlit frontend
- FastAPI backend
- scikit-learn / TF-IDF recommendations
- TMDB API for movie information and images

## Requirements

- Python 3.11
- A TMDB API key
- The model files in the project root: `df.pkl`, `indices.pkl`, `tfidf_matrix.pkl`, and `tfidf.pkl`

## Run locally

Open PowerShell in the project directory and create/activate a virtual environment:

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Create a `.env` file in the project directory and add your TMDB API key:

```text
TMDB_API_KEY=your_tmdb_api_key
```

Do not commit your `.env` file or share your API key publicly.

### Start the API

In one PowerShell terminal, run:

```powershell
uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

The API health check is available at `http://127.0.0.1:8000/health`, and interactive API documentation is at `http://127.0.0.1:8000/docs`.

### Start the Streamlit app

In a second PowerShell terminal, activate the same virtual environment, then run:

```powershell
.\.venv\Scripts\Activate.ps1
streamlit run app.py
```

The frontend currently points to the hosted API at `https://movie-rec-466x.onrender.com`. To use the API started locally above, change `API_BASE` near the top of `app.py` to:

```python
API_BASE = "http://127.0.0.1:8000"
```

## API endpoints

- `GET /health` — API health status
- `GET /home` — movie feed by category
- `GET /tmdb/search?query=...` — search TMDB titles
- `GET /movie/id/{tmdb_id}` — movie details
- `GET /recommend/genre?tmdb_id=...` — genre-based recommendations
- `GET /recommend/tfidf?title=...` — local TF-IDF recommendations
- `GET /movie/search?query=...` — movie details and combined recommendations

## Data and notebook

`movies_metadata.csv` and `movies.ipynb` contain the movie-data exploration and recommendation-model work. The API loads the precomputed pickle files from the project root when it starts. The notebook is optional for running the existing app.

## Attribution

Movie metadata and images are provided by [The Movie Database (TMDB)](https://www.themoviedb.org/). This project is not endorsed or certified by TMDB.