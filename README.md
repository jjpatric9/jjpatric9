## TallmanGames

Small, carefully-tested Android games. Made by Joshua Patrick, in Canada.

Six years of software development, now channelled into games — I build with AI tooling and
care a lot about the things players feel but never see: input that never fights the finger,
difficulty that's measured rather than guessed at, and a game that's had thousands of test
runs played against it before anyone else touches it.

---

### 🎮 BoxStacker

A stacking game about balance. A crane holds the crate you picked from your hand; you slide it
sideways and drop it. Complete a row and it sets, becoming the tower's new foundation — but the
crates you're dealt rarely let you finish a row cleanly, and every hole and overhang pushes the
tower further off centre. Lean too far and the whole thing goes over.

<!-- SCREENSHOT: replace with a GIF of one placement and a topple -->

**Android · Kotlin · Jetpack Compose**

<!-- STORE LINK: add once the listing is live -->

Some of how it's built:

- **The game rules are a pure-JVM module** with no Android dependencies at all, so the entire
  ruleset is testable in seconds without an emulator.
- **Difficulty is measured, not assumed.** Each hand of pieces is generated against the board
  actually in front of you, then played out by bots hundreds of times to check it's survivable
  before you're dealt it.
- **The balance model was rebuilt four times.** Two of those versions were *correct* physics and
  were thrown out anyway for being unplayable — the shipped one is worse physics and a far better
  game.
- **No network permission, no analytics, no tracking.** BoxStacker cannot send anything anywhere,
  by construction.

---

### Coming next

More games in the same shape: small, offline, no accounts, nothing that gets between you and the
thing you're playing.

---

### Contact

📧 **jjpatric9@gmail.com**

🌐 **[tallmangames site](https://jjpatric9.github.io/)** · [Privacy](https://jjpatric9.github.io/privacy.html) · [Support](https://jjpatric9.github.io/support.html)
