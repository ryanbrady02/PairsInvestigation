#Plotting concentration against time 
import numpy as np
import matplotlib.pyplot as plt
from scipy.integrate import odeint

# Define the system of differential equations
def model(y, t):
    Y, Z, M = y
    a, b, c, e, f, g, h, k = 1, 100, 1, 1, 1, 1, 1, 1  # Replace these with your parameter values
    dydt = c / (a + b * M) - k * Y
    dzdt = e * Y - f * Z
    dmdt = g * Z - h * M
    return [dydt, dzdt, dmdt]

# Initial conditions
initial_conditions = [0.0, 0.0, 0.0]  # Y(0), Z(0), M(0)

# Time points to solve the equations
t = np.linspace(0, 10, 1000)

# Solve the system of differential equations
solution = odeint(model, initial_conditions, t)

# Extract solutions for Y, Z, and M
Y, Z, M = solution.T

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(t, Y, label='mRNA (Y)')
plt.plot(t, Z, label='Protein (Z)')
plt.plot(t, M, label='Repressor (M)')
plt.title('Dynamics of mRNA, Protein, and Repressor', fontsize=24)
plt.xlabel('Time', fontsize=24)
plt.ylabel('Concentration', fontsize=24)
plt.legend(fontsize=20)
plt.grid(True)
plt.show()
