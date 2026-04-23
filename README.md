# Revamine Hybrid App - Firestore Database Schema
This document defines the authoritative structure for the Flutter Hybrid Application. It shares the same backend as the Web platform but with platform-specific display logic.

## 1. users
The app uses this to sync profile, balance, and levels.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `userId` | String | Unique ID of the user (Document ID) |
| `name` | String | Full name of the user |
| `email` | String | Email address |
| `pointsBalance` | Number | Current points  |
| `totalPointsEarned` | Number | Lifetime earnings |
| `referralCode` | String | User's invite code |
| `photoURL` | String | Profile picture URL |
| `status` | String | 'Active', 'Suspended', 'Banned' |

---

## 2. app_tasks (missions)
**Primary Data Source for App missions**. Only documents from this collection appear in the App's "Available missions" list.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `id` | String | Unique Task ID |
| `title` | String | Task Title |
| `question` | String | Interactive question for the user |
| `description` | String | Context or hints (Optional) |
| `points` | Number | RC points reward |
| `type` | String | 'mcq', 'poll', 'true_false' |
| `image` | String | Main reference image URL |
| `correctOptionIndex` | Number | Index of the correct answer |
| `status` | String | Must be 'available' for app visibility |

---
---

## 4. redemptions (Gift Card Only)
Used for rewards. While history shows all past types, **New requests from the app** are restricted to Gift Cards.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `id` | String | Request ID |
| `item` | String | Name of the Gift Card (e.g., '1000 pts Google Play') |
| `points` | Number | Points cost |
| `status` | String | 'Pending', 'Approved', 'Rejected' |
| `code` | String | The Gift Code (Visible to user after approval) |
| `createdAt` | Timestamp | Request date |

---

## 5. activity_logs
Shared point transaction history visible in the app.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `type` | String | Activity description ('redeem Approved', etc.) |
| `points` | Number | Point change amount |
| `timestamp` | String | Displayable date string |

---

## 6. notifications
In-app alerts for the hybrid app.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `title` | String | Alert title |
| `description` | String | Message body |
| `type` | String | 'success', 'error', 'wallet' |

---


