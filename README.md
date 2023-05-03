Download Link: https://assignmentchef.com/product/solved-cs2208b-lab-no-3
<br>
<h2>ADDRESSING MODES</h2>

An addressing mode is simply a means of <em>expressing the location of an operand</em>. An address can be a register such as r3 or PC (<em>Program Counter</em>). An address can be a location in memory such as address 0x12345678. You can even express an address <em>indirectly </em>by saying, for example, “the address is the location whose address is in register r1”. The various ways of expressing the location of data are called collectively <em>addressing modes</em>.




Suppose someone said, “Here is ten dollars”. They are giving you the actual item. This is called a <strong>literal </strong>or <strong>immediate </strong>value because it is what you actually get. Unlike all other addressing modes, you do not have to retrieve addresses from a register or memory location.




If someone says, “Go to room 30 and you will find the money on the table”, they are actually telling you <em>where </em>the money is (i.e., its address is room 30). This is called an <strong>absolute address </strong>because it expresses absolutely exactly where the money is. This addressing mode is also called <strong>direct addressing</strong>. ARM processors do <strong><em>not</em></strong> support this addressing mode.




Now here is where the fun starts. Suppose someone says, “Go to room 40 and you will find something to your advantage on the table”. You arrive at room 40 and see a message on the table saying, “The money is in room 60”. In this case we have an <strong>indirect address </strong>because room 40 does not have the money, but a pointer to where it is. We have to go to a

second room to get the money. Indirect addressing is also called <strong>pointer-based </strong>addressing, because you can think of the note in room 40 as pointing to the actual data.




<em><u>In real life we cannot confuse a room number or an address with a sum of money. However, in a computer all data is</u> <u>stored in binary form and the programmer has to remember whether a variable (or constant) is an address or a data</u> <u>value.</u> </em>




<strong>Immediate (literal) addressing </strong>is indicated by a ‘<strong>#</strong>’ symbol in front of the operand. Thus, #5 in an instruction means the actual value 5. A typical ARM instruction is MOV <strong>r0</strong>,#5 which means move the value 5 into register r0.

<strong> </strong>

<strong>Indirect addressing </strong>is indicated by ARM processors by placing the pointer in square parentheses; for example, [r1]. All ARM indirect addresses are of the basic form LDR <strong>r0</strong>,[r1] or STR r3,<strong>[r6]</strong>.

There are variations on this addressing mode; for example, LDR <strong>r0</strong>,[r1,#4]specifies an address that is four bytes on from the location pointed at by the contents of register r1. It can also has a side effect, such as <em>autoindexing pre-indexed addressing mode</em>, e.g., LDR <strong>r0</strong>,[r1,#4]!  or  <em>autoindexing post-indexed addressing mode</em>, e.g., LDR <strong>r0</strong>,[r1],#4

In all these indirect addressing modes, the offset can be a constant (as indicated in the above examples), or <em>dynamic</em>, by putting the value of the offset in a register, e.g.,

LDR <strong>r0</strong>,[r1,r2]  LDR <strong>r0</strong>,[r1,r2]!  LDR <strong>r0</strong>,[r1],r2

Copyright © 2016 Mahmoud El-Sakka.




<h2>PROBLEM SET</h2>

Before you start practicing this lab, you need to review and fully understand how to use <em>the Keil ARM simulator</em>, as well as the various addressing modes.




<ol>

 <li>The following assembly program adds together a LIST of five numbers stored in memory.</li>

</ol>




AREA Pointers, CODE, READONLY

ENTRY

Start ADR  <strong>r0</strong>,List  ;register r0 points to List

MOV  <strong>r1</strong>,#5     ;initialize loop counter in r1 to 5

MOV  <strong>r2</strong>,#0     ;clear the sum in r2

Loop     LDR  <strong>r3</strong>,[r0]  ;copy the element pointed at by r0 to r3

ADD  <strong>r0</strong>,r0,#4  ;point to the next element in the series

ADD  <strong>r2</strong>,r2,r3  ;add the element to the running total

SUBS <strong>r1</strong>,r1,#1  ;decrement to the loop counter

BNE  Loop      ;repeat until all elements added

Endless B    Endless  ;infinite loop

List    DCD  3,4,3,6,7 ;the numbers to be added together

;each one is 4 bytes (20 bytes in total)

END




(a) Modify the original program to utilize:

○ Autoindexing pre-indexed addressing mode

○ Autoindexing post-indexed addressing mode




(b) Modify the original program by eliminating the instruction  “ADD <strong>r0</strong>,r0,#4”, while keeping the functionality       of the program the same, without using any autoindexing mode.







<ol start="2">

 <li>Using only 7 ARM assembly instructions, execute the following flowchart. Test your code by assigning various values to r0, r1, r2, and r3.</li>

</ol>










<ol start="3">

 <li>Without using any of the ARM multiplication instructions, write only one ARM instruction that executes [R4] ß 16385 × [R4].</li>

</ol>

Manually generate the machine language code for this instruction and verify it using the simulator.




<ol start="4">

 <li>What is the machine language of AND r2,r3,#0x1080</li>

</ol>

Verify it using the simulator.




<ol start="5">

 <li>What is the reverse assembly of the following machine language instruction:

  <ul>

   <li>0x00000000</li>

   <li>0x50076808</li>

   <li>0xE3A01D22 (d) 0xE3A01E88</li>

  </ul></li>

</ol>

Verify it using the simulator. Hint: you may want to consult Table 3.2 and figure 3.26 in the textbook.




<ol start="6">

 <li>What is the reverse assembly of the following machine language instruction: 0xE6DCA408?</li>

</ol>

Verify it using the simulator.

Hint: you may want to consider Figure 3.39 in the textbook.




Copyright © 2016 Mahmoud El-Sakka.