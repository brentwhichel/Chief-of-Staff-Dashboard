# Chief of Staff Dashboard

Build your own **COS Communications Dashboard**: a private Chief of Staff app that Microsoft 365 Copilot Cowork
builds for you. Cowork automations screen every email and Teams chat against your Chief of Staff constitution,
research the answer, and draft a reply in your voice. Your dashboard app shows them day by day so you can review,
edit and send each reply, mark it complete or delete it, and keep your own task list in the same app.

![The dashboard with fictional demo data, one draft open with its placeholders highlighted](https://brentwhichel.github.io/Chief-of-Staff-Dashboard/docs/images/dashboard-demo.svg)

- **Setup guide:** https://brentwhichel.github.io/Chief-of-Staff-Dashboard/
- **Demo with sample data:** https://brentwhichel.github.io/Chief-of-Staff-Dashboard/demo.html

This repository holds the setup guide, the prompts and the app source Cowork builds from. Your dashboard
itself is always a private app in your own Microsoft 365, never this website. The demo shows how it works with
sample data from a fictional company; it never signs in or reads real mail, chats or files.

## What you get

- **My tasks** at the top: add, complete, reopen and delete your own to-dos.
- **Latest check**, with a full run log: every automation run shows up, even when nothing needed you, and
  the app warns you when the automations look paused.
- **A day-by-day timeline** of the emails and Teams chats that need you, each with priority, why it matters,
  a summary, who's on it, private research notes, and a researched draft reply.
- **Scan first, open when needed.** Each draft stays folded behind **Show draft reply**, next to
  **See original**, which loads the original email or Teams message as plain text (it never marks mail read).
- **Placeholders you can't miss.** Anything Cowork couldn't confirm is left in `[brackets]` and highlighted in
  yellow, with a count on the button, a banner above the draft, and a **Send anyway?** check if any are left.
- **Send with a 5-second undo**, Reply all, add people to a reply (external recipients flagged), Mark
  Complete, Reopen, Delete with undo, and All / Open / Completed filters.
- **External replies through Outlook.** A reply that reaches anyone outside your company opens as a prefilled
  draft in Outlook, because many organizations block app-sent email to outside addresses. Ask Cowork to
  change this in your app if your organization allows it.

Nothing is ever sent unless you press **Send** on a specific item.

## How it works

```
 Watch (Cowork automations)         Store (your OneDrive)                    Act (your dashboard app)
 ─────────────────────────          ─────────────────────────────            ────────────────────────
 Inbox email screening      ──┐     Documents/Cowork/COS Comms Dashboard/    My tasks
 Customer email screening   ──┤──►    comms-feed.json   (items + run log) ──► Latest check
 Key-person chat alerts     ──┤       dashboard-state.json  ◄───────────────  Review, edit, send
 Scheduled Teams sweep      ──┘       my-tasks.json         ◄───────────────  Complete / delete
                                      teams-sweep.json
```

Your dashboard is a private app that Cowork builds and Microsoft hosts in your own Microsoft 365. It signs you in
with your work account and reads and sends through your own Outlook, Teams and OneDrive connections, so there's
nothing for IT to register, and each person sees only their own email, chats and tasks.

## Set up your own dashboard

Open the [setup guide](https://brentwhichel.github.io/Chief-of-Staff-Dashboard/) and follow Steps 1 to 7. It fills
your details into every prompt:

1. **Constitution.** Tell Cowork how to act as your Chief of Staff.
2. **Private feed.** Cowork creates the folder and files in your OneDrive.
3. **Your dashboard app.** Cowork builds the app from [`cowork-app/`](cowork-app) and gives you its link.
4. **Email screening.** Every new email is added with a draft or skipped with a reason.
5. **Customer email.** Its own screening watches your Inbox, so every customer email lands on the dashboard. No
   Outlook folder or rule to set up.
6. **Key people.** Instant capture and a private self-chat alert for the few people who can't wait.
7. **Teams sweep.** A scheduled sweep of every chat, every customer message, every @mention and every unread
   one-on-one chat.

Then audit after the first week (Step 10) and tune weekly. The same prompts are in [`prompts/`](prompts),
and [`docs/facilitator-guide.md`](docs/facilitator-guide.md) is a 60-minute plan for walking someone else
through it.

You need Microsoft 365 Copilot with Cowork, including automations, and permission to build apps in Cowork (on for
everyone unless your admin has limited it).

## Changing the prompts

Edit [`assets/prompts.js`](assets/prompts.js), then run `node tools/build-prompts.js` to refresh the Markdown
copies in `prompts/`.

## Privacy and security

- This repository holds no personal data. Every name and company in the demo is fictional.
- The demo never signs in, never reads real mail, chats or files, and never sends anything. Changes you make in
  it are kept only in that browser tab.
- Your dashboard app follows your organization's policies, and it reads and sends only as you.

## Repository layout

| Path | What it is |
|---|---|
| `index.html`, `setup.html` | The step-by-step setup guide (`index.html` opens it) |
| `demo.html`, `config.js` | The demo with sample data |
| `assets/` | Demo code and styles (`app.js`, `core.js`, `styles.css`), the setup guide (`setup.js`, `setup.css`), all prompts (`prompts.js`) and the fictional demo data |
| `prompts/` | Every setup prompt as Markdown |
| `cowork-app/` | The app source Cowork builds your dashboard from (Step 3) |
| `docs/` | Feed format and facilitator guide |
| `starter-files/` | Empty copies of the four feed files |
| `tools/build-prompts.js` | Rebuilds `prompts/` from `assets/prompts.js` |
