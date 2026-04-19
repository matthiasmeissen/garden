# AT Protocol

[tags: #atproto #bluesky #open-social #web]

Protocol for decentralised social data. Each user has a **personal data server (PDS)** — a web server storing signed JSON records at `at://` URIs. Records link to each other like hyperlinks. Apps read and write to your repo; they do not own your data.

## Key Ideas

- **Handles are domains you own** (`@alice.com`), not identifiers allocated by a platform.
- **Data is cryptographically signed** — you do not need to trust any relay serving it.
- **"AT" = Authenticated Transfer.** Pronounced "at", not "ay-tee".
- **Apps aggregate over a firehose** (a websocket event stream from all repos) into local caches. The source of truth stays in your repo.
- **Products can be forked.** If an app dies, data survives in users' repos because the app was never the owner.

## The Atmosphere

The ecosystem of apps built on atproto. Bluesky is the largest, but the space is broader:

- **Tangled** — git / social hybrid
- **Leaflet** — publishing
- **Anisota**, **Popfeed** — feed and discovery experiments

An app on atproto is effectively a lens over shared user data, which inverts the usual platform dynamic.

## Repo Inspection Tools

Useful for debugging, exploring, or just seeing what any account's repo looks like in the raw.

- [atproto.at](https://atproto.at) — Taproot, tree explorer for any repo
- [pdsls.dev](https://pdsls.dev) — repo browser plus firehose / jetstream viewer
- [atproto-browser.vercel.app](https://atproto-browser.vercel.app) — browse by handle or DID

## See Also

- [[web|Web]]
