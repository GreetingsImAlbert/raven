# Raven 0 — System Architecture

Each system is a line of its own. Under it, each numbered item is a subsystem,
with its inputs (←) and outputs (→) as sub-items. Use "—" when there are none.
Systems are drawn in the diagram in the order listed here.

Communications & Data
1. Radio control
   1. ← user control signals
   2. → stick positions, mode switch, arm state, link status
2. Telemetry
   1. ← time-stamped flight logs
   2. → transmit to ground station
3. Logging
   1. ← state estimate, desired states, motor commands, sensor outputs, active flight mode, arm state, motor enable, battery status, failsafe trigger
   2. → time-stamped flight logs

Power System
1. Battery
   1. ← charge
   2. → battery power
2. PDB
   1. ← battery power
   2. → regulated power
3. Monitoring
   1. ← battery power
   2. → battery status

State Estimation
1. Attitude + rates
   1. ← IMU (acc, gyr, mag)
   2. → φ, θ, ψ, rates
2. Absolute altitude
   1. ← barometer
   2. → z pos
3. Absolute position
   1. ← GPS
   2. → x, y pos
4. Sensor fusion
   1. ← all outputs above
   2. → state estimate, state health checks

Safety
1. Failsafe
   1. ← link status, state health checks, battery status
   2. → failsafe trigger
2. Procedures
   1. ← —
   2. → pre-flight checklist, test plan and rules

Control
1. Mode manager (FSM)
   1. ← mode switch, arm state, failsafe trigger, battery status, state health checks, touchdown flag, disarm request, link status
   2. → active flight mode, motor enable
2. Automator (landing, GPS hold)
   1. ← active flight mode, state estimate
   2. → automated setpoints, touchdown flag, disarm request
3. Setpoint generator
   1. ← active flight mode, stick positions, state estimate, automated setpoints
   2. → desired states
4. Controller
   1. ← desired states, state estimate
   2. → thrust and torque commands
5. Motor mixer
   1. ← thrust and torque commands, motor enable
   2. → motor commands

Airframe
1. Structure
   1. ← —
   2. → —
2. Mounting interfaces
   1. ← component dimensions and mass
   2. → mounting points

Powertrain
1. ESC
   1. ← motor commands, regulated power
   2. → 3-phase motor drive
2. Motors
   1. ← 3-phase motor drive
   2. → shaft torque
3. Propellers
   1. ← shaft torque
   2. → thrust, yaw reaction torque

Avionics
1. Flight computer
   1. ← —
   2. → hosts all software