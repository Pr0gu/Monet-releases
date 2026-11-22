# Monet

Monet is a macOS menu bar app that shows the usage limits of every Claude account you use, all at once.

This repository holds **only Monet's releases**: the notarized disk image of each version, and the signed update
feed (`appcast.xml`) that Monet checks once a day. Monet's source code is private.

You need a Mac with macOS 15.4 (Sequoia) or later, and one or more Claude accounts on a paid plan (Pro, Max or Team).

## Install

1. Download `Monet-<version>.dmg` from the latest release. Its SHA-256 checksum is next to it:
   `shasum -a 256 -c Monet-<version>.dmg.sha256`.
2. Open it and drag Monet to Applications.
3. Open Monet. macOS asks once whether to open an app downloaded from the internet, and names the developer.
   Monet is notarized by Apple.

A small window, **Welcome to Monet**, walks you through its steps:

1. **Continue.**
2. **Know before a limit runs out.** Choose **Allow Notifications** so Monet can tell you when an account is running
   low and when its limit resets, or **Not Now**. You can change this later in System Settings › Notifications.
   If you have installed Monet before, macOS already has your answer and this step is skipped.
3. **Add your accounts.** See the next section. **Done** works once at least one account is added.

Monet then lives in the menu bar: a small sun over water, with one reflection stroke for each account. Each stroke
is as long as that account's limit has left. Click it to see every account.

If the menu bar is full, macOS may hide Monet behind the camera notch, and Monet says so. Hold ⌘ and drag Monet's
icon to the right, or remove an icon you don't use.

To have Monet open when you log in, turn on **Settings › Menu Bar › Open at login**.

## Add your accounts

Each account signs in once, on Anthropic's own sign-in page. You type your password there, never in Monet, and
Monet never sees it.

1. In Monet, click **Add Account**. It is in the first-run window, in **Settings › Accounts** (**+ Add Account**),
   and in the menu bar panel before any account is added.
2. Anthropic's **Log in** page opens in your default browser, where your saved passwords are. Log in with the
   account you want to add (by email, Google or Apple), then click **Authorize**.
3. Monet says the account is connected, under its Claude name (for example **"Jane Doe is connected"**), or under
   the name your other Macs give it, and you can rename it there, to "Work" for instance. If your other Macs keep it
   hidden, Monet says so and offers **Unhide**.
4. Click **Add Another** for the next account, or **Done**.

Your browser signs Monet in to the Claude account it is signed in to. To add a different account, sign out of
claude.ai in your browser first, then click **Add Another**.

If you add an account that is already in Monet, its sign-in is renewed, and Monet says so (**"Jane Doe is signed in
again"**). While Monet waits, **Cancel** stops the sign-in; if nothing comes back within 10 minutes, Monet says so and
saves nothing, and **Try Again** starts over. If an account's access ever expires, its row says so and offers **Sign
in**.

**Sign in again before it ends.** Each account's sign-in in Monet lasts about four weeks. In its last week Settings ›
Accounts says when it ends and offers **Sign In Again…**, the account's row says **sign-in ends Thu** where it has room
(not while Monet is waiting for Anthropic or can't reach it), and three days before the end a notification offers
**Sign In Again**. You can sign in again at any time from the account's menu in the panel or in
Settings. Monet asks you to sign in as that account. If your browser signs in as a different one, Monet tells you and
adds nothing.

**To remove an account:** Settings › Accounts, select it, then **− Remove**. This deletes its sign-in and its
history on this Mac. Your Claude account itself is not changed.

## Updates

Monet checks this repository for a new version once a day. Every update is signed, and Monet checks the signature
before it installs anything. To check now, choose **Check for Updates…** in the panel's **More** menu. To stop the
daily check, turn off **Settings › About › Check for updates automatically**.

## Privacy

**What Monet contacts, and why.** Nothing else, and no analytics or crash reports:

| Where | Why |
| --- | --- |
| claude.com, in your browser | Anthropic's sign-in page, when you add an account |
| platform.claude.com | to finish a sign-in, and to renew an account's access when it expires |
| api.anthropic.com | to read each account's usage limits, and its name and email when it is added |
| status.claude.com | Claude's service status, every 5 minutes, to show incidents |
| github.com (this repository) | the daily update check, and the download when you install an update |
| iCloud (Apple), through macOS | to keep Monet's settings the same on your Macs signed in to the same iCloud: account names, colours, alert levels and plans. Never a sign-in, a token or usage |
| app.draumo.com, in your browser | Draumo's page where you allow Monet and choose where its card shows, when you press Connect to Draumo (1.9) |
| api.draumo.com, only once you connect Monet to Draumo | your card in your own Draumo's top bar. Opt-in, off by default, per Mac. Monet can post and update its own card in your top bar; it can't read anything in Draumo or see anyone else's cards. Sent: the names you gave your accounts in Monet (one you haven't renamed goes as "Account 1", "Account 2" and so on), each one's 5-hour and week use and reset times, and which account has the most room left. Never sent: emails, account ids, org names, Claude profile names, plans, bills, tokens, project names, costs. Disconnect ends Monet's access, and Draumo takes the card down. "Use a key instead" takes an API key with `statusItems:write` only; Test checks it with a dry run that stores nothing. Monet never reads your Draumo cards |

Monet asks Anthropic only for permission to read your profile and usage (`user:profile`). It identifies itself
honestly, as `Monet/<version>`.

**What it keeps on your Mac.** Each account's sign-in, and Monet's Draumo token (or your key) if you connect, are kept in your macOS
Keychain, in Monet's own items. The account list and
usage history are in `~/Library/Application Support/Monet/`. Nothing leaves your Mac except the requests above.

**Cost.** Monet adds up what your Claude Code use would cost at API prices, from Claude Code's own logs on this Mac
(`~/.claude/projects`). From those logs it reads only the model and the token counts; what you and Claude wrote is
never read into Monet. Cost per account is optional: **Settings › Data › Cost tracking › Set Up…** shows the five
lines it would add to Claude Code's settings before it changes anything. After that, Claude Code reports each session's cost to
Monet on your own Mac (`127.0.0.1`), and **Turn Off…** removes the lines again.

**What Monet never touches.** Monet never reads or changes Claude Code's own sign-in, so it can't sign you out of
Claude Code. It never sees your password.

## Releases

- `v<version>`: Monet. The newest one is marked **Latest**, and its `appcast.xml` is Monet's update feed.
- `dev`: a pre-release test channel that only Monet Dev reads. Monet Dev is the developer's own test build, so
  this channel is not for installing.

Monet is an independent app. It is not made by, or affiliated with, Anthropic.
