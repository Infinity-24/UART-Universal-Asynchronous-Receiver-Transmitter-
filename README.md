# UART-Universal-Asynchronous-Receiver-Transmitter-
Universal Asynchronous Receiver/ Transmitter is such a hardware circuit that uses asynchronous serial communication for data transmission.
Clearly, to implement UART on Verilog, we will need to convert data from parallel to serial at the transmitter end, and, serial to parallel at the receiver end.
There are a few ways we can go about this:
We can use register blocks, i.e., Parallel-In Serial-Out (at Transmitter end), and Serial-In Parallel-Out registers, and apply our knowledge of digital design.
We can design a Finite State Machine (FSM), identifying the states of the Transmitter/ Receiver considering the data bits being transmitted/ received as the outputs/inputs to the FSM. According to the Frame Format of the UART, we will decide the next state.
We will use the concept of Finite State Machines (Behavioral Modeling) as it is easier and more intuitive
