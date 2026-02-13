# CLAUDE.md

## Project Overview

**Hello** is a single-page interactive greeting web application. It displays a personalized greeting based on user input, real-time date/time, and current weather information. The entire application lives in a single `index.html` file with no build system or dependencies to install.

## Repository Structure

```
Hello/
└── index.html    # Entire application (HTML + CSS + JavaScript)
```

There is no build system, package manager, bundler, or preprocessor. The project is pure static HTML/CSS/JavaScript served directly from the single file.

## How to Run

Open `index.html` in a web browser. No server, build step, or installation required.

For local development with a server (useful for testing geolocation/fetch):
```bash
python3 -m http.server 8000
# Then open http://localhost:8000
```

## Architecture

The application is a monolithic single-file SPA structured as:

| Section | Lines | Description |
|---------|-------|-------------|
| HTML structure | 1-6, 276-414 | Semantic HTML5 markup |
| CSS styles | 7-274 | Embedded `<style>` block |
| JavaScript | 302-408 | Embedded `<script>` block |

### Key HTML Elements (by ID)

- `nameInput` - Text input for the user's name
- `greeting` - Displays the personalized greeting
- `datetime` - Shows current date and time
- `weather` - Shows weather information

### JavaScript Functions

- **`updateDateTime()`** - Updates the date/time display every second using `toLocaleString`
- **`getWeather()`** - Requests geolocation, fetches weather from wttr.in API using coordinates
- **`fetchDefaultWeather()`** - Fallback that fetches London weather when geolocation is unavailable

### External Dependencies (CDN/API)

- **Google Fonts** - Poppins font family (weights: 300, 400, 600, 700)
- **wttr.in API** - Weather data (`https://wttr.in/{lat},{lon}?format=j1`), no API key required
- **Browser Geolocation API** - User location for weather lookup

## Code Conventions

### Naming

- **HTML IDs**: camelCase (`nameInput`, `greeting`, `datetime`, `weather`)
- **CSS classes**: kebab-case (`info-card`, `input-group`, `weather-info`)
- **JS variables/functions**: camelCase (`updateDateTime`, `getWeather`, `fetchDefaultWeather`)

### CSS Patterns

- Sunset orange color scheme: `#ff6b6b`, `#ff8e53`, `#feb47b`
- Glassmorphism: semi-transparent backgrounds with `backdrop-filter: blur()`
- Gradient text via `background-clip: text`
- Keyframe animations: `float`, `slideUp`, `pulse`, `fadeIn`
- Mobile breakpoint at `max-width: 600px`

### JavaScript Patterns

- Event-driven input handling via `addEventListener`
- `async/await` for API calls with `try/catch` error handling
- Graceful degradation: geolocation failure falls back to London weather
- `setInterval` for real-time clock updates

## Testing

No test framework or tests exist. To verify changes manually:
1. Open `index.html` in a browser
2. Confirm the greeting updates as you type a name
3. Confirm the date/time updates every second
4. Confirm weather data loads (may require allowing location access)
5. Test on mobile viewport (600px breakpoint)

## Deployment

The project is a single static file. Deploy by serving `index.html` through any static hosting provider (GitHub Pages, Netlify, Vercel, etc.) or any web server.

## Common Modification Patterns

- **Change color scheme**: Update the gradient values in `body`, `h1`, `.greeting`, `.info-card h3`, and the input border gradient (all in the `<style>` block)
- **Change default weather location**: Modify the fetch URL in `fetchDefaultWeather()` (line 386)
- **Add new info cards**: Follow the existing `.info-card` HTML pattern and add corresponding JS logic
- **Modify animations**: Edit the `@keyframes` blocks (`float`, `slideUp`, `pulse`, `fadeIn`)
