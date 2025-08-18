

🎯 Core Features Implemented:

  1. Game Management
    - Create games with 10x10 board
    - Join games (2 players max)
    - Start/finish game logic
    - Turn-based gameplay with 3-second timer
  2. Player System
    - Player objects with position, score, and name
    - Starting positions at opposite corners (0,0) and (9,9)
    - Movement in 4 directions (up, down, left, right)
    - Score tracking
  3. Sui Tiles
    - 10 randomly placed tiles on board
    - Tile capture mechanics
    - Ownership tracking
    - Value system (1 point per tile)
  4. Game Logic
    - Turn management and switching
    - Boundary validation
    - Win condition (all tiles captured)
    - Timer enforcement

  🧪 Testing Complete:

  ✅ 8 tests passing:
  - Game creation
  - Player joining
  - Game starting
  - Player movement
  - Coordinate helpers
  - Plus original example tests

  📁 Files Created:

  - sources/tile_game.move - Main contract (424 lines)
  - tests/tile_game_tests.move - Comprehensive tests (202 lines)

  🔧 Key Functions:

  - create_game() - Initialize new game
  - join_game() - Add players
  - start_game() - Begin gameplay and create tiles
  - move_player() - Handle player movement
  - capture_tile() - Tile collection mechanics