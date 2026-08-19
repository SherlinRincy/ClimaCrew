<!-- SPEC.md

ClimateGuard Traffic — Climate-Adaptive Traffic Signal & Human Exposure Reduction Platform

> Document status: Implementation-ready specification
Role: Single source of truth for implementation
Primary objective: Reduce avoidable climate exposure of people waiting at road intersections, with two-wheeler riders and pedestrians as the primary road-user focus.
Prototype safety rule: The system simulates signal changes and does not directly control real public traffic signals.




---

1. PROJECT VISION

ClimateGuard Traffic is an AI-assisted, climate-adaptive traffic management platform that combines real-time climate conditions with traffic and human-density information to identify where road users are experiencing the greatest climate exposure and recommend safe traffic-signal adjustments to reduce that exposure.

The system is intentionally climate-first, not traffic-first.

The primary question is:

> "Which group of people is currently experiencing the highest climate exposure at this intersection, why, and can we safely reduce their waiting time?"



The system considers:

temperature;

apparent/feels-like temperature;

rainfall;

visibility;

wet-road conditions;

traffic density;

two-wheeler density;

pedestrian density;

waiting time;

queue length;

current signal phase;

road conditions.


The system produces:

1. a Climate Exposure Score;


2. an exposure score for each intersection approach;


3. the major factors causing the exposure;


4. a safe adaptive signal recommendation;


5. predicted before/after exposure;


6. analytics showing the reduction in exposure.




---

2. PROBLEM STATEMENT

Extreme heat and heavy rainfall increasingly affect urban mobility and the safety and comfort of people waiting at traffic intersections.

Conventional traffic signals generally optimize traffic flow using:

fixed timing;

vehicle density;

historical traffic patterns;

basic adaptive traffic rules.


They generally do not explicitly model human exposure to hazardous outdoor climate conditions.

This creates a specific problem:

Extreme climate
       +
People waiting
       +
Long signal cycle
       =
Unnecessary climate exposure

The problem is particularly important for:

Primary users

two-wheeler riders;

pedestrians;

other road users.


Two-wheeler riders and pedestrians are directly exposed to outdoor conditions instead of being protected by an enclosed vehicle.

During extreme heat:

High temperature
      +
High feels-like temperature
      +
Long waiting time
      +
High 2W/P density
      ↓
High climate exposure

During heavy rainfall:

Rain
+
Poor visibility
+
Wet roads
+
Long waiting
      ↓
Higher exposure + increased road risk

ClimateGuard Traffic attempts to reduce this exposure through safe, explainable, adaptive signal recommendations.


---

3. PRIMARY DIFFERENTIATOR

The project is not:

> "Another AI traffic signal system."



The project is:

> "A climate-aware traffic management system that measures the outdoor climate exposure of road users—especially two-wheeler riders and pedestrians—and safely adapts signal timing to reduce avoidable exposure."



The architecture must therefore preserve this priority:

CLIMATE CONDITIONS
        ↓
HUMAN EXPOSURE
        ↓
TWO-WHEELERS + PEDESTRIANS
        ↓
WAITING TIME
        ↓
CLIMATE EXPOSURE SCORE
        ↓
SAFE SIGNAL OPTIMIZATION
        ↓
LOWER EXPOSURE


---

4. TARGET USERS

4.1 Primary road users

Two-wheeler riders

The system separately tracks:

number waiting;

average waiting time;

queue position;

climate hazard;

exposure score.


Pedestrians

The system separately tracks:

number waiting;

average waiting time;

crossing state;

climate hazard;

exposure score.


Other road users

Includes:

cars;

buses;

trucks;

other vehicles.


They remain part of traffic optimization but are not the primary climate-exposure focus.


---

5. SECONDARY USERS

Traffic control operator

Can:

view intersection conditions;

view climate exposure;

inspect individual approaches;

generate recommendations;

accept/reject simulated recommendations;

view analytics.


Traffic police

Can:

monitor high-exposure conditions;

view alerts;

inspect current signal state;

use recommendations as decision support.


Municipal/transport authority

Can:

monitor historical exposure;

compare intersections;

configure thresholds;

evaluate climate-adaptive traffic performance.


Administrator

Can:

manage users;

manage intersections;

configure thresholds;

configure system settings.



---

6. GOALS

MVP goals

The MVP MUST:

1. provide authentication;


2. display a live intersection dashboard;


3. display weather conditions;


4. display traffic density;


5. separately display two-wheeler density;


6. separately display pedestrian density;


7. display waiting times;


8. calculate Climate Exposure Score;


9. calculate exposure for each approach;


10. classify exposure risk;


11. identify dominant exposure factors;


12. generate safe signal-timing recommendations;


13. simulate recommended signal changes;


14. show before/after exposure;


15. show alerts;


16. show historical exposure analytics;


17. support heatwave simulation;


18. support heavy-rain simulation;


19. support high-two-wheeler-density simulation;


20. support high-pedestrian-density simulation.




---

7. NON-GOALS

The MVP will NOT:

1. directly control public traffic signals;


2. replace traffic police;


3. provide medical advice;


4. claim to diagnose heat-related illness;


5. guarantee prevention of health effects;


6. use an LLM as the direct signal controller;


7. override mandatory traffic-safety rules;


8. optimize only for vehicle throughput;


9. treat simulated data as real-world measurements;


10. make uncontrolled changes to real traffic infrastructure.




---

8. COMPLETE SYSTEM FLOW

flowchart TD

    A[Weather Conditions]
    B[Traffic Density]
    C[Two-Wheeler Density]
    D[Pedestrian Density]
    E[Waiting Time]
    F[Queue Length]
    G[Road Condition]
    H[Current Signal State]

    A --> I[Data Normalization]
    B --> I
    C --> I
    D --> I
    E --> I
    F --> I
    G --> I
    H --> I

    I --> J[Climate Exposure Engine]

    J --> K[Heat Risk]
    J --> L[Rain Risk]
    J --> M[Visibility Risk]
    J --> N[Wet Road Risk]
    J --> O[Human Exposure]
    J --> P[Waiting Exposure]

    K --> Q[Climate Exposure Score]
    L --> Q
    M --> Q
    N --> Q
    O --> Q
    P --> Q

    Q --> R[Risk Classification]

    R --> S[Adaptive Signal Optimizer]

    S --> T[Generate Candidate Timings]

    T --> U[Safety Validator]

    U -->|Unsafe| V[Reject Candidate]

    U -->|Safe| W[Impact Simulation]

    W --> X[Compare Before vs After]

    X --> Y[Recommendation]

    Y --> Z[Operator Dashboard]

    Z --> AA{Operator Decision}

    AA -->|Accept| AB[Apply to Traffic Simulator]

    AA -->|Reject| AC[Keep Existing Timing]

    AB --> AD[Recalculate Exposure]

    AD --> Z


---

9. COMPLETE WEBSITE USER FLOW

flowchart TD

    START([User opens website])
    START --> LOGIN[Login]

    LOGIN --> AUTH{Valid credentials?}

    AUTH -->|No| ERROR[Show login error]
    ERROR --> LOGIN

    AUTH -->|Yes| DASH[Dashboard]

    DASH --> SELECT[Select Intersection]

    SELECT --> LOAD[Load Current Intersection State]

    LOAD --> WEATHER[Weather]
    LOAD --> TRAFFIC[Traffic]
    LOAD --> PEOPLE[2W + Pedestrian Density]
    LOAD --> SIGNAL[Signal State]
    LOAD --> ROAD[Road Condition]

    WEATHER --> ENGINE[Climate Exposure Engine]
    TRAFFIC --> ENGINE
    PEOPLE --> ENGINE
    SIGNAL --> ENGINE
    ROAD --> ENGINE

    ENGINE --> SCORE[Exposure Score]

    SCORE --> RISK{Risk}

    RISK -->|Low| NORMAL[Maintain current timing]
    RISK -->|Moderate| OPT[Generate recommendation]
    RISK -->|High| OPT
    RISK -->|Critical| PRIORITY[Prioritize exposure reduction]

    PRIORITY --> OPT

    OPT --> SAFETY[Safety Validation]

    SAFETY -->|Unsafe| REJECT[Reject candidate]
    REJECT --> OPT

    SAFETY -->|Safe| SIM[Simulate timing]

    SIM --> COMPARE[Before vs After]

    COMPARE --> REVIEW[Operator Review]

    REVIEW -->|Accept| APPLY[Apply to simulator]
    REVIEW -->|Reject| KEEP[Keep existing timing]

    APPLY --> RECALC[Recalculate exposure]
    RECALC --> DASH

    KEEP --> DASH
    NORMAL --> DASH


---

10. CORE INPUTS

The system receives seven major categories of information.

10.1 Climate

temperature
feelsLikeTemperature
humidity
rainfall
visibility
wind
weatherCondition

10.2 Traffic

vehicleCount
averageSpeed
queueLength
averageWait

10.3 Two-wheelers

twoWheelerCount
twoWheelerAverageWait
twoWheelerQueue

10.4 Pedestrians

pedestrianCount
pedestrianAverageWait
crossingDemand

10.5 Road

wetRoad
roadCondition
visibility

10.6 Signal

currentPhase
currentGreenDuration
remainingGreen
remainingRed
yellowDuration
allRedDuration

10.7 Time

timestamp
hour
dayOfWeek


---

11. DATA FLOW

┌───────────────────┐
             │     WEATHER       │
             │ Temperature       │
             │ Rain              │
             │ Visibility        │
             └─────────┬─────────┘
                       │
                       ▼
┌──────────────┐  ┌────────────────────┐  ┌──────────────┐
│ TRAFFIC      │  │                    │  │ ROAD         │
│ Cars         ├─►│  DATA NORMALIZER   │◄─┤ Wetness      │
│ 2-Wheelers   │  │                    │  │ Condition    │
│ Trucks       │  └─────────┬──────────┘  └──────────────┘
└──────────────┘            │
                            ▼
                  ┌────────────────────┐
                  │ EXPOSURE ENGINE    │
                  └─────────┬──────────┘
                            │
                            ▼
                  ┌────────────────────┐
                  │ EXPOSURE SCORE     │
                  │ 0 - 100            │
                  └─────────┬──────────┘
                            │
                            ▼
                  ┌────────────────────┐
                  │ SIGNAL OPTIMIZER   │
                  └─────────┬──────────┘
                            │
                            ▼
                  ┌────────────────────┐
                  │ SAFETY VALIDATOR   │
                  └─────────┬──────────┘
                            │
                            ▼
                  ┌────────────────────┐
                  │ DASHBOARD          │
                  └────────────────────┘


---

12. CLIMATE EXPOSURE ENGINE

12.1 Purpose

Convert climate conditions + human presence + waiting time into a transparent score between 0 and 100.


---

12.2 Climate hazard

Calculate:

heatRisk
rainRisk
visibilityRisk
wetRoadRisk

Each is normalized between:

0.0 → no/low risk
1.0 → maximum configured risk


---

13. HEAT RISK

The prototype uses configured thresholds.

Example:

Temperature < configured lower threshold
    → low heat risk

Temperature between lower and upper threshold
    → proportional risk

Temperature >= upper threshold
    → high heat risk

The implementation must use configuration rather than hard-code medical claims.

Input:

{
  "temperatureC": 39,
  "feelsLikeC": 43
}

The higher relevant heat indicator should be used according to configured rules.


---

14. RAIN RISK

Input:

rainfallMmPerHour

Rainfall is normalized according to configurable bands.

The system must also consider:

visibility
wetRoad

because rainfall alone does not fully represent road risk.


---

15. VISIBILITY RISK

Lower visibility produces higher risk.

Example:

High visibility → low risk
Moderate visibility → moderate risk
Poor visibility → high risk


---

16. WET-ROAD RISK

Input:

wetRoad = true / false

If:

rainfall > threshold

the system may infer wet-road conditions if configured.

If actual road-condition data exists, it takes priority.


---

17. CLIMATE HAZARD FORMULA

Default configurable weights:

heat = 0.45
rain = 0.30
visibility = 0.15
wetRoad = 0.10

Formula:

climateHazard =
    0.45 * heatRisk +
    0.30 * rainRisk +
    0.15 * visibilityRisk +
    0.10 * wetRoadRisk

All weights must sum to 1.0.


---

18. ROAD-USER EXPOSURE

The system must not combine all vehicles into a single number.

Track separately:

twoWheelers
pedestrians
cars
heavyVehicles
otherVehicles

Default prototype weights:

twoWheelerWeight = 1.00
pedestrianWeight = 1.00
carWeight = 0.25
heavyVehicleWeight = 0.35
otherVehicleWeight = 0.30

These are configurable prototype weights, not scientific claims.


---

19. HUMAN EXPOSURE FORMULA

personExposure =
    twoWheelerCount * twoWheelerWeight
    +
    pedestrianCount * pedestrianWeight
    +
    carCount * carWeight
    +
    heavyVehicleCount * heavyVehicleWeight
    +
    otherVehicleCount * otherVehicleWeight


---

20. WAITING FACTOR

For an approach:

waitingFactor =
    currentAverageWaitSeconds / targetWaitSeconds

Clamp:

0 → 2

Then normalize:

normalizedWaitingFactor =
    clamp(waitingFactor, 0, 2) / 2


---

21. DENSITY FACTOR

densityFactor =
    clamp(
        personExposure / capacityReference,
        0,
        1
    )

capacityReference must be configurable per intersection/approach.


---

22. FINAL EXPOSURE SCORE

exposureScore =
    clamp(
        100
        *
        climateHazard
        *
        (0.5 + 0.5 * normalizedWaitingFactor)
        *
        (0.5 + 0.5 * densityFactor),
        0,
        100
    )

The implementation MUST store all intermediate values.

This is required because the dashboard must be able to answer:

> "Why is the exposure score 82?"




---

23. RISK LEVEL

Default configuration:

Score	Risk

0–24	LOW
25–49	MODERATE
50–74	HIGH
75–100	CRITICAL



---

24. APPROACH EXPOSURE

Each approach receives an independent score.

Example:

NORTH
Exposure = 82
Risk = CRITICAL

SOUTH
Exposure = 61
Risk = HIGH

EAST
Exposure = 35
Risk = MODERATE

WEST
Exposure = 27
Risk = MODERATE

The dashboard must make these scores visually obvious.


---

25. PRIMARY KPI

The most important KPI is:

Climate Exposure Reduction

baselineExposure = exposure before recommendation

predictedExposure = exposure after simulated recommendation

reductionPercent =
(
    baselineExposure - predictedExposure
)
/
baselineExposure
× 100

If baseline exposure is 0:

reductionPercent = 0


---

26. SECONDARY KPIs

Display:

Average waiting time
Maximum waiting time
Two-wheeler waiting time
Pedestrian waiting time
Two-wheeler exposure
Pedestrian exposure
Rain exposure
Heat exposure
Queue length
Traffic flow
Signal efficiency


---

27. SIGNAL OPTIMIZATION

Purpose

Find a signal timing adjustment that reduces climate exposure without violating safety constraints or creating unacceptable traffic imbalance.


---

28. OPTIMIZATION PRIORITY

The optimizer follows:

1. Safety
2. Climate exposure reduction
3. Two-wheeler/pedestrian waiting reduction
4. Queue control
5. General traffic efficiency

Safety is always an absolute constraint.


---

29. SIGNAL CANDIDATES

If current green is:

45 seconds

generate:

35
40
45
50
55

seconds.

The range is configurable.


---

30. SAFETY VALIDATION

Every candidate must be checked.

Reject if:

green < minimumGreen

or:

green > maximumGreen

or:

yellow < configured minimum

or:

allRed < configured minimum

or:

pedestrian crossing time < minimum

or:

conflicting approaches become green simultaneously

or any other configured safety constraint fails.


---

31. CANDIDATE SIMULATION

For each safe candidate:

1. Calculate estimated new wait.
2. Calculate estimated new queue.
3. Calculate new two-wheeler wait.
4. Calculate new pedestrian wait.
5. Calculate predicted exposure.
6. Calculate traffic penalty.
7. Calculate queue penalty.
8. Calculate total objective.


---

32. RECOMMENDATION OBJECTIVE

Conceptually:

totalCost =
    exposureCost
    +
    trafficPenalty
    +
    queuePenalty

with:

exposureCost

having the highest configurable weight.


---

33. RECOMMENDATION OUTPUT

Example:

{
  "recommendationId": 17,
  "approach": "NORTH",
  "action": "EXTEND_GREEN",
  "oldGreenSeconds": 45,
  "newGreenSeconds": 55,
  "exposureBefore": 82,
  "exposureAfter": 58,
  "exposureReductionPercent": 29,
  "waitBefore": 54,
  "waitAfter": 39,
  "safetyValid": true,
  "reason": [
    "High heat exposure",
    "High two-wheeler density",
    "High pedestrian density",
    "Long waiting time"
  ]
}


---

34. DASHBOARD DESIGN

The dashboard is the most important page in the project.

It must answer these questions within a few seconds:

1. What is happening?
2. How dangerous is the climate exposure?
3. Who is exposed?
4. Why is exposure high?
5. What does the system recommend?
6. Will the recommendation be safe?
7. What happens after the recommendation?


---

35. DASHBOARD ARCHITECTURE

┌─────────────────────────────────────────────────────────────────────────┐
│ CLIMATEGUARD TRAFFIC     CENTRAL JUNCTION       ● LIVE     14:32        │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│ WEATHER             CLIMATE EXPOSURE             SYSTEM STATUS          │
│ ┌──────────────┐    ┌─────────────────────┐     ┌────────────────────┐ │
│ │ 39°C         │    │                     │     │ ● ONLINE            │ │
│ │ Feels 43°C   │    │       82 / 100      │     │ Data: 5 sec ago     │ │
│ │ Rain 4.5mm/h │    │       CRITICAL      │     │ Engine: ACTIVE      │ │
│ │ Visibility   │    │                     │     │ Signal: SIMULATION  │ │
│ └──────────────┘    └─────────────────────┘     └────────────────────┘ │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                         INTERSECTION SIMULATOR                          │
│                                                                         │
│                              NORTH                                      │
│                         ┌─────────────┐                                  │
│                         │ 2W: 82      │                                  │
│                         │ P : 31      │                                  │
│                         │ WAIT: 54s   │                                  │
│                         └──────┬──────┘                                  │
│                                │                                         │
│        WEST ───────────────────●────────────────── EAST                  │
│                                │                                         │
│                         ┌──────┴──────┐                                  │
│                         │ 2W: 52      │                                  │
│                         │ P : 18      │                                  │
│                         │ WAIT: 38s   │                                  │
│                         └─────────────┘                                  │
│                              SOUTH                                       │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│ APPROACH EXPOSURE                                                       │
│                                                                         │
│ NORTH    ██████████████████ 82  CRITICAL                               │
│ SOUTH    █████████████       61  HIGH                                   │
│ EAST     ███████             35  MODERATE                              │
│ WEST     █████               27  MODERATE                              │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                    ADAPTIVE RECOMMENDATION                              │
│                                                                         │
│ NORTH GREEN: 45s  →  55s                                               │
│                                                                         │
│ WHY?                                                                     │
│ Severe heat + high 2W density + high pedestrian density + long wait     │
│                                                                         │
│ EXPOSURE                    WAITING                                     │
│ 82 → 58                     54s → 39s                                   │
│ 29% REDUCTION               28% REDUCTION                               │
│                                                                         │
│ SAFETY VALIDATION: ✓ SAFE                                               │
│                                                                         │
│ [ ACCEPT & SIMULATE ]     [ REJECT ]     [ VIEW FULL EXPLANATION ]      │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│ ALERTS                 EXPOSURE TREND          SIGNAL TIMELINE            │
│ 🔥 Heat: HIGH          40 55 62 70 82          N RED 45s                 │
│ 🌧 Rain: MODERATE      ───────────────          N GREEN 55s              │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘


---

36. DASHBOARD COMPONENTS

Header

Displays:

project name;

intersection;

live status;

current timestamp;

logged-in operator;

system mode.



---

Weather Card

Displays:

Temperature
Feels-like temperature
Rainfall
Visibility
Humidity
Road condition


---

Climate Exposure Card

Displays:

Overall score
Risk
Change from previous period
Main climate driver

Example:

82 / 100
CRITICAL

↑ 18 points

Main driver:
EXTREME HEAT


---

37. INTERSECTION SIMULATOR

The simulator must show:

North
South
East
West

Each approach displays:

Signal state
Vehicle count
2W count
Pedestrian count
Queue length
Average waiting time
Exposure

The active signal must visually change.


---

38. APPROACH CARDS

Example:

NORTH
────────────────────

Exposure
82 / 100
CRITICAL

Two-wheelers
82

Pedestrians
31

Vehicles
126

Average wait
54 sec

Queue
95 m

[VIEW DETAILS]


---

39. EXPOSURE DETAIL

Clicking an approach must open:

NORTH APPROACH

Climate Exposure
82 / 100

Heat Risk
█████████ 91%

Rain Risk
█████     48%

Visibility Risk
██        20%

Wet Road
████      40%

People Exposed
2W: 82
Pedestrians: 31
Cars: 40

Average Wait
54 seconds

Dominant Factors:
1. Heat
2. Two-wheeler density
3. Pedestrian density
4. Waiting time


---

40. RECOMMENDATION PANEL

The recommendation must never simply say:

AI recommends +10 seconds.

It must say:

WHY
WHAT CHANGES
WHY IT IS SAFE
EXPECTED RESULT

Example:

RECOMMENDATION

Extend NORTH green:
45s → 55s

Reason:
North has the highest climate exposure because of
high heat, high 2W density, pedestrian demand and
long waiting time.

Expected:
Exposure: 82 → 58
Wait: 54s → 39s

Safety:
✓ Minimum green satisfied
✓ Maximum green satisfied
✓ Yellow interval preserved
✓ Pedestrian minimum preserved
✓ No conflicting phase


---

41. BEFORE/AFTER VIEW

This is one of the most important hackathon visuals.

BEFORE             AFTER

Exposure       82                 58
Risk         CRITICAL             HIGH

Wait           54s                39s

2W Wait        HIGH              LOWER

Pedestrian     HIGH              LOWER

Queue          95m              100m*

Signal         45s                55s

        ───── 29% EXPOSURE REDUCTION ─────

                 ✓ SAFE

* simulated value.


---

42. ANALYTICS PAGE

Analytics must contain:

Climate Exposure Trend

Exposure
100 |
 80 |             ●
 60 |        ●────●
 40 | ●────●
 20 |
    +------------------
       Time

Heat vs Exposure

Shows relationship between:

Temperature
Exposure

Rain vs Exposure

Shows:

Rainfall
Visibility
Exposure

Road-user exposure

Separate series:

Two-wheelers
Pedestrians
Cars


---

43. ALERTS

Alerts must be generated when:

Climate risk becomes high
Exposure becomes high
Exposure becomes critical
Weather data becomes stale
Traffic data becomes unavailable
Road visibility becomes poor
Unsafe recommendation is attempted

Example:

🔥 HIGH CLIMATE EXPOSURE

North approach:
82 / 100

Main cause:
High heat + 2W waiting

Recommended action available.


---

44. USER ROLES

Operator

Can:

login;

view dashboard;

select intersection;

view exposure;

generate recommendation;

simulate;

accept recommendation;

reject recommendation;

view analytics;

acknowledge alerts.


Cannot:

change safety constraints;

modify users;

modify production configuration.



---

Administrator

Can:

perform all operator functions;

manage users;

manage intersections;

configure thresholds;

configure signal limits;

configure data providers.



---

Viewer

Can:

view dashboard;

view exposure;

view analytics.


Cannot:

accept/reject recommendations;

change configuration.



---

45. DATABASE

users

id                 BIGINT PRIMARY KEY
name               VARCHAR(100) NOT NULL
email              VARCHAR(255) UNIQUE NOT NULL
password_hash      VARCHAR(255) NOT NULL
role               ENUM('ADMIN','OPERATOR','VIEWER')
active             BOOLEAN DEFAULT TRUE
created_at         DATETIME NOT NULL
updated_at         DATETIME NOT NULL

Indexes:

UNIQUE(email)
INDEX(role, active)


---

46. intersections

id              BIGINT PRIMARY KEY
name            VARCHAR(150) NOT NULL
latitude        DECIMAL(10,7)
longitude       DECIMAL(10,7)
status          ENUM('ONLINE','OFFLINE','MAINTENANCE')
created_at      DATETIME


---

47. approaches

id
intersection_id
direction
lane_count
minimum_green_seconds
maximum_green_seconds
yellow_seconds
all_red_seconds
pedestrian_min_seconds

Constraint:

UNIQUE(intersection_id, direction)

Directions:

NORTH
SOUTH
EAST
WEST


---

48. weather_observations

id
intersection_id
temperature_c
feels_like_c
humidity_percent
rainfall_mm_h
visibility_m
wind_speed_kph
condition
observed_at

Index:

(intersection_id, observed_at)


---

49. traffic_observations

id
approach_id
two_wheeler_count
pedestrian_count
car_count
heavy_vehicle_count
average_speed_kph
queue_length_m
average_wait_seconds
captured_at

Index:

(approach_id, captured_at)


---

50. signal_states

id
intersection_id
active_approach_id
state
remaining_seconds
cycle_id
recorded_at

Signal states:

RED
YELLOW
GREEN
ALL_RED


---

51. exposure_scores

id
approach_id
weather_observation_id
traffic_observation_id

heat_risk
rain_risk
visibility_risk
wet_road_risk

climate_hazard
waiting_factor
density_factor

score
risk_level

calculated_at


---

52. signal_recommendations

id
intersection_id
target_approach_id

old_green_seconds
new_green_seconds

exposure_before
exposure_after

wait_before
wait_after

traffic_penalty

safety_valid
explanation

status
created_at
decided_at
decided_by

Statuses:

PENDING
ACCEPTED
REJECTED
EXPIRED


---

53. alerts

id
intersection_id
severity
category
title
message
acknowledged
created_at
acknowledged_at

Categories:

HEAT
RAIN
VISIBILITY
WET_ROAD
HIGH_EXPOSURE
STALE_DATA
SYSTEM


---

54. COMPLETE FOLDER STRUCTURE

climateguard-traffic/
│
├── client/
│   ├── src/
│   │   ├── api/
│   │   │   ├── axios.js
│   │   │   ├── authApi.js
│   │   │   ├── dashboardApi.js
│   │   │   ├── weatherApi.js
│   │   │   ├── trafficApi.js
│   │   │   └── analyticsApi.js
│   │   │
│   │   ├── components/
│   │   │   ├── layout/
│   │   │   ├── weather/
│   │   │   ├── exposure/
│   │   │   ├── intersection/
│   │   │   ├── recommendation/
│   │   │   ├── alerts/
│   │   │   └── analytics/
│   │   │
│   │   ├── pages/
│   │   │   ├── Login.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Analytics.jsx
│   │   │   ├── Intersections.jsx
│   │   │   └── Settings.jsx
│   │   │
│   │   ├── hooks/
│   │   ├── context/
│   │   ├── utils/
│   │   ├── App.jsx
│   │   └── main.jsx
│   │
│   └── package.json
│
├── server/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── routes/
│   │   ├── middleware/
│   │   ├── services/
│   │   │   ├── exposure/
│   │   │   ├── optimization/
│   │   │   ├── weather/
│   │   │   ├── traffic/
│   │   │   ├── analytics/
│   │   │   └── alerts/
│   │   ├── repositories/
│   │   ├── validators/
│   │   ├── sockets/
│   │   ├── jobs/
│   │   └── app.js
│   │
│   ├── tests/
│   └── package.json
│
├── database/
│   ├── migrations/
│   └── seed.sql
│
├── docs/
│
├── .env.example
├── README.md
├── SPEC.md
└── proposal.md


---

55. TECHNOLOGY STACK

Frontend

React

Purpose:

dashboard;

simulator;

charts;

interaction;

state management.


Vite

Purpose:

development server;

production build.


React Router

Purpose:

Login;

Dashboard;

Analytics;

Settings.


Axios

Purpose:

REST API calls.


Recharts

Purpose:

exposure graphs;

climate graphs;

waiting-time graphs.


Socket.IO Client

Purpose:

real-time dashboard updates.


Leaflet

Optional:

map visualization;

intersection location;

future multi-intersection view.



---

56. BACKEND

Node.js

Runtime.

Express.js

REST API.

MySQL2

Database connectivity.

JWT

Authentication.

bcrypt

Password hashing.

Zod

Input validation.

Socket.IO

Real-time events.

Axios

External weather API communication.


---

57. AI ARCHITECTURE

The AI architecture must be divided into:

DATA
 ↓
EXPOSURE ENGINE
 ↓
DECISION/OPTIMIZATION
 ↓
SAFETY VALIDATION
 ↓
SIMULATION
 ↓
EXPLANATION

An LLM must NOT directly decide:

"Set signal to green for 55 seconds."

Instead, the deterministic optimizer produces the validated decision.

The LLM may explain it.


---

58. OPTIONAL AI AGENT

flowchart TD

    A[Intersection State]
    A --> B[Climate Analysis Agent]

    B --> C[Calculate Exposure]

    C --> D[Decision Agent]

    D --> E[Generate Candidate Timings]

    E --> F[Safety Validation Tool]

    F -->|Invalid| G[Discard]

    F -->|Valid| H[Simulation Tool]

    H --> I[Compare Outcomes]

    I --> J[Recommendation]

    J --> K[Explanation Agent]

    K --> L[Dashboard]


---

59. AI TOOLS

An optional agent can access:

getWeather()
getTraffic()
getTwoWheelerDensity()
getPedestrianDensity()
getSignalState()
calculateExposure()
generateSignalCandidates()
validateSignalSafety()
simulateSignal()
compareImpact()
generateExplanation()

The agent cannot call:

setRealTrafficSignal()

in the hackathon implementation.


---

60. OPTIONAL ML MODEL

A later ML model may predict:

future traffic density
future waiting time
future climate exposure

Potential input features:

temperature
feelsLike
rainfall
visibility
time
day
2W density
pedestrian density
vehicle density
queue length
current signal phase
historical waiting time

Output:

{
  "predictedExposure": 74.3,
  "confidence": 0.84
}

If confidence is below the configured minimum:

Use deterministic exposure engine.


---

61. LLM EXPLANATION

The LLM receives structured information:

{
  "risk": "CRITICAL",
  "exposure": 82,
  "dominantFactors": [
    "high heat",
    "high two-wheeler density",
    "high pedestrian density",
    "long waiting"
  ],
  "recommendation": {
    "oldGreen": 45,
    "newGreen": 55
  },
  "predictedExposure": 58,
  "safetyValid": true
}

It may produce:

> North has the highest climate exposure because severe heat is affecting a large number of waiting two-wheeler riders and pedestrians. Extending the green phase by 10 seconds is predicted to reduce waiting exposure while remaining within the configured safety limits.



The output must be generated only from supplied structured data.


---

62. AUTHENTICATION

MVP:

Email
Password
JWT
Role

Password:

Minimum 8 characters
At least one letter
At least one number

Passwords must be hashed.

Tokens must not be stored in plaintext database fields.


---

63. API DESIGN

Base URL:

/api/v1

Response:

{
  "success": true,
  "data": {},
  "error": null,
  "timestamp": "ISO-8601"
}

Error:

{
  "success": false,
  "data": null,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request",
    "details": []
  },
  "timestamp": "ISO-8601"
}


---

64. AUTH API

POST /auth/login

Request:

{
  "email": "operator@example.com",
  "password": "password123"
}

Success:

{
  "user": {
    "id": 1,
    "name": "Operator",
    "role": "OPERATOR"
  },
  "accessToken": "JWT"
}

Errors:

401 INVALID_CREDENTIALS
403 ACCOUNT_DISABLED
422 VALIDATION_ERROR


---

65. INTERSECTION API

GET /intersections

Returns all accessible intersections.

GET /intersections/:id

Returns:

intersection
approaches
signal configuration
latest weather
latest traffic
latest exposure

GET /intersections/:id/dashboard

Returns the complete dashboard payload.


---

66. WEATHER API

GET /intersections/:id/weather/current

Backend:

1. Identify weather provider.
2. Request current weather.
3. Normalize provider response.
4. Save observation.
5. Return normalized response.

If provider fails:

Use recent observation if within freshness limit.

Otherwise:

WEATHER_UNAVAILABLE

The UI must show:

STALE

instead of pretending the data is live.


---

67. TRAFFIC API

GET /intersections/:id/traffic/current

Returns current traffic by approach.

POST /intersections/:id/traffic/simulate

Request:

{
  "approaches": [
    {
      "direction": "NORTH",
      "twoWheelerCount": 82,
      "pedestrianCount": 31,
      "carCount": 40,
      "heavyVehicleCount": 4,
      "averageWaitSeconds": 54,
      "queueLengthMeters": 95
    }
  ]
}

Validation:

Counts >= 0
Wait >= 0
Queue >= 0
Direction must exist


---

68. EXPOSURE API

POST /intersections/:id/exposure/calculate

Process:

Load weather
↓
Load traffic
↓
Load signal state
↓
Calculate climate hazard
↓
Calculate human exposure
↓
Calculate waiting factor
↓
Calculate final score
↓
Classify risk
↓
Store score
↓
Return result

Response:

{
  "intersectionId": 1,
  "overallScore": 82,
  "riskLevel": "CRITICAL",
  "approaches": [
    {
      "direction": "NORTH",
      "score": 82,
      "riskLevel": "CRITICAL",
      "dominantFactors": [
        "HIGH_HEAT",
        "HIGH_TWO_WHEELER_DENSITY",
        "HIGH_PEDESTRIAN_DENSITY",
        "LONG_WAIT"
      ]
    }
  ]
}


---

69. RECOMMENDATION API

POST /intersections/:id/recommendation/generate

Process:

Current state
↓
Current exposure
↓
Candidate signal timings
↓
Safety validation
↓
Simulation
↓
Exposure calculation
↓
Traffic penalty
↓
Select best candidate
↓
Save recommendation


---

70. ACCEPT RECOMMENDATION

POST /recommendations/:id/accept

Server must:

1. authenticate;


2. check role;


3. verify recommendation is pending;


4. revalidate safety;


5. apply to simulator;


6. record user;


7. update signal state;


8. recalculate exposure;


9. broadcast updated state.




---

71. REJECT RECOMMENDATION

POST /recommendations/:id/reject

Server must:

1. authenticate;


2. check role;


3. verify pending status;


4. mark rejected;


5. retain existing timing;


6. record operator decision.




---

72. ANALYTICS API

GET /intersections/:id/analytics

Query:

from
to
interval

Returns:

averageExposure
maximumExposure
averageWait
maximumWait
twoWheelerExposure
pedestrianExposure
heatExposure
rainExposure
recommendationCount
acceptedCount
estimatedExposureReduction


---

73. ALERT API

GET /alerts

Returns active alerts.

POST /alerts/:id/acknowledge

Marks alert acknowledged.


---

74. REAL-TIME ARCHITECTURE

Use Socket.IO.

Events:

weather.updated
traffic.updated
exposure.updated
signal.updated
recommendation.created
alert.created

Rooms:

intersection:{intersectionId}

Flow:

Weather changes
      ↓
Backend receives update
      ↓
Exposure recalculated
      ↓
Database updated
      ↓
Socket event
      ↓
Dashboard updates


---

75. BACKGROUND JOBS

Weather polling

Default:

5 minutes

Configurable.

Exposure recalculation

Trigger when:

weather changes
traffic changes
signal changes

or at configured interval.


---

76. ERROR STATES

The UI must handle:

Invalid login
No weather data
Stale weather
No traffic data
Stale traffic
Database unavailable
Recommendation unavailable
Unsafe recommendation
Recommendation expired
Socket disconnected
Intersection unavailable


---

77. EDGE CASES

Extreme heat + low traffic

Do not artificially create traffic.

Exposure can still increase due to climate hazard, but the optimizer must not create unnecessary congestion.

Heavy rain + high traffic

Prioritize safety.

The optimizer may choose a smaller adaptation if a larger change creates excessive road-safety risk.

High exposure on multiple approaches

Optimize overall exposure.

If scores are tied:

1. pedestrian count
2. two-wheeler count
3. waiting time
4. deterministic direction order

Weather unavailable

No climate-driven recommendation should be generated if there is insufficient climate data.

Traffic unavailable

Do not claim a valid human-exposure calculation without traffic/person data.

Recommendation becomes old

Before acceptance:

Recalculate current state.
Revalidate recommendation.

If conditions changed substantially:

EXPIRED


---

78. SECURITY

Required:

HTTPS in production;

JWT expiry;

bcrypt;

role authorization;

parameterized SQL;

request validation;

CORS restrictions;

login rate limiting;

secret management;

no API keys in frontend;

no password logging;

server-side signal validation.



---

79. ENVIRONMENT VARIABLES

NODE_ENV=development

PORT=5000

DATABASE_HOST=localhost
DATABASE_PORT=3306
DATABASE_NAME=climateguard
DATABASE_USER=root
DATABASE_PASSWORD=

JWT_SECRET=
JWT_EXPIRES_IN=1h

WEATHER_PROVIDER=
WEATHER_API_KEY=

MAP_PROVIDER=
MAP_API_KEY=

CLIENT_URL=http://localhost:5173

SOCKET_ENABLED=true

WEATHER_POLL_INTERVAL_MS=300000
EXPOSURE_RECALC_INTERVAL_MS=30000

MIN_RECOMMENDATION_CONFIDENCE=0.70


---

80. DEVELOPMENT SETUP

Backend

cd server
npm install
npm run dev

Frontend

cd client
npm install
npm run dev

Database

1. Create MySQL database.
2. Run migrations.
3. Run seed.sql.
4. Configure .env.
5. Start backend.
6. Start frontend.


---

81. DEMO DATA

The seeded demo must contain:

Temperature = 38.5°C
Feels-like = 42°C
Rainfall = 4.5 mm/h
Visibility = 2500m

North:

2W = 82
Pedestrians = 31
Cars = 40
Wait = 54 sec
Queue = 95m
Exposure = approximately 82

South:

2W = 52
Pedestrians = 18
Wait = 38 sec
Exposure = approximately 61

East:

2W = 30
Pedestrians = 12
Wait = 22 sec
Exposure = approximately 35

West:

2W = 24
Pedestrians = 8
Wait = 18 sec
Exposure = approximately 27


---

82. DEMO SIMULATION CONTROLS

The dashboard must include:

NORMAL
HEATWAVE
HEAVY RAIN
HIGH 2W DENSITY
HIGH PEDESTRIAN DENSITY
RESET

These controls are for the hackathon prototype.


---

83. HEATWAVE DEMO

Initial:

32°C
Exposure = 35

Click:

HEATWAVE

Change:

39°C
Feels-like 43°C

Exposure should rise.

Dashboard:

CRITICAL

Then:

Generate Recommendation


---

84. HEAVY RAIN DEMO

Change:

rainfall
visibility
wetRoad

The system recalculates:

rainRisk
visibilityRisk
wetRoadRisk
exposure

The recommendation must respect safety constraints.


---

85. HIGH TWO-WHEELER DEMO

Change:

North 2W:
40 → 85

The system must show:

2W exposure ↑
Total exposure ↑

and identify the North approach as a priority if it becomes the highest exposure approach.


---

86. HIGH PEDESTRIAN DEMO

Change:

Pedestrians:
10 → 40

The system must increase the human-exposure component.

The optimizer must preserve pedestrian minimum crossing requirements.


---

87. TESTING STRATEGY

Unit tests

Must test:

heatRisk()
rainRisk()
visibilityRisk()
wetRoadRisk()
calculateClimateHazard()
calculatePersonExposure()
calculateWaitingFactor()
calculateExposureScore()
classifyRisk()
generateCandidates()
validateCandidate()
simulateCandidate()
selectBestRecommendation()


---

88. INTEGRATION TESTS

Test:

Login
Dashboard API
Weather API
Traffic simulation
Exposure calculation
Recommendation generation
Recommendation acceptance
Recommendation rejection
Analytics
Alerts


---

89. END-TO-END TEST

Required flow:

Login
↓
Dashboard
↓
Select intersection
↓
Activate heatwave
↓
Exposure rises
↓
View exposure breakdown
↓
Generate recommendation
↓
View before/after
↓
Safety validation
↓
Accept
↓
Signal simulator changes
↓
Exposure recalculates
↓
Dashboard displays reduction
↓
Analytics records event


---

90. ACCEPTANCE CRITERIA

Climate input

The dashboard must display:

temperature;

feels-like temperature;

rainfall;

visibility;

road condition.



---

Two-wheeler input

The dashboard must separately display:

2W count
2W waiting time
2W exposure


---

Pedestrian input

The dashboard must separately display:

pedestrian count
pedestrian waiting time
pedestrian exposure


---

Exposure

Every approach must have:

score
risk
dominant factors


---

Recommendation

Every recommendation must contain:

old timing
new timing
exposure before
exposure after
waiting before
waiting after
safety result
reason


---

Simulation

After acceptance:

signal state changes
dashboard updates
exposure recalculates
before/after remains visible


---

91. PERFORMANCE

MVP target:

Dashboard API < 2 seconds
Exposure calculation < 200ms
Recommendation calculation < 500ms
Frontend interaction < 200ms
Real-time update < 2 seconds


---

92. SCALABILITY

The architecture must separate:

Weather Adapter
Traffic Adapter
Exposure Engine
Optimizer
Safety Validator
Database
Frontend

Therefore the prototype can later replace:

Simulated Traffic

with:

Camera → Computer Vision → Traffic Service

without rebuilding the frontend.


---

93. PRODUCTION CONSIDERATIONS

Before any physical traffic-light integration:

1. validate controller protocol;


2. validate signal timing rules;


3. validate pedestrian safety;


4. test sensor failures;


5. test network failures;


6. test weather API failures;


7. test false detections;


8. implement manual override;


9. implement fixed fallback timing;


10. conduct controlled field testing.



The hackathon implementation remains a simulator.


---

94. IMPLEMENTATION ORDER

Phase 1 — Project setup

Create Git repository
↓
Create React client
↓
Create Node server
↓
Create MySQL database
↓
Configure environment

Phase 2 — Database

users
↓
intersections
↓
approaches
↓
weather
↓
traffic
↓
signals
↓
exposure
↓
recommendations
↓
alerts

Phase 3 — Authentication

Login
↓
JWT
↓
Role middleware

Phase 4 — Exposure engine

Heat
↓
Rain
↓
Visibility
↓
Wet road
↓
People
↓
Waiting
↓
Exposure

Phase 5 — Signal optimizer

Current signal
↓
Generate candidates
↓
Safety validation
↓
Simulation
↓
Exposure comparison
↓
Recommendation

Phase 6 — Dashboard

Header
↓
Weather
↓
Exposure
↓
Intersection simulator
↓
Approach cards
↓
Recommendation
↓
Alerts
↓
Analytics

Phase 7 — Integration

Connect all APIs.

Phase 8 — Simulation

Add:

Heatwave
Rain
High 2W
High pedestrians
Reset

Phase 9 — Real-time

Add Socket.IO.

Phase 10 — Optional AI

Only after MVP is stable:

Prediction
↓
Confidence
↓
LLM explanation


---

95. MVP VS OPTIONAL

MUST HAVE

✓ Climate data
✓ Traffic density
✓ 2W density
✓ Pedestrian density
✓ Waiting time
✓ Climate Exposure Score
✓ Four-way intersection
✓ Signal simulator
✓ Safety validator
✓ Adaptive recommendation
✓ Before/after comparison
✓ Dashboard
✓ Analytics
✓ Heatwave scenario
✓ Heavy-rain scenario

OPTIONAL

○ Real weather API
○ Computer vision
○ ML prediction
○ LLM explanation
○ Map
○ Multi-intersection optimization
○ Mobile application
○ Notifications
○ Physical traffic-light integration


---

96. HACKATHON DEMO SCRIPT

0–30 seconds: Problem

Show normal traffic.

Explain:

> Traffic systems usually know how many vehicles are waiting, but they do not explicitly measure how much hazardous outdoor climate exposure people experience while waiting.




---

30–60 seconds: Climate event

Activate:

HEATWAVE

Show:

Temperature 32°C → 39°C
Feels-like → 43°C

Exposure rises.


---

60–90 seconds: Human exposure

Point to:

North:
82 two-wheelers
31 pedestrians
54-second wait

Then show:

Climate Exposure:
82 / 100
CRITICAL


---

90–120 seconds: AI recommendation

Click:

GENERATE RECOMMENDATION

System produces:

45s → 55s

Explain:

> The system is not simply giving green to the road with the most vehicles. It is prioritizing the approach where people are experiencing the highest climate exposure.




---

120–150 seconds: Safety

Show:

✓ Minimum green
✓ Maximum green
✓ Yellow preserved
✓ Pedestrian crossing preserved
✓ No conflicting green


---

150–180 seconds: Result

Show:

Exposure:
82 → 58

Wait:
54s → 39s

Estimated climate exposure reduction:
29%

Then show analytics.


---

97. CLIMATE-FIRST SUCCESS METRIC

The project must present:

> Estimated reduction in human climate exposure



as the main success metric.

Not:

> Vehicles moved per minute.



Traffic efficiency remains important, but it is a constraint and secondary objective.


---

98. FINAL PRODUCT ARCHITECTURE

┌─────────────────────┐
                       │   WEATHER DATA      │
                       │ Heat / Rain /       │
                       │ Visibility          │
                       └──────────┬──────────┘
                                  │
                                  ▼
┌─────────────────┐     ┌─────────────────────┐
│ TRAFFIC DATA    │────►│                     │
│ Cars            │     │                     │
│ 2-Wheelers      │     │   DATA NORMALIZER   │
│ Trucks          │     │                     │
└─────────────────┘     └──────────┬──────────┘
                                   │
┌─────────────────┐                │
│ PEOPLE DATA     │────────────────┤
│ Pedestrians     │                │
│ 2W Riders       │                │
└─────────────────┘                │
                                   ▼
                         ┌─────────────────────┐
                         │ CLIMATE EXPOSURE    │
                         │ ENGINE              │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ EXPOSURE SCORE      │
                         │ 0 ──────────── 100  │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ ADAPTIVE SIGNAL     │
                         │ OPTIMIZER            │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ SAFETY VALIDATOR    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ IMPACT SIMULATOR    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ BEFORE / AFTER      │
                         │ EXPOSURE            │
                         └──────────┬──────────┘
                                    │
                                    ▼
                    ┌────────────────────────────┐
                    │       REACT DASHBOARD      │
                    │                            │
                    │ Weather                    │
                    │ Exposure                   │
                    │ 2W / Pedestrians           │
                    │ Intersection               │
                    │ Recommendation             │
                    │ Analytics                  │
                    └────────────────────────────┘


---

99. HIGH-LEVEL PROPOSAL / DESIGN PLAN

Architecture principle

The project must be presented as:

CLIMATE
                       ↓
                  EXPOSURE
                       ↓
                 HUMAN IMPACT
                       ↓
                 SAFE RESPONSE
                       ↓
                 SIGNAL CHANGE
                       ↓
                LOWER EXPOSURE

Traffic is the intervention mechanism.

Climate exposure is the problem being optimized.


---

100. THE THREE-LAYER DEMO STORY

Layer 1 — Sensing

"What is happening?"

Show:

Weather
Traffic
2W
Pedestrians
Waiting
Road


---

Layer 2 — Intelligence

"Who is exposed and why?"

Show:

Climate Exposure Score

and its factors.


---

Layer 3 — Action

"What can we safely do?"

Show:

Signal recommendation
↓
Safety validation
↓
Simulation
↓
Exposure reduction


---

101. FINAL SYSTEM FLOW

┌───────────────┐
                     │ EXTREME HEAT  │
                     │ OR HEAVY RAIN │
                     └───────┬───────┘
                             │
                             ▼
                 ┌─────────────────────┐
                 │ PEOPLE WAITING      │
                 │                     │
                 │ 2W + PEDESTRIANS    │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ CLIMATE EXPOSURE    │
                 │ CALCULATION         │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ EXPOSURE SCORE      │
                 │                     │
                 │ LOW / MOD / HIGH /  │
                 │ CRITICAL            │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ SIGNAL OPTIMIZATION │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ SAFETY VALIDATION   │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ BEFORE / AFTER      │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ EXPOSURE REDUCED    │
                 └─────────────────────┘


---

102. FINAL IMPLEMENTATION PRINCIPLE

Do not build a normal smart-traffic dashboard and add weather as a small widget.

Build the product around this central idea:

CLIMATE HAZARD
                    +
              PEOPLE WAITING
                    +
          TWO-WHEELER / PEDESTRIAN
                 EXPOSURE
                    ↓
          CLIMATE EXPOSURE SCORE
                    ↓
           SAFE ADAPTIVE SIGNAL
                    ↓
           LOWER HUMAN EXPOSURE

The strongest statement for the project is:

> ClimateGuard Traffic transforms traffic signals from systems that only manage vehicle movement into climate-aware systems that actively reduce unnecessary outdoor exposure for the people using the road.




---

103. OPEN DECISIONS

The implementation agent must not silently invent the following:

1. Final project name.


2. Final demo intersection.


3. Weather API provider.


4. Map provider.


5. Real traffic-data provider.


6. Camera hardware.


7. Production signal-controller protocol.


8. Final climate threshold values.


9. Final exposure weights.


10. Final geographic deployment region.


11. Whether SMS/push notifications are required.


12. Whether an external LLM is required.


13. Whether ML prediction is required for the judging demo.



For the hackathon MVP, use:

Simulated weather
+
Simulated traffic
+
Simulated people density
+
Deterministic climate exposure engine
+
Safety-constrained signal optimizer
+
Interactive dashboard

This guarantees that the central climate-exposure demonstration works even without external hardware or paid APIs. -->



Yes. The best approach is to turn your `SPEC.md` into a **single implementation-ready master prompt** for the VS Code Agent, while clearly separating the project into **1.1, 1.2, 1.3 and 1.4**.

The important part is that the agent must **not invent features or change your architecture**. It should use the specification below as the only source of truth.

You can paste the following prompt into the VS Code Agent.

# ClimateGuard Traffic — Master Implementation Prompt

## 0. INSTRUCTION TO THE VS CODE AGENT

You are implementing the **ClimateGuard Traffic — Climate-Adaptive Traffic Signal & Human Exposure Reduction Platform**.

The existing `SPEC.md` is the **single source of truth** for this project.

You MUST follow the specification exactly.

### Absolute rules

1. Do not invent features that are not specified.
2. Do not remove any required feature.
3. Do not replace the climate-first concept with a conventional traffic-management system.
4. Do not directly control real traffic signals.
5. The traffic signal functionality is a **simulation only**.
6. Do not use an LLM as the direct signal controller.
7. The deterministic exposure engine and safety validator must control the recommendation logic.
8. Optional ML, LLM, maps, real weather APIs and hardware integration must not be required for the MVP.
9. Use simulated data for the hackathon MVP.
10. Do not silently invent final climate thresholds, geographic location, weather provider, map provider or hardware.
11. Keep the project modular so four developers can work on separate Git branches with minimal merge conflicts.
12. Do not unnecessarily modify files owned by another module.
13. Do not create duplicate implementations of the same business logic.
14. Keep all calculations transparent and store intermediate exposure values.
15. The main success metric is **Estimated Reduction in Human Climate Exposure**, not vehicles moved per minute.

---

# 1. PROJECT MODULE DIVISION

The entire project is divided into four independent modules.

## 1.1 MODULE 1 — Dashboard, Interactive Junction Map & Frontend UI

### Responsibility

Build the complete React frontend and the dashboard shown in the provided reference design.

This module owns:

* Login page UI
* Main dashboard
* Left analytics/sidebar
* Center interactive junction/map
* Right signal-processing panel
* Approach details
* Climate exposure visualization
* Traffic-density visualization
* Recommendation panel
* Before/after comparison
* Alerts
* Analytics charts
* Simulation controls
* Responsive layout

### Main frontend folders

```text
client/src/
├── components/
│   ├── layout/
│   ├── weather/
│   ├── exposure/
│   ├── traffic/
│   ├── intersection/
│   ├── signal/
│   ├── recommendation/
│   ├── alerts/
│   └── analytics/
│
├── pages/
│   ├── Login.jsx
│   ├── Dashboard.jsx
│   ├── Analytics.jsx
│   ├── Intersections.jsx
│   └── Settings.jsx
│
├── hooks/
├── context/
├── utils/
├── api/
├── App.jsx
└── main.jsx
```

### Technology

Use:

* React
* Vite
* React Router
* Axios
* Recharts
* Socket.IO Client

Leaflet is optional and must not be required for the MVP.

---

## 1.1.1 DASHBOARD STRUCTURE

The main dashboard MUST have three major areas.

```text
┌───────────────────────────────────────────────────────────────┐
│                         HEADER                                │
├──────────────────┬──────────────────────────┬─────────────────┤
│                  │                          │                 │
│ LEFT ANALYTICS   │ CENTER JUNCTION/MAP      │ RIGHT SIGNAL    │
│                  │                          │                 │
│ Traffic Density  │ Interactive Intersection │ Signal Status   │
│ Climate Exposure │ Clickable Junctions      │ Cycle Timing    │
│ Climate Factors  │ Severity Visualization   │ Flow Rate       │
│                  │                          │ Wait Time       │
│                  │                          │ Recommendation  │
└──────────────────┴──────────────────────────┴─────────────────┘
```

---

## 1.1.2 HEADER

Display:

* ClimateGuard Traffic
* Selected intersection
* Live status
* Current timestamp
* Logged-in operator
* System mode
* Emergency mode indicator

The design should follow the dark, professional traffic-control dashboard shown in the provided reference.

---

# 1.1.3 LEFT ANALYTICS PANEL

The left side is an analytical panel, not merely navigation.

It MUST contain:

### A. Traffic Density

Display:

* Total vehicle count
* Two-wheeler count
* Pedestrian count
* Car count
* Heavy vehicle count
* Queue length
* Average waiting time
* Traffic density classification

Example:

```text
TRAFFIC DENSITY

HIGH

Two-Wheelers       82
Pedestrians        31
Cars               40
Heavy Vehicles      4

Queue              95 m
Average Wait       54 s
```

### B. Climate Exposure

Display:

* Overall exposure score
* Risk level
* Heat risk
* Rain risk
* Visibility risk
* Wet-road risk
* Main climate driver

Example:

```text
CLIMATE EXPOSURE

82 / 100
CRITICAL

Heat Risk          91%
Rain Risk          48%
Visibility Risk    20%
Wet Road Risk      40%

Main Driver:
EXTREME HEAT
```

The climate exposure section must be visually prominent.

---

# 1.1.4 CENTER INTERACTIVE JUNCTION

The center of the dashboard MUST contain an interactive four-way intersection.

The four approaches are:

* NORTH
* SOUTH
* EAST
* WEST

The center should visually resemble a real intersection/simulator.

Each approach must show relevant traffic information.

Example:

```text
                         NORTH
                           │
                       ┌───●───┐
                       │  82   │
                       │CRITICAL│
                       └───┬───┘
                           │
                           │
WEST ───────────────────── ● ───────────────────── EAST
                           │
                           │
                       ┌───●───┐
                       │  61   │
                       │ HIGH   │
                       └───────┘
                         SOUTH
```

Each approach must be clickable.

---

# 1.1.5 CLICKABLE JUNCTION BEHAVIOUR

When a user clicks an approach, display detailed information.

Example:

```text
NORTH APPROACH

Exposure
82 / 100

Risk
CRITICAL

Two-Wheelers
82

Pedestrians
31

Vehicles
126

Average Wait
54 sec

Queue
95 m

Heat Risk
91%

Rain Risk
48%

Visibility Risk
20%

Wet Road Risk
40%

Dominant Factors:
1. Heat
2. Two-wheeler density
3. Pedestrian density
4. Waiting time
```

The selected approach should be visually highlighted.

---

# 1.1.6 SEVERITY VISUALIZATION

Use:

```text
0–24      LOW
25–49     MODERATE
50–74     HIGH
75–100    CRITICAL
```

Every approach must visually show:

* Score
* Risk
* Signal state
* 2W count
* Pedestrian count
* Average wait
* Queue

Example:

```text
NORTH    82    CRITICAL
SOUTH    61    HIGH
EAST     35    MODERATE
WEST     27    MODERATE
```

---

# 1.1.7 RIGHT SIGNAL PANEL

The right side MUST focus on signal processing.

It should contain:

### Signal status

* Signal ID
* Intersection name
* Active/inactive status
* Current phase
* Remaining time

### Wait and flow

* Average wait
* Flow rate
* Traffic volume

### Cycle timing

Display:

* Current cycle
* Green
* Yellow
* Red
* All-red

### Manual simulation controls

Provide:

```text
FORCE GREEN
FORCE RED
RESET TO AUTOMATIC
```

These controls operate ONLY on the simulator.

---

# 1.1.8 ADAPTIVE RECOMMENDATION PANEL

The right panel must also contain the adaptive recommendation.

Never display only:

```text
AI recommends +10 seconds
```

Instead display:

```text
ADAPTIVE RECOMMENDATION

NORTH GREEN

45s → 55s

WHY?

Severe heat + high two-wheeler density +
high pedestrian density + long waiting time

EXPECTED RESULT

Exposure:
82 → 58

Waiting:
54s → 39s

Estimated Exposure Reduction:
29%

SAFETY VALIDATION:
✓ Safe
```

Buttons:

```text
ACCEPT & SIMULATE
REJECT
VIEW FULL EXPLANATION
```

---

# 1.1.9 BEFORE/AFTER VIEW

This is a major hackathon visual.

Display:

```text
                 BEFORE       AFTER

Exposure            82          58
Risk             CRITICAL      HIGH
Wait               54s         39s
2W Wait            HIGH        LOWER
Pedestrian         HIGH        LOWER
Queue              95m        100m*
Signal              45s         55s

      29% ESTIMATED EXPOSURE REDUCTION

                    ✓ SAFE
```

Simulated values must be clearly identified as simulated.

---

# 1.1.10 ALERTS

Display alerts for:

* High climate risk
* High exposure
* Critical exposure
* Stale weather
* Traffic unavailable
* Poor visibility
* Unsafe recommendation
* System errors

Example:

```text
HIGH CLIMATE EXPOSURE

North Approach

82 / 100

Main Cause:
High heat + high 2W waiting

Recommended action available.
```

---

# 1.1.11 ANALYTICS PAGE

The analytics page MUST display:

* Climate Exposure Trend
* Heat vs Exposure
* Rain vs Exposure
* Two-wheeler exposure
* Pedestrian exposure
* Car exposure
* Average waiting time
* Maximum waiting time
* Recommendation count
* Accepted recommendations
* Estimated exposure reduction

Use Recharts.

---

# 1.1.12 SIMULATION CONTROLS

The dashboard must include:

```text
NORMAL
HEATWAVE
HEAVY RAIN
HIGH 2W DENSITY
HIGH PEDESTRIAN DENSITY
RESET
```

These are hackathon simulation controls.

---

# 1.1.13 RESPONSIVE DESIGN

The dashboard must work on:

* Desktop
* Laptop
* Tablet
* Mobile

Desktop should prioritize the three-column traffic-control layout.

On smaller screens, stack:

1. Traffic/climate analytics
2. Junction simulator
3. Signal panel
4. Recommendation
5. Alerts/analytics

---

# 1.2 MODULE 2 — Climate, Traffic, Human Exposure & Risk Engine

### Responsibility

This module contains the deterministic climate-exposure intelligence.

It owns:

* Weather normalization
* Heat risk
* Rain risk
* Visibility risk
* Wet-road risk
* Human exposure
* Waiting factor
* Density factor
* Climate Exposure Score
* Risk classification
* Dominant-factor detection

### Main folders

```text
server/src/services/
├── exposure/
│   ├── heatRisk.js
│   ├── rainRisk.js
│   ├── visibilityRisk.js
│   ├── wetRoadRisk.js
│   ├── climateHazard.js
│   ├── humanExposure.js
│   ├── waitingFactor.js
│   ├── densityFactor.js
│   ├── exposureScore.js
│   └── riskClassifier.js
│
├── weather/
│   └── weatherService.js
│
└── traffic/
    └── trafficService.js
```

---

# 1.2.1 CLIMATE INPUTS

Use:

```text
temperatureC
feelsLikeC
humidity
rainfallMmPerHour
visibilityM
wind
weatherCondition
```

---

# 1.2.2 TRAFFIC INPUTS

Use:

```text
vehicleCount
averageSpeed
queueLength
averageWait
```

---

# 1.2.3 TWO-WHEELER INPUTS

Track separately:

```text
twoWheelerCount
twoWheelerAverageWait
twoWheelerQueue
```

---

# 1.2.4 PEDESTRIAN INPUTS

Track separately:

```text
pedestrianCount
pedestrianAverageWait
crossingDemand
```

---

# 1.2.5 ROAD INPUTS

Use:

```text
wetRoad
roadCondition
visibility
```

---

# 1.2.6 SIGNAL INPUTS

Use:

```text
currentPhase
currentGreenDuration
remainingGreen
remainingRed
yellowDuration
allRedDuration
```

---

# 1.2.7 HEAT RISK

Use configured thresholds.

Do not make medical claims.

The higher relevant heat indicator must be used according to configured rules.

Example:

```text
temperature = 39°C
feelsLike = 43°C
```

---

# 1.2.8 RAIN RISK

Use:

```text
rainfallMmPerHour
```

Also consider:

* Visibility
* Wet road

Rainfall alone must not represent total road risk.

---

# 1.2.9 VISIBILITY RISK

Lower visibility must produce higher risk.

---

# 1.2.10 WET-ROAD RISK

Use actual road-condition data when available.

If configured, rainfall can infer wet-road conditions.

---

# 1.2.11 CLIMATE HAZARD

Default configurable weights:

```text
heat = 0.45
rain = 0.30
visibility = 0.15
wetRoad = 0.10
```

Formula:

```text
climateHazard =
    0.45 * heatRisk +
    0.30 * rainRisk +
    0.15 * visibilityRisk +
    0.10 * wetRoadRisk
```

Weights must sum to 1.0.

---

# 1.2.12 HUMAN EXPOSURE

Track separately:

```text
twoWheelers
pedestrians
cars
heavyVehicles
otherVehicles
```

Default prototype weights:

```text
twoWheelerWeight = 1.00
pedestrianWeight = 1.00
carWeight = 0.25
heavyVehicleWeight = 0.35
otherVehicleWeight = 0.30
```

Formula:

```text
personExposure =
    twoWheelerCount * twoWheelerWeight
    +
    pedestrianCount * pedestrianWeight
    +
    carCount * carWeight
    +
    heavyVehicleCount * heavyVehicleWeight
    +
    otherVehicleCount * otherVehicleWeight
```

These are configurable prototype weights, not scientific claims.

---

# 1.2.13 WAITING FACTOR

```text
waitingFactor =
    currentAverageWaitSeconds / targetWaitSeconds
```

Clamp:

```text
0 → 2
```

Normalize:

```text
normalizedWaitingFactor =
    clamp(waitingFactor, 0, 2) / 2
```

---

# 1.2.14 DENSITY FACTOR

```text
densityFactor =
    clamp(
        personExposure / capacityReference,
        0,
        1
    )
```

`capacityReference` is configurable per approach.

---

# 1.2.15 FINAL EXPOSURE SCORE

```text
exposureScore =
    clamp(
        100
        *
        climateHazard
        *
        (0.5 + 0.5 * normalizedWaitingFactor)
        *
        (0.5 + 0.5 * densityFactor),
        0,
        100
    )
```

Store every intermediate value.

The system must be able to explain:

```text
Why is this exposure score 82?
```

---

# 1.2.16 RISK CLASSIFICATION

```text
0–24       LOW
25–49      MODERATE
50–74      HIGH
75–100     CRITICAL
```

---

# 1.2.17 APPROACH EXPOSURE

Every approach must independently calculate exposure.

Example:

```text
NORTH = 82 CRITICAL
SOUTH = 61 HIGH
EAST  = 35 MODERATE
WEST  = 27 MODERATE
```

---

# 1.2.18 DOMINANT FACTORS

The engine must identify factors such as:

```text
HIGH_HEAT
HIGH_RAIN
LOW_VISIBILITY
WET_ROAD
HIGH_TWO_WHEELER_DENSITY
HIGH_PEDESTRIAN_DENSITY
LONG_WAIT
HIGH_QUEUE
```

The frontend will display these factors.

---

# 1.2.19 DEMO DATA

Use the specified demo data:

```text
Temperature = 38.5°C
Feels-like = 42°C
Rainfall = 4.5 mm/h
Visibility = 2500m
```

North:

```text
2W = 82
Pedestrians = 31
Cars = 40
Wait = 54 sec
Queue = 95m
Exposure ≈ 82
```

South:

```text
2W = 52
Pedestrians = 18
Wait = 38 sec
Exposure ≈ 61
```

East:

```text
2W = 30
Pedestrians = 12
Wait = 22 sec
Exposure ≈ 35
```

West:

```text
2W = 24
Pedestrians = 8
Wait = 18 sec
Exposure ≈ 27
```

---

# 1.2.20 TESTING

Create unit tests for:

```text
heatRisk()
rainRisk()
visibilityRisk()
wetRoadRisk()
calculateClimateHazard()
calculatePersonExposure()
calculateWaitingFactor()
calculateExposureScore()
classifyRisk()
```

---

# 1.3 MODULE 3 — Signal Optimization, Safety Validation & Simulation

### Responsibility

This module owns:

* Signal candidate generation
* Signal optimization
* Safety validation
* Signal simulation
* Queue simulation
* Impact simulation
* Recommendation generation
* Before/after comparison

### Main folders

```text
server/src/services/
├── optimization/
│   ├── candidateGenerator.js
│   ├── optimizer.js
│   ├── objective.js
│   └── recommendation.js
│
└── simulation/
    ├── signalSimulator.js
    ├── queueSimulator.js
    └── impactSimulator.js
```

---

# 1.3.1 OPTIMIZATION PRIORITY

Always prioritize:

```text
1. Safety
2. Climate exposure reduction
3. Two-wheeler/pedestrian waiting reduction
4. Queue control
5. General traffic efficiency
```

Safety is an absolute constraint.

---

# 1.3.2 SIGNAL CANDIDATES

If current green is:

```text
45 seconds
```

Generate:

```text
35
40
45
50
55
```

The range must be configurable.

---

# 1.3.3 SAFETY VALIDATION

Reject a candidate if:

```text
green < minimumGreen

green > maximumGreen

yellow < configured minimum

allRed < configured minimum

pedestrian crossing time < minimum

conflicting approaches become green simultaneously
```

Also reject any candidate violating another configured safety constraint.

---

# 1.3.4 CANDIDATE SIMULATION

For each safe candidate:

1. Estimate new waiting time.
2. Estimate new queue.
3. Estimate new two-wheeler waiting time.
4. Estimate new pedestrian waiting time.
5. Calculate predicted exposure.
6. Calculate traffic penalty.
7. Calculate queue penalty.
8. Calculate total objective.

---

# 1.3.5 OBJECTIVE

Conceptually:

```text
totalCost =
    exposureCost
    +
    trafficPenalty
    +
    queuePenalty
```

Exposure cost has the highest configurable weight.

---

# 1.3.6 RECOMMENDATION OUTPUT

Use:

```json
{
  "recommendationId": 17,
  "approach": "NORTH",
  "action": "EXTEND_GREEN",
  "oldGreenSeconds": 45,
  "newGreenSeconds": 55,
  "exposureBefore": 82,
  "exposureAfter": 58,
  "exposureReductionPercent": 29,
  "waitBefore": 54,
  "waitAfter": 39,
  "safetyValid": true,
  "reason": [
    "High heat exposure",
    "High two-wheeler density",
    "High pedestrian density",
    "Long waiting time"
  ]
}
```

---

# 1.3.7 PRIMARY KPI

Calculate:

```text
baselineExposure = exposure before recommendation

predictedExposure = exposure after simulation

reductionPercent =
(
    baselineExposure - predictedExposure
)
/
baselineExposure
× 100
```

If baseline exposure is zero:

```text
reductionPercent = 0
```

---

# 1.3.8 ACCEPT RECOMMENDATION

Acceptance must:

1. Authenticate user.
2. Check role.
3. Verify recommendation is pending.
4. Revalidate safety.
5. Apply only to simulator.
6. Record user.
7. Update simulated signal state.
8. Recalculate exposure.
9. Broadcast updated state.

---

# 1.3.9 REJECT RECOMMENDATION

Rejection must:

1. Authenticate user.
2. Check role.
3. Verify pending status.
4. Mark recommendation rejected.
5. Retain existing timing.
6. Record operator decision.

---

# 1.3.10 EDGE CASES

### Extreme heat + low traffic

Do not create artificial traffic.

### Heavy rain + high traffic

Prioritize safety.

### Multiple high-exposure approaches

Optimize overall exposure.

If tied:

```text
1. pedestrian count
2. two-wheeler count
3. waiting time
4. deterministic direction order
```

### Recommendation becomes old

Recalculate current state.

Revalidate safety.

If conditions changed substantially:

```text
EXPIRED
```

---

# 1.3.11 TESTING

Create unit tests for:

```text
generateCandidates()
validateCandidate()
simulateCandidate()
selectBestRecommendation()
```

Also test:

* Unsafe candidate rejection
* Safe candidate acceptance
* Recommendation expiry
* Before/after calculation
* Multiple high-exposure approaches

---

# 1.4 MODULE 4 — Database, Authentication, API, Analytics, Alerts & Real-Time Integration

### Responsibility

This module owns backend infrastructure and integration.

It must provide the API consumed by Modules 1, 2 and 3.

---

# 1.4.1 DATABASE

Use MySQL.

Required tables:

```text
users
intersections
approaches
weather_observations
traffic_observations
signal_states
exposure_scores
signal_recommendations
alerts
```

---

# 1.4.2 USERS

Fields:

```text
id
name
email
password_hash
role
active
created_at
updated_at
```

Roles:

```text
ADMIN
OPERATOR
VIEWER
```

---

# 1.4.3 INTERSECTIONS

Fields:

```text
id
name
latitude
longitude
status
created_at
```

Statuses:

```text
ONLINE
OFFLINE
MAINTENANCE
```

---

# 1.4.4 APPROACHES

Fields:

```text
id
intersection_id
direction
lane_count
minimum_green_seconds
maximum_green_seconds
yellow_seconds
all_red_seconds
pedestrian_min_seconds
```

Constraint:

```text
UNIQUE(intersection_id, direction)
```

Directions:

```text
NORTH
SOUTH
EAST
WEST
```

---

# 1.4.5 WEATHER OBSERVATIONS

Fields:

```text
id
intersection_id
temperature_c
feels_like_c
humidity_percent
rainfall_mm_h
visibility_m
wind_speed_kph
condition
observed_at
```

Index:

```text
(intersection_id, observed_at)
```

---

# 1.4.6 TRAFFIC OBSERVATIONS

Fields:

```text
id
approach_id
two_wheeler_count
pedestrian_count
car_count
heavy_vehicle_count
average_speed_kph
queue_length_m
average_wait_seconds
captured_at
```

Index:

```text
(approach_id, captured_at)
```

---

# 1.4.7 SIGNAL STATES

Fields:

```text
id
intersection_id
active_approach_id
state
remaining_seconds
cycle_id
recorded_at
```

States:

```text
RED
YELLOW
GREEN
ALL_RED
```

---

# 1.4.8 EXPOSURE SCORES

Store:

```text
id
approach_id
weather_observation_id
traffic_observation_id
heat_risk
rain_risk
visibility_risk
wet_road_risk
climate_hazard
waiting_factor
density_factor
score
risk_level
calculated_at
```

---

# 1.4.9 RECOMMENDATIONS

Store:

```text
id
intersection_id
target_approach_id
old_green_seconds
new_green_seconds
exposure_before
exposure_after
wait_before
wait_after
traffic_penalty
safety_valid
explanation
status
created_at
decided_at
decided_by
```

Statuses:

```text
PENDING
ACCEPTED
REJECTED
EXPIRED
```

---

# 1.4.10 ALERTS

Fields:

```text
id
intersection_id
severity
category
title
message
acknowledged
created_at
acknowledged_at
```

Categories:

```text
HEAT
RAIN
VISIBILITY
WET_ROAD
HIGH_EXPOSURE
STALE_DATA
SYSTEM
```

---

# 1.4.11 AUTHENTICATION

Use:

* Email
* Password
* JWT
* bcrypt
* Role-based authorization

Password requirements:

```text
Minimum 8 characters
At least one letter
At least one number
```

Never store plaintext passwords.

Never log passwords.

---

# 1.4.12 BACKEND TECHNOLOGY

Use:

* Node.js
* Express.js
* MySQL2
* JWT
* bcrypt
* Zod
* Socket.IO
* Axios

---

# 1.4.13 API BASE

```text
/api/v1
```

Response structure:

```json
{
  "success": true,
  "data": {},
  "error": null,
  "timestamp": "ISO-8601"
}
```

Error structure:

```json
{
  "success": false,
  "data": null,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid request",
    "details": []
  },
  "timestamp": "ISO-8601"
}
```

---

# 1.4.14 REQUIRED APIs

Authentication:

```text
POST /auth/login
```

Intersections:

```text
GET /intersections
GET /intersections/:id
GET /intersections/:id/dashboard
```

Weather:

```text
GET /intersections/:id/weather/current
```

Traffic:

```text
GET /intersections/:id/traffic/current
POST /intersections/:id/traffic/simulate
```

Exposure:

```text
POST /intersections/:id/exposure/calculate
```

Recommendations:

```text
POST /intersections/:id/recommendation/generate

POST /recommendations/:id/accept

POST /recommendations/:id/reject
```

Analytics:

```text
GET /intersections/:id/analytics
```

Alerts:

```text
GET /alerts
POST /alerts/:id/acknowledge
```

---

# 1.4.15 DASHBOARD API

```text
GET /intersections/:id/dashboard
```

This endpoint should return the complete data required by the dashboard:

```text
intersection
approaches
weather
traffic
people
signal
exposure
recommendation
alerts
system status
```

Do not make the frontend reconstruct business logic that belongs in the backend.

---

# 1.4.16 REAL-TIME SOCKET.IO

Use:

```text
weather.updated
traffic.updated
exposure.updated
signal.updated
recommendation.created
alert.created
```

Room:

```text
intersection:{intersectionId}
```

Flow:

```text
Data changes
     ↓
Backend
     ↓
Exposure recalculated
     ↓
Database updated
     ↓
Socket event
     ↓
Dashboard updates
```

---

# 1.4.17 ANALYTICS

Return:

```text
averageExposure
maximumExposure
averageWait
maximumWait
twoWheelerExposure
pedestrianExposure
heatExposure
rainExposure
recommendationCount
acceptedCount
estimatedExposureReduction
```

---

# 1.4.18 ERROR HANDLING

Handle:

```text
Invalid login
No weather data
Stale weather
No traffic data
Stale traffic
Database unavailable
Recommendation unavailable
Unsafe recommendation
Recommendation expired
Socket disconnected
Intersection unavailable
```

Never pretend stale data is live.

---

# 2. SHARED PROJECT ARCHITECTURE

The final project MUST use:

```text
climateguard-traffic/
│
├── client/
│   ├── src/
│   │   ├── api/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── context/
│   │   ├── utils/
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
│
├── server/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── routes/
│   │   ├── middleware/
│   │   ├── services/
│   │   │   ├── exposure/
│   │   │   ├── optimization/
│   │   │   ├── simulation/
│   │   │   ├── weather/
│   │   │   ├── traffic/
│   │   │   └── analytics/
│   │   ├── repositories/
│   │   ├── validators/
│   │   ├── sockets/
│   │   └── app.js
│   │
│   ├── tests/
│   └── package.json
│
├── database/
│   ├── migrations/
│   └── seed.sql
│
├── docs/
│
├── .env.example
├── README.md
├── SPEC.md
└── proposal.md
```

---

# 3. TECHNOLOGY STACK

## Frontend

```text
React
Vite
React Router
Axios
Recharts
Socket.IO Client
```

## Backend

```text
Node.js
Express.js
MySQL2
JWT
bcrypt
Zod
Socket.IO
Axios
```

---

# 4. AI ARCHITECTURE

The architecture MUST remain:

```text
DATA
 ↓
EXPOSURE ENGINE
 ↓
DECISION / OPTIMIZATION
 ↓
SAFETY VALIDATION
 ↓
SIMULATION
 ↓
EXPLANATION
```

The LLM must NOT directly decide signal timing.

The deterministic optimizer generates the candidate.

The safety validator validates it.

The simulator evaluates it.

An optional LLM can explain the structured result.

---

# 5. OPTIONAL AI

Optional tools:

```text
getWeather()
getTraffic()
getTwoWheelerDensity()
getPedestrianDensity()
getSignalState()
calculateExposure()
generateSignalCandidates()
validateSignalSafety()
simulateSignal()
compareImpact()
generateExplanation()
```

The system MUST NOT provide:

```text
setRealTrafficSignal()
```

---

# 6. OPTIONAL ML

Only after MVP stability.

Possible prediction:

```text
future traffic density
future waiting time
future climate exposure
```

Potential output:

```json
{
  "predictedExposure": 74.3,
  "confidence": 0.84
}
```

If confidence is below configured minimum:

```text
Use deterministic exposure engine.
```

ML is optional and must not block the MVP.

---

# 7. DEMO SCENARIOS

The dashboard must support:

## NORMAL

Normal baseline.

## HEATWAVE

Change:

```text
32°C → 39°C
Feels-like → 43°C
```

Exposure must increase.

## HEAVY RAIN

Change:

```text
rainfall
visibility
wetRoad
```

Recalculate exposure.

## HIGH TWO-WHEELER DENSITY

Example:

```text
North 2W:
40 → 85
```

Exposure must increase.

## HIGH PEDESTRIAN DENSITY

Example:

```text
Pedestrians:
10 → 40
```

Human exposure must increase.

## RESET

Return to demo baseline.

---

# 8. REQUIRED DEMO FLOW

The final website must support this exact demonstration:

```text
LOGIN
 ↓
DASHBOARD
 ↓
SELECT INTERSECTION
 ↓
NORMAL STATE
 ↓
ACTIVATE HEATWAVE
 ↓
TEMPERATURE INCREASES
 ↓
CLIMATE EXPOSURE INCREASES
 ↓
SELECT NORTH JUNCTION
 ↓
VIEW EXPOSURE BREAKDOWN
 ↓
GENERATE RECOMMENDATION
 ↓
VIEW 45s → 55s
 ↓
VIEW BEFORE/AFTER
 ↓
SAFETY VALIDATION
 ↓
ACCEPT & SIMULATE
 ↓
SIGNAL CHANGES
 ↓
EXPOSURE RECALCULATES
 ↓
DASHBOARD UPDATES
 ↓
ANALYTICS RECORDS REDUCTION
```

---

# 9. ACCEPTANCE CRITERIA

The final MVP is complete only when all of the following work.

## Climate

Dashboard displays:

* Temperature
* Feels-like temperature
* Rainfall
* Visibility
* Road condition

## Two-wheelers

Dashboard displays:

* 2W count
* 2W waiting time
* 2W exposure

## Pedestrians

Dashboard displays:

* Pedestrian count
* Pedestrian waiting time
* Pedestrian exposure

## Exposure

Every approach has:

* Score
* Risk
* Dominant factors

## Recommendation

Every recommendation contains:

* Old timing
* New timing
* Exposure before
* Exposure after
* Waiting before
* Waiting after
* Safety result
* Reason

## Simulation

After acceptance:

* Signal state changes
* Dashboard updates
* Exposure recalculates
* Before/after remains visible

---

# 10. PERFORMANCE TARGETS

Target:

```text
Dashboard API          < 2 seconds
Exposure calculation   < 200 ms
Recommendation         < 500 ms
Frontend interaction   < 200 ms
Real-time update       < 2 seconds
```

---

# 11. SECURITY

Required:

```text
HTTPS in production
JWT expiry
bcrypt
Role authorization
Parameterized SQL
Request validation
CORS restrictions
Login rate limiting
Secret management
No API keys in frontend
No password logging
Server-side signal validation
```

---

# 12. ENVIRONMENT

Create:

```text
NODE_ENV=development

PORT=5000

DATABASE_HOST=localhost
DATABASE_PORT=3306
DATABASE_NAME=climateguard
DATABASE_USER=root
DATABASE_PASSWORD=

JWT_SECRET=
JWT_EXPIRES_IN=1h

WEATHER_PROVIDER=
WEATHER_API_KEY=

MAP_PROVIDER=
MAP_API_KEY=

CLIENT_URL=http://localhost:5173

SOCKET_ENABLED=true

WEATHER_POLL_INTERVAL_MS=300000
EXPOSURE_RECALC_INTERVAL_MS=30000

MIN_RECOMMENDATION_CONFIDENCE=0.70
```

Do not put secrets in frontend code.

---

# 13. GIT / TEAM DEVELOPMENT RULES

The project is designed for four developers.

Branches:

```text
main

feature/dashboard-ui
feature/exposure-engine
feature/signal-optimizer
feature/backend-integration
```

## Module ownership

### 1.1

Own:

```text
client/
```

### 1.2

Own:

```text
server/src/services/exposure/
server/src/services/weather/
server/src/services/traffic/
```

### 1.3

Own:

```text
server/src/services/optimization/
server/src/services/simulation/
```

### 1.4

Own:

```text
database/
server/src/config/
server/src/controllers/
server/src/routes/
server/src/middleware/
server/src/repositories/
server/src/validators/
server/src/sockets/
server/src/services/analytics/
server/src/services/alerts/
```

Avoid simultaneous editing of:

```text
client/src/App.jsx
client/src/main.jsx
server/src/app.js
package.json
```

Keep these files minimal and stable.

---

# 14. IMPLEMENTATION ORDER

Implement in this order:

## Phase 1

Create:

```text
client
server
database
```

and configure environment.

## Phase 2

Create database schema and seed data.

## Phase 3

Implement authentication.

## Phase 4

Implement Module 2:

```text
Climate
 ↓
Exposure
 ↓
Risk
```

## Phase 5

Implement Module 3:

```text
Candidates
 ↓
Safety
 ↓
Simulation
 ↓
Recommendation
```

## Phase 6

Implement Module 1:

```text
Dashboard
 ↓
Interactive Junction
 ↓
Exposure
 ↓
Recommendation
```

## Phase 7

Integrate APIs.

## Phase 8

Add simulation scenarios.

## Phase 9

Add Socket.IO.

## Phase 10

Only after MVP works, consider optional:

```text
ML
LLM explanation
Real weather API
Computer vision
Map
Multi-intersection optimization
Notifications
```

---

# 15. FINAL UI REQUIREMENT

The dashboard MUST visually follow the provided reference design:

* Dark traffic-control interface
* Left analytical sidebar
* Center intersection/map
* Right signal-control panel
* High-contrast status indicators
* Live status
* Exposure severity
* Traffic density
* Climate information
* Signal timing
* Recommendation
* Before/after comparison
* Alerts
* Analytics

The **left side must primarily answer:**

> What is happening and how much exposure exists?

The **center must answer:**

> Where is the exposure happening?

The **right side must answer:**

> What signal action can safely reduce the exposure?

---

# 16. CORE PRODUCT PRINCIPLE

Do NOT build a normal smart-traffic dashboard with a weather widget.

Build the product around:

```text
CLIMATE HAZARD
       +
PEOPLE WAITING
       +
TWO-WHEELER / PEDESTRIAN EXPOSURE
       ↓
CLIMATE EXPOSURE SCORE
       ↓
SAFE ADAPTIVE SIGNAL
       ↓
LOWER HUMAN EXPOSURE
```

The strongest product statement is:

> ClimateGuard Traffic transforms traffic signals from systems that primarily manage vehicle movement into climate-aware systems that help reduce unnecessary outdoor exposure for people using the road.

---

# 17. FINAL AGENT TASK

Now implement the project from this specification.

Before writing code:

1. Inspect the repository.
2. Inspect the existing `SPEC.md`.
3. Preserve the existing project if code already exists.
4. Identify which parts are already implemented.
5. Do not duplicate existing functionality.
6. Create the required folder structure.
7. Implement the four modules with clear ownership.
8. Connect them through well-defined APIs.
9. Use simulated data for the MVP.
10. Make the dashboard functional, not merely static.
11. Ensure every clickable junction updates its details.
12. Ensure exposure calculations come from the backend engine.
13. Ensure recommendations come from the deterministic optimizer.
14. Ensure every recommendation passes the safety validator before simulation.
15. Ensure accepting a recommendation changes only the simulated signal.
16. Ensure the dashboard recalculates exposure after simulation.
17. Ensure analytics record the simulated result.
18. Add appropriate unit and integration tests.
19. Add seed data for the demo intersection.
20. Add the five simulation scenarios:

    * NORMAL
    * HEATWAVE
    * HEAVY RAIN
    * HIGH 2W DENSITY
    * HIGH PEDESTRIAN DENSITY
    * RESET
21. Do not add real traffic-light control.
22. Do not add unrequested external services.
23. Do not make up missing project decisions.
24. Keep the implementation suitable for a hackathon demonstration.
25. Run the project and fix build/runtime errors before considering the implementation complete.

## Definition of done

The application must allow a user to:

```text
LOGIN
→ VIEW DASHBOARD
→ SEE TRAFFIC DENSITY
→ SEE CLIMATE CONDITIONS
→ SEE CLIMATE EXPOSURE
→ CLICK NORTH/SOUTH/EAST/WEST
→ VIEW SEVERITY
→ VIEW EXPOSURE FACTORS
→ ACTIVATE HEATWAVE/RAIN/2W/PEDESTRIAN SCENARIO
→ SEE EXPOSURE CHANGE
→ GENERATE SIGNAL RECOMMENDATION
→ SEE SAFETY VALIDATION
→ SEE BEFORE/AFTER
→ ACCEPT RECOMMENDATION
→ SIMULATE SIGNAL CHANGE
→ SEE EXPOSURE RECALCULATED
→ VIEW ANALYTICS
```

The result must be a working **ClimateGuard Traffic prototype**, not a collection of disconnected pages.
