# Morro Bay Weather Station

A simple, clean weather display for the Morro Bay (Back Bay) station showing current conditions.

## What It Shows

- **Temperature** - Current air temperature in °F
- **Rain** - 24-hour precipitation accumulation in inches
- **Wind Speed** - Current wind speed in mph
- **Tide** - Current water level in feet (MLLW datum)

## Data Sources

- **Weather Data**: [CeNCOOS ERDDAP](https://erddap.cencoos.org/) - Station `edu_calpoly_marine_morro_bay_met`
- **Tide Data**: [NOAA Tides & Currents API](https://tidesandcurrents.noaa.gov/) - Station `9412110` (Morro Bay)

## Setup for GitHub Pages

1. **Create a new GitHub repository**
   ```bash
   # Navigate to the project directory
   cd morro-bay-weather

   # Initialize git repository
   git init
   git add .
   git commit -m "Initial commit: Morro Bay weather station"
   ```

2. **Push to GitHub**
   ```bash
   # Create a new repository on GitHub first, then:
   git remote add origin https://github.com/YOUR-USERNAME/morro-bay-weather.git
   git branch -M main
   git push -u origin main
   ```

3. **Enable GitHub Pages**
   - Go to your repository on GitHub
   - Click **Settings** → **Pages**
   - Under "Build and deployment":
     - **Source**: Select "GitHub Actions"
   - The workflow will automatically deploy on the next push

4. **Access your site**
   - After the workflow completes, your site will be live at:
   - `https://YOUR-USERNAME.github.io/morro-bay-weather/`

## How It Works

### Data Freshness
- Data is fetched **on page load** and when you click **"Refresh Data"**
- No automatic background updates (keeps it simple and reduces API calls)
- Weather data is typically updated every 5-10 minutes by the station
- Tide data is updated every 6 minutes by NOAA

### API Calls
The site makes two API calls when you refresh:

1. **ERDDAP (CeNCOOS)** - Gets the latest weather measurements
   ```
   https://erddap.cencoos.org/erddap/tabledap/edu_calpoly_marine_morro_bay_met.json
   ```

2. **NOAA CO-OPS** - Gets the current tide level
   ```
   https://api.tidesandcurrents.noaa.gov/api/prod/datagetter
   ```

Both APIs are public and don't require authentication.

### Browser Compatibility
Works in all modern browsers. The site uses:
- Native Fetch API for data retrieval
- No external dependencies or frameworks
- Responsive design for mobile and desktop

## Customization

### Change Units
Edit `index.html` to modify the unit conversions:

```javascript
// Temperature: Change to Celsius
document.getElementById('temperature').textContent = weatherData.temperature.toFixed(1);
// Update the unit label in HTML from °F to °C

// Wind: Keep in m/s
document.getElementById('windspeed').textContent = weatherData.windSpeed.toFixed(1);
// Update the unit label in HTML from mph to m/s

// Rain: Keep in mm
document.getElementById('rainfall').textContent = weatherData.precipitation.toFixed(1);
// Update the unit label in HTML from in to mm
```

### Add Auto-Refresh
To add automatic updates, add this to the `<script>` section:

```javascript
// Refresh every 5 minutes (300000 ms)
setInterval(updateDisplay, 300000);
```

### Styling
All styles are in the `<style>` section of `index.html`. The design uses:
- Gradient background (purple/blue)
- White card container
- Clean typography
- Large, readable numbers

## Development

To test locally:
```bash
# Serve with any static file server
python3 -m http.server 8000

# Or use Node.js
npx serve .

# Then open http://localhost:8000
```

## About the Station

**Morro Bay BS1 Met Station**
- Location: 35.3338°N, 120.8473°W
- Operator: Cal Poly San Luis Obispo / SLOSEA
- Part of: CeNCOOS (Central & Northern California Ocean Observing System)
- Data available since: February 2016

## Troubleshooting

**"Error loading data"**
- Check browser console for details
- ERDDAP or NOAA APIs might be temporarily unavailable
- Try again in a few minutes

**Tide shows "N/A"**
- NOAA tide data may be temporarily unavailable
- Weather data will still load normally

**Page won't deploy**
- Check GitHub Actions tab for workflow errors
- Ensure GitHub Pages is enabled in repository settings
- Verify the workflow file is in `.github/workflows/`

## License

This project is free to use and modify. Weather and tide data are provided by public government agencies (NOAA, CeNCOOS).

## Resources

- [CeNCOOS Shore Station Network](https://www.cencoos.org/observations/sensor-platforms/shore-stations/)
- [ERDDAP Documentation](https://erddap.cencoos.org/erddap/information.html)
- [NOAA Tides & Currents API](https://api.tidesandcurrents.noaa.gov/api/prod/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
