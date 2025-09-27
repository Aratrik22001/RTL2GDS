# Day 1: Introduction to Verilog RTL Design & Synthesis

## Introduction to use of Open-Source Simulator and Waveform Viewer

## Iverilog

I have simulated the Verilog file **good_mux.v**, which implements a 2×1 multiplexer. The output correctly updates whenever the select line changes.

Design of good_mux.v
```verilog
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
Test-Bench tb_good_mux.v
```verilog
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

	// Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

Command to run the design and testbench
```
iverilog good_mux.v tb_good_mux.v
./a.out
```
Iverilog creates a **a.out** file executing which dumps the vcd file to be viewed by the waveform viewer.

## GTKWave
