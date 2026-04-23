# 📦 DataPrime — Interactive E-Commerce Analytics Dashboard

> **Drop your CSVs. Watch your data come alive.**

![Dashboard Preview](https://img.shields.io/badge/status-live-brightgreen?style=flat-square) ![HTML](https://img.shields.io/badge/built%20with-HTML%20%2F%20JS-FF9900?style=flat-square) ![No Backend](https://img.shields.io/badge/backend-none-black?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-orange?style=flat-square)

DataPrime is a **zero-dependency, browser-only analytics dashboard** built for e-commerce data. Upload your five CSV exports, hit one button, and instantly get an interactive dashboard with KPIs, trend charts, category breakdowns, and a city-level customer map — all styled in Amazon's iconic orange and black.

No server. No setup. No accounts. Just open the HTML file and go.

---

## ✨ Features

| Feature | Details |
|---|---|
| 📂 **5-file CSV upload** | Drag-and-drop zones for Customers, Order Items, Payments, Products & Transactions |
| 📊 **4 KPI Buckets** | Delivered On Time %, Total Purchases, Total Customers, Total Revenue |
| 📈 **Trend Analysis** | Line chart with weekly / monthly / yearly granularity |
| 🏷️ **Top 5 Product Categories** | Horizontal bar chart, filtered in real time |
| 🌆 **Top 10 Cities** | Ranked table with revenue and customer share bar |
| 🔍 **Global Filters** | Metric type, time granularity, and date range — all charts react instantly |
| 🔗 **Smart Table Joins** | Auto-joins across all five files using the schema below |
| 🎨 **Amazon-themed UI** | Orange `#FF9900` + deep black, animated, fully responsive |

---

## 🚀 Getting Started

No installation needed. Seriously.

```bash
# Clone the repo
git clone https://github.com/your-username/dataprime.git

# Open the dashboard
open amazon_dashboard.html
```

Or just **[download the HTML file](./amazon_dashboard.html)** and open it in any modern browser.

---

## 📁 Expected CSV Files

Upload one file per slot. Column names are auto-detected (case-insensitive).

### 👤 Customers
| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `customer_city` | City used for the Top Cities table |

### 📊 Customer Transactions
| Column | Description |
|---|---|
| `order_id` | Links to Order Items and Payments |
| `customer_id` | Links to Customers |
| `order_status` | Used for Delivered On Time % (value: `delivered`) |
| `order_purchase_timestamp` | **Primary date column** — drives all date filters |

### 🛒 Order Items
| Column | Description |
|---|---|
| `order_id` | Links to Transactions |
| `product_id` | Links to Products |
| `price` / `order_item_total` | Optional — used for revenue fallback |

### 💳 Payments
| Column | Description |
|---|---|
| `order_id` | Links to Transactions |
| `payment_value` | Used for Total Revenue calculations |

### 📦 Products
| Column | Description |
|---|---|
| `product_id` | Links to Order Items |
| `product_category_name` | Drives the Top Categories chart |

---

## 🔗 Data Model & Join Logic

```
Customers ──────────────────────────────┐
  customer_id                           │
                                        ▼
Transactions ── customer_id ──► [Customer lookup]
     │
     └── order_id ──► Payments (payment_value → Revenue)
     │
     └── order_id ──► Order Items
                           │
                           └── product_id ──► Products (category_name)
```

All joins happen **in-browser at runtime** using pre-built lookup maps — no SQL, no server.

---

## 📐 Metrics Reference

| Metric | Calculation |
|---|---|
| **Delivered On Time %** | `COUNT(order_status = 'delivered') / COUNT(*)` from Transactions |
| **Total Purchases** | Count of rows in filtered Transactions |
| **Total Customers** | `COUNT DISTINCT(customer_id)` from Customers file |
| **Total Revenue** | `SUM(payment_value)` from Payments file |

> KPI buckets respond to the **date range** filter only.
> Charts respond to **all filters** (metric, granularity, date range).

---

## 🛠️ Built With

- **[PapaParse](https://www.papaparse.com/)** — CSV parsing
- **[Chart.js](https://www.chartjs.org/)** — Trend line & category bar charts
- **[Google Fonts](https://fonts.google.com/)** — Rajdhani + DM Sans
- **Vanilla JS** — Zero frameworks, zero build steps

---

## 🗂️ Project Structure

```
dataprime/
│
├── amazon_dashboard.html   # The entire app — single self-contained file
└── README.md               # You are here
```

Everything lives in one HTML file. CSS, JS, and markup — all in one place, intentionally. Makes it dead simple to share, fork, or embed.

---

## 🖼️ Dashboard Walkthrough

```
┌─────────────────────────────────────────────────────┐
│  📦 DataPrime                        Analytics Dash  │
├─────────────────────────────────────────────────────┤
│  [ Customers ] [ Orders ] [ Payments ] [ Products ]  │
│  [ Transactions ]                                    │
│                                                      │
│              🚀 Let's Analyze It!                    │
├─────────────────────────────────────────────────────┤
│  Filters: Metric ▾  Granularity ▾  From──To         │
├────────────┬────────────┬────────────┬──────────────┤
│ Delivered  │  Total     │  Total     │   Total      │
│ On Time %  │  Purchases │  Customers │   Revenue    │
├────────────┴──────────────┬──────────┴──────────────┤
│  📈 Trend Analysis        │  🏷️ Top Categories       │
│                           │                          │
├───────────────────────────┴──────────────────────────┤
│  🌆 Top 10 Cities — customers · revenue · share bar  │
└──────────────────────────────────────────────────────┘
```

---

## 🤝 Contributing

Got ideas? Found a bug? PRs are welcome.

1. Fork the repo
2. Create your branch: `git checkout -b feature/my-improvement`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/my-improvement`
5. Open a Pull Request

---

## 📄 License

MIT © [Your Name](https://github.com/your-username)

---

<div align="center">
  <strong>Built with ☕ and 🟠 — because data should be beautiful.</strong>
</div>
