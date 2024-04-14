# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

**AIM:** 

&emsp;&emsp;To simulate and implement SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using VIVADO 2023.2.

**APPARATUS REQUIRED:**

&emsp;&emsp;VIVADO 2023.2

**PROCEDURE:**

STEP:1  Launch the Vivado 2023.2 software.<br>
STEP:2  Click on “create project ” from the starting page of vivado.<br>
STEP:3  Choose the design entry method:RTL(verilog/VHDL).<br>
STEP:4  Crete design source  and give name to it and click finish.<br>
STEP:5  Write the verilog code and check the syntax.<br>
STEP:6  Click “run simulation” in the navigator window and click “Run behavioral simulation”.<br>
STEP:7  Verify the output in the simulation window.<br>

**SR FLIPFLOP:**

**LOGIC DIAGRAM:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)

**VERILOG CODE:**

```
module srff(s,r,q,clk,reset);
input s,r,clk,reset;
output reg q;
always @(posedge clk)
begin
if(reset==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bx;
endcase
end
end
endmodule
```

**OUTPUT:**

![image](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/d294e10b-657d-4a98-95b4-296c8c35cbaa)

**JK FLIPFLOP:**

**LOGIC DIAGRAM:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

**VERILOG CODE:**

```
module jkff(j,k,q,clk,reset);
input j,k,clk,reset;
output reg q;
always @(posedge clk)
begin
if(reset==1)
q=0;
else
begin
case({j,k})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=~q;
endcase
end
end
endmodule
```

**OUTPUT:**

![WhatsApp Image 2024-04-13 at 20 09 15_2cf42949](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/34fb53f9-f0f7-409e-a8dd-ff17966de6ac)

**T FLIPFLOP:**

**LOGIC DIAGRAM:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)

**VERILOG CODE:**

```
module tff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
```

**OUTPUT:**

 ![WhatsApp Image 2024-04-13 at 20 09 15_06ab6913](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/a4a31c6f-32c4-4cf9-8430-705bec54e37f)

**D FLIPFLOP:**

**LOGIC DIAGRAM:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)

**VERILOG CODE:**

```
module dff(clk,reset,d,q);
input clk,d,reset;
output reg q;
always@(posedge clk)
begin
if(reset)
q<=1'b0;
else
q<=d;
end
endmodule
```

**OUTPUT:**

![WhatsApp Image 2024-04-13 at 20 09 14_7c3b17fe](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/6f519779-c80b-481d-b4a4-7873123f7be6)

**COUNTER:**

**LOGIC DIAGRAM:**

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)

**UPDOWN COUNTER:**

**VERILOG CODE:**

  ```
module updowncounter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always @ (posedge clk)
begin
if(rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
```

**OUTPUT:**

![image](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/7ddc9e9e-2580-4907-bba8-2f688c308015)

**MOD 10 COUNTER:**

**VERILOG CODE:**

```
module mod10counter(clk,rst,out);
input clk,rst;
output reg[3:0]out;
always @(posedge clk)
begin
if(rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
```

**OUTPUT:**

![image](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/8cf34364-a8da-4cb6-a11e-e8132377c964)

**RIPPLE CARRY COUNTER:**

**VERILOG CODE:**

```
module ripplecounter(q, clk, reset);
output [3:0] q;
input clk, reset;
T_FF tff0(q[0], clk, reset);
T_FF tff1(q[1], q[0], reset);
T_FF tff2(q[2], q[1], reset);
T_FF tff3(q[3], q[2], reset);
endmodule

module T_FF(q, clk, reset);
output q;
input clk, reset;
wire d;
D_FF dff0(q, d, clk, reset);
not n1(d, q); 
endmodule

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
```

**OUTPUT:**

![image](https://github.com/SwarnaMallikaPL/VLSI-LAB-EXP-4/assets/160829667/860c050a-314e-4d3b-be3e-27a458292650)

**RESULT:**

&emsp;&emsp;Thus the simulation of sequential circuits is done and outputs are verified
successfully.
