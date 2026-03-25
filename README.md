# Scrabble (macOS)

A personal Scrabble app for Mac, built with SwiftUI and the [Quackle](https://github.com/quackle/quackle) C++ engine. Identical gameplay and UI to the [iOS version](https://github.com/fitelson/quackle-ios).

## Features

- **Click-to-place** tile interaction — no text input
- **Real-time validation** — green tiles for valid moves, red for invalid
- **AI opponent** using Quackle's NormalPlayer with Gaussian move selection
- **Skill slider** — adjust AI difficulty from easy (0.0) to near-perfect (1.0)
- **Blank tile picker** — click a blank, choose a letter from an A–Z grid
- **Exchange, pass, and new game** support
- **Move history** and **top 50 candidate moves** views
- Uses the **TWL06** dictionary

## Requirements

- Xcode 16.3+
- macOS 14.0+
- [XcodeGen](https://github.com/yonaskolb/XcodeGen) (`brew install xcodegen`)
- The [quackle-ios](https://github.com/fitelson/quackle-ios) repo cloned as a sibling directory (for shared `libquackle` and `data` symlinks)

## Setup

Clone both repos side by side:

```bash
git clone https://github.com/fitelson/quackle-ios.git
git clone https://github.com/fitelson/quackle-macos.git
```

The `libquackle/` and `data/` symlinks point to `../quackle-ios/`, so both repos must be in the same parent directory.

## Build

```bash
xcodegen generate
xcodebuild -project QuackleScrabble.xcodeproj \
  -scheme QuackleScrabble \
  -configuration Release \
  build
```

> **Note:** Always use the `Release` configuration. Debug builds trigger a `strict_weak_ordering` assertion in Quackle's move comparator.

To install:

```bash
cp -R build/Build/Products/Release/Scrabble.app /Applications/
```

## Project Structure

```
QuackleScrabble/
  App/            — SwiftUI app entry point and main ContentView
  Bridge/         — Obj-C++ bridge (QuackleBridge) and QuackleEngine
  Model/          — GameState, TilePlacement, MoveHistoryEntry
  Views/
    Board/        — BoardView, SquareView
    Rack/         — RackView
    Game/         — ScoreboardView, MoveInputView
  Assets.xcassets — App icon
libquackle/       — symlink → ../quackle-ios/libquackle
data/             — symlink → ../quackle-ios/data
project.yml       — XcodeGen project spec
```

## Acknowledgments

This app uses the [Quackle](https://github.com/quackle/quackle) crossword game AI engine, created by **Jason Katz-Brown**, **John O'Laughlin**, and **John Fultz**. Quackle is released under the [GPL v2+](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

## Related

- [quackle-ios](https://github.com/fitelson/quackle-ios) — the iOS version of this app (and source of the shared C++ engine)
