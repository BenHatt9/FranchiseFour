[README.md](https://github.com/user-attachments/files/32495226/README.md)
# Franchise Four: put your fantasy league online for free

This folder is a complete website. `index.html` is the whole app. It runs on
GitHub Pages (free) and stores shared league data in Firebase (free plan), so
anyone with your invite link can join. No paid plan and no Claude account are
needed for your friends.

You need: a free Google account (for Firebase) and a free GitHub account.
Plan for about 15 minutes the first time.

## 1. Create the Firebase project

1. Go to https://console.firebase.google.com and click **Create a project**.
   Name it anything (for example `franchise-four`). You can turn Google
   Analytics off.
2. Stay on the free **Spark** plan. You never need to add a card.

## 2. Turn on the database and sign-in

1. **Build > Firestore Database > Create database.** Choose **production mode**
   and a region near you (this can't be changed later).
2. Open the **Rules** tab, delete what's there, paste the entire contents of
   `firestore.rules` from this folder, and click **Publish**.
3. **Build > Authentication > Get started > Sign-in method.** Enable
   **Anonymous**. (Optional: also enable **Google**, which lets people reach
   their seat from a second device.)
4. **Authentication > Settings > Authorized domains:** add
   `YOUR-GITHUB-USERNAME.github.io`.

## 3. Add your keys to the site

1. In Firebase, click the gear icon > **Project settings** > **Your apps** and
   add a **Web app** (the `</>` icon). Skip hosting.
2. Copy the `firebaseConfig` values it shows you.
3. Open `index.html` in any text editor. Near the top, replace the four
   `PASTE_...` values in the `window.FIREBASE_CONFIG` block. Save.

These keys are safe to publish. They only identify your project; the security
rules you published in step 2 are what protect your data.

## 4. Publish on GitHub Pages

1. On https://github.com click **New repository**. Name it (for example
   `fantasy`), make it **Public**, and create it.
2. Click **Add file > Upload files**, drag in `index.html`, and commit.
3. **Settings > Pages.** Under **Build and deployment**, set **Source** to
   **Deploy from a branch**, branch **main**, folder **/ (root)**, and Save.
4. After a minute your site is live at
   `https://YOUR-GITHUB-USERNAME.github.io/fantasy/`.

## 5. Start your league

1. Open your site and click **Create a new league**.
2. Enter a league name and your name. You are now the **commissioner**: only
   you can change settings and scoring, start the draft, enter stats and
   finalize weeks.
3. Click **Invite** (top right), copy the link, and send it to your managers.
   Each person opens the link, enters their name and a team name, and joins.

The invite link looks like `https://YOUR-USERNAME.github.io/fantasy/?l=abc123`.
Each league has its own link, so you can run several leagues from one site.

## Good to know

- **Seats are tied to a browser.** Managers are signed in anonymously, so if
  someone switches phone to laptop they'd appear as a new person. The
  **Keep my seat on other devices** button (in the Invite box) links their seat
  to a Google account. It only works if you enabled Google sign-in in step 2.
- **Trust level.** Draft picks, trades and chat can be written by any signed-in
  person who has the link. That's fine for friends, but don't post the link
  publicly. Settings, stats and results are locked to the commissioner by the
  rules.
- **Cost.** The free plan allows about 50,000 reads and 20,000 writes a day,
  far more than a friend league uses. Nothing is charged on the Spark plan.
- **Testing the rules.** In Firestore's Rules tab, use the **Rules Playground**
  to try a write as a signed-in user who isn't the commissioner, for example to
  `leagues/abc/stats/w1`. It should be denied.
- **Updating the site.** To change anything later, edit `index.html` in your
  GitHub repository and commit. Data stays in Firebase.
- **Team logos** the managers upload are stored as small images inside the
  league data, so no extra storage service is needed.
