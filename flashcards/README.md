# Real Estate Exam Cards

Flashcards, study lists and multiple-choice tests for the real estate salesperson license exam. It runs in any browser on a Mac, PC, iPhone or Android phone, with no account and nothing to install.

**Starting deck:** 238 terms in 10 topics: Real Property & the Law, Ownership & Interests, Land Use & Government, Valuation & Appraisal, Financing, Contracts, Agency & Listings, Title, Deeds & Closing, Fair Housing & Leasing, and Real Estate Math.

## Features

- **Study:** tap a card to flip between term and definition, then mark it **Got it** or **Still learning**. Missed cards come back later in the round. Swipe on phones; Space and arrow keys on a computer.
- **Browse:** search every term and definition across all topics (or narrow to the selected topic or list), and tap one to study it.
- **Lists:** build your own study lists (for example, one per course unit) and study just those words.
- **Tests:** a 4-choice multiple-choice test for any list, with a score, a review of missed terms and a "retest the ones I missed" option.
- **Add cards:** add your own terms to any topic.
- **Real-world examples:** after flipping a card, search Google for the term in context.

## Use it

Open the GitHub Pages link for this repository (see below). On iPhone, tap **Share → Add to Home Screen** to use it like an app.

Progress, lists and added cards are saved **in that browser on that device**. They don't sync between devices, and clearing the browser's website data erases them.

> Open the app from its web address. Double-clicking `index.html` on your computer won't load the cards, because browsers block reading the data file that way.

## Put it online with GitHub Pages

1. In this repository, go to **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**, pick the **main** branch and the **/ (root)** folder, and click **Save**.
3. After a minute or two, the page shows your site's address, for example `https://<your-username>.github.io/real-estate-exam-cards/`.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app in one file: HTML, CSS and JavaScript, no build step |
| `data/re-exam-cards-data.json` | The card deck: topics, terms and definitions |
| `SPEC.md` | Full specification, for rebuilding the app with any AI assistant |

## Edit the cards

Change terms and definitions in `data/re-exam-cards-data.json` and commit; the app picks them up on the next load. Give every new card an id that isn't used anywhere else in the file, and never reuse or renumber an id: progress and lists point at card ids.

## Build your own version

`SPEC.md` describes every screen and rule. Give it and the data file to an AI assistant (Claude, ChatGPT or a coding tool) and paste the prompt at the top of the spec. A version built as a Claude artifact also gets syncing between devices and AI-written real-world examples.

## Disclaimer

Study aid only. Not affiliated with any state real estate commission or exam provider. Definitions are AI-generated for general exam study and may differ in wording from your course or your state's law. Check your state's licensing materials for state-specific rules.
