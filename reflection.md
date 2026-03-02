# 💭 Reflection: Game Glitch Investigator

## 1. What was broken when you started?

When I first ran the game, it looked functional on the surface — there was a text input, a submit button, and a score counter — but it immediately felt off once I started playing. The biggest thing I noticed was that the hints were completely backwards. I'd guess a number that was too high and the game would tell me to go even higher, which made it basically impossible to win without cheating and looking at the debug panel. The second bug I caught pretty quickly was that the score would randomly go up even when I guessed wrong, which made no sense. It felt like the game was rewarding me for being wrong on certain attempts, which killed any sense of competition or fairness.

---

## 2. How did you use AI as a teammate?

I used Claude and GitHub Copilot throughout this project. For Claude, I checked in the app.py after I did a solo investigation and asked it to identify the bugs, which it did a solid job of — it correctly flagged the inverted hints in check_guess and explained that the messages "Go HIGHER" and "Go LOWER" were swapped, which I verified by manually tracing through the function with a guess of 60 and a secret of 50. One area where the AI was misleading was when I asked Copilot to refactor the scoring logic — it suggested keeping the even-attempt condition but just flipping the sign, which still would have made scoring inconsistent depending on what attempt number you were on. I caught that by running a quick manual test with a few wrong guesses in a row and noticing the score was still behaving unevenly, so I ended up removing that condition entirely instead.

---

## 3. Debugging and testing your fixes

My main way of deciding a bug was fixed was to test it in the live game first — I'd open the debug panel to see the secret number, then make a guess I knew was too high and check whether the hint matched. For more confidence, I wrote a pytest case for check_guess that passed in guess=60 and secret=50 and asserted the outcome came back as "Too High" with a "Go LOWER" message. That test failed before my fix and passed after, which gave me a clear signal the logic was actually corrected. Claude helped me think through the structure of the test — I described what I was trying to verify and it suggested using a straightforward assert statement rather than anything overly complex, which kept the test easy to read and understand.

---

## 4. What did you learn about Streamlit and state?

The secret number kept changing in the original app because Streamlit reruns the entire script from top to bottom every time a user interacts with anything — clicks a button, types in a box, anything. Without session state protecting the secret, it got regenerated with random.randint() on every single rerun. The way I'd explain it to a friend is: imagine every time you clicked a button on a website, the whole page reloaded from scratch and forgot everything it knew — that's Streamlit without session state. Session state is basically a way to say "remember this value even when the page reloads." The fix was wrapping the secret generation in an if "secret" not in st.session_state check, so it only generates once at the very start and stays locked in after that.

---

## 5. Looking ahead: your developer habits

One habit I want to carry forward is adding a comment right next to every bug fix explaining what was wrong and what I changed — I did this with # FIX: comments throughout the code and it made it way easier to track what I'd done without having to re-read everything from scratch. Next time I work with AI on a coding task, I'd be more skeptical earlier — I caught the misleading Copilot suggestion, but only after I'd already started implementing it, so in the future I want to read AI suggestions more carefully before touching the code at all. This project genuinely changed how I see AI-generated code — I used to assume that if AI wrote it and it ran without errors, it was probably fine, but this showed me that code can run perfectly and still be completely wrong in its logic.