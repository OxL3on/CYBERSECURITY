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


