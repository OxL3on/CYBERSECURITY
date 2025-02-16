# x86 Architecture Overview

### CPU Architecture 

1. **Von Neumann Architecture**:
   - CPU interacts with **Memory** and **I/O devices**.
   - CPU has three main components: **Control Unit**, **ALU**, and **Registers**.

2. **Control Unit (CU)**:
   - Fetches instructions from **Memory** using the **Instruction Pointer (IP)**.
     - *32-bit*: EIP, *64-bit*: RIP.

3. **Arithmetic Logic Unit (ALU)**:
   - Executes instructions fetched by the CU.
   - Stores results in **Registers** or **Memory**.

4. **Registers**:
   - Small, fast storage inside the CPU for quick access.

5. **Memory (RAM)**:
   - Holds program code and data.
   - Data is loaded into memory before execution.

6. **I/O Devices**:
   - Input/Output devices like keyboard, mouse, display, etc.

**Execution Flow**:
- Program → Loaded into Memory → CU fetches instructions → ALU executes → Results stored.


**Remembering Tip**:  
Think of the CPU as a chef:
- **CU**: Reads the recipe.
- **ALU**: Cooks the food.
- **Registers**: Prep table.
- **Memory**: Pantry.
- **I/O**: Tools and senses.

---
---



### Registers Overview

1. **Registers**:
   - Small, fast storage inside the CPU.
   - Limited size, so used efficiently.
   - Types: **Instruction Pointer**, **General-Purpose**, **Status Flag**, **Segment Registers**.

2. **Instruction Pointer (IP)**:
   - Holds the address of the next instruction to execute.
     - *32-bit*: EIP, *64-bit*: RIP.
   - Also called **Program Counter**.

3. **General-Purpose Registers**:
   - Used for general execution tasks.
   - Key registers:
     - **EAX/RAX**: Accumulator (arithmetic results).
     - **EBX/RBX**: Base (stores base address).
     - **ECX/RCX**: Counter (used in loops).
     - **EDX/RDX**: Data (multiplication/division).
     - **ESP/RSP**: Stack Pointer (points to top of stack).
     - **EBP/RBP**: Base Pointer (access stack parameters).
     - **ESI/RSI**: Source Index (string operations).
     - **EDI/RDI**: Destination Index (string operations).
     - **R8-R15**: New 64-bit registers (not in 32-bit systems).

4. **Addressing Modes**:
   - Registers can be accessed in different sizes:
     - Full size (e.g., RAX), lower 32-bit (e.g., EAX), 16-bit (e.g., AX), or 8-bit (e.g., AL/AH).

**Remembering Tip**:
Think of registers as tiny "buckets" inside the CPU:
- **IP/EIP/RIP**: Points to the next step in your recipe.
- **EAX/RAX**: Holds math results (like a calculator).
- **ESP/RSP**: Tracks the stack (like a pile of plates).
- **R8-R15**: Extra buckets added in 64-bit systems.

--- 
---



