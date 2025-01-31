# Solana Number Guessing Game Project

## Project Goals
- Create a simple, focused number guessing game on Solana
- Learn and evaluate Aider's architect capabilities
- Gain hands-on experience with core Solana development
- Keep scope minimal while demonstrating key concepts
- Document the learning process for both tools

## Learning Focus
### Aider Architect
- Explore AI-assisted project structuring
- Test collaborative development workflow
- Evaluate code generation and modification capabilities
- Document effective interaction patterns

### Solana Development
- Implement basic on-chain state management
- Handle program-derived addresses (PDAs)
- Manage secure random number generation
- Create simple client interactions

## Core Game Mechanics
1. Program generates random number using recent blockhash
2. Player gets limited attempts to guess correctly
3. Program provides higher/lower feedback
4. Win condition checked on each guess
5. Game state stored on-chain

## Program Structure

### State Management
```rust
pub struct GameAccount {
    pub player: Pubkey,           // Player's public key
    pub target_number: u8,        // Number to guess (1-100)
    pub attempts_remaining: u8,   // Remaining guess attempts
    pub max_attempts: u8,         // Maximum allowed attempts
    pub game_status: GameStatus,  // Current game state
    pub last_guess: Option<u8>    // Last guess made (for feedback)
}

pub enum GameStatus {
    Active,
    Won,
    Lost,
    Complete
}
```

### Instructions
1. initialize_game
   - Creates new game account (PDA)
   - Generates random target number
   - Sets initial state

2. make_guess
   - Validates player and game state
   - Processes guess and updates state
   - Provides feedback (higher/lower)
   - Checks win condition

3. close_game
   - Cleanup completed games
   - Return rent lamports

## Security Considerations
- Secure random number generation using recent blockhash
- Account validation and ownership checks
- Prevention of multiple active games per player
- Proper error handling for all state transitions
- Protection against common attack vectors:
  - Double transactions
  - State manipulation
  - Unauthorized access

## Implementation Plan
1. Core Program Structure
   - Account structures
   - Instruction handlers
   - State management

2. Game Logic
   - Random number generation
   - Guess processing
   - Win/lose conditions

3. Security Features
   - Account validation
   - Error handling
   - Edge case handling

4. Testing
   - Unit tests for logic
   - Integration tests
   - Security tests

5. Client Interface
   - Basic TypeScript client
   - Game interaction flow
   - Error handling

## Development Stack
- Rust for Solana program
- Anchor framework
- TypeScript for client
- Web3.js for blockchain interaction

## Project Structure
```
/solana-game-project
├── program/           
│   ├── src/
│   │   ├── lib.rs    # Main program logic
│   │   ├── state.rs  # Game state structures
│   │   └── error.rs  # Custom error types
├── tests/            # Program tests
└── client/           # TypeScript client
```

## Error Handling Strategy
- Custom error enum for all failure cases
- Comprehensive input validation
- Clear error messages
- Graceful failure handling

## Testing Strategy
1. Unit Tests
   - State transitions
   - Game logic
   - Input validation

2. Integration Tests
   - Full game flows
   - Error conditions
   - Edge cases

3. Security Tests
   - Account validation
   - Permission checks
   - State manipulation attempts

## Next Steps
1. Setup basic program structure
2. Implement core state management
3. Add game logic and instructions
4. Implement security features
5. Create test suite
6. Build client interface

## Resources Referenced
- Solana Program Examples (program-examples repo)
- Solana Cookbook
- Anchor Documentation
- Web3.js Documentation