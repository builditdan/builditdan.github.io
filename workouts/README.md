# Workouts

Workout lists with photos, instructions and video links, built for trainers, massage therapists and anyone following a routine. Make a list per routine or per client, then share it as a single web page that opens on any phone. It runs in any browser on a Mac, PC, iPhone or Android phone, with no account and nothing to install.

**Starting list:** "My workout", 4 exercises with YouTube links (no photos, so you can add your own): TRX Lat Workout, Landmine row, Dumbell Step and Belt Squat Machine.

## Features

- **Lists:** make as many as you need, for example "Leg day" or "Sarah – Week 1". Rename or delete them (deleting takes two taps).
- **Exercises:** a name, a description (sets, reps, cues), an optional photo, and up to two links to YouTube, Vimeo, Instagram or any website. Reorder with **Move up** and **Move down**.
- **Follow along:** numbered exercises, **Previous** and **Next** buttons, and tap a photo to see it full screen.
- **Share:** turn any list into one `.html` page with the photos built in. Send it from your phone's share menu or save it and attach it to a text or email. The person receiving it needs no app or account, and every video link is a tappable button.
- **Back up and restore:** download all your lists as one file and load them on another device or browser.

## Use it

Open the GitHub Pages link for this repository (see below). On iPhone, tap **Share → Add to Home Screen** to use it like an app.

Lists and photos are saved **in that browser on that device**. They don't sync between devices, and clearing the browser's website data erases them, so use **Back up lists** now and then. Browsers allow about 5 MB, which fits roughly 30 to 60 photos; the app warns you before it runs out.

> Open the app from its web address. Double-clicking `index.html` on your computer opens the app, but it won't load the starting list, because browsers block reading the data file that way.

## Put it online with GitHub Pages

1. Create a **public** repository on GitHub (for example `workouts`) and upload `index.html`, `README.md`, `SPEC.md` and the `data` folder. In the browser: **Add file → Upload files**, drag them in, then **Commit changes**.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**, pick the **main** branch and the **/ (root)** folder, and click **Save**.
4. After a minute or two, the page shows your site's address, for example `https://<your-username>.github.io/workouts/`.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app in one file: HTML, CSS and JavaScript, no build step |
| `data/workouts-data.json` | The starting lists: exercises, descriptions and links |
| `SPEC.md` | Full specification, for rebuilding the app with any AI assistant |

## Edit the starting lists

The easiest way: open the app, change the lists, tap **Back up lists**, and replace `data/workouts-data.json` with the backup file (rename it to `workouts-data.json`). The backup and the data file use the same format.

The starting lists load only the first time the app opens in a browser. Anyone who has already opened it keeps their own lists; they can load the new file with **Restore from backup**.

To start empty instead, set `"lists": []` in the data file.

## Build your own version

`SPEC.md` describes every screen and rule. Give it and the data file to an AI assistant (Claude, ChatGPT or a coding tool) and paste the prompt at the top of the spec. A version built as a Claude artifact also saves photos online and keeps the lists the same on every device you open it on.

## Disclaimer

Exercise descriptions and links are for general guidance. Check with a qualified trainer or health professional before starting a new exercise program.
