# n8n template: WalnutLink A-share Desk

Import `walnutlink-a-share-desk.json` into n8n (Workflows → Import from File), hit
**Test workflow**, and read the answer.

The HTTP Request node calls `POST https://walnutlink.ai/api/ask` with
`{"question": "..."}`. No credential needed.

Two things worth knowing before you run it:

**It can take five minutes.** A question that was researched before returns instantly.
A new one goes into a queue read by a human-plus-agent loop, and the HTTP node is
configured with a 300 000 ms timeout to cover that. The response always tells you the
queue position (`你排第 3 位，大约 15 分钟`) so a timeout is not silent.

**It refuses quotes on purpose.** Ask for a price, a PE or a market cap and the API
returns `410 gone_by_design` with an explanation. This desk only answers *why* a number
moved, traced to a filing. If your workflow needs prices, use a quote API — this is not
one.

Machine-readable rules: https://walnutlink.ai/skill.md
