# Metro Automation System Using PLC Ladder Logic

## Theory of Operation

This project demonstrates a simplified metro train automation system implemented using PLC Ladder Logic. The objective is to simulate the movement of a train through three sequential track blocks while maintaining safe separation between trains using the block occupancy principle.

In railway signaling, a track is divided into sections called **blocks**. Only one train is permitted within a block at any given time. A block occupied by a train is considered unsafe for another train to enter. This fundamental concept prevents collisions and forms the basis of modern railway signaling systems.

The program implements a sequential state machine using internal memory bits. A departure command initiates the train movement, after which the train progresses automatically through Block 1, Block 2, and Block 3. Timers are used to represent the train's travel time within each block.

As the train enters a block, the corresponding signal changes to **RED**, indicating that the block is occupied. Once the timer expires, the train transitions to the next block, releasing the previous block and updating the signals accordingly.

### Sequence of Operation

1. A pulse on `Dept_Signal` starts the journey.
2. The train enters **Block 1** and occupies it for 3 seconds.
3. After `Timer_1` completes, the train moves to **Block 2**.
4. After `Timer_2` completes, the train moves to **Block 3**.
5. After `Timer_3` completes, the train exits the system.
6. All states are reset, making the system ready for the next departure.

### Concepts Demonstrated

* PLC State Machine Design
* Timer-Based Sequencing
* Railway Block Signaling Concepts
* Occupancy Detection Logic
* Latch and Unlatch Operations
* Safe Train Movement Simulation

---

## Nomenclature

### Inputs

| Tag           | Description                                        |
| ------------- | -------------------------------------------------- |
| `Dept_Signal` | Departure command used to start the train sequence |

### Internal Memory

| Tag          | Description             |
| ------------ | ----------------------- |
| `Memory_1.0` | Train Occupying Block 1 |
| `Memory_1.1` | Train Occupying Block 2 |
| `Memory_1.2` | Train Occupying Block 3 |

### Timers

| Tag       | Description                       |
| --------- | --------------------------------- |
| `Timer_1` | Travel time through Block 1 (3 s) |
| `Timer_2` | Travel time through Block 2 (3 s) |
| `Timer_3` | Travel time through Block 3 (3 s) |

### Outputs

| Tag            | Description               |
| -------------- | ------------------------- |
| `Signal_BLK_1` | Signal status for Block 1 |
| `Signal_BLK_2` | Signal status for Block 2 |
| `Signal_BLK_3` | Signal status for Block 3 |

### Signal Convention

| Signal Value | Meaning                        |
| ------------ | ------------------------------ |
| `1`          | 🔴 RED Signal (Block Occupied) |
| `0`          | 🟢 GREEN Signal (Block Clear)  |

### Block Occupancy Convention

| Occupancy Status | Meaning                 |
| ---------------- | ----------------------- |
| `1`              | Block Occupied          |
| `0`              | Block Empty / Available |

---

## Simulation

To observe the sequence:

1. Click **Start** to run the simulation.
2. Open the **I/O Panel** from the left tab of the right sidebar.
3. Toggle **Dept_Signal**.
4. Observe the timers, block occupancy states, and signal transitions as the train progresses through the three blocks.
5. After Block 3 is completed, the system automatically resets and waits for the next departure command.

