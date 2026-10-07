# Marketing Puzzle

Two files go in your GitHub repository:
- `index.html`: the complete game (your Firebase settings go at the top)
- `database.rules.json`: security rules you paste into Firebase (it doesn't need to be on GitHub, but keeping it there is handy)

## 1. Create the database
1. Go to https://console.firebase.google.com and click **Create a project** (Google Analytics is optional).
2. Left menu: **Build → Realtime Database → Create database**. Choose a location and start in **locked mode**.
3. Open the **Rules** tab, delete what's there, paste the contents of `database.rules.json`, and click **Publish**.
4. Open the **Data** tab and copy the URL at the top (it ends in `firebaseio.com` or `firebasedatabase.app`).

## 2. Get your web config
1. Click the gear icon → **Project settings** → **General**.
2. Under **Your apps**, click the web icon `</>`, enter a nickname, and click **Register app** (leave Hosting unticked).
3. Copy the values from the `firebaseConfig` it shows.

## 3. Paste into index.html
Open `index.html` and find the **FIREBASE + CLASS SETTINGS** block near the bottom of the file, just above the game code. Replace each placeholder:
```js
firebase: {
  apiKey:            "AIza...",
  authDomain:        "my-class.firebaseapp.com",
  databaseURL:       "https://my-class-default-rtdb.firebaseio.com",   // from step 1.4
  projectId:         "my-class",
  storageBucket:     "my-class.appspot.com",
  messagingSenderId: "1234567890",
  appId:             "1:1234567890:web:abc123"
},
groups: ["Class A", "Class B"],
```
If Firebase's config doesn't include `databaseURL`, add it yourself from step 1.4. This is the most common cause of a leaderboard that won't save.

## 4. Publish on GitHub Pages
1. Create a repository on GitHub and upload `index.html` (top level, not in a folder).
2. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → **Save**.
3. After a minute or two the game is live at `https://<username>.github.io/<repo>/`. Share that link.

## Checking it works
- The top bar should say **Live leaderboard** with a green dot.
- Finish one game; the results screen should say **Score saved to the live leaderboard**.
- Open the link on a second device — the score should appear there within seconds.
- If something is wrong, the message at the bottom of the leaderboard explains what to fix.

## Teacher tips
- **Reset scores:** Firebase → Realtime Database → Data → hover `scores` → delete icon. Or change `scoresPath` (e.g. `"scores-term2"`) for a fresh board that keeps old results.
- **Security:** students can only add new scores — they can't edit or delete scores, and impossible scores are rejected. The web config isn't secret; the rules are what protect the data.
- Open the game from the GitHub Pages link, not by double-clicking the file.
