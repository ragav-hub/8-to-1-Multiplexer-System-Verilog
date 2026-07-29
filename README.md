# Experiment 2: Design and Functional Verification of 8:1 Multiplexer using SystemVerilog

---

## Aim  
To design and functionally verify an **8:1 Multiplexer** using **SystemVerilog HDL** and simulate it using **Synopsys VCS & DVE**.

---

## Apparatus Required  
- Computer with **Windows** OS  
- **MobaXterm** (for remote terminal access)
- **Synopsys VCS and DVE** (accessed via college server/license) 
- SystemVerilog source code editor   

---

## Description about 8:1 Multiplexer  
A **Multiplexer (MUX)** is a combinational logic circuit that selects one of several input signals and forwards the selected input to a single output line.  
- An **8:1 MUX** has **8 input lines**, **3 select lines**, and **1 output line**.  
- The output depends on the binary value of the select inputs.  

**Truth Table Overview:**  

| Select Lines (S2 S1 S0) | Output (Y) |  
|--------------------------|------------|  
| 000                      | I0         |  
| 001                      | I1         |  
| 010                      | I2         |  
| 011                      | I3         |  
| 100                      | I4         |  
| 101                      | I5         |  
| 110                      | I6         |  
| 111                      | I7         |  

---

## Features  
- Designed in **SystemVerilog** for clarity and modularity  
- Supports **8 data inputs** and **3-bit selection**  
- Testbench for functional verification  
- Compatible with **Synopsys VCS & DVE**  

---

## Procedure  

1. **Connect to the Server via MobaXterm**  
   - Open MobaXterm and log in using the college-provided license email ID and password.  
   - Run the `xdg-open` command to access the file system and navigate through the folders.  

2. **Create a Working Directory**  
   - Create a new folder for the project.  
   - Inside this folder, create the design file and the testbench file `ALU.sv`.  

3. **Set Up the Simulation Environment**  
   - Open a terminal session (bash).  
   - Source the Synopsys VCS environment setup script (e.g.,`source /synopsys/start.sh`).  

4. **Compile the Design and Testbench**  
   - Run the following command to compile the SystemVerilog files : `vcs -full64 -sverilog ALU.sv`
   - Ensure there are no syntax or compilation errors.  

5. **Run the Simulation**  
   - Execute the compiled simulation binary : `./simv`

6. **Launch DVE (Discovery Visualization Environment)**  
   - Open the waveform viewer : `dve -full64`
   - In the DVE window, go to `File → Open Database`.  
   - Select and open the generated `.vcd`/dump file.  

7. **Add Signals to the Waveform Window**  
   - Right-click on the file/module in the hierarchy.  
   - Select **Add Wave → Add New Wave to Window** to display the signals.  

8. **Analyze Waveforms**  
   - Verify the outputs of the ALU for each enumerated operation.  
   - Check that addition, subtraction, logical operations, and shifts are working correctly.  

9. **Save Results**  
   - Save the waveform for documentation.

---

## SystemVerilog Code  

### Multiplexer Design (`mux8to1.sv`)
```systemverilog
// Class for 8:1 Multiplexer
class Mux8to1;

    // Properties (Inputs, Select & Output)
    bit [7:0] d;     // 8 input lines
    bit [2:0] sel;   // 3-bit select line
    bit y;           // output

    // Constructor
    function new(bit [7:0] d_in, bit [2:0] sel_in);
        d   = d_in;
        sel = sel_in;
    endfunction

    // Method to compute MUX output
    function void compute();
        case(sel)
            3'b000: y = d[0];
            3'b001: y = d[1];
            3'b010: y = d[2];
            3'b011: y = d[3];
            3'b100: y = d[4];
            3'b101: y = d[5];
            3'b110: y = d[6];
            3'b111: y = d[7];
        endcase
    endfunction

    // Method to display result
    function void display();
        $display("MUX 8:1 -> d=%b, sel=%0d, y=%0b", d, sel, y);
    endfunction

endclass

```
### Testbench code (`mux8to1_tb.sv`)
```systemverilog
module tb_mux8to1;
	logic d,sel,y;
	Mux8to1 m1,m2,m3,m4,m5,m6,m7,m8;
    initial begin

      // Create object of Mux8to1 class

      m1 = new(8'b10101010, 3'b000);
      m1.compute();
		d=m1.d;
		sel=m1.sel;
		y=m1.y;
      m1.display();
		#10;

      m2 = new(8'b10101010, 3'b001);
      m2.compute();
		d=m2.d;
		sel=m2.sel;
		y=m2.y;
      m2.display();
		#10;

      m3 = new(8'b10101010, 3'b010);
      m3.compute();
		d=m3.d;
		sel=m3.sel;
		y=m3.y;
      m3.display();
		#10;

      m4 = new(8'b10101010, 3'b011);
      m4.compute();
		d=m4.d;
		sel=m4.sel;
		y=m4.y;
      m4.display();
		#10;

      m5 = new(8'b10101010, 3'b100);
      m5.compute();
		d=m5.d;
		sel=m5.sel;
		y=m5.y;
      m5.display();
		#10;

      m6 = new(8'b10101010, 3'b101);
      m6.compute();
		d=m6.d;
		sel=m6.sel;
		y=m6.y;
      m6.display();
		#10;

      m7 = new(8'b10101010, 3'b110);
      m7.compute();
		d=m7.d;
		sel=m7.sel;
		y=m7.y;
      m7.display();
		#10;

      m8 = new(8'b10101010, 3'b111);
      m8.compute();
		d=m8.d;
		sel=m8.sel;
		y=m8.y;
      m8.display();
		#10;

		$finish;
    end

	initial begin
        $dumpfile("MUX8to1.vcd");
        $dumpvars(0,tb_mux8to1); 
    end

endmodule
```

---

### Simulation Output

<img width="1915" height="1141" alt="Screenshot 2026-07-28 144040" src="https://github.com/user-attachments/assets/56b722b5-b856-4b0d-8c73-717f8eb7e7be" />



---

### Result

The design and functional verification of an 8:1 Multiplexer using SystemVerilog HDL was successfully carried out in Synopsys VCS & DVE.
The multiplexer correctly selected one of the eight inputs based on the 3-bit select signal.
