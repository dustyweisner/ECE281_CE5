ECE281_CE5
==========

MIPS Assembly Program


__*PART ONE*__


|CODE|COMMENTS|
|:-----------------------|:------------------------|
|addi $S0, $0, 0x002C|#Stores 0 + 44 into S0|
|addi $S1, $0, 0xFFDB|#Stores 0 - 37 into S1|
|add $S0, $S1, $S2|#Stores S0 + S1 into S2|
|sw $S2, 0x0054($0)|#Stores S2 into hexadecimal memory address x54|


Because there is no initialize instruction, MIPS actually just adds what is already in the register (0 if initializing) with whatever it wants to initialize the register with.


__*PART TWO*__


|CODE|op|rs|rt|rd|shamt|funct|TYPE|INSTRUCTION|
|:----------|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|addi $S0, $0, 0x002C|001000|00000|10000|00000|00000|101100|I|0x2010002C|
|addi $S1, $1, 0xFFDB|001000|00000|10001|11111|11111|011011|I|0x2011FFDB|
|add $S0, $S1, $S2|000000|10000|10001|10010|00000|100000|R|0x02119020|
|sw $S2, 0x0054($0)|101011|00000|10010|00000|00000|110100|I|0xAC120054|


Below is the waveform that the instructions above created:


![](https://github.com/dustyweisner/ECE281_CE5/blob/master/Part2_Waveform.GIF?raw=true)


According to the waveform, my instructions did what they were supposed to. If you look at wd, it shows each value that is being stored in their registers. 44-37 = 7, and from 20 to 30 ns, 00000007 is stored, which is the value of the two added registers.


__*PART THREE*__


Below are the Main Decoder, ALU Decoder, and Schematic Modifications respectively, altered so that the MIPS assembly includes the instruction "ORI":

![](https://github.com/dustyweisner/ECE281_CE5/blob/master/MainDecoder.png?raw=true)

![](https://github.com/dustyweisner/ECE281_CE5/blob/master/ALUDecoder.png?raw=true)

![](https://github.com/dustyweisner/ECE281_CE5/blob/master/Schematic_Modification.GIF?raw=true)

Because I have to make the ORI instruction immediate, I made a "Zero Extend" so that it changed the number to a 32 bit number with out changing the number. Then I added to the MUX, and Added another bit to the ALUsrc.

To do that in vhdl was an entirely different story. First I had to go through and change all of the alusrc signals to STD_LOGIC_VECTOR(1 downto 0). Then I had to add the ORI instruction to both the Main and ALU decoder, which can be viewed in "Mips.vhd" on the ECE281_CE5 homepage. After doing so I made sure that there were now 10 instead of 9 controls because the alusrc was now 2 bits. Then I had to copy a mux but make it a mux of 4 bits and declare it and make its architecture. After that I changed the behavior of the mux, and I made the zero extend architecture and declaration. Finally I changed the ALU input to the new 4 bit mux. I added the following code to the testbench to demosntrate an ORI instruction:

![](https://github.com/dustyweisner/ECE281_CE5/blob/master/Code_Test.GIF?raw=true)

After inserting all of the changes into the Mips assembly program, I tested the resulting waveform as shown below:

![](https://github.com/dustyweisner/ECE281_CE5/blob/master/Part3_Waveform.GIF?raw=true)

I knew that this waveform did as expected because I looked at the memory address which showed the correct answer to the ORI of -37 and 44. The answer was "0000ffff" because -37 (0000000000101100) or 44 (1111111111011011) is -1 (1111111111111111), which is also ffff, but since it needs to be a 32 bit number, the ORI instruction that I created now extends the rest of the number to 0000ffff.
