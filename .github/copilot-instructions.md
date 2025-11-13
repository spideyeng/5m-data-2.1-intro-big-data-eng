# Copilot Instructions for Data Engineering 2.1 Module

## Project Overview

This is an educational module on **Introduction to Big Data and Data Engineering**, focusing on NoSQL databases (MongoDB) and CRUD operations. The repository contains lesson materials, assignments, and Jupyter notebooks for hands-on learning.

**Key Structure:**
- `notebooks/`: Contains interactive lessons and assignments using Jupyter
- `environments/`: Conda environment files for reproducible setups
- `assignment.md`, `lesson.md`, `studies.md`, `reference.md`: Course materials in markdown

## Environment Setup (Critical for Context)

**All Python code runs in conda environments**. When assisting with code:

1. **Primary Environment**: `bde` (defined in `environments/bde-environment.yml`)
   - Python 3.10 + pandas, pyarrow, sqlalchemy, duckdb
   - **Always includes**: `pymongo==4.4.1`, `notebook==6.5.4`
   - Creation: `cd environments && conda env create --file bde-environment.yml`

2. Other environments for later lessons: `elt`, `dagster`, `kafka`, `ooc`

3. **Never pip install without considering conda compatibility** — the `bde-environment.yml` explicitly pins versions (e.g., Python 3.10, pymongo 4.4.1)

## MongoDB Patterns & Workflow

### Connection Pattern (Used in Both Notebooks)

```python
from pymongo.mongo_client import MongoClient
from pymongo.server_api import ServerApi

uri = "mongodb+srv://spidey_dbuser:Asimov23@spideycluster.7fu5sbe.mongodb.net/?appName=SpideyCluster"
client = MongoClient(uri, server_api=ServerApi('1'))

# Verify connection with ping
try:
    client.admin.command('ping')
    print("Successfully connected!")
except Exception as e:
    print(e)
```

### Data Access Hierarchy

```python
import pymongo

# 1. List databases
client.list_database_names()  # → returns list

# 2. Get database
db = client.sample_mflix

# 3. List collections
db.list_collection_names()

# 4. Access collection
movies = db.movies

# 5. Query operations
movies.find_one()  # single document
movies.find({...}, sort=[...], limit=5)  # filtered query
```

### Common Query Patterns

- **Case-insensitive regex**: `{'plot': {'$regex': '^War', '$options': 'i'}}`
- **Sorting**: `sort=[("year", pymongo.ASCENDING)]` or `pymongo.DESCENDING`
- **Field projection**: `find({...}, {'_id': 0, 'title': 1, 'plot': 1})`  to include/exclude fields
- **Aggregation**: Use `.count_documents()` for counts, not `.count()` (deprecated)

### Assignment Context

Three questions to solve in `notebooks/2.1 Intro Big Data Assignment.ipynb`:

1. Find movies with plots starting with "war" (regex `^War`), sorted by release year, return title/plot/released fields, limit 5
2. Group by `rated` field and count movies — typically use pandas `.groupby()` on cursor results
3. Count movies with 3+ comments — requires join logic with `comments` collection

**Note**: The assignment expects answers in Python code blocks within the notebook — use proper pymongo syntax with aggregation/filtering where needed.

## Notebook Conventions

1. **Cell ordering matters**: Setup/imports → connection → data exploration → queries → analysis
2. **Comments precede complex code**: See `nosql_lesson.ipynb` pattern — explanatory markdown before code cells
3. **Error handling**: Always wrap MongoDB operations in try/except for connection/network issues
4. **Display outputs**: Use `.limit(5)` and `print()` to avoid overwhelming output in educational context

## Key Files to Reference

- `lessons/nosql_lesson.ipynb` — complete MongoDB examples (CRUD, aggregation, indexing)
- `notebooks/2.1 Intro Big Data Assignment.ipynb` — assignment template with stub cells
- `reference.md` — links to pymongo documentation (https://pymongo.readthedocs.io)

## When Helping with Code

- **Always suggest conda environment activation** before running notebooks
- **Validate MongoDB connection** before querying — the cluster requires credentials
- **Use `pymongo.ASCENDING` / `pymongo.DESCENDING`** constants (not strings)
- **Prefer `.find() + sort()` chain** over `.find_one()` for large result sets
- **Document assumptions** about collection schema (sample_mflix has collections: movies, comments, users)
