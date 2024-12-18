# 4-BIT-RIPPLE-COUNTER

**AIM:**

To implement  4 Bit Ripple Counter using verilog and validating their functionality using their functional tables

**SOFTWARE REQUIRED:**

Quartus prime

**THEORY**

**4 Bit Ripple Counter**

A binary ripple counter consists of a series connection of complementing flip-flops (T or JK type), with the output of each flip-flop connected to the Clock Pulse input of the next higher-order flip-flop. The flip-flop holding the least significant bit receives the incoming count pulses. The diagram of a 4-bit binary ripple counter is shown in Fig. below.

![Screenshot 2024-12-18 215216](https://github.com/user-attachments/assets/50e08ed3-1fed-4046-aad0-310c8d98a68e)

In timing diagram Q0 is changing as soon as the negative edge of clock pulse is encountered, Q1 is changing when negative edge of Q0 is encountered(because Q0 is like clock pulse for second flip flop) and so on.

![Screenshot 2024-12-18 215239](https://github.com/user-attachments/assets/a4fd534c-ad88-4b82-96cf-f29a10e3abff)


![Screenshot 2024-12-18 215255](https://github.com/user-attachments/assets/d62538e7-2064-4e6f-b50e-2d46ec32a637)


**Procedure**

1.Code Overview: Understand the Verilog module ripple_counter, which includes clock (clk) and reset (rst) inputs, and a 4-bit output count. The counter increments on each positive clock edge unless reset is asserted, resetting the count to 0.

2.Simulation Preparation: Use a Verilog simulator (e.g., ModelSim) and write a testbench module to apply clock and reset signals while monitoring the counter output.

3.Testbench Implementation: Instantiate the ripple_counter module in the testbench, generate clock and reset signals, apply them to the counter module, and observe the count output.

4.Simulation Execution: Compile both the counter module and the testbench, simulate the design, and verify that the counter counts from 0 to 15 (binary 1111) and resets to 0 when the reset signal is activated.

5.Verification and Debugging: Analyze timing diagrams to ensure proper counter behavior, debug any encountered issues during simulation, and make necessary modifications to the design for optimal functionality.

Program for 4 Bit Ripple Counter and verify its truth table in quartus using Verilog programming.

**PROGRAM**

/* Program for 4 Bit Ripple Counter and verify its truth table in quartus using Verilog programming.

 Developed by:Sarankumar.V RegisterNumber:24010668
 ```
module ripple (
    input clk,     // Clock input
    input reset,   // Reset input (active high)
    output [3:0] q // 4-bit output
);
    // Internal signals for flip-flops
    reg [3:0] q_int;

    // Assign internal register to output
    assign q = q_int;

    always @(posedge clk or posedge reset) begin
        if (reset) 
            q_int[0] <= 1'b0; // Reset the first bit to 0
        else 
            q_int[0] <= ~q_int[0]; // Toggle the first bit on clock edge
    end

    // Generate the other flip-flops based on the output of the previous one
    genvar i;
    generate
        for (i = 1; i < 4; i = i + 1) begin : ripple
            always @(posedge q_int[i-1] or posedge reset) begin
                if (reset) 
                    q_int[i] <= 1'b0; // Reset the bit to 0
                else 
                    q_int[i] <= ~q_int[i]; // Toggle the bit on clock edge of previous stage
            end
        end
    endgenerate
endmodule
```


**RTL LOGIC FOR 4 Bit Ripple Counter**

![Screenshot 2024-12-18 215338](https://github.com/user-attachments/assets/10e91f91-480c-4a7c-a086-c85c9a5b6222)

**TIMING DIGRAMS FOR 4 Bit Ripple Counter**

**RESULTS**
The 4-bit ripple counter was successfully implemented using Verilog in Quartus Prime. The functionality was verified using a testbench, which simulated the counter's operation. The counter correctly counted from 0000 to 1111, incrementing by 1 on each clock pulse. After reaching 1111, the counter reset to 0000, as expected. The timing diagrams and the functional table showed that the ripple counter operated as intended, with each flip-flop toggling on the rising edge of the previous flip-flop's output. The simulation results confirmed the correct operation of the 4-bit ripple counter.
