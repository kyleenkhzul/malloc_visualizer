# Malloc Visualizer

A **web-based visualizer for dynamic memory allocation** in C-style heaps. This interactive tool demonstrates how `malloc`, `free`, and `realloc` work, including allocation, splitting, coalescing, and alignment.

---

## 🔹 Demo

Hover over blocks to view metadata and payload information. Click on a block to select its payload pointer for freeing or reallocating.  

**Animation Speed:** Adjustable via the slider to control visualization speed.

---

## ⚙️ Key Features

- **Dynamic Allocation:** `malloc` allocates memory blocks with first-fit strategy.
- **Freeing & Reallocation:** `free` and `realloc` work on the visible payload pointer.
- **Alignment:** All allocations are aligned to 16 bytes for proper memory alignment.
- **Metadata:** Each block contains 16 bytes of metadata (shown for educational purposes) and is tracked with boundary tags.
- **Doubly Linked List:** Blocks are stored in a doubly linked list to facilitate coalescing and splitting.
- **Explicit Free List:** Free blocks are tracked in a separate list for efficient allocation.
- **Animations:** Animated allocation, split, and coalescing to visually demonstrate memory operations.
- **Interactive:** Hover for details, click to select payload pointers.

---

## 📝 Assumptions

1. **16-byte alignment** for all allocations.
2. **Metadata is 16 bytes** per block.
3. **First-fit allocation** strategy.
4. **Blocks are doubly linked** with boundary tags.
5. **Explicit free list** is used for free blocks.
6. **Most recently freed block** is the head of the free linked list.
7. **Splitting and coalescing** are visualized.

---

## 🎮 How to Use

1. Enter the **allocation size** and click **malloc**.
2. Hover over blocks to see:
   - Metadata pointer
   - Payload pointer
   - Total block size
3. Click a block to select its **payload pointer**.
4. Enter the pointer in the input field to:
   - `free` a block
   - `realloc` a block to a new size
5. Use the **animation speed slider** to adjust visualization speed (in milliseconds per step). Higher value = slower animations.
6. Invalid operations (double free, negative sizes, invalid pointers) trigger error messages via toast notifications.
7. Alignment adjustments show info to indicate requested vs aligned size.

---

## ⚡ Implementation Details

- **Heap Representation:** A single linked list of `Block` objects with `prev_phys` and `next_phys` pointers.
- **Free List:** Blocks marked as free are maintained in a separate explicit free list (`prev_free`, `next_free`).
- **Allocation:** 
  - If a free block fits, it is reused and split if large enough.
  - Otherwise, the heap grows by creating a new block.
- **Deallocation:** 
  - Frees the block and coalesces adjacent free blocks.
- **Reallocation:**
  - Shrinks blocks in place when possible.
  - Expands into neighboring right free block if available.
  - Otherwise, allocates a new block and frees the old one.
- **User Interaction:** 
  - Only the payload pointer is used for `free` and `realloc`.
  - Metadata pointer is internal, only being shown in the free list and when hovering on the blocks for educational purposes.

---

## 🎨 UI Highlights

- **Color Coding:**
  - Allocated: Blue
  - Free: Red
  - Split Highlight: Cyan
  - Coalesce Highlight: Green
  - Search/Allocation: Yellow/Orange
- **Tooltips:** Show block metadata and size.
- **Animations:** Smooth transitions for allocation, splitting, and coalescing.

---

## 🛠️ Technologies

- **HTML/CSS/JS** — fully client-side, no server required.
- **Vanilla JavaScript** — handles all heap operations and animations.
- **CSS Animations** — highlight memory operations.

---

## 🧩 Potential Extensions

- Visualize different allocation strategies (best-fit, next-fit).
- Customize alignment.
- Show memory fragmentation statistics.
- Export heap state as JSON for testing.

---

## 📚 Credits

Created by **Artem Khaiet, Jimmy Hackney, and Kyle Enkhzul** as an interactive teaching tool for understanding dynamic memory allocation.