# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [ ] Describe the game's purpose.
- [ ] Detail which bugs you found.
- [ ] Explain what fixes you applied.

## 📸 Demo

- [ ] [Insert a screenshot of your fixed, winning game here]

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, insert a screenshot of your Enhanced Game UI here] 


TF Notes:
The biggest thing students need to walk away understanding is that working code and correct code are not the same thing — this game runs fine, it just lies to you the entire time. The trickiest bug to catch is the string comparison one, where the secret gets converted to a string on even attempts and Python starts sorting alphabetically instead of numerically, so "9" beats "10" and everything breaks in a way that's really hard to spot just by reading. AI was actually pretty useful here for the obvious stuff — it flagged the inverted hints and the hardcoded UI text without much prompting — but it got it wrong on the scoring fix, suggesting we flip the sign on the even-attempt condition instead of just deleting it, which would've kept the scoring weird in a different way. That's a good moment to point students to when they ask why they can't just trust whatever Copilot spits out. If a student is stuck and frustrated, my go-to is to ask them what check_guess actually returns when guess is 60 and secret is 50 — just tracing through one real example by hand usually gets them there without me having to spell it out.
