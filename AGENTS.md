# AGENTS.md: for AI coding agents

You may build a game for kidvo, or help a person translate it (see [Translating](#translating)). Read `CONTRIBUTING.md` first: it is the charter, and it decides what gets merged.

## In short

- kidvo only merges small games that help children aged 7 to 13 use AI wisely while thinking for themselves.
- Games never call a real AI or the network. They use the practice-AI panel in `shell/ask-ai.js`, with answers written in the game, some deliberately wrong.
- Start from `templates/app/`. Study `apps/maze/` (Robot Maze), the reference game.
- Every text goes into `lang/en.js`. Add `lang/hu.js` and `lang/ro.js` only if you can write them well; a native-speaker steward reviews every language.
- Ship `parents/en.html`: one printable A4 page for parents and teachers.
- Make it work on phones: no sideways scrolling at 360 px, buttons at least 44 px tall on touch screens, playable in short landscape screens. `npm test` checks the first part.
- Touch nothing outside `apps/<your-id>/`. Run `npm test` until it passes.
- Open **one** pull request per GitHub account, titled `game: <id>: <what the child practises>`. Wait for review before sending another.

## Writing for children

- Explorers (7–9): sentences under 10 words, one idea each, no irony.
- Investigators (10–13): short paragraphs are fine; explain trade-offs.
- Never make the practice AI cute, flattering or friend-like. It is a tool.
- No scary content, no personal data prompts (except in a `keep-secrets` game, where saying no is the right answer), no brands or copyrighted characters.

## Translating

The open translations are the issues titled "Translate kidvo into …". Each one lists the steps, the files and the rules for that language. Follow it. You write the draft; the person who asked you speaks the language and decides every word.

- **One step of the issue per pull request.** A GitHub account may have one open pull request, so the next step waits until the last is merged. Update the fork from `main` before each step.
- **Step 1 first: the desktop texts in `shell/i18n.js`.** It is the only translation step that changes files outside `apps/`; the maintainer labels it `core`. It also puts the language in the top bar, so later steps can only be tried once it is merged. Every later step changes one game's folder and nothing else.
- **Translate the values, never the keys.** Keep the `{n}` placeholders, the plural endings (`_one`, `_other`, plus any the issue says the language needs), any HTML inside a text, and the machine names: ORACLE-3000, SORT-1, QUIZ-O-TRON, Sunny and Vo.
- **Wrong answers stay wrong.** Some practice-AI answers are wrong on purpose, so children can catch them. Translate them as confidently as the English; never correct them. If a true fact in Confident Nonsense is not true in the person's language or country, tell them rather than changing it.
- **Explorers' texts** (keys ending in `_explorers`) follow the rules in [Writing for children](#writing-for-children): under 10 words a sentence.
- **Let the person read it in the running site before any pull request.** Start it with `npm run dev`, open http://localhost:8080 and pick the language in the top bar. They read every screen of the step in both age bands (every game can change who is playing), and in a window about 360 px wide, because CI checks the width only in English. Fix what they ask, then run `npm test`.
- **Open the pull request only when they say the texts are right.** Title it `lang: <code>: <step>`, for example `lang: fr: robot maze`. In the description, write `Part of #<issue>` (not "Closes", which would close the whole issue after one step) and list what they read.

## Sandbox facts

Your game runs in `<iframe sandbox="allow-scripts">` with an opaque origin: no `localStorage` (use `kidvo.store`), no cookies, no popups, no forms that submit, no network beyond this repository's files. Canvas, SVG, CSS animation, Web Audio after a tap, and pointer or keyboard input all work.

Keep the content-policy `<meta>` first in `<head>`. SVG files may only draw (inline `<svg>` inside your HTML may do more), and parents' guides run no scripts. `npm run check` enforces all three.
