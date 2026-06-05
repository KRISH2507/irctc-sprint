# 5-Minute Presentation Script

**[Slide 1: Title Screen]**
**[0:00 - 0:30] Introduction**
"Hello everyone, I’m excited to act as a hybrid Product Manager and Design Engineer today to walk you through our recent sprint: Fixing IRCTC Before It Crashes. IRCTC handles millions of people moving across India daily, but the digital experience is currently fraught with anxiety. Our mission was to strip away the jargon, eliminate the crashes, and bring intelligence into the booking flow."

**[Slide 2: Research Methodology]**
**[0:30 - 1:00] Research Process**
"To do this, we didn't just guess. We mapped the exact technical triggers causing UX failures. By conducting cognitive walkthroughs and simulating peak loads, we identified where the backend infrastructure was failing the frontend UI, leading to the crashes and frustration we all know too well."

**[Slide 3: Overview of 6 Problems]**
**[1:00 - 2:00] Top 6 Problems**
"We documented six major flaws. Three provided to us: the notorious 10 AM Tatkal crashes, the broken search filters, and the seat selections resetting. But we also discovered three more on our own: opaque refund tracking that just says 'Processing', incredibly confusing PNR jargon like 'RLWL', and a mobile flow that feels like a shrunken desktop site causing infinite scrolling."

**[Slide 4: Deep Dive]**
**[2:00 - 3:00] Deep Dive into one self-discovered problem**
"Let’s deep dive into the Refund Tracking issue. Currently, when you cancel a ticket, the UI simply says 'Processing'. It stays that way for days. From an engineering standpoint, this happens because IRCTC fires off the refund to a payment gateway but doesn't surface the gateway's webhook responses to the user. From a product perspective, the impact is massive anxiety and flooded customer support lines. Users are left completely in the dark on their own money."

**[Slide 5: Proposed Solution Matrix]**
**[3:00 - 3:45] Proposed Solution**
"The solution? We engineered a Real-time Refund Dashboard. By pulling data from payment webhooks into our API gateway, we can now show users a step-by-step timeline—just like tracking an Amazon package. 
We prioritized all these solutions on an Impact vs Effort Matrix. Fixing filters and PNR acronyms are our 'Quick Wins' for Phase 1. The massive Queue Management system to solve Tatkal crashes is our Phase 3 'Major Project'."

**[Slide 6: The AI Edge]**
**[3:45 - 4:40] AI Feature**
"But to truly future-proof IRCTC, we need to move from a static portal to an intelligent partner. Introducing the IRCTC AI Travel Assistant. If your train is waitlisted, you no longer have to guess. Our trained ML prediction engine spits out a '75% chance of confirmation'. Better yet, using Natural Language Processing, it can act on prompts like 'Get me to Mumbai by tomorrow.' It will comb the database, skip the full direct trains, and stitch together a train-flight combo for you instantly. By wrapping the complex DB with an LLM orchestration layer, we keep hallucinations to zero while providing a radically personalized experience."

**[Slide 7: Conclusion]**
**[4:40 - 5:00] Conclusion**
"By bridging scalable design engineering with actionable AI, we can transform IRCTC from a frustrating monopoly into a world-class travel platform. Thank you."