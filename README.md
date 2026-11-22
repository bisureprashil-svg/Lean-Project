# Lean Plan

Fat-loss and muscle tracker. One HTML page that runs on GitHub Pages and syncs to your own Firebase. It includes:
- the meal plan
- a daily log
- two progress photos a day
- the training plan
- a progress chart
- a weekly check-in that adjusts calories
- a weekly dietitian review through Claude

## 1. Firebase (about 10 minutes)

1. Go to https://console.firebase.google.com and click **Add project**. Name it `lean-plan`. Analytics can be off.
2. Turn on sign-in: **Build → Authentication → Get started → Sign-in method → Email/Password → Enable → Save**.
3. Create the database: **Build → Firestore Database → Create database**. Choose a location close to you, e.g. `us-west1 (Oregon)`, and start in **production mode**.
4. Lock it down: **Firestore Database → Rules**. Replace everything with the contents of `firestore.rules`, then click **Publish**.
5. Get the web config: **Project settings (gear) → General → Your apps → Web (`</>`)**. Register an app named `Lean Plan` (no hosting needed), then copy the `firebaseConfig` block.

Photos are stored compressed (about 150–250 KB each) in Firestore. You don't need Firebase Storage, so everything runs on the free Spark plan.

## 2. GitHub Pages

1. Create a new repository `lean-plan` and upload every file in this folder.
2. Edit `firebase-config.js` in GitHub. Replace `null` with your config (see the example in the file) and commit. Every device will then connect automatically.
3. Go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, then branch `main`, folder `/ (root)`, and click **Save**.
4. After about a minute the app is live at `https://bisureprashil-svg.github.io/lean-plan/`.
5. Back in Firebase, go to **Authentication → Settings → Authorized domains → Add domain** and add `bisureprashil-svg.github.io`.

## 3. iPhone

1. Open the link in **Safari**. Tap **Create account** with your email and a password.
2. Tap **Share → Add to Home Screen**. It now opens full-screen with its own icon.
3. Photos: tap **Add photo**. iPhone offers **Take Photo** or **Photo Library**.

## Moving data from the Claude version

In the old app go to **Settings → Copy data**. In this app go to **Settings → Restore from text** and paste. This moves the log only, not photos.

## Notes

- Your data lives at `users/<your uid>/…` and only your signed-in account can read it.
- The page works offline once loaded and syncs when you're back online.
- No Firebase yet? Tap **Use on this device only**. Data and photos stay in that browser.
