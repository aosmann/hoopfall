# Hoopfall

Educational basketball flick game for the EduGames portal. A question sits at the top; three hoops carry the three answers on their backboards. Flick the ball up through the right one.

- Right hoop: +1 (×2 from 3 in a row, ×3 from 5 in a row), net swish, next question
- Swish (no rim, no board) on the right hoop: +1 bonus
- Wrong hoop: lose a ball (3 balls), the backboard flashes red and the right hoop lights up green
- Air ball (misses every hoop): no ball lost, but −2 s and the streak resets; same question again, and it does not count as asked
- The run ends when the balls run out, the clock hits zero, or the topic has no fresh questions left ("Topic cleared")
- Easy: big hoops, still. Medium: smaller hoops at different heights. Hard: hoops slide left and right
- Streaks: combo banner, crowd cheer and a flaming ball
- Fixed time per run: 60, 90 or 120 s
- No question repeats in a run. Record kept per topic, difficulty and time

## Controls
- Touch or mouse: drag up from the ball and let go. The swipe's direction aims, its speed sets the power. A faint arc preview shows while dragging. A flick that lines up with a hoop is pulled onto it, so a clean flick toward a hoop goes in; very slow flicks fall short, very fast ones go long off the rim or board.
- Keyboard: 1 / 2 / 3 throws a perfect shot at that hoop (accessibility). Esc or P pauses.

Plain canvas 2D (pseudo-3D court, real arc with gravity, rim and backboard bounces), no build step, works offline after the first visit, installs to the home screen. Portrait first, works on laptops; fills the visible screen with 100dvh.

## Files
- `index.html`: the game (court, hoops, ball physics, flick input, menus, audio, scoring, PORTAL EMBED block)
- `questions.js`: the shared EduQ question bank (v2), byte-identical to Lanefall, Stackfall and Slicefall. Do not edit here.
- `game.json`: portal metadata and teacher settings (level, time)
- `sw.js`, `manifest.webmanifest`, `icon-*.png`: offline support and install

## Portal
Follows the EduGames game contract v1: `?topic=<id>&level=1-3&time=60|90|120&lock=1` starts a run at once; posts `edu-ready`, `edu-progress` after every answer and `edu-result` at the end (also kept in `localStorage['edu-results']`). The result adds `swishes`, `livesLeft`, `timeUsed` (seconds played), `time`, `airballs`, `shots` and `cause` (`time` / `lives` / `done` / `quit`); `missed[].picked` is the answer on the hoop the ball went through.

`?debug=1` exposes a read-only `window.HF` hook used by the automated tests.
