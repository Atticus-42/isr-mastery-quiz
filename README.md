# ISR Operations Mastery Quiz

A free, browser-based practice aid for the *Introduction to ISR Operations* lesson. Students take a 25-question Easy, Medium, or Hard examination at https://atticus-42.github.io/isr-mastery-quiz/ after entering their name and confirming that this mock exam does not replace studying the complete lesson.

Questions use only the substantive slides 21-58 of the supplied presentation. Instructor profile, classroom rules, safety, objectives, check-on-learning prompts and administration slides are excluded. Scenarios are fictional Philippine Army situations grounded in those slides.

No login, payment, analytics, cookies, advertising, external fonts, images, scripts or runtime libraries. Answers stay in browser memory and are never sent anywhere. Sound cues are synthesised in the browser with the Web Audio API and can be switched off.

## Class score history

When `HISTORY_ENDPOINT` is set in `src/template.html`, each finished attempt sends the student's name, difficulty, score, total, percentage, mastery band and finish time to a Google Sheet owned by the instructor, and the start page shows the class's recent attempts. That URL is the only network address the page contacts. Leave it empty (`''`) to switch history off. Setup: [`apps-script/SETUP.md`](apps-script/SETUP.md); the sheet-side code is [`apps-script/Code.gs`](apps-script/Code.gs).

## Building

`src/questions/` holds the three banks, `src/template.html` is the page source, and `scripts/build.mjs` produces the self-contained `index.html`. Test gate (no network access; the history endpoint is faked):

```sh
node scripts/build.mjs && node scripts/verify.mjs
```
