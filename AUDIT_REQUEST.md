# Meta8 Showdown V2 - Audit Request

## Goal

Please audit Meta8 Showdown V2 as a playable web game and Firebase-backed app.

I want a practical audit focused on bugs, exploit risks, scoring problems, unclear rules, Firestore security issues, and anything that could make the game feel unfair, broken, or easy to manipulate.

## Provided Materials

- Main game code: `index.html`
- Firebase hosting config: `firebase.json`
- Firestore security rules: `firestore.rules`
- Firestore schema/index screenshots: included in this repo/thread
- Live playable link: ADD_LIVE_FIREBASE_LINK_HERE

## What To Review

### 1. Gameplay Logic

Check whether the game behaves correctly during normal play.

Look for:
- broken win/loss/tie states
- scoring bugs
- timer bugs
- stuck screens
- invalid game states
- duplicate actions
- refresh/reload exploits
- mobile vs desktop behavior differences

### 2. Scoring And Fairness

Check whether players can cheat or manipulate results.

Look for:
- score values controlled only by the browser
- players able to edit score, streaks, rolls, match results, or rewards
- leaderboard manipulation
- duplicate submissions
- replaying old game events
- forcing wins/losses in PvP
- fake pack purchases or fake reward claims

### 3. Firestore Rules / Security

Review `firestore.rules` against the game code.

Look for:
- overly broad reads/writes
- users able to write to other users' documents
- users able to edit protected fields
- unsafe public writes
- admin-only collections exposed to players
- leaderboard, match, config, purchase, and tournament collections being client-writable when they should not be

High-risk collections include:
- `config`
- `lw_scores`
- `lwRolls`
- `pvp_matches`
- `pvp_queue`
- `packPurchases`
- `playerProfiles`
- `users`
- `tournaments`
- `adminMessages`

### 4. Firebase / Data Model

Use the schema/index screenshots to understand the database shape.

Check whether the code and rules line up with these collections:
- `adminMessages`
- `collections`
- `config`
- `ladderRuns`
- `live_wire_rooms`
- `lw_lottery`
- `lw_lottery_broadcast`
- `lw_scores`
- `lw_stats`
- `lwRolls`
- `matchEvents`
- `meta`
- `packPurchases`
- `playerProfiles`
- `pvp_matches`
- `pvp_queue`
- `riders`
- `rooms`
- `sessions`
- `stats`
- `testerFeedback`
- `tournaments`
- `users`
- `winStreakRuns`

### 5. UX / Clarity

Check whether a new player can understand the game from the current UI.

Look for:
- unclear How to Play text
- missing scoring explanation
- confusing buttons
- unclear results
- weak error messages
- bad mobile layout
- places where the UI lets players do something invalid

### 6. Code Quality

Review the HTML/JS/CSS for maintainability and reliability.

Look for:
- duplicate logic
- fragile state handling
- hidden bugs
- console errors
- async/Firebase race conditions
- poor error handling
- hardcoded values that should be config
- unused or dead code

## Expected Output

Please return:

1. Top issues ranked by severity: Critical, High, Medium, Low
2. Exact file/line references where possible
3. Why each issue matters
4. Suggested fix for each issue
5. Any Firestore rule changes recommended
6. Any missing game-rule or UI clarification
7. Final verdict:
   - Ready for testing
   - Needs polish
   - Needs major fixes before wider release

## Important Notes

Do not assume the client/browser is trusted.

If score, match results, purchases, rewards, rolls, streaks, or leaderboard placement can be changed from browser-side code without server validation, flag it.

If a collection is public-writable and affects gameplay, ranking, rewards, admin messages, config, or purchases, treat that as high-risk.
