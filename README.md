# Efficient Garbage Collection Simulator

A visual, interactive web-based simulator designed to demonstrate how different Garbage Collection (GC) algorithms manage memory in a heap. This tool helps in understanding the mechanics of memory allocation, object liveness, and reclamation strategies through real-time visualization.

## Features

- **Interactive Visualization**: Watch how memory blocks are allocated, marked, sweeped, and compacted in real-time on a visual heap canvas.
- **Multiple GC Algorithms**:
  - **Mark & Sweep**: Classic reachability analysis.
  - **Mark & Compact**: Addresses fragmentation by compacting live objects.
  - **Reference Counting**: Immediate reclamation with reference tracking (includes cycle handling simulation or issues).
  - **Generational GC**: Simulates young and old generation promotion for efficiency (Hypothesis/Tenuring).
- **Simulation Controls**:
  - **Start/Pause/Resume**: Control the flow of the simulation.
  - **Step-by-Step**: Execute the simulation one frame/tick at a time for detailed observation.
  - **Variable Speed**: Adjust the speed of the simulation ticks.
  - **Manual Allocation**: Manually allocate objects to stress the heap.
  - **Force GC**: Trigger a Garbage Collection cycle on demand.
- **Metrics Dashboard**: Real-time stats including:
  - GC Cycles count
  - Last Pause Time (ms)
  - Reclaimed Blocks
  - Heap Fragmentation %
- **Customizable Heap**: Configure the total heap size (blocks) to test different scenarios.
- **Color-Coded Legend**: unique colors for Free, Allocated, Garbage, Marked, and Old Gen blocks.

## Getting Started

### Prerequisites

This project is built using standard web technologies and requires a modern web browser (Chrome, Firefox, Edge, Safari) that supports **ES Modules**.

### Running the Simulator

1.  **Clone or Download** the repository to your local machine.
2.  **Open** the project folder.
3.  **Launch** `index.html` directly in your browser.
    *   *Note: Due to ES Module security policies in some browsers (CORS), checking functionality might require serving the file via a local server (like Live Server in VS Code, `python -m http.server`, or `npx serve`).*
    *   If simply opening `index.html` does not work, try:
        ```bash
        # Python 3
        python -m http.server 8000
        # Then open http://localhost:8000
        ```
        OR
        ```bash
        # Node.js
        npx serve .
        ```

## Supported Algorithms

1.  **Mark & Sweep**:
    *   **Phase 1 (Mark)**: Traverses the object graph from roots, marking reachable objects.
    *   **Phase 2 (Sweep)**: Scans the entire heap, reclaiming unmarked (unreachable) blocks.
    *   *Pros*: Simple loop detection. *Cons*: Fragmentation.

2.  **Mark & Compact**:
    *   Similar to Mark & Sweep but moves live objects to one end of the heap.
    *   *Pros*: Eliminates fragmentation. *Cons*: Expensive movement (updating pointers).

3.  **Reference Counting**:
    *   Each object tracks the number of incoming references.
    *   Objects are reclaimed immediately when the count drops to zero.
    *   *Pros*: Real-time reclamation. *Cons*: Cannot handle cyclic references (unless augmented).

4.  **Generational**:
    *   Divides the heap into "Nursery" (New) and "Old Gen".
    *   Objects start in Nursery; survivors of a GC cycle are promoted to Old Gen.
    *   Typically runs minor GCs on Nursery often, and major GCs less frequently.

## Project Structure

- **`index.html`**: The main entry point and UI layout.
- **`style.css`**: Application styling and themes.
- **`js/`**:
  - **`main.js`**: Application bootstrapping.
  - **`config.js`**: Global configuration constants.
  - **`engine/`**: Core simulation logic (Heap, MemoryObject, Simulator).
  - **`gc/`**: Implementation of GC algorithms (`MarkSweep.js`, `Generational.js`, etc.).
  - **`ui/`**: Canvas rendering (`Renderer.js`) and DOM event handling (`Controls.js`).

## Technologies

- **HTML5 Canvas**: For high-performance grid rendering.
- **Vanilla JavaScript**: (ES6+) No frameworks, purely native implementations.
- **CSS3**: Modern layout and styling.

## License

[MIT License](LICENSE) (Assuming MIT for this educational project, otherwise specify your own).

