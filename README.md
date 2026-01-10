# Reaction-Time-Challenge-PLC-Structured-Text-
Reaction Time Challenge (PLC Structured Text)A reaction speed measurement game developed using Structured Text (ST) for PLC/HMI systems. The logic uses a multi-timer and multi-counter approach to calculate high-precision results with a "snapshot" display feature.

🕹️ How the Game WorksSystem Initialization: 

The game is powered on via GAMEONBUTTON.

The Countdown: Before the game starts, the system calculates a variable delay (WILLCOUNT) using two background timers. This ensures the "Green Light" timing is different each time.The Trigger: When GAMESTART is activated, the system waits for the calculated duration. Once reached, the "Green Light" (T2) turns on.

Measurement: As soon as the light is on, three parallel timers (1s, 0.1s, and 0.01s) begin tracking your reaction time.Result Capture: When the user hits the SHOWBUTTON, the counters are frozen. The system instantly calculates the final score using the formula:
$Result = (Counter_{Sec} \times 1.0) + (Counter_{Deci} \times 0.1) + (Counter_{Centi} \times 0.01)$

Grading:
CONGRATS: Reaction time < 1.0 second.
NOT BAD: Reaction time between 1.0 and 9.0 seconds.
TRY AGAIN: Failed to press in time or pressed too early.


🛠️ Logic Breakdown

Time Decomposition Strategy
Instead of using a single complex clock, this project utilizes three synchronized Timer-Counter pairs to break down time into Seconds, Tenths, and Hundredths. 
Example of the calculation logic:

- SHOWCOUNT := (TO_REAL(CT3) + (TO_REAL(CT4) * 0.1) + (TO_REAL(CT5) * 0.01));
- FeaturesEarly Press Detection: Includes logic to detect if the user cheated by pressing the button before the light turned green.
- Automatic Reset: A CLEAR function to reset all counters and timers for a new round.
- State Management: Uses Boolean interlocks to ensure the game flows correctly from Power On -> Start -> Measure -> Show.

🚀 How to Use

- Import the provided Structured Text into your PLC environment (TIA Portal, CODESYS, Schneider Machine Expert, etc.).
- Map the global variables (GAMEONBUTTON, STARTBUTTON, SHOWBUTTON) to your HMI or physical push buttons.
- Monitor the SHOWCOUNT variable to see the reaction speed on your display.

📺 Logic Demonstration & HMI Interaction 🛠️


https://github.com/user-attachments/assets/b9e60014-797f-44ae-b16c-a077f161e5ca




