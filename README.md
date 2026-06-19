# ✈️ AeroInsights — Airline Revenue Analytics Dashboard

A React-based single-page application built as a frontend engineering project at KL University. AeroInsights lets airline revenue analysts monitor KPIs, visualize revenue trends, track seat occupancy, and review forecast accuracy — all in one secured dashboard.

---

## 🚀 Quick Start

```bash
# 1. Extract the zip and navigate into the folder
cd aeroinsights-final

# 2. Install dependencies
npm install

# 3. Start the development server
npm run dev
```

Open your browser at **http://localhost:5173**

> Sign up first, then log in to access the dashboard and all module pages.

---

## 📁 Project Structure

```
aeroinsights-final/
├── index.html
├── vite.config.js
├── package.json
└── src/
    ├── main.jsx                      # Entry point — renders App into DOM
    ├── App.jsx                       # Root component — all routes defined here
    ├── styles.css                    # Global stylesheet (light theme)
    ├── context/
    │   └── AeroContext.jsx           # Global state + Axios API call
    ├── components/
    │   ├── Header.jsx                # Top nav bar with logout
    │   ├── Footer.jsx                # Bottom bar
    │   ├── KPICards.jsx              # 5 metric cards
    │   ├── RevenueTrendChart.jsx     # LineChart (actual vs forecast)
    │   ├── LoadFactorChart.jsx       # PieChart donut (occupancy)
    │   ├── TopRoutes.jsx             # Top 5 routes table
    │   ├── FilterControls.jsx        # Route + date filter bar
    │   └── InsightsPanel.jsx         # Insight cards on Dashboard
    └── pages/
        ├── Home.jsx                  # Landing page
        ├── Login.jsx                 # Login form
        ├── Signup.jsx                # Signup form
        ├── Dashboard.jsx             # KPIs + module summaries
        ├── Revenue.jsx               # LineChart + routes table
        ├── LoadFactor.jsx            # PieChart + occupancy table
        ├── Forecast.jsx              # BarChart + gap analysis table
        └── Insights.jsx              # 6 categorized insight cards
```

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 18.2.0 | UI component framework |
| React Router DOM | 6.22.0 | Client-side routing / SPA navigation |
| Axios | 1.6.7 | HTTP client for API calls |
| Recharts | 2.12.0 | Chart components (Line, Pie, Bar) |
| Vite | 5.1.0 | Build tool and dev server |

---

## 📊 Pages & Features

### 🏠 Home
Landing page with a hero section and feature highlights. Navigates to Login or Dashboard depending on auth state.

### 🔐 Login / Signup
Split-panel auth forms. Credentials stored in browser LocalStorage. Password confirmation and duplicate username checks on signup.

### 📋 Dashboard *(protected)*
- 5 KPI cards — Total Revenue, Total Passengers, Load Factor, Total Flights, Net Profit
- 4 module summary banners with color-coded status tags
- Data fetched live from dummyjson API via Axios

### 📊 Revenue *(protected)*
- LineChart — actual (solid) vs forecast (dashed) revenue across 8 months
- 4 stat boxes — revenue, forecast, avg ticket price, revenue per passenger
- Top 5 routes table with contribution percentage bars

### 🪑 Load Factor *(protected)*
- PieChart (donut) — occupied vs unoccupied seats
- Route occupancy table — 7 routes with Good / Average / Low status badges
- 4 stat boxes — load factor %, occupied seats, empty seats, below-threshold count

### 🔮 Forecast *(protected)*
- BarChart — grouped bars for actual vs forecast per month
- 4 stat boxes — actual, forecast, gap, accuracy
- Month-by-month gap table with Above / Below Target badges

### 💡 Insights *(protected)*
- 6 auto-generated insight cards
- Color-coded by type — green (success), yellow (warning), blue (informational)
- Summary count boxes at the top

---

## 🌐 API Integration

Data is fetched from **[dummyjson.com](https://dummyjson.com)** — the same API used in class examples — and transformed into airline metrics.

```
dummyjson.com/products?limit=100  ──┐
                                     ├── Promise.all (parallel fetch)
dummyjson.com/users?limit=50      ──┘
        │
        ▼
.reduce()  →  Total Revenue
.filter()  →  Load Factor %
.map()     →  Revenue Trend (monthly)
        │
        ▼
AeroContext (global state)
        │
        ▼
KPICards / Charts / Tables
```

If the API is unreachable, the app shows a fallback error state instead of crashing.

---

## 🔑 Authentication Flow

```
Signup → credentials saved to LocalStorage (JSON array under key "users")
   ↓
Login → Array.find() checks username + password match
   ↓
Success → isLoggedIn = "true" + username saved to LocalStorage
   ↓
Protected pages → useEffect checks isLoggedIn on mount → redirect if missing
   ↓
Logout → removeItem("isLoggedIn") + removeItem("username") → redirect to Home
```

---

## 🗺️ Course Outcome Mapping

| CO | Concept | Where in Project |
|----|---------|-----------------|
| CO1 | Virtual DOM, declarative UI, component architecture | Every JSX component; `main.jsx` → `App.jsx` → pages → components |
| CO2 | ES6+ — async/await, Promise.all, .map/.filter/.reduce, destructuring | `AeroContext.jsx` — full data transformation pipeline |
| CO3 | useState, useEffect, props, controlled forms, .map() rendering | `Login.jsx`, `Signup.jsx`, `KPICards.jsx`, all page hooks |
| CO4 | Context API, Axios API integration, Recharts library | `AeroContext.jsx`, `RevenueTrendChart`, `LoadFactorChart`, `Forecast.jsx` |
| CO5 | React Router v6, protected routes, form validation, useNavigate | `App.jsx`, all protected pages, `Login.jsx`, `Signup.jsx` |
| CO6 | Vite build system, bundling, deployment | `vite.config.js`, `npm run build` → `dist/` for Netlify/Vercel |

---

## ⚙️ Available Scripts

```bash
npm run dev      # Start local dev server at localhost:5173
npm run build    # Build for production → outputs to dist/
npm run preview  # Preview the production build locally
```

---

## 📦 Deployment

After running `npm run build`, drag and drop the generated `dist/` folder into [Netlify](https://netlify.com) or [Vercel](https://vercel.com) for instant deployment.

---

## 📌 Assumptions & Notes

- No backend or database — all auth data lives in the browser's LocalStorage
- dummyjson data is transformed and scaled to simulate airline KPIs — it is not real airline data
- LocalStorage is browser-specific — credentials won't transfer between browsers or devices
- Tested on Chrome and Edge at 768px and above

---

## 👩‍💻 Built By

**Rasagnya M-2520090018,  Hasini P-2520030282**  
Frontend Engineering Project | B.Tech CSE  
Academic Year 2024–25
