*****README.txt*****

Andrew Martin 260456771
Joe Steele 260516386
Hyunyung Boo 260513655

***************************
HOW TO LOAD A PROGRAM
***************************

Our RAM is located on the main circuit on the upper right edge.
There are 16 black box circuits lined up vertically with address 0
at the top and address 15 at the bottom. Click the finger icon,
and then double-click the magnifying glass hovering over each
black box to go inside it. Each black box consists of 8 flip-flops
which store the binary values of each data box in RAM. Toggle these
according to the program instructions (see below for a description of
the OP-codes). When ready, you can begin the simulation either by manually
clicking the clock on the top left of the main circuit to trigger each 
tick individually, or from the simulation menu you can set the tick frequency
and enable the automatic simulation. By convention we have been reserving 
the last few bytes for data since we assume the first byte always has the first
program instruction.


**********************
OP code reference
**********************

We have split up our supported instructions into 4 categories of
2-bit op-codes, whereby depending on the category the rest of the 
instruction register stores instruction arguments. The op-code occupies
the two left-most bits of the instruction.

OP-CODE | CATEGORY
------------------
00      | Load/Save
01      | ALU (add/sub)
10      | Branch
11      | Print/Input/Stop/Jump

On top of the required instructions, we have implemented support for two
additional instructions, JUMP and INCREMENT.

Here is a complete table of all supported instructions and their IR format.

Required Instruction Set:

ADD  R1 R2      0100 0000
ADD  R2 R1      0100 1000
SUB  R1 R2      0101 0000
SUB  R2 R1      0101 1000
LD   R1 ADDR    0000 ADDR
LD   R2 ADDR    0001 ADDR
STR  R1 ADDR    0010 ADDR
STR  R2 ADDR    0011 ADDR
BEQ  R1 R2 ADDR 1000 ADDR
BNQ  R1 R2 ADDR 1010 ADDR
PRT  R1         1100 0000
PRT  R2         1100 1000
INP  R1         1101 0000
INP  R2         1101 1000
STOP            1110 0000

Additional Instructions:

JUMP ADDR       1111 address       (jump to [ADDR])
INC  R1         0100 0100          (increment value stored at register [R1])
INC  R2         0100 1100          (increment value stored at register [R2])

*****************************************
LOAD PROGRAM USING READ-ONLY MEMORY (ROM)
*****************************************

If you would like to instead load the program from ROM, do the following.
Rather than manually setting the values in RAM, which reset to 0 when you 
reset the simulation, navigate to the lower-right section of the main circuit;
you will see an array of constant pins lined up in similar fashion to the ram
data boxes. These values are stored in hexadecimal, so refer to the above table
and convert to the corresponding hex number. To set the value, use the pointer icon
and click on the respective constant pin. On the lower left frame one of the properties
of the pin is "value" which is hexadecimal. Just change it. Once you are finished with 
setting up the ROM, to load it into RAM click the "Load" input pin just above and to the
right. ***IMPORTANT*** -- make sure to turn off the load pin immediately after toggling it,
because when this is enabled it plexes the input to RAM to come from ROM instead of the data
bus. During program execution it must be the data bus that is feeding into RAM, so this must
be disabled.