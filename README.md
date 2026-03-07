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

### Standard Badges
Entry-count based competitions. The user with the most approved entries wins.

| Badge | Description |
|-------|-------------|
| **Notes Paramedic** | Save and submit fan notes |
| **Renewal Reaper** | Close resubscriptions |
| **Consistency Machine** | Consistent daily performance |
| **Buyer Reviver** | Revive cold or lapsed buyers |

### Bingo Badge
A stamp-collection challenge. Complete all 10 unique stamp challenges to win.

| Badge | Description |
|-------|-------------|
| **Weekly Bingo** | Complete all 10 stamp challenges to earn a Spin of the Wheel |

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

> 💡 When a period end date is reached, the bot **auto-concludes** the badge every 30 minutes.

---

#### `/setstartdate`
> Set, view, or clear the **global start date** used as a default for resync and filtering.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `date` | No | `YYYY-MM-DD`, `YYYY-MM-DD HH:MM`, or `clear` |

- **View:** Run with no parameter.
- **Set:** Provide a date. Used as the fallback when no per-badge period is set.
- **Clear:** Pass `clear` to remove it.

---

#### `/reset`
> Reset a badge period — archive summary to history, soft-delete entries.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |

**What it does:**
1. Posts a full period summary embed to the badge's **history channel**.
2. Soft-deletes all entries in the current period.
3. Automatically advances period dates by the configured interval.

Requires confirmation (✅ / ❌ buttons). Does **not** award the Badge Holder role — use `/conclude` for that.

---

#### `/conclude`
> Conclude a period — award Badge Holder, remove Challengers, archive, and reset.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |

**What it does (for each badge):**
1. **Awards** the 🏅 Badge Holder role to the #1 ranked user(s). If there's a tie, all tied users receive the role.
2. **Removes** the 🏆 Challenger role from everyone (period is over).
3. **Posts** a full period summary to the history channel, including the winner announcement.
4. **Sends** a conclusion announcement to the entry channel.
5. **Soft-deletes** all entries in the period.
6. **Hard-deletes** old entries outside the period (automatic cleanup).
7. **Advances** the period dates to the next window.

For **bingo badges**: awards the role to the first 3 users who completed all 10 stamps.

> 🤖 **Auto-conclude:** The bot automatically runs this every 30 minutes when a period's end date has passed.

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

**Date range priority:** `since_date` parameter → per-badge period dates → global start date → all history.

Use this after the bot was offline, or to fix any data inconsistencies.

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

#### `/purgeentries`
> Permanently delete database entries — outside current period, by date range, or by specific message IDs.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `badge_name` | No | Badge type, or "All Badges" for all |
| `start_date` | No | Delete entries from this date onward (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |
| `end_date` | No | Delete entries up to this date (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |
| `message_ids` | No | Comma-separated message IDs (e.g. `123456789,987654321`) |

**Three modes** (automatically detected from which parameters you provide):

1. **No dates/IDs** → Deletes all entries **outside** the current period (+ soft-deleted). Default cleanup mode.
2. **`start_date` / `end_date`** → Deletes entries **within** the given date range. Requires `badge_name`. Shows preview count before confirming.
3. **`message_ids`** → Deletes specific entries by message ID, regardless of badge type.

**⚠️ Destructive — cannot be undone.** Requires confirmation. Leaderboards auto-refresh after deletion.

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

### Bot Configuration

---

#### `/settings`
> View or toggle bot feature settings.

| Parameter | Required | Description |
|-----------|----------|-------------|
| `feature` | No | Feature to toggle (omit to view all) |
| `is_enabled` | No | `Enable` or `Disable` |

**Available feature toggles:**

| Feature | Default | Description |
|---------|---------|-------------|
| **Entry Feedback** | ✅ On | Bot replies "This is your Nth entry" when you submit |
| **Leaderboard Updates** | ✅ On | Auto-update the stats channel embed on changes |
| **Role Assignment** | ✅ On | Auto-assign/remove Challenger and Holder roles |
| **Reaction Tracking** | ✅ On | Bot adds ❌/✅ placeholder reactions on new entries |

- Run `/settings` with no parameters to see all current toggle states.
- Run `/settings <feature>` to see the current state of a specific feature.
- Run `/settings <feature> Enable/Disable` to change it.

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
| `/purgeentries` | Admin | Hard-delete DB entries (outside period, date range, or by ID) |
| `/userstats` | Admin | View any member's stats |
| `/settings` | Admin | Toggle bot features |

### Permission Levels
| Level | Who |
|-------|-----|
| **Admin** | Server administrator, Chat Manager role, Bot Admin role, or Command Access role |
| **Elevated** | Admin-level **or** Chatter role |
| **Everyone** | Any server member |

---

*Need help? Contact a server admin or check the entry channel pins for badge-specific instructions.*
