|1.| Module: automatic_door_controller
This module implements the logic of an automatic door controller using an FSM with four states.
\\\\\\\\Inputs:
----clk: Clock signal for synchronization.
----reset: Resets the FSM to its initial state (IDLE).
----motion_detected: Indicates if motion is detected near the door.
----close_request: Signal to request the door to close.
\\\\\\\\Output:
door_open: Signal indicating whether the door is open.
\\\\\\\\\FSM States:
-----IDLE (2'b00):
The door is closed and waiting for motion detection.
If motion_detected is high, the FSM transitions to OPENING.
-----OPENING (2'b01):
The door is opening.
The door_open signal is set to 1.
After opening, the FSM transitions to OPEN.
-----OPEN (2'b10):
The door remains open.
The door_open signal is set to 1.
If close_request is high, the FSM transitions to CLOSING.
-----CLOSING (2'b11):
The door is closing.
If no motion is detected, the FSM transitions to IDLE.
Logic Implementation:
\\\\\\\\\\State Update:
On every clock edge, the FSM updates the current_state based on the next_state.
\\\\\\\\Next State and Output Logic:
The next_state and door_open values are determined based on the current state and input signals (motion_detected and close_request).


|2.| Module: tb_automatic_door_controller
This is the testbench for simulating the behavior of the door controller.
\\\\\\\\Signals:
-----clk: Simulated clock signal toggling every 5 time units.
-----reset: Resets the FSM to its initial state (IDLE).
-----motion_detected: Simulates motion near the door.
-----close_request: Simulates a request to close the door.
-----door_open: Observes the door's open status.
\\\\\\\\\\\Simulation Steps:
\\\\\\\\\\\\Clock Initialization:
The clock toggles every 5 time units using the forever loop.
Simulation Scenario:
At the start, reset is high to reset the FSM.
After 10 units, reset is set low to start the FSM.
Motion is simulated by setting motion_detected = 1.
Later, close_request is set to 1 to close the door.
\\\\\\\\\Output Monitoring:
$monitor prints the values of motion_detected, close_request, and door_open at every simulation time step.


|3.|Key Points in Simulation
When motion is detected (motion_detected = 1), the door starts opening (door_open = 1).
Once open, if a close request (close_request = 1) is received, the door starts closing.
The FSM transitions between states (IDLE, OPENING, OPEN, CLOSING) based on the inputs.
\\\\\\\\\\\Sample Simulation Output
# Time 10: Motion=0, CloseReq=0, DoorOpen=0
# Time 20: Motion=1, CloseReq=0, DoorOpen=1
# Time 40: Motion=0, CloseReq=1, DoorOpen=1
# Time 50: Motion=0, CloseReq=0, DoorOpen=0
This shows how the door transitions through its states based on inputs, ensuring safe and logical operation.







