# Finlibrary - A Jellyfin Library Organizer

A smart Jellyfin Plugin for automatically organizing and renaming movie files based on metadata from **The Movie Database (TMDB) API**.

## 🎬 Features

- **Automatic Movie Detection**: Extracts movie names and years from filenames using intelligent parsing
- **TMDB Integration**: Searches for movies in the TMDb database and retrieves detailed metadata
- **Smart Renaming**: Reorganizes movie files according to a unified naming schema with metadata
- **Subtitle Management**: Recognizes and organizes subtitle files (SRT, ASS, VTT, etc.) with language and type information
- **Intelligent Filtering**: Automatically removes irrelevant tags (quality, codec, language, release groups, etc.)
- **Caching System**: Stores API requests locally to save API quotas and improve performance

## 📋 Requirements

- Python 3.8+
- TMDb API key (free at [themoviedb.org](https://www.themoviedb.org/settings/api))

## 🚀 Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd Movie_File_Organizer
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure your TMDb API key**:
   Create a `.env` file in the project directory:
   ```env
   TMDB_API_KEY=your_api_key_here
   ```

## 💻 Usage

### Basic execution

```bash
python main.py
```

The program processes the directory defined in `main.py` under `ROOT_DIR`.


## 🏗️ Project Structure

```
Movie_File_Organizer/
├── main.py              # Main entry point
├── parser.py            # Filename parsing and metadata extraction
├── filesystem.py        # File and directory operations
├── tmdb.py              # TMDb API integration
├── processer.py         # Main processing logic
├── cache.py             # Caching mechanisms
├── requirements.txt     # Python dependencies
└── cache/
    └── tmdb_cache.json  # Cached API results
```

### Modules

- **`main.py`**: Entry point, loads cache and starts processing
- **`parser.py`**: Parses movie names from filenames, removes irrelevant tags and codec information
- **`filesystem.py`**: Handles file and directory operations, renaming and subtitle management
- **`tmdb.py`**: Communicates with the TMDb API, searches for movies and retrieves metadata
- **`processer.py`**: Orchestrates the process from parsing through API queries to renaming
- **`cache.py`**: Manages local caching of API results

## 🔧 Configuration

Edit the variables in `main.py`:

```python
ROOT_DIR = "E:/Testdateien_FinLibrary/MediaServer/Movies"  # Your movies directory
```

## 📝 Supported File Types

### Video
All common video formats (MP4, MKV, AVI, MOV, etc.)

### Subtitles
- `.srt`, `.ass`, `.ssa`, `.sub`, `.vtt`, `.idx`

### Metadata
- Posters, backdrops, covers, etc.

## 🎯 Workflow

1. **Read directory**: Recursively searches the specified directory
2. **Parse filenames**: Extracts movie names and year from the filename
3. **TMDb query**: Searches for the movie in the database (with caching)
4. **Retrieve metadata**: Fetches relevant information such as release year
5. **Renaming**: Renames the file according to a unified schema
6. **Subtitle management**: Organizes subtitles together with the movie
7. **Save cache**: Updates the local cache with new results

## 🚫 Ignored Tags

The tool automatically removes:
- **Video formats**: 1080p, 720p, 4K, x264, x265, etc.
- **Audio codecs**: AAC, AC3, DTS, ATMOS, etc.
- **Source types**: BluRay, WebRip, DVDRip, HDTV, etc.
- **Languages**: German, English, Deutsch, Eng, etc.
- **Release groups**: RARBG, FGT, etc.
- **Other tags**: Extended, Uncut, Directors Cut, etc.

## 🔐 Security & API

- The TMDb API key is read from environment variables (do not commit to repository!)
- API requests are cached to save quotas
- `.env` file should be added to `.gitignore`

## 📦 Dependencies

- **tmdbv3api**: Python wrapper for the TMDb API
- **python-dotenv**: Loads environment variables from `.env` files

## 🐛 Troubleshooting

### "Source directory does not exist"
Make sure `ROOT_DIR` in `main.py` points to an existing directory.

### "TMDB_API_KEY not set"
Check that a `.env` file exists with `TMDB_API_KEY=...`

### Movies are not found
- Verify that filenames contain the movie title and year (e.g., `The Matrix 1999.mkv`)
- Some movies may not be in the TMDb database

## 📄 License

[Please add license]

## 👤 Author

[Please add name]

## 🤝 Contributing

Contributions are welcome! Please create a pull request with your improvements.
