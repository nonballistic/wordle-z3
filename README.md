# wordle solver

wordle is cool. I also want to learn Z3 and be better at wordle.

its basically hangman+. you get 5 guesses for a 5 letter word, and with each word guess it states whether a letter either doesnt exist in the answer, exists but you entered it at the wrong position, or it exists and you entered it in the right position.


## requirements

- requests
- z3

## usage

run the `get_dict.py` to download the dictionary of words scraped from the website.

run the `solve.py` and enter constraints to determine the word to enter into the wordle website. The first and second guesses should be 'slate' and 'round' because it seems to work reliably. run the script when wanting to find the 3rd word. its pretty hacky but makes solving it easier and its how a human would do it.

the gray constraints are just the excluded letters.

the gold constraints are the letter and position pairs separated by a .

the green constraints are the letter, position, and occurrence pairs separated by a . T for occurrence means it occurs only once, F means multiple times or unknown. 

for example, for 2022-01-14:
- entering 'slate' reveals 'a' and 't' as gold, else gray
- constraints are 'sle,a2.t3,'
- entering 'round' reveals 'n' as gold, else gray
- constraints are now 'sleroud,a2.t3.n3,'
- script returns 'antic'. entering this reveals 'a', 'n', 't' as gold else gray
- constraints are now 'sleroudic,a0.n1.t2.a2.t3.n3,'
- script returns 'tanga'. 'tang' are green, else gray.
- constraints are now 'sleroudic,a0.n1.t2.a2.t3.n3,t0F.a1T.n2F.g3F'.
- script returns 'tangy', which is correct.
```
Wordle 209 5/6

⬛⬛🟨🟨⬛
⬛⬛⬛🟨⬛
🟨🟨🟨⬛⬛
🟩🟩🟩🟩⬛
🟩🟩🟩🟩🟩
```
