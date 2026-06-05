# Flagship AI Feature: IRCTC AI Travel Assistant

## Problem Statement
Booking a multi-leg journey, figuring out the probability of a waitlisted ticket confirming, or quickly finding alternative transport when trains are full requires immense cognitive effort, manual searching, and dependency on third-party apps.

## Why AI is Needed
IRCTC possesses massive amounts of historical travel data. Rule-based systems cannot handle the edge cases of user inquiries (e.g., "Find me the fastest way to reach Kerala if direct trains are booked"). LLMs and ML can process historical data to predict waitlist outcomes and use NLP to construct complex, multi-modal itineraries seamlessly.

## User Flow
1. User enters destination and taps a "Plan with AI" glowing icon.
2. User types/speaks: *"I need to reach Bangalore from Delhi by tomorrow evening. Direct trains are waitlisted."*
3. AI Assistant processes the prompt.
4. AI outputs a card: "Direct: 40% chance of confirmation. AI Alternative Flight + Train combo: Flight DEL->BOM, Train BOM->SBC. Tap to book combo."
5. User selects the alternative and system adds all tickets to cart.

## AI Inputs
- Natural Language Prompt (Text/Voice)
- User's travel history & age (for berth preferences)
- Live IRCTC DB (Train API, alternative quotas)
- Historical confirmation logs
- Third-party API (Flights/Buses via IRCTC Tourism portal)

## AI Outputs
- Waitlist Confirmation % Probability (e.g., "75% chance").
- Plain English explanations of status.
- Alternative routing ("Split Booking" recommendations).
- Pre-filled forms.

## Architecture Diagram (ASCII)
```
[ User UI ] <--> [ NLP API Gateway ]
                      |
                      v
             [ Orchestration Layer (LangChain) ]
                /             |              \
               v              v               v
    [ IRCTC Live DB]   [ ML Prediction ]  [ LLM (Gemini/OpenAI) ]
     (Seat Avail)       (Waitlist %)       (Natural Language)
```

## LLM Usage
We will utilize a specialized, fine-tuned LLM instructed purely on Indian Railway routing and IRCTC policies. It acts as an orchestrator, converting natural language to API parameters and transforming the JSON API response back into conversational, accessible UI components.

## NLP Features
- Voice-to-text booking for rural accessibility.
- Multilingual intent recognition (Hindi, Tamil, Bengali).
- Semantic entity extraction (Date, Origin, Destination, Class).

## Recommendation Engine
Recommends Vikalp (Alternate Train Accommodation System) with high precision by analyzing which alternate trains have actual availability rather than blindly opting users in.

## Waitlist Prediction
Uses XGBoost trained on 5 years of historical IRCTC PNR data (Train Number, Date, Quota, Current WL number) to output realistic confirmation percentages.

## Refund Guidance
"Chat with AI regarding PNR XXXXXX" — The bot instantly queries the payment microservice and explains the refund status explicitly: "Your Rs. 1500 was released to HDFC Bank on Oct 2 at 4PM. It will reflect in your account by Tomorrow 5PM."

## PNR Explanation
Translates `RLWL/45` into "Remote Location Waitlist. You are 45th in line. Based on history, there is a 20% chance this will get confirmed. Consider our alternative route option."

## Benefits
- Drastically reduces customer support queries.
- Recaptures revenue lost to competitors (MakeMyTrip, Ixigo).
- Makes the app highly accessible.

## Risks
- Hallucination (recommending non-existent trains).
- High latency during NLP processing.
- Increased cloud cost for LLM tokens.

## Mitigation Strategies
- **Strict Grounding:** The LLM does NOT generate data; it only formats data returned by the deterministic IRCTC APIs (RAG architecture).
- **Edge ML:** Use lightweight models for waitlist prediction to keep latency < 200ms.
- **Caching:** Cache common queries (e.g., "Trains to Mumbai tomorrow") heavily.

## KPIs
- AI Booking Conversion Rate (% of AI conversations ending in ticketing).
- User query dwell time (aiming for reduction).
- Prediction Accuracy (>85% matching reality).