# 🏏 Scoreboard — Live Cricket Broadcast & Scorer

**Score the match ball-by-ball on your phone. Everyone else watches a real-time broadcast scoreboard, Worm & Manhattan charts, and full scorecards on theirs.**

Zero app installs. Zero backend servers to maintain. Secret-safe deployment via GitHub Actions + Firebase Realtime Database.

## ✨ What Makes Scoreboard Stand Out

### 1. Real Ball-by-Ball Cricket Engine

* **Complete Delivery Telemetry:** Logs runs off the bat (`0, 1, 2, 3, 4, 6`), extras (`Wide`, `No Ball`, `Bye`, `Leg Bye`), and wickets with fielder attribution.

* **Automated Cricket Laws:**

  * Automatic strike rotation on odd runs and at the end of every 6-ball legal over.

  * Wides and No Balls accurately handle extra running byes and bat-on-no-ball boundaries.

  * **Free Hit enforcement:** Every No Ball triggers a live Free Hit banner on the next delivery and protects the batter from standard bowler dismissals (while keeping Run Out active).

  * **Bowler Quota & Consecutive Over Guards:** Enforces per-format bowler limits (`2` overs in T10, `4` in T20, `10` in ODI) and prevents any bowler from bowling consecutive overs.

  * **Full Multi-Step Undo Stack:** Reverts deliveries, wickets, over transitions, strike swaps, and innings completions cleanly.

### 2. Interactive Pause & Command Menu (`⏸ Menu`)

* **Live Match Pause & Broadcast Status:** Pause the match for *Drinks Break*, *Rain Delay*, *Innings Break*, *Tactical Timeout*, or *Umpire Review* — instantly displaying a live status banner to all connected viewers.

* **Quick Navigation & Tactical Actions:**

  * Jump between **Home (Connect Hub)**, **Live Scorer Console**, **Scoreboard & Analytics**, and **Team Roster Setup**.

  * **Manual Strike Swap**, **Mid-Over Bowler Change**, **Retire Hurt / Impact Substitute**, and **Declare / Conclude Innings**.

  * **Export HD Scorecard Poster (PNG)** & **JSON Match Backup**.

  * Optional **Stadium Audio Feedback** (Web Audio API boundary & wicket chimes).

### 3. Broadcast-Grade Scoreboard & Interactive Score Graph

* **3-Mode Interactive Graph Suite:**

  * **Worm Chart (Cumulative Runs):** Dual-innings trajectory comparison with plotted wicket markers (`W`), target line, and projected score.

  * **Manhattan Chart (Runs Per Over):** Side-by-side over-by-over bar comparison with wicket indicators.

  * **Run Rate Wave (CRR Progression):** Momentum tracker across every over.

* **Interactive Over Inspector:** Tap or hover any over on the chart to inspect exact runs, wickets, bowler, and cumulative score at that point in the match.

* **Phase & Partnership Analytics:** Powerplay / Middle / Death overs breakdown, boundary distribution, and partnership progress bars.

### 4. Verified Match Code & Role Security

* **Viewer Match Code Validation:** Checks if a match code actually exists before joining and displays a clear error alert if an invalid or inactive code is entered.

* **SHA-256 Scorer Password Protection:** Only the scorer with the match password can log or modify deliveries; viewers get read-only live updates via a 5-character code or QR scan.


## 📁 Repository Structure

```
Cric-scorer-main/
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions workflow injecting Firebase secrets at build time
├── favicon.svg             # Vector cricket emblem favicon
├── index.html              # Self-contained Live Scorer, Viewer, Analytics & Pause Menu app
├── privacy.html            # Privacy Policy page
├── terms.html              # Terms and Conditions page
└── README.md               # Documentation & setup guide

```

## 🚀 Deploying with GitHub Secrets

1. Create a Firebase project with **Realtime Database** and **Anonymous Authentication** enabled.

2. In your GitHub repository, navigate to **Settings → Secrets and variables → Actions** and add:

   * `FIREBASE_API_KEY`

   * `FIREBASE_AUTH_DOMAIN`

   * `FIREBASE_DATABASE_URL`

   * `FIREBASE_PROJECT_ID`

   * `FIREBASE_STORAGE_BUCKET`

   * `FIREBASE_MESSAGING_SENDER_ID`

   * `FIREBASE_APP_ID`

   * `FIREBASE_MEASUREMENT_ID`

3. Push to the `main` branch (or trigger **Deploy to GitHub Pages** manually in the Actions tab). `.github/workflows/deploy.yml` injects your credentials safely into the build artifact and publishes to GitHub Pages.