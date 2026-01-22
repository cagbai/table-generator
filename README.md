# HTML Table Generator for Webflow

A simple, local-first web app that generates responsive HTML tables from CSV data or pasted content. Designed specifically for embedding tables in Webflow rich text elements or code embeds.

## Features

- **Multiple input methods**: Paste data directly or upload CSV/TSV files
- **Flexible delimiter support**: Auto-detect, comma, tab, semicolon, or line-per-cell (Google Docs)
- **Google Docs compatibility**: Special parsing mode for tables copied from Google Docs
- **Customizable styling**: Header colors, border colors, cell padding, alternating row colors
- **Responsive output**: Tables scroll horizontally on smaller screens
- **Easy export**: Copy to clipboard or download as HTML file
- **Live preview**: See the table before copying the code

## Usage

### Running Locally

Simply open `index.html` in any modern web browser:

```bash
open index.html
```

Or double-click the file in Finder/Explorer.

### Input Formats

#### Tab or Comma Separated (from Excel, Google Sheets, etc.)

```
Model,Developer,Release Date
Claude Opus 4.5,Anthropic,Nov-25
GPT-5.2,OpenAI,Dec-25
```

#### Line-per-cell (from Google Docs tables)

When copying tables from Google Docs, each cell appears on its own line:

```
Header 1
Header 2
Header 3
Row 1 Cell 1
Row 1 Cell 2
Row 1 Cell 3
```

Select "Line-per-cell (Google Docs)" from the delimiter dropdown and specify the number of columns.

### Generated HTML Structure

The app generates a responsive table wrapped in a scrollable container:

```html
<div style="overflow-x: auto; width: 100%;">
  <table style="width: 100%; border-collapse: collapse; min-width: 600px;">
    <thead>
      <tr style="background-color: black; color: white;">
        <th style="padding: 1rem; text-align: left; ...">Header</th>
      </tr>
    </thead>
    <tbody>
      <tr style="background-color: white;">
        <td style="padding: 1rem; ...">Cell</td>
      </tr>
      <tr style="background-color: #f9f9f9;">
        <td style="padding: 1rem; ...">Cell</td>
      </tr>
    </tbody>
  </table>
</div>
```

### Customization Options

| Option | Default | Description |
|--------|---------|-------------|
| Delimiter | Auto-detect | How cells are separated in input data |
| Number of Columns | 3 | Only shown for line-per-cell mode |
| Header Background | `black` | Background color of header row |
| Header Text Color | `white` | Text color of header row |
| Border Color | `#e0e0e0` | Color of cell borders |
| Cell Padding | `1rem` | Padding inside each cell |
| Alternating Row Color | `#f9f9f9` | Background color for odd rows |

## Project Structure

```
table-generator/
├── index.html      # The entire application (HTML, CSS, JS)
├── vercel.json     # Vercel deployment configuration
└── README.md       # This file
```

## Technical Details

### Architecture

This is a single-file application with no dependencies or build process. All HTML, CSS, and JavaScript are contained in `index.html`.

### Key Functions

| Function | Description |
|----------|-------------|
| `detectDelimiter(text)` | Auto-detects whether input uses tabs, commas, or semicolons |
| `parseCSV(text, delimiter)` | Parses CSV/TSV with proper quote handling |
| `generateTable()` | Main function that parses input and generates HTML output |
| `escapeHtml(text)` | Sanitizes text to prevent XSS |
| `copyToClipboard()` | Copies generated HTML to clipboard |
| `downloadHTML()` | Downloads generated HTML as a file |

### Browser Compatibility

Works in all modern browsers (Chrome, Firefox, Safari, Edge). Uses standard Web APIs:
- Clipboard API for copy functionality
- FileReader API for CSV upload
- No polyfills required

## Development

### Making Changes

1. Edit `index.html` directly
2. Refresh browser to see changes
3. Test with various input formats

### Adding New Delimiter Types

1. Add option to the delimiter `<select>` element
2. Update `generateTable()` to handle the new delimiter
3. If needed, add UI elements for additional configuration

### Modifying Table Styles

The table styles are generated in the `generateTable()` function. Look for the template literals that build the HTML string.

## Deployment

### Vercel (Current Setup)

The app is deployed on Vercel. To deploy updates:

```bash
vercel --prod
```

Or push to GitHub and deploy via Vercel dashboard if GitHub integration is enabled.

### Other Static Hosts

Since this is a single HTML file with no build process, it can be deployed to any static hosting:

- **GitHub Pages**: Push to a `gh-pages` branch
- **Netlify**: Drag and drop the folder
- **Any web server**: Just serve `index.html`

## URLs

- **GitHub**: https://github.com/cagbai/table-generator
- **Live App**: https://table-generator-cagbais-projects.vercel.app

## License

MIT
