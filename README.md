
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

# AIM:
```
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.
```
# APPARATUS REQUIRED: 
```
Vivado™ ML 2023.2
```
# PROCEDURE:
```
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.
```
# LOGIC DIAGRAM**
# D FLIP FLOP :
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/c7aed3ac-d838-49bb-90ee-fb5db74e1d63)
# CODE:
```
module dff(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else
q=d;
end
endmodule
```
# OUTPUT WAVEFORM
 ![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/9b80644c-4c1e-4fdc-b316-141a352e3fd5)

# JK FLIP FLOP:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/3d275988-5ade-4afe-a883-a434143041a3)

# CODE:
```
  module JK_flipflop (q, q_bar, j,k, clk, reset);
  input j,k,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin
    if(!reset)        q <= 0;
    else 
  begin
      case({j,k})
        2'b00: q <= q;  
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1;
        2'b11: q <= ~q; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/6a8331bc-36d3-40d5-ad71-b530ad53f49a)


# MOD 10 COUNTER:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/5ad8810d-a5bc-4bcc-afed-e1812e59a7c9)

# CODE: 
```
module counter(
input clk,rst,enable,
output reg [3:0]counter_output
);
always@ (posedge clk)
begin 
if( rst | counter_output==4'b1001)
counter_output <= 4'b0000;
else if(enable)
counter_output <= counter_output + 1;
else
counter_output <= 0;
end
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/4d7a2165-4ce1-4a2a-b7b3-ebd3b83a6ca6)

# CODE RIPPLE COUNTER:
```
module D_FF(q, d, clk, reset);
output q;
input d, clk, reset;
reg q;
always @(posedge reset or negedge clk)
if (reset)
q = 1'b0;
else
q = d;
endmodule
module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule
module ripple_carry_counter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tffo(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/6208762f-456d-4dfa-8235-4daf57db0f31)

# SR FLIPFLOP :
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/20440464-d49a-44f8-a3e2-2f8e531801ae)

# CODE:
```
  module SR_flipflop (q, q_bar, s,r, clk, reset);
  input s,r,clk, reset;
  output reg q;
  output q_bar;
  always@(posedge clk) begin 
    if(!reset)�        q <= 0;
    else 
  begin
      case({s,r})
        2'b00: q <= q;    
        2'b01: q <= 1'b0; 
        2'b10: q <= 1'b1; 
        2'b11: q <= 1'bx; 
      endcase
    end
  end
  assign q_bar = ~q;
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/61b4bab0-27e9-4fe8-89cd-8351f81ecdfb)

#  T FLIP FLOP :
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/7d07796f-3560-4347-a34d-66caa577cc09)

# CODE:
```
module tff (t,clk, rstn,q);  
 input t,clk, rstn;
 output reg q;
  always @ (posedge clk) begin  
    if (!rstn)  
      q <= 0;  
    else  
        if (t)  
            q <= ~q;  
        else  
            q <= q;  
  end  
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/8c29c966-0b3b-4ce2-a919-8ef304ec443e)

# UPDOWN COUNTER:
# CODE:
```
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```
# OUTPUT:
![image](https://github.com/kamali109/VLSI-LAB-EXP-4/assets/160600794/2cc5bb01-9b3c-49d5-95b6-faa65c1c7f74)


# RESULT:
```
Simulate And Synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN is Successfully Verified using Vivado Software.
```

