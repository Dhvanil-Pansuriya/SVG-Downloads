# SVG Icon Scraper for SimpleIcons.org

This Node.js script automatically downloads SVG icons from [simpleicons.org](https://simpleicons.org/) based on icon names listed in `input/req.txt`.

## 📁 Project Structure

```
SVG Downloads/
├── src/
│   └── scraper.js          # Main scraper script
├── input/
│   └── req.txt             # List of icon names to download
├── output/
│   └── svgs/               # Downloaded SVG files (auto-generated)
├── package.json            # Project dependencies
├── README.md               # This file
└── .gitignore             # Git ignore rules
```

## 📋 Prerequisites

- Node.js (v14 or higher)
- npm or yarn

## 🚀 Installation

1. Install the required packages:

```bash
npm install
```

This will install:
- `puppeteer` - For browser automation
- `fs-extra` - For file system operations

## 📝 Usage

1. **Edit `input/req.txt`**: Add the icon names you want to download (one per line)
   ```
   react
   nextjs
   vue
   angular
   typescript
   ```

2. **Run the script**:
   ```bash
   npm start
   ```
   
   Or directly:
   ```bash
   node src/scraper.js
   ```

3. **Find your SVGs**: Downloaded SVG files will be saved in the `output/svgs/` directory

## 📁 Output

- All SVG files are saved in the `output/svgs/` folder
- Files are named using your search term (e.g., `nextjs.svg`, `react.svg`, `vue.svg`)
- **Smart naming**: Handles SimpleIcons internal naming (e.g., `nextdotjs.svg` → `nextjs.svg`)

## 🔧 How It Works

1. Reads icon names from `input/req.txt`
2. For each icon name:
   - Searches on simpleicons.org using the query parameter
   - Finds the first matching result
   - Extracts the SVG file path
   - Downloads the SVG content
   - **Saves with clean filename** based on your search term (removes "dot" suffixes)
3. Provides a detailed summary of successful and failed downloads

## ✨ Features

- **Clean file naming**: Automatically removes "dot" from filenames
  - `nextdotjs.svg` → `nextjs.svg`
  - `vuedotjs.svg` → `vue.svg`
- **Organized structure**: Separate folders for input, output, and source code
- **Progress tracking**: Real-time progress updates for each icon
- **Error handling**: Continues downloading even if some icons fail
- **Respectful scraping**: 1-second delay between requests

## 🐛 Troubleshooting

- **Puppeteer installation issues**: Try `npm install puppeteer --unsafe-perm=true`
- **Timeout errors**: Increase the timeout values in `src/scraper.js`
- **Icon not found**: Check if the icon name exists on simpleicons.org
- **Permission errors**: Ensure you have write permissions in the project directory

## 🎯 Tips

- Use lowercase names in `req.txt` for consistency
- One icon name per line
- Check simpleicons.org to verify icon availability
- The script will automatically create the `output/svgs/` directory

## 📄 License

ISC
