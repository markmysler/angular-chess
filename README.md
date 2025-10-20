# ♟️ Angular Chess Game

A fully-featured chess game built with Angular 17, implementing complete chess rules, move validation, and an intuitive user interface.

![Angular](https://img.shields.io/badge/Angular-17.3.0-red?logo=angular)
![TypeScript](https://img.shields.io/badge/TypeScript-5.4.2-blue?logo=typescript)
![License](https://img.shields.io/badge/License-MIT-green)

## 📋 Table of Contents

- [Features](#-features)
- [Demo](#-demo)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [How to Play](#-how-to-play)
- [Project Structure](#-project-structure)
- [Technical Architecture](#-technical-architecture)
- [Game Logic](#-game-logic)
- [Components Overview](#-components-overview)
- [Development](#-development)
- [Build & Deployment](#-build--deployment)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)

---

## ✨ Features

### Core Chess Features
- ♟️ **Complete Chess Rules Implementation**
  - All piece movements (Pawn, Rook, Knight, Bishop, Queen, King)
  - Move validation and legal move highlighting
  - Check and checkmate detection
  - Stalemate detection

### Special Moves
- 🏰 **Castling** (both kingside and queenside)
- 🎯 **En Passant** capture
- 👑 **Pawn Promotion** with piece selection dialog
- 📝 **FEN (Forsyth-Edwards Notation)** support

### Game Rules & Endings
- ⚖️ **Draw Conditions**
  - Fifty-move rule
  - Threefold repetition
  - Insufficient material
- 🎮 **Turn-based gameplay** with player color switching
- 🔄 **Board flipping** for better viewing angles

### User Interface
- 🎨 **Visual feedback** for selected pieces and valid moves
- 🔴 **Check indication** with king highlighting
- 📱 **Responsive design** with clean, modern interface
- 🖱️ **Click-to-move** interaction system

---

## 🚀 Demo

To see the chess game in action:
1. Follow the [Installation & Setup](#-installation--setup) instructions
2. Navigate to `http://localhost:4200/` in your browser
3. Start playing immediately - White moves first!

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js** (version 18.x or higher)
- **npm** (comes with Node.js)
- **Angular CLI** (version 17.x)

```bash
# Check your versions
node --version
npm --version
ng version
```

### Installing Angular CLI (if not already installed)
```bash
npm install -g @angular/cli
```

---

## 🚀 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/markmysler/angular-chess.git
cd angular-chess
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Start Development Server
```bash
npm start
# or
ng serve
```

### 4. Open in Browser
Navigate to `http://localhost:4200/`

The application will automatically reload when you make changes to the source files.

---

## 🎮 How to Play

### Basic Controls
1. **Select a Piece**: Click on any piece of your color (White starts first)
2. **View Legal Moves**: Valid squares will be highlighted in green
3. **Make a Move**: Click on a highlighted square to move the piece
4. **Deselect**: Click the same piece again or click an empty square

### Special Actions
- **Castling**: Select your king and click on the castling square (2 squares away)
- **En Passant**: Available when an opponent's pawn moves two squares and can be captured
- **Pawn Promotion**: When a pawn reaches the opposite end, select the desired piece from the dialog
- **Flip Board**: Use the "Flip" button to rotate the board view

### Game States
- **Check**: Your king is highlighted in red when in check
- **Checkmate**: Game ends when a player has no legal moves while in check
- **Stalemate**: Game ends in a draw when a player has no legal moves but isn't in check
- **Draw**: Game can end in various draw conditions (50-move rule, repetition, insufficient material)

---

## 📁 Project Structure

```
src/
├── app/
│   ├── chess-logic/                 # Core chess game logic
│   │   ├── pieces/                  # Individual piece classes
│   │   │   ├── piece.ts            # Abstract base piece class
│   │   │   ├── king.ts             # King piece logic
│   │   │   ├── queen.ts            # Queen piece logic
│   │   │   ├── rook.ts             # Rook piece logic
│   │   │   ├── bishop.ts           # Bishop piece logic
│   │   │   ├── knight.ts           # Knight piece logic
│   │   │   └── pawn.ts             # Pawn piece logic
│   │   ├── chess-board.ts          # Main chess board logic
│   │   ├── FENConverter.ts         # FEN notation converter
│   │   └── models.ts               # Type definitions and enums
│   ├── modules/
│   │   └── chess-board/            # Chess board component
│   │       ├── chess-board.component.ts    # Board component logic
│   │       ├── chess-board.component.html  # Board template
│   │       ├── chess-board.component.scss  # Board styles
│   │       └── models.ts           # Component-specific models
│   ├── app.component.ts            # Root component
│   └── app.config.ts               # App configuration
├── assets/
│   └── pieces/                     # SVG piece images
│       ├── white king.svg
│       ├── black king.svg
│       └── ... (all piece variants)
└── styles.scss                    # Global styles
```

---

## 🏗️ Technical Architecture

### Technology Stack
- **Framework**: Angular 17.3.0 (Standalone Components)
- **Language**: TypeScript 5.4.2
- **Styling**: SCSS
- **Build Tool**: Angular CLI with Webpack
- **Testing**: Jasmine & Karma

### Key Design Patterns
- **Object-Oriented Programming**: Each piece type inherits from a base `Piece` class
- **State Management**: Game state managed within the `ChessBoard` class
- **Component Architecture**: Modular components with clear separation of concerns
- **Reactive Programming**: Uses RxJS for event handling (where applicable)

### Architecture Highlights
- **Standalone Components**: Leverages Angular 17's standalone component architecture
- **Type Safety**: Full TypeScript implementation with strict typing
- **Modular Design**: Clear separation between game logic and UI components
- **Performance Optimized**: Efficient change detection and rendering

---

## ♟️ Game Logic

### Core Systems

#### Move Validation
- **Legal Move Calculation**: Each piece calculates its valid moves based on current board state
- **Check Prevention**: Moves that would put the player's own king in check are filtered out
- **Special Move Handling**: Castling, en passant, and pawn promotion logic

#### Position Evaluation
```typescript
// Example: Checking if a square is safe after a move
private isPositionSafeAfterMove(prevX: number, prevY: number, newX: number, newY: number): boolean {
  // Simulates move and checks if king would be in check
}
```

#### Game State Management
- **Turn Management**: Alternates between White and Black players
- **Check Detection**: Continuously monitors for check conditions
- **Game Over Detection**: Handles checkmate, stalemate, and draw conditions

### FEN Notation Support
The game implements full FEN (Forsyth-Edwards Notation) support:
- **Board Representation**: Converts current position to FEN string
- **Game State Tracking**: Includes castling rights, en passant, move counters
- **Position Restoration**: Can recreate board state from FEN string

### Special Rules Implementation

<details>
<summary><strong>Castling Rules</strong></summary>

- King and rook must not have moved
- No pieces between king and rook
- King not in check
- King doesn't pass through or end up in check
- Supports both kingside (O-O) and queenside (O-O-O) castling

</details>

<details>
<summary><strong>En Passant Rules</strong></summary>

- Opponent's pawn must have just moved two squares
- Your pawn must be on the 5th rank (for White) or 4th rank (for Black)
- Capture is made diagonally to the square the opponent's pawn passed over

</details>

<details>
<summary><strong>Pawn Promotion</strong></summary>

- Triggered when pawn reaches the opposite end of the board
- Player can choose: Queen, Rook, Bishop, or Knight
- Immediate promotion with visual selection dialog

</details>

---

## 📦 Components Overview

### ChessBoardComponent
**Location**: `src/app/modules/chess-board/`

**Responsibilities**:
- Renders the 8x8 chess board grid
- Handles user interactions (piece selection, moves)
- Manages visual states (highlighting, check indication)
- Coordinates with ChessBoard logic class

**Key Features**:
- Click-to-move interaction
- Visual feedback for legal moves
- Pawn promotion dialog
- Board flipping functionality

### ChessBoard Class
**Location**: `src/app/chess-logic/`

**Responsibilities**:
- Core game logic and rule enforcement
- Move validation and generation
- Game state management
- FEN notation handling

**Key Methods**:
```typescript
public move(prevX: number, prevY: number, newX: number, newY: number, promotedPieceType: FENChar | null): void
public isInCheck(playerColor: Color, checkingCurrentPosition: boolean): boolean
private findSafeSqares(): SafeSquares
```

### Piece Classes
**Location**: `src/app/chess-logic/pieces/`

Each piece inherits from the abstract `Piece` class:

| Piece | Special Features |
|-------|-----------------|
| **King** | Castling, check detection |
| **Queen** | Combined rook and bishop movement |
| **Rook** | Castling participation, moved tracking |
| **Bishop** | Diagonal movement only |
| **Knight** | L-shaped moves, can jump over pieces |
| **Pawn** | Double move, en passant, promotion |

---

## 🛠️ Development

### Running Tests
```bash
# Run unit tests
npm test

# Run tests with coverage
ng test --code-coverage

# Run tests in headless mode
ng test --watch=false --browsers=ChromeHeadless
```

### Code Style & Linting
```bash
# Check for linting errors
ng lint

# Auto-fix linting issues
ng lint --fix
```

### Development Workflow
1. **Feature Development**: Create feature branches from `main`
2. **Code Standards**: Follow Angular style guide and TypeScript best practices
3. **Testing**: Write unit tests for new features
4. **Documentation**: Update README and code comments

### Available NPM Scripts
```bash
npm start          # Start development server
npm run build      # Build for production
npm run watch      # Build in watch mode
npm test           # Run unit tests
npm run lint       # Run linting (if configured)
```

### Debugging Tips
- Use browser developer tools for debugging
- Angular DevTools extension for component inspection
- Console logging available in development mode

---

## 🚀 Build & Deployment

### Production Build
```bash
# Build for production
npm run build

# Build output will be in dist/ directory
```

### Build Configuration
- **Output Directory**: `dist/chess-game/`
- **Bundle Optimization**: Enabled in production
- **Source Maps**: Available in development mode
- **Asset Optimization**: Images and styles are optimized

### Deployment Options

#### Static Hosting (Recommended)
Deploy the `dist/chess-game/` folder to any static hosting service:
- **Netlify**: Drag and drop the dist folder
- **Vercel**: Connect your GitHub repository
- **GitHub Pages**: Use GitHub Actions for automatic deployment
- **Firebase Hosting**: Use Firebase CLI

#### Example Netlify Deployment
```bash
# After building
npm run build

# Deploy to Netlify (install netlify-cli first)
npx netlify deploy --dir=dist/chess-game --prod
```

#### Example Firebase Deployment
```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login and initialize
firebase login
firebase init

# Deploy
firebase deploy
```

### Environment Configuration
The app uses Angular's environment system:
- `environment.ts` - Development configuration
- `environment.prod.ts` - Production configuration

---

## 🚧 Future Enhancements

### Planned Features
- [ ] **Multiplayer Support**
  - Real-time online gameplay
  - WebSocket integration
  - Player matchmaking

- [ ] **Game Analysis**
  - Move history with notation
  - Game replay functionality
  - Position analysis tools

- [ ] **AI Opponent**
  - Computer player with difficulty levels
  - Move suggestion system
  - Opening book integration

- [ ] **Enhanced UI/UX**
  - Drag and drop piece movement
  - Sound effects and animations
  - Customizable themes and board colors
  - Mobile-responsive design improvements

- [ ] **Advanced Features**
  - Time controls (blitz, rapid, classical)
  - Tournament mode
  - PGN (Portable Game Notation) export/import
  - Opening explorer

### Known Issues
- Board rotation animation could be smoother
- Mobile touch controls need optimization
- Performance optimization for move calculation in complex positions

### Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Credits & Acknowledgments

### Libraries & Dependencies
- **Angular** - The web framework used
- **TypeScript** - Programming language
- **RxJS** - Reactive programming library
- **Angular CLI** - Development tooling

### Resources
- Chess piece SVG icons from various open-source collections
- Chess rules implementation inspired by standard FIDE regulations
- FEN notation specification from chess programming community

### Inspiration
This project was built as a learning exercise to explore Angular's capabilities and implement complex game logic in TypeScript.

---

<div align="center">

**Built with ❤️ using Angular**

[⬆ Back to Top](#-angular-chess-game)

</div>
