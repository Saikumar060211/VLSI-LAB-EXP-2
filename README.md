# SIMULATION AND IMPLEMENTATION OF COMBINATIONAL LOGIC CIRCUITS
                                                                                                                                                                                                 
# AIM 
 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

# APPARATUS REQUIRED:
Xilinx 14.7 Spartan6 FPGA

# PROCEDURE
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

# ENCODER

# LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)

# VERILOG CODE
```
module encoder8_3(a,y);
input [7:0]a;
output [2:0]y;
reg [7:0]y;
always@(*)
   begin
      case(a)
         8'b00000001: y=3'b000;
         8'b00000010: y=3'b001;
         8'b00000100: y=3'b010;
         8'b00001000: y=3'b011;
         8'b00010000: y=3'b100;
         8'b00100000: y=3'b101;
         8'b01000000: y=3'b110;
         8'b10000000: y=3'b111;
       endcase
   end     
endmodule
```

# OUTPUT

![Screenshot 2024-03-16 113016](https://github.com/Mohanraj7896/VLSI-LAB-EXP-2/assets/166592482/e26c4198-9b78-49eb-a2f1-16fa4506a25b)

# DECODER

# LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)

# VERILOG CODE
```
module decoder3_8(a,y);
input [2:0]a;
output [7:0]y;
reg [7:0]y;
always@ (*)
  begin
     case(a)
        3'b000: y=8'b00000001;
        3'b001: y=8'b00000010;
        3'b010: y=8'b00000100;
        3'b011: y=8'b00001000;
        3'b100: y=8'b00010000;
        3'b101: y=8'b00100000;
        3'b110: y=8'b01000000;
        3'b111: y=8'b10000000;
      endcase
   end    
endmodule
```

# OUTPUT

![Screenshot 2024-03-16 121655](https://github.com/Mohanraj7896/VLSI-LAB-EXP-2/assets/166592482/8e3ef12b-1437-4618-bf86-5b28f9a7e3cf)

# MULTIPLEXER

# LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)

# VERILOG CODE
```
module mux(a,s,y);
input [7:0]a;
input [2:0]s;
output y;
reg y;
always@({s ,a})
   begin
      case(s)
         3'b000: y=a[0];
         3'b001: y=a[1];
         3'b010: y=a[2];
         3'b011: y=a[3];
         3'b100: y=a[4];
         3'b101: y=a[5];
         3'b110: y=a[6];
         3'b111: y=a[7];
      endcase
   end
endmodule
```

# OUTPUT

![Screenshot 2024-04-13 at 09 59 59_d27e847f](https://github.com/Mohanraj7896/VLSI-LAB-EXP-2/assets/166592482/fb4d3280-85b3-41d0-8610-418b4409b768)

# DEMULTIPLEXER

# LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)

# VERILOG CODE
```
module demux(din,s,d);
input din;
input[2:0]s;
output [7:0]d;
assign d[0]=(din&~s[2]&~s[1]&~s[0]);
assign d[1]=(din&~s[2]&~s[1]&s[0]);
assign d[2]=(din&~s[2]&s[1]&~s[0]);
assign d[3]=(din&~s[2]&s[1]&s[0]);
assign d[4]=(din&s[2]&~s[1]&~s[0]);
assign d[5]=(din&s[2]&~s[1]&s[0]);
assign d[6]=(din&s[2]&s[1]&~s[0]);
assign d[7]=(din&s[2]&s[1]&s[0]);
endmodule
```

# OUTPUT

![Screenshot 2024-03-15 195918](https://github.com/Mohanraj7896/VLSI-LAB-EXP-2/assets/166592482/c0f43882-e3bd-45d5-9dce-f3d29bc0b051)

# MAGNITUDE COMPARATOR

# LOGIC DIAGRAM

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)

# VERILOG CODE
```
module magnitudecomparator(a,b,eq,lt,gt);
input [3:0]a,b;
output reg eq,lt,gt;
always@({a,b})
begin
 if(a==b)
 begin
eq=1'b1;
lt=1'b0;
gt=1'b0;
 end
 else if (a>b)
 begin
eq=1'b0;
lt=1'b0;
gt=1'b1;
 end
 else
 begin
eq=1'b0;
lt=1'b1;
gt=1'b0;
 end
end
endmodule
```

# OUTPUT

![Screenshorts Image 2024-04-13 at 09 59 59_e263eb8c](https://github.com/Mohanraj7896/VLSI-LAB-EXP-2/assets/166592482/478f74a3-0f9c-41f4-9966-8741ef87c589)

# RESULT
Hence ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR are simulated and synthesised using Xilinx ISE.
