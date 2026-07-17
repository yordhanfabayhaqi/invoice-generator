# Sheet Invoice Generator (Google Apps Script)

Turn a Google Sheets tracker into one-click internal invoices. Tick a checkbox on a row, run the menu, and the script generates a formatted invoice (Google Doc → PDF) into a Drive folder, then writes the invoice number, dates, and PDF link back to the sheet.

## Features

- **Checkbox-gated generation** — only rows you tick get an invoice; rows that already have a link are skipped, so nothing is ever generated twice.
- **Auto invoice numbering** — sequential per month (`PREFIX/YYYY/MM/001`), stored safely in Script Properties with a lock, written back to the sheet.
- **Due-date calculation** — parses payment terms like `30 Days` from a cell and computes the deadline.
- **Digital signature block** — the signer's name rendered in a cursive font (mimicking a hand signature), followed by the name in a normal font and an optional employee ID. No more printing to sign.
- **Header-name column resolution** — columns are found by their header text, not position, so you can reorder your sheet freely.
- **Zero hardcoded config** — no IDs, keys, names, or organization details in the code.

## Setup

1. Open your tracker spreadsheet → **Extensions → Apps Script**, paste `InvoiceGenerator_public.gs`, save.
2. Reload the spreadsheet. Two menus appear: **Invoice Tools** and **⚙️ Setup**.
3. Run **⚙️ Setup → Run setup wizard** and answer the prompts (company name, departments, invoice prefix, Drive folder, signature font, etc.). Everything is stored in Script Properties — you never edit the code. Re-run the wizard anytime to change values; **View current config** shows what's stored.
4. Make sure your sheet's row 1 headers match the names in the `COLUMNS` constant at the top of the script (or edit that constant to match your headers).
5. Tick **Create Invoice?** on a row and run **Invoice Tools → Generate Invoices (checked rows)**. Approve the authorization prompts on first run.

## Caveats

- Some data-source logic is **deliberately simplified or example-only**: the author works with confidential HR data and cannot publish production specifics. In particular, the line-item description parser (`parseNotesDescriptions_`) and the amount-in-words function are demonstration schemas — adapt them to your own data conventions and locale before relying on them.
- Long numeric IDs (16+ digits) must be stored as **Plain text** in the sheet, or Sheets itself will corrupt the trailing digits before the script ever sees them.
- The cursive signature is a visual convenience for internal documents, not a cryptographic signature.

## Attribution

100% AI-generated, 100% human-directed. Directed and iterated by Yordhan Fitrians Akhmad B. based on real HR pain points — refined repeatedly for business fit, user experience, and workflow comfort.
