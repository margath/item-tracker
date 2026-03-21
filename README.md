# 🐉 Party Loot Tracker

A zero-hosting, single-file web application designed to track party inventory, encumbrance, and hidden magical secrets for D&D 5e/5.5e campaigns. 

Instead of relying on a paid database, this app uses a **Google Sheet** as its backend via Google Apps Script. It completely separates Player knowledge from Dungeon Master knowledge, ensuring that cursed items and unidentified magic stay completely secret until the DM decides to reveal them.

## ✨ Key Features

* **Serverless Backend:** All data is saved directly into beautifully formatted columns in a private Google Sheet. No hosting fees or database setups required.
* **Role-Based Access:** Players log in with a PIN to claim items, equip gear, and consume potions. The DM logs in to grant items, reveal true names, and manage the party.
* **Encrypted Secrets:** If an item is unidentified, its true name, magical description, and curses are encrypted *in the browser* before being saved to the cloud. Players peeking at the raw Google Sheet will only see ciphertext.
* **Hidden Curses:** The *Identify* spell doesn't reveal curses! DMs can input hidden curses and Identify DCs that remain entirely invisible to players until explicitly revealed.
* **Built-in SRD Library:** DMs can auto-fill standard D&D magic items (like Bags of Holding or Weapons +1) with a single click.
* **Consumables & Phantoms:** Track arrows, rations, and potions with quick `+` and `-` buttons. 
* **QR Code Joining:** DMs can generate a custom QR code or join-link directly from the app so players can connect instantly on their phones.

## 🎮 Trying the Demo

If you open the `index.html` file without a Google Sheet connected, it will automatically load a **Demo Mode** featuring the cast of the 1980s D&D Cartoon.

1. Open `index.html` in any web browser.
2. Click **👤 Log In**.
3. Log in as **Hank** (PIN: `1111`) to see the Player view. Try claiming items from the Party Stash or drinking a potion.
4. Log out, then log back in as **Dungeon Master** (PIN: `7777`) and click **🔒 Unlock DM View**. Notice how the "Glowing Red Scale" can now be edited, and its hidden curse is visible to you!

## 🚀 Setting Up Your Own Campaign

Ready to use this for your own table? You just need a free Google account.

1. **Create the Database:** Create a new [Google Sheet](https://sheets.new).
2. **Setup the Roster:** At the bottom left, add a new tab and name it exactly: `Players`. Starting in Row 2, add your group:
   * *Column A:* Player Name
   * *Column B:* Their 4-digit PIN
   * *Column C:* Character Name (Optional)
3. **Add the Code:** In the top menu of the Google Sheet, click **Extensions > Apps Script**.
4. Delete the default code and paste in the Apps Script code (you can copy this directly from the ⚙️ Setup menu inside the `index.html` app).
5. Click **Deploy > New deployment**. Select type **Web app**. 
6. Set *Execute as* to **Me**, and *Who has access* to **Anyone**. 
7. Click Deploy, authorize the permissions, and copy the generated **Web app URL**.
8. Open the `index.html` app, click **⚙️ Setup**, and paste your URL!

## 🛠️ Development & CI/CD

This repository utilizes Calendar Versioning (CalVer) via GitHub Actions. 

Whenever a commit is pushed to the `main` branch, the `.github/workflows/stamp.yml` action automatically wakes up, stamps the `index.html` file with the current date, run iteration, and commit hash (e.g., `🐙 2026.03.20.42`), and commits it back to the repository. 

If you fork this repository, the GitHub Action will automatically update the source code links in the app header to point to your new repository path!
