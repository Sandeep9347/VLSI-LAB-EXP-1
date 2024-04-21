# VLSI-LAB-EXPERIMENTS
# AIM: To simulate and synthesis Logic Gates,Adders and Subtractor using Vivado 2023.1

# APPARATUS REQUIRED: Vivado 2023.1

# PROCEDURE: 
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design


Logic Diagram :

VERILOG CODE:
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
Logic Gates:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)


Half Adder:
VERILOG CODE:
module half_adder(Sum,carry,a,b);
input a,b;
output Sum,carry;
assign Sum = a ^ b;
assign carry = a & b;
endmodule

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)
out put:

![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/9fbb8208-eadf-4dd1-aef5-8f846255c836)


Full adder:
VERILOG CODE:
module fulladder(sum,cout,a,b,c);
input a,b,c;
output sum,cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and a1(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,c1,c2);
or o2(cout,w5,c3);
endmodule
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)
out put:

![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/d0b0e475-4157-409c-977e-0bfad51cb02e)


Half Subtractor:
VERILOG CODE:
module half_sub(Diff,Borrow,a,b);
input a,b;
output Diff,Borrow;
wire w1;
not(w1,a);
xor(Diff,a,b);
and(Borrow,b,w1);
endmodule
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)

out put:

![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/b1f1ae07-33ad-4cbb-af92-8ecc7611f1f9)


Full Subtractor:
VERILOG CODE:
module full_sub(borrow,diff,a,b,c);
output borrow,diff;
input a,b,c;
wire w1,w4,w5,w6;
xor (diff,a,b,c);
not n1(w1,a);
and a1(w4,w1,b);
and a2(w5,w1,c);
and a3(w6,b,c);
or o1(borrow,w4,w5,w6);
endmodule
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)


out put:

![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/d5986f3d-edd5-47d8-9a17-5aa18f0bbc7f)

4-bit ripple carry adder:
VERILOG CODE:
module rippe_adder(S, Cout, X, Y,Cin);
input [3:0] X, Y;
input Cin;
output [3:0] S;
output Cout;
wire w1, w2, w3;
fulladder u1(S[0], w1,X[0], Y[0], Cin);
fulladder u2(S[1], w2,X[1], Y[1], w1);
fulladder u3(S[2], w3,X[2], Y[2], w2);
fulladder u4(S[3], Cout, X[3], Y[3], w3);
endmodule

module fulladder(S, Co, X, Y, Ci);
input X, Y, Ci;
output S, Co;
wire w1,w2,w3;
xor G1(w1, X, Y);
xor G2(S, w1, Ci);
and G3(w2, w1, Ci);
and G4(w3, X, Y);
or G5(Co, w2, w3);
endmodule

out put:

![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/5ec25163-9246-406e-8e7d-1a62bc7ad766)


8 Bit Ripple Carry Adder
VERILOG CODE:
module rippe_adder(S, Cout, X, Y,Cin);
input [7:0] X, Y;// Two 4-bit inputs
input Cin;
output [7:0] S;
output Cout;
wire w1, w2, w3, w4, w5, w6, w7;
 // instantiating 8 1-bit full adders in Verilog
fulladder u1(S[0], w1,X[0], Y[0], Cin);
fulladder u2(S[1], w2,X[1], Y[1], w1);
fulladder u3(S[2], w3,X[2], Y[2], w2);
fulladder u4(S[3], w4,X[3], Y[3], w3);
fulladder u5(S[4], w5,X[4], Y[4], w4);
fulladder u6(S[5], w6,X[5], Y[5], w5);
fulladder u7(S[6], w7,X[6], Y[6], w6);
fulladder u8(S[7], Cout,X[7], Y[7], w7);
endmodule
module fulladder(S, Co, X, Y, Ci);
input X, Y, Ci;
output S, Co;
wire w1,w2,w3;
  //Structural code for one bit full adder
xor G1(w1, X, Y);
xor G2(S, w1, Ci);
and G3(w2, w1, Ci);
and G4(w3, X, Y);
or G5(Co, w2, w3);
endmodule

module fulladder(S, Co, X, Y, Ci);
input X, Y, Ci;
output S, Co;
wire w1,w2,w3;
xor G1(w1, X, Y);
xor G2(S, w1, Ci);
and G3(w2, w1, Ci);
and G4(w3, X, Y);
or G5(Co, w2, w3);
endmodule
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)
out put :


![image](https://github.com/21004601/VLSI-LAB-EXP-1/assets/160619092/04aa0fa7-d7c9-4d65-b6a8-fccc029a5063)


RESULT:
THUS THE LOGIC GATES,ADDERS,SUBTRACTORS VERILOG CODE IS SIMULATED AND OUTPUT VERIFIED SUCCESSFULLY



























