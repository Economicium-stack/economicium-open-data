# Submission pack

Where to list Economicium's open data and MCP server, and one place we have
decided not to. Every requirement below was checked against the destination's
own documentation on 2026-08-16, not assumed.

Ordered by effort-to-value.

---

## 1. Google Dataset Search (nothing to submit)

**Status:** already done, just needs crawling.

`https://economicium.com/data/` carries `DataCatalog` schema with 16 `Dataset`
and 32 `DataDownload` entries. Google Dataset Search reads that automatically.

**Action:** resubmit the sitemap in Search Console so `/data/` gets crawled
sooner. Nothing else. No form, no account, no gatekeeper.

Highest value on this page and the only one with zero friction. Its audience is
academic, the same audience as the library and university prospects in the
outreach list.

---

## 2. MCP server directories

The server is **live and verified**:

```
POST https://economicium-mcp.economicium.workers.dev/mcp
  -> serverInfo: {"name":"economicium","version":"1.0.0"}
  -> tools/list returns the calculator tools
```

Both destinations below exist specifically so developers can list their own
servers. The official registry authenticates you as the owner before it will
accept an entry. Self-submission is the intended mechanism here, not a
loophole, which is what separates these from item 3.

### 2a. mcpservers.org

`wong2/awesome-mcp-servers` does **not** accept pull requests. Its README
directs submissions to <https://mcpservers.org/submit>. A web form, so no
packaging work.

Suggested copy:

> **Name:** Economicium
> **URL:** https://economicium-mcp.economicium.workers.dev/mcp
> **Description:** Free trading and personal-finance calculators as MCP tools:
> position sizing, risk/reward, pip value, margin, compounding, RMD, I bonds,
> inflation and real wages. Computed from official public data. No API key, no
> signup, no rate limit.

### 2b. Official registry (registry.modelcontextprotocol.io)

Prepared entry: `mcp-server.json` in this folder.

**Blocker found.** Publishing requires namespace authentication, and the
namespace decides what else is needed:

- `io.github.Economicium-stack/...` authenticates via GitHub, but the
  `repository` field must point at a **public** repo, and
  `Economicium-stack/economicium` is private. Not usable as-is.
- `com.economicium/...` authenticates by proving control of `economicium.com`
  with a DNS TXT record. No repo required, and the namespace matches the brand.

The prepared entry uses the DNS route for that reason. If you would rather go
the GitHub route, `worker/mcp-server/` is 340 lines, was scanned for secrets and
is clean, so publishing it as its own public repo is safe and arguably reads as
more trustworthy in a directory.

**Worth doing either way:** the public URL is a `workers.dev` subdomain. A
custom domain such as `mcp.economicium.com` would look considerably more
credible in a permanent public listing. That DNS record does not exist yet.

---

## 3. Awesome Public Datasets: decided against

**Decision, 2026-08-16: we are not submitting. Do not revive this.**

The route itself was worked out and is not the obvious one. Contributions do
**not** go to `awesomedata/awesome-public-datasets`, whose README is
auto-generated (recent commits are all bot `Update README sha` entries, human
PRs from June still open in August). They go to `awesomedata/apd-core`.

None of that matters, because of this, quoted verbatim from their CONTRIBUTING:

> No advertisement! No Spam! No reputation promotion!

Our reason for wanting the listing was distribution and backlinks. That is
reputation promotion by their own definition, whatever the dataset's merits, and
the fact that their Economics folder already contains many company-published
indexes is not a justification for adding another.

The prepared entry has been deleted rather than left here to be found and filed
later.

**If someone else** finds these datasets genuinely useful and submits them, that
is legitimate and outside our control. We simply should not be the ones filing
it.

**A second reason it was a poor target anyway:** GitHub applies `rel="nofollow"`
to links in README markdown, so a merged entry passes no link equity at all. The
only value would have been human discovery. Small upside, real rule against it.

---

## Files here

| File | For |
|---|---|
| `mcp-server.json` | Official MCP registry, DNS namespace route |
