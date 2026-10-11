# ⚡ Survive the Month — Gen Z Personal Finance & What-If Simulator

> A modern, interactive fintech personal finance application designed for Gen Z to survive a strict **₹10,000 monthly budget** over 30 days. Beyond basic tracking, it connects income, balance, velocity burn, fixed commitments, savings milestones, and risk indicators into a live **What-If Simulation Engine**.

[![React](https://img.shields.io/badge/React-19-blue?logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite)](https://vitejs.dev/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.4-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![Zustand](https://img.shields.io/badge/State-Zustand-orange)](https://github.com/pmndrs/zustand)
[![Recharts](https://img.shields.io/badge/Charts-Recharts-22c55e)](https://recharts.org/)
[![Framer Motion](https://img.shields.io/badge/Motion-Framer_Motion-f43f5e?logo=framer)](https://www.framer.com/motion/)

---

## 🌐 Running App & Local Access Link

- **Live Local Web App URL**: [http://localhost:5173/](http://localhost:5173/) or [http://127.0.0.1:5173/](http://127.0.0.1:5173/)
- **Repository Owner**: [GNBharath2606](https://github.com/GNBharath2606)

---

## ✨ Key Highlights & Features

### 1. 🔮 The "What-If" Simulation Engine (Killer Feature)
Test impulsive spending decisions before committing real money:
- **Instant Consequence Modeling**: Input an amount (e.g., *₹2,000 wireless earbuds* or *₹2,500 weekend party*) or choose from Gen Z preset scenarios.
- **Before vs. After Impact Matrix**:
  - **Remaining Balance**: Real-time cushion shrinkage.
  - **Safe Daily Allowance**: Dynamically drops via `(Remaining Balance - Spend) ÷ Days Left`.
  - **Financial Health Score**: Velocity burn recalibration (0–100).
  - **Risk Level Escalation**: Visual badges transitioning from `LOW` to `MEDIUM` or `HIGH`.
  - **Savings Goals Delay**: Calculates how many days high-priority goals (e.g., *M3 MacBook Fund*) will be pushed back.
- **Budget Breaker Alert**: Triggers a high-contrast danger alert if a simulated purchase exceeds remaining reserves.
- **Commit or Discard**: Lock simulated expenses directly into the real ledger with celebratory confetti or discard without trace.

### 2. 📊 Bento Grid Dashboard
- **Financial Health Score (0–100)**: Circular animated SVG gauge measuring spending velocity, buffer days, and emergency runway.
- **Financial Risk Radar**: Live status indicators (`Safe to spend freely`, `Moderate caution`, `Budget burnout`).
- **Monthly Survival Budget Progress Card**:
  - Total Cap: **₹10,000**
  - Spent: **₹3,200**
  - Remaining: **₹6,800**
  - Safe Daily Allowance: **₹234 / day** (29 days remaining).
- **Quick Stats Grid**: Tracks upcoming subscriptions, active goals, daily allowance, and 14-day survival streak.
- **Interactive Donut Chart**: Recharts visualization of category breakdowns with custom hover tooltips.

### 3. 💳 Transaction Ledger & Leakage Radar
- Log planned, unexpected, and recurring commitments.
- Real-time consequence preview inside modals prior to logging.
- Filter by transaction type (`Planned`, `Unexpected`, `Recurring`) or category.
- Search expenses by keyword and audit unbudgeted leakage.

### 4. 🎯 Savings Goals & Auto-Debit Manager
- Track milestone funds (*M3 MacBook Air*, *Goa Roadtrip*, *Emergency Stash*).
- Quick deposit shortcuts (`+₹200`, `+₹500`, `+₹1000`) with celebratory particle animations upon reaching 100%.
- Monthly subscription switches to pause or resume recurring services (Spotify, Netflix, Gym) that dynamically adjust monthly commitments.

---

## 🏛️ Component Architecture & File Structure

Strict multi-file component design adhering to modular architecture:

```
src/
├── types/
│   └── index.ts                 # TypeScript interfaces (Expense, Goal, Sub, SimulationResult, etc.)
├── store/
│   └── financeStore.ts          # Zustand store with localStorage persistence & derived hooks
├── utils/
│   ├── calculations.ts          # Health score, risk radar, daily allowance & simulation formulas
│   └── formatters.ts            # Indian Rupee (₹ en-IN) & date formatters
├── components/
│   ├── ui/                      # Reusable UI primitives
│   │   ├── Card.tsx             # Glassmorphic Bento containers
│   │   ├── Button.tsx           # Multi-variant button tokens
│   │   ├── Progress.tsx         # Animated linear gradients
│   │   ├── Badge.tsx            # Status pills (Risk, categories)
│   │   ├── Modal.tsx            # Framer Motion backdrop dialogs
│   │   └── Toast.tsx            # Floating toast notification system
│   ├── Dashboard/
│   │   ├── HealthScoreCard.tsx  # SVG circular progress gauge
│   │   ├── BudgetOverviewCard.tsx # Full-width linear budget progress
│   │   ├── QuickStatsGrid.tsx   # 4-column Bento grid stats
│   │   ├── RecentTransactions.tsx # Recent 5 transactions list
│   │   └── SpendingPieChart.tsx # Recharts donut spending breakdown
│   ├── Simulation/
│   │   ├── SimulationForm.tsx   # Inputs & Gen Z presets
│   │   ├── ImpactForecastCard.tsx # Before vs After delta card
│   │   ├── ImpactVisualizer.tsx # Budget shrinkage visualizer
│   │   └── DecisionActions.tsx  # Commit or discard decisions
│   ├── Transactions/
│   │   ├── ExpenseList.tsx      # Filterable & searchable transaction log
│   │   └── AddExpenseModal.tsx  # Modal with real-time math projection
│   ├── Goals/
│   │   ├── SavingsGoals.tsx     # Milestones with deposit increments
│   │   ├── SubscriptionsManager.tsx # Recurring bills with toggle
│   │   ├── AddGoalModal.tsx     # Goal creator
│   │   └── AddSubscriptionModal.tsx # Subscription creator
│   └── Layout/
│       ├── Header.tsx           # Top navigation with streak pill & reset
│       └── MobileBottomNav.tsx  # Mobile navigation dock
├── pages/
│   ├── Dashboard.tsx            # Home Bento view
│   ├── Simulation.tsx           # What-If simulator page
│   ├── TransactionsPage.tsx     # Expenses ledger
│   └── GoalsPage.tsx            # Goals & Subscriptions page
├── App.tsx                      # App shell with animated transitions
└── index.css                    # Tailwind directives & glassmorphic utility classes
```

---

## 🧮 Mathematical Simulation Model

1. **Daily Safe Allowance**:
   $$\text{Daily Allowance} = \max\left(0, \frac{\text{Remaining Balance}}{\text{Days Left}}\right)$$

2. **Simulation Impact Delta**:
   $$\text{Simulated Balance} = \text{Remaining Balance} - \text{Spend}$$
   $$\text{Simulated Allowance} = \max\left(0, \frac{\text{Simulated Balance}}{\text{Days Left}}\right)$$
   $$\Delta \text{Allowance} = \text{Simulated Allowance} - \text{Current Allowance}$$

3. **Spending Velocity**:
   $$\text{Velocity} = \frac{\text{Actual Daily Burn}}{\text{Ideal Daily Burn}} = \frac{(\text{Total Budget} - \text{Remaining}) / \text{Days Elapsed}}{\text{Total Budget} / 30}$$

4. **Financial Health Index (0–100)**:
   - Evaluates balance pace ratio against expected calendar consumption.
   - Adjusts for velocity acceleration factors.
   - Factors in recurring commitment coverage and emergency buffers.

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or newer)
- npm or pnpm

### Installation & Run

```bash
# Clone the repository
git clone https://github.com/GNBharath2606/survive-the-month.git
cd survive-the-month

# Install dependencies
npm install

# Start development server
npm run dev
```

Visit **`http://localhost:5173/`** in your browser.

### Production Build

```bash
npm run build
```

---

## 🎨 Design System
- **Theme**: Dark mode by default (`bg-slate-950`).
- **Glassmorphism**: `backdrop-blur-xl`, `bg-slate-900/60`, borders `border-white/10`.
- **Palette**: Indigo (`#6366f1`) for Primary, Emerald (`#10b981`) for Safe/Growth, Amber (`#f59e0b`) for Caution, Rose (`#f43f5e`) for Budget Breakers.
- **Typography**: Plus Jakarta Sans & JetBrains Mono.

---

## 👤 Author
Developed with ❤️ by **[GNBharath2606](https://github.com/GNBharath2606)**.
