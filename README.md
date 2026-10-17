# Our Lovely Memories ❤️

Responsive Arabic romantic-memory website inspired by the provided screen recording. Built with HTML, CSS, Tailwind CDN, HTMX CDN, and vanilla JavaScript. Firebase integration is scaffolded for Authentication, Firestore, Storage, and Hosting.

## Files
- `index.html` — visitor experience: password gate, welcome screen, memory carousel, dates, quiz.
- `admin.html` — admin content editor for site settings, text, images, dates, and quiz questions.
- `firebase-config.js` — Firebase Web App configuration placeholders. Replace them with your project's config.
- `firestore.rules`, `storage.rules` — baseline rules; review before production.
- `firebase.json` — Firebase Hosting configuration.

## Preview locally
Open `index.html` directly for the visitor demo. Open `admin.html`, enter any email and a password of at least 4 characters to test the local editor. Local edits are stored in this browser using `localStorage`; local image uploads are limited to 2 MB because they're stored as data URLs in this prototype.

## Enable Firebase
1. Create a project at https://console.firebase.google.com/.
2. Register a Web App and copy its configuration into `firebase-config.js`.
3. Enable **Authentication → Email/Password**.
4. Create a **Cloud Firestore** database and enable **Storage**.
5. Create an admin user under Authentication. Then create a document in the `admins` collection whose document ID is that user's **UID**. The document can contain `{ "role": "admin" }`.
6. Publish `firestore.rules` and `storage.rules` from the Firebase console or with Firebase CLI.
7. Deploy with Firebase CLI: `npm install -g firebase-tools`, `firebase login`, `firebase init hosting firestore storage` (choose existing project and current directory), then `firebase deploy`.

## GitHub
Create a repository, then run:
```bash
git init
git add .
git commit -m "Create Our Lovely Memories website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

For GitHub Pages, note that `firebase-config.js` is public client-side configuration and must never contain service-account keys. Firebase security must be enforced by Firestore/Storage rules. Firebase Hosting is recommended if using the included Firebase rules and Storage.

## Important implementation note
The bundled experience runs in local-demo mode until Firebase is configured. After adding a real web-app config, the admin page uses Firebase Authentication, checks the signed-in user against `admins/{uid}`, loads and saves `siteContent/main` in Firestore, and uploads selected images to Firebase Storage. If config placeholders remain, it falls back to a local-only demo login; that fallback is intentionally not secure and must not be used as a production admin login. The visitor page reads `siteContent/main` from Firestore when Firebase is configured.
