# SVG Icon Scraper for SimpleIcons.org

A Node.js tool to automatically download SVG icons from [simpleicons.org](https://simpleicons.org/) using parallel browser tabs for efficient batch processing.

## Features

- **Parallel Processing** - Downloads multiple icons simultaneously using 8 browser tabs
- **Automatic Backup** - Backs up existing files with timestamps before each run
- **Progress Tracking** - Real-time updates showing download progress
- **Clean File Naming** - Sanitizes filenames based on your search terms
- **Visible Mode** - Optional mode to watch the browser tabs in action
- **Error Handling** - Continues processing even if individual downloads fail

## Project Structure

```
SVG Downloads/
├── src/
│   ├── scraper.js          # Main scraper (headless mode)
│   └── scraper-visible.js  # Scraper with visible browser
├── input/
│   └── req.txt             # List of icon names to download (one per line)
├── output/
│   ├── svgs/               # Downloaded SVG files
│   └── old/                # Timestamped backups of previous downloads
├── package.json
├── README.md
└── .gitignore
```

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn

## Installation

1. **Clone or download this project**

2. **Install dependencies:**

```bash
npm install
```

This will install:
- `puppeteer` - Browser automation (handles Chromium installation)
- `fs-extra` - Enhanced file system operations

## Usage

### 1. Add Icon Names

Edit `input/req.txt` and add icon names (one per line):

```
react
nextjs
vue
angular
typescript
javascript
html5
css3
tailwind
bootstrap
nodejs
python
docker
kubernetes
```

### 2. Run the Scraper

**Standard Mode** - Headless browser with 8 parallel tabs:
```bash
npm start
```

**Visible Mode** - Watch the browser tabs in action:
```bash
npm run visible
```

### 3. Get Your SVGs

Downloaded SVG files will be in the `output/svgs/` directory.

## Output & Backup System

### Downloaded Files
- Saved in `output/svgs/` folder
- Named using your search term (e.g., `nextjs.svg`, `react.svg`)
- Special characters removed for clean filenames

### Automatic Backups
- Before each run, existing SVGs are backed up
- Backups saved in `output/old/YYYY-MM-DD_HH-MM-SS/`
- Previous downloads are never overwritten

Example backup structure:
```
output/
├── svgs/
│   ├── react.svg
│   └── vue.svg
└── old/
    ├── 2024-01-15_10-30-45/
    │   ├── react.svg
    │   └── vue.svg
    └── 2024-01-15_14-20-10/
        └── angular.svg
```

## How It Works

### Parallel Processing

1. **Launches browser with 8 tabs**
2. **Splits icon list into 8 chunks**
3. **Each tab processes its chunk:**
   - Navigates to search URL: `https://simpleicons.org/?q={iconName}`
   - Waits for search results
   - Extracts first matching icon
   - Downloads SVG content
   - Saves with sanitized filename
4. **All tabs work simultaneously**

### Example Output

```
========================================================
  OPTIMIZED SVG Icon Scraper - Parallel Tabs Mode
  Uses PROVEN search logic for 100% accuracy
========================================================

Found 110 icons to download
Parallel tabs: 8 (processing 8 icons simultaneously)

========================================================
DOWNLOADING ICONS
========================================================

[001/110] [TAB 1] Processing: react
  [TAB 1] [SUCCESS] react → React → react.svg
[002/110] [TAB 2] Processing: nextjs
  [TAB 2] [SUCCESS] nextjs → Next.js → nextjs.svg
[003/110] [TAB 3] Processing: vue
  [TAB 3] [SUCCESS] vue → Vue.js → vue.svg
...

========================================================
DOWNLOAD SUMMARY
========================================================
Total requested: 110
Successfully downloaded: 108
Failed: 2

Total time: 55.23 seconds
Average: 0.50 seconds per icon
```

## Configuration

You can adjust the number of parallel tabs in the scripts:

```javascript
// In src/scraper.js or src/scraper-visible.js
const PARALLEL_TABS = 8; // Change this number (recommended: 4-10)
```

**Note:** More tabs uses more memory and CPU resources.

## Troubleshooting

### Puppeteer Installation Issues
```bash
npm install puppeteer --unsafe-perm=true
```

### Icon Not Found
- Verify the icon exists on [simpleicons.org](https://simpleicons.org/)
- Try the exact name shown on the website
- Check for typos in `req.txt`

### Timeout Errors
- Reduce `PARALLEL_TABS` to 4 or 5
- Check your internet connection
- Some icons may take longer to load

### Permission Errors
- Ensure write permissions in the project directory
- Run terminal/command prompt as administrator (Windows)

### Memory Issues
- Reduce `PARALLEL_TABS` to 4
- Process icons in smaller batches
- Close other applications

## Tips & Best Practices

1. **Icon Names**
   - Use lowercase for consistency
   - One icon name per line in `req.txt`
   - Remove empty lines

2. **Performance**
   - 8 parallel tabs is optimal for most systems
   - Reduce to 4-5 if you have limited RAM
   - Increase to 10 if you have a powerful machine

3. **Visible Mode**
   - Useful for debugging
   - Watch all tabs working simultaneously
   - Uses slightly more resources

4. **Backups**
   - Old files are automatically backed up
   - Safe to run multiple times
   - Check `output/old/` for previous downloads

## Scripts

| Command | Description |
|---------|-------------|
| `npm start` | Run scraper in headless mode (8 parallel tabs) |
| `npm run visible` | Run scraper with visible browser windows |

## License

ISC

## Credits

- Icons from [Simple Icons](https://simpleicons.org/)
- Built with [Puppeteer](https://pptr.dev/)
