# Class score history: setup

The quiz can save each finished attempt (name, difficulty, score, total, percentage, mastery band and finish time) to a Google Sheet that you own, and show the recent attempts to the class. Individual answers are never sent. Setup takes about ten minutes and needs only a Google account.

## 1. Create the Google Sheet

1. Go to sheets.google.com and sign in with the Google account that should own the class history.
2. Click **Blank spreadsheet**.
3. Click the title **Untitled spreadsheet** (top left) and rename it, for example `ISR Quiz Class History`.

You do not need to create any tabs or headers. The script creates a sheet named **History** with its header row the first time a score is saved.

## 2. Add the script

1. In the spreadsheet menu, click **Extensions > Apps Script**. A new browser tab opens with a file named `Code.gs`.
2. Select everything in `Code.gs` and delete it.
3. Open `apps-script/Code.gs` from this repository, copy its entire contents, and paste them into the editor.
4. Click the **Save project** icon (the floppy disk), or press Ctrl+S (Cmd+S on a Mac).
5. Optional: click **Untitled project** at the top and rename it, for example `ISR Quiz History`.

## 3. Deploy it as a web app

1. Click the blue **Deploy** button (top right), then **New deployment**.
2. Next to **Select type**, click the gear icon and choose **Web app**.
3. Fill in the form:
   - **Description**: `Class history` (any text).
   - **Execute as**: **Me** (your email address).
   - **Who has access**: **Anyone**.
4. Click **Deploy**.
5. Google asks you to authorise the script the first time:
   1. Click **Authorize access** and choose your Google account.
   2. If you see "Google hasn't verified this app", click **Advanced**, then **Go to ISR Quiz History (unsafe)**. This warning appears for every personal script; the script is the one you just pasted and only touches this spreadsheet.
   3. Click **Allow**.
6. Under **Web app**, copy the **URL**. It looks like `script.google.com/macros/s/AKfy.../exec` with `https://` in front and must end in `/exec`.
7. Click **Done**.

Quick check: paste the URL into a new browser tab and add `?mode=all&limit=5` to the end. You should see `{"ok":true,"rows":[]}`.

## 4. Connect the quiz

1. Open `src/template.html` in this repository.
2. Near the top of the app script, find the configuration block:

   ```js
   var HISTORY_ENDPOINT = '';
   ```

3. Paste the `/exec` URL between the quotes, keeping the quotes:

   ```js
   var HISTORY_ENDPOINT = 'PASTE-YOUR-EXEC-URL-HERE';
   ```

4. Rebuild and test:

   ```sh
   node scripts/build.mjs && node scripts/verify.mjs
   ```

   The tests never contact your sheet; they use a fake network.
5. Commit and push:

   ```sh
   git add src/template.html index.html
   git commit -m "config: connect class score history"
   git push
   ```

6. After GitHub Pages redeploys (usually within a minute or two), open the quiz. The **Class score history** section on the start page should say that no attempts have been recorded yet. Finish one attempt to confirm a row appears in the **History** sheet.

## Updating the script later

If you change `Code.gs`, keep the same URL by editing the existing deployment instead of creating a new one: **Deploy > Manage deployments**, click the pencil icon, set **Version** to **New version**, and click **Deploy**.

## Privacy and housekeeping

- The web app is public: anyone with the `/exec` URL (which is visible in the quiz page source) can read the recent names and scores and could add rows. Ask students to use a first name or a class username rather than a full name if that matters for your class.
- Only the fields listed at the top are stored. Answers stay in the student's browser.
- To remove entries, delete rows in the **History** sheet. To reset the class, delete every row below the header.
- To switch history off, set `HISTORY_ENDPOINT` back to `''`, rebuild, commit and push. To stop the sheet accepting data at all, use **Deploy > Manage deployments > Archive**.
