# 📉 Ticker BuyLow – Smart Crypto Buy Signal Engine

**Ticker BuyLow** is a real-time crypto market watcher and analytics engine built on top of the Binance API. It monitors market tickers, identifies buy opportunities based on configurable logic, and surfaces price dip insights via a lightweight web UI and REST API.

---

## 💼 Business Context

Cryptocurrency markets are highly volatile, and manually tracking buying opportunities is inefficient for traders and portfolio managers. **Ticker BuyLow** automates this process:

- Detects and alerts on dips relative to rolling averages
- Tracks multiple crypto pairs in real time
- Offers web visualizations and API access for algorithmic trading pipelines
- Helps both individual investors and automated systems buy low — when prices deviate significantly below recent highs or averages

---

## ⚙️ Core Features

- 📊 **Real-Time Ticker Monitoring** using Binance API
- 🧠 **Buy Signal Calculation** based on configurable thresholds
- 📈 **Chart Visualization** with Highcharts
- 🧪 **Spring Boot Backend** with modular services
- 🚀 **Dockerized & Dev/Prod Ready** (3 Dockerfiles)
- 📡 **Scheduled Polling** via Spring `@Scheduled`
- 🔑 **API Key Config Handling** via profiles (dev/prod)

---

## 🛠 Architecture Overview

```
+---------------------+       +------------------------+
| Binance API         | <---> | APIClient (Dev/Prod)   |
+---------------------+       +------------------------+
         |                             |
         v                             v
+------------------+        +---------------------------+
| ScheduledTasks   |        | BuyLowPrimeService        |
| (fetches data)   |------->| Computes Buy Signals      |
+------------------+        +---------------------------+
         |                             |
         v                             v
+------------------+        +---------------------------+
| TradeFacts       |<------>| AnalyticsService          |
| TradeLog         |        | Profit/Sell Calculations  |
+------------------+        +---------------------------+
         |
         v
+------------------+
| Web Layer (Charts)|
+------------------+
```

---

## 🧪 Run Locally (Dev Mode)

### 1. Prerequisites
- Java 11+
- Maven
- Binance API Key (optional for deeper integrations)

### 2. Clone & Build

```bash
git clone https://github.com/your-org/ticker-buylow.git
cd ticker-buylow
./mvnw spring-boot:run -Dspring.profiles.active=dev
```

### 3. Access

- UI: [http://localhost:8080](http://localhost:8080)
- Charts: `/chart`
- API Endpoints: `/buylow`, `/facts`, `/log`, etc.

---

## 🐳 Docker Support

Choose your flavor:

- **Dev Mode**:
  ```bash
  docker build -f Dockerfile.dev -t ticker-dev .
  docker run -p 8080:8080 ticker-dev
  ```

- **Production Mode**:
  ```bash
  docker build -f Dockerfile -t ticker-prod .
  docker run -p 8080:8080 ticker-prod
  ```

- **Test Image**:
  ```bash
  docker build -f Dockerfile.test -t ticker-test .
  ```

---

## 🔐 Configuration

Set environment-specific keys in:

- `application-dev.properties`
- `application-prod.properties`

Customizable settings include:

- Binance base URL
- Refresh interval
- Ticker pairs to monitor
- Buy signal threshold %

---

## 🧱 Tech Stack

- Java 11, Spring Boot
- Maven
- Binance API
- Highcharts.js
- Thymeleaf templates
- Docker / Docker Compose

---

## 📈 Sample Output

```json
{
  "symbol": "ETHUSDT",
  "currentPrice": 1710.42,
  "isBuyLow": true,
  "dropPercent": 6.34,
  "buySignal": "Triggered"
}
```

---

## 📌 Future Enhancements

- Telegram/Slack notifications
- Signal customization via UI
- Trading bot hooks
- SQLite support for offline logging
- Multi-exchange support

---


