# Walnut Backgammon

**Play it:** https://robogb2021.github.io/walnut-backgammon/ (TV mode: add `#tv` to the address)

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
- **Learning mode.** Turn on *Learning mode* to get a coach.
  - **Hint** (or <kbd>H</kbd>) opens a card with the coach's best move. Teal arcs
    trace the move on the board while ghost checkers fly it. The card explains
    why the move is best (hits, key points, primes, anchors, escaping back
    checkers, risk as "N of 36 rolls" and what a hit would cost) and ranks the
    alternatives. **Play it** makes the move for you.
  - When you end your turn the coach grades your move as Best, Good, Doubtful
    or Mistake. If there was a better move, **Show me the best move** takes yours
    back and animates the best one.
  - Short lesson pop-ups appear the first time something important happens in a
    game: being hit, entering from the bar, doubles, blots, and bearing off.
  - The coach panel gives a tip for the current situation and explains each
    computer move.
- **Engine.** The computer and the coach share one engine. It uses an opening
  book of the standard first moves from computer rollouts. After that it looks
  one roll ahead: each candidate play is scored against the opponent's best reply
  to all 36 rolls. In self-play it wins about 60% of games against the earlier
  version. It is still a heuristic engine, not a neural network, so its advice is
  sound on the fundamentals but can be wrong on fine points.
- **The room.** The board sits on a card table under a pendant lamp, in a
  panelled room with a log fire, a rainy moonlit window, a bookcase and a
  mantel clock that shows your real local time. Bloom, flickering fire and
  candle light, soft contact shadows under the checkers, embers and dust in the lamp beam set the mood. The fire crackles
  and the clock ticks in the background. The page opens with a camera drift
  across the room; click or press a key to skip it.
- **Opponents.** Play against a heuristic computer player, or two players can
  share one screen.

- **Player names.** Type each player's name in **Menu** (one box against the
  computer, two for two players). Names replace "White" and "Black" on the
  scoreboard, in messages, on the TV banner and on the cursor tags, and are
  remembered on that device. A phone controller sets its player's name under
  **☰ Menu → Your name**. A friend who joins by invite link is asked for their
  name, which appears on your screen as soon as they type it.

- **TV mode.** Press **TV mode** (or <kbd>T</kbd>), or open the page with `#tv`
  at the end of its address. Text and buttons get bigger and the margins widen
  so nothing is cut off at the edges of the TV. You can play with a TV remote,
  a keyboard or a game controller, with no mouse needed. The arrow keys (or
  D-pad) jump a teal cursor between the checkers you can move, then between
  the places the chosen checker can go. OK/Enter selects and Back cancels.
  Coach cards work the same way.
  - **Graphics** switches between High and Smooth. Smooth turns off glow, dust and
    embers and renders at normal resolution, for TV browsers and older devices.
    The game picks Smooth by itself if the first few seconds run slowly.
  - **Full screen** is offered where the browser allows it.
  - To get it on a TV: cast the browser tab from Chrome (⋮ → Cast → Cast tab),
    connect a laptop by HDMI, or open the page in the TV's own web browser.

- **Phones as controllers.** Press **Phones** (or <kbd>P</kbd>) and a QR code
  appears for each colour. Each player scans theirs and their phone becomes a
  **swipe pad** for the TV. Swipe and the cursor on the TV moves the same way
  (left is left, as you see the board), and a longer drag keeps stepping. Tap to
  pick up the checker under the cursor, then swipe to where it should go and
  tap again. The pad says where the cursor is ("Checker on 13 (5 there)", "Put
  it on the 8 point (hits!)"), so you rarely need to look down. Below the pad
  are Roll / End turn, Undo, Hint and Back, plus your dice and the status.
  Coach cards appear on the phone of the player whose turn it is.
  - **On the TV** the cursor takes the colour of the player steering it (cream
    for White, red for Black) with their name above it, and a banner reads "Black
    is playing from their phone" and pulses with each swipe.
  - **Menu on the phone.** The ☰ Menu button opens the game settings: opponent,
    learning mode, camera, graphics, sound and TV mode. It also has buttons to
    show the join codes on the TV and to start a new game (it asks first).
    Either player can change settings at any time, and the TV briefly confirms
    each change.
  - **The TV stays uncluttered.** The settings row is hidden. A small **Menu**
    button next to the scores (or <kbd>M</kbd>) shows it when needed.
  - Phones only act on their own turn and buzz when it starts. A Black phone
    joining switches the game to two players. Without a camera, open
    `controller.html` and type the six-letter code shown on the TV.
  - The phone first tries a direct WebRTC link to the game, introduced by the
    free [PeerJS](https://peerjs.com) service. If that hasn't connected within
    about 7 seconds, it falls back to a relay through a free public MQTT
    broker (EMQX, then HiveMQ, then Mosquitto). The relay works on any Wi-Fi or
    mobile data. The phone's status shows "Connected" or "Connected via relay".
    Phones only work from the GitHub Pages copy, not from inside an embedded
    frame.

- **Action camera.** **Camera: Action** (the default; toggle with the button or
  <kbd>C</kbd>) swoops low to follow the dice as they tumble, holds on the
  result, then follows each checker as it moves. A hit gives a camera jolt and a
  moment of slow motion, and a win gets a slow victory orbit. The camera stays
  still while you choose your move. **Classic** keeps the camera where you put it.

- **Play a friend remotely.** Open **Menu → Invite a friend** on the game, or
  **Menu → Invite a friend to play remotely** on your phone controller. You get
  a link to send by WhatsApp, Messages or anything else (**Share…**, a
  **WhatsApp** button and **Copy link**). Your friend taps it and the full 3D
  table opens on their phone, tablet or computer, viewed from Black's side.
  They play by clicking or tapping the board, or with the arrow keys, and have
  their own Roll / End turn and Undo buttons and the coach's cards.
  - Your game page is the table: it runs the rules and must stay open. Your
    friend's page mirrors it and sends their moves back. Both screens throw
    their own dice with real physics; your page's roll is the official one, and
    if your friend's dice settle differently they tip over onto the right
    numbers.
  - The connection works across the internet: a direct WebRTC link where
    possible, otherwise the public MQTT relay. On the TV the banner reads "Black
    is playing remotely". The game remembers it is hosting, so your friend can
    reconnect if you reload.

## Controls

| Action | Input |
| --- | --- |
| Roll / end turn | **Roll** button or <kbd>Space</kbd> |
| Move a checker | Click a glowing checker, then a gold arrow. Combined-dice moves are offered too. |
| Undo a move this turn | **Undo** or <kbd>U</kbd> |
| Show the coach's suggestion (learning mode) | **Hint** or <kbd>H</kbd> |
| Deselect | <kbd>Esc</kbd> |
| Orbit / zoom | Drag / scroll or pinch |
| Choose / select / cancel (keyboard or remote) | Arrow keys / <kbd>Enter</kbd> (OK) / <kbd>Esc</kbd> (Back) |
| Gamepad | D-pad or stick to choose, A select, B back, X hint, Y undo, Start roll / end turn |
| Toggle TV mode | **TV mode** or <kbd>T</kbd> |
| Action / Classic camera | **Camera** or <kbd>C</kbd> |
| Phones panel | **Phones** or <kbd>P</kbd> |
| Show / hide settings | **Menu** or <kbd>M</kbd> |
