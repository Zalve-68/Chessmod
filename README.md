Donne moi une description en anglais de l'app
Here's a ready-to-use description, from the GitHub "About" line up to a README block.

About (short, ~1 line for GitHub)

Android overlay for chess.com: reads the live board through accessibility, runs Stockfish on-device, and draws gradient arrows, evaluation and chess.com-style move grades on top of the game.

Topics (GitHub tags) android chess stockfish overlay accessibility-service chess-com kotlin-free java arm64 chess-engine

Long description

ChessMod is a no-root Android overlay that watches a live chess.com game and helps you understand the position in real time.

It never takes screenshots — chess.com is protected by FLAG_SECURE — so the board is reconstructed by walking the accessibility node tree (d7, empty / Black Rook on a8). From that position, a bundled Stockfish engine (arm64-v8a, executed as a local process) analyses the position and the result is drawn directly over the board: a themed gradient arrow for the suggested move, a compact evaluation chip, and BEST / MID / WORST badges for the top three lines.

Moves are annotated with chess.com's own ten-grade scale (Brilliant, Great, Best, Excellent, Good, Book, Inaccuracy, Mistake, Blunder, Miss) through a win-probability model, so the feedback matches what the site itself would say — including per-grade counters for the current game.

Features

Live board reading via AccessibilityService, no screenshots, no root, no emulator
On-device Stockfish (arm64), MultiPV search, watchdog + self-test on startup
12 selectable arrow gradients, rendered once and shared by the overlay and the in-app preview
Clock detection: the remaining time on both clocks is read and the engine depth, think time and gesture speed adapt to it
"Human" mode: deliberately imperfect move choice, natural-move bias, rotating aggressive / positional / defensive style, one minor inaccuracy every 7–10 moves, fast forced moves, and resignation when the position is lost
Auto-play and auto-new-game, with result detection (win / loss / draw)
Dashboard app: live journal, 12 languages with system-locale detection, game history with board thumbnails, accuracy and a per-move review
Small draggable floating menu with animated toggles, status indicator and grade strip
Tech Built without AndroidX or Gradle: the APK is assembled on-device (Termux) with aapt2 → javac → d8 → zipalign → apksigner. The UI is written entirely in Java, programmatically, on a dark palette (#080D0A background, #111A15 cards, #2AA79B accent). Roughly 4,500 lines across 16 classes; the APK is about 92 MB, mostly the engine binary.

Requirements Android 8+, arm64 device, accessibility permission, and chess.com installed. The accessibility service must be re-enabled after every reinstall.

Disclaimer The project automates the chess.com interface. Using it on rated games breaks the site's terms of service and can get the account closed. It is published for study and for unrated games with friends only. Stockfish is GPLv3: any redistribution of the APK must ship the corresponding source.

What it is not Not a bot farm, not an account service, not a screenshot/OCR pipeline — it reads only what the accessibility layer already exposes and works entirely offline.
