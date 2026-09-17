# Slash Royale - Serverless Edition

A lightweight, zero-setup OBS Browser Source mini-game inspired by 80s slasher movies. Viewers type `!join` in chat to enter a 60-second lobby, then hide across a series of rooms while a randomly-cast killer hunts them down. Anyone caught doesn't make it to the next room. 

The last survivor faces the killer one-on-one in a Final Chase: a pure coin flip that decides whether they escape the night, or the killer wins outright.

**This "Serverless Fork" completely removes the need for a Python backend or configuration files.** Player stats and leaderboards are saved directly to your browser's local storage, and the target Twitch channel is configured dynamically via the URL. It also introduces interactive audience polling and custom grindhouse background art.

## What's in this version?

* **No Backend Required:** Drops `server.py` entirely. Leaderboards run purely on browser `localStorage`.
* **URL Configuration:** Simply append `?username=YourChannel` to the URL. No more editing JavaScript files.
* **Audience Polling:** Chat can use `!vote [name]` to predict who dies next, complete with end-of-round achievements ("Crystal Ball" and "Loudest Voice").
* **Custom Backgrounds:** Swaps plain CSS gradients for generated pixel-art backgrounds (The Cabin, The Cemetery, The Saw Mill, The Gas Station, etc.).

## 1. Setup & OBS Integration

Because this version has no backend, it is perfect for hosting on **GitHub Pages**, or you can run it straight from your hard drive. 

1. In OBS, add a **Browser Source**.
2. Point it to your `index.html` file (either check "Local file" or paste your GitHub Pages link).
3. **Crucial:** Append `?username=YOUR_TWITCH_NAME` to the end of the file path/URL.
   * *Local Example:* `file:///C:/path/to/game/index.html?username=PaladinArcade`
   * *Hosted Example:* `https://pasiegel.github.io/slash-royale-serverless-edition/?username=PaladinArcade`
4. Set the source size to **640 x 480**.
5. The background is already transparent—no chroma key needed.

*(Note: If you ever need to clear your cache in OBS, you will lose your all-time leaderboard stats since they are stored locally in the browser source's cache).*

## 2. How a Round Plays Out

- **Lobby:** 60-second countdown while players type `!join` (requires at least 2 players to start).
- **Tonight's Killer:** A random slasher-parody persona (featuring a funny name and a one-line backstory) is introduced before the hunt begins.
- **The Rooms:** Players hide across a rotating set of grimy, themed locations. 
- **Audience Polling:** Before the killer enters, the action pauses for 10 seconds. Chat uses `!vote [name]` to guess who is about to expire.
- **The Hunt:** The killer catches 1-2 players per room; survivors sprint to the next location.
- **Final Chase:** When exactly one player remains, it's a straight 50/50 coin flip. They either escape the night, or the killer catches them and wins the round outright. 
- **Case Files & Awards:** An evidence-board recap gives every caught player their own card with a dark-comedy epitaph. Finally, top audience voters and predictors are awarded.

## 3. Chat Commands

| Command | Who | Effect |
|---|---|---|
| `!join` | anyone | Joins the queue; opens the lobby if it's the first join of a cycle. |
| `!vote [name]`| anyone | Casts a prediction on who will die in the current room. Only active during the 10-second room countdown. |
| `!stats` | anyone | Shows the requester's own stats on screen for a few seconds (games played, wins/losses, total points). Only works when the game is idle. |
| `!resetslash` | broadcaster | Wipes all saved local storage stats to start fresh. |

## 4. Developer / Simulator Mode

Want to test the game offline without spamming your live chat? 

Open the game in a normal web browser and append `&dev=1` to the URL (or click the small **`dev`** button in the top-left corner). 

This unlocks a Dev Console panel on the right side of the screen with buttons to simulate `!join` commands, flood the lobby with random players, trigger audience votes, and run test rounds.