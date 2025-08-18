# Orphaned-Torrents-Finder

A Python script that finds orphaned files in your qBittorrent completed downloads folder. It compares files in your completed folder against the active torrents in qBittorrent and generates removal commands for orphaned files.

## Features

- Connects to qBittorrent Web API to get active torrents
- Scans completed downloads folder (including category subfolders)
- Identifies orphaned files not associated with any active torrents
- Generates Linux removal commands for cleanup
- Excludes files in the "ISOs" category from deletion

## Requirements

- Python 3.6+
- qBittorrent with Web UI enabled
- Access to the completed downloads folder

## Installation

1. Clone the repository:
```shell
git clone https://github.com/Owen-3456/Orphaned-Torrents-Finder.git
cd Orphaned-Torrents-Finder
```

2. Install dependencies:
```shell
python -m pip install -r requirements.txt
```
   Or install manually:
```shell
python -m pip install requests python-dotenv
```

3. Configure environment variables:
   - Copy `.env-example` to `.env`
   - Edit `.env` with your settings:
```shell
cp .env-example .env
```

## Configuration

Edit the `.env` file with your qBittorrent and folder settings:

```properties
QB_URL=http://localhost:8080
QB_USER=admin
QB_PASS=your_password
COMPLETED_FOLDER=/path/to/completed/downloads
```

### Environment Variables

- `QB_URL`: URL to your qBittorrent Web UI (default: http://localhost:8080)
- `QB_USER`: qBittorrent Web UI username (default: admin)
- `QB_PASS`: qBittorrent Web UI password (default: admin)
- `COMPLETED_FOLDER`: Path to your completed downloads folder

## Usage

Run the script:
```shell
python orphaned-torrents-finder.py
```

The script will:
1. Connect to qBittorrent and retrieve active torrents
2. Scan your completed folder for files and subfolders
3. Compare the two lists to find orphaned files
4. Display orphaned files and generate removal commands
5. Output bash commands to delete orphaned files (excluding ISOs)

## Output

The script provides detailed output including:
- Number of torrents found in qBittorrent
- Number of files found in completed folder
- List of orphaned files with their categories
- Generated bash commands for file removal

## Safety Features

- Files in the "ISOs" category are automatically excluded from deletion
- Commands are only displayed, not executed automatically
- Review the generated commands before running them

## Troubleshooting

### Common Issues

1. **Environment variables not loaded**: Make sure you have a `.env` file in the same directory as the script
2. **qBittorrent connection failed**: Verify the `QB_URL` is correct and qBittorrent Web UI is enabled
3. **Permission denied**: Ensure the script has access to read the completed downloads folder
4. **Module not found errors**: Install all dependencies using `pip install -r requirements.txt`

### qBittorrent Web UI Setup

1. Open qBittorrent
2. Go to Tools → Options → Web UI
3. Enable "Web User Interface (Remote control)"
4. Set username and password
5. Note the port number (default: 8080)

## License

This project is open source. Please always backup your data before running cleanup commands. I'm not responsible for any data loss.
