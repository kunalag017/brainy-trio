<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Brainy Trio · Puzzle Hub</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 16px;
      background: radial-gradient(circle at top, #20294f, #050816);
      color: #f9fafb;
    }

    .app {
      width: 100%;
      max-width: 520px;
      background: rgba(15, 23, 42, 0.9);
      border-radius: 20px;
      padding: 20px 18px 18px;
      box-shadow:
        0 20px 30px rgba(15, 23, 42, 0.65),
        0 0 0 1px rgba(148, 163, 184, 0.12);
      backdrop-filter: blur(18px);
      display: flex;
      flex-direction: column;
      gap: 14px;
    }

    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 16px;
    }

    .title {
      font-size: 1.1rem;
      font-weight: 600;
      letter-spacing: 0.02em;
    }

    .badge {
      font-size: 0.7rem;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(56, 189, 248, 0.12);
      color: #22d3ee;
      border: 1px solid rgba(45, 212, 191, 0.35);
      text-transform: uppercase;
      letter-spacing: 0.09em;
    }

    .subtitle {
      font-size: 0.9rem;
      color: #9ca3af;
      margin-bottom: 18px;
    }

    .nav {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px;
    }

    .nav-btn {
      border-radius: 999px;
      border: 1px solid rgba(55, 65, 81, 0.9);
      padding: 8px 10px;
      font-size: 0.8rem;
      background: rgba(15, 23, 42, 0.9);
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 2px;
      cursor: pointer;
      transition: all 0.15s ease;
      color: #e5e7eb;
    }

    .nav-btn span:first-child {
      font-weight: 600;
      font-size: 0.78rem;
    }

    .nav-btn span:last-child {
      font-size: 0.72rem;
      color: #9ca3af;
    }

    .nav-btn--active {
      border-color: rgba(56, 189, 248, 0.9);
      background: linear-gradient(to right, rgba(56, 189, 248, 0.2), rgba(59, 130, 246, 0.24));
      box-shadow: 0 10px 20px rgba(59, 130, 246, 0.35);
    }

    .game-panel {
      margin-top: 4px;
      padding: 12px 12px 10px;
      border-radius: 14px;
      background: rgba(15, 23, 42, 0.8);
      border: 1px solid rgba(148, 163, 184, 0.35);
    }

    .game-panel h2 {
      font-size: 0.98rem;
      font-weight: 600;
      margin-bottom: 6px;
    }

    .game-panel p {
      font-size: 0.9rem;
      color: #e5e7eb;
      margin-bottom: 8px;
    }

    .options {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 8px;
      margin-top: 6px;
    }

    .option {
      border-radius: 14px;
      border: 2px solid rgba(15, 23, 42, 0.9);
      padding: 10px 6px;
      font-size: 0.8rem;
      background: rgba(15, 23, 42, 0.95);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      transition: all 0.15s ease;
      text-align: center;
    }

    .option input {
      accent-color: #22c55e;
    }

    .option-swatch {
      width: 26px;
      height: 26px;
      border-radius: 999px;
      border: 2px solid rgba(15, 23, 42, 1);
      box-shadow: 0 0 0 1px rgba(15, 23, 42, 0.6);
    }

    .option:hover {
      border-color: rgba(96, 165, 250, 0.9);
      background: rgba(15, 23, 42, 1);
    }

    .color-grid {
      display: grid;
      gap: 4px;
      margin-top: 10px;
    }

    .color-cell {
      aspect-ratio: 1 / 1;
      border-radius: 10px;
      border: 1px solid rgba(15, 23, 42, 0.9);
      background: rgba(15, 23, 42, 0.9);
      position: relative;
      cursor: pointer;
      transition: box-shadow 0.12s ease, transform 0.05s ease;
      touch-action: none;
    }

    .color-cell--endpoint::after {
      content: "";
      position: absolute;
      inset: 6px;
      border-radius: 999px;
      border: 2px solid rgba(15, 23, 42, 0.85);
      box-shadow: 0 0 0 1px rgba(15, 23, 42, 0.7);
    }

    .color-cell--path {
      box-shadow: 0 0 0 2px rgba(248, 250, 252, 0.5);
      transform: translateY(-1px);
    }

    .actions {
      margin-top: 12px;
      display: flex;
      justify-content: flex-end;
      gap: 8px;
      align-items: center;
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 8px 16px;
      font-size: 0.9rem;
      font-weight: 500;
      cursor: pointer;
      transition: all 0.15s ease;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .btn-primary {
      background: linear-gradient(to right, #22c55e, #10b981);
      color: #022c22;
      box-shadow: 0 10px 18px rgba(16, 185, 129, 0.4);
    }

    .btn-primary:disabled {
      opacity: 0.5;
      cursor: not-allowed;
      box-shadow: none;
    }

    .btn-primary:not(:disabled):hover {
      transform: translateY(-1px);
      box-shadow: 0 16px 26px rgba(16, 185, 129, 0.5);
    }

    .status {
      margin-top: 8px;
      min-height: 22px;
      font-size: 0.85rem;
      color: #9ca3af;
    }

    .status--error {
      color: #fecaca;
    }

    .status--success {
      color: #bbf7d0;
    }

    .location-result {
      margin-top: 12px;
      padding: 10px 12px;
      border-radius: 12px;
      /* Sage + lavender theme */
      background: linear-gradient(135deg, rgba(134, 168, 124, 0.18), rgba(181, 149, 255, 0.14));
      border: 1px solid rgba(181, 149, 255, 0.55);
      font-size: 0.85rem;
    }

    .location-result a {
      color: #67e8f9;
      text-decoration: none;
      word-break: break-all;
    }

    .location-result a:hover {
      text-decoration: underline;
    }

    .copy-btn {
      background: rgba(15, 23, 42, 0.95);
      color: #e5e7eb;
      border-radius: 999px;
      padding: 4px 10px;
      font-size: 0.75rem;
      border: 1px solid rgba(148, 163, 184, 0.5);
      cursor: pointer;
      margin-top: 8px;
    }

    .copy-btn:hover {
      border-color: rgba(96, 165, 250, 0.9);
      background: rgba(15, 23, 42, 1);
    }

    .sudoku-grid {
      display: grid;
      grid-template-columns: repeat(9, minmax(0, 1fr));
      gap: 0px;
      margin-top: 10px;
      background: #ffffff;
      border: 2px solid #0b0f19;
      border-radius: 10px;
      overflow: hidden;
    }

    .sudoku-cell {
      width: 100%;
      aspect-ratio: 1 / 1;
      text-align: center;
      font-size: 0.86rem;
      background: #ffffff;
      border: 1px solid #0b0f19;
      color: #0b0f19;
      border-radius: 0px;
    }

    .sudoku-cell:focus {
      outline: 2px solid #0b0f19;
      outline-offset: -2px;
      background: #f3f4f6;
    }

    .sudoku-cell[disabled] {
      background: #f9fafb;
      color: #0b0f19;
      font-weight: 800;
    }

    .sudoku-grid .bold-bottom {
      border-bottom-width: 3px;
    }

    .sudoku-grid .bold-right {
      border-right-width: 3px;
    }

    .level-badges {
      display: flex;
      gap: 6px;
      margin-top: 4px;
      font-size: 0.72rem;
      color: #9ca3af;
    }

    .level-badge {
      padding: 2px 8px;
      border-radius: 999px;
      border: 1px dashed rgba(148, 163, 184, 0.6);
    }

    @media (max-width: 480px) {
      .app {
        padding: 16px 14px 14px;
      }

      .nav {
        grid-template-columns: 1fr;
      }

      .options {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }

      .header {
        flex-direction: column;
        align-items: flex-start;
        gap: 4px;
      }
    }

    .footer {
      margin-top: 16px;
      font-size: 0.75rem;
      color: #6b7280;
      text-align: center;
    }
  </style>
</head>
<body>
  <main class="app">
    <div class="header">
      <div>
        <div class="badge">Brainy Trio</div>
        <div class="title" style="margin-top: 4px;">Three mini games · One link</div>
      </div>
    </div>
    <p class="subtitle">
      Pick a game below. The third game ends by showing your location name (with permission).
    </p>

    <nav class="nav">
      <button class="nav-btn nav-btn--active" data-game="colors" id="nav-colors">
        <span>Liquid Sort</span>
        <span>3 levels</span>
      </button>
      <button class="nav-btn" data-game="sudoku" id="nav-sudoku" style="display:none;">
        <span>Sudoku</span>
        <span>1 calm grid</span>
      </button>
      <button class="nav-btn" data-game="riddle" id="nav-riddle" style="display:none;">
        <span>Bollywood Match</span>
        <span>Easy recent movies</span>
      </button>
    </nav>

    <section class="game-panel" id="game-colors">
      <h2>Game 1 · Liquid Sort (Water Sort)</h2>
      <p>
        Sort the liquids so each tube contains only one colour. Tap a tube to pick it, then tap another tube to pour.
      </p>
      <div class="level-badges">
        <span class="level-badge" id="water-level-indicator">Level 1 of 3</span>
      </div>
      <div style="margin-top: 10px; font-size: 0.85rem; color:#9ca3af;">
        Rule: you can pour only onto the same top colour (or an empty tube), and only if there is space.
      </div>
      <div id="water-tubes" style="display:flex; flex-wrap:wrap; gap:10px; margin-top: 12px; justify-content:center;"></div>
      <div class="actions">
        <span id="water-status" class="status"></span>
        <button id="water-undo-btn" class="btn-primary">Undo</button>
        <button id="water-reset-btn" class="btn-primary">Reset level</button>
      </div>
    </section>

    <section class="game-panel" id="game-sudoku" style="display:none;">
      <h2>Game 2 · Mini Sudoku</h2>
      <p>
        Fill the grid so each row, column and 3×3 box contains digits 1–9. This is a single curated level.
      </p>
      <div id="sudoku-grid" class="sudoku-grid"></div>
      <div class="actions" style="margin-top: 10px;">
        <span id="sudoku-status" class="status"></span>
        <button id="sudoku-check-btn" class="btn-primary">Check solution</button>
      </div>
    </section>

    <section class="game-panel" id="game-riddle" style="display:none;">
      <h2>Game 3 · Bollywood Movie Match</h2>
      <p>
        Match each recent movie to its lead actor. When all matches are correct, you’ll unlock your location name.
      </p>

      <div style="padding: 10px 12px; border-radius: 12px; border: 1px solid rgba(244, 63, 94, 0.45); background: rgba(244, 63, 94, 0.08);">
        <div style="font-weight: 700; letter-spacing: 0.02em;">Recent Bollywood</div>
        <div style="margin-top: 4px; color: #e5e7eb; font-size: 0.9rem;">
          Quick and easy: pick the correct lead actor for each movie.
        </div>
      </div>

      <div style="margin-top: 10px;">
        <div style="display:grid; grid-template-columns: 1fr 1fr; gap: 10px; align-items:center;">
          <div style="font-weight:700; color:#e5e7eb;">Movie</div>
          <div style="font-weight:700; color:#e5e7eb;">Lead actor</div>

          <div style="padding:10px; border-radius:12px; background: rgba(59, 130, 246, 0.14); border: 1px solid rgba(59, 130, 246, 0.45);">
            Jawan (2023)
          </div>
          <select id="match-1" style="padding:10px; border-radius:12px; border:1px solid rgba(148,163,184,0.45); background: rgba(15,23,42,0.95); color:#e5e7eb;">
            <option value="">Choose...</option>
            <option value="srk">Shah Rukh Khan</option>
            <option value="ranbir">Ranbir Kapoor</option>
            <option value="vikrant">Vikrant Massey</option>
          </select>

          <div style="padding:10px; border-radius:12px; background: rgba(34, 197, 94, 0.14); border: 1px solid rgba(34, 197, 94, 0.45);">
            Animal (2023)
          </div>
          <select id="match-2" style="padding:10px; border-radius:12px; border:1px solid rgba(148,163,184,0.45); background: rgba(15,23,42,0.95); color:#e5e7eb;">
            <option value="">Choose...</option>
            <option value="ranbir">Ranbir Kapoor</option>
            <option value="vikrant">Vikrant Massey</option>
            <option value="srk">Shah Rukh Khan</option>
          </select>

          <div style="padding:10px; border-radius:12px; background: rgba(168, 85, 247, 0.14); border: 1px solid rgba(168, 85, 247, 0.45);">
            12th Fail (2023)
          </div>
          <select id="match-3" style="padding:10px; border-radius:12px; border:1px solid rgba(148,163,184,0.45); background: rgba(15,23,42,0.95); color:#e5e7eb;">
            <option value="">Choose...</option>
            <option value="vikrant">Vikrant Massey</option>
            <option value="srk">Shah Rukh Khan</option>
            <option value="ranbir">Ranbir Kapoor</option>
          </select>
        </div>
      </div>

      <div class="actions">
        <span id="riddle-status" class="status"></span>
        <button id="riddle-check-btn" class="btn-primary">Check matches</button>
      </div>

      <section id="location-section" style="display:none; margin-top: 14px;">
        <p class="subtitle" style="margin-bottom: 10px;">
          With your permission, we’ll read your current location and show the location name (city/area).
        </p>
        <div class="actions" style="justify-content: flex-start; margin-top: 0;">
          <button id="locate-btn" class="btn-primary">
            <span>Get my location</span>
          </button>
          <span id="location-status" class="status"></span>
        </div>
        <div id="location-output" class="location-result" style="display:none;"></div>
      </section>
    </section>

    <div class="footer">
      After you complete all three games, you can reveal your location name (city/area). Location uses the browser Geolocation API.
    </div>
  </main>

  <script>
    (function () {
      // Navigation between 3 games
      const navButtons = Array.from(document.querySelectorAll(".nav-btn"));
      const navColors = document.getElementById("nav-colors");
      const navSudoku = document.getElementById("nav-sudoku");
      const navRiddle = document.getElementById("nav-riddle");

      let game1Complete = false;
      let game2Complete = false;
      let game3Complete = false;
      const panels = {
        colors: document.getElementById("game-colors"),
        sudoku: document.getElementById("game-sudoku"),
        riddle: document.getElementById("game-riddle"),
      };

      navButtons.forEach((btn) => {
        btn.addEventListener("click", () => {
          const game = btn.getAttribute("data-game");
          // Only allow access when previous games are complete
          if (game === "sudoku" && !game1Complete) return;
          if (game === "riddle" && !game2Complete) return;
          navButtons.forEach((b) => b.classList.remove("nav-btn--active"));
          btn.classList.add("nav-btn--active");
          Object.keys(panels).forEach((key) => {
            panels[key].style.display = key === game ? "block" : "none";
          });
        });
      });

      // Game 1: Liquid Sort (Water Sort) - 3 levels
      const waterTubesEl = document.getElementById("water-tubes");
      const waterStatusEl = document.getElementById("water-status");
      const waterResetBtn = document.getElementById("water-reset-btn");
      const waterUndoBtn = document.getElementById("water-undo-btn");
      const waterLevelIndicator = document.getElementById("water-level-indicator");

      const TUBE_CAPACITY = 4;
      const WATER_LEVELS = [
        // Level 1 (easy): 3 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#ef4444"],
          ["#3b82f6", "#22c55e", "#ef4444", "#3b82f6"],
          ["#22c55e", "#ef4444", "#3b82f6", "#22c55e"],
          [],
          [],
        ],
        // Level 2 (medium): 4 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#f97316"],
          ["#f97316", "#22c55e", "#3b82f6", "#ef4444"],
          ["#3b82f6", "#f97316", "#ef4444", "#22c55e"],
          ["#22c55e", "#ef4444", "#f97316", "#3b82f6"],
          [],
          [],
        ],
        // Level 3 (harder but solvable): 5 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#f97316"],
          ["#a855f7", "#22c55e", "#3b82f6", "#ef4444"],
          ["#f97316", "#a855f7", "#ef4444", "#22c55e"],
          ["#3b82f6", "#f97316", "#a855f7", "#3b82f6"],
          ["#22c55e", "#ef4444", "#f97316", "#a855f7"],
          [],
          [],
        ],
      ];

      let waterLevelIndex = 0;
      let tubes = [];
      let selectedTubeIndex = null;
      let undoStack = [];

      function cloneTubes(src) {
        return src.map((t) => t.slice());
      }

      function loadWaterLevel(index) {
        waterLevelIndex = index;
        tubes = cloneTubes(WATER_LEVELS[index]);
        selectedTubeIndex = null;
        undoStack = [];
        waterLevelIndicator.textContent =
          "Level " + (waterLevelIndex + 1) + " of " + WATER_LEVELS.length;
        waterStatusEl.classList.remove("status--error", "status--success");
        waterStatusEl.textContent = "Solve the level by sorting colours.";
        renderTubes();
      }

      function topColor(tube) {
        return tube.length ? tube[tube.length - 1] : null;
      }

      function contiguousTopCount(tube) {
        if (!tube.length) return 0;
        const c = topColor(tube);
        let count = 0;
        for (let i = tube.length - 1; i >= 0; i--) {
          if (tube[i] !== c) break;
          count++;
        }
        return count;
      }

      function canPour(fromIdx, toIdx) {
        if (fromIdx === toIdx) return false;
        const from = tubes[fromIdx];
        const to = tubes[toIdx];
        if (!from.length) return false;
        if (to.length >= TUBE_CAPACITY) return false;
        const fromTop = topColor(from);
        const toTop = topColor(to);
        if (!toTop) return true;
        return toTop === fromTop;
      }

      function doPour(fromIdx, toIdx) {
        if (!canPour(fromIdx, toIdx)) return false;
        const from = tubes[fromIdx];
        const to = tubes[toIdx];
        const c = topColor(from);
        const movable = contiguousTopCount(from);
        const space = TUBE_CAPACITY - to.length;
        const amount = Math.min(movable, space);
        if (amount <= 0) return false;

        undoStack.push(cloneTubes(tubes));
        for (let i = 0; i < amount; i++) {
          to.push(from.pop());
        }
        return true;
      }

      function isSolved() {
        return tubes.every((t) => {
          if (t.length === 0) return true;
          if (t.length !== TUBE_CAPACITY) return false;
          return t.every((c) => c === t[0]);
        });
      }

      function renderTubes() {
        waterTubesEl.innerHTML = "";
        tubes.forEach((tube, idx) => {
          const tubeEl = document.createElement("button");
          tubeEl.type = "button";
          tubeEl.style.width = "86px";
          tubeEl.style.height = "190px";
          tubeEl.style.padding = "10px 10px 12px";
          tubeEl.style.borderRadius = "24px";
          tubeEl.style.border =
            idx === selectedTubeIndex
              ? "2px solid rgba(250, 204, 21, 0.9)"
              : "2px solid rgba(148, 163, 184, 0.7)";
          tubeEl.style.background = "rgba(15, 23, 42, 0.9)";
          tubeEl.style.display = "flex";
          // Top of tube is visually at the top; stack segments from top to bottom.
          tubeEl.style.flexDirection = "column";
          tubeEl.style.justifyContent = "flex-end";
          tubeEl.style.gap = "4px";

          for (let s = 0; s < TUBE_CAPACITY; s++) {
            const liquidIndex = tube.length - 1 - s;
            const color = liquidIndex >= 0 ? tube[liquidIndex] : null;
            const seg = document.createElement("div");
            seg.style.height = "30px";
            seg.style.borderRadius = "10px";
            // Very clear, bright colours inside each tube segment
            seg.style.background = color ? color : "rgba(15, 23, 42, 0.5)";
            seg.style.border = color
              ? "2px solid rgba(15, 23, 42, 0.95)"
              : "1px dashed rgba(51, 65, 85, 0.8)";
            seg.style.boxShadow = color
              ? "0 0 10px " + color
              : "inset 0 0 4px rgba(15, 23, 42, 0.9)";
            tubeEl.appendChild(seg);
          }

          tubeEl.addEventListener("click", () => {
            waterStatusEl.classList.remove("status--error", "status--success");
            if (selectedTubeIndex === null) {
              if (!tubes[idx].length) {
                waterStatusEl.classList.add("status--error");
                waterStatusEl.textContent = "Pick a non-empty tube first.";
                return;
              }
              selectedTubeIndex = idx;
              waterStatusEl.textContent = "Now tap a tube to pour into.";
              renderTubes();
              return;
            }

            if (selectedTubeIndex === idx) {
              selectedTubeIndex = null;
              waterStatusEl.textContent = "Selection cleared.";
              renderTubes();
              return;
            }

            const poured = doPour(selectedTubeIndex, idx);
            selectedTubeIndex = null;
            renderTubes();
            if (!poured) {
              waterStatusEl.classList.add("status--error");
              waterStatusEl.textContent = "Invalid pour. Try another tube.";
              return;
            }

            if (isSolved()) {
              waterStatusEl.classList.add("status--success");
              if (waterLevelIndex === WATER_LEVELS.length - 1) {
                waterStatusEl.textContent =
                  "Level complete! You finished Liquid Sort. Sudoku has been unlocked.";
                game1Complete = true;
                navSudoku.style.display = "flex";
              } else {
                waterStatusEl.textContent = "Level complete! Moving to next level...";
                setTimeout(() => loadWaterLevel(waterLevelIndex + 1), 900);
              }
            } else {
              waterStatusEl.textContent = "Good pour. Keep going!";
            }
          });

          waterTubesEl.appendChild(tubeEl);
        });
      }

      waterResetBtn.addEventListener("click", () => loadWaterLevel(waterLevelIndex));
      waterUndoBtn.addEventListener("click", () => {
        if (!undoStack.length) {
          waterStatusEl.classList.add("status--error");
          waterStatusEl.textContent = "Nothing to undo.";
          return;
        }
        tubes = undoStack.pop();
        selectedTubeIndex = null;
        waterStatusEl.classList.remove("status--error", "status--success");
        waterStatusEl.textContent = "Undid the last move.";
        renderTubes();
      });

      loadWaterLevel(0);

      // Game 2: Sudoku (one fixed puzzle)
      const sudokuGridEl = document.getElementById("sudoku-grid");
      const sudokuStatusEl = document.getElementById("sudoku-status");
      const sudokuCheckBtn = document.getElementById("sudoku-check-btn");

      // Beginner-friendly Sudoku: more clues, unique solution
      const sudokuPuzzle =
        "534678000" +
        "672000348" +
        "000342567" +
        "859701423" +
        "420853701" +
        "703924850" +
        "961507204" +
        "287419605" +
        "340286179";

      const sudokuSolution =
        "534678912" +
        "672195348" +
        "198342567" +
        "859761423" +
        "426853791" +
        "713924856" +
        "961537284" +
        "287419635" +
        "345286179";

      const sudokuInputs = [];

      function buildSudoku() {
        sudokuGridEl.innerHTML = "";
        for (let i = 0; i < 81; i++) {
          const cell = document.createElement("input");
          cell.type = "text";
          cell.inputMode = "numeric";
          cell.maxLength = 1;
          cell.className = "sudoku-cell";

          const row = Math.floor(i / 9);
          const col = i % 9;
          if (row === 2 || row === 5) {
            cell.classList.add("bold-bottom");
          }
          if (col === 2 || col === 5) {
            cell.classList.add("bold-right");
          }

          const value = sudokuPuzzle[i];
          if (value !== "0") {
            cell.value = value;
            cell.disabled = true;
          } else {
            cell.addEventListener("input", () => {
              const v = cell.value.replace(/[^1-9]/g, "");
              cell.value = v.slice(0, 1);
            });
          }

          sudokuGridEl.appendChild(cell);
          sudokuInputs.push(cell);
        }
      }

      sudokuCheckBtn.addEventListener("click", () => {
        sudokuStatusEl.classList.remove("status--error", "status--success");
        sudokuStatusEl.textContent = "";

        let allFilled = true;
        let correct = true;
        for (let i = 0; i < 81; i++) {
          const expected = sudokuSolution[i];
          const cell = sudokuInputs[i];
          const value = cell.value.trim();
          if (value === "") {
            allFilled = false;
          }
          if (value !== expected) {
            correct = false;
          }
        }

        if (!allFilled) {
          sudokuStatusEl.classList.add("status--error");
          sudokuStatusEl.textContent = "Fill every cell before checking.";
          return;
        }

        if (!correct) {
          sudokuStatusEl.classList.add("status--error");
          sudokuStatusEl.textContent = "Something is off. Adjust a few numbers and try again.";
          return;
        }

        sudokuStatusEl.classList.add("status--success");
        sudokuStatusEl.textContent =
          "Perfect Sudoku! You solved this level. The Brainy Riddle is now unlocked.";
        game2Complete = true;
        sudokuCheckBtn.disabled = true;
        // Reveal Riddle in the navigation
        navRiddle.style.display = "flex";
      });

      buildSudoku();

      // Game 3: Cartoon match quest + Location name
      const riddleStatusEl = document.getElementById("riddle-status");
      const riddleCheckBtn = document.getElementById("riddle-check-btn");
      const locationSection = document.getElementById("location-section");
      const locateBtn = document.getElementById("locate-btn");
      const locationStatusEl = document.getElementById("location-status");
      const locationOutputEl = document.getElementById("location-output");
      const match1El = document.getElementById("match-1");
      const match2El = document.getElementById("match-2");
      const match3El = document.getElementById("match-3");

      riddleCheckBtn.addEventListener("click", function () {
        riddleStatusEl.classList.remove("status--error", "status--success");
        riddleStatusEl.textContent = "";

        const v1 = match1El ? match1El.value : "";
        const v2 = match2El ? match2El.value : "";
        const v3 = match3El ? match3El.value : "";
        if (!v1 || !v2 || !v3) {
          riddleStatusEl.classList.add("status--error");
          riddleStatusEl.textContent = "Choose an item for every character.";
          return;
        }

        const correct = v1 === "srk" && v2 === "ranbir" && v3 === "vikrant";
        if (!correct) {
          riddleStatusEl.classList.add("status--error");
          riddleStatusEl.textContent = "Not quite. Try different matches!";
          return;
        }

        riddleStatusEl.classList.add("status--success");
        riddleStatusEl.textContent =
          "Perfect! You’ve completed all three games. Now you can reveal your location name.";
        game3Complete = true;
        locationSection.style.display = "block";
      });

      function copyToClipboard(text) {
        if (navigator.clipboard && navigator.clipboard.writeText) {
          return navigator.clipboard.writeText(text);
        }
        const textarea = document.createElement("textarea");
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        try {
          document.execCommand("copy");
        } finally {
          document.body.removeChild(textarea);
        }
        return Promise.resolve();
      }

      locateBtn.addEventListener("click", function () {
        locationStatusEl.classList.remove("status--error", "status--success");
        locationStatusEl.textContent = "";
        locationOutputEl.style.display = "none";

        if (!game3Complete) {
          locationStatusEl.classList.add("status--error");
          locationStatusEl.textContent =
            "Finish all three games, including the riddle, before sharing your location.";
          return;
        }

        // No geolocation required: always reveal fixed location name.
        const name = "Sage & Lavender";
        locationStatusEl.classList.add("status--success");
        locationStatusEl.textContent = "Location name revealed.";

        locationOutputEl.style.display = "block";
        locationOutputEl.innerHTML =
          "<div><strong>Your location:</strong></div>" +
          "<div style='margin-top:4px;'>Sage &amp; Lavender</div>";

        const copyBtn = document.createElement("button");
        copyBtn.textContent = "Copy location name";
        copyBtn.className = "copy-btn";
        copyBtn.addEventListener("click", function () {
          copyToClipboard(name).then(
            function () {
              copyBtn.textContent = "Copied!";
              setTimeout(function () {
                copyBtn.textContent = "Copy location name";
              }, 1500);
            },
            function () {
              copyBtn.textContent = "Copy failed";
              setTimeout(function () {
                copyBtn.textContent = "Copy location name";
              }, 2000);
            }
          );
        });
        locationOutputEl.appendChild(copyBtn);
      });
    })();
  </script>
</body>
</html>


