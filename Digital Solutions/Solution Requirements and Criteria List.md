# Solution Requirements
## Functional Requirements
### Data collection
- Collect heart rate and HRV from Apple Watch sensors
- Track study session duration
- Record optimal manual focus rating
- Access sleep duration from Health data
- Detect inactivity vs movement to filter physical stress

### Data processing
- Calculate Cognitive Load Score using weighted variables
- Compare current values with baseline
- Detect sustained high cognitive load
- Identify stress spikes unrelated to movement
- Adjust recommendations based on time of day and study duration

### Feedback and output
- Display realtime cognitive load
- Categorize load into low/moderate/high
- Provide adaptive break recommendations
- Display daily and weekly trend summaries
- Limit notifications to prevent overload

## Non-functional Requirements
### Performance
- Focus status must load within 3 seconds
- Calculations must run in background without noticeable lag
- App must not reduce battery life by more than 10% per day in background

### Reliability
- Sensor data must be handled safely if missing
- System must function offline
- Data must sync automatically when internet is available

### Privacy and security
- All data stored locally
- No third-party
- Clear explanation of data usage

### Usability
- Learnable within 2 minutes
- Core state readable within 1 second/in a glance
- Manual input must take >5 seconds
- No more than `N` notifications per day -> `N` given by user

## UX Requirements (Didn't know which category this went in)
- Reduce cognitive overload
- Avoid anxiety induction
- Provide actionable guidance
- Adapt to individual patterns
- Support academic pressures

# Mind Map
[[Student Focus and Wellbeing Companion App WIP PART 1.png]]