VERSION: v2.6.2

───────────────
REQUIRED
───────────────
• Calendar entity with location-based events
• Person entity (home location)
• Google Travel Time integration (via input_text)

───────────────
OPTIONAL MODULES
───────────────

Travel Assistant:
• input_boolean.not_returning_home → Skip return trip calculation

Preconditioning:
• input_datetime.ev_preheat_time → Stores calculated preheat start time

EV & Charging:
• Battery SOC sensor (percentage)
• Range sensor (in km or miles)
• Miles option will be built in later version
• Target SOC number helper (used by EV Smart Charge)

───────────────
HOW IT WORKS
───────────────

1. Reads all calendar events with a location for the next day
2. Calculates driving time + distance using Google Travel Time
3. Automatically creates "Travel" events in your calendar (before each appointment)
4. Plans total distance including optional return trip home
5. Calculates smart target SOC with configurable safety buffer
6. Sets target SOC for your EV Smart Charge integration
7. Calculates preconditioning start time (first travel block start – buffer)
8. Sends notification with summary & charging recommendations

───────────────
EXAMPLE WORKFLOW
───────────────

Meeting at 09:00 (location: Work)
→ Calculates 30min travel time
→ Creates Travel event: 08:00–09:00
→ Preconditioning (20min buffer): starts at 07:40
→ Google uses 60min earlier departure for traffic accuracy (first trip only)

───────────────
KEY FEATURES
───────────────

• Smart Zone Matching: "home"/"thuis" → zone.home | "werk"/"office"/"kantoor" → zone.werk
• Traffic-Aware Timing: First trip uses 60 minutes earlier departure for Google API (subsequent trips use previous event end time)
• Preconditioning Alignment: Preheat starts at (first travel block start – buffer) so your car is ready exactly when needed
• Configurable Execution Time: Set daily run time (default 14:30 for next-day planning)
• Supports km only
• All modules outside Core Settings are fully optional

───────────────
TIPS & BEST PRACTICES
───────────────

• Works best with Google Calendar + Google Travel Time integration
• waze will be tested in the future (because it does not worjk in my HA) 
• Pair with EV Smart Charge blueprint for automatic charging optimization
• Use input_boolean.not_returning_home to skip return trip on specific days
• Adjust safety buffer % based on your charging preferences (default 15%)
• Monitor preconditioning times via your preheat input_datetime entity
