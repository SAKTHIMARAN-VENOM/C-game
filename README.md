#  Space Shooter — Week 1
### Topics: SFML Setup · Game Loop · Player Class · Movement · Delta Time

---

This is the **foundation** of the Space Shooter game. No bullets or enemies yet — just the core architecture every game needs before anything else can be added.

| Feature | Status |
|---------|--------|
| SFML window (800×600) | ✅ Done |
| Clean game loop | ✅ Done |
| Delta time (frame-rate independent movement) | ✅ Done |
| Player class with spaceship shape | ✅ Done |
| Left / Right arrow key movement | ✅ Done |
| Screen boundary clamping | ✅ Done |
| Scrolling star background | ✅ Done |
| Live FPS counter | ✅ Done |

---

##  File Structure

```
Week1/
├── main.cpp       ← Full source code
└── README.md      ← This file
```

> After compiling, place `arial.ttf` in the same folder as the executable for text to display correctly.

---

##  How to Compile

### Linux / macOS
```bash
# Install SFML (Ubuntu/Debian)
sudo apt-get install libsfml-dev

# Install SFML (macOS)
brew install sfml

# Compile
g++ main.cpp -o SpaceShooter -lsfml-graphics -lsfml-window -lsfml-system -std=c++17

# Run
./SpaceShooter
```

### Windows (MinGW)
```bash
g++ main.cpp -o SpaceShooter.exe -IC:\SFML\include -LC:\SFML\lib ^
    -lsfml-graphics -lsfml-window -lsfml-system -std=c++17
```

### Windows (Visual Studio)
1. Create an Empty C++ Project
2. Add `main.cpp` to Source Files
3. Project → Properties → C/C++ → Additional Include Dirs → `C:\SFML\include`
4. Project → Properties → Linker → Input → Additional Dependencies:
   - `sfml-graphics.lib;sfml-window.lib;sfml-system.lib`
5. Copy all `.dll` files from `C:\SFML\bin` next to the `.exe`

---

##  Controls

| Key | Action |
|-----|--------|
| ← Left Arrow | Move player left |
| → Right Arrow | Move player right |
| ESC | Quit game |

---


##  Code Walkthrough

```
main()
  └── Game game;          creates window, player, stars
      └── game.run()
            └── while(window.isOpen())
                  ├── dt = clock.restart().asSeconds()   ← measure frame time
                  ├── processEvents()                    ← check ESC / close
                  ├── update(dt)                         ← move stars + player
                  └── render()                           ← draw everything
```

---



---

##  Notes

- The `struct Star` is defined inside the `Game` class — it is only used by the Game so it makes sense to keep it local.
- `ConvexShape` is used for the player hull because it allows any convex polygon, not just rectangles or circles.
- `setFramerateLimit(60)` caps the loop to 60 FPS so the CPU isn't running at 100% unnecessarily.
