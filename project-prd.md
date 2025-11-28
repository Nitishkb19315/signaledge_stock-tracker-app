## 📋 Executive Summary

**SignalEdge** is a modern, AI-powered stock market application that enables users to track real-time stock prices, set personalized alerts, explore detailed company insights, and manage customizable watchlists. Built with Next.js, the platform leverages event-driven workflows (Inngest) for automated alerts, AI-generated daily digests, and personalized notifications, empowering retail investors with data-driven decision-making tools.

### 📊 Implementation Status Overview

**✅ Fully Implemented (80%):**
- Stock dashboard with TradingView widgets (Market Overview, Heatmap, Top Stories, Market Data)
- Stock search with command palette (Cmd+K) and real-time Finnhub integration
- Stock detail pages with comprehensive TradingView widgets (6 widget types)
- User authentication (Better Auth with MongoDB)
- Welcome email workflow (Inngest + Gemini AI)
- Daily news summary workflow (Inngest + Gemini AI)
- All email templates (Welcome, News Summary, Price Alerts, Volume Alerts, Inactive User)
- Watchlist database model and button component

**⚠️ Partially Implemented (15%):**
- Watchlist management (backend ready, dedicated UI page pending)
- Alert system (TypeScript types and email templates ready, core functionality pending)

**❌ Not Implemented (5%):**
- Alert creation UI and database model
- Alert monitoring/checking Inngest workflow
- Inactive user reminder Inngest workflow (template ready)

**Last Updated:** Based on codebase analysis as of current date

---

## 🎯 Product Overview

### Vision
To democratize stock market investing by providing retail investors with institutional-grade tools, real-time market insights, and AI-powered personalized alerts in an intuitive, accessible interface.

### Mission
Create a seamless platform that combines real-time market data, intelligent notifications, and AI-driven insights to help investors make informed, timely trading decisions.

### Core Value Proposition
- **Real-Time Tracking**: Monitor stock prices with interactive charts and historical data
- **Intelligent Alerts**: Custom price and volume alerts with instant email notifications
- **AI Insights**: Personalized market summaries and earnings notifications
- **Simplified Discovery**: Powerful search and filtering capabilities
- **User-Centric Design**: Dark mode UI optimized for market professionals

---

## 🔋 Key Features

### 1. **Stock Dashboard**
- **Market Overview Widget**: Interactive market overview with tabs for Financial, Technology, and Services sectors
- **Stock Heatmap Widget**: Visual heatmap showing S&P 500 stocks grouped by sector with market cap-based sizing
- **Top Stories Widget**: Market news timeline with real-time updates
- **Market Data Widget**: Real-time stock quotes grouped by industry sectors
- **TradingView integration** for professional-grade charting (all widgets configured in `constants.ts`)
- **Responsive grid layout** optimized for desktop and mobile (2-column on desktop, single column on mobile)
- **Dark theme** optimized for extended market viewing

**Implementation Status:** ✅ Fully Implemented

**Related Files:**
- `app/(root)/page.tsx` - Main dashboard page
- `components/TradingViewWidget.tsx` - Reusable widget wrapper component
- `lib/constants.ts` - Widget configurations (MARKET_OVERVIEW_WIDGET_CONFIG, HEATMAP_WIDGET_CONFIG, etc.)
- `hooks/useTradingViewWidget.tsx` - Custom hook for widget management

---

### 2. **Powerful Stock Search**
- **Intelligent search system** with real-time Finnhub API integration
- **Command palette interface** (Cmd/Ctrl + K) for quick access via keyboard shortcut
- **Debounced search** (300ms delay) for optimal performance
- **Popular stocks display**: Shows top 10 popular stocks when no search query
- **Search results**: Filters by symbol, company name, and exchange
- **Stock details**: Displays symbol, company name, exchange, and stock type
- **Direct navigation**: Clicking a stock navigates to detailed stock page
- **Loading states**: Visual feedback during API calls
- **Empty states**: Handles no results gracefully

**Implementation Status:** ✅ Fully Implemented

**Related Files:**
- `components/SearchCommand.tsx` - Main search component
- `components/ui/command.tsx` - Shadcn command palette component
- `lib/actions/finnhub.actions.ts` - `searchStocks()` function
- `hooks/useDebounce.ts` - Debounce hook for search optimization
- `lib/constants.ts` - POPULAR_STOCK_SYMBOLS array

---

### 3. **Watchlist Management**
- **WatchlistButton component**: Toggle button for adding/removing stocks from watchlist
- **Visual feedback**: Star icon (filled when in watchlist, outlined when not)
- **Two display modes**: Button mode (with text) and icon-only mode
- **MongoDB persistence**: Watchlist items stored with userId, symbol, company, and addedAt timestamp
- **Unique constraints**: Prevents duplicate symbols per user via database index
- **Watchlist schema**: Mongoose model with proper indexing for performance

**Implementation Status:** ⚠️ Partially Implemented
- ✅ WatchlistButton component exists
- ✅ Database model and schema implemented
- ✅ Server actions for watchlist operations (`watchlist.actions.ts`)
- ⚠️ Dedicated watchlist page/route not found in codebase
- ⚠️ Watchlist table view with sortable columns not implemented
- ⚠️ Real-time price updates for watchlist items not implemented

**Related Files:**
- `components/WatchlistButton.tsx` - Toggle button component
- `database/models/watchlist.model.ts` - Mongoose schema
- `lib/actions/watchlist.actions.ts` - Server actions (getWatchlistSymbolsByEmail, etc.)
- `app/globals.css` - Watchlist styling classes

---

### 4. **Advanced Alert System**
- **TypeScript definitions**: Alert types defined in `global.d.ts`
- **Email templates**: Complete templates for upper, lower, and volume alerts
- **Alert data structure**: Supports symbol, company, alert name, type (upper/lower), threshold, and current price

**Implementation Status:** ⚠️ Partially Implemented
- ✅ TypeScript type definitions exist (`Alert`, `AlertData`, `AlertModalProps`)
- ✅ Email templates fully implemented (STOCK_ALERT_UPPER_EMAIL_TEMPLATE, STOCK_ALERT_LOWER_EMAIL_TEMPLATE, VOLUME_ALERT_EMAIL_TEMPLATE)
- ❌ Alert creation UI/forms not found in codebase
- ❌ Alert database model/schema not found
- ❌ Alert management (CRUD operations) not implemented
- ❌ Alert monitoring/checking workflow not implemented
- ❌ Inngest function for alert checking not found

**Note:** Alert system appears to be in planning/design phase. Email templates are ready, but the core functionality (creation, storage, monitoring) needs to be implemented.

**Related Files:**
- `types/global.d.ts` - Alert type definitions
- `lib/nodemailer/templates.ts` - Email templates for alerts
- `lib/constants.ts` - ALERT_TYPE_OPTIONS, CONDITION_OPTIONS

---

### 5. **Company Insights (Stock Detail Page)**
- **Symbol Info Widget**: Current price, change percentage, and basic stock information
- **Advanced Chart Widget**: Candlestick chart with daily intervals, volume, and technical indicators
- **Baseline Chart Widget**: Baseline analysis chart for technical analysis
- **Technical Analysis Widget**: Automated technical analysis with buy/sell signals
- **Company Profile Widget**: Company overview, business description, and key metrics
- **Company Financials Widget**: Financial statements, revenue, earnings, and key ratios
- **Watchlist integration**: Add/remove stock from watchlist directly from detail page
- **Responsive layout**: 2-column grid on desktop, single column on mobile

**Implementation Status:** ✅ Fully Implemented

**Related Files:**
- `app/(root)/stocks/[symbol]/page.tsx` - Stock detail page
- `components/TradingViewWidget.tsx` - Widget wrapper component
- `components/WatchlistButton.tsx` - Watchlist toggle on detail page
- `lib/constants.ts` - Widget configurations (SYMBOL_INFO_WIDGET_CONFIG, CANDLE_CHART_WIDGET_CONFIG, etc.)

---

### 6. **Real-Time Email Notifications**
Automated, personalized email templates for different scenarios:

#### **Welcome Email** (On Sign-Up)
- Personalized greeting based on user profile
- Feature overview and quick start guide
- AI-generated intro using user's investment goals, risk tolerance, and preferred industries
- Call-to-action to explore dashboard

**Related Files:**
- templates.ts - `WELCOME_EMAIL_TEMPLATE`
- prompts.ts - `PERSONALIZED_WELCOME_EMAIL_PROMPT`

#### **Price Alert Emails** (Upper/Lower Targets)
- **Upper Alert**: "Price Above Target" notification in green (#10b981)
- **Lower Alert**: "Price Below Target" notification in red (#ef4444)
- Current price, target threshold, and percentage change
- Visual card layout with stock symbol and company name
- Call-to-action button linking to dashboard

**Related Files:**
- `STOCK_ALERT_UPPER_EMAIL_TEMPLATE`
- `STOCK_ALERT_LOWER_EMAIL_TEMPLATE`

#### **Volume Alert Emails**
- Volume spike detection notifications
- Current volume vs. average volume comparison
- Purple accent color (#7c3aed) for volume alerts
- Educational context about volume significance
- Links to dashboard for real-time monitoring

**Related Files:**
- `VOLUME_ALERT_EMAIL_TEMPLATE`

#### **Daily News Summary Email**
- Market overview and key movers
- Stock-specific news for tracked symbols
- AI-summarized content using Gemini API
- Section-based organization with icons
- Yellow bullet points for readability

**Related Files:**
- templates.ts - `NEWS_SUMMARY_EMAIL_TEMPLATE`
- prompts.ts - `NEWS_SUMMARY_EMAIL_PROMPT`

#### **Inactive User Reminder Email**
- Re-engagement campaign for dormant users
- Market activity summary
- Watchlist status reminder
- Incentive to return to dashboard

**Related Files:**
- `INACTIVE_USER_REMINDER_EMAIL_TEMPLATE`

---

### 7. **AI-Powered Workflows** (Inngest)

#### **Welcome Email Generation** (`sendSignUpEmail`)
- Triggered on user creation event
- Extracts user profile data (country, investment goals, risk tolerance, preferred industry)
- AI-generates personalized welcome content using Gemini API
- Sends custom welcome email with HTML template

**Related Files:**
- functions.ts - `sendSignUpEmail`

#### **Daily News Summary** (`sendDailyNewsSummary`)
- **Schedule**: Runs daily at 12:00 PM UTC (cron: `0 12 * * *`)
- **Step 1**: Fetches all active users eligible for news emails
- **Step 2**: For each user, retrieves watchlist symbols and fetches relevant news
- **Step 3**: Falls back to general market news if no watchlist-specific news found
- **Step 4**: AI-summarizes news using Gemini API (gemini-2.5-flash-lite model)
- **Step 5**: Sends personalized email with AI-generated content
- **Error handling**: Graceful fallbacks for missing data or API failures
- **Article limit**: Maximum 6 articles per user email
- **News source**: Company-specific news from Finnhub, with general market news fallback

**Implementation Status:** ✅ Fully Implemented

**Related Files:**
- `lib/inngest/functions.ts` - `sendDailyNewsSummary` function
- `lib/actions/user.actions.ts` - `getAllUsersForNewsEmail` function
- `lib/actions/watchlist.actions.ts` - `getWatchlistSymbolsByEmail` function
- `lib/actions/finnhub.actions.ts` - `getNews` function
- `lib/inngest/prompts.ts` - `NEWS_SUMMARY_EMAIL_PROMPT`
- `lib/nodemailer/templates.ts` - `NEWS_SUMMARY_EMAIL_TEMPLATE`

---

### 8. **User Authentication**
- **Better Auth integration** with MongoDB adapter
- **Email/password authentication**: Sign-up and sign-in flows
- **User profile collection**: Stores user data in MongoDB `user` collection
- **Sign-up form**: Collects full name, email, password, country, investment goals, risk tolerance, and preferred industry
- **Password requirements**: Minimum 8 characters, maximum 128 characters
- **Auto sign-in**: Automatically signs in user after successful registration
- **Session management**: JWT-based sessions with Better Auth
- **Protected routes**: Middleware redirects unauthenticated users
- **Session validation**: Checks session on protected route layouts

**Implementation Status:** ✅ Fully Implemented

**Related Files:**
- `lib/better-auth/auth.ts` - Better Auth configuration
- `lib/actions/auth.actions.ts` - `signUpWithEmail` server action
- `app/(auth)/sign-up/page.tsx` - Sign-up form with React Hook Form
- `app/(auth)/sign-in/page.tsx` - Sign-in page
- `app/(auth)/layout.tsx` - Auth layout
- `app/(root)/layout.tsx` - Protected route layout with session check
- `middleware/index.ts` - Route protection middleware

---

### 9. **Responsive UI/UX**
- **Dark mode design** optimized for extended market viewing
- **Mobile-first approach** with breakpoints for tablet/desktop
- **Accessible components** using Radix UI primitives
- **Tailwind CSS** for rapid, consistent styling
- **Toast notifications** (Sonner) for user feedback

**Color Palette:**
- Primary Yellow: `#E8BA40`, `#FDD458` (accents and CTAs)
- Dark Background: `#050505`, `#141414`, `#212328`
- Text: `#CCDADC` (light), `#9ca3af` (secondary)
- Status Colors: Green (#10b981), Red (#ef4444), Purple (#7c3aed)

**Related Files:**
- globals.css
- `components/ui/*`

---

## 👥 User Personas

### 1. **Retail Investor - "Active Trader"**
- **Characteristics**: Checks market 2-3x daily, follows 10-15 stocks, sets multiple alerts
- **Needs**: Real-time prices, quick alerts, easy watchlist management
- **Pain Points**: Information overload, missed trading opportunities

### 2. **Conservative Investor - "Long-term Planner"**
- **Characteristics**: Monthly portfolio review, holds 5-8 blue chips, prefers stability
- **Needs**: Reliable alerts, company fundamentals, dividend tracking
- **Pain Points**: Market volatility concerns, complex financial data

### 3. **Beginner Investor - "Learning Enthusiast"**
- **Characteristics**: New to investing, learns from educational content, uncertain about strategy
- **Needs**: Simple interface, educational insights, personalized guidance
- **Pain Points**: Complexity, jargon, analysis paralysis

---

## 🔄 User Workflows

### **Workflow 1: Getting Started (Onboarding)**
```
1. User visits SignalEdge
2. Sign up with email + investment profile (goals, risk tolerance, preferred industry)
3. Personalized welcome email received
4. Dashboard loads with market overview and trending stocks
5. User receives feature walkthrough or tips
```

### **Workflow 2: Adding a Stock to Watchlist**
```
1. User clicks "Add Stock" button or uses Cmd+K search
2. Searches for company by symbol or name
3. Selects stock from filtered results
4. Stock added to watchlist
5. User can now set alerts or view detailed analytics
```

### **Workflow 3: Creating Price Alert** (⚠️ Pending Implementation)
```
1. User selects stock from watchlist or stock detail page
2. Clicks "Create Alert" button (UI to be implemented)
3. Chooses alert type (upper/lower price threshold)
4. Sets target price and alert name
5. Alert saved to database (model to be created)
6. Inngest workflow monitors alerts (to be implemented)
7. When threshold met → Email notification triggered (template ready)
```

**Status**: Email templates are ready, but the alert creation UI, database model, and monitoring workflow need to be implemented.

### **Workflow 4: Receiving Daily News Summary**
```
1. Scheduled Inngest function runs daily (e.g., 8 AM ET)
2. Fetches user's watchlist stocks
3. Retrieves relevant market news from Finnhub
4. AI-summarizes news using Gemini API
5. Formatted HTML email sent to user
6. User receives personalized, digestible market summary
```

### **Workflow 5: Re-engagement (Inactive User)** (⚠️ Pending Implementation)
```
1. User hasn't visited dashboard in 30+ days
2. Inngest trigger identifies inactive user (function to be created)
3. Reminder email with market updates sent (template ready: INACTIVE_USER_REMINDER_EMAIL_TEMPLATE)
4. User clicks link, returns to dashboard
5. Engagement tracked and re-engagement workflow stops
```

**Status**: Email template exists, but the Inngest function to identify inactive users and send reminders needs to be implemented.

---

## 💻 Technical Architecture

### **Frontend Stack**
- **Framework**: Next.js 15.5.2 (App Router, Turbopack)
- **UI Library**: React 19.1.0 with Shadcn components
- **Styling**: Tailwind CSS 4.0 + PostCSS
- **Forms**: React Hook Form 7.62.0
- **Charts**: TradingView Widgets (embedded)
- **Notifications**: Sonner 2.0.7 (toast)
- **State**: React hooks, server components

### **Backend Stack**
- **Runtime**: Node.js with TypeScript 5.x
- **Database**: MongoDB 6.19.0 + Mongoose 8.18.0
- **Authentication**: Better Auth 1.3.7
- **Email Service**: Nodemailer 7.0.6
- **Workflow Engine**: Inngest 3.40.1 (event-driven tasks)
- **AI Integration**: Google Gemini API (2.5-flash-lite model)
- **Market Data**: Finnhub API (real-time stock data)

### **Deployment**
- **Hosting**: Vercel (Next.js optimized)
- **Database**: MongoDB Atlas
- **Environment Variables**: .env (see README for setup)

### **Project Structure**
```
├── app/                          # Next.js App Router
│   ├── (auth)/                   # Auth routes (sign-up, sign-in)
│   │   ├── layout.tsx            # Auth layout
│   │   ├── sign-in/page.tsx     # Sign-in page
│   │   └── sign-up/page.tsx     # Sign-up page with profile form
│   ├── (root)/                   # Protected routes
│   │   ├── page.tsx             # Dashboard (market overview)
│   │   ├── stocks/[symbol]/     # Stock detail pages
│   │   │   └── page.tsx         # Individual stock page
│   │   └── layout.tsx           # Root layout with header & session check
│   ├── api/
│   │   └── inngest/
│   │       └── route.ts         # Inngest webhook endpoint
│   ├── layout.tsx                # Root app layout
│   └── globals.css               # Global styles
├── components/                   # React components
│   ├── ui/                       # Shadcn UI components
│   │   ├── avatar.tsx
│   │   ├── button.tsx
│   │   ├── command.tsx
│   │   ├── dialog.tsx
│   │   ├── dropdown-menu.tsx
│   │   ├── input.tsx
│   │   ├── label.tsx
│   │   ├── popover.tsx
│   │   ├── select.tsx
│   │   └── sonner.tsx           # Toast notifications
│   ├── forms/                    # Form components
│   │   ├── CountrySelectField.tsx
│   │   ├── FooterLink.tsx
│   │   ├── InputField.tsx
│   │   └── SelectField.tsx
│   ├── Header.tsx               # App header with nav
│   ├── NavItems.tsx             # Navigation items
│   ├── SearchCommand.tsx        # Stock search command palette
│   ├── TradingViewWidget.tsx    # TradingView widget wrapper
│   ├── UserDropdown.tsx         # User menu dropdown
│   └── WatchlistButton.tsx      # Watchlist toggle button
├── database/
│   ├── mongoose.ts              # MongoDB connection
│   └── models/                   # Mongoose schemas
│       └── watchlist.model.ts   # Watchlist schema
├── lib/
│   ├── actions/                  # Server actions
│   │   ├── auth.actions.ts      # Auth logic (signUpWithEmail)
│   │   ├── watchlist.actions.ts # Watchlist operations
│   │   ├── finnhub.actions.ts   # Finnhub API calls
│   │   └── user.actions.ts      # User operations
│   ├── better-auth/              # Auth config
│   │   └── auth.ts              # Better Auth setup
│   ├── inngest/                  # Workflow definitions
│   │   ├── client.ts            # Inngest client
│   │   ├── functions.ts        # Event handlers (sendSignUpEmail, sendDailyNewsSummary)
│   │   └── prompts.ts          # AI prompts for Gemini
│   ├── nodemailer/               # Email setup
│   │   ├── index.ts            # Email sending functions
│   │   └── templates.ts        # HTML email templates
│   ├── constants.ts             # App constants & widget configs
│   └── utils.ts                 # Helper functions
├── middleware/
│   └── index.ts                 # Route protection middleware
├── hooks/                        # Custom React hooks
│   ├── useDebounce.ts           # Debounce hook
│   └── useTradingViewWidget.tsx # TradingView widget hook
├── public/                       # Static assets
│   └── assets/
│       ├── icons/               # SVG icons
│       └── images/              # Images
├── scripts/
│   ├── test-db.mjs              # DB connection test
│   └── test-db.ts              # TypeScript DB test
├── types/
│   └── global.d.ts              # Global TypeScript types
├── .env                          # Environment variables
├── package.json                  # Dependencies
├── tsconfig.json                 # TypeScript config
├── next.config.ts                # Next.js config
├── postcss.config.mjs            # PostCSS config
├── eslint.config.mjs             # ESLint config
├── components.json               # Shadcn config
├── project-prd.md                # This document
└── README.md                     # Documentation
```

---

## 📊 Data Models

### **User Schema** (Better Auth MongoDB Collection)
```typescript
{
  _id: ObjectId;
  id: string;                    // Better Auth user ID
  name: string;                  // Full name from sign-up
  email: string;                 // Unique email address
  emailVerified: boolean;        // Email verification status
  password: string;              // Bcrypt hashed password
  country: string;               // Selected country code
  investmentGoals: 'Growth' | 'Income' | 'Balanced' | 'Conservative';
  riskTolerance: 'Low' | 'Medium' | 'High';
  preferredIndustry: string;      // Preferred industry sector
  createdAt: Date;               // Account creation timestamp
  updatedAt: Date;               // Last update timestamp
  // Additional Better Auth fields (sessions, etc.)
}
```

**Note**: User data stored in MongoDB `user` collection. Better Auth manages the schema, with custom fields (country, investmentGoals, riskTolerance, preferredIndustry) added during sign-up.

### **Watchlist Schema**
```typescript
interface WatchlistItem extends Document {
  userId: string;              // Reference to User
  symbol: string;              // Stock symbol (uppercase)
  company: string;             // Company name
  addedAt: Date;
}
// Unique index: { userId: 1, symbol: 1 }
```

### **Alert Schema** (TypeScript Types Defined, Database Model Pending)
```typescript
// Type definition in global.d.ts
type Alert = {
  id: string;
  symbol: string;
  company: string;
  alertName: string;
  currentPrice: number;
  alertType: 'upper' | 'lower';
  threshold: number;
  changePercent?: number;
};

// Alert creation data structure
type AlertData = {
  symbol: string;
  company: string;
  alertName: string;
  alertType: 'upper' | 'lower';
  threshold: string;  // String for form input, converted to number
};
```

**Note**: Alert types are defined in TypeScript, but the MongoDB model/schema and CRUD operations need to be implemented. Email templates are ready for when alerts are triggered.

### **News Article Schema**
```typescript
type MarketNewsArticle = {
  id: number;
  headline: string;
  summary: string;
  source: string;
  url: string;
  datetime: number;         // Unix timestamp
  category: string;
  related: string;
  image?: string;
};
```

---

## 🔌 API Integrations

### **Finnhub API**
- **Purpose**: Real-time stock data and market news
- **Endpoints Used**:
  - `/search` - Stock symbol and company search
  - `/company-news` - Company-specific news articles
  - `/news` - General market news (fallback)
  - `/stock/profile2` - Company profile data (for popular stocks)
- **Rate Limits**: Handled with React cache and revalidation strategies
  - Search results: 1800 seconds (30 minutes) cache
  - Company profiles: 3600 seconds (1 hour) cache
  - News articles: 300 seconds (5 minutes) cache
- **Base URL**: `https://finnhub.io/api/v1`
- **Error Handling**: Graceful fallbacks, returns empty arrays on errors
- **Article Filtering**: Validates and formats articles, removes duplicates
- **Round-robin Selection**: Distributes articles evenly across user's watchlist symbols

**Related Files:**
- `lib/actions/finnhub.actions.ts` - `searchStocks()`, `getNews()` functions
- `lib/utils.ts` - `validateArticle()`, `formatArticle()`, `getDateRange()` helpers

### **Google Gemini API**
- **Purpose**: AI-powered content generation
- **Use Cases**:
  - Personalized welcome email content
  - Daily news summary generation
  - News simplification for non-technical readers
- **Model**: `gemini-2.5-flash-lite` (fast, cost-effective)

**Related Files:**
- functions.ts
- prompts.ts

### **TradingView Widgets**
- **Purpose**: Professional charting and market data visualization
- **Widget Types**:
  - Symbol Info widget (current price, change %)
  - Advanced Chart (candlestick, line charts)
  - Baseline widget (technical analysis)
  - Technical Analysis widget
  - Company Profile widget
  - Company Financials widget
  - Market Overview
  - Stock Heatmap
  - Top Stories

**Configuration:**
- All configured in constants.ts
- Dark theme optimized
- Custom colors matching SignalEdge brand
- Fully responsive

---

## 📧 Email Communication

### **Email Service Configuration**
- **Provider**: Nodemailer (SMTP)
- **Transport**: Gmail SMTP or custom SMTP server
- **Environment Variables**:
  - `NODEMAILER_EMAIL`: Sender email address
  - `NODEMAILER_PASSWORD`: App-specific password (Gmail app password)
- **Email Functions**:
  - `sendWelcomeEmail()` - Sends personalized welcome email
  - `sendNewsSummaryEmail()` - Sends daily news summary
  - Additional functions for alert emails (ready for implementation)

**Related Files:**
- `lib/nodemailer/index.ts` - Email sending functions
- `lib/nodemailer/templates.ts` - All HTML email templates

### **Email Template System**
All templates are **responsive HTML** with:
- Mobile-first design (@media queries for 768px, 600px, 480px)
- Dark mode colors matching app
- Inline CSS for email client compatibility
- Fallback fonts and colors
- Clear CTAs with proper styling
- Personalization placeholders (`{{variable}}`)

**Template Variables:**
- `{{name}}`: User first/last name
- `{{email}}`: User email
- `{{symbol}}`: Stock ticker symbol
- `{{company}}`: Company name
- `{{currentPrice}}`: Current stock price
- `{{targetPrice}}`: Alert threshold price
- `{{changePercent}}`: Price change percentage
- `{{timestamp}}`: Current date/time
- `{{newsContent}}`: AI-generated news summary
- `{{dashboardUrl}}`: Link to dashboard
- `{{unsubscribeUrl}}`: Unsubscribe link

---

## 🎨 UI/UX Design System

### **Color Palette**
| Purpose | Color | Hex |
|---------|-------|-----|
| Primary Accent | Yellow | `#E8BA40`, `#FDD458` |
| Background | Dark | `#050505`, `#141414`, `#212328` |
| Primary Text | Light Gray | `#CCDADC` |
| Secondary Text | Medium Gray | `#9ca3af` |
| Border | Gray | `#30333A`, `#374151` |
| Success/Buy Signal | Green | `#10b981` |
| Alert/Sell Signal | Red | `#ef4444`, `#dc2626` |
| Volume Alert | Purple | `#7c3aed` |

### **Typography**
- **Font Family**: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`
- **Headings**: Bold, 24-28px
- **Body Text**: Regular, 14-16px
- **Secondary Text**: 12-14px, reduced opacity

### **Component Library** (Shadcn)
- `Button`: Primary (yellow), secondary, ghost variants
- `Input`: Text, email, password, search
- `Label`: Paired with inputs
- `Dropdown-Menu`: User menu, context actions
- `Dialog`: Confirmation dialogs, modals
- `Popover`: Tooltips, inline information
- `Command`: Search/command palette
- `Avatar`: User profile pictures
- `Checkbox`, `Radio`: Form controls

### **Responsive Breakpoints**
- **Mobile**: < 640px
- **Tablet**: 640px - 1024px (md: 768px)
- **Desktop**: > 1024px (lg: 1024px, xl: 1280px)

---

## 🔐 Security & Authentication

### **Authentication Flow**
1. **Sign-Up**: User provides email, password, full name, country, investment goals, risk tolerance, and preferred industry
2. **Password Hashing**: Better Auth handles bcrypt hashing automatically
3. **User Storage**: User data stored in MongoDB `user` collection via Better Auth MongoDB adapter
4. **Auto Sign-In**: User automatically signed in after successful registration
5. **Session Management**: JWT-based sessions with Better Auth, stored in cookies
6. **Protected Routes**: Middleware (`middleware/index.ts`) checks session cookie and redirects to `/` (home) if not authenticated
7. **Session Validation**: `auth.api.getSession()` called in `app/(root)/layout.tsx` to validate session
8. **Event Trigger**: User creation triggers Inngest event `app/user.created` for welcome email workflow

**Related Files:**
- `middleware/index.ts` - Route protection middleware
- `lib/better-auth/auth.ts` - Better Auth configuration with MongoDB adapter
- `lib/actions/auth.actions.ts` - `signUpWithEmail` server action
- `app/(auth)/layout.tsx` - Auth layout
- `app/(root)/layout.tsx` - Protected route layout with session validation
- `app/(auth)/sign-up/page.tsx` - Sign-up form with React Hook Form

### **Data Privacy**
- **User Data**: Encrypted at rest in MongoDB
- **Watchlist**: User-specific with `userId` isolation
- **Alerts**: Associated with user ID only
- **Email**: Hashed and salted, no PII exposed
- **GDPR Compliance**: Unsubscribe functionality, data export capability

---

## 🚀 Feature Roadmap

### **Phase 1: MVP (Current)**
- ✅ Stock dashboard with TradingView widgets (Market Overview, Heatmap, Top Stories, Market Data)
- ✅ Stock search with command palette (Cmd+K)
- ✅ Stock detail pages with comprehensive TradingView widgets
- ✅ Watchlist button component and database model
- ⚠️ Watchlist management page (UI not implemented, backend ready)
- ⚠️ Price and volume alerts (email templates ready, core functionality pending)
- ✅ Email notification templates (Welcome, News Summary, Alert templates)
- ✅ User authentication (Better Auth with MongoDB)
- ✅ AI-powered welcome emails (Inngest workflow)
- ✅ Daily news summaries (Inngest workflow with AI summarization)

### **Phase 2: Enhanced Analytics (Q2)**
- 📊 Portfolio performance tracking
- 📊 Earnings calendar integration
- 📊 Dividend tracking
- 📊 Tax lot management
- 📊 Advanced technical indicators

### **Phase 3: Social & Community (Q3)**
- 👥 Stock watchlists sharing
- 👥 User discussions/forums
- 👥 Expert recommendations
- 👥 Social trading integration
- 👥 Leaderboards

### **Phase 4: Mobile App (Q4)**
- 📱 Native iOS app
- 📱 Native Android app
- 📱 Push notifications
- 📱 Biometric authentication
- 📱 Offline mode

### **Phase 5: Advanced Features (Future)**
- 🤖 ML-powered price prediction
- 🤖 Sentiment analysis
- 🤖 Automated portfolio rebalancing
- 🤖 API for third-party integrations
- 🤖 Options trading support

---

## 📈 Success Metrics

### **User Engagement**
- **Daily Active Users (DAU)**: Target 5K+ within 6 months
- **Monthly Active Users (MAU)**: Target 25K+ within 6 months
- **Session Duration**: Average 15-30 minutes
- **Watchlist Average Size**: 8-12 stocks per user

### **Feature Adoption**
- **Watchlist Creation Rate**: 80%+ of new users
- **Alert Setup Rate**: 60%+ of new users
- **Email Open Rate**: 35-40% (industry benchmark)
- **Email Click-Through Rate**: 5-8% (CTA buttons)

### **Retention**
- **7-Day Retention**: 50%+
- **30-Day Retention**: 35%+
- **60-Day Retention**: 25%+
- **Churn Rate**: < 5% monthly

### **Technical Performance**
- **Page Load Time**: < 2 seconds (90th percentile)
- **API Response Time**: < 500ms
- **Uptime**: 99.9%+
- **Error Rate**: < 0.1%

---

## 🛠️ Development Guidelines

### **Technology Decisions**
1. **Next.js App Router**: Server-side rendering for SEO, server actions for data mutations
2. **MongoDB**: Flexible schema, scalability, developer-friendly
3. **Inngest**: Reliable, event-driven workflows without managing servers
4. **Tailwind CSS**: Rapid UI development with utility classes
5. **TypeScript**: Type safety and better developer experience

### **Code Quality**
- **Linting**: ESLint + Next.js recommended rules
- **Type Safety**: Strict TypeScript mode enabled
- **Testing**: Unit tests for utilities, integration tests for workflows
- **Documentation**: JSDoc comments for public functions
- **Git Workflow**: Feature branches, PR reviews

### **Environment Setup**
```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your credentials

# Run development server
npm run dev

# Run Inngest locally
npx inngest-cli@latest dev

# Test database connection
npm run test:db

# Build for production
npm run build
npm start
```

---

## 📝 Notes & Considerations

### **Implementation Status Summary**

**✅ Fully Implemented:**
- Stock dashboard with TradingView widgets
- Stock search with command palette
- Stock detail pages with comprehensive widgets
- User authentication (Better Auth)
- Welcome email workflow (Inngest + AI)
- Daily news summary workflow (Inngest + AI)
- Email templates (all types)
- Watchlist database model and button component

**⚠️ Partially Implemented:**
- Watchlist management (backend ready, UI page pending)
- Alert system (types and templates ready, core functionality pending)

**❌ Not Implemented:**
- Alert creation UI and database model
- Alert monitoring/checking workflow
- Dedicated watchlist management page
- Inactive user reminder workflow (template ready, function pending)

### **Known Limitations**
1. **Real-Time Updates**: TradingView widgets update on market hours only
2. **Email Delivery**: Depends on email service provider (Gmail, SendGrid)
3. **API Rate Limits**: Finnhub has rate limits (managed with server-side caching and React cache)
4. **Scaling**: MongoDB connection pooling needed for high-concurrent users
5. **Geographic**: Initially US stock market focused (can expand)
6. **Alert System**: Email templates are ready, but alert creation, storage, and monitoring workflows need to be implemented
7. **Watchlist UI**: Backend model exists, but dedicated watchlist management page/table view not implemented
8. **News Caching**: News articles cached for 300 seconds (5 minutes) to manage API rate limits
9. **Popular Stocks**: Hardcoded list of 50 popular stock symbols in constants.ts

### **Future Considerations**
- WebSocket integration for real-time stock price streaming
- Redis caching for frequently accessed data
- CDN for static assets and images
- Database indexing optimization as data grows
- Analytics pipeline (Google Analytics, custom events)
- A/B testing framework for feature rollouts
- Admin dashboard for stock/news management

---

## 📞 Support & Resources

- **GitHub Repository**: [signalist_stock-tracker-app](https://github.com/nitishkb19315/signaledge_stock-tracker-app)
- **Documentation**: See README.md
- **API Docs**: 
  - [Finnhub API](https://finnhub.io/docs/api)
  - [Google Gemini API](https://ai.google.dev/docs)
  - [TradingView Widgets](https://www.tradingview.com/external-embedding/)
  - [Inngest Documentation](https://www.inngest.com/docs)

---