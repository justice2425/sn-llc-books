# LLC Books: a Standard Notes plugin for single-member LLC bookkeeping

LLC Books is an editor plugin for Standard Notes. Open a note with it and the note becomes a
cash-basis ledger: income, expenses grouped by IRS Schedule C line, owner contributions and
draws, estimated tax payments, and a mileage log, with year-end reports for you or your CPA.

It organizes records. It does not calculate tax, and it is not a substitute for a CPA.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole plugin: layout, styles, and logic |
| `component-relay.js` | Standard Notes' official library for talking to the app (v2.2.2, AGPL-3.0) |
| `ext.json` | The descriptor Standard Notes reads when you install the plugin |
| `COMPONENT-RELAY-LICENSE.txt` | License for `component-relay.js` |

## Try it before installing

Open `index.html` directly in a browser. It runs in demo mode and keeps data in that browser
only. Use this to get a feel for it; demo data does not move into Standard Notes.

## Host it (GitHub Pages)

Standard Notes installs custom plugins from a URL, so these files must be on a web host.

1. Create a GitHub repository named `sn-llc-books`. GitHub Pages on a free account needs the
   repository to be public. Only this code is public; your ledger data never goes to GitHub.
2. Upload the four files above to the repository root.
3. Edit `ext.json` and replace `YOUR-USERNAME` in all three places with your GitHub username.
4. In the repository, open Settings, then Pages. Under "Build and deployment", choose
   "Deploy from a branch", branch `main`, folder `/ (root)`, and save.
5. After a minute, check that `https://YOUR-USERNAME.github.io/sn-llc-books/index.html` loads
   in demo mode, and that `.../ext.json` shows your edited file.

Any static host works the same way. If you use another host, put its URL in `ext.json`.

## Install in Standard Notes

1. Open Preferences, then Plugins.
2. Find "Install Custom Plugin", paste the URL of your `ext.json`, and install.
3. Create a new note, for example "LLC Books 2027".
4. Change the note's editor (note type) to "LLC Books".

The exact menu wording may differ by app version.

## How data is stored

- The ledger is saved as JSON in the note's text, so it is encrypted and synced by Standard
  Notes like any other note. One note holds all years; use the Tax year selector to switch.
- If you open the note in the plain text editor you will see the JSON. Do not edit it by hand.
- If you switch an existing note with text in it to LLC Books, the plugin asks before replacing
  anything and keeps the old text under Settings.
- Use Settings, "Export full backup (JSON)" monthly, and keep the file with your tax records.
  Use "Export selected year as CSV" to hand a year to your CPA or open it in a spreadsheet.
- If a download button does nothing (some app versions block downloads from plugins), use the
  "Show to copy" buttons and paste the text into a file.

## Using it

- **Ledger.** Enter each deposit and each payment once, on the date money moved (cash basis).
  Amounts are always positive; the type decides whether it is money in or out.
- **Owner / non-deductible.** Money you put in or take out, estimated tax payments, health
  insurance, and retirement contributions go here. They are not business income or expenses.
- **Reports.** Profit and loss by Schedule C line, calendar quarters, income by payer (to check
  against 1099s), contract labor by payee (to spot 1099-NEC filings), and the owner account.
  The California LLC fee watch compares total income with the $250,000 threshold.
- **Mileage.** Log business trips. Enter the IRS standard mileage rate for the year in Settings
  to see the deduction. Use either this or actual car costs, not both.
- **Settings.** Business name, tax reserve percentage, mileage rate, deductible share of meals
  (default 50%), contractor threshold (default $2,000), and LLC fee threshold. These are your
  inputs; confirm them with your CPA each year.

## What it does not do

- No tax computation, no depreciation schedules, no home office calculation.
- No invoicing, bank feeds, or receipt storage. Put the receipt file name in the Ref field.
- No double-entry balance sheet. It tracks cash in, cash out, and owner activity, which is what
  Schedule C and California Form 568 for a small disregarded LLC draw on. If you later elect
  S corporation status or take on inventory, employees, or loans, move to full accounting
  software.

## Privacy and security

- The plugin makes no network requests and loads no outside fonts, scripts, or analytics.
- A Standard Notes plugin can read the note it is editing. Install it only from a URL you
  control, and keep control of that repository, because whoever can change the hosted files
  can change what the plugin does.

## Tested and not tested

Tested in headless Chrome against a mock of the Standard Notes plugin protocol: loading,
saving, editing, deleting, locked notes, adopting a note with existing text, reports math,
CSV output, and a phone-width layout.

Not tested: the real Standard Notes desktop, web, or mobile apps. I also could not confirm
whether your Standard Notes plan allows custom plugins, or how the mobile app handles them.
Try it with a throwaway note first.

## Changing it

To add or rename a category, edit the `CATS` list near the top of the script in `index.html`.
Keep each `id` stable once you have entries using it. Schedule C line numbers follow recent
versions of the form; check them against the form for the year you file.

Because `component-relay.js` is AGPL-3.0, keep the source available if you share the plugin
with others.
