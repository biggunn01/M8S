# Firestore Schema - M8S

This file describes the Firestore collections used by Meta8 Showdown V2.
It is for code/security audit context only. No real user/player data is included.

## adminMessages
Admin-created messages or announcements shown inside the game/admin tools.

Known fields:
- icon
- message
- notifLog

Audit notes:
- Check who can create/edit/delete admin messages.
- Make sure regular players cannot write fake admin messages.

## collections
Appears to store collection/NFT/project metadata used by the game.
Known fields:
- active (boolean)

Audit notes:
- Check whether this data is public read-only or admin-managed.
- Players should not be able to modify collection metadata.

## config
Global game configuration.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Important security collection.
- Players should not be able to edit game settings, rewards, timers, score rules, or admin flags.

## ladderRuns
Likely stores ladder/leaderboard run records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check whether score/run submissions can be faked from the browser.
- Validate ownership and limits.

## live_wire_rooms
Live Wire room/session data.
Known indexed fields:
- status
- createdAt
- __name__

Audit notes:
- Check who can create rooms.
- Check who can update room status.
- Make sure completed/closed rooms cannot be manipulated.

## lw_lottery
Live Wire lottery data.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check randomness, eligibility, duplicate entries, and write permissions.

## lw_lottery_broadcast
Broadcast records for Live Wire lottery events.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Likely should be admin/server controlled.

## lw_scores
Live Wire score/leaderboard records.
Known indexed fields:
- weekId
- top100
- score
- __name__

Audit notes:
- High-risk collection.
- Check whether users can submit arbitrary scores.
- Check whether weekId/top100/score can be edited after submission.
- Confirm leaderboard queries match the intended scoring rules.

## lw_stats
Live Wire stats.
Known fields:
- Unknown from current screenshot.

Audit notes:
- Check if stats are derived/server-controlled or client-writable.

## lwRolls
Live Wire roll records.

Known indexed fields:
- weekId
- score
- __name__

- Audit notes:
- Check whether roll outcomes are client-generated or server-validated.
- Check duplicate/replay prevention.

## matchEvents
Match event logs.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check event ownership.
- Check whether users can spoof match events.

## meta
General metadata.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Usually should be read-only to players.

## packPurchases
Pack purchase records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- High-risk collection.
- Check payment/purchase validation.
- Players should not be able to create fake purchase records.

## playerProfiles
Player profile records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Users should only edit safe fields on their own profile.
- Protected fields like score, admin, balance, inventory, rewards, wins, losses, or rank should not be freely writable.

## pvp_matches
PvP match records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check match ownership.
- Check whether either player can force wins/losses.
- Check completion and replay edge cases.

## pvp_queue
PvP matchmaking queue.

Known indexed fields:
- matchId
- uid
- __name__

Audit notes:
- Check whether users can queue as another uid.
- Check duplicate queue entries.
- Check stale queue cleanup.

## riders
Rider/player/avatar data.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check whether users can only modify their own rider data.
- Check if rarity/stats/power values are protected.

## rooms
Room/session records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check create/update permissions.
- Check room lifecycle: open, active, complete, cancelled.

## sessions
Game session records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check session ownership.
- Check whether scores/results are client-trusted.

## stats
General stats.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Usually should be derived or protected from direct player writes.

## testerFeedback
Tester feedback submissions.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Can probably allow user create.
- Should limit spam/abuse if public.

## tournaments
Tournament records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Admin-controlled.
- Players should not be able to modify tournament rules, entrants, prizes, or results.

## users
User records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Users should only read/write their own safe profile fields.
- Admin/status/reward fields should be protected.

## winStreakRuns
Win streak run records.

Known fields:
- Unknown from current screenshot.

Audit notes:
- Check whether streaks can be faked, replayed, or edited from the browser.

If the Firestore schema file has missing/unknown fields, infer any used collections and field names from `index.html` and `firestore.rules`. Flag any collection where the code/rules reference fields that are not documented.

