# HappyX.Bruno

[Bruno](https://www.usebruno.com/) workspace with every call of [HappyX.Api](https://github.com/happyx-app/HappyX.Api).

## Open it

1. Bruno 3 or later → **Open workspace** → this folder.
2. Open the **HappyX API** collection and pick an environment: `Local` or `Production`.
3. Fill the environment's secrets (Bruno keeps their values on your machine, never in these files):
   - `apiKey`: a bot API key whose SHA-256 is in the API's `API_KEY_HASHES`.
   - `sessionCookie`: log in on the web, then copy the `happyx_session` cookie from the
     browser's dev tools (Application → Cookies). It lasts 12 hours.
4. Set `guildId`, `userId` and the other IDs you want to try.

## What's inside

| Folder | Routes | Auth |
| --- | --- | --- |
| `Health` | `GET /health` | none |
| `Bot API (v1)` | `/v1/...`, what the Discord bot calls | `Authorization: Bearer {{apiKey}}` |
| `Web dashboard` | `/web/...`, what the web calls | `Cookie: happyx_session={{sessionCookie}}` |

`/v1` isn't published on the web domain (nginx only forwards `/api/web/`), so in `Production`
set `apiUrl` to the API's port on the server (8083 by default). The Discord OAuth callback
(`/web/auth/callback`) isn't in the collection: only Discord calls it.

## Keep it in sync

Any change to the API's routes or request bodies comes with the matching change here.
