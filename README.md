
# Workshop On RTL Design Using Verilog With Sky 130 Technology
![image](https://user-images.githubusercontent.com/86367130/123824988-22239100-d91c-11eb-95ae-bf2f17e4e701.png)

# Contents

Day-1-Introduction to RTL Design And Synthesis
1.<div class="text-white bg-blue mb-2">
  
</div>
Day-2 Hierarchical Vs Flat Synthesis and Efficient Flip-Flop Coding Styles

Day-3 Introduction To Ligic Optimization

Day-4 GLS, Blocking vs Non-blocking and Synthesis Simulation Mismatch

Day-5 If, Case, For Loop and for generate



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

  



 
