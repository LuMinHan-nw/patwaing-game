# Pat Waing Echo

A memory game on the Burmese tuned drum circle, made to link out of the Mg Waing
chatbot.

Mg Waing plays a phrase on the drums, you tap it back, and each round adds one
more drum. Miss one and the run ends. Best score is kept in the browser.

## Two pages

- `index.html` — the game on its own.
- `play.html` — the game **and** the Mg Waing webchat on one page. When a run
  ends, the game hands its score to the bot as `user.gameScore` /
  `user.gameRound`. This is the connected version.

  The score is written to the user record rather than posted as a chat message,
  because the bot is usually sitting on a choice card and a choice card rejects
  free text. See the build guide for the menu option that reads it back out.

`play.html` loads `index.html` in an iframe and listens for a `postMessage`, so
there is only one copy of the game. The game notices when it is running inside
the frame and hides its "Back to Mg Waing" link, since the chat is already
on screen.

Everything else is in `index.html` — no build step, no libraries, no image or
audio files. The drum sounds are generated with the Web Audio API (a sine tone with a
fast pitch drop, which is what makes it read as a struck drum rather than a
beep).

Nine drums instead of the real instrument's twenty-one, tuned to a pentatonic
scale. That's an approximation — actual pat waing tuning is close to
equidistant and doesn't line up with Western notes.

## Running it locally

Open `index.html` in a browser. That's it.

## Putting it on GitHub Pages

GitHub account: **LuMinHan-nw**. The repo must be named exactly `patwaing-game`
for the URLs below to be right.

1. Go to https://github.com/new. Repository name `patwaing-game`, set it to
   **Public**, click Create.
2. On the empty repo page click **uploading an existing file**, then drag in
   `index.html`, `play.html` and this README. Click **Commit changes**.
3. Repo **Settings → Pages**, set Source to `Deploy from a branch`, branch
   `main`, folder `/ (root)`, save.
4. Wait a minute or two, then it is live at:
   - https://luminhan-nw.github.io/patwaing-game/ — the game on its own
   - https://luminhan-nw.github.io/patwaing-game/play.html — game + chat together

The chatbot button points at the `play.html` one.

## Changing things

- **Chatbot link** — the "Back to Mg Waing" URL is set at the bottom of the
  script, in one place.
- **Number of drums** — add or remove frequencies from the `NOTES` array. The
  circle lays itself out from the array length.
- **Speed** — the `550` in `playSequence()` is the gap between drums when the
  phrase is played back.
