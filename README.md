# 🤖 Monetize Me Helper — Bot Command Guide

Welcome to the **Monetize Me Helper** bot! This bot manages badge competitions, tracks entries, and maintains leaderboards for your team. Below is a complete guide to every command and feature.

---

## Table of Contents

- [How It Works](#how-it-works)
- [Badge Types](#badge-types)
- [For Chatters (Team Members)](#-for-chatters-team-members)
  - [Submitting Entries](#submitting-entries)
  - [Bingo Entries](#bingo-entries)
  - [Chatter Commands](#chatter-commands)
- [For Managers & Admins](#-for-managers--admins)
  - [Approving & Rejecting Entries](#approving--rejecting-entries)
  - [Period Management](#period-management)
  - [Data & Sync Commands](#data--sync-commands)
  - [Cleanup Commands](#cleanup-commands)
  - [Admin Lookup Commands](#admin-lookup-commands)
  - [Bot Configuration](#bot-configuration)

---

## How It Works

The bot runs a **badge competition system** with timed periods. Team members submit screenshot entries in designated channels, managers approve or reject them with reactions, and the bot tracks everything on a live leaderboard. At the end of each period, the top performer earns the **Badge Holder** role, and a new period begins.

**Key concepts:**
- **Period** — A competition window with a start and end date. Only entries within the period count toward the leaderboard.
- **Entry** — A message with an image posted in a badge's entry channel. The bot automatically detects and tracks it.
- **Approval** — A manager reacts with ✅ to approve an entry, or ❌ to reject it.
- **Challenger** — The user currently ranked #1 on the leaderboard gets the Challenger role.
- **Badge Holder** — Awarded to the winner(s) when a period is concluded.

---

## Badge Types

The bot supports two **modes** of badges:

### Standard Badges (14-day periods)
Entry-count based competitions. The user with the most approved entries wins.

| Badge | Description |
|-------|-------------|
| **Notes Paramedic** | Save and submit fan notes |
| **Renewal Reaper** | Close resubscriptions |
| **Consistency Machine** | Consistent daily performance |
| **Buyer Reviver** | Revive cold or lapsed buyers |
| **Good Samaritan** | Helping & supporting others on the team |
| **Bond Builder** | Building strong, lasting fan relationships |

### Bingo Badge (7-day period)
A stamp-collection challenge. Complete all 10 unique stamp challenges to win.

| Badge | Description |
|-------|-------------|
| **Weekly Bingo** | Complete all 10 stamp challenges to earn a Spin of the Wheel |

### Period Cadence
- **Standard badges** run **14 days**, Monday → second Sunday after.
- **Weekly Bingo** runs **7 days**, Monday → Sunday.
- All periods snap to **Monday 00:00 PHT** (Philippines time, UTC+8).
- Periods auto-conclude **on their end date**; the bot checks every 15 minutes.

**Bingo Stamp Challenges:**
| # | Challenge |
|---|-----------|
| 1 | Close a Resubscription |
| 2 | Revive a Cold Buyer |
| 3 | Hit Shift Benchmark |
| 4 | Save a Fan Note |
| 5 | Discover a Fan Preference |
| 6 | $200 Fan Session |
| 7 | Convert a New Buyer |
| 8 | Hit Weekly Sales Target |
| 9 | Share a Tip for Success |
| 10 | Perfect Shift Handover |

> 🏆 The first **3** people to complete all 10 stamps each period automatically earn the Weekly Bingo role!

---

## 👤 For Chatters (Team Members)

### Submitting Entries

1. Go to the **entry channel** for the badge you want to submit to.
2. Post a message **with a screenshot** (image attachment or image link).
3. The bot will confirm your entry with a reply like:
   > *Entry received! This is your **3rd** entry this period (2 approved so far).*
4. The bot adds ❌ and ✅ reactions for managers to use.
5. Wait for a manager to approve (✅) or reject (❌) your entry.

**Important:**
- Your message **must contain an image** — text-only messages are ignored.
- Entries are automatically de-duplicated; the same message won't be counted twice.

### Bingo Entries

For the **Weekly Bingo** badge, you must include the **stamp number** in your message so the bot knows which challenge you're completing.

**Accepted formats:**
- `Stamp 3 - Hit Shift Benchmark` ✅
- `#3 — here's my proof` ✅
- `3. Hit Shift Benchmark` ✅
- Just the number `3` somewhere in the message ✅

The bot will reply with your progress:
> 🎯 *Entry received for **Stamp #3: Hit Shift Benchmark**! Progress: 4/10 stamps completed.*

⚠️ If you forget the stamp number, the bot will warn you. Your entry is still saved but won't count toward a stamp until a manager identifies it.

⚠️ If you submit a duplicate stamp (one already approved), the bot will let you know it won't count again.

✏️ **Editing entries:** If you edit your bingo entry message to change the stamp number, the bot automatically detects it and updates your progress. *(Note: If no tracking period is set via `/setperiod`, old entries from previous weeks will still remain on the leaderboard alongside your edited entry.)*

---

### Chatter Commands

These commands are available to all team members. Responses are **ephemeral** (only you can see them).

---

#### `/mystats`
> View your personal stats for a specific badge or all badges.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Choose a specific badge, or "All Badges" for a summary |

Shows your approved ✅, pending ⏳, rejected ❌, and total entry counts plus your approval rate.

If no badge is specified and you're in a badge channel, it auto-detects the badge type.

---

#### `/myentries`
> List all your entries and their approval status.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Choose a specific badge, or "All Badges" for all |

Shows each entry with its status (✅ Approved / ⏳ Pending / ❌ Rejected), date, and a **Jump** link back to the original message.

---

#### `/leaderboard`
> View the detailed leaderboard with full stats for each participant.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Choose a specific badge, or "All Badges" for all |

Shows rank, approved count, pending, rejected, and approval rate for every participant. Non-participants are listed at the bottom.

---

#### `/badges`
> List all active badge types, their channels, period dates, and roles.

No parameters. Shows a summary of every active badge with its entry channel, stats channel, current period, and assigned roles.

---

#### `/bingostamps`
> View all 10 bingo stamp challenges and the reward.

No parameters. Displays the full list of stamp challenges and the reward for completion.

---

#### `/bingostats`
> View your bingo stamp progress.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `member` | No | Admin-only: view another member's bingo progress |

Shows each of the 10 stamps with ✅ (completed), ⏳ (pending), or ⬜ (not started).

---

#### `/bingoleaderboard`
> Show the bingo stamp progress leaderboard.

No parameters. Displays all participants with a visual progress bar showing their completed, pending, and remaining stamps. Winners (first 3 to complete all stamps) get a 🏆 icon.

---

## 🛡️ For Managers & Admins

### Approving & Rejecting Entries

Managers approve or reject entries using **reactions** on entry messages:

| Reaction | Action |
|----------|--------|
| ✅ | **Approve** the entry — counts toward the leaderboard |
| ❌ | **Reject** the entry — does not count |

**How it works:**
- When a new entry is posted, the bot adds both ❌ and ✅ reactions as placeholders.
- A manager clicks ✅ to approve or ❌ to reject.
- The **latest manager reaction** is authoritative — if multiple managers react, the last one wins. Previous manager reactions are automatically removed.
- Removing your ✅ or ❌ reaction resets the entry back to **pending**.
- Non-managers who try to react with ✅/❌ will have their reaction automatically removed.

**Live updates:**
- The **stats channel leaderboard** updates automatically after every approval/rejection.
- The **Challenger role** (🏆) is automatically assigned to whoever is ranked #1, and removed when they lose the lead.

---

### Period Management

These commands require **admin, chat manager, bot admin, or command access** role.

---

#### `/setperiod`
> Set or view the competition period dates for badges.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" to set all at once |
| `start` | No | Period start date (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |
| `end` | No | Period end date (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |

- **View current:** Run with no `start`/`end` to see current period dates.
- **Set dates:** Provide `start` and/or `end` to update. Only entries within this window count.
- **All Badges:** Choose "All Badges" to set the same dates across every badge.
- **Auto-Monday alignment:** When `/reset` or `/conclude` advances a period (or when no period is set yet), the new period snaps to **Monday 00:00 PHT** automatically. Standard badges run 14 days, Weekly Bingo runs 7 days.

> 💡 When a period end date is reached, the bot **auto-concludes** the badge within ~15 minutes (auto-conclude loop runs every 15 min).

---

#### `/setstartdate`
> Set, view, or clear the **global start date** used as a default for resync and filtering.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `date` | No | `YYYY-MM-DD`, `YYYY-MM-DD HH:MM`, or `clear` |

- **View:** Run with no parameter.
- **Set:** Provide a date. Used as the fallback when no per-badge period is set.
- **Clear:** Pass `clear` to remove it.

> ⚠️ **Important — global start date is a fallback only.** If a badge has its **period start or period end** set (via `/setperiod`), the period wins and the global start date is **ignored** for that badge during `/resync`. To force a resync over a custom range without touching periods, use `/resync since_date:<date>` instead. See the `/resync` section for the full priority order.

---

#### `/reset` — archive-only
> Post summary to history, soft-delete entries, advance period dates. **No role changes.**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |

**What it does:**
1. Posts a full period summary embed to the badge's **history channel**.
2. Soft-deletes all entries in the current period.
3. Advances period dates Monday-aligned (next Mon → +6 days bingo, +13 days standard).

**What it does NOT do:**
- Does **not** award 🏅 Badge Holder role.
- Does **not** remove 🏆 Challenger roles.
- Does **not** hard-delete old DB entries.

**When to use:** Mid-period do-over, testing, or any time you want a clean slate without crowning a winner. For real end-of-period workflow use **`/conclude`**.

Requires confirmation (✅ / ❌ buttons).

---

#### `/conclude` — full end-of-period
> Everything `/reset` does **plus** the role + cleanup work that ends a real competition.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |

**What it does (for each badge):**
1. **Awards** 🏅 Badge Holder role to the #1 ranked user(s). Ties: all tied users receive the role.
2. **Removes** 🏆 Challenger role from everyone (period is over).
3. **Posts** a full period summary to the history channel, including the winner announcement.
4. **Sends** a conclusion announcement to the entry channel.
5. **Soft-deletes** all entries in the period.
6. **Hard-deletes** old DB entries outside the period (auto cleanup — no `/deleteentries mode:outside-period` needed afterward).
7. **Advances** period dates Monday-aligned to the next window.

For **bingo badges**: awards the role to the first 3 users who completed all 10 stamps. The history-channel summary highlights all 3 winners (no MVP line).

**When to use:** A competition period genuinely ends and you're ready to crown winners. This is the command auto-conclude calls.

> 🤖 **Auto-conclude:** The bot automatically runs this every **15 minutes** when a period's end date has passed (using local time PHT / UTC+8). Errors are logged so the loop never gets stuck.

> 🎯 **Bingo periods** always use a **7-day** interval. Standard badges use **14 days**. Both snap to Monday 00:00 PHT.

> 📊 **Progress bar:** `/conclude` (and other long-running commands) edits a textual progress bar so you can watch each badge complete in real time. Tune the edit frequency with `/settings progress_interval:<N>` (default 25).

Requires confirmation.

---

### Data & Sync Commands

---

#### `/resync`
> Re-read the entry channel, sync the database, and clean stale reactions.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |
| `since_date` | No | Only resync from this date onward (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |

**What it does:**
- Scans every message in the entry channel (within the date range).
- Creates DB entries for any missing messages with images.
- Fixes `created_at` timestamps on existing entries.
- Removes stale/duplicate reactions, keeping only the authoritative manager reaction.
- Ensures bot's ❌/✅ placeholder reactions are present.
- Syncs DB approval state to match the actual reactions.
- Refreshes the Challenger role and stats display.

**Date range priority (READ THIS FIRST):**

The resync uses **exactly one** date filter, picked in this order. Whichever applies first **completely ignores** the others:

1. **`since_date` argument** — if you pass it. Wins over everything.
2. **Per-badge period dates** (set via `/setperiod`). Wins over global start date.
3. **Global start date** (set via `/setstartdate`). Used **only when both period start and period end are empty** for that badge.
4. **All history** — only if none of the above are set.

> ⚠️ **Common gotcha:** if you set a period to a *future* window (e.g. next Monday → next Sunday), `/resync` will scan that future window and find nothing. Setting `/setstartdate` does **not** override an already-set period — period wins. To pull entries from a different range without changing your period, use `since_date`:
> ```
> /resync badge_name: All Badges since_date: 2026-04-27
> ```

**What it does:**
- Scans every message in the entry channel (within the date range chosen above).
- Server-side filters via Discord's `after`/`before` so it only fetches in-period messages — fast even on huge channels.
- Creates DB entries for any missing messages with images.
- Fixes `created_at` timestamps on existing entries.
- Removes stale/duplicate reactions, keeping only the authoritative manager reaction.
- Ensures bot's ❌/✅ placeholder reactions are present.
- Syncs DB approval state to match the actual reactions.
- Refreshes the Challenger role and stats display.

**Live progress bar:** While resyncing, the bot edits its message every N items (default 25, configurable via `/settings progress_interval`). For "All Badges" the bar shows badge X/Y plus per-message scan progress underneath, so you always know it's working.

**Cancellable:** `/resync` registers in the task registry. If it's stuck or scanning the wrong range, run `/stoptask` to list, then `/stoptask task_id:<id>` to cancel.

Use this after the bot was offline, or to fix any data inconsistencies. Approvals (✅) made in a prior period **automatically count** when an entry is included in a new period — no re-reaction is needed.

---

### Cleanup Commands

---

#### `/purge`
> Delete messages in the current channel.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `count` | No | Number of messages to delete (default: up to 1000) |
| `start_date` | No | Only delete from this date onward |
| `end_date` | No | Only delete up to this date |

Requires confirmation. Useful for clearing out old messages in stats or entry channels.

---

#### `/purgereacts`
> Remove ALL reactions from messages in entry channels.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |
| `count` | No | Number of messages to process (default: all) |
| `start_date` | No | Only process from this date onward |
| `end_date` | No | Only process up to this date |

Requires confirmation. After purging reactions, run `/resync` to re-add bot reactions and sync approval state.

---

#### `/deleteentries`
> Permanently delete database entries. Pick a `mode`. (Replaces the old `/purgeentries` — that command no longer exists.)

| Parameter | Required | Description |
|-----------|----------|-------------|
| `mode` | **Yes** | `outside-period`, `range`, or `ids` |
| `badge_name` | depends | Required for `outside-period` and `range`; ignored for `ids` |
| `start_date` | depends | Required for `range`; `YYYY-MM-DD` or `YYYY-MM-DD HH:MM` |
| `end_date` | depends | Required for `range`; `YYYY-MM-DD` or `YYYY-MM-DD HH:MM` |
| `message_ids` | depends | Required for `ids`; comma-separated (e.g. `123,456`) |

**Modes:**

- **`mode:outside-period`** — Cleanup. Hard-deletes all entries that fall *outside* the current period for the chosen badge(s), plus any soft-deleted entries. Useful when `/conclude` didn't run for some reason. Pick a badge or "All Badges".
- **`mode:range`** — Surgical. Hard-deletes entries *within* a date range for the chosen badge(s). Shows a preview count before you confirm. Pick a badge or "All Badges". At least one of `start_date` / `end_date` is required.
- **`mode:ids`** — Targeted. Hard-deletes the exact entries matching the comma-separated `message_ids`. Badge selection is ignored.

**⚠️ Destructive — cannot be undone.** All modes require confirmation. Leaderboards auto-refresh after deletion. Run `/resync` afterward if channel reactions need cleanup.

---

### Admin Lookup Commands

---

#### `/userstats`
> View detailed stats for a specific team member.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `member` | **Yes** | The Discord member to look up |
| `badge_name` | No | Badge type, or "All Badges" for all |

Shows the same stats as `/mystats` but for any member. Admin only.

---

### Stopping a Stuck or Long Task

#### `/stoptask`
> List or cancel a running long task (resync, conclude, reset, purgereacts).

| Parameter | Required | Description |
|-----------|----------|-------------|
| `task_id` | No | Task ID to cancel. Omit to list all running tasks. |

**Listing running tasks** (no arg):

```
🛠️ Running tasks:
• `a1b2c3d4` — /resync All Badges (by jave, running 47s)
• `e5f6g7h8` — /conclude weekly_bingo (by jave, running 12s)

Cancel one: /stoptask task_id:<id>
```

**Cancelling** (`task_id:<id>`):
- Sends `asyncio.Task.cancel()` to the running coroutine.
- The task stops at its next `await` point and posts a final "⏹️ cancelled by admin" message in its own channel.
- Database/role state already committed before the cancel point is **not** rolled back. Treat cancel as "stop here, don't undo".

**When to use:** A `/resync All Badges` is taking forever, you want to abort. A `/conclude` was triggered with the wrong badge. A `/purgereacts` is hammering rate limits.

The long-running command's final message includes a `task_id:` line at the end, so you can copy that ID directly.

---

### Bot Configuration

---

#### `/settings`
> View or toggle bot feature settings.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `feature` | No | Feature to toggle (omit to view all) |
| `is_enabled` | No | `Enable` or `Disable` |
| `progress_interval` | No | Numeric: edit progress bar every N items (default 25, must be > 0) |

**Available feature toggles:**

| Feature | Default | Description |
|---------|---------|-------------|
| **Entry Feedback** | ✅ On | Bot replies "This is your Nth entry" when you submit |
| **Leaderboard Updates** | ✅ On | Auto-update the stats channel embed on changes |
| **Role Assignment** | ✅ On | Auto-assign/remove Challenger and Holder roles |
| **Reaction Tracking** | ✅ On | Bot adds ❌/✅ placeholder reactions on new entries |
| **Auto Welcome** | ❌ Off | Auto-welcome new trialists in chat |
| **Auto Trialist** | ❌ Off | Auto-assign Trialist role on join |

**Numeric settings:**

| Setting | Default | Description |
|---------|---------|-------------|
| **progress_interval** | 25 | How often progress bars edit during long-running commands (lower = smoother, but Discord rate-limits at ~5 edits/5sec). Used by `/resync`, `/reset` (all), `/conclude`, `/purgereacts`. |

- Run `/settings` with no parameters to see all current toggle states **and** the current `progress_interval`.
- Run `/settings <feature>` to see the current state of a specific feature.
- Run `/settings <feature> Enable/Disable` to change a toggle.
- Run `/settings progress_interval:10` to make progress bars update more frequently.

---

## Quick Reference

### Chatter Commands
| Command | Description |
|---------|-------------|
| `/mystats` | View your personal stats |
| `/myentries` | List your entries with status |
| `/leaderboard` | View detailed leaderboard |
| `/badges` | List all active badges and channels |
| `/bingostamps` | View bingo stamp challenges |
| `/bingostats` | View your bingo progress |
| `/bingoleaderboard` | Bingo progress leaderboard |

### Manager / Admin Commands
| Command | Permission | Description |
|---------|------------|-------------|
| `/setperiod` | Admin | Set/view period dates |
| `/setstartdate` | Admin | Set global start date |
| `/reset` | Admin | Archive & reset a period |
| `/conclude` | Admin | Full end-of-period flow with role awards |
| `/resync` | Admin | Sync DB with channel messages |
| `/purge` | Elevated | Delete channel messages |
| `/purgereacts` | Elevated | Remove reactions from entry messages |
| `/deleteentries` | Admin | Hard-delete DB entries (mode: outside-period, range, or ids) |
| `/userstats` | Admin | View any member's stats |
| `/settings` | Admin | Toggle bot features |
| `/stoptask` | Admin | List / cancel running long tasks (resync, conclude, etc.) |
| `/welcome` | Admin | Welcome members with Chatter mention |
| `/setrole` | Admin | Set member to Chatter or Trainee |

### Permission Levels
| Level | Who |
|-------|-----|
| **Admin** | Server administrator, Chat Manager role, Bot Admin role, or Command Access role |
| **Elevated** | Admin-level **or** Chatter role |
| **Everyone** | Any server member |

### Response Visibility (ephemeral vs public)

Most commands now respond **publicly** so admin actions are visible/auditable. Only **personal noise** stays ephemeral (you-only).

| Visibility | Commands |
|------------|----------|
| **Ephemeral (you only)** | `/mystats`, `/myentries`, `/bingostats`, plus all permission-denied / validation errors |
| **Public** | Everything else: `/leaderboard`, `/badges`, `/bingostamps`, `/bingoleaderboard`, `/userstats`, `/setperiod`, `/setstartdate`, `/settings`, `/setrole`, all admin commands |

> Validation/error messages (e.g. "Invalid date format", "You don't have permission") are always ephemeral so they don't clutter the channel.

---

*Need help? Contact a server admin or check the entry channel pins for badge-specific instructions.*

---

## 🪵 Logs & Debuggability

The bot writes structured logs to **both** stdout and `bot.log` (rotating, ~5 MB × 3).

- **Format:** `2026-04-28 14:00:01 [INFO] mmhelper.commands.badge_commands: ...`
- **Level:** controlled by `LOG_LEVEL` in `.env` — set to `DEBUG` for verbose traces, `INFO` (default), `WARNING`, or `ERROR`.
- **Existing `print()` statements are kept** for backwards compatibility with existing operator habits; logs add structured detail on top.
- **Auto-conclude debug:** every 15-minute tick logs which badges were checked and whether each was due. Errors are caught and logged but never break the loop.
- **Resync debug:** start/end of each resync logs scanned/new/updated counts.

---

## 🆕 New Member Auto-Role & Welcome

When a new member joins the server, the bot automatically:
1. **Assigns the Trialist role** (if `TRIALIST_ROLE_ID` is set in `.env`).
2. **Sends a welcome message** (if the "Auto Welcome" feature is enabled via `/settings`).

---

## 💬 Smart Auto-Responses

The bot can automatically reply to casual messages using regex pattern matching.

**Built-in triggers:** greetings (hi/hello/hey), thanks, "who's your daddy", "who is the best", "good bot", "bad bot".

**Features:**
- 🔀 Randomly picks from multiple possible responses
- 👑 Optional `creator_responses` list for special replies to the bot creator
- 📝 Supports `{user}` (mention) and `{name}` (display name) placeholders
- ⏱️ 5-second per-user cooldown to prevent spam
- 🎯 Regex-based partial matching (or exact match with `"exact": True`)

To customize triggers, edit the `CUSTOM_RESPONSES` list in `commands/badge_events.py`.

---

### `/welcome`
> Send a welcome message for one or more members (admin only).

| Parameter | Required | Description |
|-----------|----------|-------------|
| `member1` | **Yes** | Member to welcome |
| `member2`–`member5` | No | Additional members to welcome |

Sends:
> 👋 Welcome @user1, @user2! Say hi to @Chatter!

---

### `/setrole`
> Set a member to Chatter or Trainee role (admin only).

| Parameter | Required | Description |
|-----------|----------|-------------|
| `member` | **Yes** | The member to change |
| `role` | **Yes** | `Chatter` or `Trainee` |

- Assigning **Chatter** automatically removes Trainee (and vice versa).
- Requires `CHATTER_ROLE_ID` and/or `TRIALIST_ROLE_ID` in `.env`.
