# 🕯️ Single Candle Stick Pattern Detection

> **Automated Technical Analysis using Computer Vision**

Welcome to the **Single Candle Stick Pattern Detection** project! This tool bridges the gap between traditional financial technical analysis and modern computer vision. Using state-of-the-art Deep Learning (YOLOv8), it automatically detects and classifies important candlestick patterns in stock market charts, helping traders identify potential market reversals or continuations in real-time.

---

## 📖 Overview

Technical analysis often involves staring at charts for hours to find specific patterns. This project automates that process. It fetches real-time stock data, generates candlestick charts, and uses a trained **Object Detection Model** to spot 6 specific single-candle patterns that are crucial for trading strategies.

The system is wrapped in a user-friendly **Web Application**, allowing anyone to search for a stock symbol (like `AAPL` or `TSLA`) and instantly see an annotated chart with detected patterns and their market sentiment (Bullish 🐂 / Bearish 🐻).

### 🎯 Key Features
*   **Real-time Analysis**: Fetches live daily stock data via Alpha Vantage.
*   **Visual Detection**: Draws bounding boxes around detected patterns on the chart.
*   **Sentiment Analysis**: Automatically tags patterns as **Bullish** (Signal to potential Buy), **Bearish** (Signal to potential Sell), or **Neutral**.
*   **Interactive Web UI**: Simple, clean interface to analyze any stock.
*   **6 Supported Patterns**:
    *   **Dragonfly Doji** (Bullish Reversal)
    *   **Gravestone Doji** (Bearish Reversal)
    *   **Hammer** (Bullish Reversal)
    *   **Hanging Man** (Bearish Reversal)
    *   **Marubozu** (Trend Continuation)
    *   **Spinning Top** (Indecision)

---

## 🛠️ Tech Stack

This project is built with a robust Python stack, combining financial data auditing with computer vision.

*   **Core AI/ML**: `PyTorch`, `Ultralytics YOLOv8` (Object Detection)
*   **Web Backend**: `Flask` (Python Web Server)
*   **Frontend**: HTML/CSS/JavaScript (Embedded in Flask)
*   **Data Handling**: `Pandas`, `NumPy`
*   **Visualization**: `Matplotlib`, `mplfinance` (Financial Plotting)
*   **Data Source**: `Alpha Vantage API`

---

## 🚀 Getting Started

Follow these steps to set up the project on your local machine.

### Prerequisites
*   Python 3.11+ installed.
*   A free **Alpha Vantage API Key** (Get one [here](https://www.alphavantage.co/support/#api-key)).
*   (Optional) A **Roboflow API Key** if you plan to retrain the model or download the dataset.

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd Single-Candle-Stick-Pattern-Detection-CV
```

### 2. Install Dependencies
It's recommended to create a virtual environment first.
```bash
# Create virtual env (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install requirements
pip install -r requirements.txt
```

### 3. Setup Configuration
Create a `.env` file in the project root to store your API keys. You can use the template provided.

**Create `.env`:**
```properties
# .env file
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key_here
ROBOFLOW_API_KEY=your_roboflow_key_here  # Optional: Only for training/data download
```

### 4. Weights Setup
Ensure the model weights are present. The application expects the best trained model at:
`models/weights/best.pt`

(If you have trained the model yourself, copy your `best.pt` to this location).

---

## 🖥️ Usage

### Running the Web Application
To start the user interface and analyze stocks:

1.  Run the Flask application:
    ```bash
    python webapp/app.py
    ```
2.  Open your browser and navigate to:
    ```
    http://localhost:5000
    ```
3.  Enter a stock symbol (e.g., `NVDA`, `GOOGL`) and click **Analyze**.

### Training / Data (Advanced)
If you want to download the raw dataset or explore the code structure:
*   **Download Data**: `python src/download_data.py`
*   **Configuration**: Check `src/config.py` to adjust model parameters, confidence thresholds, or chart settings.

---

## 📂 Project Structure

A quick guide to navigating the codebase:

```
├── webapp/                 # Web server & UI code
│   ├── app.py              # Flask backend entry point
│   └── index.html          # Frontend UI
├── src/                    # Core source code
│   ├── config.py           # Settings & Constants (Paths, Classes, Colors)
│   ├── alpha_vantage_api.py# Stock data fetching logic
│   ├── chart_generator.py  # Creates candle charts from data
│   ├── pattern_detector.py # Runs YOLO inference on charts
│   └── download_data.py    # Scripts for dataset management
├── models/                 # Model artifacts
│   └── weights/            # Trained .pt files go here
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```

---

## 💡 How It Works
1.  **Input**: User asks for stock "TSLA".
2.  **Fetch**: App calls Alpha Vantage API to get the last 100 days of OHLCV (Open, High, Low, Close, Volume) data.
3.  **Render**: `mplfinance` converts this data into a clean candlestick chart image (without indicators/grid lines to avoid noise).
4.  **Detect**: The image is passed to `YOLOv8`, which scans for the 6 learned visual patterns.
5.  **Result**: The tagged image is sent back to the browser, displaying exactly where the Hammer or Doji occurred!

---

## 🤝 Contributing
Feel free to open issues or submit pull requests if you have ideas for better detection accuracy or new features!

---

*Verified locally on macOS (Apple Silicon).*
