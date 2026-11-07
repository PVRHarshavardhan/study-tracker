# Study Tracker: installable app for phone and laptop

Study hours, tasks and subtasks, habits, a Pomodoro timer and reports with green/red status (day → week → month → quarter → year → overall goal).

- **Install:** people install it from your link (like an app) on Android, iPhone and laptops.
- **Sign-in:** everyone signs in with their own Gmail.
- **Data:** each person's data lives in a private Google Sheet in **their own Google Drive** and syncs across their devices.
- **Offline:** the app works offline and syncs when the internet is back.
- **Cost:** free. You need a GitHub account (free, for hosting) and a Google Cloud project (free, for the Gmail sign-in key).

---

## Owner setup (one time, about 20 minutes)

### Step 1: Put the app online (GitHub Pages, free)
1. Go to **github.com** and create a **New repository** named `study-tracker`. Set it to **Public**.
2. Click **Add file → Upload files**. Drag in **everything in this folder**: `index.html`, `config.js`, `manifest.webmanifest`, `sw.js`, the `icons` folder and this README. Click **Commit**.
3. Go to **Settings → Pages**. Under Source, choose **Deploy from a branch**, pick `main` and `/ (root)`, then click **Save**.
4. After about a minute your app link appears, for example `https://YOUR-GITHUB-NAME.github.io/study-tracker/`.

### Step 2: Create the Google sign-in key (free)
1. Open **console.cloud.google.com** and create a **New project** called "Study Tracker".
2. Go to **APIs & Services → Library** and **Enable** both **Google Drive API** and **Google Sheets API**.
3. Go to **Google Auth Platform** (shown as "OAuth consent screen" in some console versions) and click **Get started**.
   - App name: `Study Tracker`. Add your email. Audience: **External**.
   - In **Data access**, add the scope `.../auth/drive.file` ("See, edit, create and delete only the specific Google Drive files you use with this app").
   - In **Audience**, click **Publish app**. This makes the app available to everyone, not only test users. Because the app only asks for access to its own files (a non-sensitive permission), Google normally doesn't require a review.
4. Go to **Clients → Create client**.
   - Type: **Web application**.
   - **Authorized JavaScript origins**: `https://YOUR-GITHUB-NAME.github.io`. Use the domain only, with no `/study-tracker`.
   - Click Create and **copy the Client ID** (it ends in `.apps.googleusercontent.com`).

### Step 3: Connect them
1. In GitHub, open `config.js`, click ✏️ Edit, and replace `PASTE_YOUR_CLIENT_ID.apps.googleusercontent.com` with your Client ID. Commit.
2. Open your app link and sign in. Done.

---

## Installing (you and anyone you share the link with)
| Device | How |
|---|---|
| Android | Open the link in **Chrome**, then tap **Install app** (or ⋮ menu → *Install app*) |
| iPhone / iPad | Open the link in **Safari**, tap **Share**, then **Add to Home Screen** |
| Laptop (Windows/Mac) | Open in **Chrome or Edge** and click the **install icon** in the address bar |

Then **Sign in with Google**. The first time, you choose your own plan: exam type, goal date, hours for each weekday, subjects and habits. Sign in with the **same Gmail** on your phone and laptop and both show the same data.

If sign-in doesn't open inside the iPhone home-screen app, use the link in Safari instead. Your data is the same either way.

---

## Releasing an improved version
1. Replace the changed files in GitHub.
2. In `sw.js`, change `VERSION` (for example `v4.0.0` → `v4.1.0`). Commit.
3. Installed apps show **"A new version is ready → Update now"**.

Updates never delete anyone's data, because the data lives in each user's own Google Sheet.

## Where is my data?
Google Drive → **"Study Tracker — Your name"**. It has these tabs: Settings, Plans (your weekly hour plans with history), DayOverrides, Tasks, Sessions and HabitLog. To get an Excel copy, open the sheet and go to **File → Download → Microsoft Excel**.

## Optional: Play Store / App Store later
- **Google Play:** go to **pwabuilder.com**, enter your app link and choose **Package for stores → Android**. A Google Play developer account costs **$25 one-time**.
- **Apple App Store:** needs an Apple Developer account at **$99 per year**. Until then, iPhone users install the app with *Add to Home Screen*.
