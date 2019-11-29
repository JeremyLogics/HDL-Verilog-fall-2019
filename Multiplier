`timescale 1ns / 1ps
// `default nettype none
//////////////////////////////////////////////////////////////////////////////////
// Company: University of South Alabama ECE department, EE-543
// Engineer: 
// 
// Create Date: 11/17/2019 06:25:03 AM
// Design Name: 4-bit multiplier
// Module Name: MUL4JLapane
// Project Name: HDL/Verilog course Final Project
// Target Devices: 
// Tool Versions: 
// Description: Design a 4-bit multiplier using gate level modeling
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
// Sublime text 3 notes: 
// CNTL+Shift+/ : comment block selection shortcut
//
//
//
//////////////////////////////////////////////////////////////////////////////////

/*module myAND (input1,input2,result); 
input input1, input2; //and gate inputs, the first and second inputs. 
output result; //"result" is the output of the and gate
and g1 (result, input1, input2);
endmodule*/
 
/*module AND1x4 (a, b, out);
input [3:0] a;
input b;
output [3:0] out;

and (out[0], a[0], b);
and (out[1], a[1], b);
and (out[2], a[2], b);
and (out[3], a[3], b);

endmodule*/

/*module FADD4 (fourin1, fourin2, sum, carryin, carryout);
input  [3:0] fourin1, fourin2; //first and second inputs
input  carryin;
output [3:0] sum;
output carryout;

wire carry1, carry2, carry3; //internal carries

FADD1 g1  (fourin1[0], fourin2[0], sum[0], carryin, carry1);
FADD1 g2  (fourin1[1], fourin2[1], sum[1], carry1, carry2);
FADD1 g3  (fourin1[2], fourin2[2], sum[2], carry2, carry3);
FADD1 g4  (fourin1[3], fourin2[3], sum[3], carry3, carryout);

endmodule*/

//FADD1 COMPLETE
module FADD1 (in1, in2, s, cin, cout); 
//using different naming conventions to better distinguish code, since this will be instanced in the 4-bit full adder
input  in1, in2, cin; //port declaration
output s, cout; //port dec
wire   out1, out2, out3; //internal variables
//using built in-gates, the following gate-level modeling arranges a 1-bit full adder, to be instanced in the 4-bit full adder, FADD4
xor g1 (out1, in1, in2);
xor g2 (s, out1, cin);
and g3 (out2, out1, cin);
and g4 (out3, in1, in2);
or g5  (cout, out2, out3);

endmodule


//TOP MODULE
module MUL4JLAPANE (inputa, inputb, Output_P_eq_ab); 
//using different naming conventions again, this module is the top module for the 4-bit multiplier design, using instances of FADD1, FADD4, AND1x4 
input [3:0] inputa, inputb;
output [7:0] Output_P_eq_ab;
wire [7:0] internalx, internaly, internalz; // poor naming convention for internal wires between ANDs and FADDers. 
wire [8:0] carry;

assign internalx[3] = 1'b0;

//inputs initial and
and (Output_P_eq_ab[0], inputa[0], inputb[0]);
and (internalx[0], inputa[1], inputb[0]);
and (internalx[1], inputa[2], inputb[0]);
and (internalx[2], inputa[3], inputb[0]);
//group0 and+FADD COMPLETE
and (internalx[4], inputa[0], inputb[1]); //0
and (internalx[5], inputa[1], inputb[1]); //0
and (internalx[6], inputa[2], inputb[1]); //0
and (internalx[7], inputa[3], inputb[1]); //0

FADD1 A1 (internalx[0],internalx[4], Output_P_eq_ab[1], 1'b0,     carry[0]); //0
FADD1 A2 (internalx[1],internalx[5], internaly[0], carry[0], carry[1]); //0
FADD1 A3 (internalx[2],internalx[6], internaly[1], carry[1], carry[2]); //0
FADD1 A4 (internalx[3],internalx[7], internaly[2], carry[2], internaly[3]); //0

//group1 and+FADD 
and (internaly[4], inputa[0], inputb[2]); //1
and (internaly[5], inputa[1], inputb[2]); //1
and (internaly[6], inputa[2], inputb[2]); //1
and (internaly[7], inputa[3], inputb[2]); //1

FADD1 B1 (internaly[0],internaly[4], Output_P_eq_ab[2], 1'b0, carry[3]); //1
FADD1 B2 (internaly[1],internaly[5], internalz[0], carry[3],     carry[4]); //1
FADD1 B3 (internaly[2],internaly[6], internalz[1], carry[4],     carry[5]); //1
FADD1 B4 (internaly[3],internaly[7], internalz[2], carry[5],     internalz[3]); //1

//group2 and+FADD
and (internalz[4], inputa[0], inputb[3]); //2
and (internalz[5], inputa[1], inputb[3]); //2
and (internalz[6], inputa[2], inputb[3]); //2
and (internalz[7], inputa[3], inputb[3]); //2

FADD1 C1 (internalz[0],internalz[4], Output_P_eq_ab[3], 1'b0, carry[6]); //2
FADD1 C2 (internalz[1],internalz[5], Output_P_eq_ab[4], carry[6], carry[7]); //2
FADD1 C3 (internalz[2],internalz[6], Output_P_eq_ab[5], carry[7], carry[8]); //2
FADD1 C4 (internalz[3],internalz[7], Output_P_eq_ab[6], carry[8], Output_P_eq_ab[7]);  //2



endmodule
