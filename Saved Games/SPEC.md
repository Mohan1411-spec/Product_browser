# Product Browser - Specification

## Project Overview
- **Project Name**: Product Browser
- **Type**: Single-page web application (React + Tailwind CSS)
- **Core Functionality**: Browse and search products from Fake Store API with filtering, loading states, and responsive design
- **Target Users**: General users browsing e-commerce products

## Technical Stack
- React 18 (via CDN for simplicity)
- Tailwind CSS (via CDN)
- Fake Store API: `https://fakestoreapi.com/products`

## Visual & Rendering Specification

### Layout Structure
```
┌─────────────────────────────────────────────┐
│  Header: Logo + Search Bar                  │
├─────────────────────────────────────────────┤
│  Category Filter Tabs                       │
├─────────────────────────────────────────────┤
│  Product Grid (responsive: 1/2/3/4 cols)    │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐           │
│  │     │ │     │ │     │ │     │           │
│  └─────┘ └─────┘ └─────┘ └─────┘           │
│  ┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐           │
│  │     │ │     │ │     │ │     │           │
│  └─────┘ └─────┘ └─────┘ └─────┘           │
└─────────────────────────────────────────────┘
```

### Responsive Breakpoints
- **Mobile** (<640px): 1 column grid
- **Tablet** (640-1024px): 2 columns
- **Desktop** (>1024px): 4 columns

### Color Palette
- Background: `#0f172a` (slate-900)
- Card Background: `#1e293b` (slate-800)
- Primary Accent: `#f97316` (orange-500)
- Text Primary: `#f8fafc` (slate-50)
- Text Secondary: `#94a3b8` (slate-400)
- Rating Star: `#fbbf24` (amber-400)
- Error: `#ef4444` (red-500)

### Typography
- Font: "DM Sans" (Google Fonts) with system fallback
- Header: 2rem bold
- Card Title: 1rem semibold
- Price: 1.25rem bold orange
- Description: 0.875rem secondary

### Component Design
- **ProductCard**: Rounded corners (0.75rem), subtle shadow, hover scale effect
- **SearchBar**: Large input with search icon, rounded pill shape
- **CategoryTabs**: Horizontal scrollable tabs with active state indicator
- **LoadingState**: Skeleton cards with pulse animation
- **ErrorState**: Centered error message with retry button

## Functionality Specification

### Core Features
1. **Fetch Products**: Load all 20 products from Fake Store API on mount
2. **Search Filter**: Real-time search filtering by product title (case-insensitive)
3. **Category Filter**: Filter by category (All, Electronics, Jewelery, Men's Clothing, Women's Clothing)
4. **Combined Filtering**: Search and category filters work together

### User Interactions
- Type in search bar → instant filter update
- Click category tab → filter by category
- Hover product card → subtle scale and shadow increase
- Click "Retry" on error → re-fetch products

### Data Handling
- Store products in React state
- Store search query in state
- Store selected category in state
- Filter products reactively (no debounce needed for 20 items)

### API Response Structure
```json
{
  "id": 1,
  "title": "Fjallraven - Foldsack No. 1 Backpack",
  "price": 109.95,
  "description": "Your perfect pack for...",
  "category": "men's clothing",
  "image": "https://fakestoreapi.com/img/...",
  "rating": { "rate": 3.9, "count": 120 }
}
```

## Component Architecture
```
App
├── Header
│   └── SearchBar
├── CategoryFilter
├── ProductGrid
│   └── ProductCard (×N)
├── LoadingState
└── ErrorState
```

## Acceptance Criteria
1. ✓ Page loads with skeleton loading state
2. ✓ Products display in responsive grid with image, title, price, rating
3. ✓ Search filters products by title in real-time
4. ✓ Category tabs filter by product category
5. ✓ Combined search + category filtering works
6. ✓ Error state shows with retry button on API failure
7. ✓ Fully responsive across mobile/tablet/desktop
8. ✓ Smooth hover animations on cards
9. ✓ No console errors
