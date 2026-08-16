# Submission pack

Everything needed to list Economicium's open data and MCP server in third-party
directories. Every requirement below was checked against the destination's own
documentation on 2026-08-16, not assumed.

Ordered by effort-to-value. Do them in this order.

---

## 1. Google Dataset Search (nothing to submit)

**Status:** already done, just needs crawling.

`https://economicium.com/data/` carries `DataCatalog` schema with 16 `Dataset`
and 32 `DataDownload` entries. Google Dataset Search reads that automatically.

**Action:** resubmit the sitemap in Search Console so `/data/` gets crawled
sooner. Nothing else. No form, no account, no waiting on a maintainer.

This is the highest-value item on the page and the only one with zero friction.
Its audience is academic, which is the same audience as the 18 library and
university prospects in the outreach list.

---

## 2. MCP server directories

The server is **live and verified**:

```
POST https://economicium-mcp.economicium.workers.dev/mcp
  -> serverInfo: {"name":"economicium","version":"1.0.0"}
  -> tools/list returns the calculator tools
```

### 2a. mcpservers.org

`wong2/awesome-mcp-servers` **does not accept pull requests**. Its README
directs submissions to <https://mcpservers.org/submit>. That is a web form, so
it is the fastest route and needs no packaging work.

Suggested copy for the form:

> **Name:** Economicium
> **URL:** https://economicium-mcp.economicium.workers.dev/mcp
> **Description:** Free trading and personal-finance calculators as MCP tools:
> position sizing, risk/reward, pip value, margin, compounding, RMD, I bonds,
> inflation and real wages. Computed from official public data. No API key, no
> signup, no rate limit.

### 2b. Official registry (registry.modelcontextprotocol.io)

Authoritative but has a real prerequisite. See `mcp-server.json` in this folder
for the prepared entry.

**Blocker found:** publishing requires namespace authentication, and the
namespace determines what else you need.

- `io.github.Economicium-stack/...` authenticates via GitHub, but the
  `repository` field must point at a **public** repo. `Economicium-stack/economicium`
  is private, so it cannot be used as-is.
- `com.economicium/...` authenticates by proving you control `economicium.com`
  via a DNS TXT record. This avoids the private-repo problem entirely and is
  probably the better route, since the namespace then matches the brand.

**Two ways forward, pick one:**

1. **DNS route (recommended).** Add the TXT record the registry asks for, publish
   under `com.economicium/economicium`. No new repo needed.
2. **GitHub route.** Publish `worker/mcp-server/` as its own small public repo.
   The source was scanned and contains no secrets or credentials, so this is safe.
   340 lines, and an open-source MCP server reads as more trustworthy in a
   directory than a closed one.

**Also worth doing either way:** the public URL is a `workers.dev` subdomain.
A custom domain such as `mcp.economicium.com` would look considerably more
credible in a permanent public listing. That DNS record does not exist yet.

---

## 3. Awesome Public Datasets

**Do not PR the repo you would expect to.** `awesomedata/awesome-public-datasets`
(78k stars) has an **auto-generated** README: its recent commits are all bot
entries reading `Update README sha: ...`, and human PRs from June were still
open in August. Submitting there means being ignored.

Contributions go to **`awesomedata/apd-core`**, subtitled "Contribute new data
here!", which is the source the README is generated from.

**Process, from their CONTRIBUTING.md:**

```bash
# fork awesomedata/apd-core, then
git clone https://github.com/<you>/apd-core.git && cd apd-core
cp ../economicium-open-data/SUBMISSIONS/apd-core-Economicium-Open-Data.yml \
   core/Economics/Economicium-Open-Data.yml
pip install -r tests/requirements.txt
./tests/testing.sh          # must pass before opening the PR
```

Only `title`, `homepage` and `category` are validated, and `category` must match
the folder name exactly (`Economics`). The prepared file fills the optional
fields too.

### Two things to weigh first

**Their policy says, verbatim: "No advertisement! No Spam! No reputation
promotion!"** Submitting your own project to earn links is what that rule
forbids. In practice the Economics folder's 53 entries include plenty of
company-published indexes, so enforcement is loose. Submit because the dataset is
genuinely useful to someone doing economics research, and let that be true. The
prepared description is deliberately modest and leads with the sources rather
than the brand.

**Timing:** both repos carry the notice "Primary maintainer on vacation until
Aug 24. Pull requests will be viewed upon my return." Nothing merges before then.

### What this is actually worth

GitHub applies `rel="nofollow"` to links in README markdown, so a merged entry
passes **no link equity**. The value is humans finding the repo, and some of them
citing the datasets from their own sites, where the links do count. That is a
slower and less certain mechanism than a direct backlink, and worth being honest
about before spending effort on it.

---

## Files here

| File | For |
|---|---|
| `apd-core-Economicium-Open-Data.yml` | Awesome Public Datasets, via apd-core |
| `mcp-server.json` | Official MCP registry |
