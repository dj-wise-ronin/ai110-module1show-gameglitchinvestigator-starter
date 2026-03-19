# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

This project started with an AI-generated guessing game that was fundamentally broken. The hints were backward, the difficulty levels were inconsistent, and the scoring system was unfair. Through careful investigation and AI-assisted debugging, these issues have been resolved.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt` (Note: `streamlit` and `pytest` are required).
2. Run the fixed app: `python3 -m streamlit run app.py`

## 🕵️‍♂️ My Mission

The goal was to transform a "glitchy" prototype into a production-ready application by:
1.  **Identifying Bugs:** Backward hints, incorrect difficulty ranges, and scoring glitches.
2.  **Refactoring:** Moving core game logic from the UI (`app.py`) to a dedicated utility file (`logic_utils.py`).
3.  **Automated Testing:** Writing and passing unit tests to ensure logical correctness.
4.  **State Management:** Properly using Streamlit's session state to maintain game progress.

## 📝 Document Your Experience

- **Game Purpose:** A number guessing game where players try to find a secret number within a limited number of attempts, with hints and scoring based on their performance.
- **Bugs Found:**
    - **Backward Hints:** The game told players to go higher when they were already too high.
    - **Difficulty Mismatch:** "Hard" mode was actually 1-50, making it easier than "Normal" (1-100).
    - **Scoring Glitches:** Players could gain points for incorrect guesses if their attempt number was even.
    - **Type Confusion:** The secret number was occasionally compared as a string, leading to lexicographical errors (e.g., "10" < "2").
- **Fixes Applied:**
    - Refactored all game logic into `logic_utils.py`.
    - Corrected the comparison logic and hint messages in `check_guess`.
    - Adjusted `get_range_for_difficulty` so "Hard" mode is 1-200.
    - Standardized `update_score` to deduct points for incorrect guesses.
    - Ensured the secret number is always handled as an integer during comparisons.

## 📸 Demo

- **Test Results:** All 6 unit tests passed successfully.
- **Winning Game:** The game now provides accurate "Go HIGHER/LOWER" hints and correctly tracks scores and attempts.

## 🚀 Stretch Features

- [x] **Refactored Logic:** Successfully separated UI and business logic.
- [x] **Automated Tests:** Added 6 robust test cases in `tests/test_game_logic.py`.
- [x] **Type Safety:** Resolved the string/integer comparison bug.
