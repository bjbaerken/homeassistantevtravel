VERSION: v2.6.2<br>

───────────────<br>
REQUIRED<br>
───────────────<br>
• Calendar entity with location-based events<br>
• Person entity (home location)<br>
• Google Travel Time integration (via input_text)<br>

───────────────<br>
OPTIONAL MODULES<br>
───────────────<br>

Travel Assistant:<br>
• input_boolean.not_returning_home → Skip return trip calculation<br>

Preconditioning:<br>
• input_datetime.ev_preheat_time → Stores calculated preheat start time<br>

EV & Charging:<br>
• Battery SOC sensor (percentage)<br>
• Range sensor (in km or miles)<br>
• Miles option will be built in later version<br>
• Target SOC number helper (used by EV Smart Charge)<br>

───────────────<br>
HOW IT WORKS<br>
───────────────<br>

1. Reads all calendar events with a location for the next day<br>
2. Calculates driving time + distance using Google Travel Time<br>
3. Automatically creates "Travel" events in your calendar (before each appointment)<br>
4. Plans total distance including optional return trip home<br>
5. Calculates smart target SOC with configurable safety buffer<br>
6. Sets target SOC for your EV Smart Charge integration<br>
7. Calculates preconditioning start time (first travel block start – buffer)<br>
8. Sends notification with summary & charging recommendations<br>

───────────────<br>
EXAMPLE WORKFLOW<br>
───────────────<br>

Meeting at 09:00 (location: Work)<br>
→ Calculates 30min travel time<br>
→ Creates Travel event: 08:00–09:00<br>
→ Preconditioning (20min buffer): starts at 07:40<br>
→ Google uses 60min earlier departure for traffic accuracy (first trip only)<br>

───────────────<br>
KEY FEATURES<br>
───────────────<br>

• Smart Zone Matching: "home"/"thuis" → zone.home | "werk"/"office"/"kantoor" → zone.werk<br>
• Traffic-Aware Timing: First trip uses 60 minutes earlier departure for Google API (subsequent trips use previous event end time)<br>
• Preconditioning Alignment: Preheat starts at (first travel block start – buffer) so your car is ready exactly when needed<br>
• Configurable Execution Time: Set daily run time (default 14:30 for next-day planning)<br>
• Supports km only<br>
• All modules outside Core Settings are fully optional<br>

───────────────<br>
TIPS & BEST PRACTICES<br>
───────────────<br>

• Works best with Google Calendar + Google Travel Time integration<br>
• waze will be tested in the future (because it does not worjk in my HA) 
• Pair with EV Smart Charge blueprint for automatic charging optimization<br>
• Use input_boolean.not_returning_home to skip return trip on specific days<br>
• Adjust safety buffer % based on your charging preferences (default 15%)<br>
• Monitor preconditioning times via your preheat input_datetime entity<br>
