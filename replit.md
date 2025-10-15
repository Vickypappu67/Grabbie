# Grabbie Restaurant Partner System

## Overview

Grabbie is a restaurant order management system designed for train food delivery services. The application provides a real-time dashboard for restaurant staff to receive, track, and manage food orders from train passengers. Built with a modern tech stack, it features live order notifications via WebSocket, comprehensive order status tracking, and a professional dark-themed UI optimized for high-information density environments.

The system handles the complete order lifecycle from initial placement through delivery, with specialized features for train-specific delivery details (PNR, coach, seat numbers, station information).

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Build System**
- React 18 with TypeScript for type-safe component development
- Vite as the build tool and development server with HMR support
- Wouter for lightweight client-side routing

**UI Component System**
- shadcn/ui component library (New York variant) with Radix UI primitives
- Tailwind CSS for utility-first styling with custom design tokens
- Dark mode by default with custom color palette focused on order status visualization
- Framer Motion for animations and micro-interactions

**State Management & Data Fetching**
- TanStack Query (React Query) for server state management and caching
- Real-time updates via WebSocket connection for live order notifications
- Session-based authentication with express-session

**Design System**
- Custom color palette with distinct status colors for order workflow (New, Accepted, Preparing, Ready, Delivered, Cancelled)
- Typography: Inter for UI/body text, Sora for headers and emphasis
- Follows Material Design principles combined with Linear's clean typography and Toast POS patterns
- High-information density layout optimized for professional restaurant environments

### Backend Architecture

**Server Framework**
- Express.js server with TypeScript
- WebSocket server (ws library) for real-time bidirectional communication
- Session-based authentication with cookie storage

**Data Layer**
- Database ORM: Drizzle ORM configured for PostgreSQL
- Database provider: Neon serverless PostgreSQL (based on @neondatabase/serverless dependency)
- In-memory storage implementation (MemStorage class) used for development/demo purposes
- Schema includes: users, restaurants, orders, and order status history tables

**API Design**
- RESTful endpoints for CRUD operations on orders
- WebSocket endpoint (`/ws`) for real-time order notifications
- Authentication middleware protecting dashboard routes
- Session management with configurable secrets

**Order Status Workflow**
The system implements a defined order lifecycle:
1. **new** - Initial order received
2. **accepted** - Restaurant acknowledges order
3. **preparing** - Food preparation in progress
4. **ready** - Order ready for pickup
5. **assigned** - Delivery partner assigned (external system integration)
6. **delivered** - Order completed
7. **cancelled** - Order rejected/cancelled

### Data Schema

**Core Tables**
- `users`: Restaurant staff authentication (username, password, role, restaurantId)
- `restaurants`: Restaurant information (name, description, isActive)
- `orders`: Complete order details with JSONB fields for items and train details
- `order_status_history`: Audit trail for status changes with timestamps and notes

**Key Fields**
- Order items stored as JSONB array with name, quantity, price
- Train details stored as JSONB with trainNumber, trainName, pnr, coach, seat, station
- Decimal precision for monetary amounts (10,2)
- UUID primary keys with PostgreSQL gen_random_uuid()

## External Dependencies

### Database & Storage
- **Neon Serverless PostgreSQL**: Primary database (CONNECTION_URL via environment variable)
- **Drizzle ORM**: Type-safe database queries and migrations
- **connect-pg-simple**: PostgreSQL session store (configured but not actively used in demo mode)

### UI Component Libraries
- **Radix UI**: Headless accessible UI primitives (@radix-ui/react-* packages)
- **shadcn/ui**: Pre-built components following New York variant styling
- **cmdk**: Command palette component
- **Framer Motion**: Animation library for smooth transitions and micro-interactions
- **embla-carousel-react**: Carousel/slider functionality

### Form & Validation
- **React Hook Form**: Form state management with @hookform/resolvers
- **Zod**: Schema validation with drizzle-zod integration
- **date-fns**: Date formatting and manipulation

### Real-time Communication
- **WebSocket (ws)**: Native WebSocket server for order notifications
- Custom useWebSocket hook manages connection state and auto-reconnection
- Broadcasts new orders to all connected clients

### Development Tools
- **TypeScript**: Full type safety across frontend and backend
- **Vite plugins**: Runtime error overlay, cartographer, dev banner (Replit-specific)
- **PostCSS & Autoprefixer**: CSS processing

### Authentication & Security
- **express-session**: Session-based authentication
- Cookie-based session storage with configurable secrets
- Password stored in plain text (demo implementation - needs bcrypt/argon2 for production)

### Environment Configuration
Required environment variables:
- `DATABASE_URL`: PostgreSQL connection string
- `SESSION_SECRET`: Session encryption key
- `NODE_ENV`: Environment mode (development/production)

### Font Dependencies
- Google Fonts: Inter (weights 300-900) and Sora (weights 400-800)
- Loaded via CDN in HTML head for optimal performance