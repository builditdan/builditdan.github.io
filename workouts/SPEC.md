# Workouts — App Specification

Updated Nov 6, 2026

## How to use this spec

Give this document and the companion data file to any AI coding assistant, and it can build its own copy of the app. The data file, **workouts-data.json**, holds the starting list ("My workout", 4 exercises with video links and no photos), so the new app opens with real content.

**Data file:** workouts-data.json (1 list, 4 exercises, updated Nov 6, 2026) is shared alongside this spec, in this repository at [data/workouts-data.json](data/workouts-data.json).

1. Download this file (SPEC.md) and the data file.
2. Open your AI assistant (Claude, ChatGPT, or a coding tool) and attach both files.
3. Paste the prompt below and send it.
4. Open the app it builds in a browser on your Mac and iPhone. On iPhone, use Share → Add to Home Screen.

Prompt to paste:

> Build the web app described in the attached specification, "Workouts." Load the attached file workouts-data.json as the starting lists. Follow every feature and behavior rule in the spec, and use the "Build notes" section to choose storage and sharing options for your platform. If you are Claude, publish it as an artifact with the db, assets and downloads capabilities. When done, tell me which features, if any, you could not include.

## Overview & goals

Workouts is a single-page web app for building workout lists and sharing them. Trainers, massage therapists and physical therapists often send clients loose YouTube links by email or text. This app turns those into a clean, numbered list with a photo, instructions and video buttons for each exercise, sent as one web page the client opens on any phone.

- **Audience:** a trainer or therapist building lists for clients, or one person building their own routine. Clients only receive shared pages; they never need the app.
- **Platforms:** runs in Safari or Chrome on a Mac and on an iPhone. Must work at phone width (about 390px) and be usable as a Home Screen web app.
- **Starting content:** one list from the data file. Users add their own lists.
- **Storage:** lists and photos save automatically. Syncing between devices is a nice-to-have; saving per device with backup and restore is an acceptable fallback.

Core principles:

- Fast to build: a list with five exercises takes a few minutes.
- Easy to receive: shared pages need no app, account or internet connection once opened (except to play videos).
- Nothing is lost: changes save immediately with no Save-all button, and there is always a backup path.
- Plain language: buttons say exactly what they do ("Add exercise", "Move up", "Save the web page").

## Data model

| Record | Fields | Notes |
| --- | --- | --- |
| List | id, name, items\[\] | Ordered. Name is required, max 80 characters. |
| Exercise (item) | id, name, desc, links\[\], imgData *or* imgId | Lives inside its list, in order. Name required (max 120). desc optional (max 4000, line breaks kept). links: 0–2 URLs. |

- **Ids** use lowercase letters and digits only (e.g. `Date.now().toString(36)` plus 4 random base-36 characters) because they appear in the page address. Ids are unique across all lists.
- **Photos:** `imgData` is a JPEG data URL, resized so the longest side is at most 1000px, quality 0.8. A platform with file storage can instead store the file and keep its id in `imgId`.
- **Links:** only `http` and `https`. If the user leaves off the scheme, add `https://`. The host must contain a dot.

Data file format (workouts-data.json), which is also the backup format:

```
{
  "app": "Workouts",
  "format_version": 2,
  "lists": [ { "id": "main", "name": "My workout",
               "items": [ { "id": "mvwjuxvu6lkg", "name": "TRX Lat Workout", "desc": "",
                            "links": ["https://youtube.com/shorts/..."],
                            "imgData": "data:image/jpeg;base64,..." } ] } ]
}
```

Migration: an older format stored a plain array of exercises. Treat an array as one list, `{ id: "main", name: "My workout", items: <array> }`.

On first run, import the lists from the data file if nothing has been saved yet. Never re-import over existing data, including when the user has deleted every list.

## Screens & features

The app is one page. The page address (hash) decides which screen shows, so the browser Back button works:

| Address | Screen |
| --- | --- |
| *(none)* | Home |
| `#newlist`, `#editlist-<listId>` | List form (new / rename) |
| `#l-<listId>` | List |
| `#new-<listId>`, `#edit-<itemId>` | Exercise form (new / edit) |
| `#ex-<itemId>` | Exercise detail |

Unknown addresses show Home. On every screen change, scroll to the top and move keyboard focus to the screen title.

### Home

- Large title "Workouts" and a count ("3 lists" / "No lists yet").
- One row per list: list name, exercise count, and a square thumbnail of the list's first photo if it has one.
- Empty state: "Make a list for each routine or client, then add exercises to it."
- Backup section: a note that lists are saved in this browser on this device, then **Back up lists** (disabled with no lists) and **Restore from backup**.
- Fixed bottom bar: **New list**.

### List

- "‹ All lists" back link, the list name as the title, exercise count.
- Numbered rows: number badge, exercise name, a two-line description preview, link count ("2 links"), photo thumbnail on the right. Tapping a row opens the exercise.
- Empty state: "Add the first exercise: a name, how to do it, a photo, and up to two video links."
- **Rename list** and **Delete list** (two taps; deleting removes its exercises).
- Fixed bottom bar: **Share** (only when the list has exercises) and **Add exercise**.

### Exercise detail

- "‹ \<list name>" back link, "Exercise 2 of 5", the name as a very large title.
- Photo in a bordered frame. Tapping it opens a full-screen dark view with a **Close** button; tapping anywhere or Esc also closes it.
- Description with line breaks kept, or "No description." in muted italics.
- "Links": one large button per link, showing a friendly label (YouTube video, Vimeo video, Instagram post, TikTok video, or the website's name) and the address underneath. Opens in a new tab.
- **Previous** / **Next** showing the neighbouring exercise names.
- **Edit**, **Move up**, **Move down** (disabled at the ends), **Delete** (two taps).

### Exercise form

- Name, Image (Choose image; once chosen, a square preview with **Change image** and **Remove**), Description (hint: "how to do it, sets, reps"), Link 1, Link 2.
- Buttons: **Add exercise** or **Save changes**, and **Cancel**. Enter in a text field saves.

### List form

- One field, "List name", hint "a routine like “Leg day”, or a client’s name". Buttons: **Create list** or **Save**, and **Cancel**. Creating a list opens it.

### Share sheet

Opens from **Share** on a list. A bottom sheet titled “Share “\<list name>””:

- **Send the web page:** shown only when the device can share files (`navigator.canShare({ files })`). Opens the phone's share menu with the page attached, ready for Messages or Mail.
- **Save the web page:** downloads `<list-name>.html`.
- **Close.** Esc or tapping outside also closes it.

## Behavior rules

### The shared page

- One self-contained `.html` file: inline CSS, photos embedded as data URLs, no scripts, no outside files except an optional web font with a fallback.
- Content: the list name as the title, an exercise count, a numbered overview of exercise names, then one section per exercise with its number, name, photo, description and link buttons.
- The overview is plain text, **not** jump links: phone file previewers often ignore in-page links, which confused testers.
- Same colors and fonts as the app, light and dark mode.
- Do not offer "text the list" or "email the list" as plain message text. It was tried and removed: the page with tappable buttons is the reliable way to send it.

### Saving

- Save immediately after every change (create, edit, reorder, delete).
- If storage is full, don't apply the change and show: "Storage is full. Remove some images or back up and delete old lists, then try again."
- Resize photos before saving (see Data model).

### Deleting and confirming

- Deleting a list or exercise takes two taps: the button changes to "Tap again to delete" (or "Tap again to delete list") for 4 seconds.
- Never use browser alert or confirm dialogs. Restoring a backup over existing lists shows an in-page box: "Replace your 2 lists with the 3 in this backup? This can’t be undone." with **Replace my lists** and **Cancel**.

### Backup and restore

- **Back up lists** downloads `workouts-backup-YYYY-MM-DD.json` in the data file format.
- **Restore from backup** reads a `.json` file, applies the migration, and rejects anything without lists ("That file isn’t a workout backup.").

### Messages

Short, and say what to do: "Give this exercise a name.", "That isn’t a web address. Try something like youtube.com/watch?v=abc", "That image couldn’t be opened. Try a JPG or PNG."

## Design

The look is a gym whiteboard: tall, condensed, heavy titles over a pale concrete background, with yellow number plates like bumper plates. Matching it exactly is optional; the layout and behavior matter more.

- **Layout:** one centered column, max width 640px, side padding 20px (respect iPhone safe areas). The bottom action bar stays fixed and clears the iPhone home indicator. Nothing scrolls sideways.
- **Type:** Archivo (Google Fonts) for everything. Titles and exercise names use the condensed width (`font-stretch: 62%`) at weight 800; body text is regular width at 17px.
- **Rows:** separated by thin lines under a thick top rule. Number badges are yellow plates with dark numbers.
- **Buttons:** at least 44px tall, 2px borders, 8px corners. One filled blue primary button per screen.
- **Dark mode:** follow the device setting. Every color has a light and dark value.
- **Motion:** minimal; none when the device asks for reduced motion.
- **Accessibility:** visible keyboard focus, buttons labeled in words, status messages announced to screen readers.

| Role | Light | Dark |
| --- | --- | --- |
| Background | #E9ECE6 | #12171D |
| Surface | #F8F9F5 | #1B222B |
| Text | #18222E | #E8ECEF |
| Muted text | #56616D | #9AA5B1 |
| Lines | #C6CCC3 | #2E3844 |
| Accent (links, primary button) | #2346D8 | #8AA2FF |
| Number plates | #F0BE1E | #E8B820 |
| Delete / errors | #B42318 | #FF8A80 |

## Build notes

Pick the row that matches where the app will run.

| Platform | Storage & sync | Photos | Sharing | Setup needed |
| --- | --- | --- | --- | --- |
| Claude (claude.ai artifact) | Artifact database (db capability), or the artifact capability with lists saved into the page itself; same lists on every device | assets capability (upload files, store `imgId`) | downloads capability to save the page; fetch photos and embed them when building the shared page | None. Load the data file's lists after the first publish |
| Plain web app, one device (this repository) | Browser localStorage, wrapped in try/catch | Data URLs inside the saved lists (about 5 MB total) | Blob download link, plus `navigator.share` with files where supported | None |
| Web app with sync | A hosted database with sign-in, e.g. Supabase or Firebase | The service's file storage | Optionally host each shared page at its own link | Database project, sign-in, hosting (e.g. Netlify or Vercel) |

Notes for any platform:

- **Single file is fine.** The original is one HTML page with inline CSS and JavaScript and no framework.
- **Links to phone apps may be blocked.** Inside some embedded views (such as a Claude artifact), `sms:` and `mailto:` links do nothing. Don't rely on them; use file sharing and downloads.
- **Video embeds aren't needed.** Link buttons open YouTube in a new tab, which works everywhere.
- **Keep ids** from the data file unchanged.

## Acceptance checklist

The build is done when every box below can be ticked on both a Mac and an iPhone.

- [ ] First open shows "My workout" with 4 exercises and links from the data file
- [ ] Deleting every list and reloading does not bring the starter list back
- [ ] Lists can be created, renamed and deleted (two taps)
- [ ] Exercises can be added, edited, moved up and down, and deleted (two taps)
- [ ] Photos can be chosen, changed and removed; tapping a photo shows it full screen
- [ ] Links without "https://" still work; a non-address shows the error message
- [ ] Previous and Next step through a list in order
- [ ] Back button returns to the previous screen
- [ ] Share saves a single .html file that opens offline with all photos and working video buttons
- [ ] On iPhone, Send the web page opens the share menu with the file attached
- [ ] Back up lists and Restore from backup round-trip every list, photo and link
- [ ] Restoring over existing lists asks in the page first; no browser pop-ups anywhere
- [ ] A full-storage error leaves existing lists untouched and shows the message
- [ ] Works at 390px wide in light and dark mode with no sideways scrolling
