# x86 Architecture Overview

### CPU Architecture Overview

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



