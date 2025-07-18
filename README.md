# DIGITAL FILTER DESIGN
COMPANY : CODTECH IT SOLUTIONS

NAME : ADITYA AVINASH GAIKWAD

INTERN ID :CITS0D81

DOMAIN : VLSI

DURATION : 4 WEEKS

MENTOR : NEELA SANTOSH

DESCRIPTION :

SOFTWARE USED- MODELSIM

CODE-


module fir_filter (

    input clk,
    input reset,
    input [7:0] x_in,
    output reg [15:0] y_out
);
    // Filter Coefficients

    parameter h0 = 1;
    parameter h1 = 2;
    parameter h2 = 3;
    parameter h3 = 4;

    // Delay elements
    reg [7:0] x1, x2, x3;

    always @(posedge clk or posedge reset) begin
        if (reset) begin
            x1 <= 0;
            x2 <= 0;
            x3 <= 0;
            y_out <= 0;
        end else begin
            // Shift registers
            x1 <= x_in;
            x2 <= x1;
            x3 <= x2;

            // Multiply-accumulate
            y_out <= (x_in * h0) + (x1 * h1) + (x2 * h2) + (x3 * h3);
        end
    end
endmodule



module tb_fir_filter;
    reg clk, reset;
    reg [7:0] x_in;
    wire [15:0] y_out;

    fir_filter dut (
        .clk(clk),
        .reset(reset),
        .x_in(x_in),
        .y_out(y_out)
    );

    // Clock generation
    always #5 clk = ~clk;

    initial begin
        $dumpfile("fir_filter.vcd");
        $dumpvars(0, tb_fir_filter);

        clk = 0;
        reset = 1;
        x_in = 0;
        #10;
        reset = 0;

        // Apply inputs
        x_in = 1; #10;
        x_in = 2; #10;
        x_in = 3; #10;
        x_in = 4; #10;
        x_in = 5; #10;
        x_in = 6; #10;
        x_in = 0; #10;

        $finish;
    end
endmodule

OUTPUT-
![Image](https://github.com/user-attachments/assets/77f9a7f3-ac3a-44b9-9e3a-a512b3e7e484)


The 4-tap FIR filter design performs accurately, producing correct outputs that match theoretical values after an initial 3-cycle delay. It processes one input per clock cycle and generates one output per cycle, ensuring high throughput. The reset and clock work properly, and timing is well-synchronized. Simulation results confirm smooth and correct output behavior. The design is resource-efficient, scalable, and suitable for real-time DSP applications. Overall, the filter is functionally correct, fast, and ready for hardware implementation.
