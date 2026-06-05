# PR Title
feat(core): Comprehensive IRCTC UX Redesign & Tatkal Reliability Update V1

# PR Description

This pull request introduces critical architectural and design engineering updates to stabilize the IRCTC booking flow and massively reduce user cognitive load. The changes address high-severity database locking constraints during peak volume (Tatkal) and revamp frontend state management for filters and session persistence.

## Summary of Addressed Problems

| Issue Category | Problem Desciption | Frequency | Impact Level |
| :--- | :--- | :--- | :--- |
| **System Reliability** | Tatkal Booking Crashes at 10:00 AM | Daily | Critical |
| **Frontend State** | Search Filters Do Not Work Reliably | Every Session | High |
| **Frontend State** | Seat Selection Resets Randomly | Moderate | Medium |
| **Post-Booking UX** | Refund Status is opaque ("Processing") | Every Cancellation | High |
| **Information Arch**| PNR Terminology (RLWL, GNWL) is confusing | Very High | Medium |
| **Mobile UX** | Mobile Booking Flow Requires Excessive Scrolling| Every Mobile Session | High |

## Changes Included:
- **Architecture:** Implemented Edge-based Queue Management System.
- **Frontend:** Persisted Search Filters in Context & URL params.
- **Frontend:** Persisted user seat preferences across CAPTCHA reloads via `localStorage`.
- **Integrations:** Razorpay/PayU webhooks mapped to a new Refund UI Timeline Component.
- **UI/UX:** Added semantic tooltips and prediction ML integration for PNR checks.
- **UI/UX:** Replaced legacy desktop-stacked mobile views with strict responsive, card-based mobile-first layouts.

## Testing Steps
1. Navigate to search & apply filters; hit back button. Verify filters persist.
2. Enter Tatkal booking flow at peak simulated load. Verify redirection to Waiting Room queue.
3. Cancel a mock ticket and track refund webhook response reflecting in UI.