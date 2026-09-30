# ISR Operations Mastery Quiz

A free, browser-based practice aid for the *Introduction to ISR Operations* lesson. Students take a 25-question Easy, Medium, or Hard examination at https://atticus-42.github.io/isr-mastery-quiz/ after confirming that this mock exam does not replace studying the complete lesson.

Questions use only the substantive slides 21-58 of the supplied presentation. Instructor profile, classroom rules, safety, objectives, check-on-learning prompts and administration slides are excluded. Scenarios are fictional Philippine Army situations grounded in those slides.

No login, payment, analytics, cookies, advertising, external fonts, images, scripts or runtime libraries. Answers and scores stay in browser memory.

`src/questions/` holds the three banks, `src/template.html` is the page source, and `scripts/build.mjs` produces the self-contained `index.html`. Test gate:

```sh
node scripts/build.mjs && node scripts/verify.mjs
```
