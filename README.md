# Fill the Boxes! (Uno-card edition)

A kid-friendly 2-player game for a phone or tablet. One file, no internet needed: `index.html`.

## Rules
- Each player has **10 boxes numbered 0-9**. A shuffled real 108-card Uno deck sits in the middle (reshuffled when it runs out).
- On your turn **tap the deck**. The card flips face up. **Touch, hold and drag** it down onto the matching numbered box on **your own board** (the right box glows/pulses).
  - **New number** → box fills, you draw again.
  - **Number you already have** → drop it on its (filled) box; your turn ends.
  - **Special card** (Skip, Reverse, Draw Two, Wild, Wild Draw Four) → "Special card! Turn over". Drag it to the 🗑️ bin (or just tap it). No box is filled.
  - Wrong box or empty space → the card snaps back with a little shake. No penalty.
- **First to fill all 10 boxes wins** (confetti + Play Again). Win counts are remembered.
- Helper: if the card isn't dragged for a few seconds it wiggles; **tapping it then auto-places it**.
- Random pick for who goes first. Names and win tally are stored in `localStorage` (⚙️ = change names, 🔊 = mute).

## Change the rules
At the top of the `<script>` in `index.html`:
```js
const SPECIAL_CARD_RULE = 'end-turn';   // or 'draw-again' (special = no penalty, draw again)
```
Timings (hint delay etc.) are in `CONFIG` just below it.

## Open it on a phone / tablet
The game is a single file, so you just need to get it onto the device:
1. **Easiest (same Wi-Fi):** on the computer that has the file run  
   `cd uno-fill && python3 -m http.server 8080`  
   then on the phone open `http://<computer-ip>:8080/` in Safari (iPhone/iPad) or Chrome (Android).
2. **Or** put `index.html` on any web host (GitHub Pages, Netlify drop, etc.) and open that link.
3. **Or** AirDrop / email / cloud-drive the file to the device and open it (Android Chrome: open from Files; on iOS use option 1 or 2 for home-screen install).

### Add to Home Screen
- **iPhone / iPad (Safari):** tap Share ⬆️ → **Add to Home Screen** → Add. It opens full-screen like an app.
- **Android (Chrome):** ⋮ menu → **Add to Home screen** / **Install app**.

### Offline
There are no external files or fonts, so once the page has loaded (or the file is saved on the device) it runs with no internet. Note: there's no service worker (a single file can't register one), so if you install from a web link, keep that page cached by opening it once; opening a local copy of the file always works offline. Names/wins are saved per browser/origin — use the same address each time.

## Tests
`node test-headless.js` (needs `playwright-core` and Chrome) runs 44 checks: deck, drag & drop with mouse and real touch events, turn rules, 0-9 boxes, specials, win, reshuffle, and a full random game.
