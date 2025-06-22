# 8-Bit-Interrupt-Controller using verilog
# <u>ABSTRACT</u>
 In modern digital systems, the efficient handling of interrupt requests is
 essential for ensuring real-time responsiveness and reliable operation. This
 project aims to design and implement an Interrupt Controller using Verilog
 HDL.
# WHAT IS AN INTERRUPT-CONTROLLER?
An Interrupt Controller is an integrated circuit that manages multiple interrupt requests (IRQs) from external devices and helps the CPU handle them efficiently. It prioritizes IRQs and directs the CPU to the appropriate Interrupt Service Routine (ISR) based on predefined or programmable priority modes like fixed, rotating, or cascading. These controllers are often configurable and are commonly known as Programmable Interrupt Controllers (PICs).
#  BRIEF IDEA:
Interrupt Controllers usually include three main registers: the Interrupt Request Register (IRR), In-Service Register (ISR), and Interrupt Mask Register (IMR). The IRR holds pending interrupts awaiting acknowledgment, while the ISR tracks acknowledged interrupts that are still being serviced (waiting for End of Interrupt or EOI). The IMR defines which interrupts are masked (ignored). This setup allows one interrupt to wait for acknowledgment and another to wait for completion. Common priority schemes include fixed, specific, and rotating priorities.
# TABLE OFCONTENTS
 ● Introduction <br>
 ● Theory <br>
 ● Functions done in our Project <br>
 ● Major components of our Project <br>
 ● Motivation <br>
 ● Novelty <br>
 ● Verilog HDL Code <br>
 ○ Design Code <br>
 ○ Testbench Code <br>
 ● Result <br>
 ● Conclusion <br>
 ● Future Work <br>
 ● References <br>
 # INTRODUCTION
 **THE SOFTWARE USED:** <br>
 XILINX VIVADO (version 2014) as HDL- implementation tool <br>
 **THE HARDWARE USED**: <br>
 NEXYS 4DDRArtix-7 FPGA board <br>
 **Introduction to FPGA:** <br>
 FPGAs, or Field-Programmable Gate Arrays, are dynamic integrated
 circuits allowing post-manufacture programming. They feature a matrix of
 programmable logic blocks and interconnects, enabling users to configure
 custom digital circuits.They are widely used across industries like
 telecommunications, automotive, and consumer electronics, FPGAs are
 prized for rapid prototyping and adaptability. They offer a balance between
 off-the-shelf chips and custom ASICs, accommodating evolving needs
 efficiently.
# THEORY
 As mentioned earlier in this report we are going to discuss about 8259A
 programmable interrupt controllers.Here is a brief theory explaining about
 these PICs’ functionality and architecture. <br>
 
 **8259A PROGRAMMABLE INTERRUPT CONTROLLER :** <br>
 The Intel 8259A is a widely used Programmable Interrupt Controller (PIC), especially in early IBM PCs. It can manage eight vectored priority interrupts for the CPU and comes in a 28-pin Dual Inline Package (DIP), operating on a single +5V DC supply. Designed to reduce both software and real-time overhead, it supports various modes to adapt to different system needs.

When connected to microprocessors like the 8085 (with 5 interrupts) or 8086 (with 2 interrupts), the 8259 significantly expands their interrupt-handling capability. A single 8259 provides 8 interrupt inputs (IR0–IR7) and consolidates them into a single interrupt output to the CPU. For example, interfacing it with the 8085 increases its interrupt levels from 5 to 8.

 
