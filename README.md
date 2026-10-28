# AgroSphere

Farm management + produce marketplace platform (Software Project Management course project).

## Modules

- Farm & Crop management
- Market & Batch Traceability
- Finance & Price Forecast
- Community forum
- Project status / milestone tracker

## Project Variants

| Variant | Folder | Stack | Data Storage |
|---|---|---|---|
| Prototype 1 (Static) | `website/index.html` | HTML / CSS / JS | Browser localStorage |
| Prototype 2 (Frontend v2) | `AgroSphere_Frontend_v2/` | React 18 + Vite + Tailwind | In-memory React state |
| Prototype 2 (Backend) | `website/AgroSphere/` | ASP.NET Core 8 MVC + EF Core | SQLite (`agrosphere.db`) |

## Prerequisites

- Node.js (includes npm), for Frontend v2
- .NET 8 SDK, for ASP.NET Core app

## Run

### Static Prototype
- Open `website/index.html` in a browser
- Or: `npx serve website`

### Frontend v2 (React + Vite)
```bash
cd AgroSphere_Frontend_v2
npm install      # first time only
npm run dev
```
- URL: http://localhost:5173
- Windows shortcut: `run_frontend_v2.bat`

### ASP.NET Core Backend
```bash
cd website/AgroSphere
dotnet restore
dotnet run
```
- URL: http://localhost:5000
- Windows shortcut: `run_backend.bat`

### Demo Accounts (Backend)

| Role | Username | Password |
|---|---|---|
| Admin | samarth | pass123 |
| Farmer | panth | pass123 |

- Login page has 1-click "Use" buttons for both
- New users can register via the Register link

## Frontend v2 Details

- **Stack:** React 18, Vite 5, Tailwind CSS 3, lucide-react, framer-motion, GSAP, Lenis, TanStack React Query
- **Theme:** dark glassmorphism (slate / emerald palette)
- **Features:**
  - Sidebar navigation (Dashboard, Farm & Crop, Market & Trace, Finance & Forecast, Community, Project Status)
  - Live KPI cards (Active Farms, Active Listings, Net Balance in ₹, Open Questions)
  - Add Listing modal with auto-generated batch code (`AGS-XXX`)
  - Milestone tracker (Architecture, Core Platform, Marketplace MVP, Pilot Launch)

```
AgroSphere_Frontend_v2/
├── index.html
├── package.json
├── vite.config.js
└── src/
    ├── main.jsx
    ├── App.jsx
    └── index.css
```

## Backend Details

- **Stack:** ASP.NET Core 8 MVC, EF Core (code-first), SQLite, Razor views, session-based auth
- **Models:** User, Farm, Crop, InventoryItem, Listing, Order, Transaction, Forum

```
website/AgroSphere/
├── Program.cs
├── agrosphere.db
├── Data/AppDbContext.cs
├── Models/Models.cs
├── Controllers/
│   ├── AccountController      # login, register, logout
│   ├── HomeController         # dashboard stats
│   ├── FarmController         # plots, crops, inventory, resell
│   ├── MarketController       # listings, buy, orders, batch trace
│   ├── FinanceController      # ledger, subsidies, forecasts
│   └── CommunityController    # forum, replies, likes
└── Views/
```

### Cross-Module Logic

- **Buy from marketplace:**
  - Creates Order (batch ID `AGRO-YYYYMMDD-XXXX`)
  - Adds item to buyer's inventory
  - Logs Expense for buyer
  - Credits Income to seller (if registered)
- **Cancel order:** logs Refund in ledger
- **Resell inventory:** lists surplus stock on marketplace

## Troubleshooting

- **`DirectoryNotFoundException: C:\mnt\c\...` on `dotnet run`**
  - Cause: stale `bin/` and `obj/` built under WSL/Linux
  - Fix: delete `bin/` and `obj/` in `website/AgroSphere`, then run `dotnet run` again
- **Vite error `"Farm" is not exported by "lucide-react"`**
  - Fix: use `Tractor` icon instead of `Farm` in `src/App.jsx`
- **Port 5173 busy:** kill the old Vite process, or restart terminal
- **Stop any server:** `Ctrl + C`

## Roadmap

- Connect Frontend v2 to ASP.NET Core backend via REST APIs (React Query already included)
