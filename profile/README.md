<div align="center">

<img src="https://raw.githubusercontent.com/clair-app/.github/main/profile/assets/icon.png" alt="Clair" width="96" height="96">

# Clair

**Answer Claude Code from your wrist.**

When Claude Code stops to ask for something, Clair puts it on your Wear OS watch and Android phone.
Allow a command, pick an answer or approve a plan from there, and the session keeps working while
you're away from your desk.

[![Google Play](https://img.shields.io/badge/Google%20Play-get%20Clair-3DDC84?logo=googleplay&logoColor=white)](https://play.google.com/store/apps/details?id=app.claircode.clair)
[![Agent release](https://img.shields.io/github/v/release/clair-app/clair-agent?logo=github&label=agent)](https://github.com/clair-app/clair-agent/releases/latest)
[![Clair changelog on whatsnew.fyi](https://whatsnew.fyi/product/clair/badge.svg)](https://whatsnew.fyi/product/clair)
[![Agent license](https://img.shields.io/github/license/clair-app/clair-agent?label=agent%20license)](https://github.com/clair-app/clair-agent/blob/main/LICENSE)

<img src="https://raw.githubusercontent.com/clair-app/.github/main/profile/assets/watch-tile.png" alt="The Clair tile on a Wear OS watch: a Bash prompt waiting in the payments-api session, two more sessions, and a Respond button." width="200">&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/clair-app/.github/main/profile/assets/watch-bash.png" alt="The watch's answers for a Bash prompt: Allow, Allow and remember for go test commands, and Deny with a reason." width="200">&nbsp;&nbsp;
<img src="https://raw.githubusercontent.com/clair-app/.github/main/profile/assets/watch-plan.png" alt="A plan review on the watch: Approve plan? with Yes, and use auto mode, and Yes, auto-accept edits." width="200">

</div>

## What reaches your wrist

- A permission prompt shows the exact command or edit. Allow it once, for the session, or by the
  rule Claude Code suggests, like every `go test` run. Or deny it with a reason you type or dictate,
  and Claude reads why.
- A question arrives with every option and its description. Pick one or several, or answer in your
  own words.
- A plan review lets you read the plan and approve it the way the terminal would: auto mode,
  auto-accept edits, or approve each edit yourself. Or send it back with notes on what should change.
- A tile shows what needs you next. A complication counts the sessions waiting on you, and its ring
  shows your usage in the current five-hour window. On Wear OS 6 and later, Clair's own watch face
  adds your weekly limit and the session's context window.

The watch is optional. Every prompt also reaches your phone, with Allow and Deny right in the
notification, and it still shows in your terminal. Answer wherever you are; the first answer settles
it and the others clear.

## How it works

```text
 Your computer                   Clair relay                Your phone            Your watch
 Claude Code + clair agent ───▶  holds sealed messages ───▶ opens each prompt ──▶ Wear OS
                    sealed on your computer, opened only on your phone
```

The Clair agent runs on the computer where you use Claude Code, on macOS, Linux or Windows. It
receives Claude Code's hooks on your machine, seals each prompt before it leaves, and brings your
answer back. Only your phone holds the key to open a prompt, so it travels end-to-end encrypted from
your computer to your phone.

Your computer and phone don't have to share a network. Both connect out to Clair's relay over HTTPS,
which holds a sealed message until your phone collects it, and never longer than a day. The relay
can't read or forge a command, a plan or an answer. To deliver messages and hold off abuse, it does
see when each pairing is active, how much it sends, the IP addresses your devices connect from, and
the push token that wakes your phone. From the phone, prompts reach your watch over Wear OS's own
phone-to-watch connection, which is not part of Clair's end-to-end encryption.

Revoke a computer from the phone or run `clair unpair` on it. Either one ends the pairing and deletes
anything still waiting on the relay.

## Get started

<img src="https://raw.githubusercontent.com/clair-app/.github/main/profile/assets/phone-notification.png" alt="A Clair notification on the phone asking whether Bash may run go test, with Allow, Allow for session and Deny buttons, above the session list." width="220" align="right">

1. Install [Clair from Google Play](https://play.google.com/store/apps/details?id=app.claircode.clair)
   on your Android phone (Android 12 or later), and on your Wear OS watch (Wear OS 4 or later) if you
   have one.
2. Install the agent on your computer. It keeps itself up to date from claircode.app.

   ```sh
   curl -fsSL https://claircode.app/install.sh | sh    # macOS and Linux
   irm https://claircode.app/install.ps1 | iex         # Windows, in PowerShell
   ```

3. Run `clair pair`, scan the code with your phone, confirm the phone's name in the terminal, and
   restart Claude Code.

The [setup guide](https://claircode.app/docs/) walks through each step. Installing Clair is free.
Answering prompts from your watch or phone takes a subscription through Google Play, which may start
with a free trial. Without one, sessions, the tile, the complication and notifications still work,
and prompts wait for you in the terminal.

## Here on GitHub

[**clair-agent**](https://github.com/clair-app/clair-agent) is the agent: the hook server, the
encryption between your computer and your phone, pairing, the login service and the self-update. It's written in Go and
licensed under Apache 2.0. Issues and pull requests are welcome, and vulnerabilities can be
reported privately from its Security tab.

The phone and watch apps ship through Google Play, and the relay runs at `relay.claircode.app`.
Their source isn't published here. For help with the app, email
[support@claircode.app](mailto:support@claircode.app).

---

<sub>Clair is an independent app built by [Jeff Mixon](https://www.jeffmixon.com/). Claude and Claude
Code are trademarks of Anthropic, PBC. Clair is not made, sponsored or endorsed by Anthropic.</sub>
