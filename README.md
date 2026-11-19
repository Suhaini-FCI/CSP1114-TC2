# Class Quiz Live (Firebase version, for 200+ students)

A free Kahoot-style live quiz. The teacher hosts, students join from their phones with a 5-digit code. Game data goes through Google’s Firebase servers, so it does not depend on the teacher’s computer handling every student’s connection.

Files:
- `index.html`: the whole app
- `firebase-config.js`: your Firebase settings (you fill this in)
- `firestore.rules`: security rules (you paste these into Firebase)

## Part 1: Set up Firebase (free, no credit card, about 10 minutes)

1. Go to https://console.firebase.google.com and sign in with a Google account.
2. **Add project**, give it a name (e.g. `class-quiz`), and turn Google Analytics off.
3. **Build → Firestore Database → Create database.** Choose a location close to you (e.g. `asia-southeast1` Singapore) and start in **production mode**.
4. Open the **Rules** tab, delete everything there, paste the contents of `firestore.rules`, and click **Publish**.
5. **Build → Authentication → Get started → Sign-in method → Anonymous → Enable → Save.** (Students never see a login. This only gives each phone a private ID so nobody can fake another player’s answers.)
6. Click the gear icon → **Project settings**. Under **Your apps**, click the web icon `</>`, register an app (skip Firebase Hosting), and copy the `firebaseConfig` values.
7. Open `firebase-config.js` and replace the four `PASTE_...` values with yours. Keep it on the **Spark (free)** plan. These values are not secret; the rules protect your data.

## Part 2: Put it online with GitHub Pages

1. Create a free GitHub account and a new **public** repository (e.g. `class-quiz`).
2. Upload `index.html`, `firebase-config.js` and this README.
3. **Settings → Pages → Deploy from a branch → `main` → `/ (root)` → Save.**
4. After a minute your site is live at `https://YOUR-USERNAME.github.io/class-quiz/`.

If the page says it could not sign in, go to Firebase **Authentication → Settings → Authorized domains** and add `YOUR-USERNAME.github.io`.

## Running a game

**Teacher:** open the site, tap **host a game**, paste your questions, then **Create game**. Show the 5-digit code on the projector. When students have joined, press **Start quiz**.

Question format (first line is the question, `*` marks the correct answer, blank line between questions):

```
What is the capital of Malaysia?
*Kuala Lumpur
Penang
Johor Bahru
Kuching

Which planet is the Red Planet?
Venus
*Mars
Jupiter
```

**Students:** open the site, enter the code and a nickname. Faster correct answers earn more points (500 to 1000).

## Free plan limits (important for 200 students)

The free Spark plan has daily caps: 50,000 reads and 20,000 writes per day for the whole project. When a cap is hit, the app stops working until the daily reset.

Rough estimate for a 20-question game with 200 students: about 4,300 writes and 12,500 reads. That is around **3 to 4 full-size games per day**. Smaller classes or fewer questions use proportionally less. You can see your usage under Firebase **Firestore → Usage**.

Other notes:
- Firebase’s own free Realtime Database is capped at 100 simultaneous connections, which is why this app uses Firestore instead.
- Keep the teacher’s tab open during the game. If it closes mid-game, restart with a new game code.
- Run a small test with 2 to 3 phones before your first real class.
