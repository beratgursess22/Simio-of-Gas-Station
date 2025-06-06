Fuel Station Simulation Project – Full Detailed Description

--Project Title: Discrete-Event Simulation of a Fuel Station

--Simulation Tool: Simio

1. 📌 Problem Overview and Objectives
   
This project models a high-traffic fuel station in Kağıthane, İstanbul, which serves approximately 600 vehicles daily. Main issues observed in the real system include:

--Long queues and customer waiting times

--Uneven utilization of fuel pumps and cashier

--Delays in payment processing


--Limited number of staff and station space

🎯 Project Goal:

Serve at least 85% of customers within 7 minutes, using no more than 8 staff members.

The simulation is built to evaluate:

--System efficiency

--Congestion levels

--Resource allocation strategies

The model includes realistic vehicle arrival patterns, fuel-based routing, secondary resource constraints (pump attendants), and behaviors such as balking (leaving due to long queues).



![Ekran-Resmi-2025-06-06-11 42 38](https://github.com/user-attachments/assets/cf5edfd9-2674-4f61-b1f1-ef33399d36e1)


2. 🧱 System and Conceptual Model
We built the conceptual model based on direct field observations and interviews. Key components:

Vehicle types:

--Gasoline/Diesel (78%)

--LPG (20%)

--Electric (2%)

Routing:
Vehicles are assigned to fuel types using Table Routing with three node lists: Nodelist_benzin_or_diesel, Nodelist_gas, and Nodelist_elec.

Separator-Combiner Logic:
Drivers separate from their vehicles after arrival. 50% walk to the cashier, others wait near their cars. Numerical weights (ModelEntity.path_no) control driver-path matching for return.

Queuing Discipline:
FIFO with infinite queue capacities.

-- Figure 1.1 System --
![Ekran-Resmi-2025-06-06-11 46 37](https://github.com/user-attachments/assets/d0dc2911-507d-4d2a-a08a-dfc25ee25049)
                                   
-- Figure 1.2 System Flow Chart --                                      
![Ekran Resmi 2025-06-06 11 46 23](https://github.com/user-attachments/assets/97ee1bc0-111d-4961-9014-7665cc81f2d5)
         
                                    
3. ⚙️ Simulation Model Implementation (Simio)

Vehicles arrive following a Poisson process (Lognormal interarrival times).

Each vehicle has Fuel Type and Payment Method as state variables.

Fuel pumps require a secondary resource (attendant) to operate.

The cashier has 3-shift coverage but is modeled as a single server.

Logic includes:

--Balking behavior

--Routing based on vehicle type

--Status Labels (e.g., Number of Entities, Balked Vehicles)

--Step-run and Breakpoint debugging

-- Figure 1.3 System Screenshot --

![Resim2](https://github.com/user-attachments/assets/b6201e3e-c7e3-417f-83ec-973afc73a7e3)

![Resim1](https://github.com/user-attachments/assets/fa21b7d2-492d-451b-a3ad-e2f2299d4751)

-- Figure 1.4 bird's eye view of the system --
![Resim3](https://github.com/user-attachments/assets/b4165fee-ef28-4601-ba3f-8456b4b294cc)

4. ✅ Verification of the Model
The Simio simulation outputs were compared to analytical queueing theory calculations for each service point (gas, benzin, electric, cashier).

-Utilization (ρ), queue length (Lq), and waiting time (Wq) values were closely aligned for the cashier and overall system.

-Discrepancies in gas and electric points were attributed to:

--High variability in arrival/service times

--Server assignment randomness

--Modeling simplifications (e.g., ignoring license plate recognition)

Conclusion: Model is partially verified but falls within acceptable tolerance.

-- Figure 1.5 system Conceptual Model --

![Resim1](https://github.com/user-attachments/assets/d4fb2683-5606-42fb-bfb2-05e214881039)
![Resim2](https://github.com/user-attachments/assets/9f7b1809-4431-4727-b3cc-ce9c89d0356a)
![Resim3](https://github.com/user-attachments/assets/1ce94c89-1728-4c0d-9fe1-42d696899b26)

5. 📊 Input Data Collection and Modelling
-100 samples collected between 10:00–13:00 for:

--Interarrival time

--Service times for benzin, gas, electric, cashier

--Fuel types and payment methods

Distributions used (p > 0.05 for all):

--Interarrival: Lognormal(μ = 2.3277, σ = 0.9885)

--Benzin: Beta(α₁ = 0.04448, α₂ = 1.4484)

--Gas: Normal(μ = 87.735, σ = 32.098)

--Cashier: Gamma(107.02, 0.79198)

--Electric: Lognormal(μ = 0.1569, σ = 7.8448)

-- Figure 1.6 Service Time Histogram (Gas) --

![Resim1](https://github.com/user-attachments/assets/68638e17-931f-4d55-8429-d7fe67d3e023) 

-- Figure 1.7 Service Time Histogram (Benzin) --

![Resim2](https://github.com/user-attachments/assets/c58b0db3-6de2-4360-810a-eaf15740171c)

-- Figure 1.8 Service Time Histogram (Cashier) --

![Resim3](https://github.com/user-attachments/assets/dcd364ad-ffc6-43a1-b5ed-23f789e59a52)

-- Figure 1.9 Service Time Histogram (Interarrival Time) --

![Resim4 ,jpg](https://github.com/user-attachments/assets/4ce32821-7833-4584-87bd-46f4cc0f3116)

-- Figure 1.10 Final Table --

<img width="514" alt="Resim9" src="https://github.com/user-attachments/assets/d00ecd29-155c-4fa7-be9e-65d1b36c51d2" />



6, 🧪 Model Validation

We compared simulation results with field-measured values. For 8 key metrics:

![Resim1](https://github.com/user-attachments/assets/f4acfc93-e305-4665-85ff-d96855acee15)

7. 📈 Output Analysis
   
The system was simulated as non-terminating with no downtimes. Outputs tracked:

-Queue lengths

-Waiting times

-Resource utilization

-Financial metrics:

--Revenue

--Cost

--Profit

Example results:

--Avg number in system: 39.9

--Avg cashier queue: 21.7

--Electric utilization: 45%

--Profit: 25,864 units

-- Figure 1.11 System Output Analysis -- 
 
![Resim1](https://github.com/user-attachments/assets/616ce40b-b4da-4340-a247-b1ce19864364)

8. 🔁 Alternative Scenario Analysis

Five scenarios were tested by changing:

-Service times

-Number of pumps or cashier capacity

-Staff allocation

🔍 Results:

Scenario 1: Best across all performance KPIs (but high variability)

Scenario 2: Balanced and stable

Scenario 5: Most efficient in electric/gas queues

Scenario 3: High profit, but system congestion

Scenario 4: Underperforming in queues and utilization


-- Figure 1.12 Scnerio -- 

![Resim1](https://github.com/user-attachments/assets/7550007b-7092-4510-b548-b958c3e4c4e1)



