# UART-Universal-Asynchronous-Receiver-Transmitter-
Universal Asynchronous Receiver/ Transmitter is such a hardware circuit that uses asynchronous serial communication for data transmission.

Clearly, to implement UART on Verilog, we will need to convert data from parallel to serial at the transmitter end, and, serial to parallel at the receiver end.
There are a few ways we can go about this:

We can use register blocks, i.e., Parallel-In Serial-Out (at Transmitter end), and Serial-In Parallel-Out registers, and apply our knowledge of digital design.
We can design a Finite State Machine (FSM), identifying the states of the Transmitter/ Receiver considering the data bits being transmitted/ received as the outputs/inputs to the FSM. According to the Frame Format of the UART, we will decide the next state.
We will use the concept of Finite State Machines (Behavioral Modeling) as it is easier and more intuitive

Transmitter Code Explanation:
Initially, we declare clock and data_loaded and data byte as input and lineactive,uart_out, and done as output.We have taken transmitter state, clock counter, data index, data_byte_reg, done_reg, and lineactive_reg as 0 initially. When data_loaded is 0, it indicates that no data is to be transmitted and the output line is to be pulled high. So, we stay in the IDLE state and transmit 1 bit continuously. Now, when data_loaded is 1, the transmission of data starts and the state goes to START_BIT. In the START_BIT, the bit waits for clocks_per_bit clock cycles for the start bit which is a 0 bit, to finish transmission. After completion, the next state is the DATA_BIT and each data bit is transmitted to uart_out one after the other starting from the Least Significant Bit. After data bits are transmitted successfully, state goes to the STOP_BIT. In the STOP_BIT state, uart_out becomes 1 and this shows that all data is transmitted. After this we go to the RESET state where everything is reset and then the state goes back to IDLE, so that new data bits can be transmitted.

Receiver Code Explanation:
Initially, the received data bits will be high indicating no data being communicated. During this period, the state of the FSM is IDLE. Now, when a 0 bit, i.e., a START bit is encountered, the FSM goes to the next state which is the START_BIT state. Now, we sample the incoming data at the middle of the bit, to minimize any error in sampling the incoming data. If the incoming bit is still 0 when sampled at the middle, we go to the DATA_BITS state, where we continue sampling the data bits. Otherwise, we return to the IDLE state. In the DATA_BITS state, we again sample each data bit at the middle to minimize any errors, store it in a register and do so till 8 bits are sampled. After this, we move on to the STOP_BIT state.
