# Real Estate Exam Cards — App Specification

Updated Nov 6, 2026

## How to use this spec

Give this document and the companion data file to any AI coding assistant, and it can build its own copy of the app. The data file, **re-exam-cards-data.json**, holds all 238 cards in 10 topics, so the new app starts with the full deck and nobody retypes definitions.

**Data file:** re-exam-cards-data.json (238 cards, 10 topics, updated Nov 4, 2026) is shared alongside this spec, in this repository at [data/re-exam-cards-data.json](data/re-exam-cards-data.json).

1. Download this file (SPEC.md) and the data file.
2. Open your AI assistant (Claude, ChatGPT, or a coding tool) and attach both files.
3. Paste the prompt below and send it.
4. Open the app it builds in a browser on your Mac and iPhone. On iPhone, use Share → Add to Home Screen.

Prompt to paste:

> Build the web app described in the attached specification, "Real Estate Exam Cards." Load the attached file re-exam-cards-data.json as the starting deck. Follow every feature and behavior rule in the spec, and use the "Build notes" section to choose storage and AI options for your platform. If you are Claude, publish it as an artifact with the db, user and sample capabilities. When done, tell me which features, if any, you could not include.

## Overview & goals

Real Estate Exam Cards is a single-page flashcard web app for studying the real estate salesperson license exam. A term sits on one side of each card and its definition on the other.

- **Audience:** one student, possibly a few study partners. No admin or teacher roles.
- **Platforms:** runs in Safari or Chrome on a Mac and on an iPhone. Must work at phone width (about 390px) and be usable as a Home Screen web app.
- **Starting content:** 238 cards in 10 topics, all in the data file. Lists start empty; each student makes their own.
- **Sync:** study progress and lists should be the same on every device the student signs in on. If the platform can't sync, saving per device is an acceptable fallback.

Core principles:

- Fast to study: one tap flips a card, one tap scores it.
- Nothing is lost: progress saves automatically with no Save button.
- Works without AI: AI examples are an add-on. Every other feature runs without an AI service.
- Plain language: buttons say exactly what they do ("Got it", "Still learning", "Add to list").

## Data model

The app stores five kinds of records. Card ids are stable strings and are the glue between everything: progress, lists and examples all point at card ids, so every id must be unique across all topics and never reused or renumbered.

| Record | Shared or private | Fields | Notes |
| --- | --- | --- | --- |
| Topic (deck) | Shared | id, name, order, cards\[\] of {id, term, def} | Built-in deck, loaded from the data file. One record per topic. |
| Custom card | Shared | id, topic (topic id), term, def, createdAt | Cards the student adds. Can be deleted. Built-in cards cannot. |
| List | Shared (or per person, see Build notes) | id, name, cardIds\[\], createdAt, lastTest {correct, total, at} | Ordered set of card ids. lastTest is set only by a full-list test. |
| Example | Shared | id (= card id), text, term, createdAt | One saved AI example per card; a new one replaces the old. |
| Progress | Private per person | cards: map of card id → "learning" or "known", updatedAt | A card missing from the map is "new". One record per person. |

Data file format (re-exam-cards-data.json):

```
{
  "topics": [ { "id": "realprop", "name": "Real Property & the Law", "order": 0,
                "cards": [ { "id": "realprop-01", "term": "Accession", "def": "..." } ] } ],
  "lists":  []
}
```

On first run, import the topics from the file if the store is empty. Never re-import over existing data.

## Screens & features

The app has one page with four tabs (Study, Browse, Lists, Add card) and one full-page Test view. Above the tabs' content sit a progress meter and a row of topic chips.

### Header, meter and topic chips

- Title "Real Estate Exam Cards" and the four tabs.
- **Progress meter** for the selected topic or list: "Name · N% mastered", counts of mastered / learning / new, and a three-color bar.
- **Chip row** (scrolls sideways on phones): "All topics", each topic, then a divider and each saved list tagged "List". Each chip shows mastered/total, e.g. "Contracts 4/20". Tapping a chip selects it and starts a new shuffled round.
- Meter and chips are hidden during a test.

### Study tab

- Toggles: **Skip mastered cards** and **Show definition first** (swaps the faces). Link: **Shuffle & restart**. When a round was opened from Browse, a **← Back to Browse** link also shows.
- **Card:** front shows topic name, a status pill (New / Learning / Mastered), the term, a counter "12 / 140" and "Tap to see definition". Tapping flips it with a 3D turn to the definition.
- Under the card: **+ Add to list** and "In: List A, List B" for lists that hold this card.
- Answer buttons: **← Back** (previous card, no scoring), **Still learning**, **Got it**.
- Shortcuts: Space flips; ← = Still learning; → = Got it. On phones: tap flips, swipe left = Still learning, swipe right = Got it.
- **Round complete** screen: count got / missed, buttons **Study the N I missed**, **New round**, and when a list is selected, **Take a test**.

### Real-world example panel

Shown below the answer buttons only after the card is flipped, so it never gives the answer away.

- **Show a real-world example:** asks an AI for a 3–4 sentence realistic scenario plus an "Exam tip:" line. Text streams in, then is saved and reused for that card.
- **Try another example** replaces the saved one.
- **Search Google ↗** opens a new tab searching "\<term> real estate example".

### Browse tab

- Search box filtering term and definition text across all topics by default. When a topic or list is selected, an "Only show \<name>" checkbox narrows results to it. Results sorted A–Z with a count that names the scope ("2 cards match in all topics").
- Each row: term, definition, **+ List** button, status pill (tap cycles New → Learning → Mastered → New), and **Delete** on custom cards only (two taps: Delete, then Confirm delete).
- Tapping a term or definition opens Study at that card; the rest of the round follows the current search results in order.

### Add-to-list panel

Opens from "+ Add to list" (Study) or "+ List" (Browse). A bottom sheet on phones, a centered dialog on desktop.

- Shows the term, a **List** dropdown and **+ New list…** as the last option. Lists that already hold the card are disabled and labeled "(already added)".
- Default selection = the last list the student added a word to. No lists yet = New list with a name field.
- "Already in:" chips; tapping one removes the card from that list.
- Buttons: Cancel, Add (or "Create list & add"). Esc or tapping outside closes it.

### Lists tab

- Create a list by name.
- One card per list: name, term count, mastered count, "all memorized" when every card is mastered, last test score (e.g. "last test 9/12 (75%)"), and a mastery bar.
- Buttons: **Study** (selects the list in Study), **Test**, **Delete list** (two taps). Deleting a list never deletes cards or progress.
- **Show terms** expands the terms with status pills and a **Remove** button each.

### Test view

- Header: list name, "Question 3 of 12 · 2 correct", progress bar.
- The term, then four definitions labeled A–D. Exactly one is correct.
- After an answer: correct choice green, wrong pick amber, others dimmed, "Correct." or "Not quite. The answer is D.", then **Next question** (or **See results**). Keys: 1–4 or A–D to answer, Enter for next.
- Results: "N of M correct", score %, the missed terms with definitions, and buttons **Retest the N I missed**, **Retake test**, **Done**.

### Add card tab

Form with Topic (dropdown), Term (max 120 characters) and Definition (max 800). Saving adds a custom card and confirms with "Added to \<topic>".

## Behavior rules

These rules define how the app decides what to show. Build them exactly; they are what make studying effective.

### Card status

- Three states: **New** (never scored), **Learning**, **Mastered** (stored as "known").
- "Got it" sets Mastered. "Still learning" sets Learning. A wrong test answer sets Learning. A right test answer changes nothing.
- Status is per person and shared across that person's devices.

### Study round (queue)

1. Take the cards in the selected topic, list or "All topics".
2. If "Skip mastered cards" is on, drop Mastered cards.
3. Shuffle (Fisher–Yates).
4. On "Still learning", re-insert that card 5 positions later (or at the end). Each card is re-inserted at most once per round, so a round always ends.
5. The round ends when the queue is used up; show the Round complete screen.

If the selection is empty, show a clear message: "Every card here is mastered" (with a Review all cards button), "This list is empty", or "No cards in this topic".

### Test question generation

No AI is needed for tests. For each card in the list, in shuffled order:

1. The correct answer is the card's own definition.
2. Pick 3 distractors from the other cards' definitions: same topic first (shuffled), then any topic. Skip any definition identical to the correct one or to a distractor already picked.
3. Shuffle the 4 options and label them A–D.

A full-list test saves lastTest on the list. A "Retest the N I missed" test does not.

### AI example prompt

Send this, filled in, using a fast, low-cost model:

> You help someone study for a US real estate salesperson licensing exam. Term: {term}. Definition: {def}. Write one concrete, realistic scenario in 3 to 4 sentences that shows this term in an actual property situation or transaction. Use made-up first names and specific details such as prices, places, or dates. Then, on a new line starting with "Exam tip:", give one short sentence on how the exam typically tests this term or what it is commonly confused with. Plain text only. No markdown, no headings, no bullet points.

Render the "Exam tip:" line as a highlighted callout. On failure, show a plain message ("Couldn't write an example right now. Try again.") and keep the Google button working.

### Saving and sync

- Save progress automatically after each answer, batching rapid answers (about 0.7 seconds) into one write. Only one write in flight at a time.
- Listen for changes so another device's progress, lists and examples appear without reloading.
- Remember per device: selected topic or list, the two toggles, and the last list used.
- Loading: show "Loading your cards…". After 10 seconds without data, show "Can't reach your cards yet" and keep retrying.
- Errors are short and say what to do, e.g. "Couldn't update the list. Try again." Never use browser alert or confirm dialogs; confirmations happen in the page (two-tap delete).

## Design

The look is a clean index card on a faint blueprint grid, like a plat map. Matching it exactly is optional; the layout and behavior matter more.

- **Layout:** one centered column, max width 680px, side padding at least 16px (respect iPhone safe areas). Nothing scrolls sideways except the chip row.
- **Card:** white, 14px rounded corners, soft shadow, at least 300px tall (340px on phones). Term in a bold sans serif, 24–34px; definition in a readable serif, 17–20px.
- **Phones:** answer buttons become two columns with Back on its own row; the add-to-list panel slides up from the bottom.
- **Dark mode:** follow the device setting. Every color has a light and dark value.
- **Motion:** card flip about 0.45s; turn animations off when the device asks for reduced motion.
- **Accessibility:** visible keyboard focus, buttons labeled in words, status shown by text as well as color.

| Role | Light | Dark |
| --- | --- | --- |
| Background (with faint grid) | #E9EEF2 | #0E141A |
| Card / surface | #FFFFFF | #17212B |
| Text | #15202B | #E5EBF0 |
| Muted text | #5A6876 | #92A0AD |
| Lines | #D3DBE2 | #2A3743 |
| Accent (blueprint blue) | #1E5A85 | #7AB2DE |
| Mastered / correct | #24754A | #63C48E |
| Learning / wrong | #9A5B0C | #E7AE55 |

Fonts (Google Fonts): Archivo for headings and terms, Source Serif 4 for definitions, IBM Plex Mono for counts and labels.

## Build notes

Pick the row that matches where the app will run. On Claude, every feature works with no setup; elsewhere, sync and AI examples need extra services.

| Platform | Storage & sync | AI examples | Setup needed |
| --- | --- | --- | --- |
| Claude (claude.ai artifact) | Artifact database (db capability); progress under each person's private data/users/\<id> path; user capability for the id | sample capability, quick model tier; asks the viewer once for permission | None. Seed topics from the data file after the first publish |
| Plain web app, one device | Browser localStorage (or IndexedDB), wrapped in try/catch | Optional; hide the AI button if no key | None. Progress stays on that one browser |
| Web app with sync | A hosted database with sign-in, e.g. Supabase or Firebase | Call an AI API (e.g. Anthropic) from a small server function, never with the key in the page | Database project, sign-in, API key, hosting (e.g. Netlify or Vercel) |

Notes for any platform:

- **Single file is fine.** The original is one HTML page with inline CSS and JavaScript and no framework.
- **Lists per person (optional change):** the original shares lists among everyone who opens the app. For a shared study group, store lists under each person's private data instead, like progress.
- **AI is optional.** If no AI service is set up, show only the Search Google button in the example panel. Everything else still works.
- **Embedding Google is not possible.** Google blocks being shown inside other pages, so the search always opens a new tab.
- **Keep card ids** from the data file unchanged, so lists and progress stay linked.

## Acceptance checklist

The build is done when every box below can be ticked on both a Mac and an iPhone.

- [ ] App opens showing 10 topics and 238 cards, with no lists until the student makes one
- [ ] Tapping a card flips it; Space flips on the Mac; swipes score on the iPhone
- [ ] Got it / Still learning update the status pill, meter and chip counts
- [ ] A "Still learning" card returns later in the same round, once
- [ ] Skip mastered cards and Show definition first both work and are remembered
- [ ] Example panel appears only after flipping; Google opens a new tab
- [ ] AI example streams in, is saved, and shows instantly next time (if AI is set up)
- [ ] Browse search filters; tapping a term opens it in Study; Back to Browse keeps the search
- [ ] Add to list defaults to the last list used, can create a new list, and can remove from a list
- [ ] Lists tab can create, study, test, remove terms and delete lists (two taps)
- [ ] Test shows 4 options with one correct, scores correctly, marks misses as Learning, and saves the last score
- [ ] Custom cards can be added and deleted; built-in cards cannot be deleted
- [ ] Progress made on one device appears on the other (sync builds only)
- [ ] Works at 390px wide in light and dark mode with no sideways scrolling
