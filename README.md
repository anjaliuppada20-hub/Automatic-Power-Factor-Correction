# Automatic-Power-Factor-Correction

import math

print("======================================")
print(" AUTOMATIC POWER FACTOR CORRECTION")
print("======================================")

# Input electrical parameters
voltage = float(input("Enter AC Voltage (V): "))
current = float(input("Enter Current (A): "))
frequency = float(input("Enter Frequency (Hz): "))
power_factor = float(input("Enter Existing Power Factor: "))

target_pf = 0.95

# Apparent power
apparent_power = voltage * current

# Real power
real_power = apparent_power * power_factor

# Reactive power before correction
reactive_power = math.sqrt(
    apparent_power ** 2 - real_power ** 2
)

# Target reactive power
target_reactive_power = real_power * math.tan(
    math.acos(target_pf)
)

# Required capacitor reactive power
capacitor_kvar = (
    reactive_power - target_reactive_power
) / 1000

# Capacitor value for a single-phase system
if capacitor_kvar > 0:
    capacitance = (
        capacitor_kvar * 1000
        / (2 * math.pi * frequency * voltage ** 2)
    )
else:
    capacitance = 0

print("\n========== RESULTS ==========")

print(f"Real Power: {real_power:.2f} W")
print(f"Apparent Power: {apparent_power:.2f} VA")
print(f"Initial Power Factor: {power_factor:.2f}")
print(f"Target Power Factor: {target_pf:.2f}")

print(f"Required Capacitor: {capacitor_kvar:.2f} kVAR")
print(f"Capacitance: {capacitance * 1e6:.2f} uF")

if capacitor_kvar > 0:
    print("\nAPFC Status: Capacitor Compensation Required")
else:
    print("\nAPFC Status: No Capacitor Compensation Required")

print("\nSimulation Completed")
