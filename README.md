# FoodFast - Food Delivery Mobile App

A cross-platform food delivery mobile application built with React Native, Expo, and Supabase. Supports Android, iOS, and Web with a unified codebase, featuring real-time cart synchronization, MoMo payment integration, and a modern dark/light theme system.

## Overview

FoodFast is a full-featured mobile food ordering app that allows customers to browse restaurant menus by category, manage their cart, place orders, and pay via MoMo e-wallet. The application uses Supabase as the backend service for authentication, database operations, and real-time updates. Payment processing is handled client-side with HMAC-SHA256 signature generation.

## Features

### Customer Features

- **Onboarding Flow** - Smooth onboarding experience on first launch
- **User Authentication** - Secure registration and login via Supabase Auth
- **Browse Menu** - View products by category with search, filter, and pagination
- **Product Details** - Detailed product pages with description, price, and ratings
- **Shopping Cart** - Add/remove items, update quantities with real-time total calculation
- **Checkout** - Address form with delivery time picker and order summary
- **MoMo Payment** - E-wallet payment integration with deep-link redirect
- **Order History** - View all past orders with status tracking
- **Profile Management** - Edit personal information, address, and change password
- **Dark / Light Theme** - System-aware automatic theme switching

### Technical Features

- **File-based Routing** - Expo Router with typed routes for navigation
- **New Architecture** - React Native New Architecture enabled (Fabric + TurboModules)
- **React Compiler** - Enabled via Expo experimental flag
- **Custom Hooks** - Debounced search, pagination, menu data, cart data, theme utilities
- **Cart Context** - Global cart state management via React Context API
- **Form Validation** - Input validation utilities for checkout and profile
- **Responsive UI** - Shared styles and constants for consistent design across screens

## Tech Stack

### Core

- **React Native 0.81.4** - Cross-platform mobile UI framework
- **React 19.1.0** - UI library with React Compiler support
- **Expo ~54.0.13** - Managed workflow and native module access
- **TypeScript** - Static typing throughout the project

### Navigation

- **Expo Router ~6.0.11** - File-based routing with typed routes
- **React Navigation 7** - Bottom tabs and native stack navigation
  - `@react-navigation/bottom-tabs ^7.4.0`
  - `@react-navigation/native ^7.1.8`

### Backend & Storage

- **Supabase JS ^2.75.0** - Authentication, PostgreSQL database, real-time
- **AsyncStorage 2.2.0** - Persistent local storage for auth sessions

### UI & Animation

- **React Native Reanimated ~4.1.1** - High-performance animations
- **React Native Gesture Handler ~2.28.0** - Native touch and gesture handling
- **React Native Modal ^14.0.0** - Customizable modal overlays
- **Expo Image ~3.0.9** - Optimized image rendering
- **Expo Vector Icons ^15.0.2** - Icon library
- **Expo Haptics ~15.0.7** - Haptic feedback for interactions
- **React Native Safe Area Context ~5.6.0** - Safe area insets handling
- **React Native Screens ~4.16.0** - Native screen containers

### Payment

- **CryptoJS ^4.2.0** - HMAC-SHA256 signature generation for MoMo API
- **Expo Linking ~8.0.8** - Deep-link handling for MoMo payment redirect
- **Expo Web Browser ~15.0.8** - In-app browser for payment flow

### Development Tools

- **ESLint** - Code linting with Expo config
- **depcheck ^1.4.7** - Unused dependency detection

## Project Structure

```
FE_Mobile/
├── app/                        # Expo Router file-based routes
│   ├── _layout.tsx             # Root layout (Onboarding + CartProvider)
│   ├── (tabs)/                 # Bottom tab navigator
│   │   ├── _layout.tsx         # Tab bar configuration
│   │   ├── index.tsx           # Home / Menu page
│   │   ├── orders.tsx          # Order history page
│   │   └── profile.tsx         # Profile page
│   ├── auth/                   # Authentication screens
│   │   ├── _onboarding.tsx     # Onboarding screen
│   │   ├── _welcome.tsx        # Welcome screen
│   │   ├── _login.tsx          # Login screen
│   │   └── _signup.tsx         # Registration screen
│   ├── context/
│   │   └── _cartContext.tsx    # Cart global state provider
│   └── screen/                 # Additional screens (stack navigation)
│       ├── menu.tsx            # Full menu screen
│       ├── productDetail.tsx   # Product detail screen
│       ├── checkout.tsx        # Checkout screen
│       ├── payment.tsx         # Payment screen
│       ├── editProfile.tsx     # Edit profile screen
│       └── changePassword.tsx  # Change password screen
│
├── components/                 # Reusable UI components
│   ├── themed-text.tsx         # Theme-aware Text component
│   ├── themed-view.tsx         # Theme-aware View component
│   ├── auth/                   # Auth-specific components
│   │   ├── authButton.tsx
│   │   ├── authHeader.tsx
│   │   ├── authInput.tsx
│   │   └── index.ts
│   ├── cart/                   # Cart components
│   │   ├── cart.tsx
│   │   ├── cartItem.tsx
│   │   ├── cartSummary.tsx
│   │   ├── emptyCart.tsx
│   │   └── index.ts
│   ├── checkout/               # Checkout components
│   │   ├── addressForm.tsx
│   │   ├── deliveryTimePicker.tsx
│   │   ├── orderSummary.tsx
│   │   └── index.ts
│   ├── menu/
│   │   └── menu.tsx            # Menu list with category filter
│   ├── orders/                 # Order components
│   │   ├── orderCard.tsx
│   │   ├── orderTabs.tsx
│   │   ├── emptyOrders.tsx
│   │   └── index.ts
│   ├── profile/                # Profile components
│   │   ├── profileHeader.tsx
│   │   ├── profileField.tsx
│   │   ├── profileButton.tsx
│   │   ├── profileInput.tsx
│   │   └── index.ts
│   └── account/
│       └── accountModal.tsx    # Account action modal
│
├── constants/                  # App-wide constants
│   ├── app.ts                  # Colors, pricing, sizes, pagination config
│   ├── theme.ts                # Light/dark theme color tokens + font families
│   └── sharedStyles.ts         # Shared StyleSheet definitions
│
├── hooks/                      # Custom React hooks
│   ├── use-cart-data.ts        # Cart data access hook
│   ├── use-color-scheme.ts     # Color scheme (native)
│   ├── use-color-scheme.web.ts # Color scheme (web)
│   ├── use-debounce.ts         # Input debounce hook
│   ├── use-filtered-items.ts   # Search/filter logic hook
│   ├── use-menu-data.ts        # Menu and category fetching hook
│   ├── use-pagination.ts       # Pagination logic hook
│   └── use-theme-color.ts      # Theme color resolution hook
│
├── services/                   # Data access and API layer
│   ├── supabaseClient.ts       # Supabase client initialization
│   ├── menuService.ts          # Category and product fetching
│   ├── orderService.ts         # Order creation and history
│   ├── paymentService.ts       # MoMo payment API integration
│   └── profileService.ts       # Customer profile CRUD
│
├── utils/
│   └── validation.ts           # Form validation helpers
│
├── assets/
│   └── images/                 # App icons, splash screen, adaptive icons
│
├── scripts/
│   └── reset-project.js        # Reset project to starter state
│
├── app.json                    # Expo app configuration
├── package.json                # Dependencies and scripts
├── tsconfig.json               # TypeScript configuration
├── eslint.config.js            # ESLint configuration
└── fastfood.sql                # Database schema for Supabase
```

## Database Schema

Run `fastfood.sql` in the Supabase SQL Editor to initialize the database. This creates the following tables:

| Table          | Description                          |
| -------------- | ------------------------------------ |
| `category`     | Product categories with icon URLs    |
| `product`      | Menu items with price, rating, image |
| `customer`     | Customer profiles linked to auth     |
| `orders`       | Order records with status tracking   |
| `order_detail` | Line items belonging to each order   |
| `payment`      | Payment records with transaction IDs |
| `cart`         | Shopping cart items per customer     |

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** v18 or higher
- **npm** v9 or higher (or **yarn**)
- **Git**
- **Expo CLI** — install globally: `npm install -g expo-cli`
- **Supabase Account** — free tier at [supabase.com](https://supabase.com)
- **Android Studio** (for Android emulator) or **Xcode** (for iOS simulator, macOS only)
- **Expo Go** app on your physical device (optional, for quick testing)

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/Ngct253/FoodDeliveryApp.git
cd FoodDeliveryApp/FE_Mobile
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up Supabase

1. Go to [supabase.com](https://supabase.com) and create a new project
2. Navigate to **Settings > API** and copy the **Project URL** and **anon/public key**
3. Open the **SQL Editor** in the Supabase Dashboard and run the contents of `fastfood.sql`
4. Enable **Email Auth** under **Authentication > Providers**

### 4. Configure environment variables

Create a `.env` file in the root of `FE_Mobile/`:

```env
EXPO_PUBLIC_SUPABASE_URL=your_supabase_project_url
EXPO_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
```

> All variables prefixed with `EXPO_PUBLIC_` are exposed to the client bundle. Never put secrets in these variables.

### 5. Start the development server

```bash
npm start
```

## Running the Application

### On a Physical Device

1. Install the **Expo Go** app (Android / iOS)
2. Run `npm start` in the terminal
3. Scan the QR code displayed in the terminal or browser

### On Android Emulator

```bash
npm run android
```

Ensure Android Studio is installed and an AVD (Android Virtual Device) is running before executing this command.

### On iOS Simulator (macOS only)

```bash
npm run ios
```

Requires Xcode and the iOS Simulator to be installed.

### On Web Browser

```bash
npm run web
```

Opens the app in your default browser using React Native Web.

## Available Scripts

| Script                   | Description                                          |
| ------------------------ | ---------------------------------------------------- |
| `npm start`              | Start Expo development server (interactive CLI)      |
| `npm run android`        | Launch app on Android emulator or connected device   |
| `npm run ios`            | Launch app on iOS simulator (macOS only)             |
| `npm run web`            | Launch app in web browser                            |
| `npm run lint`           | Run ESLint across the project                        |
| `npm run reset-project`  | Move starter code to `app-example/` and reset `app/` |

## App Routing Structure

This project uses Expo Router's file-based routing. Routes are derived directly from the file system inside the `app/` directory.

### Tab Routes (always visible in bottom navigation)

| Route         | Screen       | Description                        |
| ------------- | ------------ | ---------------------------------- |
| `/`           | Home / Menu  | Browse products and categories     |
| `/orders`     | Orders       | Order history with status tabs     |
| `/profile`    | Profile      | User profile and settings          |

### Auth Routes

| Route              | Screen      | Description                       |
| ------------------ | ----------- | --------------------------------- |
| `/auth/_onboarding`| Onboarding  | Shown on first launch             |
| `/auth/_welcome`   | Welcome     | Entry point to auth flow          |
| `/auth/_login`     | Login       | Email and password login          |
| `/auth/_signup`    | Sign Up     | New account registration          |

### Stack Routes (pushed on top of tabs)

| Route                  | Screen          | Description                      |
| ---------------------- | --------------- | -------------------------------- |
| `/screen/menu`         | Full Menu       | Browsable menu with search       |
| `/screen/productDetail`| Product Detail  | Item description, price, rating  |
| `/screen/checkout`     | Checkout        | Address form and delivery time   |
| `/screen/payment`      | Payment         | MoMo payment initiation          |
| `/screen/editProfile`  | Edit Profile    | Update name, phone, address      |
| `/screen/changePassword`| Change Password| Update account password          |

## MoMo Payment Integration

Payments are processed via the **MoMo Sandbox API** using a direct client-to-gateway request. Signatures are generated client-side with **HMAC-SHA256** using CryptoJS.

**Payment flow:**

1. User taps **Pay with MoMo** on the payment screen
2. `paymentService.ts` builds the request payload and signs it
3. A request is sent to MoMo's sandbox endpoint
4. The returned `payUrl` is opened via `expo-web-browser`
5. MoMo redirects back to the app via a deep-link (`fooddeliveryapp://`)
6. The order and payment records are saved to Supabase

**Configuration** (in `services/paymentService.ts`):

| Parameter      | Value                                              |
| -------------- | -------------------------------------------------- |
| Currency       | VND                                                |
| Platform       | Mobile (expo-linking deep link)                    |
| Endpoint       | `https://test-payment.momo.vn/v2/gateway/api/create` |
| Request Type   | `payWithMethod`                                    |
| Signature Algo | HMAC-SHA256                                        |

> For production deployment, move the MoMo secret key and signature generation to a secure backend server to avoid exposing credentials in the client bundle.

## Environment Variables Reference

| Variable                        | Required | Description                        |
| ------------------------------- | -------- | ---------------------------------- |
| `EXPO_PUBLIC_SUPABASE_URL`      | Yes      | Your Supabase project URL          |
| `EXPO_PUBLIC_SUPABASE_ANON_KEY` | Yes      | Your Supabase anon/public API key  |

## Key Implementation Details

### Cart State Management

Cart state is managed globally via `CartProvider` in `app/context/_cartContext.tsx`, wrapping the entire app from the root layout. This allows any screen to access and mutate cart data without prop drilling.

### Custom Hooks

| Hook                  | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| `use-menu-data`       | Fetches categories and products from Supabase       |
| `use-cart-data`       | Reads cart state from context                       |
| `use-filtered-items`  | Filters menu items by search query and category     |
| `use-pagination`      | Slice items for paginated list rendering            |
| `use-debounce`        | Delays search query propagation (200ms default)     |
| `use-theme-color`     | Resolves color token based on active color scheme   |
| `use-color-scheme`    | Detects system light/dark preference (native + web) |

### Theme System

- **App colors** (primary, accent, text) are defined in `constants/app.ts`
- **Light/dark tokens** are defined in `constants/theme.ts`
- `ThemedText` and `ThemedView` components automatically apply the correct color based on system preference
- Fonts are resolved per platform (iOS system-ui, Android normal, Web system-ui stack)

## Troubleshooting

**Metro bundler cache issues:**

```bash
npx expo start --clear
```

**Environment variables not loading:**

Ensure your `.env` file is at the root of `FE_Mobile/` and all variable names start with `EXPO_PUBLIC_`. Restart the dev server after any changes to `.env`.

**Android build fails with NDK error:**

```bash
cd android && ./gradlew clean && cd ..
npm run android
```

**Supabase auth errors:**

Verify that **Email Auth** is enabled in your Supabase project under **Authentication > Providers > Email**.

## Support

For issues and questions:

- Issues: [GitHub Issues](https://github.com/Ngct253/FoodDeliveryApp/issues)
- Expo Documentation: [docs.expo.dev](https://docs.expo.dev)
- Supabase Documentation: [supabase.com/docs](https://supabase.com/docs)

---

**Built with React Native, Expo, and Supabase**
