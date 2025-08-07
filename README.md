# Pack Dashboard

A modern SvelteKit dashboard application built with TypeScript, featuring data visualization, responsive design, and Docker deployment.

## 🚀 Quick Start with Docker

### Build the Docker image:

```bash
docker build -t pack-dashboard .
```

### Run the application:

```bash
docker run -p 3000:3000 pack-dashboard
```

## Run with pnpm

```bash
pnpm dev
```

The application will be available at `http://localhost:3000`

## 🛠️ Technology Stack

### Frontend Framework

- **[SvelteKit 2.22.0]**
- **[Svelte 5]**
- **[TypeScript 5]**

### UI & Styling

- **[Tailwind CSS 4]**
- **[shadcn/ui (Svelte)]** - Beautiful, accessible component library
- **[Iconify]** - Comprehensive icon library with SVG icons

### Data Visualization

- **[Chart.js 4.5.0]** - Responsive canvas-based charts
  - Doughnut charts for percentage displays
  - Line charts for time-series data
  - Pie charts for category breakdowns
- **[chartjs-adapter-date-fns]** - Date handling for time-based charts

### Development Tools

- **[Vite 7]** - Fast build tool and development server
- **[ESLint 9]** - Code linting with TypeScript support
- **[Prettier]** - Code formatting with Svelte and Tailwind plugins
- **[Docker]** - Containerized deployment

### State Management & Utilities

- **[svelte-sonner]** - Toast notifications
- **[date-fns]** - Modern JavaScript date utility library

## 📊 Features

### Dashboard Overview

- Interactive data visualizations with Chart.js
- Responsive flex grid layout with card-based components
- Statistics display with trending indicators

### Data Tables

### Navigation & UX

- Responsive navigation with mobile menu
- Toast notifications for user feedback

### Upload & Management

- Modal-based file upload system
- Multi-category resource organization

## 🔧 Development

### Prerequisites

- Node.js 22+ (or use Docker)
- pnpm (preferred package manager)

### Local Development

```bash
# Install dependencies
pnpm install

# Start development server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

### Code Quality

```bash
# Format code
pnpm format

# Lint code
pnpm lint

# Type checking
pnpm check
```

## 📁 Project Structure

```
src/
├── lib/
│   ├── components/          # Reusable UI components
│   │   ├── ui/             # shadcn/ui components
│   │   └── card-section/   # Dashboard-specific components
│   ├── data/               # Mock data files
│   └── assets/styles/      # Custom CSS and theme
├── routes/                 # SvelteKit file-based routing
└── app.html               # HTML template
```

## What would I improve

**Toast Notifications (svelte-sonner)**

- Originally positioned on tabs
- Currently positioned above tabs

**Data Tables**

- Basic sorting implemented with visual indicators
- **Missing**: Pagination for large datasets
- **Improvement**: Add pagination with "Previous/Next" controls and result counters
- **Rationale**: Essential for performance and usability with real-world data volumes
