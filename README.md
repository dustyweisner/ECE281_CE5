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



