# Word Serpent

A neon-styled twist on the classic Snake game. Instead of eating generic food, the snake spells out a word you choose — each letter is collected in order until the word is complete.

## How it works

1. Enter any word (2–16 letters, A–Z).
2. The snake starts as a bare head — no letters collected yet.
3. The first letter of your word appears somewhere on the board. Steer the snake into it.
4. Each time you eat the next correct letter, the snake grows by one body segment that displays the collected letter. Body segments are arranged from head to tail in the order the letters were eaten, so the snake literally spells out your word as it grows.
5. The word on the progress bar lights up as letters are collected, and the next target letter pulses to remind you what you're hunting for.
6. Complete the word to win. Hit a wall, your own tail, a wrong letter (Challenge / Mad / Utterly Unhinged), or the red serpent (Utterly Unhinged) — and it's game over.

## Game modes

Pick a mode from the **Mode** dropdown on the start screen.

### Classic
The original behavior. Only the correct next letter appears on the board at any time. Eat it, the next correct letter spawns, and so on. The only ways to lose are walls and self-collisions.

### Challenge
Two **decoy letters** appear alongside the correct letter (3 pellets total on the board). Decoys look identical to the real letter — same glow, same pulse — so you have to actually know what letter you're hunting for. Eating a wrong letter ends the game immediately. When you eat the correct letter, the existing decoys are cleared and a fresh set of 2 decoys spawns alongside the next target.

### Mad
Like Challenge, but the decoys **accumulate**. The board starts with the correct letter + 2 decoys. Every time you eat a correct letter, the eaten pellet is removed and a *new* correct letter plus 2 *additional* decoys are added — nothing on the board is ever cleared mid-game. After a few correct letters the board is crowded with pellets and you have to navigate carefully.

A subtle consequence: because decoys persist, a letter that was a decoy earlier can become the correct target later in the word. In that case you can eat that pellet and it counts — the rule is always "does the letter on the pellet match the current target letter?", regardless of when the pellet was placed.

### Utterly Unhinged
Challenge rules (correct letter + 2 reshuffled decoys, wrong letter is instant death) **plus** a hostile AI snake — a glaring **red serpent** with reptilian slit pupils and angry brows. It spawns in the far corner of the board and:

- Constantly pathfinds toward the **correct** letter (it ignores decoys), greedy + obstacle-avoiding.
- Moves on its own timer, ~1.4× slower than your snake.
- Grows by one segment every time it eats a correct letter.
- If it eats the food before you do, that letter respawns somewhere else and the decoys reshuffle — you're still hunting the same target, but the red snake has stolen a head start and grown bigger.

There are now three extra ways to lose in this mode:

1. **Touch the red snake** — your green snake's head entering any cell occupied by the red serpent (head or any body segment) is an instant loss. (Equivalently: if the red snake walks into your body, you also lose — you can't shield yourself behind your tail.)
2. **Wrong letter** — same Challenge rule.
3. **Get out-eaten** — if the red snake eats as many correct letters as the *whole word* has (e.g., 4 for "COSA", 5 for "SNAKE"), the player loses. Watch the red snake's growing body length as a built-in danger meter: it starts at 3 segments and gains one per letter it steals, so a length of `3 + word.length` is game over.

If the red snake gets trapped and kills itself (corners itself with its own body or yours), it bursts into red particles and respawns ~1 second later in a far corner. Its eaten-letter tally **does not** reset on death — you can't farm respawns to wipe its progress.

## Play

Open `index.html` in any modern browser — no build step, no dependencies.

## Controls

- **Arrow keys** or **WASD** — move
- **Enter** — start / restart
- **On-screen D-pad** — appears automatically on small screens

## Speed

Pick **Slow / Normal / Fast / Turbo** from the dropdown before pressing Play. Speed only controls how often the snake takes a step — input handling stays smooth at every setting. The combo of high speed + Mad mode quickly becomes a panic puzzle of dodging letters you placed yourself.

## Tips

- Plan your route to the next letter before you start moving — once the snake is long, you can't double back.
- In Mad mode, try to remember where the older decoys are placed; some of them may end up matching a future target letter, giving you a shortcut.
- In Utterly Unhinged mode, race the red snake to the food — but also try to corner it. The greedy AI can paint itself into a wall with its own body, and a brief respawn delay is the closest thing to a breather you'll get.
- A shorter word in Utterly Unhinged is *not* necessarily easier: the loss threshold (red eating `word.length` letters) is lower, so the red snake doesn't need to steal as many letters before you lose.
- Shorter words are easier on small screens. Longer words mean a longer snake — and a more crowded board in Mad mode.

## File layout

- `index.html` — the entire game (HTML + CSS + JavaScript in a single file, no build step, no dependencies).
- `README.md` — this file.
