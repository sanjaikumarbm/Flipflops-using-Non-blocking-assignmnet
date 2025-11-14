# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```verilog
module SR_FF_B(
    input  wire S,
    input  wire R,
    input  wire clk,
    output reg  Q
);
    always @(posedge clk) begin
        if (S == 0 && R == 0)
            Q <= Q;
        else if (S == 0 && R == 1)
            Q <= 1'b0;
        else if (S == 1 && R == 0)
            Q <= 1'b1;
        else 
            Q <= 1'bx;
    end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module tb_SR_FF_B;
    reg S, R, clk;
    wire Q;

    SR_FF_B uut (
        .S(S),
        .R(R),
        .clk(clk),
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        S <= 0; R <= 0;
        #10;  

        @(posedge clk);
        S <= 1; R <= 0;  

        @(posedge clk);
        S <= 0; R <= 1;  

        @(posedge clk);
        S <= 1; R <= 1;  

        @(posedge clk);
        S <= 0; R <= 0;   

        @(posedge clk);
        $stop;            
    end

endmodule


```
#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="SR_FF_B" src="https://github.com/user-attachments/assets/c2c6d8ec-090b-40b3-9853-e9ace8061edb" />
---

### JK Flip-Flop (Non Blocking)
```verilog
module JK_FF_B (
    input  wire J,
    input  wire K,
    input  wire clk,
    output reg  Q
);
    always @(posedge clk) begin
        if (J == 0 && K == 0)
            Q <= Q;
        else if (J == 0 && K == 1)
            Q <= 1'b0;
        else if (J == 1 && K == 0)
            Q <= 1'b1;
        else 
            Q <= ~Q;
    end
endmodule

```
### JK Flip-Flop Test bench 
```verilog
module tb_JK_FF_B;
    reg J, K, clk;
    wire Q;

    JK_FF_B uut (
        .J(J),
        .K(K),
        .clk(clk),
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        J <= 0; K <= 0;
        #10;

        @(posedge clk);
        J <= 1; K <= 0;
        @(posedge clk);
        J <= 0; K <= 1;   

        @(posedge clk);
        J <= 1; K <= 1;    

        @(posedge clk);
        J <= 0; K <= 0;    

        @(posedge clk);
        $stop;
    end

endmodule


```
#### SIMULATION OUTPUT

<img width="1919" height="1079" alt="JK_FF_B" src="https://github.com/user-attachments/assets/344150e4-08f0-487f-8c20-78abf1803230" />
---

### D Flip-Flop (Non Blocking)
```verilog
module D_FF_B (
    input  wire D,
    input  wire clk,
    output reg  Q
);
    initial Q = 0; 
    always @(posedge clk) begin
        Q <= D;      
    end
endmodule
```
### D Flip-Flop Test bench 
```verilog
module tb_D_FF_B;
    reg D, clk;
    wire Q;

    D_FF_B uut (
        .D(D),
        .clk(clk),
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        
        D <= 0;
        #10;

        @(posedge clk);
        D <= 1;

        @(posedge clk);
        D <= 0;

        @(posedge clk);
        D <= 1;

        @(posedge clk);
        D <= 0;

        @(posedge clk);
        $stop;
    end

endmodule


```

#### SIMULATION OUTPUT

<img width="1918" height="1079" alt="D_FF_B" src="https://github.com/user-attachments/assets/dc734064-d7af-4e0f-9c47-3d9245910569" />
---

### T Flip-Flop (Non Blocking)
```verilog
module T_FF_B (
    input  wire T,
    input  wire clk,
    output reg  Q
);
    initial Q = 0;
    always @(posedge clk) begin
        Q <= (T ? ~Q : Q);
    end
endmodule
```

### T Flip-Flop Test bench 
```verilog

module tb_T_FF_B;
    reg T, clk;
    wire Q;

    T_FF_B uut (
        .T(T),
        .clk(clk),
        .Q(Q)
    );

    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    initial begin
        T <= 0;
        #10;

        @(posedge clk);
        T <= 1;

        @(posedge clk);
        T <= 0;

        @(posedge clk);
        T <= 1;

        @(posedge clk);
        T <= 1;

        @(posedge clk);
        T <= 0;

        @(posedge clk);
        $stop;
    end

endmodule

```

#### SIMULATION OUTPUT

<img width="1915" height="1076" alt="T_FF_B" src="https://github.com/user-attachments/assets/ece129f2-a10f-4a6b-b64a-0d4aecabeee7" />

---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
