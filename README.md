# Walnut Backgammon

A 3D backgammon table built with [three.js](https://threejs.org) and the
[cannon-es](https://github.com/pmndrs/cannon-es) physics engine. It is a single
self-contained `index.html` with no build step.

## Run it

Open `index.html` in a modern browser, or serve the folder:

```bash
cd walnut-backgammon
python -m http.server 8080   # then visit http://localhost:8080
```

three.js and cannon-es load from the jsDelivr CDN, so the first load needs a
network connection.

## What's in it

- **Physics dice.** Each throw is a rigid-body simulation. The result is read
  from whichever face ends up on top. A die that comes to rest tilted against a
  checker or the bar counts as cocked and is thrown again, as under tournament
  rules.
- **Physical checkers.** Checkers are lifted and carried in an arc, then released
  just above their point and land under gravity. Dice bounce off resting
  checkers, the bar and the frame.
- **Synthesised sound.** Every sound is generated with the Web Audio API, so there
  are no audio files. Collision impulses from the physics engine drive the
  volume and type of each hit: dice on felt, dice on the walnut rim, dice on
  dice, and checker on checker. The page also synthesises the rattle of the
  leather cup, the rolling noise of a tumbling die, and a short room reverb.
- **Full rules.** The game handles hitting, the bar, entering, bearing off,
  doubles, the rule that you must use both dice where possible (or the larger
  one when only one can be played), and gammon and backgammon scoring.
- **Opponents.** Play against a heuristic computer player, or two players can
  share one screen.

## Controls

| Action | Input |
| --- | --- |
| Roll / end turn | **Roll** button or <kbd>Space</kbd> |
| Move a checker | Click a glowing checker, then a lit point. Combined-dice moves are offered too. |
| Undo a move this turn | **Undo** or <kbd>U</kbd> |
| Deselect | <kbd>Esc</kbd> |
| Orbit / zoom | Drag / scroll or pinch |
