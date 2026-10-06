# VISION VECTORS

## Train Delay Prediction and Passenger Advisory System

VISION VECTORS is a machine-learning-based railway application designed
to predict the likely delay of a train journey in advance and provide
passengers with an early advisory. It also provides railway operations
teams with route-level delay-risk analytics and administrators with
model-accuracy information.

> **Hackathon:** Codegnan Hackathon\
> **Domain:** Computer Vision / Machine Learning\
> **Location:** Codegnan Vizag

## Problem Statement

Passengers often do not have reliable advance visibility into whether
their train is likely to be delayed. Delay information may become
available only a few hours before departure, when travel plans are
difficult to change.

Railway operations teams also need a forward-looking view of routes,
seasons, days, and time periods that are more prone to delays instead of
relying only on reactive, day-of monitoring.

## Goal

The system predicts the likely train delay in minutes or provides a
delay-risk category using historical railway running data.

Relevant inputs include:

-   Train number and route
-   Origin and destination
-   Travel date
-   Route distance
-   Season/month
-   Day of week
-   Historical punctuality/running data

The result is presented as an early passenger advisory while also
supporting route-level analysis for operations teams.

## Key Features

### Passenger

-   Search for a train/route and travel date.
-   Get a predicted delay in minutes.
-   View a confidence indicator/range.
-   Receive a delay-risk category where applicable.
-   Save prediction history and frequently travelled routes after
    registration.
-   Guest users can check predictions without registering.

### Operations Analyst

-   Access an internal operations dashboard.
-   View route-wise average delay.
-   View on-time percentages.
-   Analyze delay risk by season/month and day of week.
-   Identify delay-prone routes and time slots.

### Admin

-   Manage the historical dataset.
-   Review model accuracy.
-   Track MAE and RMSE on held-out data.
-   Review model/training metadata.

## End-to-End Workflow

1.  Passenger selects a train/route and travel date.
2.  The system retrieves relevant historical running data.
3.  The prediction model estimates the expected delay and confidence
    range.
4.  The passenger receives an advisory and can plan accordingly.
5.  Operations analysts review route-level delay-risk trends.
6.  Administrators periodically review model accuracy.

## Data

The application works with a public railway punctuality dataset or
simulated railway data.

The expected historical data includes:

-   Train number
-   Route
-   Origin
-   Destination
-   Scheduled arrival/departure
-   Actual arrival/departure
-   Distance
-   Season/month
-   Day of week
-   Historical delay information

Each prediction can be logged with:

-   Query input
-   Predicted delay
-   Confidence
-   Prediction date

## Machine Learning

The project can use a regression model to predict delay duration.

Suggested models include:

-   Random Forest
-   Gradient Boosting

An alternative passenger-friendly output is delay-risk banding:

-   Low Risk
-   Medium Risk
-   High Risk

Feature importance can also be used to explain which factors, such as
season, route length, and day of week, have the greatest influence on
predictions.

## Model Evaluation

Model performance is evaluated using held-out data.

Primary metrics:

-   **MAE (Mean Absolute Error):** measures the average absolute
    difference between predicted and actual delay.
-   **RMSE (Root Mean Squared Error):** gives greater weight to larger
    prediction errors.

These metrics are exposed in the admin/model-accuracy view.

## Database Design

The main entities are:

  Entity                    Purpose
  ------------------------- ------------------------------------------------
  `Trains`                  Stores core train records
  `Routes`                  Stores origin, destination and distance
  `HistoricalRunningData`   Stores scheduled vs. actual timings
  `DelayPredictions`        Stores model outputs for passenger queries
  `ModelMetadata`           Stores model accuracy and training information

The database can use **SQLite or PostgreSQL**.

## Technology Stack

  Layer              Technology
  ------------------ -----------------------------------------
  Frontend           Streamlit
  Backend            Python
  Database           SQLite / PostgreSQL
  Data Processing    Pandas
  Machine Learning   scikit-learn
  Forecasting        statsmodels / Prophet, where applicable
  Visualization      Plotly / Matplotlib
  Deployment         Streamlit Cloud

## Expected Application Modules

``` text
Passenger
 ├── Journey Query
 ├── Delay Prediction
 └── Prediction History

Operations
 ├── Route Analytics
 ├── Seasonal/Day-wise Risk
 └── Delay-prone Route Analysis

Admin
 ├── Dataset Management
 ├── Model Accuracy
 └── Training / Model Metadata
```

## Suggested Project Structure

``` text
VISION-VECTORS/
│
├── app.py
├── requirements.txt
├── README.md
│
├── data/
│   └── railway_data.csv
│
├── models/
│   └── delay_prediction_model.pkl
│
├── src/
│   ├── data_processing.py
│   ├── feature_engineering.py
│   ├── model_training.py
│   ├── prediction.py
│   └── database.py
│
├── pages/
│   ├── passenger.py
│   ├── operations.py
│   └── admin.py
│
└── tests/
    └── test_prediction.py
```

> The structure above is a suggested organization. Update the filenames
> and folders to match the actual repository implementation.

## Installation

### 1. Clone the repository

``` bash
git clone <YOUR_REPOSITORY_URL>
cd VISION-VECTORS
```

### 2. Create a virtual environment

Windows:

``` bash
python -m venv venv
venv\Scripts\activate
```

Linux/macOS:

``` bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

``` bash
pip install -r requirements.txt
```

### 4. Prepare the dataset

Place the railway historical running dataset in the project's configured
`data/` directory.

The dataset should contain the fields required by the preprocessing and
prediction pipeline.

### 5. Run the application

For a Streamlit application:

``` bash
streamlit run app.py
```

The application will open in the browser.

## Example Passenger Flow

``` text
Train / Route
      ↓
Travel Date
      ↓
Historical Data Retrieval
      ↓
Feature Preparation
      ↓
ML Prediction
      ↓
Predicted Delay + Confidence
      ↓
Passenger Advisory
```

## Analytics Dashboard

The operations dashboard is designed to provide:

-   Route-wise average delay
-   On-time percentage
-   Seasonal/monthly delay-risk trends
-   Day-of-week delay trends
-   Most delay-prone routes
-   Delay-prone time slots

## Authentication and Access Control

The system supports role-based access:

  Role                 Access
  -------------------- --------------------------------------------------
  Passenger            Journey predictions and saved prediction history
  Operations Analyst   Operations analytics dashboard
  Admin                Dataset/model management and accuracy metrics

Passengers may use the prediction functionality as guests or register to
save frequently travelled routes.

## Validation and Error Handling

The application should validate:

-   Required journey fields
-   Train/route selection
-   Travel date
-   Dataset availability
-   Model availability
-   Invalid or incomplete prediction requests

User-friendly error messages should be displayed instead of exposing
internal application errors.

## Testing

Core flows should be tested before deployment, including:

-   Passenger prediction flow
-   Prediction history
-   Route analytics
-   Model prediction output
-   Database operations
-   Authentication and role access
-   Invalid input handling

## Deployment

The proposed deployment platform is **Streamlit Cloud**.

Before deployment:

1.  Add all required Python packages to `requirements.txt`.
2.  Ensure the application entry point is correct.
3.  Include the required dataset/model files or configure their
    deployment path.
4.  Configure database access if PostgreSQL is used.
5.  Test the complete passenger, operations, and admin flows.

## Future Scope

Potential extensions include:

-   More advanced forecasting models.
-   Real-time railway data integration.
-   More detailed route and station-level prediction.
-   Improved confidence estimation.
-   Additional operational risk indicators.
-   Automated retraining as new railway running data becomes available.
-   More explainable model outputs for passengers and operations teams.

## Demo Flow

The final demonstration follows this sequence:

1.  Passenger selects a train/route and travel date.
2.  System predicts the expected delay with a confidence range.
3.  Passenger saves the route for future reference.
4.  Operations analyst views route-wise delay-risk trends.
5.  Admin reviews model accuracy metrics.

## Hackathon Deliverables

The project is intended to demonstrate:

-   A working application rather than static screens.
-   A clean and usable interface.
-   Functional backend business logic.
-   A connected database with meaningful relationships.
-   Input validation and error handling.
-   Authentication and role-based access where applicable.
-   Basic testing of core flows.
-   Shared source code.
-   A live end-to-end demo.

## Team

**VISION VECTORS --- Codegnan Hackathon**

Add team member names and individual contributions here:

``` text
1. Name — Role / Contribution
2. Name — Role / Contribution
3. Name — Role / Contribution
4. Name — Role / Contribution
```

## License

This project was developed as part of the Codegnan Hackathon. Add the
appropriate license here if the repository is intended for public
distribution.
"# RailVision" 
"# RailVision" 
