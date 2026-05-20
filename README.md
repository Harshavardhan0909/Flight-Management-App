# ✈️ FlightDeck Manager

A modern and responsive flight management platform built with **Next.js App Router**, **Supabase**, **Zustand**, **Tailwind CSS**, and **next-pwa**.
The application provides a complete flight booking experience with realtime seat selection, secure booking workflows, booking management, and Progressive Web App (PWA) support.

---

## 🚀 Features

### 🔍 Flight Search & Comparison

* Search flights by:

  * Route
  * Departure date
  * Passenger count
* Compare flights based on:

  * Price
  * Duration
  * Aircraft type
  * Travel class

### 💺 Realtime Seat Selection

* Interactive seat map with:

  * First Class
  * Business Class
  * Economy Class
* Live seat availability updates
* Optimistic UI seat locking

### 📦 Secure Booking Flow

* Supabase RPC-powered transactional booking system
* Atomic seat reservation using database row locking (`FOR UPDATE`)
* Passenger management during booking flow
* Protected against double booking issues

### 📋 Booking Management

* View all bookings in **My Bookings**
* Reschedule bookings
* Cancel bookings
* Booking status badges
* Confirmation dialogs for critical actions

### 🔒 Advanced Security & Validation

* Database-level cancellation protection
* Prevents cancellation within 2 hours of departure
* Row-Level Security (RLS) enabled on all tables
* Auth-scoped access for user bookings and passenger data

### ⚡ State Management

* Zustand-powered global stores
* Persisted booking progress
* Sensitive passport numbers excluded from local storage persistence

### 📱 Progressive Web App (PWA)

* Installable application
* Offline support
* Runtime caching
* Optimized Lighthouse PWA performance

---

# 🛠️ Tech Stack

## Frontend

* Next.js App Router
* React
* Tailwind CSS
* Zustand

## Backend & Database

* Supabase
* PostgreSQL
* Supabase RPC Functions
* Row Level Security (RLS)

## PWA & Deployment

* next-pwa
* Vercel

---

# 📂 Project Structure

```bash
app/
components/
store/
supabase/
public/
```

---

# ⚙️ Local Setup

## 1️⃣ Install Dependencies

```bash
npm install
```

---

## 2️⃣ Configure Environment Variables

Create a `.env.local` file:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

---

## 3️⃣ Run Database Migrations

Apply the SQL migrations inside:

```bash
supabase/migrations/
```

Main schema file:

```bash
202605190001_flightdeck_schema.sql
```

---

## 4️⃣ Seed Demo Data

```bash
npm run seed
```

### Demo Credentials

```txt
Email: demo@flightdeck.test
Password: FlightDeck123!
```

---

## 5️⃣ Start Development Server

```bash
npm run dev
```

---

# 🗄️ Database & Security

## 🔐 Row-Level Security (RLS)

RLS is enabled across all tables:

* Flights
* Seats
* Bookings
* Passengers
* Reschedules

Users can only access their own booking-related data using `auth.uid()`.

---

## 💺 Seat Reservation Flow

The `reserve_seat_and_create_booking` RPC function:

* Locks selected seat rows using `FOR UPDATE`
* Validates seat availability
* Creates booking and passenger records
* Updates seat availability atomically

This prevents:

* Race conditions
* Duplicate reservations
* Inconsistent bookings

---

## ❌ Cancellation Rules

The `bookings_reject_late_cancellation` trigger prevents booking cancellations within:

```txt
2 hours of departure
```

Validation occurs directly at the database layer for stronger security.

---

# 🧠 Zustand Store Architecture

## `useFlightStore.ts`

Manages:

* Search queries
* Selected flight
* Selected seat
* Passenger draft data
* Booking progress
* Optimistic seat selection

Sensitive fields like passport numbers are excluded from persistence.

---

## `useUserStore.ts`

Manages:

* Supabase session
* Cached user bookings
* Lightweight persisted authentication state

---

# 📱 PWA Configuration

Configured using `next-pwa`.

### Caching Strategies

* `StaleWhileRevalidate`

  * Flight search results
  * Booking pages

* `CacheFirst`

  * Static Next.js assets

### Offline Support

* `/offline` fallback page

### Manifest

Located in:

```bash
public/manifest.json
```

Includes:

* 192x192 icon
* 512x512 icon

---

# 🚀 Deployment

Deploy easily using:

* Vercel
* Supabase

Configure the same environment variables in your deployment platform.

---

# 📸 Screenshots

<img width="1810" height="892" alt="image" src="https://github.com/user-attachments/assets/49455f2c-fc86-4256-8a6d-f83248fb4f14" />


Examples:

* Flight Search
* Seat Selection
* Booking Confirmation
* My Bookings Dashboard
* Mobile Responsive UI

---

# 🌟 Future Improvements

* Multi-city bookings
* Real-time flight status tracking
* Payment gateway integration
* Admin dashboard
* AI-powered fare prediction
* Email & SMS notifications

---

# 👨‍💻 Author

**Harshavardhan Korlepara**

* GitHub: https://github.com/Harshavardhan0909
* LinkedIn: https://linkedin.com/in/k-harshavardhan

---

# 📄 License

This project is licensed under the MIT License.
