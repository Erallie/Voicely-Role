# Voicely Role

Voicely Role watches selected Discord voice channels and pings a selected role when a configured number of counted, non-bot users is reached. Server managers can exclude specific users from all threshold counts.

Each notification/channel pair is independent. This allows several notifications on the same voice channel, such as:

- 2 users: ping `@Casual Players`
- 4 users: ping `@Gaming`
- 8 users: ping `@Large Group`

After a notification triggers for a voice channel, that notification will not trigger there again until the channel becomes completely empty.

## Commands

- `/voicely-role add` — Create a notification with dropdowns and a details modal.
- `/voicely-role remove` — Select and remove a saved notification.
- `/voicely-role list` — List saved notifications.
- `/voicely-role edit-message` — Change a notification's custom message.
- `/voicely-role exclude-user user:@User` — Exclude a mentioned user from all threshold counts.
- `/voicely-role include-user user:@User` — Make an excluded user count again.
- `/voicely-role excluded-users` — List the server's excluded users.
- `/voicely-role admin-roles` — Select roles allowed to manage notifications. Requires Discord Administrator permission.

Discord Administrators can always manage notifications. The configured Voicely Role admin roles can also add, remove, list, and edit notifications and manage excluded users.

## Invite

Invite Voicely Role to your server using [this invite link](https://discord.com/oauth2/authorize?client_id=1527731147428073493)!

## Message placeholders

Custom messages support:

- `{role}` — role mention
- `{channel}` — voice channel mention
- `{channel_name}` — voice channel name without a mention
- `{count}` — current number of counted, non-bot users
- `{threshold}` — configured threshold

Default message:

```text
🔊 {role} There are now **{count} people** in {channel}!
```

## Excluded users

Excluded users are ignored for every notification in the server. For example, if a voice channel contains two regular users and one excluded user, its count is `2`. This is useful if you have alt accounts that you use the join voice channels.

An excluded user also does not keep a notification armed. If all counted users leave and only excluded users remain, the effective count is zero and notifications for that channel re-arm. Use the slash command's `user` field to type or paste an `@mention`.

## Restart behavior

When the bot starts:

- Empty watched channels are re-armed.
- Occupied channels below a notification's threshold remain armed and can trigger when the threshold is reached.
- Occupied channels already at or above the threshold are marked as triggered without sending a startup ping.

Settings are stored in `voicely-role.db`.
