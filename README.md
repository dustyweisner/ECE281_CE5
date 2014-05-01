ECE281_CE5
==========

MIPS Assembly Program


__*PART ONE*__


|CODE|COMMENTS|
|:-----------------------|:------------------------|
|addi $S0, $S0, 0x002C|#Stores S0 + 44 into S0|
|addi $S1, $S1, 0xFFDB|#Stores S1 - 37 into S1|
|add $S0, $S1, $S2|#Stores S0 + S1 into S2|
|sw $S2, 0x0054($0)|#Stores S2 into hexadecimal memory address x54|


Because there is no initialize instruction, MIPS actually just adds what is already in the register (0 if initializing) with whatever it wants to initialize the register with.


__*PART TWO*__


|CODE|op|rs|rt|rd|shamt|funct|TYPE|
|:----------|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|addi $S0, $S0, 0x002C|001000|10000|10000|00000|00000|101100|I|
|addi $S1, $S1, 0xFFDB|001000|
|add $S0, $S1, $S2|000000|
|sw $S2, 0x0054($0)|110000|
