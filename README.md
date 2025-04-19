# 🌤️ Historical Weather Scraper

This Python project scrapes historical **daily maximum temperatures** for selected cities from [Weather Underground](https://www.wunderground.com/) over a specified date range. It stores the data in CSV files — one file per city — in Celsius.

---

## 📁 Project Structure

```
.
├── WeatherScrapper.ipynb     # Main notebook that runs the scraper
├── requirements.txt          # All dependencies listed here
├── output/                   # Directory where CSVs will be saved
└── README.md                 # You're here
```

---

## 📍 Cities Covered

- Taipei
- Hangzhou
- Beijing
- Tehran
- Shenzhen

Each city is mapped to a specific airport/station code used by Weather Underground.

---

## ⚙️ Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/KarolC02/WebScrapper
cd WebScrapper
```

### 2. Create and activate a Python virtual environment

#### ✅ For Linux/macOS:
```bash
python3 -m venv venv
source venv/bin/activate
```

#### ✅ For Windows:
```bash
python -m venv venv
venv\Scripts\activate
```

### 3. Install all dependencies
```bash
pip install -r requirements.txt
```

---

## 📦 Dependencies

The main dependencies are:
- `selenium` — for dynamic page rendering
- `beautifulsoup4` — for parsing HTML
- `requests`, `re`, and standard libraries
- `chromedriver-autoinstaller` *(optional, if you're auto-installing drivers)*

---

## 🧪 Running the Scraper

This project is built as a Jupyter Notebook. To run it:

### 1. Launch Jupyter
```bash
jupyter notebook
```

### 2. Open `WeatherScrapper.ipynb`

From the Jupyter interface, click to open the notebook named:

```
WeatherScrapper.ipynb
```

### 3. Run the notebook

Execute all cells (select `Run All` or use Shift+Enter through each one).  
The scraper will start collecting and saving data in CSV format.

---

The script will:
- Load each city's station code
- Iterate from 2005-01-01 to 2025-04-15 (or fewer, if limited)
- Scrape max temperature for each day using Selenium and BeautifulSoup
- Convert values from Fahrenheit to Celsius (rounded to 2 decimal places)
- Save daily values to CSV in the `output/` directory

---

## 🔧 `fill_csv_with_weather_data()` Parameters

The scraping logic is driven by the function:

```python
def fill_csv_with_weather_data(
    station_code_dic: dict = station_code_dic,
    specific_cities: list[str] = station_code_dic.keys(),
    limited_days=False,
    days_to_cover: int = -1
) -> None
```

- **`station_code_dic`** – maps city names to ICAO airport codes for scraping
- **`specific_cities`** – subset of cities to scrape (default: all)
- **`limited_days`** – if `True`, only scrape a limited number of days per city
- **`days_to_cover`** – number of days to scrape per city when `limited_days` is enabled

### Example:

Scrape just 3 days of data for Beijing and Shenzhen:
```python
fill_csv_with_weather_data(specific_cities=["Beijing", "Shenzhen"], limited_days=True, days_to_cover=3)
```

---

## 📝 Sample Output

Each CSV file looks like this:

```
Date,Max Temperature
2005-01-01,21.1
2005-01-02,22.3
...
```

---

## 💡 Notes

- The scraper uses **headless Chrome** via Selenium. Make sure you have **Google Chrome** installed.
- The script automatically creates the `output/` folder if it doesn't exist.
- For best results, run this script with a stable internet connection and avoid interrupting long runs.
- The code includes error handling and logs dates where no temperature data was found.

---

## 📌 Troubleshooting

- **Chromedriver issues?** Make sure your `chromedriver` version matches your installed Chrome version.
- **Data missing or inconsistent?** Try increasing `WebDriverWait` or adding `time.sleep(1.5)` between requests.
- **Rate-limiting?** Consider adding exponential backoff or retry logic.
- **Page not loading?** Make sure you're waiting long enough in Selenium before grabbing `page_source`.

---
