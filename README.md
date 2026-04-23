# Revamine Hybrid App - Firestore Database Schema
This document defines the authoritative structure for the Flutter Hybrid Application. It shares the same backend as the Web platform but with platform-specific display logic.

## 1. users
The app uses this to sync profile, balance, and levels.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `userId` | String | Unique ID of the user (Document ID) |
| `name` | String | Full name of the user |
| `email` | String | Email address |
| `pointsBalance` | Number | Current RC balance |
| `totalPointsEarned` | Number | Lifetime earnings |
| `level` | String | User tier ('Bronze', 'Silver', etc.) |
| `referralCode` | String | User's invite code |
| `photoURL` | String | Profile picture URL |
| `status` | String | 'Active', 'Suspended', 'Banned' |

---

## 2. app_tasks
**Primary Data Source for App Tasks**. Only documents from this collection appear in the App's "Available Tasks" list.

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
| `instructions` | Array | Answer options shared with the UI |

---

## 3. task_submissions (Synced History)
Shows the status of all work done by the user. Note: In the app, users see submissions for **BOTH** Web tasks and App tasks.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `id` | String | Unique Submission ID |
| `taskId` | String | ID from either `tasks` or `app_tasks` collection |
| `taskTitle` | String | Title of the task for display in app history |
| `status` | String | 'Pending', 'Approved', 'Rejected' |
| `points` | Number | Reward amount |
| `submittedAt` | Timestamp | Date of submission |

---

## 4. redemptions (Gift Card Only)
Used for rewards. While history shows all past types, **New requests from the app** are restricted to Gift Cards.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `id` | String | Request ID |
| `item` | String | Name of the Gift Card (e.g., '$5 Google Play') |
| `points` | Number | Points cost |
| `status` | String | 'Pending', 'Approved', 'Rejected' |
| `code` | String | The Gift Code (Visible to user after approval) |
| `createdAt` | Timestamp | Request date |

---

## 5. activity_logs
Shared point transaction history visible in the app.

| Field Name | Data Type | Description |
|------------|-----------|-------------|
| `type` | String | Activity description ('Task Approved', etc.) |
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

## ❌ EXCLUDED FOR HYBRID APP
These collections/logics are completely ignored in the Hybrid App pages:
- **tasks**: Not shown in the available list (only appears in submission history).
- **Settings**: System-level backend configuration.
- **user_tasks**: Web-only multi-step tracking logic.
