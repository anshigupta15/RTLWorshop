
# [#c5f015] Workshop On RTL Design Using Verilog With Sky 130 Technology
![image](https://user-images.githubusercontent.com/86367130/123824988-22239100-d91c-11eb-95ae-bf2f17e4e701.png)

# Contents

 + Day-1-Introduction to RTL Design And Synthesis

 + Day-2 Hierarchical Vs Flat Synthesis and Efficient Flip-Flop Coding Styles

 + Day-3 Introduction To Ligic Optimization

 + Day-4 GLS, Blocking vs Non-blocking and Synthesis Simulation Mismatch

 + Day-5 If, Case, For Loop and for generate



# Day-1


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

# Day-3 Introduction To Logic Optimization
  
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




  
# Day-4
  
# Day-5 
 
  



 
