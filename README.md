## Simulating Patient Heart Rate Monitoring

This notebook simulates continuous heart rate (HR) monitoring, like the data a wearable or bedside monitor would collect. It builds from simple threshold alerts to context-aware detection of **POTS (Postural Orthostatic Tachycardia Syndrome)**, a condition in which heart rate rises excessively when a person stands up.

All data is **synthetically generated** with Python's `random` module. No real patient data is used.

### What the notebook covers

**1. Basic monitoring (8 hours, 1 reading per minute)**
- Generates random HR readings between 55 and 110 bpm
- Flags any reading outside the normal resting range of 60–100 bpm
- Reports the total number of abnormal readings and the percentage of time spent abnormal

**2. POTS simulation**
- The patient stands up once every hour, which produces a higher HR range (75–130 bpm)
- A standing reading above 100 bpm is flagged as a possible POTS episode

**3. Organizing results with pandas**
- Stores each minute's reading in a DataFrame with columns `Minute`, `HeartRate`, `Event` (Normal or Standing), `Abnormal` and `SuspectedPOTS`

**4. Personalized POTS detection (14 days)**
Replaces the fixed 100 bpm cutoff with a more clinically realistic rule:
- **Personal baseline:** a rolling 7-day mean of the patient's non-standing HR
- **Relative rise:** a standing HR at least **30 bpm above baseline** counts as POTS-like
- **Persistence:** a day is flagged only if at least 5 standing readings meet that rule
- **Context:** each day randomly includes coffee, a workout or poor sleep, which shift HR. Workout days are excluded from POTS flagging to avoid false alarms.

**5. Clinical scenario: caffeine, poor sleep and anxiety (24 hours)**
Models one realistic day for a single patient:
- Lower HR during sleep (2:00–6:00 AM)
- Morning coffee (+8 bpm for 2 hours) and poor sleep (+5 bpm while awake)
- Two short exercise bursts (110–150 bpm)
- Random stress or anxiety spikes (a 3% chance each minute, +25 bpm for 3 minutes)

This shows how lifestyle factors, not only disease, can produce "abnormal" heart rates, and why monitoring systems need context to avoid false alerts.

### Example output
Results change on every run because readings are random. One run of the 24-hour scenario produced 248 abnormal readings (17.2% of the day), 35 stress spikes and 2 exercise events.

### Key takeaways
- Fixed thresholds (such as HR > 100) are simple but produce many false alarms
- Personal baselines and relative changes are closer to how POTS is actually defined clinically
- Context data (caffeine, sleep, exercise, stress) is essential for interpreting wearable HR data

### Tech stack
Python · `random` · pandas 

### How to run
Open the notebook in Google Colab using the badge at the top and run the cells in order. No data files are needed.
