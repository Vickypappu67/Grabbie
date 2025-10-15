# Design Guidelines: Grabbie Restaurant Order Management System

## Design Approach: Utility-First Dashboard Design
**Selected Approach**: Hybrid of Material Design principles + Linear's clean typography + Toast POS system patterns
**Justification**: Restaurant management requires high-information density, real-time updates, and quick decision-making in a professional environment. The design prioritizes efficiency, clarity, and rapid order processing.

---

## Core Design Elements

### A. Color Palette

**Primary Brand Colors:**
- Primary Orange: `25 100% 60%` - Used for CTAs, active states, new order alerts
- Deep Black: `0 0% 10%` - Primary background and text
- Pure White: `0 0% 100%` - Text on dark backgrounds, cards

**Status Colors (Critical for Order Workflow):**
- New Order: `220 90% 56%` (Blue) - Incoming orders requiring attention
- Accepted: `45 100% 51%` (Amber) - Orders acknowledged
- Preparing: `280 67% 60%` (Purple) - Active cooking
- Ready: `142 76% 36%` (Green) - Ready for pickup
- Delivered: `142 71% 45%` (Success Green) - Completed
- Cancelled: `0 84% 60%` (Red) - Rejected/cancelled

**UI Backgrounds:**
- Primary BG: `0 0% 7%` - Main dashboard background
- Card BG: `0 0% 13%` - Order cards, panels
- Hover BG: `0 0% 18%` - Interactive elements
- Border: `0 0% 25%` - Subtle dividers

### B. Typography

**Font Families:**
- Primary: 'Inter' (Google Fonts) - UI, body text, data
- Accent: 'Sora' (Google Fonts) - Headers, order IDs, emphasis

**Type Scale:**
- Order ID/Headers: text-2xl/3xl font-bold (Sora)
- Status Labels: text-sm font-semibold uppercase tracking-wide
- Body/Details: text-sm/base (Inter)
- Timestamps: text-xs text-gray-400
- Data/Numbers: text-lg/xl font-semibold tabular-nums

### C. Layout System

**Spacing Primitives:** Use Tailwind units: 2, 3, 4, 6, 8, 12, 16, 20
- Card padding: p-6
- Section spacing: space-y-6
- Grid gaps: gap-6
- Button padding: px-6 py-3

**Grid Structure:**
- Sidebar: w-64 (fixed navigation)
- Main content: flex-1 with max-w-7xl
- Order cards: grid-cols-1 lg:grid-cols-2 xl:grid-cols-3
- Dashboard stats: grid-cols-2 md:grid-cols-4

### D. Component Library

**Navigation & Layout:**
- Fixed left sidebar with restaurant logo, main navigation (Orders, Menu, Analytics, Settings)
- Top header bar with user profile, notifications badge, real-time clock
- Breadcrumb navigation for context

**Order Cards (Primary Component):**
- Elevated dark cards (bg-gray-900) with colored left border indicating status
- Header: Order ID (large, Sora font) + timestamp
- Body: Customer name, train details (PNR, seat), items list with quantities
- Footer: Total amount (prominent) + action buttons
- Pulsing glow animation for new orders
- Slide-in animation when new order arrives

**Status Workflow Indicators:**
- Horizontal stepper showing: New → Accept → Preparing → Ready → Assigned → Delivered
- Active step highlighted with brand orange
- Completed steps with success green checkmark
- Progress bar beneath stepper
- Auto-advance animations between steps

**Action Buttons:**
- Accept Order: Solid orange (bg-orange-600 hover:bg-orange-700)
- Reject Order: Outline red (border-red-600 text-red-600)
- Mark Preparing: Solid purple
- Mark Ready: Solid green
- All buttons: rounded-lg px-6 py-3 font-semibold transition-all

**Notification System:**
- Toast notifications (top-right): slide-in from right
- Sound alert icon with toggle (on/off)
- Badge count on navigation items
- Browser notification permission prompt on login

**Data Display:**
- Dashboard stat cards: Large number (text-3xl) + label + trend indicator
- Order items list: Item name + emoji + quantity badge + price
- Timeline view for order history with connecting lines

**Real-time Elements:**
- WebSocket connection indicator (green dot + "Live" text)
- "New Order" badge with ping animation
- Auto-refresh timestamp (e.g., "Updated 2s ago")
- Loading skeleton for order cards

### E. Animations & Interactions

**Order Arrival (High Priority):**
- Card slides in from right with scale animation (0.95 → 1)
- Orange glow pulse effect (3 pulses)
- Subtle shake animation to draw attention
- Sound notification (optional toggle)

**Status Transitions:**
- Status badge fade-out/fade-in with color change
- Progress bar smooth fill animation
- Confetti burst when order marked "Delivered"
- Haptic feedback simulation (scale pulse on button click)

**Micro-interactions:**
- Button hover: scale(1.02) + brightness increase
- Card hover: translateY(-2px) + shadow increase
- Toggle switches: smooth slide animation
- Number counter animations for dashboard stats

---

## Page-Specific Layouts

### Login Page
- Split screen: Left (2/5) = brand messaging with Grabbie logo, tagline; Right (3/5) = login form
- Dark gradient background (black to dark gray)
- Glowing orange accent lines
- Simple email/password inputs with floating labels
- "Remember me" toggle + "Forgot password" link
- Prominent orange login button

### Dashboard (Main Orders View)
- Top: 4-column stat cards (Today's Orders, Revenue, Pending, Active)
- Filter tabs: All | Incoming | Preparing | Ready | Completed
- Order grid with real-time updates
- Empty state: Illustration + "No orders yet" message

### Order Detail Modal
- Full-screen overlay with backdrop blur
- Center modal (max-w-3xl) with order details
- Left column: Customer info, delivery details, timeline
- Right column: Items breakdown, total, payment status
- Bottom action bar with status update buttons

---

## Images & Assets

**Icons:** Font Awesome (CDN) for consistent iconography
- Order status icons (circle-check, clock, truck, etc.)
- Navigation icons (home, list, chart, cog)
- UI actions (filter, search, bell, user)

**No hero images needed** - This is a dashboard application focused on data and functionality

**Brand Assets:**
- Grabbie restaurant logo (orange/white) in sidebar header
- Empty state illustrations (minimal, orange accent)
- Loading spinner with orange gradient

---

## Accessibility & Responsiveness

- WCAG AA contrast compliance (test all status colors on dark bg)
- Keyboard navigation for all order actions (Tab, Enter, Escape)
- Screen reader labels for status changes
- Responsive breakpoints: Mobile (single column), Tablet (2 cols), Desktop (3 cols)
- Touch-friendly button sizes (min 44px) for tablet use
- Dark mode only (optimized for restaurant low-light environments)