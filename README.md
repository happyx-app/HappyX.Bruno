<div align="center">

<a href="https://github.com/happyx-app/HappyX"><img src="https://raw.githubusercontent.com/happyx-app/HappyX/main/docs/images/logo.svg" alt="HappyX logo" width="72" height="72"></a>

# HappyX.Bruno

The API collection of **[HappyX](https://github.com/happyx-app/HappyX)**, the Discord bot that asks your team how they
feel every working day and turns the answers into reports.

[![Bruno](https://img.shields.io/badge/Bruno-3-F4AA41?style=flat-square)](https://www.usebruno.com/)

[HappyX](https://github.com/happyx-app/HappyX) ·
[Api](https://github.com/happyx-app/HappyX.Api) ·
[Bot](https://github.com/happyx-app/HappyX.Bot) ·
[Web](https://github.com/happyx-app/HappyX.Web) ·
**Bruno**

</div>

> [!TIP]
> New here? Start with the [main HappyX README](https://github.com/happyx-app/HappyX): what HappyX
> does, screenshots, the architecture and how to self-host the whole stack.

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

| Folder / file | Routes | Auth |
| --- | --- | --- |
| `health.yml` (collection root) | `GET /health` | none |
| `Bot API (v1)` | `/v1/...`, what the Discord bot calls | `Authorization: Bearer {{apiKey}}` |
| `Web dashboard` | `/web/...`, what the web calls | `Cookie: happyx_session={{sessionCookie}}` |

`/v1` and `/health` aren't published on the web domain (nginx only forwards `/api/web/`), and the
stack binds the API's port (8083 by default) to the server's `127.0.0.1` only. To reach them from
your machine in `Production`, open an SSH tunnel first and leave `apiUrl` as
`http://localhost:8083`:

```sh
ssh -N -L 8083:127.0.0.1:8083 you@your-server
```

The `/web` routes go through the public dashboard, so set `webApiUrl` to `https://<your domain>/api`.
The Discord OAuth callback (`/web/auth/callback`) isn't in the collection: only Discord calls it.

## Keep it in sync

Any change to the API's routes or request bodies comes with the matching change here.

## License

[MIT](LICENSE).
