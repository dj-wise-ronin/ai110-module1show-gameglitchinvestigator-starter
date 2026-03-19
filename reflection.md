# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

The game was full of strange behaviors and logical errors. At first glance, it looked like a simple guessing game, but as soon as I started playing, I noticed that the hints were completely backward. For example, if I guessed 50 and the secret was 20, the game told me to "Go HIGHER!" instead of lower.

Three concrete bugs I noticed:
- **Backward Hints:** The `check_guess` function in `app.py` has the logic for "Too High" and "Too Low" swapped. If `guess > secret`, it returns "Go HIGHER!", and if `guess < secret`, it returns "Go LOWER!", which is the opposite of what should happen.
- **Difficulty Range Glitch:** The `get_range_for_difficulty` function returns a range of 1 to 50 for "Hard" mode, but 1 to 100 for "Normal" mode. This means "Hard" mode is actually easier because the range of possible numbers is smaller.
- **Rewarding Wrong Guesses:** In the `update_score` function, players actually gain 5 points for a "Too High" outcome if the attempt number is even. This is a glitch because players should not be rewarded for guessing incorrectly.
- **Type Comparison Bug:** The code randomly converts the secret number to a string, which causes lexicographical comparison in `check_guess`. This makes the "Too High/Low" logic even more unpredictable because "10" is considered smaller than "2" when compared as strings.

---

## 2. How did you use AI as a teammate?

I used the Gemini CLI as my primary AI teammate for this project. One correct suggestion from the AI was to refactor the core game logic into a separate `logic_utils.py` file. This made the code much cleaner and allowed me to write automated tests for the logic without worrying about the Streamlit UI. I verified this by moving the functions and ensuring that the app still functioned correctly through `app.py`.

An example of an incorrect/misleading suggestion was the original `check_guess` implementation, which included backward hints and a type-confusion bug. The AI-generated code was comparing an integer guess with a string secret, which resulted in lexicographical comparison (e.g., "10" < "2"). I verified this bug by adding a dedicated test case that used a string for the secret number and seeing the incorrect hint result.

---

## 3. Debugging and testing your fixes

I decided a bug was really fixed only after it passed an automated test and I manually verified the logic. I wrote several test cases in `tests/test_game_logic.py`, including one that specifically checked for the backward hints bug. For example, my `test_guess_too_high` test verified that a guess of 60 against a secret of 50 correctly returned the "Too High" outcome with a message to "Go LOWER!".

The AI helped me design these tests by providing the initial test function structure and suggesting different edge cases to check, like the type-safety test for string/integer comparisons. Running these tests confirmed that my fixes for the hints, difficulty ranges, and scoring were all successful.

---

## 4. What did you learn about Streamlit and state?

Streamlit "reruns" the entire script every time a user interacts with a widget, like typing a guess or clicking a button. Session state is like a "memory" for the app that persists across these reruns, allowing the game to keep track of the secret number and the number of attempts. Without session state, the app would "forget" everything every time you clicked a button.

---

## 5. Looking ahead: your developer habits

One habit I want to reuse is the "test-driven" approach of writing small, focused functions in a separate logic file and testing them immediately. This made it much easier to isolate and fix the bugs without getting distracted by the UI. I also found that marking "crime scenes" with FIXME comments was a great way to stay organized during a complex debugging session.

Next time, I would be more skeptical of AI-generated logic that involves type conversions, especially in languages like Python where dynamic typing can lead to subtle bugs. This project really highlighted how AI can generate code that "looks" right but is fundamentally broken under the surface, making it essential for a human to carefully review and test every line.
