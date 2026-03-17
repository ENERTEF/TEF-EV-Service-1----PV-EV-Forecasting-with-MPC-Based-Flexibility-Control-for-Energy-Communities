TEF_EV-ECC_FLEXIBILITY
========================

**AI-based forecasting and flexibility services for Energy Communities with EV charging**

Overview (version 1.0)
----------------------

**TEF_EV-ECC_FLEXIBILITY** implements data-driven forecasting and optimisation services for photovoltaic (PV) generation and electric vehicle (EV) charging demand in an Energy Community (ECC) context. The project supports flexibility assessment and smart charging strategies for a supermarket-based EV hub, developed within the TEF-EV framework.

The implemented framework combines **AI-based forecasting models with Model Predictive Control (MPC)** to enable coordinated EV charging and renewable-aware energy management. The services operate at **15-minute resolution** and provide **24-hour ahead forecasts**, enabling proactive energy management, PV self-consumption maximization, and grid interaction optimization.

Implemented AI Services
-----------------------

### PV Forecasting Service

*   Hybrid **LSTM-based forecasting model**

*   Inputs: historical PV production, Open-Meteo weather data, cyclical time features

*   Outputs:

    *   One-step-ahead PV power forecasts
        
    *   Recursive **24-hour ahead PV generation forecasts**
        
    *   Short-term PV production profiles for energy management
        

### EV Charging Demand Forecasting Service

*   Hybrid **CNN–LSTM-based forecasting model**

*   Inputs: historical EV load, lagged and rolling statistics, time-of-day / day-of-week features, optional PV coupling

*   Outputs:

    *   One-step-ahead EV charging demand forecasts
        
    *   Recursive **24-hour ahead EV charging demand forecasts**
        
    *   Baseline EV demand profiles for flexibility optimization
        

### EV Flexibility Optimization Service

*   **Model Predictive Control (MPC)** optimization framework

*   Inputs:

    *   PV generation forecasts
        
    *   EV baseline demand forecasts
        
    *   electricity price signals
        
    *   operational charging constraints
        

*   Outputs:

    *   Optimized EV charging trajectories
        
    *   Grid import/export power profiles
        
    *   Cost-aware charging schedules
        
    *   Flexibility indicators for energy community operation
        

Data Sources
------------

*   **Smart meter measurements** (15-minute resolution)

    *   PV production (PV_TotalProduction_kW)
        
    *   EV charging consumption (EMOB1, EMOB2)
        
    *   Aggregated EV demand profiles
        

*   **Meteorological data** from **Open-Meteo**

    *   Solar radiation
        
    *   Cloud cover
        
    *   Temperature
        
    *   Wind speed
        

Use Case
--------

*   Supermarket-based EV charging hub

*   Energy Community settlement with rooftop PV generation

*   Aggregated EV charging infrastructure (EMOB1 / EMOB2)

*   AI-enabled flexibility services for renewable-aware charging

*   Developed within **TEF-EV Luxembourg experimental environment**

Outputs (version 1.0)
---------------------

*   Trained forecasting models (PV LSTM, EV CNN–LSTM)

*   One-step and 24-hour ahead PV forecasts

*   One-step and 24-hour ahead EV demand forecasts

*   MPC-based EV charging optimisation results

*   Grid import/export power profiles

*   Performance metrics (MAE, RMSE, R²)

*   Rolling forecasting backtests and optimisation evaluations
