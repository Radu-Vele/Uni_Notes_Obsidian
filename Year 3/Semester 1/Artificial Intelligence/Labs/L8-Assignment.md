# First Order Logic cont'd

## Assignment 

> [!info] Assignment on Logics
> - Deadline `Sunday 18 december`
> - Postponed for `23 december`

_Task:_ Implement something of your own choice with Prover9/Mace4.

Deliverable:
1.  source code in zip format
2.  documentation using the laboratory template

_Evaluation:_
Main criteria: originality, creativity.
Other criteria: code quantity in Prover9/Mace4/Python.

### Ideas: 

0a. AllOuts - extend the game with other patterns or else (https://users.utcluj.ro/~agroza/papers/2022/iccp2022_preprint_borbalagroza.pdf)

0.b Mupuzels (https://livrepository.liverpool.ac.uk/3027148/1/Revisiting_MU_puzzle__A_case_study_in_finite_countermodels_verification___.pdf)

0c. Puzzle-based dataset (https://users.utcluj.ro/~agroza/papers/2021/21_consilr_preprint.pdf)

0d Question answering (https://users.utcluj.ro/~agroza/papers/[slides](https://moodle.cs.utcluj.ro/mod/folder/view.php?id=39882 "Slides")/sac2022.pdf)

1. MineFOL + Pacman. Pacman gets messages in FOL where the food is.

2. MineFOL. Generate (by hand or automatically from Python) some valid/difficult MineFOL games.

2b. MineFOL. Build a Web interface or Phython Jupyter code (similar with http://intrologic.stanford.edu/extras/minefield.html) in which one cannot go in cells for which Prover9 fails to prove safeness. Install your Web Interface/or run from Jupyther notebook on one computer from room 21).

3. Escape room games. See EscapeRoom.pdf for some examples or develop/adapt your own game/ideas). The nmeain ides: At each step ask Prover9 to prove that the specific position is safe.

4. Puzzles  in First Order Logic. Some example at https://github.com/APGroza/logic-games or https://users.utcluj.ro/~agroza/puzzles/maloga/codes.html

5. Among Us in FOL. starting from Knight and Knaves towards Crewmates and Impostors, messages are in FOL. Maybe something related with Knights, Knaves and Spies puzzles)

6. Code verification (some examples http://www.tptp.org/cgi-bin/SeeTPTP?Category=Problems&Domain=SWV)

7. Hardware verification  (some examples http://www.tptp.org/cgi-bin/SeeTPTP?Category=Problems&Domain=HWV)

8. Natural Language Understanding: NLTK + mace4 (discourse checking - http://www.nltk.org/howto/discourse.html) (max 9 points) (some examples http://www.tptp.org/cgi-bin/SeeTPTP?Category=Problems&Domain=NLP)

9. A curious number machine 1-20 ([0_Smullyan, Raymond M - The Lady or the Tiger And Other Logic Puzzles Including a Mathematical Novel That Features Gödels Great Discovery (2013).pdf](https://moodle.cs.utcluj.ro/pluginfile.php/93142/mod_wiki/attachments/92//0_Smullyan%2C%20Raymond%20M%20-%20The%20Lady%20or%20the%20Tiger%20And%20Other%20Logic%20Puzzles%20Including%20a%20Mathematical%20Novel%20That%20Features%20G%C3%B6dels%20Great%20Discovery%20%282013%29.pdf?forcedownload=1)) - maybe with set(production)

10. Craigs Law 1-9 ([0_Smullyan, Raymond M - The Lady or the Tiger And Other Logic Puzzles Including a Mathematical Novel That Features Gödels Great Discovery (2013).pdf](https://moodle.cs.utcluj.ro/pluginfile.php/93142/mod_wiki/attachments/92//0_Smullyan%2C%20Raymond%20M%20-%20The%20Lady%20or%20the%20Tiger%20And%20Other%20Logic%20Puzzles%20Including%20a%20Mathematical%20Novel%20That%20Features%20G%C3%B6dels%20Great%20Discovery%20%282013%29.pdf?forcedownload=1)) - maybe with set(production) (?)

11. Operation numbers ([0_Smullyan, Raymond M - The Lady or the Tiger And Other Logic Puzzles Including a Mathematical Novel That Features Gödels Great Discovery (2013).pdf](https://moodle.cs.utcluj.ro/pluginfile.php/93142/mod_wiki/attachments/92//0_Smullyan%2C%20Raymond%20M%20-%20The%20Lady%20or%20the%20Tiger%20And%20Other%20Logic%20Puzzles%20Including%20a%20Mathematical%20Novel%20That%20Features%20G%C3%B6dels%20Great%20Discovery%20%282013%29.pdf?forcedownload=1)) - maybe with set(production) (?)

12. Domino puzzles (Dudeney, 536 puzzles, http://www.mathematische-basteleien.de/dominos.htm) (9 points)

13. Wumpus (Pacman framework + call Prover9 from Python)

14. Wumpus + Mace4/Prover9 (https://github.com/mcdougal/WumpusWorld) (! you need to go in bin directory and "chmod +x prover9")

15. Abstract argumentation in FOL/propositional (Dung argumentation framework)

16. Catabot Rescue Game (http://ceur-ws.org/Vol-1651/12340026.pdf)

17. Using Mace4 to generate/design Sudoku games (not to solve them)

18. Detecting unknots via Mace4 (see paper)

19. Self Configuration of Network device (see paper)

20. Compilers and Prover9 (see paper)

21. Given a big rectangle and a number of small rectangles, can you fit the small rectangles  
in the big one such that no two overlap? (see paper)

22. Model Visualisation (extend the model.zip with something)

23. Web interface - logic quiz for students (see paper below)

24. Puzzle generator using Mace4

25. Planning in FOL. You have to use set(production) mode in Prover9. Two examples "Going to church" and "Buying wine" from https://users.utcluj.ro/~agroza/puzzles/maloga/codes.html

26. Polyomino puzzles (see book) (http://puzzler.sourceforge.net/docs/polyominoes.html)

27. Magnets (see logicpuzzle.pdf, https://www.chiark.greenend.org.uk/~sgtatham/puzzles/js/magnets.html)

29. Minefield + Python (see mine4x4in below and minesweeper.in from https://users.utcluj.ro/~agroza/puzzles/maloga/codes.html)

30. Card puzzles (https://www.mathsisfun.com/puzzles/card-puzzles-index.html)

31. Game (https://www.mathsisfun.com/games/allout.html) - Planning in Fol; use set(production).

32. Cryptography puzzles. For instance, https://www.braingle.com/brainteasers/Cryptography.html

33. Logic puzzles. For instance, https://www.braingle.com/brainteasers/Logic.html

34. Logic grid. https://www.braingle.com/brainteasers/Logic-Grid.html

35. Mystery. For instance https://www.braingle.com/brainteasers/Mystery.html

36. Probability. For instance, https://www.braingle.com/brainteasers/40606/two-games-in-a-row.html. You could run mace4 twice. First to compute/count the possible models. Second, to compute/count the favorable models.

37. Comparison puzzles. For instance https://www.funtrivia.com/trivia-quiz/BrainTeasers/Who-is-Taller-101647.html

38. Social deduction games. For instance Werewolf  (aka Mafia)

39. Can you crack the code (puzzles similar to https://me.me/i/will-you-crack-the-code-o-6-8-2-one-6091172)

### My choice:
Maybe one of the:
	- 33. Logic puzzles. For instance, https://www.braingle.com/brainteasers/Logic.html
	- 20. Compilers and Prover9 (see paper)
	- 7. Hardware verification  (some examples http://www.tptp.org/cgi-bin/SeeTPTP?Category=Problems&Domain=HWV)
	- 0a. AllOuts - extend the game with other patterns or else (https://users.utcluj.ro/~agroza/papers/2022/iccp2022_preprint_borbalagroza.pdf)

# Lab 8 Material - Inference in FOL
### Resolution

### Skolemization
- implement the who-killed-the-cat problem

### Paramodulation
- deal with equality in mace4
### Demodulation


### Wumpus