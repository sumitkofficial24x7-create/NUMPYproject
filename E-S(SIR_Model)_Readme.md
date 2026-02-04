# ============================================================
# EPIDEMIC SIMULATION (SIR MODEL)
# FINAL MAJOR PROJECT
# ============================================================
# Author        : Robin
# Libraries     : NumPy, Matplotlib ONLY
# Project Type  : Simulation-Based Data Science Major Project
#
# PURPOSE OF THIS PROJECT:
# ------------------------
# This project simulates how a disease spreads in a population
# over time using mathematics and probability.
#
# We DO NOT use real disease data.
# Instead, we CREATE our own data using scientific formulas.
#
# This helps beginners understand:
# - How epidemics start
# - Why infections increase rapidly
# - How recovery, lockdown, and vaccination help control disease
# ============================================================


# ------------------------------------------------------------
# IMPORT REQUIRED LIBRARIES
# ------------------------------------------------------------
# NumPy is used for mathematical calculations and arrays
# Matplotlib is used to draw graphs for visual understanding
import numpy as np
import matplotlib.pyplot as plt


# ------------------------------------------------------------
# BASIC POPULATION SETTINGS
# ------------------------------------------------------------
# N = Total number of people in the population
N = 1000

# I0 = Number of people infected on Day 0
I0 = 1

# R0 = Number of people already recovered on Day 0
R0 = 0

# S0 = People who can get infected
# Total population = Susceptible + Infected + Recovered
S0 = N - I0 - R0


# ------------------------------------------------------------
# TIME SETTINGS
# ------------------------------------------------------------
# Total number of days we want to simulate the epidemic
days = 180

# Creating an array of days: [0, 1, 2, ..., 179]
# This helps us track changes over time
time = np.arange(days)


# ------------------------------------------------------------
# FUNCTION: SIR MODEL SIMULATION
# ------------------------------------------------------------
# This function runs the SIR mathematical model
# It calculates how S, I, R change every day
#
# PARAMETERS:
# beta  -> infection rate (how fast disease spreads)
# gamma -> recovery rate (how fast people recover)
# vaccination_rate -> how many susceptible people get vaccinated daily
#
# RETURNS:
# Arrays of S, I, R values for each day
def run_sir_model(beta, gamma, vaccination_rate=0.0):

    # Create empty arrays to store values for each day
    S = np.zeros(days)
    I = np.zeros(days)
    R = np.zeros(days)

    # Set initial population values on Day 0
    S[0] = S0
    I[0] = I0
    R[0] = R0

    # Loop through each day to update values
    for t in range(1, days):

        # ----------------------------------------------------
        # CALCULATING NEW INFECTIONS
        # ----------------------------------------------------
        # Formula:
        # New Infected = beta * S * I / N
        #
        # Meaning in simple words:
        # - More infected people → more spread
        # - More susceptible people → more chances
        # - Dividing by N keeps values realistic
        new_infected = beta * S[t-1] * I[t-1] / N

        # ----------------------------------------------------
        # CALCULATING RECOVERIES
        # ----------------------------------------------------
        # Formula:
        # New Recovered = gamma * I
        #
        # Meaning:
        # A fixed fraction of infected people recover daily
        new_recovered = gamma * I[t-1]

        # ----------------------------------------------------
        # CALCULATING VACCINATION EFFECT
        # ----------------------------------------------------
        # Vaccinated people move directly from S to R
        # This reduces future infections
        vaccinated = vaccination_rate * S[t-1]

        # ----------------------------------------------------
        # UPDATING POPULATION VALUES
        # ----------------------------------------------------
        # Susceptible decreases due to infection & vaccination
        S[t] = S[t-1] - new_infected - vaccinated

        # Infected increases by new infections and decreases by recovery
        I[t] = I[t-1] + new_infected - new_recovered

        # Recovered increases by recovery and vaccination
        R[t] = R[t-1] + new_recovered + vaccinated

    # Return final results
    return S, I, R


# ------------------------------------------------------------
# SCENARIO 1: NORMAL EPIDEMIC (NO CONTROL)
# ------------------------------------------------------------
# High infection rate
# No lockdown
# No vaccination
beta_normal = 0.35
gamma_normal = 0.1

S1, I1, R1 = run_sir_model(beta_normal, gamma_normal)


# ------------------------------------------------------------
# SCENARIO 2: LOCKDOWN SCENARIO
# ------------------------------------------------------------
# Lockdown reduces contact between people
# This is modeled by lowering infection rate
beta_lockdown = 0.18
gamma_lockdown = 0.1

S2, I2, R2 = run_sir_model(beta_lockdown, gamma_lockdown)


# ------------------------------------------------------------
# SCENARIO 3: VACCINATION STRATEGY
# ------------------------------------------------------------
# Some susceptible people get vaccinated daily
# This moves them directly to recovered group
beta_vaccine = 0.35
gamma_vaccine = 0.1
vaccination_rate = 0.02   # 2% vaccinated per day

S3, I3, R3 = run_sir_model(beta_vaccine, gamma_vaccine, vaccination_rate)


# ------------------------------------------------------------
# VISUALIZATION 1: SIR CURVES (NORMAL CASE)
# ------------------------------------------------------------
# This graph shows how S, I, R change over time
# Helps understand epidemic lifecycle
plt.figure(figsize=(10, 6))
plt.plot(time, S1, label="Susceptible")
plt.plot(time, I1, label="Infected")
plt.plot(time, R1, label="Recovered")

plt.title("SIR Model - Normal Epidemic Scenario")
plt.xlabel("Days")
plt.ylabel("Population")
plt.legend()
plt.grid(True)
plt.show()


# ------------------------------------------------------------
# VISUALIZATION 2: COMPARISON OF INFECTION CONTROL STRATEGIES
# ------------------------------------------------------------
# This graph compares how infection behaves under:
# - No control
# - Lockdown
# - Vaccination
plt.figure(figsize=(10, 6))
plt.plot(time, I1, label="Normal")
plt.plot(time, I2, label="Lockdown")
plt.plot(time, I3, label="Vaccination")

plt.title("Comparison of Infection Control Strategies")
plt.xlabel("Days")
plt.ylabel("Infected Population")
plt.legend()
plt.grid(True)
plt.show()


# ------------------------------------------------------------
# VISUALIZATION 3: AREA CHART (VACCINATION CASE)
# ------------------------------------------------------------
# Area chart shows population distribution clearly
# Useful for non-technical understanding
plt.figure(figsize=(10, 6))
plt.stackplot(
    time,
    S3,
    I3,
    R3,
    labels=["Susceptible", "Infected", "Recovered"]
)

plt.title("Population Distribution with Vaccination")
plt.xlabel("Days")
plt.ylabel("Population")
plt.legend(loc="upper right")
plt.show()


# ------------------------------------------------------------
# ANALYSIS: PEAK INFECTION DETAILS
# ------------------------------------------------------------
# Finding the day with maximum infections
peak_day = np.argmax(I1)

# Finding how many people were infected at peak
peak_infected = np.max(I1)

print("PEAK INFECTION ANALYSIS (Normal Scenario)")
print("----------------------------------------")
print(f"Peak Day           : {peak_day}")
print(f"Maximum Infected   : {int(peak_infected)} people")
print(f"Total Population   : {N}")
