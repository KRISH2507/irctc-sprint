# Prioritization Matrix

## 2x2 Impact vs Effort categorization

| Solution | Category | Impact (1-10) | Effort (1-10) | Justification |
| :--- | :--- | :--- | :--- | :--- |
| **Smart Filter Engine** | Quick Wins | 7 | 2 | Fixing URL/local storage state is fundamentally simple client-side engineering but removes immense user frustration daily. |
| **PNR Explanation Assistant** | Quick Wins | 8 | 4 | Building a static dictionary for acronyms and integrating basic ML adds massive UX value with low risk to the transactional core. |
| **Tatkal Queue System** | Major Projects | 10 | 9 | Essential for platform survival and reputation, but demands a massive architectural overhaul of edge networking and DB locking mechanisms. |
| **Mobile First Flow** | Major Projects | 9 | 8 | Over 80% usage is mobile. A full UI rewrite takes time but defines the next decade of IRCTC's product growth. |
| **Persistent Seat Selection** | Fill-ins | 6 | 4 | Medium value for a specific cohort (elderly/disabled). Easy to implement via session caches but less critical than system crashes. |
| **Refund Tracking Dashboard** | Fill-ins | 7 | 5 | Requires third-party payment gateway webhook integrations. High impact mostly on customer support rather than booking flow. |

## Final Roadmap

### Phase 1 (30 days) - Core Stabilization & Quick Wins
- **Smart Filter Engine**: Deploy URL query state management for search filters.
- **PNR Explanation Assistant**: Release UI updates explicitly defining PNR terminology (V1 dictionary lookup).
- **Persistent Seat Selection**: Introduce local-storage draft saving for booking forms.

### Phase 2 (60 days) - Revenue & Anxiety Reduction
- **Refund Tracking Dashboard**: Overhaul the 'Cancelled Tickets' view. Integrate payment gateway APIs to show step-by-step UI tracking.
- **Tatkal Queue System (Beta)**: Roll out the virtual waiting room infrastructure specifically on 1 highly trafficked zone (e.g., Northern Railways) as a proof of concept.

### Phase 3 (90 days) - Transformation & AI
- **Tatkal Queue System (Global)**: Enforce queueing across all nodes at 10 AM.
- **Mobile First Booking Flow**: Launch the revamped Mobile Web UI SPA.
- **AI Travel Assistant (Alpha)**: Introduce the NLP chat interface and Waitlist Prediction models for select users.