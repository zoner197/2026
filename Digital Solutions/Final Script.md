# Introduction
## Scope
Senior students face immense exam pressure but lack objective feedback on mental fatigue. Relying on their subjective feelings causes overworking, burnout, and decline in work quality. FocusED aims to fix this.

## Constraints
Constraints demand a wearable solution. The Apple Watch Series 10 was chosen for its sensor access and popularity. This implies the app caters to a small screen, runs on watchOS. The app must be completed within four weeks of development.

# Existing Solutions
## Time for Productivity
### Pros
Time for Productivity integrates Pomodoro timers and to-do lists in a minimal UI, helping users prioritise tasks. Furthermore, the app features short and long-term progress graphs.

### Cons
The main problem is the lack of real-time feedback, blinding users to their mental state when they need the information most. Graphs displayed after sessions require manual interpretation, and this limitation combined with the fragmented and overloaded UI increases cognitive load and lacks appeal for senior students.

## Stress Monitor for Watch
### Pros
Stress Monitor for Watch uses watch sensors for real-time feedback, saving time by avoiding manual logging. Daily and weekly graphs with glanceable colour indicators are also provided in the minimal UI.

### Cons
On the downside, the app relies on generic average thresholds which introduce inaccuracy considering exercise and sleep factors. Lacking an academic context, the app fails to provide a comprehensive analysis of data, actionable next steps, and also risks false reassurance.

# Requirements
After exploring aforementioned existing solutions, a comprehensive list of requirements were identified for FocusED.

## Features
The app features a 25-minute standard Pomodoro timer incorporating glanceable progress and controls. Real-time cognitive load is displayed in a simple gauge and tracked using raw HRV and BPM data, also provided for advanced users. Adaptive break recommendations prompt users to rest and breathe based on strain, with the option to dismiss.

## Usability Principles
### Accessibility
Apple System Font and high-contrast UIs are used for ADHD affected students, also featuring easy to tap on the move targets and simple diagrams.

### Effectiveness
Biometrics from HealthKit are compared against a 5-day baseline for real-time pattern detection. Weighted variables, including study duration, accurately calculate cognitive load via watchOS background tasks for sampling with screen off.

### Safety
A privacy-first, on-device approach, with non-stimulating colours and supporting text form the core of the application's safety.

### Utility
The user is provided with a weekly trend analysis for self-reflection. Adaptive breaks scale with study time, further eliminating manual decisions for lower cognitive load, alongside one-tap session restarts.

### Learnability
The UI removes the need for onboarding with an intuitive visual hierarchy, familiar gestures, and minimal text.

# UI Components
The core components include a colour-coded radial gauge that displays cognitive load scores (High, Medium, Low), HRV and BPM readings, headers with the time, and a circular glanceable timer. Additionally, the Weekly Trend page includes a simple column graph with a highlighted peak, and the Break Alert features two large buttons for starting or dismissing and some information on sustained strain time and a break length recommendation.

# UX
Let's discuss the user experience in terms of the earlier introduced proto-personas.

## Proto-Personas
### Jeffery
Jeffery struggles with time leakage, so the radial gauge's glanceability prevents distraction by letting him check his status instantly.

### Donald
Donald often confuses desk time with productivity. Objective proof provided by real-time cognitive load gauges ensure he knows when his focus is wavering.

### Bill
Bill views rest as failure and needs adaptive break recommendations with data-driven justifications to mitigate guilt when taking a break.

# Sketches
The Load Level screen uses large, bold text for accessibility and a high-contrast gauge for glanceability, still allowing advanced users to view raw data for utility.

Swiping left reveals the Study Session controls. Highly visible targets such as the large orange pause button ensure safety by preventing accidental taps, while a circular progress ring enhances effectiveness.

Swiping again leads the user to the Weekly Trend screen with a familiar column graph for learnability and text-based correlation for effective self-regulation.

Automatically displayed after 60 minutes of high strain or accessed by swiping left is the Break Alert screen, which offers a binary "Start Rest" or "Dismiss" choice to reduce decision fatigue and increase usability.

# Algorithms
## Timer
The timer manages sessions by decrementing a 25 minute `DEFAULT_TIME` while running, handling start, pause, and reset states.

## Categorisation
Live HealthKit data is compared against a 5-day average baseline. If HRV drops 20% below baseline while BPM spikes 20% above, load is categorised as "HIGH." If only one deviates, it returns "MED" (medium), and defaults "LOW" if both are normal.

## Adaptive Break
If high cognitive load is sustained for 60 minutes, a break is recommended based on half the study duration, capped at 60 minutes for practicality.

## Weekly Spike Identification
A search algorithm identifies the highest weekly stress value for column graph.

## Why these algorithms are the best approach
These algorithms eliminate subjective bias with personal baselines instead of generic averages, provide hard-to-ignore objective justification for breaks, and use simple arithmetic to ensure long battery life despite on-device data collection and analysis.

# Programming Development Tools
This application is developed using Xcode and Swift, making use of the SwiftUI framework for fast UI. HealthKit is used for biometrics and watchOS background tasks ensure persistent data sampling with the screen turned off.

# Prototype Demo
Here's a demo of the low-fidelity prototype.
(video)
# Evaluation
## Proto-Persona Analysis
Let's take a look at the proto-personas and how the application benefits them.

### Jeffery
Sub-one-second glanceability mitigates distractions

### Donald
Objective categorization prevents hours wasted on low-quality work.

### Bill
Data-driven break justifications challenge his "push-through" mindset, while the study session timer chunks his workflow.

## Impacts
It's also worth analysing FocusED's general impacts, starting with personal aspects.

### Personal
- Students see objective data regarding their stress (`cognitiveLoadScore`), reducing guilt associated with taking breaks.
- Following the `recommendedBreak` algorithm prevents users from long-term cognitive fatigue, which is common during senior exam blocks.

### Social
Socially,
- Wellbeing can be normalised by promoting a culture where monitoring mental health is as common as checking a timetable.
- Data-driven justification for rest can play part in reducing the "push through it" culture encouraged during high school.

### Economic
And economically,
- Students can study more effectively in earlier years and achieve higher results, potentially increasing their long-term career opportunities.
- Economic burden on the healthcare system related to stress-related disorders can be reduced with proactive stress management in teenagers.

# Recommendations for Improvement
- Improvement: Dynamic Baseline Window
- Justification: Student stress levels fluctuate between exam times and holidays, making the static 5-day average baseline calculation improvable.
- Refinement: The app can adapt to changes in the student's environment with a "Weighted Moving Average," which would also prevent false "High" stress alerts after a single all-nighter for users like Bill.

# Future Considerations
- Recommendation: Calendar Integration
- Justification: Referring to the Donald persona, stress is tied to deadlines rather than randomness.
- Refinement: Depending on events from the Calendar, thresholds for rest recommendations could dynamically be lowered. This proactively protects the student even before stress spikes.

# UX and Usability
By avoiding traditional manual journaling, FocusED eliminates administrative fatigue, increasing safety and effectiveness. Standard circular gauges, simple charts, and native fonts guarantee instant learnability.

# Finisher
FocusED successfully and effectively reduces senior secondary stress with the transformation of the Apple Watch into a proactive, "just works" tool. The app achieves direct mitigation of distractions for students like Jeffery, the productivity issues of Donald, and "push through" mindset of Bill.

To finalise, FocusED meets all criteria and its design purpose of providing a data-driven focus app that ensures academic success of its users without the expense of wellbeing.

# References
Focus - Time for Productivity (v5.2). (2024). [Mobile app]. Apple App Store. [https://apps.apple.com/app/focus-time-for-productivity](https://www.google.com/search?q=https://apps.apple.com/app/focus-time-for-productivity)

Stress Monitor for Watch (v2.1). (2023). [Mobile app]. Apple App Store. [https://apps.apple.com/app/stress-monitor-for-watch](https://www.google.com/search?q=https://apps.apple.com/app/stress-monitor-for-watch)
