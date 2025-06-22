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

#  Key Features of the Intel 8259 PIC include:
  1.Designed specifically for compatibility with Intel 8085 and Intel 8086
 microprocessors. <br>
 
 2.Programmable for either level-triggered or edge-triggered interrupt levels. <br>
 
 3.Allows for the masking of individual bits in the interrupt request register. <br>
 
 4.Capable of extending interrupt handling capability to 64 levels by <br>
 cascading additional 8259 PICs. <br>
 
 5.Operates without the need for a clock cycle <br>
 
 #  Functional description :
 The 8259A plays a key role in handling system interrupts. With 8 interrupt input lines, it receives requests from external devices, determines their priority, and sends an interrupt signal to the CPU. It can be expanded to handle up to 64 interrupt levels using cascading. Once an interrupt is accepted, the 8259 provides the CPU with the address of the corresponding Interrupt Service Routine (ISR), allowing the CPU to jump directly to the handler. Being programmable, it offers various modes of operation, letting programmers tailor the interrupt handling process to specific system needs.

#  Common functions/features of all PICs:
Typical PICs offer functions such as interrupt handling, prioritization, masking, vectoring, arbitration, acknowledgment, routing, cascading, fault tolerance, and power management. However, this project will focus on a few key features, using the 8259A as the primary theoretical example—especially relevant for systems using 8085 and 8086 microprocessors. The Verilog code developed for this project demonstrates a generic 8-bit interrupt controller, showcasing two fundamental features.

#  FUNCTIONS DONE IN OUR PROJECT :
 As we discussed earlier the code for our project is for a simple 8-bit
 interrupt controller.Here there are two major functions performed in our
 project. The two modes are polling and custom priority.

# Polling:
In polling mode, the processor sends xxxx_xx01 on the bus for one cycle, prompting the controller to check all interrupt sources. If an interrupt is active, intr_out is set to 1. On receiving a High–Low–High transition on intr_in, the controller sends 01011_intrID on the bus. After another similar acknowledgment, the processor signals completion with 10100_intrID. If the interrupt ID matches, the controller moves to the next source; otherwise, it resets.

# Custom Priority:
Custom priority mode works like polling but follows a user-defined priority instead of fixed order. After reset, sending xxxyyy10 sets the highest (xxx) and second-highest (yyy) priority. This input is repeated four times to set all eight priorities. The controller then checks for active interrupts in that order. Unlike polling, it uses 10011 to send interrupt info and expects 01100 as acknowledgment from the processor.

# MAJOR COMPONENTS OF OUR PROJECT:
**1. Data bus buffer:** <br>
Acts as a bridge between the 8259 and 8085/8086 microprocessors. It transfers control words from the CPU to the 8259 and sends the selected interrupt’s opcode and ISR address back to the CPU. It’s an 8-bit buffer (D0–D7), handling 8 bits of data at a time.

**2. Interrupt Request Register (IRR):** <br>
Stores all active interrupt requests that are waiting to be serviced.

**3. Interrupt Service Register (ISR):** <br>
Holds interrupts currently being serviced by the CPU.

**4. Priority Resolver:** <br>
Analyzes the IRR, ISR, and mask register to identify the highest priority interrupt, then updates the ISR accordingly.

# MOTIVATION
**What made us choose this project?** <br>
We chose this project to ensure we gain meaningful, practical knowledge. Building an Interrupt Controller as a mini FPGA project aligns with key learning goals:

**1. Real-World Relevance:** <br>
Interrupt controllers are vital in real-world systems and widely used in microcontrollers, which power most devices we use daily.


**2. Embedded Systems Focus:** <br>
As ECE students, understanding embedded systems is crucial. Since interrupt controllers are core to these systems, this project deepens our grasp of their role and design.


**3. Microcontroller Architecture Insight:** <br>
This project connects directly to microprocessor/microcontroller architecture, helping us understand how these systems manage and respond to hardware events.


**4. System Responsiveness:** <br>
By designing an interrupt controller, we explore how systems handle multiple interrupts efficiently, improving our understanding of real-time responsiveness.

# NOVELTY
The key novelty in our mini project is the inclusion of Interrupt Masking. This feature allows the system to selectively disable lower-priority interrupts while handling critical ones, improving efficiency and responsiveness—especially in real-time applications. Implemented using hardware logic in FPGA, interrupt masking helps customize interrupt handling based on application needs, enhancing both performance and reliability.

# CONCLUSION
Our goal was to design an interrupt controller that efficiently handles and prioritizes multiple interrupt sources. Through both theory and practical work, we built a functioning controller that meets project objectives. While not as advanced as commercial PICs, it demonstrates a solid understanding of core concepts.

Using the Artix-7 FPGA, Vivado, and Verilog, we validated our design for integration into real-time microcontroller systems. This project not only enhanced our technical knowledge but also improved our teamwork, problem-solving, and project management skills—key traits for any engineer.

# FUTURE WORK
Future improvements can enhance the usefulness and efficiency of our interrupt controller. Some potential directions include:

**1. Level-Triggered Interrupts:** <br>
Currently, we use edge-triggered inputs. Shifting to level-triggered interrupts could make the system more stable and versatile.


**2. Advanced Modes:** <br>
Implementing auto-rotation or fully-nested modes would align the controller more closely with real-world applications.


**3. Power Optimization:** <br>
Exploring energy-efficient techniques like adaptive power management or low-power standby modes can make the controller more suitable for mobile and embedded systems.

# REFERENCES
 1. www.geeksforgeeks.org <br>
 2. www.wikipedia.org <br>
 3. www.github.com <br>
 4. Care4you.in (engineering theory references) <br>
 5. www.youtube.com <br>

