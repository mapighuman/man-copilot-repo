---
name: new-day
description: Add the current UTC date to the daily updates on the homepage.
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
tools:
  edit:
safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - index.html
---

Use the workflow run's current UTC date, obtained from the runtime environment with `date -u`. Update only `index.html`.

Before editing, inspect the existing Daily Updates navigation and every daily update dialog in `index.html`. If the current UTC date is already represented in the navigation or dialog, make no change and do not create a pull request.

When the date is not already present:

- Add one navigation item to the existing Daily Updates list.
- Use the existing date wording: an ordinal day followed by the full month name, such as `1st of August`, without a year.
- Add one matching accessible `<dialog>` using the existing structure and ID conventions. Use a lowercase month-and-day ID such as `august-1-dialog`, with matching `aria-labelledby` and `aria-describedby` IDs such as `august-1-question` and `august-1-answer`.
- Make the dialog confirm that the daily update ran for that UTC date. Keep its header wording, close control, accessibility attributes, and surrounding markup consistent with the existing dialog.
- Point the new navigation control at the new dialog and preserve the existing navigation controls and dialogs exactly.

Do not modify `styles.css`, duplicate a date, navigation control, or dialog, or remove any existing daily update. Review the final diff to ensure that only the new date entry and its matching confirmation dialog were added to `index.html`.