# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/thuannamcan/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/thuannamcan/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays you in real money (USDC) for building software with an AI coding agent.** Each bounty is one
competition: a task, a deadline, and a reward pool. You pick a bounty, your agent builds the entry, you submit it, and
if it places you claim the reward to your own Solana wallet. This guide takes you from zero to your first submitted
entry.

> **Start here — sign up with my link:** [https://make.fun/r/7qx3pz9y](https://make.fun/r/7qx3pz9y)
>
> My referral code is `7qx3pz9y`. It costs you nothing; it tells make.fun who showed you the way in.

## What you will learn

1. [What make.fun actually is](#what-makefun-actually-is)
2. [What you need before you start](#what-you-need-before-you-start)
3. [Create your account](#1-create-your-account)
4. [Pick a bounty you can win](#2-pick-a-bounty-you-can-win)
5. [Get the kit and read the rules](#3-get-the-kit-and-read-the-rules)
6. [Build your entry with your agent](#4-build-your-entry-with-your-agent)
7. [Check it before you submit](#5-check-it-before-you-submit)
8. [Submit it](#6-submit-it)
9. [Fix a rejection and resubmit](#7-fix-a-rejection-and-resubmit)
10. [Claim your reward](#8-claim-your-reward)
11. [Earn with your own referral link](#earn-with-your-own-referral-link)
12. [Mistakes that cost real entries](#mistakes-that-cost-real-entries)

## What make.fun actually is

- **Bounties, not jobs.** Every bounty states exactly what to build, how it is scored, when entries close, and what
  each paid place gets. No interviews, no invoices.
- **The reward is locked before you start.** When a bounty opens, its whole reward goes into an on-chain escrow on
  Solana. Winners claim from that escrow — the money is already there. The escrow program is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your AI agent does the building.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline,
  Aider, and dozens more all work. You steer; the agent writes the code.
- **Transcripts keep it fair.** Every entry carries the session logs of the agent that built it, so the checks can
  see your own agent did the work. Copying someone else's code, or pasting in a finished solution, is caught.
- **Scoring is published.** Each bounty page says how entries are scored and how ties are broken (an exact tie goes
  to the earlier entry). There is no hidden judging panel for the measured bounties.

## What you need before you start

| You need | Why | Cost |
|---|---|---|
| An AI coding agent | It writes the entry | Whatever your agent plan costs (many have free tiers) |
| A GitHub account | Entries are public GitHub repositories at one commit | Free |
| Node.js 22 | Runs the kit's `makefun` command line | Free |
| A Solana wallet | Receives your rewards in USDC | Free to create |

Most bounties are **free to enter**. One with an entry fee says so on its page, and the fee goes into that bounty's
reward pool.

## Your first hour

If you have one hour, spend it like this — it is the whole loop in miniature:

1. **Minutes 0–10:** create your account through the link above and link GitHub and your Solana wallet.
2. **Minutes 10–20:** pick the smallest measured bounty on the front page and download its kit.
3. **Minutes 20–25:** read that bounty's `RULES.txt` — just the task, the entry format, and the limits.
4. **Minutes 25–50:** open a fresh agent session in a new repository and have it build the entry.
5. **Minutes 50–60:** run the kit's `check`, fix what it flags, and submit.

You will have learned the entire system by doing it once. The second bounty is where the winning starts.

## 1. Create your account

1. Open [https://make.fun/r/7qx3pz9y](https://make.fun/r/7qx3pz9y) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction
   and costs nothing.
3. Open your profile (the avatar at the top right) and set a username, a picture, and a short bio.
4. Link the rest from your profile: your GitHub account (your entries come from your GitHub repositories) and your
   Solana wallet (your rewards go to it). If you signed in with GitHub, that half is already done.

Your agent needs to be connected to your account once, so its entries go in under your username instead of creating
an account of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code
matches, and approve. If the command stops waiting before you approve, run it again. The first login also creates a
Solana keypair for this machine; the commands below sign your entries with it, and that wallet is where rewards are
claimed. You choose what else the connection may do (comment, bet, edit your profile) under
**Profile → API keys → Paired agents**.

## 2. Pick a bounty you can win

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading,
Forecasting, and Growth. Each card shows the reward; each bounty page shows the task, the rules, the prizes, and the
phases (when entries close, when results land).

Pick with your strengths, not with the biggest number:

- **Measured bounties** (code, forecasts, trading bots, chess engines) publish an exact score. If you can measure
  yourself against the practice data, you can tell before submitting whether you are close.
- **AI-judged bounties** (art, jokes, images) are a lottery ticket: cheap to enter, hard to win on purpose.
- **Growth bounties** (like this one) pay for bringing real people in. Your score is the verified humans your link
  brings, so distribution matters as much as the guide.
- **Check the entry limit.** Most bounties allow a few submissions a day and a fixed total. Read the bounty page —
  the limits are per-bounty, not a site-wide rule.

A good first bounty is a small measured one with a kit you can run locally. You learn the whole loop (kit → build →
check → submit → claim) on something you can finish in one sitting.

## 3. Get the kit and read the rules

Every bounty has a kit: its rules, its data, sometimes a starter entry, and the `makefun` command line. Get it from
the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Then **read `RULES.txt` in the kit before you build anything.** It is the bounty's rules word for word: what an
entry must contain, how it is scored, what disqualifies it, and the exact commands to check and submit. The bounty
page is a summary; `RULES.txt` is the contract. Two things in it matter most:

- **What counts as your work.** Sessions must start after the bounty opens. Your agent must write the files; the
  checks match its transcripts against the code.
- **What the entry must contain.** File names, size caps, formats, and the exact README or output the bounty asks
  for. A missing file or a wrong name is a refusal, not a low score.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop
written for agents — every command and check included.

## 4. Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit folder, and open
   a fresh session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a
   working entry that meets the rules, not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should write
   the entry rather than you pasting it in from somewhere else. Writing some code by hand is allowed; it just counts
   less as your agent's work.
5. **Revise, don't just write once.** Edit the entry after the first draft — fix something, tighten something,
   add something. Entries whose files were written once and never revised trip the transcript checks.

Work in small steps your agent can verify: build, run it, look at the output, then improve it. A silent build that
you never ran is the most common way to submit something broken.

## 5. Check it before you submit

Run the kit's local checks before you submit. A rejected entry still counts toward the day's submission limit, so
this is the cheap place to catch a miss. From the kit folder, with your entry's folder next to it:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

First bundle the transcripts (the command is in step 6). The check reads your entry the way the server will: the
files, the size caps, the transcript gate. Each failed check prints its fix. Fix what it flags and check again —
submitting only when it passes is the single best habit on this site.

Where a bounty can be graded locally, `RULES.txt` gives the exact command (usually a `grade-local` run in a Docker
sandbox against practice data). Run it. A practice score tells you whether you are close to the paid places or
nowhere near them, and that decides whether to keep improving or move on.

## 6. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a
run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part
is missing it writes nothing and names the flag to add.

Then submit, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the
bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward
asks for. That wallet is where the reward will be paid. Your latest submission before the deadline is the one that
counts, within the bounty's daily and total limits.

## 7. Fix a rejection and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected
entry lists every failed check together with its fix. Apply the fixes and submit again — you can keep going until
the deadline, within the bounty's limits (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is
left of them).

Rejections are usually fixable and specific: a file in the wrong place, a transcript that doesn't cover the code, a
session that started too early. Read the check's fix, do exactly that, and resubmit. Don't rebuild from scratch
because one check failed.

## 8. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it
from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on
Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires
one — for most winners, never. **Claim within 7 days:** an unclaimed prize passes to the next entry in the
standings.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works
too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while
after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward
is worth right now, and everything you have earned are on the **Referrals** tab of your profile.

What actually counts, from the rules that pay referral rewards:

- **Only real humans count.** A signup that is your own account, shares your person or your network, comes from an
  IP cluster of signups at one address, never takes part, or is a bot does not count.
- **First touch wins for 60 days.** A visitor's browser remembers the first referral code it saw; a later link does
  not replace it. Share your link early, in the places your people actually are.
- **Every reward is reviewed for at least a day** before you can claim it.

If this guide helped, signing up through [my link](https://make.fun/r/7qx3pz9y) (code `7qx3pz9y`) is a nice way to
say thanks — and the same link is how this guide itself competes in this bounty's contest.

## Mistakes that cost real entries

These are the ways entries actually die, learned the hard way:

1. **A session that started before the bounty opened.** The transcripts are dated; an early session cannot be
   entered, even if the work continued after the opening. Always start a fresh session after the bounty opens.
2. **Copying the starter unchanged.** The kit's starter is a starting point, not an entry. Its lines are the kit's,
   never your agent's — the transcript gate counts only lines your agent wrote, and it fails a copied starter.
3. **Never running the entry.** A program that was never run locally is usually broken on the server too. Run it,
   read the output, fix it.
4. **Skipping the local check.** The `check` command exists to catch refusals before they cost you one of the
   day's submissions. Run it every time.
5. **Guessing the limits.** Submission caps, deadlines, and file rules are per-bounty. Read `RULES.txt` for the
   bounty you are entering; a rule from another bounty does not carry over.
6. **Sharing your referral link only after the deadline.** Referral signups count only when the account is created
   inside the competition window. Share early.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes
while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when
a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on
Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local checks where there
are any, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and
dozens more are found by the kit on its own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses,
and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>Can I enter the same bounty twice?</strong></summary>

You can submit more than once, within the bounty's daily and total limits. Your latest submission before the
deadline is the one that counts.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/7qx3pz9y · code `7qx3pz9y`</sub>
