# Technical Documentation - Poke App

**Version:** 1.0.0
**Last Updated:** February 2026
**Platform:** iOS 14+ | Android 5.0+ (API 21+)

---

## Table of Contents

1. [Tech Stack](#tech-stack)
2. [Architecture Overview](#architecture-overview)
3. [Database Schema](#database-schema)
4. [RevenueCat Implementation](#revenuecat-implementation)
5. [Sync Architecture](#sync-architecture)
6. [Notification System](#notification-system)

---

## Tech Stack

### Core Framework
```
React Native 0.81.5
├── Expo SDK 54
├── TypeScript 5.9.2 (strict mode)
└── Expo Router 6.0 (file-based navigation)
```

**Why React Native + Expo?**
- **Cross-platform parity** - Single codebase, identical UX on iOS/Android
- **Rapid development** - Expo SDK provides native modules out of the box
- **OTA updates** - Push bug fixes without App Store review (within limits)
- **Developer experience** - Hot reload, TypeScript support, excellent tooling

### Database & ORM
```
Local: expo-sqlite 16.0
ORM: Drizzle ORM 0.45.1
Cloud: Supabase (PostgreSQL)
```

**Why Drizzle ORM?**
- **Type safety** - Full TypeScript inference, zero runtime overhead
- **SQL-like syntax** - Easy to understand, no magic
- **Dual-driver support** - Same schema for SQLite (local) and PostgreSQL (cloud)
- **Migration-friendly** - Schema changes are straightforward

### Authentication & Subscriptions
```
Auth: Supabase Auth
Subscriptions: RevenueCat 9.7.6
Payments: Apple App Store + Google Play Store (via RevenueCat)
```

### Notifications
```
expo-notifications 0.32.16
expo-task-manager (background tasks)
rrule 2.8.1 (recurring reminder scheduling)
```

### UI & Animations
```
Styling: React Native StyleSheet
Gestures: react-native-gesture-handler 2.28
Animations: react-native-reanimated 4.1.1
Icons: @expo/vector-icons 15.0 (Ionicons)
Font: Comfortaa (Google Fonts via expo-google-fonts)
```

### Utilities
```
date-fns 4.1.0 (date manipulation)
date-fns-tz 3.2.0 (timezone handling)
uuid 13.0.0 (unique ID generation)
```

### Development Tools
```
EAS Build (cloud builds)
EAS Submit (app store submission)
ESLint 9.25 (linting)
TypeScript (type checking)
```

---

## Architecture Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────┐
│                   React Native App                   │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────┐ │
│  │ Expo Router  │  │   Contexts   │  │ Components│ │
│  │ (Navigation) │  │ (State Mgmt) │  │   (UI)    │ │
│  └──────────────┘  └──────────────┘  └───────────┘ │
│         │                  │                 │       │
│  ┌──────▼──────────────────▼─────────────────▼────┐ │
│  │              Service Layer                      │ │
│  │  ┌─────────────┐  ┌──────────────────────────┐ │ │
│  │  │  Reminder   │  │  Notification  Sync      │ │ │
│  │  │  Service    │  │  Service       Service   │ │ │
│  │  └─────────────┘  └──────────────────────────┘ │ │
│  └────────────────────────────────────────────────┘ │
│         │                  │                 │       │
│  ┌──────▼──────┐    ┌──────▼─────┐   ┌──────▼─────┐│
│  │   Drizzle   │    │    Expo    │   │ RevenueCat ││
│  │     ORM     │    │Notifications│   │            ││
│  └──────┬──────┘    └────────────┘   └──────┬─────┘│
│         │                                     │      │
├─────────┼─────────────────────────────────────┼─────┤
│  ┌──────▼──────┐                       ┌──────▼────┐│
│  │   SQLite    │                       │   Native  ││
│  │  (Local DB) │                       │   Store   ││
│  └─────────────┘                       └───────────┘│
└─────────────────────────────────────────────────────┘
                         │
                         │ (Premium Users Only)
                         ▼
              ┌─────────────────────┐
              │   Supabase Cloud    │
              ├─────────────────────┤
              │ PostgreSQL Database │
              │ Authentication      │
              │ Real-time Sync      │
              └─────────────────────┘
```

### Folder Structure

```
poke-app/
├── app/                        # Expo Router screens
│   ├── (tabs)/                 # Tab navigation
│   │   ├── home/
│   │   ├── today/
│   │   ├── upcoming/
│   │   └── settings/
│   ├── reminder/               # Reminder CRUD
│   ├── list/                   # List management
│   └── auth/                   # Authentication
├── components/                 # Reusable components
│   ├── common/                 # Buttons, inputs, etc.
│   ├── reminder/               # Reminder-specific
│   └── list/                   # List-specific
├── hooks/                      # Custom React hooks
├── services/                   # Business logic
│   ├── reminderService.ts
│   ├── notificationService.ts
│   └── syncService.ts
├── db/                         # Database
│   ├── schema.ts               # Drizzle schema
│   ├── client.ts               # DB connection
│   └── migrations/             # SQL migrations
├── contexts/                   # React Context providers
├── utils/                      # Utility functions
├── styles/                     # StyleSheets
└── constants/                  # App constants
```

---

## Database Schema

### Entity Relationship Diagram

```
┌─────────────┐       ┌──────────────┐
│    Lists    │───┐   │   Reminders  │
└─────────────┘   │   └──────────────┘
                  │           │
                  └───────────┘
                      1:Many

┌──────────────┐      ┌──────────────┐
│  Reminders   │──────│  Subtasks    │
└──────────────┘      └──────────────┘
      │ 1:1                 1:Many
      │
┌─────▼────────┐      ┌──────────────┐
│ Recurrence   │      │    Alarms    │
│   Rules      │      │  (Early      │
└──────────────┘      │  Reminders)  │
                      └──────────────┘

┌──────────────┐      ┌──────────────┐
│  Reminders   │──────│ ReminderTags │──────┐
└──────────────┘      └──────────────┘      │
                           Many:Many         │
                                        ┌────▼────┐
                                        │  Tags   │
                                        └─────────┘
```

### Sync Strategy

**Local-First with Operational Transformation**

1. **Local changes:** Immediate write to SQLite, set `syncStatus = 'pending'`
2. **Sync trigger:** Background task every 10 seconds (premium users only)
3. **Conflict resolution:** Last-write-wins with timestamp comparison
4. **Offline queue:** Changes queued locally, synced when online

**Sync Status Flow:**
```
Local Change → syncStatus = 'pending'
     ↓
Sync to Cloud → syncStatus = 'synced'
     ↓
Conflict Detected → syncStatus = 'conflict' (manual resolution)
```

---

## RevenueCat Implementation

### Integration Architecture

```
┌────────────────────────────────────────────┐
│           React Native App                 │
│  ┌──────────────────────────────────────┐ │
│  │   hooks/useSubscription.ts           │ │
│  │   - checkSubscriptionStatus()        │ │
│  │   - purchaseSubscription()           │ │
│  │   - restorePurchases()               │ │
│  └──────────────┬───────────────────────┘ │
│                 │                          │
│  ┌──────────────▼───────────────────────┐ │
│  │  react-native-purchases 9.7.6        │ │
│  │  - Purchases.configure()             │ │
│  │  - Purchases.getCustomerInfo()       │ │
│  │  - Purchases.purchasePackage()       │ │
│  └──────────────┬───────────────────────┘ │
└─────────────────┼──────────────────────────┘
                  │
                  ▼
      ┌───────────────────────┐
      │   RevenueCat API      │
      ├───────────────────────┤
      │ - Receipt Validation  │
      │ - Subscription Status │
      │ - Webhooks            │
      │ - Analytics           │
      └───────────┬───────────┘
                  │
      ┌───────────┴───────────┐
      │                       │
      ▼                       ▼
┌───────────┐         ┌─────────────┐
│App Store  │         │Google Play  │
│Connect    │         │Console      │
└───────────┘         └─────────────┘
```

---

## Sync Architecture

### Sync Flow Diagram

```
┌─────────────────────────────────────────────┐
│          Device A (iPhone)                  │
│  ┌────────────────────────────────────────┐ │
│  │ User completes reminder                │ │
│  └────────────┬───────────────────────────┘ │
│               │                              │
│  ┌────────────▼───────────────────────────┐ │
│  │ SQLite: completed = true               │ │
│  │         syncStatus = 'pending'         │ │
│  └────────────┬───────────────────────────┘ │
└───────────────┼──────────────────────────────┘
                │
                │ Sync Service (every 10s)
                ▼
    ┌───────────────────────┐
    │   Supabase Cloud      │
    │ ┌───────────────────┐ │
    │ │ UPDATE reminders  │ │
    │ │ SET completed=true│ │
    │ │ WHERE id=?        │ │
    │ └─────────┬─────────┘ │
    └───────────┼───────────┘
                │
                │ Real-time subscription
                ▼
┌─────────────────────────────────────────────┐
│          Device B (Android)                 │
│  ┌────────────────────────────────────────┐ │
│  │ Receives change via WebSocket          │ │
│  └────────────┬───────────────────────────┘ │
│               │                              │
│  ┌────────────▼───────────────────────────┐ │
│  │ SQLite: completed = true               │ │
│  │         syncStatus = 'synced'          │ │
│  └────────────┬───────────────────────────┘ │
│               │                              │
│  ┌────────────▼───────────────────────────┐ │
│  │ UI updates, reminder disappears        │ │
│  └────────────────────────────────────────┘ │
└─────────────────────────────────────────────┘
```

---

## Notification System

### Scheduling Architecture

```
Reminder Created
    ↓
┌───────────────────────────┐
│ Calculate notification    │
│ time(s) based on:         │
│ - Due date                │
│ - Recurrence rule         │
│ - Early reminder offset   │
└───────────┬───────────────┘
            ↓
┌───────────────────────────┐
│ Schedule with             │
│ expo-notifications        │
│ - Up to 64 notifications  │
│   per app (iOS limit)     │
│ - Next 30 occurrences     │
│   for recurring reminders │
└───────────┬───────────────┘
            ↓
      ┌─────────┐
      │ Native  │
      │ Alarm   │
      │ Manager │
      └─────────┘
```