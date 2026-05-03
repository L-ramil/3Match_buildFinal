# Match-3 Evolution: Strategic Turn-Based Puzzle

> "A turn-cost Match-3 puzzle where strategy overcomes chance."
> 
> Going beyond luck-dependent traditional Match-3 games, this is a strategic puzzle game where player choices determine success.

---

## Project Overview
- **Development Period**: 2026.04.08 - 2026.04.26
- **Environment**: Unity 2022.3.x, C#
- **Platform**: PC
- **Role**: Solo Developer (Game Design, Logic Architecture, UI/UX, Sound Direction)

---

## Key Features

### 1. Strategic Shuffle System (Turn-Cost Shuffle)
Instead of an automatic shuffle when no moves are available, players can sacrifice one precious turn to shuffle the board themselves. This introduces a high-risk, high-return strategic choice to resource management.

### 2. Intelligent Hint System (Retention Hint)
Detects player inactivity for 15 seconds. A coroutine-based timer triggers a subtle 'Wiggle' animation on a matchable block, preventing player drop-off and maintaining game pacing without interrupting the main thread.

### 3. Advanced Cascade Logic (Recursive Matching)
Utilizes a recursive algorithm to flawlessly handle N-th degree chain reactions (cascades) after blocks fall, ensuring logical integrity until the board completely stabilizes.

---

## Tech Stack & Architecture

### 1. Data Structure Optimization
Selected 5 core data structures based on performance and purpose:
| Data Structure | Application | Reason for Selection |
| :--- | :--- | :--- |
| **Array [,]** | Puzzle Board Grid | O(1) access time for immediate swapping using fixed X, Y coordinates. |
| **List &lt;T&gt;** | Real-time Match Validation | Manages dynamic data sets where the number of matched blocks changes constantly. |
| **Queue &lt;T&gt;** | Block Spawn Sequence | Controls the logical falling sequence using a FIFO (First-In, First-Out) structure. |
| **Stack &lt;T&gt;** | Shop Undo System | Implements a flawless purchase rollback feature leveraging LIFO (Last-In, First-Out) characteristics. |
| **Dictionary** | Item Inventory | Provides immediate quantity lookups and updates via item IDs. |

### 2. Role-Based Architecture (Modular Design)
- **Singleton Pattern**: Centralized core managers (GameManager, UIManager) to ensure data consistency across scenes.
- **Data-View Separation**: Strictly separated the logic (Model) from visual representation (View) to minimize dependencies between score calculations and UI animations.

---

## Troubleshooting

### 1. Resolving Board Data Null Exceptions During Cascades
- **Issue**: During chain reactions, the grid array occasionally evaluated to `null`, causing the game to freeze before new blocks could spawn.
- **Solution**: Identified a race condition where block destruction, gravity fall, and spawning logic executed simultaneously. Refactored the code using Coroutines to separate these actions into strict, sequential phases, permanently fixing the synchronization issue.

### 2. Ensuring Data Integrity in Multi-Currency Refunds
- **Issue**: Using the "Undo" feature in the shop refunded Gold but failed to restore the "Play Count" secondary currency required for limited-edition items.
- **Solution**: Implemented an Enum ID check when popping items from the Stack. Successfully rolled back both the primary currency (Gold) and the secondary currency (Play Count) simultaneously, securing complete data integrity.

---

## Future Roadmap
- [ ] **Interface Integration**: Implement OCP (Open-Closed Principle) by using interfaces (e.g., `IExplodable`) to easily add special blocks like bombs and rainbows.
- [ ] **ScriptableObjects**: Decouple hardcoded item data into external assets to maximize balancing efficiency.
- [ ] **VFX Polish**: Enhance chain-reaction visual feedback using Unity's Particle System.

---
