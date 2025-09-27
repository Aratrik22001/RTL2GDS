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
The testbench instantiates the multiplexer and applies the following test vectors:
- `sel` toggles every 75 time units
- `i0` toggles every 10 time units  
- `i1` toggles every 55 time units
Total runtime of the simulation is 300ns


Command to run the design and testbench
```
iverilog good_mux.v tb_good_mux.v
./a.out
```
Iverilog creates a **a.out** file executing which dumps the vcd file to be viewed by the waveform viewer.

## GTKWave
This is used to generate the waveforms and display in visual format.

Command to view the vcd file in gtkwave 
```
gtkwave tb_good_mux.vcd
```
The waveform of the good_mux.v as shown in gtkwave:
<img width="993" src="https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/gtkwave_mux.jpg?raw=true">

---

## Synthesizing using Yosys

The synthesizer converts the Register-Transfer Level (RTL) Code to Netlist, which is the representation of the design using standard cells from the technology library used to synthesize. To verify proper fucntionality the same testbench is used for the Synthesized Netlist.

### <ins> Lab with Yosys <ins>

```shell
$ yosys 														# Start Yosys
$ read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 	# Read the Library File
$ read_verilog good_mux.v										# Read the Verilog File
$ synth -top good_mux											# Synthesize the Design
$ abc -liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  	# Extracting the Netlist
$ show															# View the netlist using Dot Viewer
$ write_verilog -noattr ../netlist_file/good_mux_netlist.v		# Write the Netlist for further use
```
### <ins> Results <ins>
<img width="993" src="https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/good_mux_yosys_synth.jpg?raw=true">
<img width="993" src="https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/good_mux_stats.jpg?raw=true">
<img width="993" src="https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/good_mux_netlist.jpg?raw=true">
<img width="993" src="https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/good_mux.jpg?raw=true">

[**good_mux_netlist.v**](https://github.com/Aratrik22001/RTL2GDS/blob/main/Week1/Day1/good_mux_netlist.v) is the generated netlist file.

---

## Key Learnings
- ***Simulator***: Utilized Icarus Verilog (iverilog) for functional verification, demonstrating the ability to effectively simulate digital designs.
- ***Design***: Developed behavioral Verilog representations, showcasing proficiency in writing clean and structured RTL code.
- ***Testbench***: Built a verification environment capable of generating comprehensive test scenarios for design validation.
- ***Synthesis***: Applied Yosys to perform RTL-to-gate-level conversion, successfully synthesizing the design into a gate-level netlist.
