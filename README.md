# Conveyor Builder

A factory conveyor-building game made with Unity. Place, rotate and connect conveyor pieces on the factory floor to carry a steady stream of boxes and cans to the end of the line — and use splits and filters to send different products down different routes.

## Gameplay

### Goal
The factory spawns two kinds of products at regular intervals: **cardboard boxes** and **cans**. Build a complete conveyor line that carries them all the way to the end to deliver them. The on-screen counter tracks how many products have been delivered.

### Controls

| Input | Action |
| --- | --- |
| `1` / `2` / `3` / `4` | Select a conveyor piece (straight, short, incline, etc.) — it follows the mouse |
| `R` | Rotate the piece 90° before placing |
| Left click | Place the piece |
| `Q` | Delete the placed conveyor under the mouse (when not holding a piece) |
| Speed slider | Adjust the speed of all conveyors |
| Pause / Resume button | Pause or resume the game |

### Rules
- **Auto-snap**: when you place a new piece with its start close to the end of an existing conveyor (within 1 unit by default), it automatically lines up and connects. Pieces that don't snap aren't part of the line.
- **Splits**: each conveyor can feed up to two downstream conveyors (A and B). Attach a second piece to the same exit to create a branch.
- **Filters**: a conveyor can be set to accept only boxes or only cans. At a split, a product takes route A if allowed, otherwise route B.
- **Delivery and rejection**:
  - A product that reaches the end of a conveyor with nothing connected after it is **delivered** and the counter goes up by one.
  - If there is a path ahead but no downstream conveyor accepts that product, it is **rejected** and removed.

## Getting Started

### Requirements
- **Unity 6000.6.0f1** (Unity 6). Install the same version through Unity Hub; opening the project in a different version may prompt an upgrade.
- Render pipeline: URP (Universal Render Pipeline), already included in the project's packages.

### Steps
1. Clone or download this repository:
   ```bash
   git clone <repository-url>
   ```
   > The model files are large (around 250 MB per FBX), so the download may take a while.
2. Open **Unity Hub** → **Add** → **Add project from disk**, and select the project root (the folder containing `Assets`, `Packages` and `ProjectSettings`).
3. Open the project with Unity 6000.6.0f1. The first launch imports all assets and generates the `Library` folder, which takes a few minutes.
4. In the Project window, open `Assets/Scenes/SplitPath.unity` or `Assets/Scenes/Modular.unity`.
5. Press **▶ Play** at the top of the editor.

### Building a standalone game (optional)
Go to `File` → `Build Profiles`, make sure `SplitPath` is in the scene list (add `Modular` too if you like), choose a target platform (Windows / macOS) and click **Build**.

## Project Structure

```
Assets/
├── ConveyorBuilder/
│   ├── Scripts/        # Game logic
│   ├── Models/
│   │   ├── Conveyors/  # Conveyor models (generic, short, incline)
│   │   └── Products/   # Product models (cardboard box, can)
│   ├── Materials/      # Floor and other materials
│   └── Blender/        # Source model file
├── Scenes/             # SplitPath and Modular scenes
└── Settings/           # URP render settings
```

### Main Scripts

| Script | Description |
| --- | --- |
| `Conveyor.cs` | A conveyor: start/end points, speed, downstream A/B, product filters |
| `ConveyorPlacer.cs` | Selecting, moving, rotating, placing, snapping and deleting conveyors at runtime |
| `Product.cs` | Moves products along conveyors, picks a route at splits, delivers or rejects |
| `ProductSpawner.cs` | Spawns random products at a fixed interval |
| `SpeedSlider.cs` | Controls conveyor speed with a UI slider |
| `PauseController.cs` | Pause / resume |
| `DeliveryCounterUI.cs` | Shows the number of delivered products |
