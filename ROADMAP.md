**Timeline:** January 1, 2026 – June 30, 2026 (6 Months).
**Language Constraint:** **C Language Only**. (No C++, Python, or JS).
**Daily Commitment:** 90 Minutes (30 min Concept, 60 min Coding).

---

### **MONTH 1: POINTERS, ARRAYS & MEMORY (JANUARY)**

**Theme:** *"Memory is a Flat Line"***Semiconductor Context:**
In a high-level language (JS), memory is abstract. In Embedded Systems, memory is a physical row of capacitors (SRAM). A "Variable" is just a human name for a physical address (e.g., `0x20004000`).

- **Why Arrays?** Sensors (Camera, Audio, Accelerometer) dump data into linear buffers. You cannot "resize" a buffer in hardware without potentially crashing the system. You must work with fixed memory.
- **Why Pointers?** Passing a 1MB image buffer to a function by value creates a copy (wasting RAM). Passing it by pointer takes 4 bytes.

### **Week 1: The Physics of C (Pointers & Memory)**

- **The Logic:** Master `&` (Address of) and  (Value at). Understand that `arr[i]` is syntax sugar for `(arr + i)`.
- **Drill:** Write `swap(int *a, int *b)` and `strlen(char *s)` from scratch.
- **Must-Solve Problems:**
    1. **Concatenation of Array (LC 1929):** Understanding memory copying.
    2. **Shuffle the Array (LC 1470):** Index manipulation.
    3. **Fizz Buzz (LC 412):** Modulo arithmetic (used in timers).
    4. **Defanging an IP Address (LC 1108):** String/Memory replacement logic.
    5. **Score of a String (LC 3110):** Pointer traversal.
    6. **Permutation Difference between Two Strings (LC 3146).**
    7. **Find the Integer Added to Array (LC 3131).**
    8. **Convert the Temperature (LC 2469):** Floating point math.
    9. **LC 1929 (Concatenation):** Focus on manual `for` loops and pointer copying.
    10. **LC 1470 (Shuffle):** Teaches index mapping.
    11. **The Memory Alignment Drill.** Create a `struct` with `char`, `int`, `char`. Print its `sizeof`. It will be **12 bytes** (due to padding), not 6. Use `#pragma pack(1)` to force it to 6 and verify. (Proves knowledge of Data Bus Width and fetching efficiency).
    

### **Week 2: Prefix Sums (Time vs. Space)**

- **The Logic:** Pre-calculating a running total to answer range queries in $O(1)$ time.
- **Semiconductor Context:** **Telemetry & Battery.** If you need to calculate the total energy consumed between time $t=100ms$ and $t=500ms$, you don't iterate the loop every time. You look up the pre-calculated sums.
- **Must-Solve Problems:**
    1. **Running Sum of 1d Array (LC 1480):** The definition of Prefix Sum.
    2. **Find Pivot Index (LC 724):** Finding the "Center of Gravity" in a data stream.
    3. **Range Sum Query - Immutable (LC 303):** Fast lookups.
    4. **Product of Array Except Self (LC 238):** *Nvidia Classic.* (Hardware dividers are slow/expensive; do this using multiplication only).
    5. **Subarray Sum Equals K (LC 560):** identifying specific signal patterns.
    6. **Find the Highest Altitude (LC 1732).**
    7. **Contiguous Array (LC 525).**
    8. **Maximum Population Year (LC 1854).**
    9. **LC 303 (Range Sum):** Understand how pre-calculating saves battery/CPU cycles.
    10. **LC 238 (Product except Self):** High-end companies love this because hardware division is expensive.

### **Week 3: The Two-Pointer Technique (Static)**

- **The Logic:** Using `left` and `right` indices to scan a buffer from both ends or in tandem to solve problems in $O(n)$ instead of $O(n^2)$.
- **Semiconductor Context:** **Buffer Compaction.** You receive a packet with "dead" bytes (zeros) and need to remove them to save bandwidth *without* creating a new array (In-Place algorithm).
- **Must-Solve Problems:**
    1. **Remove Duplicates from Sorted Array (LC 26):** Data compression.
    2. **Remove Element (LC 27):** Filtering noise.
    3. **Move Zeroes (LC 283):** *Crucial.* Compacting a buffer.
    4. **Two Sum II (LC 167):** Input array is sorted (Binary Search logic).
    5. **Reverse String (LC 344):** Swapping memory bytes.
    6. **Squares of a Sorted Array (LC 977).**
    7. **Valid Palindrome (LC 125):** Checking data symmetry.
    8. **Sort Colors (LC 75):** The "Dutch National Flag" problem (Signal sorting).
    9. **LC 26 (Remove Duplicates):** Master the "Slow/Fast pointer" logic for buffer compaction.
    10. **LC 88 (Merge Sorted Array):** Learn to merge from the *back* to avoid overwriting data.

### **Week 4: 2D Arrays (Matrices)**

- **The Logic:** Mapping Row-Major `[i][j]` coordinates to linear memory addresses.
- **Semiconductor Context:** **Image Sensors & Displays.** A camera frame is a 2D matrix of pixels. Rotating a screen or processing a specific "Region of Interest" (ROI) requires matrix logic.
- **Must-Solve Problems:**
    1. **Rotate Image (LC 48):** In-place matrix rotation.
    2. **Spiral Matrix (LC 54):** Serializing 2D data for transmission.
    3. **Transpose Matrix (LC 867):** Axis swapping.
    4. **Reshape the Matrix (LC 566):** Memory re-mapping.
    5. **Set Matrix Zeroes (LC 73):** Masking rows/cols.
    6. **Search a 2D Matrix (LC 74):** Efficient lookup tables.
    7. **Matrix Diagonal Sum (LC 1572).**
    8. **Toeplitz Matrix (LC 766):** Verifying diagonal consistency. 
    9. Learn why iterating `row-major` is faster than `column-major`. Compare the execution time of a matrix sum when traversing rows vs. columns. This is "Senior Level" thinking.
    10. **LC 48 (Rotate Image):** Critical for display drivers.
    11. **LC 54 (Spiral Matrix):** Teaches you how to navigate a 2D memory-mapped sensor.
    12. Write two functions to sum a $1024 \times 1024$ int matrix. Function A: Loops Row then Col (Row-Major).Function B: Loops Col then Row (Column-Major).

---

### **MONTH 2: BIT MANIPULATION (FEBRUARY)**

**Theme:** *"The Register Interface"***Semiconductor Context:**
This is the **Highest ROI** month. In Embedded C, you control hardware by writing to **Registers**. A Register is a 32-bit integer.

- To turn on an LED, you set **Bit 5**.
- To check if a button is pressed, you read **Bit 3**.
- You must be surgically precise. Changing the wrong bit crashes the system.

### **Week 5: Basic Boolean Logic**

- **The Logic:** `&` (Clear/Check), `|` (Set), `^` (Toggle), `~` (Flip), `<<` (Shift).
- **Must-Solve Problems:**
    1. **Number of 1 Bits (LC 191):** *Hamming Weight.* Used for Parity Checks (Error detection).
    2. **Single Number (LC 136):** Using XOR to cancel out duplicates.
    3. **Missing Number (LC 268).**
    4. **Add Binary (LC 67):** Implementing a hardware adder in software.
    5. **Reverse Bits (LC 190):** Converting **Little Endian** to **Big Endian** (Network byte order).
    6. **Power of Two (LC 231):** Checking memory alignment (Must be 2, 4, 8...).
    7. **Hamming Distance (LC 461):** Comparing two binary signals.
    8. **Complement of Base 10 Integer (LC 1009).**
    9. **LC 190 (Reverse Bits):** Crucial for Big-Endian vs. Little-Endian data conversion.
    10. **LC 461 (Hamming Distance):** Used for error detection in data transmission.
    11. **The Endianness Converter.** Write `is_little_endian()`. Then, write a macro `SWAP_ENDIAN(x)` to flip a 32-bit integer (e.g., `0xAABBCCDD` $\to$ `0xDDCCBBAA`) using shifts. (Required for Network/Sensor data which is often Big Endian).

### **Week 6: Advanced Bit Hacks**

- **The Logic:** Using masks to pack/unpack data.
- **Semiconductor Context:** **Packet Headers.** A single 32-bit integer might store: [Version: 4 bits] [Length: 8 bits] [Type: 4 bits] [ID: 16 bits]. You need to extract these using shifts and masks.
- **Must-Solve Problems:**
    1. **Single Number II (LC 137).**
    2. **Single Number III (LC 260).**
    3. **Bitwise AND of Numbers Range (LC 201).**
    4. **Sum of Two Integers (LC 371):** Addition without `+` operator.
    5. **Counting Bits (LC 338):** DP + Bits.
    6. **Prime Number of Set Bits in Binary Representation (LC 762).**
    7. **Binary Number with Alternating Bits (LC 693).**
    8. **Number of Steps to Reduce a Number to Zero (LC 1342).** 
    9. **LC 137 (Single Number II):** Teaches you how to track state across 32 individual bits. 
    10. **LC 201 (Bitwise AND):** Understand the properties of bit-ranges in registers.

### **Week 7: Math & Number Theory**

- **The Logic:** Modulo arithmetic, GCD, Primes.
- **Semiconductor Context:** **Timers & Clocks.** If you have an 80MHz clock and need a 9600 baud rate, you need to calculate the divisor. **Cryptography** relies heavily on Primes and GCD.
- **Must-Solve Problems:**
    1. **Count Primes (LC 204):** Sieve of Eratosthenes.
    2. **Power of Three (LC 326).**
    3. **Excel Sheet Column Number (LC 171):** Base conversion.
    4. **Happy Number (LC 202).**
    5. **Plus One (LC 66):** Array math.
    6. **Palindrome Number (LC 9).**
    7. **Sqrt(x) (LC 69):** Hardware square root approximation.
    8. **Divide Two Integers (LC 29):** Implementing division using subtraction/shifts.
    9. **LC 29 (Divide Two Integers):** Implementing division using only shifts and subtraction (since hardware dividers are slow).
    10. **LC 69 (Sqrt):** Approximation algorithms used in signal processing.

### **Week 8: Review & Floating Point**

- **The Task:** Spend this week reviewing the hardest Bit Manipulation problems.
- **Project:** **Manual IEEE 754 Parser.** Write a C function that takes a `float` and prints its sign, exponent, and mantissa bits. **Constraint:** Do not just cast pointers. Use a `union` to overlay a `float` and `uint32_t`, then use bitmasks to extract the Sign (bit 31), Exponent (bits 30-23), and Mantissa (bits 22-0). This proves you understand how hardware stores decimals.

---

### **MONTH 3: DATA STREAMS & SLIDING WINDOWS (MARCH)**

**Theme:** *"The Continuous Stream"***Semiconductor Context:**
In MERN, you have a database with all the data. In Hardware, data arrives byte-by-byte via **UART** or **SPI**. You don't know the future; you only know the past and the current window.

### **Week 9: String Parsing (UART Context)**

- **The Logic:** Handling char arrays without standard libraries.
- **Semiconductor Context:** **AT Commands.** An ESP32 WiFi module sends `+WIFI:CONNECTED`. You need to parse this string to know the state.
- **Must-Solve Problems:**
    1. **Valid Anagram (LC 242).**
    2. **First Unique Character in a String (LC 387).**
    3. **Implement strStr() (LC 28):** Finding a substring (Command) in a buffer.
    4. **Longest Common Prefix (LC 14).**
    5. **Length of Last Word (LC 58).**
    6. **Is Subsequence (LC 392).**
    7. **Reverse Words in a String (LC 151).**
    8. **String to Integer (atoi) (LC 8):** Converting string "123" to int `123`.
    9. **LC 8 (myAtoi):** Essential for parsing data from a CLI or a sensor command.
    10. **LC 28 (Find Substring):** The "KMP" logic for finding commands in a UART stream.
    11. Task: The State Machine Parser. Instead of buffering a whole string, parse a stream of characters one by one. Trigger a "Command Found" state only when the exact sequence "\r\nOK\r\n" is detected. (Simulates reading a WiFi module response byte-by-byte).

### **Week 10: Fixed Sliding Window**

- **The Logic:** A window of size `k` moves across the array.
- **Semiconductor Context:** **Moving Average Filter.** To smooth out a noisy temperature sensor, you average the last 10 readings. As a new reading comes in, the oldest one drops out.
- **Must-Solve Problems:**
    1. **Maximum Average Subarray I (LC 643):** The literal definition of a Moving Average.
    2. **Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold (LC 1343).**
    3. **Permutation in String (LC 567).**
    4. **Find All Anagrams in a String (LC 438).**
    5. **Contains Duplicate II (LC 219).**
    6. **Diet Plan Performance (LC 1176).**
    7. **K Radius Subarray Averages (LC 2090).**
    8. **Sliding Window Maximum (LC 239):** (Hard - use Deque). Peak detection.
    9. **LC 643 (Moving Average):** The foundation of Digital Signal Processing (DSP).
    10. **LC 1456 (Vowels in Window):** Pattern detection in a fixed buffer.

### **Week 11: Dynamic Sliding Window**

- **The Logic:** The window expands and shrinks based on data validity.
- **Semiconductor Context:** **Debouncing.** A button press is noisy. You look for the longest continuous window of "High" signals to confirm a press.
- **Must-Solve Problems:**
    1. **Longest Substring Without Repeating Characters (LC 3).**
    2. **Max Consecutive Ones III (LC 1004):** Signal stabilizing.
    3. **Minimum Size Subarray Sum (LC 209).**
    4. **Longest Repeating Character Replacement (LC 424).**
    5. **Fruit Into Baskets (LC 904).**
    6. **Maximize the Confusion of an Exam (LC 2024).**
    7. **Binary Subarrays With Sum (LC 930).**
    8. **Count Complete Subarrays in an Array (LC 2799).**
    9. **LC 3 (Longest Substring):** Efficiently managing buffer boundaries.
    10. **LC 1004 (Max Consecutive Ones III):** Simulates "debouncing" a digital signal.

### **Week 12: Buffer Review**

- Re-solve the top 3 hardest Sliding Window problems. Ensure you handle "Corner Cases" (Empty array, Window size > Array size).
- Implement a "sliding window median" using two pointers.
- Challenge: Fixed-Point Arithmetic. Re-implement your Week 10 Moving Average filter without using float or double. Scale your inputs (e.g., multiply sensor values by 1000), perform the division, and manually place the decimal point when printing. (Crucial for FPU-less microcontrollers).

---

### **MONTH 4: LINKED LISTS & STACKS (APRIL)**

**Theme:** *"Dynamic Structures & The Kernel"***Semiconductor Context:**

- **Linked Lists:** This is how the **OS Kernel** (FreeRTOS/Linux) manages processes. The "Ready Queue" is a Linked List of tasks waiting to run.
- **Stacks:** The CPU Stack pointer (`SP`) moves down when you call a function. If you run out of stack, the system Hard Faults.

### **Week 13: Singly Linked Lists (Basics)**

- **The Logic:** Manipulating `next` pointers.
- **Must-Solve Problems:**
    1. **Reverse Linked List (LC 206):** *Memorize this.*
    2. **Middle of the Linked List (LC 876).**
    3. **Delete Node in a Linked List (LC 237).**
    4. **Merge Two Sorted Lists (LC 21):** Merging task lists.
    5. **Remove Duplicates from Sorted List (LC 83).**
    6. **Intersection of Two Linked Lists (LC 160).**
    7. **Palindrome Linked List (LC 234).**
    8. **Remove Linked List Elements (LC 203).**
    9. **LC 206 (Reverse List):** The most common pointer-interview question.
    10. **LC 141 (Cycle Detection):** Essential for detecting infinite loops in system tasks.
    

### **Week 14: Advanced Lists (Cycles & Doubly Linked)**

- **The Logic:** `prev` and `next` pointers. Cycle detection.
- **Semiconductor Context:** **Deadlock Detection.** If Task A waits for Task B, and Task B waits for Task A, you have a cycle (Deadlock). The "Tortoise and Hare" algorithm detects this.
- **Must-Solve Problems:**
    1. **Linked List Cycle (LC 141).**
    2. **Linked List Cycle II (LC 142).**
    3. **Remove Nth Node From End of List (LC 19).**
    4. **Rotate List (LC 61).**
    5. **Swap Nodes in Pairs (LC 24).**
    6. **Reorder List (LC 143).**
    7. **Add Two Numbers (LC 2):** Big integer math.
    8. **Copy List with Random Pointer (LC 138):** Deep copying structures.
    9. **LC 138 (Copy with Random Pointer):** Mimics "deep-copying" a memory-mapped structure.
    10. **LC 92 (Reverse II):** Partial memory reversal within a list.
    11. **Challenge:** **The "No-Malloc" Pool.** Implement a Linked List where you **pre-allocate** a global array of 100 Nodes. Write your own `alloc_node()` function that returns an unused index from this array. (Simulates Safety-Critical Static Memory logic used in Automotive).

### **Week 15: Stacks (LIFO)**

- **The Logic:** Last In, First Out.
- **Semiconductor Context:** **Nested Interrupts.** When an Interrupt fires, the CPU "pushes" the current context to the stack. When the ISR finishes, it "pops" it back.
- **Must-Solve Problems:**
    1. **Valid Parentheses (LC 20):** Parsing nested JSON or commands.
    2. **Min Stack (LC 155):** Custom Data Structure.
    3. **Implement Queue using Stacks (LC 232).**
    4. **Evaluate Reverse Polish Notation (LC 150):** How compilers calculate math.
    5. **Baseball Game (LC 682).**
    6. **Remove All Adjacent Duplicates In String (LC 1047).**
    7. **Make The String Great (LC 1544).**
    8. **Simplify Path (LC 71):** File system path navigation.
    9. **LC 155 (Min Stack):** Designing a "Hardware Monitor" that always knows the peak voltage.
    10. **LC 150 (Reverse Polish):** How the compiler evaluates math using the CPU stack.

### **Week 16: Monotonic Stacks**

- **The Logic:** Finding the "Next Greater Element."
- **Semiconductor Context:** **Telemetry Spikes.** Finding the next time the temperature exceeds the current value.
- **Must-Solve Problems:**
    1. **Next Greater Element I (LC 496).**
    2. **Daily Temperatures (LC 739).**
    3. **Online Stock Span (LC 901).**
    4. **Asteroid Collision (LC 735).**
    5. **Sum of Subarray Minimums (LC 907).**
    6. **Largest Rectangle in Histogram (LC 84)** *(Hard).*
    7. **LC 739 (Daily Temperatures):** Finding the "next peak" in a signal stream.
    8. **LC 84 (Largest Rectangle):** Advanced optimization of stack space.

---

### **MONTH 5: QUEUES, HEAPS & TREES (MAY)**

**Theme:** *"Buffering & Hierarchy"***Semiconductor Context:**

- **Circular Queues:** The **#1 Most Used** structure in firmware. It connects the hardware (UART) to the software.
- **Heaps:** The **RTOS Scheduler**. The task with the highest priority (Max Heap) runs next.

### **Week 17: Circular Queues (CRITICAL)**

- **The Logic:** A fixed array that wraps around using Modulo `%`.
- **Must-Solve Problems:**
    1. **Design Circular Queue (LC 622):** *Do this until you can write it in C without looking.*
    2. **Design Circular Deque (LC 641).**
    3. **Moving Average from Data Stream (LC 346).**
    4. **Implement Stack using Queues (LC 225).**
    5. **Number of Recent Calls (LC 933).**
    6. **Time Needed to Buy Tickets (LC 2073).**
    7. **First Unique Character in a String (LC 387).**
    8. **Dota2 Senate (LC 649).**
    9. **LC 622 (Design Queue):** **The #1 most important question.** Used in every UART/SPI driver.
    10. **LC 641 (Design Deque):** Handling bidirectional data from a network card.
    11. **Constraint:** **Atomic Correctness.** When implementing the Circular Queue, declare your `head` and `tail` indices as `volatile`. Explain to yourself why this prevents the compiler from caching the value, preventing bugs when an Interrupt modifies the queue.
    

### **Week 18: Heaps (Priority Queues)**

- **The Logic:** Accessing the Min or Max element in $O(1)$.
- **Semiconductor Context:** **Event Scheduling.** "Run Task A in 5ms, Task B in 2ms." A Min-Heap organizes these events by time.
- **Must-Solve Problems:**
    1. **Kth Largest Element in an Array (LC 215).**
    2. **Last Stone Weight (LC 1046).**
    3. **Top K Frequent Elements (LC 347).**
    4. **Sort Characters By Frequency (LC 451).**
    5. **K Closest Points to Origin (LC 973).**
    6. **Relative Ranks (LC 506).**
    7. **Task Scheduler (LC 621):** *Directly maps to RTOS logic.*
    8. **Find Median from Data Stream (LC 295).**
    9. **LC 621 (Task Scheduler):** Directly simulates how an RTOS (Real-Time OS) schedules tasks.
    10. **LC 215 (Kth Largest):** Finding the "worst-case" signal in a stream.

### **Week 19: Hash Maps & Sets**

- **The Logic:** $O(1)$ lookup using keys.
- **Semiconductor Context:** **Whitelisting.** Checking if a Bluetooth Device ID is allowed to connect.
- **Must-Solve Problems:**
    1. **Two Sum (LC 1).**
    2. **Contains Duplicate (LC 217).**
    3. **Majority Element (LC 169).**
    4. **Ransom Note (LC 383).**
    5. **Group Anagrams (LC 49).**
    6. **Longest Consecutive Sequence (LC 128).**
    7. **Word Pattern (LC 290).**
    8. **Design HashMap (LC 706).**
    9. **LC 146 (LRU Cache):** The "Gold Standard" for Cache Management interviews at Nvidia.
    10. **LC 706 (Design HashMap):** Understand collision handling in memory-constrained environments.

### **Week 20: Binary Trees (BFS/DFS)**

- **The Logic:** Hierarchical data nodes.
- **Semiconductor Context:** **Filesystems (FAT/LittleFS).** A folder contains files and other folders. This is a tree.
- **Must-Solve Problems:**
    1. **Maximum Depth of Binary Tree (LC 104).**
    2. **Invert Binary Tree (LC 226).**
    3. **Same Tree (LC 100).**
    4. **Symmetric Tree (LC 101).**
    5. **Binary Tree Level Order Traversal (LC 102).**
    6. **Path Sum (LC 112).**
    7. **Merge Two Binary Trees (LC 617).**
    8. **Lowest Common Ancestor (LC 236).**
    9. **LC 102 (Level Order):** Breadth-First Search (BFS) for system diagnostic checks.
    10. **LC 236 (Lowest Common Ancestor):** Root cause analysis in a hierarchical system.
    11. Sort an Array (LC 912) - MERGE SORT ONLY: Implement Merge Sort from scratch. The Drill: Calculate exactly how much Stack Memory your recursion uses for an array of 1,000,000 ints.

---

### **MONTH 6: GRAPHS, DP & THE FINAL EXAM (JUNE)**

**Theme:** *"Optimization & States"***Semiconductor Context:**

- **Graphs:** **State Machines (FSM).** A device moves from Init -> Idle -> Active -> Error. These states are nodes, and events are edges.
- **DP:** **Path Optimization.** Finding the most power-efficient route for a packet in a mesh network.

### **Week 21: Graphs (DFS/BFS)**

- **The Logic:** Visiting nodes in a network.
- **Must-Solve Problems:**
    1. **Number of Islands (LC 200):** Grouping pixels/sensors.
    2. **Flood Fill (LC 733).**
    3. **Find the Town Judge (LC 997).**
    4. **Find Center of Star Graph (LC 1791).**
    5. **Keys and Rooms (LC 841).**
    6. **Rotting Oranges (LC 994).**
    7. **Clone Graph (LC 133).**
    8. **Course Schedule (LC 207):** Cycle detection.
    9. **LC 207 (Course Schedule):** Cycle detection used to prevent **Deadlocks** in multi-core systems.
    10. **LC 133 (Clone Graph):** Replicating a system state in a different memory bank.
    11. **Project:** **Traffic Light Controller.** Implement an FSM with states (`RED`, `YEL`, `GRN`) and events (`TIMER`, `BTN`). Use a `switch-case` to handle transitions. (Demonstrates Event-Driven Architecture, which is 90% of firmware logic).

### **Week 22: Dynamic Programming (1D)**

- **The Logic:** Solving sub-problems once.
- **Must-Solve Problems:**
    1. **Climbing Stairs (LC 70).**
    2. **Min Cost Climbing Stairs (LC 746).**
    3. **House Robber (LC 198).**
    4. **Coin Change (LC 322).**
    5. **Maximum Subarray (LC 53):** Kadane's Algorithm.
    6. **Best Time to Buy and Sell Stock (LC 121).**
    7. **Pascal's Triangle (LC 118).**
    8. **Decode Ways (LC 91).**
    9. **LC 322 (Coin Change):** Optimizing the number of power-packets sent over a network.
    10. **LC 198 (House Robber):** Max-logic for resource gathering.

### **Week 23: Hard Problems (The Capstone)**

- **Goal:** Spend 2 hours per problem. Deep focus.
- **Problem List:**
    1. **Trapping Rain Water (LC 42).**
    2. **Merge k Sorted Lists (LC 23).**
    3. **Sliding Window Maximum (LC 239).**
    4. **Largest Rectangle in Histogram (LC 84).**
    5. **Serialize and Deserialize Binary Tree (LC 297).**
    6. **LC 42 (Trapping Rain Water):** Classic "Senior" logic test.
    7. **LC 208 (Trie):** Understand how to pack strings into a tree for fast network lookups.
    8. **LC 23 (Merge k Sorted Lists):** Merging multiple sensor streams into one timeline.

### **Week 24 & 25: Mock Interviews (Whiteboard Mode)**

- **The Rule:** No IDE. No Google. Paper and Pen only.
- **Simulate:** Pick a random medium question. Speak your logic out loud.
- **The Senior Constraint:** For every recursive solution, calculate the **Max Stack Depth**. (e.g., "This recursion goes $N$ deep. $1000 \text{ frames} \times 16 \text{ bytes} = 16\text{KB}$." -> "This would crash a microcontroller with 4KB Stack.").
- **Goal:** To be able to write valid C syntax on a whiteboard without a compiler's help.

### **Week 26: Rest & Setup**

- Prepare for **Phase 2 (Hardware)** starting July 1st. Ensure your Nucleo board is ready.