# 🎮 C++ Raylib Retro Games (Pong & Tetris)

![C++](https://img.shields.io/badge/C%2B%2B-17-blue.svg) ![Raylib](https://img.shields.io/badge/Raylib-5.0-red.svg) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

Două jocuri complete construite cu **Raylib** și tehnici **C++ Modern**. Acest proiect demonstrează folosirea programării orientate pe obiecte (OOP), a șabloanelor (templates) și a bibliotecii standard C++ (STL) în dezvoltarea jocurilor 2D.

## 📂 Structura proiectului

```text
.
├── IGameObject.hpp   # Interfață abstractă + GameObjectManager<T> template
├── Ball.hpp          # Mingea Pong cu factory method
├── Paddle.hpp        # Paddle (jucător) + CpuPaddle (AI) — moștenire & polimorfism
├── Tetris.hpp        # Tetromino + TetrisGame — board STL, ghost piece, scoring
├── pong.cpp          # Entry point pentru Pong
├── tetris.cpp        # Entry point pentru Tetris
└── CMakeLists.txt    # Build system (C++17, FetchContent pentru Raylib)
```

## 🧠 Caracteristici C++ Modern folosite

| Concept | Utilizare în proiect |
|---|---|
| `std::unique_ptr` | Ownership exclusiv al *Ball, Paddle, CpuPaddle, Tetromino, TetrisGame* |
| `std::make_unique` | Factory methods: `Ball::Create`, `Paddle::Create`, `Tetromino::Spawn` |
| Template `GameObjectManager<T>` | Container generic pentru orice `IGameObject`; validat la compile-time cu `static_assert` |
| `std::vector<Vector2>` | Trail vizual al mingii (Pong) |
| `std::array<std::array<Color,COLS>,ROWS>` | Board Tetris fără alocare pe heap |
| Algoritmi STL | `std::all_of` pentru detectare linie completă în Tetris; `std::remove_if` pentru eliminarea obiectelor moarte |
| `std::map<PieceType,Color>` | Paleta de culori per tip de piesă |
| `virtual` + `override` | `IGameObject::Draw()`, `IGameObject::Update()` implementate în derivate |
| `constexpr` + `inline` | Constante de culoare și dimensiuni rezolvate la compilare |

## 🚀 Cum să rulezi jocurile (Build)

Asigură-te că ai **CMake** și un compilator C++ instalat. Raylib se va descărca și compila automat via `FetchContent`.

```bash
# 1. Generează fișierele de build
cmake -B build -S .

# 2. Compilează jocurile
cmake --build build

# 3. Rulează Pong
./build/pong

# 4. Rulează Tetris
./build/tetris
```

## ⌨️ Controale

🕹️ **Pong:**
* `↑` / `↓` — Mișcare paletă jucător (stânga)

🧩 **Tetris:**
* `←` `→` — Mișcare stânga/dreapta
* `↑` — Rotire piesă
* `↓` — Soft drop (coborâre rapidă)

## 📄 License

This project is released under the [MIT License](./LICENSE).
