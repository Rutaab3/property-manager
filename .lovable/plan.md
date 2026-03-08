

# Rental Property Manager SPA — Implementation Plan

A full-featured rental property management dashboard built entirely with React, Tailwind CSS, and localStorage. No backend, no auth, no external APIs.

---

## Step 1: Global State & Toast System
- Create `AppContext` with all 5 localStorage collections (properties, tenants, payments, maintenance, expenses)
- Initialize from localStorage on mount, seed demo data on first load (3 properties, 3 tenants, 6 payments, 3 maintenance requests, 4 expenses)
- Implement all CRUD action functions that read→mutate→write localStorage and fire toast notifications
- Wire up toast notifications using sonner (already installed) for success/error/warning/info messages

## Step 2: Reusable UI Components
- **SlideOverPanel**: Right-sliding 480px panel with overlay, escape-to-close, cancel/save footer
- **ConfirmDialog**: Centered modal with warning icon, message, cancel/confirm buttons
- **StatusBadge**: Colored pill component mapping statuses to green/yellow/red/blue/gray
- **EmptyState**: Centered placeholder with icon, title, description, and CTA button

## Step 3: Layout Shell & Routing
- Dark sidebar (240px, #1E293B) with nav links and icons for all 7 routes
- Active link highlighting with left border accent
- Settings gear icon → modal with Export JSON, Import JSON, Clear All Data
- Responsive: hamburger menu on mobile, sidebar as overlay
- Top header bar with page title and breadcrumbs
- React Router v6 with all routes: `/`, `/properties`, `/properties/:id`, `/tenants`, `/payments`, `/maintenance`, `/reports`

## Step 4: Dashboard Page
- **4 KPI cards**: Total Properties, Monthly Rent Due, Outstanding Payments, Open Maintenance
- **Rent Collection table**: Current month's rent payments with "Mark Paid" inline action
- **Alerts panel**: Auto-generated alerts for expiring leases, overdue rent, emergency maintenance, vacant properties
- **Mini rent calendar**: Monthly grid with colored dots (green=paid, yellow=pending, red=overdue) and click-to-view popovers

## Step 5: Properties Page & Detail Page
- Grid/list view toggle with search and status filter tabs (All/Occupied/Vacant/Archived)
- Property cards showing photo, address, beds/baths/sqft, status, active tenant info, monthly rent
- Add/Edit property via SlideOverPanel with full form validation
- Archive with confirmation (blocked if active tenant exists)
- **Detail page** with 5 tabs: Overview, Tenant History, Payments, Maintenance, Expenses — each showing filtered data for that property

## Step 6: Tenants Page
- Tabbed view: Active / Past / Archived with count badges
- Tenant cards with lease progress bar, expiry countdown (color-coded), contact info, rent/deposit
- Add tenant (only vacant properties in dropdown), Edit tenant, Archive tenancy with deposit-returned checkbox
- Adding tenant auto-sets property status to "occupied"; archiving sets it to "vacant"

## Step 7: Payments Page
- Month navigator (prev/next) with status filter tabs and property dropdown filter
- Monthly summary bar: Expected, Collected, Outstanding, Collection Rate
- Payment table with Mark Paid, Edit, Delete actions
- Auto-generate rent button creates pending entries for all active tenants
- Auto-update overdue status on mount
- Add/Edit payment modal with cascading property→tenant dropdowns and auto-status logic

## Step 8: Maintenance Page
- **Kanban view** with 3 columns (Open, In Progress, Resolved) — HTML5 drag-and-drop to change status
- **List view** as alternative table layout
- Priority and property filters
- Cards show priority badge, days open, cost, contractor info
- Add/Edit via SlideOverPanel, delete with confirmation

## Step 9: Reports Page
- **Monthly P&L**: Income vs expenses breakdown with summary cards (Gross Income, Expenses, NOI, Margin), income/expense tables, and 6-month grouped bar chart
- **Annual Overview**: 12-month line chart (income vs expenses), annual summary cards, best performing property
- **Property Comparison**: Table comparing all properties by annual income, expenses, NOI, occupancy rate; horizontal bar chart of NOI per property
- Export JSON backup and Print Report buttons on every report
- Charts built with recharts (already installed)

## Design System
- Plus Jakarta Sans font (400/500/600/700)
- Primary blue (#2563EB), dark sidebar (#1E293B), light background (#F8FAFC)
- Cards: white, rounded-xl, subtle shadow and border
- Consistent color coding: green=success, yellow=warning, red=danger, blue=info
- All currency formatted as USD, all dates displayed as "Jan 15, 2025"

