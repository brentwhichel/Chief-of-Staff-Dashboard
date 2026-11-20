# Step 3: Build your dashboard app in Cowork

Your dashboard is a private app that Cowork builds for you from this repository, just like the original. It signs you in with your work account and sends the replies you approve through your own Outlook and Teams connections, so there's nothing for IT to set up. It stays empty until Step 4 runs.

**Where:** Stay in the same Cowork task and paste this prompt. Approve the Outlook, Teams and OneDrive connections when Cowork asks.

```text
Build my COS Communications Dashboard as an App Builder app named "COS Communications Dashboard".

1. Add three data sources: OneDrive for Business, Office 365 Outlook and Microsoft Teams.
2. Use the source in https://github.com/brentwhichel/Chief-of-Staff-Dashboard/tree/main/cowork-app exactly. Copy these files into the app, replacing the template's versions:
   - cowork-app/src/pages/home.tsx -> src/pages/home.tsx
   - cowork-app/src/lib/comms.ts -> src/lib/comms.ts
   - cowork-app/src/lib/connector-safety.ts -> src/lib/connector-safety.ts
   - cowork-app/src/lib/header-slot.ts -> src/lib/header-slot.ts
   - cowork-app/src/components/app-shell.tsx -> src/components/app-shell.tsx
   - the theme colors in cowork-app/theme.css -> the :root and .dark blocks of src/index.css
3. In src/lib/comms.ts set OWNER_EMAIL to "[YOUR_EMAIL]", TIME_ZONE to "[YOUR_TIME_ZONE, e.g. America/New_York]", INTERNAL_DOMAINS to my company email domains, and FOLDER to "/Documents/Cowork/COS Comms Dashboard". Leave SEND_OUTSIDE_FROM_OUTLOOK set to true, so replies to people outside my company open as drafts in Outlook.
4. Type-check it, publish it, and give me the link. Keep it private to me.

Nothing is ever sent unless I press Send on a specific item.
```

**After Cowork answers:** Open the link Cowork returns and bookmark it. That app is your dashboard; you can also find it at managedapps.cloud.microsoft.
