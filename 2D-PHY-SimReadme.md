# ============================================================
# 2D PHYSICS SIMULATION – PARTICLE MOTION
# FINAL MAJOR PROJECT (NUMPY + MATPLOTLIB ONLY)
# ============================================================
# Author        : Robin
# Project Type  : Simulation-Based Data Science Project
#
# WHAT THIS PROJECT IS ABOUT:
# ------------------------------------------------------------
# This project simulates how particles (like balls or objects)
# move in a 2D space under the effect of gravity.
#
# Particles move, fall down due to gravity, and bounce
# back when they hit the walls.
#
# This project helps beginners understand:
# • Motion in 2D space
# • Velocity, acceleration, and gravity
# • How simulations are built using mathematics
# • How NumPy handles data efficiently
# • How Matplotlib visualizes motion
# ============================================================


# ------------------------------------------------------------
# IMPORT REQUIRED LIBRARIES
# ------------------------------------------------------------
# NumPy is used for:
# • Mathematical calculations
# • Handling arrays (positions, velocities)
#
# Matplotlib is used for:
# • Drawing graphs
# • Animating particle motion
#
# FuncAnimation allows updating the same plot repeatedly
# to create animation
# ------------------------------------------------------------
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


# ------------------------------------------------------------
# NOTEBOOK SAFE DISPLAY MODE
# ------------------------------------------------------------
# This setting ensures:
# • No JavaScript errors
# • No IPython errors
# • Works in Jupyter Notebook, VS Code, and other environments
#
# The animation will render safely inside the notebook
# ------------------------------------------------------------
%matplotlib inline


# ------------------------------------------------------------
# SIMULATION PARAMETERS
# ------------------------------------------------------------
# num_particles :
# Total number of particles moving in the simulation
#
# width, height :
# Size of the 2D simulation box
#
# dt :
# Time step (how much time passes in one update)
#
# gravity :
# Acceleration due to gravity (downward force)
# Represented as a vector [x, y]
# ------------------------------------------------------------
num_particles = 15
width, height = 10, 10
dt = 0.1
gravity = np.array([0, -0.4])


# ------------------------------------------------------------
# INITIALIZE PARTICLE POSITIONS
# ------------------------------------------------------------
# Each particle has:
# • X position
# • Y position
#
# np.random.rand generates values between 0 and 1
# We multiply by width and height to place particles
# randomly inside the box
# ------------------------------------------------------------
positions = np.random.rand(num_particles, 2) * [width, height]


# ------------------------------------------------------------
# INITIALIZE PARTICLE VELOCITIES
# ------------------------------------------------------------
# Velocities decide:
# • How fast the particles move
# • In which direction they move
#
# Random velocities are assigned so that motion
# looks natural and different for each particle
# ------------------------------------------------------------
velocities = (np.random.rand(num_particles, 2) - 0.5) * 4


# ------------------------------------------------------------
# ACCELERATION ASSIGNMENT
# ------------------------------------------------------------
# All particles experience the same gravity
#
# np.tile repeats the gravity vector for all particles
# so calculations can be vectorized using NumPy
# ------------------------------------------------------------
accelerations = np.tile(gravity, (num_particles, 1))


# ------------------------------------------------------------
# CREATE FIGURE AND PLOT
# ------------------------------------------------------------
# A scatter plot is used because:
# • Each particle is a point
# • Positions update every frame
#
# This graph will be updated repeatedly to show motion
# ------------------------------------------------------------
fig, ax = plt.subplots(figsize=(6, 6))

scatter = ax.scatter(
    positions[:, 0],   # X coordinates
    positions[:, 1],   # Y coordinates
    s=60               # Size of particles
)

ax.set_xlim(0, width)
ax.set_ylim(0, height)
ax.set_title("2D Particle Motion Simulation")
ax.set_xlabel("X Position")
ax.set_ylabel("Y Position")
ax.grid(True)


# ------------------------------------------------------------
# UPDATE FUNCTION (CORE LOGIC)
# ------------------------------------------------------------
# This function runs again and again for each frame
#
# PHYSICS FORMULAS USED:
# ------------------------------------------------------------
# Velocity Update:
# v = v + a × t
#
# Position Update:
# x = x + v × t
#
# WALL COLLISION:
# • If a particle hits a wall
# • Reverse its velocity direction
# ------------------------------------------------------------
def update(frame):
    global positions, velocities

    # Update velocity using acceleration
    velocities += accelerations * dt

    # Update position using velocity
    positions += velocities * dt

    # Handle wall collisions
    for i in range(num_particles):

        # Left or Right wall collision
        if positions[i, 0] <= 0 or positions[i, 0] >= width:
            velocities[i, 0] *= -1

        # Bottom or Top wall collision
        if positions[i, 1] <= 0 or positions[i, 1] >= height:
            velocities[i, 1] *= -1

    # Update particle positions on the graph
    scatter.set_offsets(positions)

    return scatter,


# ------------------------------------------------------------
# CREATE ANIMATION OBJECT
# ------------------------------------------------------------
# FuncAnimation repeatedly calls the update function
#
# frames  : Number of simulation steps
# interval: Time between frames (milliseconds)
#
# The animation object must be stored in a variable
# to prevent automatic deletion
# ------------------------------------------------------------
anim = FuncAnimation(
    fig,
    update,
    frames=300,
    interval=50
)


# ------------------------------------------------------------
# DISPLAY OUTPUT
# ------------------------------------------------------------
# Shows the animated simulation
#
# The same graph updates continuously
# to give the effect of motion
# ------------------------------------------------------------
plt.show()
