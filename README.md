# Minecraft-CPU
A CPU with an 8 bit instruction set connected to a RAM with 4 bit addresses. Built in Minecraft. Inspiration/knowledge for this project came from the Crash Course Computer Science Youtube series. World download is the 'Computer Stuff' folder.

The CPU uses real designs for cicuits replicated with Minecrafts redstone blocks (blocks that act like electrical wires). Some circuits used in this CPU include AND gates, OR gates, NOT gates, and XOR gates. I combined these gates to form gated latches (memory), half adders and ripple carry adders. I then built a control unit to activate these components at the right time in the right order based on what instruction it was fed to make a working CPU.

The componens of the CPU include:
- A 4 bit instruction address register
- An 8 bit instruction register
- An ALU capable of addition and comparison of 4 bit numbers
- 16 bytes of RAM
- 2 registers used for addition
- A control unit that decodes the instructions
See screenshots for details.

There is not really an automatic clock for this CPU, the "clock" I have is just 3 buttons that
1. Load instruction from RAM
2. Execute instruction
3. Increment instruction address by 1
These buttons must be manually pushed by the player. Basically, the player is the clock.

The instruction set for this CPU is as follows (Note ---- means a 4 bit RAM address).
out ---- = 0100---- (prints the value at that address)
lodA ---- = 0001---- (loads the value in RAM at the address into register A)
lodB ---- = 0010---- (loads the value in RAM at the address into register B)
add ---- = 0011---- (adds the values in register A and B and moves the result to the address in RAM)
goto ---- = 0101---- (sets the current instruction address to be the specified address)

Here is a sample program that would add 5 and 3 and print the result (in binary)
First, I would manually have to store the value 5 (0000 0101) at address 0000 in RAM
Next, I would manually have to store the value 3 (0000 0011) at address 0001 in RAM

Here is the assembly:
lodA 0000 (load the value 5 into register A)
lodB 0001 (load the value 3 into register B)
add 0010 (add the values in the registers and store the result at address 0010)
out 0010 (print the value at address 0010)

And here is the program in binary:
00010000
00100001
00110010
01000010

Next, I have to store this program in RAM, and I must carefully choose where to store it. Addresses 0000, 0001, and 0010 will be used by my program during runtime, so I will start at address 0011. Note that the highest address we can use is 1111. Loading values into RAM is done manually (sort of like punched cards).
0011 -> 00010000
0100 -> 00100001
0101 -> 00110010
0110 -> 01000010

Then, I need to manually store the start address of my program (0011) in the instruction address register.

Now, we are ready to execute. Press the 'clock' buttons 1, 2, 3 in that order 4 times to execute the 4 instructions. If everything works correctly the printer will have put out 00001000 (using its red and black blocks), meaning 8.
