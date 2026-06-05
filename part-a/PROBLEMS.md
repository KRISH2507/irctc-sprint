# IRCTC Pain Points Documentation

## Given Problems

### 1. Tatkal Booking Crashes at 10:00 AM
- **What is broken**: The booking portal becomes unresponsive, throws Gateway Timeouts, or logs out users exactly when the Tatkal booking window opens.
- **Affected users**: 100% of users attempting to book Tatkal tickets at 10:00 AM / 11:00 AM.
- **Frequency**: Daily.
- **Current flow step-by-step**: 
  1. Login at 9:55 AM.
  2. Enter source and destination.
  3. Select date and click Search.
  4. Wait for 10:00 AM.
  5. Click 'Book Now' under Tatkal quota.
  6. Add passenger details.
  7. Click 'Proceed to Payment'.
- **Where exactly it breaks**: Fails prominently at Step 5 and Step 7 due to overwhelming concurrent DB writes & server thread exhaustion.
- **Business impact**: Massive loss of credibility, increased burden on alternative ticketing methods, potential revenue loss to third-party agents.
- **User impact**: High anxiety, inability to secure emergency travel, wasted time.

### 2. Search Filters Do Not Work Reliably
- **What is broken**: When applying filters (e.g., specific train types, departure times), paginating or returning from the payment page completely resets the applied filters.
- **Affected users**: Users searching across busy routes with multiple trains (e.g., Delhi-Mumbai).
- **Frequency**: Very high (every session involving filters).
- **Current flow step-by-step**: 
  1. Search for a route.
  2. View list of 20+ trains.
  3. Apply 'AC 3 Tier' and 'Departure after 18:00' filters.
  4. View filtered list.
  5. Select a train and view availability.
  6. Hit 'Back' to select a different train.
  7. Observe the list is completely unfiltered again.
- **Where exactly it breaks**: Step 7. Filter states are not persisted in local storage or session state.
- **Business impact**: Decreases conversion rate as users abandon search due to frustration.
- **User impact**: Repetitive manual effort, leading to a frustrating and slow booking experience.

### 3. Seat Selection Resets Randomly
- **What is broken**: Users select lower/upper berth preferences, but due to session timeouts or UI refresh glitches, the preference is lost before the payment gateway.
- **Affected users**: Elderly or specially-abled passengers who strictly require specific berths.
- **Frequency**: Moderate to High.
- **Current flow step-by-step**:
  1. Select a train and class.
  2. Click Book Now.
  3. Provide passenger details.
  4. Select 'Lower Berth' preference.
  5. Check "Book only if confirm berths are allotted".
  6. Proceed to review screen (system takes long to load).
  7. Form reloads or prompts CAPTCHA again, wiping the berth preference array.
- **Where exactly it breaks**: Step 7 (State management failure during form validation retries).
- **Business impact**: High customer complaints regarding wrong berth allocation, refund requests.
- **User impact**: Physical discomfort during travel, complete distrust in the preference system.

---

## Self-Discovered Problems

### 1. Refund Status Tracking is Confusing
- **What is broken**: After cancelling a ticket, the refund status says "Processing" for days with no timeline, ETA, or transaction reference ID linked to the bank.
- **Affected users**: Any user who cancels a ticket.
- **Frequency**: High (applies to all cancellations).
- **Current flow step-by-step**:
  1. Go to 'My Transactions'.
  2. Click 'Cancelled Tickets'.
  3. Select a ticket.
  4. View cancellation details.
  5. Look for refund status.
  6. See static text "Refund Processing".
  7. Wait indefinitely checking bank account manually.
- **Where exactly it breaks**: Step 6. No webhook integration with payment gateways is displayed to the user.
- **Business impact**: Flooded customer support lines and Twitter mentions regarding "Where is my refund?"
- **User impact**: Financial anxiety and uncertainty.
- **How I found it**: Attempting to cancel a booking and realizing there was no tracking timeline compared to standard e-commerce (like Amazon return tracking).
- **Screenshot description**: A screenshot of the 'Cancelled Tickets' view highlighting the vaguely worded "Processing" text with no progress bar.
- **Severity level**: High.

### 2. PNR Status Terminology is Hard to Understand
- **What is broken**: Acronyms like RLWL, GNWL, PQWL, and RAC are shown without tooltips, probabilities, or plain English explanations. Users don't know if their ticket will confirm.
- **Affected users**: Novice users, non-frequent travelers, rural user base.
- **Frequency**: Very high (applies to almost all waitlisted tickets).
- **Current flow step-by-step**:
  1. Book a waitlisted ticket.
  2. Receive PNR number.
  3. Go to "PNR Enquiry".
  4. Enter PNR.
  5. Solve CAPTCHA.
  6. See status: "RLWL/23".
  7. User is forced to Google "What is RLWL" or use a 3rd party app.
- **Where exactly it breaks**: Step 6. The interface fails to communicate the reality of the user's booking status.
- **Business impact**: Loss of traffic to third-party prediction apps (like Ixigo, ConfirmTkt).
- **User impact**: Confusion, stress, and inability to make backup travel plans.
- **How I found it**: Conducted a cognitive walkthrough pretending to be a first-time user booking a waitlisted ticket.
- **Screenshot description**: The PNR enquiry result page showing a dense table with esoteric acronyms and zero explanatory text.
- **Severity level**: Medium.

### 3. Mobile Booking Flow Requires Excessive Scrolling
- **What is broken**: The mobile web and app views simply stack desktop horizontal components vertically, resulting in a tedious amount of scrolling just to review a single train's classes.
- **Affected users**: Mobile app and mobile web users (~80% of consumer traffic).
- **Frequency**: Constant on mobile devices.
- **Current flow step-by-step**:
  1. Open IRCTC on mobile browser.
  2. Search for route.
  3. See Train #1 card.
  4. Scroll horizontally to find 3AC.
  5. Tap 3AC to load availability.
  6. Available dates pop up below, pushing next trains out of view.
  7. Must scroll up/down continuously to compare two different trains.
- **Where exactly it breaks**: Step 4 through 7. The UI is not responsive—it's just a shrunken desktop site.
- **Business impact**: Drop-offs on mobile, lower conversion on smaller screens.
- **User impact**: Frustration, accidental taps, difficulty comparing options.
- **How I found it**: Opened IRCTC on a simulated mobile viewport (iPhone 13 Pro) and attempted to compare availability across 3 trains.
- **Screenshot description**: A long scrollable page where a single train's expanded classes take up 1.5x the viewport height.
- **Severity level**: High.