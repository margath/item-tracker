# Changelog

All notable changes to this project will be documented in this file.

## [v2.0.0] - 2026-03-22
**The Campaign Manager Upgrade**

This major release transforms the Item Tracker from a simple inventory list into a robust Virtual Tabletop (VTT) campaign suite, completely overhauling the database schema, UI, and tabletop mechanics.

### 🚀 Major Features
* **New Card Archetypes:** Added the ability to spawn specific card types from a new CSS dropdown menu:
  * **Standard Items:** Weapons, armor, standard gear.
  * **Treasure & Wealth:** Dedicated tracker for PP, GP, EP, SP, CP, and Gems/Art objects.
  * **Transcription Supplies:** Tracks spellbook transcription materials by "Spell Level" charges.
  * **Note Cards:** Giant text boxes for lore, clues, and campaign notes.
  * **Quest Cards (DM Only):** Campaign objectives that pin to the top of the board and collapse into sleek table rows.
* **The Ultimate Sorting Engine:** Board visually sorts by strict hierarchy: Quests > Items > Wealth > Notes.
* **Spreadsheet View:** Added a toggleable "Table View" to display the entire party inventory as a dense, sortable data table.
* **Physical Print Mode:** Added a "Print Selected" toggle. Hides the UI, strips dark mode, and forces Standard cards to print at exactly 2.5 x 3.5 inches so they fit into standard playing card sleeves.
* **Party Wealth Summary:** DMs can now click "Party Wealth" to aggregate every coin and gem across all players into a single GP-equivalent value.

### 🛠️ Mechanics & Tabletop Improvements
* **Advanced Encumbrance & Storage Locations:** Replaced simple "Equipped" toggles with specific storage locations (Backpack, Belt, Bandolier, Pouch, Hidden, Equipped/Worn). 
* **Tactical Weight Tracking:** The Encumbrance calculator now isolates "Combat Weight" (Belt/Bandolier/Equipped) from "Backpack Weight".
* **Coin Weight Math:** The Encumbrance calculator automatically applies D&D coin weight rules (50 coins = 1 lb) based on player wealth cards.
* **Rarity & DC Auto-Suggestions:** Added item rarities (Mundane through Artifact). The app now automatically suggests standard Identify/Curse DCs when a rarity is selected.
* **Quantity & Charge Tracking:** Added dedicated inputs for Current Qty and Max Qty, complete with +/- counter buttons directly on the card face.

### ✨ UI/UX Polish
* **No More Alerts:** Completely purged native browser `alert()`, `prompt()`, and `confirm()` dialogs.
* **Toast Notifications:** Built a smooth, unobtrusive pop-up notification system for system messages.
* **2-Step Confirmations:** Deleting or discarding cards now requires a timed 2-step click ("Are you sure?") to prevent accidental data loss.
* **Smart Clipboard Reading:** The "Setup" menu now automatically checks your clipboard and pastes your Apps Script URL if it detects one.
* **Typing Focus Fix:** Decoupled input fields from the rendering engine. The app now silently saves in the background without stealing your cursor focus while typing.
* **Smart Live-Sync Pause:** Background sync automatically pauses if it detects a user actively typing in an input field.
* **Dynamic Naming:** Treasure cards now display as "Personal Wealth" to the owner, but "[Character Name] Wealth" to other players and the DM.

### 🪲 Bug Fixes & Stability
* **Database Version Safety Net:** The app now cross-references its version with the Google Apps Script. If the database schema is outdated, it safely locks the screen and forces an upgrade, preventing silent data corruption.
* **Encumbrance Calculator Crash:** Fixed a silent Javascript panic caused by legacy items lacking the new JSON wealth data format.
* **Cryptography Number Crash:** Fixed a bug where numeric fields (like Identify DCs) would crash the AES encryption engine. Values are now strictly forced to Strings.
* **Apps Script Header Bug:** Fixed a flaw in the Google Apps Script where it would fail to read players if the spreadsheet didn't have a rigid header row.

### 🏗️ DevOps & Backend
* **Live GitHub Linking:** Ripped out the fragile file-editing `sed` commands in the GitHub Action. The app now fetches the latest commit and release tags dynamically via the GitHub API.
* **Safe GitHub Actions:** Updated the workflow to use `awk` with safe `// --- BUILD INFO ---` markers for local builds, and added `git ls-remote` checks to prevent workflow retry crashes when tags already exist.
