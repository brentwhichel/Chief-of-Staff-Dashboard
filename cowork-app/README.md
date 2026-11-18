# Build the dashboard inside Cowork (Step 3, option A)

This folder holds the source of the original **COS Communications Dashboard** app, built in Cowork with
App Builder. Pick it instead of the website (option B) when you don't want to involve IT: its **Send** button uses your
own Office 365 Outlook and Microsoft Teams connections, so no IT app registration is needed.

The website (`index.html`) and this app read the same feed, so you can use both.

## Files

| File | Goes to | What it is |
|---|---|---|
| `src/pages/home.tsx` | `src/pages/home.tsx` | The dashboard screen: My tasks, Latest check, filters and the day-by-day timeline |
| `src/lib/comms.ts` | `src/lib/comms.ts` | Reads the feed, saves your state and tasks, sends replies, loads **See original**, builds Outlook drafts |
| `src/lib/connector-safety.ts` | `src/lib/connector-safety.ts` | Logs connector failures without message content |
| `src/lib/header-slot.ts` | `src/lib/header-slot.ts` | Lets the page show "Last refreshed" in the header |
| `src/components/app-shell.tsx` | `src/components/app-shell.tsx` | Header with the app name |
| `theme.css` | the `:root` and `.dark` blocks of `src/index.css` | The teal theme |

## Settings to change

At the top of `src/lib/comms.ts`:

```ts
export const OWNER_EMAIL = "you@contoso.com";      // your work email
export const TIME_ZONE = "America/New_York";       // your IANA time zone
export const INTERNAL_DOMAINS: string[] = [];      // your company's email domains (empty = your own domain)
export const SEND_OUTSIDE_FROM_OUTLOOK = true;     // replies to outside addresses open as Outlook drafts
```

and, a few lines below, `FOLDER` if your feed isn't in `/Documents/Cowork/COS Comms Dashboard`.

## Ask Cowork to build it

Use Step 3 of the setup guide (`setup.html`), which fills in your details, or paste
[`prompts/03-build-the-app-inside-cowork.md`](../prompts/03-build-the-app-inside-cowork.md)
into the same Cowork task you use for your automations. Cowork adds the three data sources (OneDrive for
Business, Office 365 Outlook, Microsoft Teams), copies these files, type-checks, publishes, and gives you
the link.

## Notes

- Many organizations block apps from emailing people outside the company. With `SEND_OUTSIDE_FROM_OUTLOOK`
  on, a reply that reaches anyone outside yours shows **Open draft in Outlook** instead of **Send**: a new
  Outlook message with the recipients, `RE:` subject and your draft filled in (and copied to your clipboard).
  Replies the app already sent to outside addresses get **Resend from Outlook**.
- Drafts stay folded behind **Show draft reply**, next to **See original**, which reads the original email or
  Teams message from your own Outlook or Teams when you open it (plain text only; it never marks mail read).
- Every `[bracketed placeholder]` in a draft is highlighted in yellow and counted, and **Send** asks
  before sending one with brackets left.
- Nothing is sent unless you press **Send** on a specific item, and every send has a 5-second undo.
