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



### Registers 

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



### Registers - Continued


#### **Status Flag Registers**:
- **EFLAGS (32-bit)** / **RFLAGS (64-bit)**:
  - A single register with individual flags (1 or 0) to indicate the status of execution.
  - Key Flags:
    - **Zero Flag (ZF)**: Set to 1 if the result of an operation is zero.
    - **Carry Flag (CF)**: Set to 1 if the result is too big/small for the register.
    - **Sign Flag (SF)**: Set to 1 if the result is negative or the most significant bit is 1.
    - **Trap Flag (TF)**: Used for debugging; executes instructions one at a time.


#### **Segment Registers**:
- **16-bit registers** used to divide memory into segments for easier addressing.
- Key Segment Registers:
  - **CS (Code Segment)**: Points to the program's code section.
  - **DS (Data Segment)**: Points to the program's data section.
  - **SS (Stack Segment)**: Points to the program's stack.
  - **ES, FS, GS (Extra Segments)**: Point to additional data sections.


**Remembering Tip**:
- **Status Flags**: Think of them as traffic lights for CPU operations:
  - **ZF**: Green light if the result is zero.
  - **CF**: Red light if the result overflows.
  - **SF**: Yellow light if the result is negative.
  - **TF**: Debugging mode—like stepping through instructions frame by frame.
  
- **Segment Registers**: Imagine memory as a house:
  - **CS**: The living room (where the action happens).
  - **DS**: The kitchen (where data is stored).
  - **SS**: The closet (stack storage).
  - **ES/FS/GS**: Extra rooms for more data.

--- 
---



### Memory 

#### **Memory Layout**:
- Programs see an **abstracted view** of memory, divided into four main sections: **Code**, **Data**, **Heap**, and **Stack**.
- The order of sections can vary, but their roles remain the same.


#### **Sections in Memory**:

1. **Code**:
   - Contains the program's executable instructions.
   - Also called the **text section** in a Portable Executable (PE) file.
   - Has **execute permissions**—CPU can run instructions here.

2. **Data**:
   - Stores initialized, constant data like **global variables**.
   - Data here doesn’t change during execution.

3. **Heap**:
   - Used for **dynamic memory allocation**.
   - Variables are created and destroyed at runtime.
   - Example: Allocating memory for objects in programming languages like C or C++.

4. **Stack**:
   - Stores **local variables**, function arguments, and **return addresses**.
   - Critical for **control flow**—often targeted by malware (e.g., buffer overflows).

**Remembering Tip**:
Think of memory as a house:
- **Code**: The living room where all the action happens (instructions executed).
- **Data**: The pantry with pre-stocked items (constants/global variables).
- **Heap**: The garage where you store things temporarily (dynamic memory).
- **Stack**: The hallway where you keep track of your steps (local variables, return addresses).

---
---



### Stack Layout


#### **What is the Stack?**
- A **Last In, First Out (LIFO)** memory structure.
- Contains:
  - **Arguments**: Passed to functions.
  - **Local Variables**: Created during function execution.
  - **Return Address**: Where the program resumes after the function ends.
  - **Control Flow Data**: Critical for program execution.

#### **Key Components**:

1. **Stack Pointer (ESP/RSP)**:
   - Points to the **top of the stack**.
   - Moves as elements are pushed or popped.

2. **Base Pointer (EBP/RBP)**:
   - Acts as a **reference point** for local variables and arguments.
   - Remains constant during function execution.

3. **Old Base Pointer**:
   - Stored below the current Base Pointer.
   - Used to restore the caller's stack frame when the function exits.

4. **Return Address**:
   - Located below the Old Base Pointer.
   - Specifies where the program should return after the function finishes.
   - **Vulnerable to attacks** (e.g., Stack Buffer Overflow).

5. **Arguments**:
   - Pushed onto the stack before the function starts.
   - Located below the Return Address.


#### **Function Prologue and Epilogue**:

- **Prologue**:
  - Prepares the stack for function execution.
  - Pushes arguments, Return Address, and Old Base Pointer.
  - Updates the Base Pointer to the new stack frame.

- **Epilogue**:
  - Restores the stack to its original state.
  - Pops the Old Base Pointer and Return Address.
  - Adjusts the Stack Pointer.

#### **Why is the Stack Important?**
- Malware often exploits the stack to hijack control flow (e.g., **Stack Buffer Overflow**).
- Overwriting the **Return Address** can redirect execution to malicious code.


**Remembering Tip**:
Think of the stack as a stack of plates:
- **Push**: Add a plate (new data) to the top.
- **Pop**: Remove the top plate (last added data).
- **Base Pointer**: A marker to keep track of your plates.
- **Return Address**: A note under the plates telling you where to go next.

