# Books Scraper

A small [Scrapy](https://scrapy.org/) project that collects book titles, prices,
and URLs from [Books to Scrape](https://books.toscrape.com/) and stores them in
MongoDB.

## Requirements

- Python 3
- MongoDB running locally
- Scrapy and PyMongo

## Setup

Create and activate a virtual environment, then install the dependencies:

```bash
python3 -m venv venv
source venv/bin/activate
pip install scrapy pymongo
```

By default, the project connects to `mongodb://localhost:27017` and writes to
the `books` collection in the `books_db` database. These values can be changed
in `books/settings.py`.

## Run the spider

From the project root:

```bash
scrapy crawl book
```

Each book is upserted using a SHA-256 hash of its URL, so running the spider
again updates existing records rather than inserting duplicates.

To export crawl results to a file as well, use Scrapy's feed export option:

```bash
scrapy crawl book -O books.json
```

## Project structure

```text
books/
├── items.py          # Scraped item fields
├── pipelines.py      # MongoDB persistence and deduplication
├── settings.py       # Scrapy and MongoDB settings
└── spiders/
    └── book.py       # Pagination and book extraction
scrapy.cfg            # Scrapy project configuration
```
