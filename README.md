
# Workshop On RTL Design Using Verilog With Sky 130 Technology
![image](https://user-images.githubusercontent.com/86367130/123824988-22239100-d91c-11eb-95ae-bf2f17e4e701.png)

# Contents

 + Introduction to RTL Design And Synthesis

 + Hierarchical Vs Flat Synthesis and Efficient Flip-Flop Coding Styles

 + Introduction To Ligic Optimization

 + GLS, Blocking vs Non-blocking and Synthesis Simulation Mismatch

 + If, Case, For Loop and for generate



# Introduction to RTL Design And Synthesis


RTL Design- register-transfer level (RTL) is a design abstraction which models a synchronous digital circuit in terms of the flow of digital signals (data) between hardware registers, and the logical operations performed on those signals.

Labs

Various Commands Used in Simulation of An RTL Design

1.iverilog – Use to load the design(RTL code and test bench) in iverilog and a file a.out is created
![image](https://user-images.githubusercontent.com/86367130/123827332-2781db00-d91e-11eb-82de-227f1fe4a2cb.png)

2./a.out – This command dumps the data of the test bench into a Value Change Data File

3.gtkwave- gtkwave is the waveform viewer whose input is the Value Change Data File.
![image](https://user-images.githubusercontent.com/86367130/123827495-4b452100-d91e-11eb-878d-1670995957f5.png)

Synthesis Commands in Yosys

1.yosys - This command is used to invoke yosys the synthesis tool.
This is the synthesizer used to convert RTL to Netlist
![image](https://user-images.githubusercontent.com/86367130/123827649-6e6fd080-d91e-11eb-9ce5-f78bcd21f6fa.png)

2.read_liberty -lib <library path> - read cells from liberty file as modules into current design. This command reads the .lib file
-lib – Only create empty black box modules
  
  ![image](https://user-images.githubusercontent.com/86367130/123827725-7fb8dd00-d91e-11eb-9ffc-5c9040246d97.png)

3.Read_verilog -command to read the design
  
4.synth -top <name of the module> - This command runs the default synthesis script
  -top -Use the specify as top module
  
  ![image](https://user-images.githubusercontent.com/86367130/123827908-a545e680-d91e-11eb-994f-d1d63b66e8d7.png)
  
5. abc – This command uses the ABC tool for technology mapping of yosys internal gate library to a target architecture. The internal gate library consists of the specification of the gates about their area, timing, power consumption, etc.
  ![image](https://user-images.githubusercontent.com/86367130/123827970-b4c52f80-d91e-11eb-8c7b-f9259ed140c6.png)
  
6.Write_verilog-Use to write the netlist.Netlist I s the representation of the design in the form of standard cells present in the .lib file.
  ![image](https://user-images.githubusercontent.com/86367130/123828041-c3abe200-d91e-11eb-8b2a-0e4b366364d2.png)
  
7.-noattr – With this command no attributes are included in the output
![image](https://user-images.githubusercontent.com/86367130/123828122-d45c5800-d91e-11eb-8066-335d022a8ea4.png)
  
  In order to verify the netlist with simulation results we give the netlist file and the same test bench to the iverilog simulator.
  

# Day-2

# Introduction To Logic Optimization
  
It is mainly done to reduce the logic to the most optimized design. Most optimized design will be in terms of Area and Power.
Techniques of Optimization for Combinational Logic
  
1.Constant Propagation-Direct Optimization technique
2.Boolean Logic Optimization-Techniques such as K-Map and Quine Mckluskey
  
Techniques of Optimization for Sequential Logic
  
1. Basic
• Sequential Constant Propagation
Whenever the Flip-Flop output is constant irrespective of clock and reset/set signals, then it is in the state of Sequential Constant.
This state of the Flip-Flop can be further optimized.
Otherwise, if it is taking values both 1 and 0, then it is not in the state of Sequential Constant.

2. Advanced
  
• State Optimization-Optimization of Unused States
  
• Retiming-It is done by slicing or Logic Partitioning to balance the timing across the circuit in order to get better performance with increased frequency.
  
• Sequential Logic Cloning-It causes multiple instances of input flip flop with Large Positive Slack.
  
Lab Examples of Optimization
  
1. Logic Optimized to AND Gate
  
This is an example of Boolean Logic Optimization.
![image](https://user-images.githubusercontent.com/86367130/123829342-028e6780-d920-11eb-96ab-266ac06eb59c.png)
  
Command to do Constant Propagation and Optimization is: opt_clean -purge
![image](https://user-images.githubusercontent.com/86367130/123829518-26ea4400-d920-11eb-97de-a1019881ea82.png)

A 2-input AND gate is synthesized after Logic Optimization
  
2.Optimization to OR Gate
  
The below logic gets optimized to 2-input OR Gate
![image](https://user-images.githubusercontent.com/86367130/123829591-38335080-d920-11eb-8252-7c0b03768fc8.png)
  
![image](https://user-images.githubusercontent.com/86367130/123829664-45e8d600-d920-11eb-9ca0-02231edacb5b.png)

OR Gate Design
![image](https://user-images.githubusercontent.com/86367130/123830946-6ebd9b00-d921-11eb-94f6-af1f33df231d.png)

3.Optimization to 3-input AND Gate

The given logic gets optimized to 3-input And Gate
![image](https://user-images.githubusercontent.com/86367130/123831034-86951f00-d921-11eb-833a-60dcc121c9ac.png)
  
Design
![image](https://user-images.githubusercontent.com/86367130/123831071-8f85f080-d921-11eb-97cd-a33ef57766f1.png)
  
4.Optimization to 2-Input X-OR Gate

  ![image](https://user-images.githubusercontent.com/86367130/123831182-b04e4600-d921-11eb-95f6-6f70e404e8be.png)
  
![image](https://user-images.githubusercontent.com/86367130/123831204-b512fa00-d921-11eb-82ed-7d2070aaf1e6.png)
  
Instead of realising 2 Multiplexer, one single XNOR gate is realised.
  
5.Multiple Module Optimization
  
Instead of realising 2 gates, one single gate is realised
  
  Code
  
![image](https://user-images.githubusercontent.com/86367130/123831357-de338a80-d921-11eb-9fbb-3e4cbbc25ccf.png)
  
  Design

![image](https://user-images.githubusercontent.com/86367130/123831405-eb507980-d921-11eb-986d-292589c3708f.png)
  
  Ab+c is realised and got optimised as shown above.
 
 6.Mulitple Module Optimization-2

Y is optimized to 1 without using any Gate
 
![image](https://user-images.githubusercontent.com/86367130/123842276-383a4d00-d92e-11eb-877f-06155592fad1.png)
 
![image](https://user-images.githubusercontent.com/86367130/123842358-51db9480-d92e-11eb-8911-abb2dea8dbae.png)
 
 Sequential Optimization- Sequential Constant Propagation
 
Lab Examples of DFF Flip-Flops
 
Example-1
 
 ![image](https://user-images.githubusercontent.com/86367130/123842514-7f284280-d92e-11eb-83ca-060915d0928f.png)
 
In dff_const_1 design Dff is set to 0 at reset else high
 
 ![image](https://user-images.githubusercontent.com/86367130/123842598-936c3f80-d92e-11eb-8837-6d27e390f5c6.png)
 
 Design: A dff is realised
 
![image](https://user-images.githubusercontent.com/86367130/123842693-b26ad180-d92e-11eb-88e5-82b63a58d348.png)
 
 Example-2
 
The output of the D-FF is always set 1 irrespective of reset or clock
 
 ![image](https://user-images.githubusercontent.com/86367130/123842832-d9290800-d92e-11eb-8a81-986968e6cfbd.png)
 
After Synthesizing
Because, library is having active low reset so it is inferring an inverter in order to have reset as active high. No flip-flop is realised q is assigned the value of 1
 
 ![image](https://user-images.githubusercontent.com/86367130/123842954-f65dd680-d92e-11eb-8692-95eeb00ae3a6.png)
 
Example-3
 
 ![image](https://user-images.githubusercontent.com/86367130/123843031-0d9cc400-d92f-11eb-9e1f-398ac03906fb.png)
 
 ![image](https://user-images.githubusercontent.com/86367130/123843067-19888600-d92f-11eb-873e-66a589c8fc0f.png)
 
 2 Flip-flops are realised with q1 given as input 1 and q is assigned q1
 
 ![image](https://user-images.githubusercontent.com/86367130/123843110-27d6a200-d92f-11eb-976c-ed66ea2361c0.png)

Example-4
 
 ![image](https://user-images.githubusercontent.com/86367130/123843211-46d53400-d92f-11eb-9bed-3f715ab6599a.png)

 ![image](https://user-images.githubusercontent.com/86367130/123843234-4e94d880-d92f-11eb-9025-593bdcfef029.png)
 
 ![image](https://user-images.githubusercontent.com/86367130/123843264-5785aa00-d92f-11eb-93e5-b09223c1284b.png)
 
When reset q and q1 are1 else q1 is 1 and q is assigned q1. So, both the flip-flops are always one
 
 Example-5

 Code
 ![image](https://user-images.githubusercontent.com/86367130/123843383-7b48f000-d92f-11eb-8763-331f15bf06f0.png)
 
 Waveform
 ![image](https://user-images.githubusercontent.com/86367130/123843449-88fe7580-d92f-11eb-8c7f-f685bf987577.png)
 
 Design
 
 ![image](https://user-images.githubusercontent.com/86367130/123843478-9287dd80-d92f-11eb-8d48-87fbf924e663.png)
 
 Unused Output Optimization
 
 Example-1
 
 Code
 ![image](https://user-images.githubusercontent.com/86367130/123843558-aaf7f800-d92f-11eb-89a2-b722b339862b.png)
 
 Gates Used
![image](https://user-images.githubusercontent.com/86367130/123843581-b2b79c80-d92f-11eb-894c-6722bf34d0df.png)
 
 Design
 ![image](https://user-images.githubusercontent.com/86367130/123843659-c95df380-d92f-11eb-8f82-731a363d08d0.png)
 
 Toggle Flip-Flop is realised as output is just last bit of the count which keeps toggling on every clock cycle
 
Example-2
 
Code-
 
 ![image](https://user-images.githubusercontent.com/86367130/123843880-fca08280-d92f-11eb-94be-f98465280637.png)

Design Realised
 
 ![image](https://user-images.githubusercontent.com/86367130/123843920-06c28100-d930-11eb-9991-aaa12ff19e2e.png)
 
 
# GLS, Blocking vs Non-blocking and Synthesis Simulation Mismatch
 
 Gate Level Simulation (GLS)
 
What is GLS?
 
Running the test bench with Netlist as Design Under Test. As Netlist is logically same as RTL Code same Test Bench will align with the design. So, we plug the Netlist in place of RTL code and run the simulation.
 
Why?
 
In order to verify the logical correctness of the design after synthesis we perform GLS. As design might not be synthesizing correct logic. GLS also ensured timing design is met for which GLS needs to be run with delay annotation.
 
GLS Flow
 
 ![image](https://user-images.githubusercontent.com/86367130/123844790-12fb0e00-d931-11eb-8db6-713408688ba1.png)
 
Gate Level Verilog Models contain information regarding gates in the netlist. These models can be either Timing or Functional Aware. If only Functional aware then we can validate only the functionality and if Timing aware then we can validate both Functionality and Timing of the gates.
 
Synthesis Simulation Mismatch
 
Synthesis and Simulation mismatch can occur due to the following:
 
• Missing Sensitivity List
 
• Blocking V/s Non-Blocking Assignment
Inside always block:
= Blocking assignment statements are executed one after the another in the order in which they are written.
<= Non-Blocking assignment statements executes all RHS statements parallelly and assign then to the LHS
Incorrect use of Blocking statements to create sequential logic can result in Simulation and Synthesis Mismatch, so it is always recommended to use NON-Blocking Assignment statements for Sequential Logic.
              
• Non-Standard Verilog Coding
              
Hence, we should check the behaviour of the circuit with GLS
              
Lab Examples
              
1.Ternary_Operator_mux
2.Bad_mux
3.Good_mux
              
Following is the Verilog Code:
              
![image](https://user-images.githubusercontent.com/86367130/123845189-843ac100-d931-11eb-8e62-8e8ab28067c5.png)
              
1.Ternary_Operator_mux
              
The below waveform after simulation clearly indicates the behaviour of 2:1 Mux.  
              
![image](https://user-images.githubusercontent.com/86367130/123845433-cd8b1080-d931-11eb-9300-ed2abb298320.png)

![image](https://user-images.githubusercontent.com/86367130/123845346-b4825f80-d931-11eb-96e0-a7daeddb1c16.png)
              
Hence, a 2:1 MUX is synthesized.

![image](https://user-images.githubusercontent.com/86367130/123845546-ee536600-d931-11eb-8e2d-5811eb5f8fff.png)

![image](https://user-images.githubusercontent.com/86367130/123845618-0925da80-d932-11eb-9900-57553e4b39cd.png)

Clearly the waveform after simulation and synthesis matches.
              
2.Bad_mux.v
              
Simulation Waveform-Here y is not following the changes in i1 or i0, only changing its value at the rising edge of sel.

![image](https://user-images.githubusercontent.com/86367130/123845794-3e322d00-d932-11eb-8e47-efc2cd9c472a.png)

Waveform after Synthesis Using Netlist-Here y is following the changing in i1 and i0.

![image](https://user-images.githubusercontent.com/86367130/123845864-530ec080-d932-11eb-910b-7969f442713c.png)

Both the waveforms obtained after simulation and synthesis are different, this clearly indicated Simulation and Synthesis Mismatch
              
Example- Synthesis and Simulation Mismatch because of Blocking Statements
              
Verilog Code
              
![image](https://user-images.githubusercontent.com/86367130/123845985-76d20680-d932-11eb-9553-cb76033c1664.png)
              
  At the pointer, we can see that past values a and b are considered and anded with c to give the present value of d. It seems as if a and b are flopped
              
![image](https://user-images.githubusercontent.com/86367130/123846140-9c5f1000-d932-11eb-9d24-9839b2048885.png)

After Synthesis-y is evaluating at present value of a and b.

![image](https://user-images.githubusercontent.com/86367130/123846217-b6005780-d932-11eb-8608-4bd5c0ca5e29.png)
              
So, this is clearly simulation and synthesis mismatch because of blocking statements
              
So, it is advisable to use Non-Blocking Statements.

# If, Case, For Loop and for generate
 
 If-else statement-It is mainly used for priority Logic
              
Cautions with If-
              
An incomplete If statement results in an Inferred Latch. Suppose we do not give else statement in if construct, then the synthesizer will synthesize a latch which will infer to the past value of output in absence of an else block.
We should not have incomplete if statements unless it is intended.
Incomplete If’s should be avoided especially in combinational circuits.
              
Case statement-
Caveats-
1.Incomplete case will also lead to Inferred Latches. To avoid this, we should add a default case in the code.
2.Partial Assignments In case- This will create an Inferred Latch. So, we should assign all the outputs in all the segments of case.
Comparison in If-else and case
If-else has a clear priority. Only one segment will execute either if, if -else or else whereas in case if more than one condition matches then it will execute both the condition in the order they appear. So, we should not have overlapping case statements.
              
For Loop-
• Used inside always block
• Evaluating expressions
• Not for instantiating hardware
              
Generate For –
• Always used outside the always block.
• Used for instantiating a hardware multiple time
              
Lab cases
              
1.Incomplete If construct:
              
The code is without else.
              
![image](https://user-images.githubusercontent.com/86367130/123846623-3c1c9e00-d933-11eb-9c42-f6aa0ff66621.png)
 
Y follows i1 if i0 is high but latching onto its previous value if i0 is low, thereby resulting in an Inferred Latch

![image](https://user-images.githubusercontent.com/86367130/123846686-4f2f6e00-d933-11eb-9211-5f47eea37643.png)

 Clearly, a D-Latch in inferred in synthesis

![image](https://user-images.githubusercontent.com/86367130/123846762-65d5c500-d933-11eb-856a-51d052c76d7b.png)

I2 is not used and y is latched to i1 without creating a Mux.
  
![image](https://user-images.githubusercontent.com/86367130/123846833-7ab25880-d933-11eb-8462-3f492a61167e.png)

2. Second Case of Incomplete -If:
              
Verilog Code- If is without else block
              
![image](https://user-images.githubusercontent.com/86367130/123846921-90278280-d933-11eb-89e5-9a784ca93e56.png)

When i0 if high y follows i1 otherwise it checks for i2 and when i2 and i3 both are y latches to its previous value.
              
 ![image](https://user-images.githubusercontent.com/86367130/123846981-a33a5280-d933-11eb-88d5-a3f02f66548e.png)

 Clearly, it is inferring a latch

![image](https://user-images.githubusercontent.com/86367130/123847055-bbaa6d00-d933-11eb-8d7e-2af4f841b12e.png)

So, a nor is synthesized for the logic of the enable of D-Latch. If both i0 and i2 are low then the latch goes high. A 2:1 mux is present with i0 as select which if high then y is i1 else i3. 

  ![image](https://user-images.githubusercontent.com/86367130/123847129-d11f9700-d933-11eb-953b-f154e6b03cd6.png)
              
Hence, resulting in an Inferred Latch in case of incomplete if statement.
              
3.Case Statements-Incomplete Case
              
If sel is 00 , y is i0
If sel is 01 , y is i1 else y will latch.

![image](https://user-images.githubusercontent.com/86367130/123847191-ed233880-d933-11eb-9989-81a445493930.png)
              
When sel is 00 y follows i0, when 11 if follows i1 and when it is 10 or 11 then y is latching to its previous value.
              
![image](https://user-images.githubusercontent.com/86367130/123847249-00ce9f00-d934-11eb-8540-e8c23a1882c7.png)
              
 Gates Synthesized
              
 ![image](https://user-images.githubusercontent.com/86367130/123847308-15ab3280-d934-11eb-991e-34ae851f96ad.png)

 So, after synthesis a D-Latch is inferred in the design because o the absence of else block.
              
 ![image](https://user-images.githubusercontent.com/86367130/123847402-2eb3e380-d934-11eb-956b-9a6c4f3a92e5.png)
             
4.Complete Case with No Inferred Latch
              
![image](https://user-images.githubusercontent.com/86367130/123847490-44c1a400-d934-11eb-8d77-2d85dc2d21e9.png)
              
When sel is 00 y is i0 , when 01 y is i1 else y is i2.Hence, no latching
              
![image](https://user-images.githubusercontent.com/86367130/123847536-530fc000-d934-11eb-8195-791c9e5c492d.png)

Clearly, no latching this time all gate synthesized are combinational logic
              
![image](https://user-images.githubusercontent.com/86367130/123847601-66229000-d934-11eb-82cb-1024e4ff8e81.png)

Design:
              
![image](https://user-images.githubusercontent.com/86367130/123847659-776b9c80-d934-11eb-8f47-0b266408d912.png)

Hence, no latch is inferred.
              
5.Partial-Assignments
              
![image](https://user-images.githubusercontent.com/86367130/123847749-92d6a780-d934-11eb-8536-4217e4e8225d.png)
              
When For x, when sel is 00, then x is i2 otherwise it is i1 and latched to its previous value for nand of sel0 and not(sel1).
              
![image](https://user-images.githubusercontent.com/86367130/123847863-ac77ef00-d934-11eb-8e07-71b0b6a0e77b.png)

 X in inferred with a Latch because Partial assignments
              
6.Overlapping case
              
![image](https://user-images.githubusercontent.com/86367130/123847959-c580a000-d934-11eb-8ca9-e725b48a34f9.png)

Waveform:
When sel is 11, it is latching to an output of 1 as it gets confused with the value.
              
![image](https://user-images.githubusercontent.com/86367130/123847998-d29d8f00-d934-11eb-9365-af92060e62f1.png)

Design:

A mux_4 is created
              
 ![image](https://user-images.githubusercontent.com/86367130/123848125-f8c32f00-d934-11eb-9b9c-b2fcbc425385.png)

Gtkwave of Netlist
Here y is referring to i3 when sel is 11
              
![image](https://user-images.githubusercontent.com/86367130/123848185-07a9e180-d935-11eb-98f0-cf8d235ccb7a.png)
              
So, there is mismatch between synthesis and simulation wave.
              
Lab of For and For Generate
              
1. A 4:1 Mux using For
Code-Here for loop is used to create a 4:1 mux . It evaluates
              
![image](https://user-images.githubusercontent.com/86367130/123848267-27d9a080-d935-11eb-83a6-4d999cd6304d.png)

Gtkwave
              
So, when sel is 00 y is i0
sel is 10 y is i1
sel is 10 y is i2
sel is 11 y is i3              
              
![image](https://user-images.githubusercontent.com/86367130/123848315-39bb4380-d935-11eb-8cca-fa92cf222770.png)

Design:
Here a 4:1 Mux is synthesized with 2 select lines and an extra D Latch because of the else block in the code.
              
 ![image](https://user-images.githubusercontent.com/86367130/123848381-4b9ce680-d935-11eb-9871-717a44b12c72.png)

The waveform of the netlist matches with the waveform of RTL code.
              
 ![image](https://user-images.githubusercontent.com/86367130/123848450-5ce5f300-d935-11eb-830e-d63109063f74.png)

 Hence, for loop generates a 4:1 mux or a mux with higher inputs and reduces the effort of writing many lines of code.
No simulation and synthesis mismatch is found.
              
2. Demux Using For Construct             
              
![image](https://user-images.githubusercontent.com/86367130/123848518-71c28680-d935-11eb-8a57-6cc42eeb0bcc.png)

Demux_case
              
![image](https://user-images.githubusercontent.com/86367130/123848608-8bfc6480-d935-11eb-9bc0-a9de9900122f.png)

![image](https://user-images.githubusercontent.com/86367130/123848629-9159af00-d935-11eb-885f-4dccccf007a0.png)

Waveform of demux with for loop
              
![image](https://user-images.githubusercontent.com/86367130/123848708-a5051580-d935-11eb-86d0-c73f3d133c7e.png)
              
3.Ripple Carry Adder using For Generate
              
![image](https://user-images.githubusercontent.com/86367130/123848781-b8b07c00-d935-11eb-854d-c712bae1fcdf.png)

 Gtkwave Waveform
              
 ![image](https://user-images.githubusercontent.com/86367130/123848841-c82fc500-d935-11eb-9e96-8a18dc26744d.png)
             
Design of Ripple Carry Adder:
              
8 instances of Full-Adder have been created in Ripple Carry Adder using for generate.
              
![image](https://user-images.githubusercontent.com/86367130/123848930-e1387600-d935-11eb-869b-e46ab03699f0.png)

              

