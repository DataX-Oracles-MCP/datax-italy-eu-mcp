# DataX Italy & EU Truth Engine — MCP Server (`stdio`)

Zero-dependency **Model Context Protocol (MCP)** `stdio` bridge (`Python 3.9+` standard library only — no `pip install` required) connecting AI agents (Claude Desktop, Cursor, OpenClaw, custom MCP clients) to live official **Italy & EU** registries with non-custodial pay-per-call settlement in **USDC** (Base, Polygon, Solana) and **MiCA EURC** (Base).

- **Live Endpoint:** `https://datax-it.duckdns.org`
- **Machine Discovery:** [`/llms.txt`](https://datax-it.duckdns.org/llms.txt) · [`/mcp.json`](https://datax-it.duckdns.org/mcp.json) · [`/.well-known/agent-card.json`](https://datax-it.duckdns.org/.well-known/agent-card.json) · [`/openapi.json`](https://datax-it.duckdns.org/openapi.json) · [`/.well-known/ai-crawl-pricing.json`](https://datax-it.duckdns.org/.well-known/ai-crawl-pricing.json)
- **Agent Payment Protocol & Wallet Guide:** See [`SKILL.md`](./SKILL.md)

---

## Official Data Sources Indexed

- **Italian Public Procurement (`ANAC BDNCP PVL`):** Real-time tenders (`BANDI` -> `PC`) and contract awards (`RISULTATI` / `AFFIDAMENTI` -> `PA`) with CIG, CPV, award values, and corporate winners (11-digit Partita IVA). Natural-person 16-char Codice Fiscale, emails, and phones stripped per GDPR.
- **Official Gazette (`Gazzetta Ufficiale`):** Serie Generale legislation (`Sec LC`) and 5ª Serie Contratti Pubblici (`Sec PC`).
- **EU Registries:** **EU TED v3** procurement (`ITA`, `Sec TE`), **EU SEDIA** grants (`Sec EU`), and **EU Consolidated Financial Sanctions List (`FSF`, `Sec SF`)**.

---

## MCP Tools Exposed (7 Tools)

| Tool | Price (`USDC` / `EURC`) | Purpose |
| :--- | :---: | :--- |
| `get_pricing` | **Free** | Fetch supported networks, contracts, treasuries, and tier prices. |
| `get_catalog` | **Free** | Check live freshness (`data_version`) and record counts by section. |
| `search_tenders` | **`0.10`** | FTS5 BM25 + BI filter search across Italy & EU registries; returns opaque `item_ref` (`dx_...`). |
| `find_distressed_auctions` | **`0.10`** | Real-estate auction endpoint (populated on Spain node; empty on Italy-only DB). |
| `find_funded_companies` | **`0.10`** | Companies winning Italian public contracts (ANAC PVL) or EU grants. |
| `check_company_risk` | **`0.30`** | Screen 11-digit Partita IVA or company_name across EU FSF sanctions & ANAC/TED awards. |
| `get_tender_detail` | **`0.50`** | Unlocks full verbatim record, winner corporate IDs, CPVs & official URLs from any `item_ref`. |

---

## Quick Setup (Claude Desktop / Cursor)

```json
{
  "mcpServers": {
    "datax-italy-eu": {
      "command": "python3",
      "args": ["/absolute/path/to/mcp_bridge.py"],
      "env": {
        "DATAX_BASE_URL": "https://datax-it.duckdns.org",
        "DATAX_TOKEN": "<unspent-utxo-token-from-issue-token>"
      }
    }
  }
}
```
