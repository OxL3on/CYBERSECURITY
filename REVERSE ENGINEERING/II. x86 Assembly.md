# x86 Assembly Crash Course


### **Opcodes and Operands**

1. **What are Opcodes?**
   - Opcodes are like "action commands" for the CPU. They tell the CPU what to do.
   - These are represented as hex numbers in the program (e.g., `b8` means "move something into the `eax` register").
   - A **disassembler** translates these hex codes into readable assembly instructions like `mov eax, 0x5f`.

2. **What are Operands?**
   - Operands are the "things" the CPU works on. There are three main types:
     - **Immediate Operands**: Fixed values, like `0x5f` (a constant number).
     - **Registers**: Small storage spots inside the CPU, like `eax` or `ebx`.
     - **Memory Operands**: Locations in RAM, written with square brackets like `[eax]`. This means "use the value in `eax` as a memory address."

3. **Little-Endian Format**
   - Numbers are stored "backward" in memory. For example:
     - The value `0x5f` is stored as `5f 00 00 00` in memory.
     - This is called **little-endian**, where the smallest part of the number comes first.

4. **How It All Works Together**
   - Example: The instruction `mov eax, 0x5f` looks like this in memory:
     ```
     b8 5f 00 00 00
     ```
     - `b8`: Opcode for "move into `eax`."
     - `5f 00 00 00`: The value `0x5f` in little-endian format.


**Remembering Tip**:
Think of it like giving directions to a friend:
- **Opcode**: The action ("Go to the store").
- **Operands**: The details ("Take $10" or "Drive to Main Street").
- **Little-Endian**: Writing the address backward, like "5F Main St" instead of "Main St 5F."

---
---



### **General Instructions**


#### **1. The MOV Instruction**
- Moves data between registers, memory, or immediate values.
- Syntax: `mov destination, source`
  - Example: `mov eax, 0x5f` → Moves the value `0x5f` into `eax`.
  - Example: `mov ebx, eax` → Copies the value in `eax` to `ebx`.
  - Example: `mov eax, [ebp+4]` → Moves the value at memory address `ebp+4` into `eax`.

**Key Point**: Square brackets `[ ]` mean "access memory."


#### **2. The LEA Instruction**
- Stands for **Load Effective Address**.
- Syntax: `lea destination, source`
- Moves the **address** of the source into the destination (not the value at the address).
  - Example: `lea eax, [ebp+4]` → Calculates `ebp+4` and stores the result (address) in `eax`.

**Why Use LEA?**
- Often used for quick arithmetic (e.g., adding offsets) without accessing memory.


#### **3. The NOP Instruction**
- Stands for **No Operation**.
- Does nothing but takes up one CPU cycle.
- Syntax: `nop`
- Used by malware authors to create a **NOP sled**:
  - A sequence of `nop` instructions to ensure execution lands safely on malicious code.


#### **4. Shift Instructions**
- Shift bits left (`shl`) or right (`shr`) in a register.
- Syntax: `shl/ shr destination, count`
  - Example: `shl eax, 1` → Shifts bits in `eax` left by 1 (multiplies by 2).
  - Example: `shr eax, 1` → Shifts bits in `eax` right by 1 (divides by 2).

**Key Point**: 
- Bits shifted out are lost; new bits are filled with zeros.
- The **carry flag (CF)** holds the last bit shifted out.

**Why Use Shifts?**
- Faster than multiplication/division by powers of 2.


#### **5. Rotate Instructions**
- Similar to shifts but **wrap around** the bits instead of losing them.
- Syntax: `rol/ ror destination, count`
  - Example: `ror al, 1` → Rotates bits in `al` to the right by 1.
  - Example: `rol al, 1` → Rotates bits in `al` to the left by 1.

**Key Difference from Shifts**:
- Overflowing bits are rotated back to the other end (no loss of data).


### **Remembering Tips**
- Think of these instructions like simple actions:
  - **MOV**: Moving items from one place to another.
  - **LEA**: Writing down an address instead of picking up what’s at the address.
  - **NOP**: Taking a step but not moving forward.
  - **Shifts**: Sliding bits left or right (like multiplying/dividing by 2).
  - **Rotates**: Spinning bits around in a circle.

---
---



### **Flags**


#### **What Are Flags?**
- Flags are **bits** in the **EFLAGS register** that indicate the outcome of operations.
- They help the CPU make decisions, like whether to jump or continue execution.


#### **Common Flags and Their Meanings**

1. **Carry Flag (CF)**:
   - Set if there’s a carry-out (or borrow) during arithmetic.
   - Example: Adding two large numbers that overflow.

2. **Parity Flag (PF)**:
   - Set if the result has an **even number of 1s** in the least significant byte.
   - Example: `0101` → PF = 1 (even), `0111` → PF = 0 (odd).

3. **Auxiliary Flag (AF)**:
   - Used for **BCD arithmetic** (rarely seen in modern code).
   - Set if there’s a carry between bit 3 and bit 4.

4. **Zero Flag (ZF)**:
   - Set if the result of an operation is **zero**.
   - Example: Subtracting equal numbers → ZF = 1.

5. **Sign Flag (SF)**:
   - Set if the result is **negative** (most significant bit = 1).
   - Example: `1000` → SF = 1 (negative).

6. **Overflow Flag (OF)**:
   - Set if there’s a **signed overflow**.
   - Example: Adding two positive numbers → negative result → OF = 1.

7. **Direction Flag (DF)**:
   - Controls string processing direction:
     - DF = 0 → Process strings **forward**.
     - DF = 1 → Process strings **backward**.

8. **Interrupt Enable Flag (IF)**:
   - Controls hardware interrupts:
     - IF = 1 → Interrupts are **enabled**.
     - IF = 0 → Interrupts are **disabled**.


#### **Why Are Flags Important?**
- Flags are used in **conditional jumps** to control program flow.
  - Example: Jump to a new instruction only if ZF = 1 (result is zero).
- They’re essential for implementing **logic and branching** in programs.


### **Remembering Tips**
Think of flags as **traffic signals** for the CPU:
- **CF**: "Did we overflow?" (Red light if yes).
- **ZF**: "Is the result zero?" (Green light if yes).
- **SF**: "Is the result negative?" (Yellow light if yes).
- **OF**: "Did something go wrong with signed math?" (Flashing red if yes).

---
---



### **Arithmetic and Logical Instructions**


#### **1. Arithmetic Instructions**
- Perform basic math operations like addition, subtraction, multiplication, and division.

**Addition (`add`)**:
- Syntax: `add destination, value`
- Adds `value` to `destination` and stores the result in `destination`.

**Subtraction (`sub`)**:
- Syntax: `sub destination, value`
- Subtracts `value` from `destination` and stores the result in `destination`.
  - **Flags**: 
    - ZF = 1 if the result is zero.
    - CF = 1 if `destination` is smaller than `value`.

**Multiplication (`mul`)**:
- Syntax: `mul value`
- Multiplies `eax` by `value` and stores the result in `edx:eax` (64-bit).
  - Lower 32 bits → `eax`, Higher 32 bits → `edx`.

**Division (`div`)**:
- Syntax: `div value`
- Divides the 64-bit value in `edx:eax` by `value`.
  - Quotient → `eax`, Remainder → `edx`.

**Increment (`inc`) and Decrement (`dec`)**:
- Increment: `inc register` → Adds 1 to the register.
- Decrement: `dec register` → Subtracts 1 from the register.


#### **2. Logical Instructions**
- Perform bitwise operations on binary data.

**AND (`and`)**:
- Syntax: `and destination, value`
- Performs a bitwise AND operation.
  - Example: `and al, 0x7c` → Keeps only matching bits.

**OR (`or`)**:
- Syntax: `or destination, value`
- Performs a bitwise OR operation.
  - Example: `or al, 0x7c` → Combines bits; sets bit to 1 if either operand has 1.

**NOT (`not`)**:
- Syntax: `not destination`
- Inverts all bits (1 → 0, 0 → 1).

**XOR (`xor`)**:
- Syntax: `xor destination, value`
- Performs a bitwise XOR operation.
  - Example: `xor al, 0x7c` → Sets bit to 1 if bits are different, 0 if same.
  - **Special Use**: `xor eax, eax` → Clears `eax` (sets it to 0).


### **Why Are These Important?**
- Arithmetic instructions handle calculations.
- Logical instructions manipulate binary data for tasks like masking, clearing, or comparing bits.
- **XOR Trick**: Often used to clear registers efficiently (e.g., `xor eax, eax`).


### **Remembering Tips**
Think of these instructions as tools in a toolbox:
- **Add/Sub**: Like adding or removing items from a pile.
- **Mul/Div**: For scaling or splitting values.
- **AND/OR/NOT/XOR**: Like filters or switches for bits:
  - **AND**: "Keep only what matches."
  - **OR**: "Combine everything."
  - **NOT**: "Flip everything."
  - **XOR**: "Find differences."


---
---



