# Steam Market Analytics — Project Context

## Overview

A React-based web application for importing, viewing, and analyzing Steam Market transaction history from CSV files. Users can filter, multi-select, and get real-time summary calculations of their trading activity.

## Core Features

- **CSV Import** — Upload Steam Market history with validation and preview confirmation
- **Transaction Table** — Multi-select with shift-click range selection
- **Advanced Filtering** — Search by item name, game, type, date range, and price range
- **Summary Analytics** — Real-time gains, spending, and net profit calculations
- **Local Persistence** — Data stored in browser localStorage
- **Responsive Design** — Optimized for desktop and mobile

## Data Model

| Field         | Type                  | Description                  |
|---------------|-----------------------|------------------------------|
| `id`          | `string` (UUID)       | Unique identifier            |
| `item`        | `string`              | Item name                    |
| `game`        | `string`              | Game name                    |
| `date`        | `string` (ISO)        | Transaction date             |
| `price_cents` | `number`              | Price in cents               |
| `type`        | `sale` \| `purchase`  | Transaction type             |
| `created_at`  | `string` (ISO)        | Creation timestamp           |
| `updated_at`  | `string` (ISO)        | Last update timestamp        |

## Tech Stack

| Layer        | Technology                              |
|--------------|-----------------------------------------|
| Framework    | React 18 + TypeScript                   |
| Build        | Vite                                    |
| Styling      | Tailwind CSS + custom design tokens     |
| UI Library   | shadcn/ui (Radix UI primitives)         |
| CSV Parsing  | PapaParse                               |
| Dates        | date-fns                                |
| Routing      | React Router DOM                        |
| Charts       | Recharts (available)                    |

## Project Structure

```
src/
├── components/
│   ├── csv-import/        # CSV upload, validation, confirmation dialog
│   ├── transactions/      # Table, filters, summary cards, empty state
│   │   └── table/         # Row, header, table components
│   ├── layout/            # Header, footer, loading skeleton
│   └── ui/                # shadcn/ui component library
├── hooks/
│   └── transactions/      # CRUD, filtering, selection, totals
├── lib/
│   ├── csv/               # Parsing and validation logic
│   ├── date.ts            # Date parsing (PT/EN formats)
│   ├── format.ts          # Price formatting (EUR)
│   ├── storage.ts         # localStorage wrapper
│   └── constants.ts       # App configuration
├── types/                 # TypeScript interfaces
└── pages/                 # Route components
```

## Key Hooks

| Hook                     | Purpose                                      |
|--------------------------|----------------------------------------------|
| `useTransactions`        | CRUD operations with localStorage sync       |
| `useTableSelection`     | Multi-select with shift-click range support  |
| `useTransactionFilters` | Filter state management and application      |
| `useTransactionTotals`  | Gains / spent / net calculation for selection |

## Data Flow

1. **Import** — CSV uploaded → parsed (PapaParse) → validated → confirmed → stored
2. **Display** — Transactions loaded from localStorage on mount
3. **Filter** — Client-side filtering with debounced search
4. **Select** — Multi-select triggers real-time summary recalculation
5. **Persist** — All changes written to localStorage

## Business Logic

- **Prices** stored as cents to avoid floating-point issues; displayed as EUR
- **Dates** parsed from multiple formats with year inference; displayed as `dd/MM/yy`
- **Filtering** is real-time, multi-criteria, and debounced
- **Selection** supports individual click, shift-click ranges, and select all

## Deployment

- **Platform**: Netlify
- **SPA Routing**: `public/_redirects` with `/* /index.html 200`
- **Build Output**: `dist/`

## Author

**Taleex** — [taleex.netlify.app](https://taleex.netlify.app/)
