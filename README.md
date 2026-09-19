<div align="center">

<img src="assets/cover.png" alt="App Store Connect through HeyMetra's MCP server" width="100%">

# App Store Connect &times; HeyMetra

**A day of App Store units, proceeds and downloads, per app and country.**

Your subscription revenue lives in App Store Connect. What you paid to get those subscribers does not. Ask about both in the same sentence.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.heymetra%2Fheymetra-1f6feb)](https://registry.modelcontextprotocol.io/v0/servers/com.heymetra%2Fheymetra/versions)
[![Transport](https://img.shields.io/badge/transport-Streamable_HTTP-444)](https://modelcontextprotocol.io/)
[![Auth](https://img.shields.io/badge/auth-OAuth_2.1-444)](https://heymetra.com/security/)
[![Connector page](https://img.shields.io/badge/heymetra.com-app-store-connect-1f6feb)](https://heymetra.com/connectors/app-store-connect/)

```
https://mcp.heymetra.com/mcp
```

</div>

---

## Ask it things like

> How many downloads did each app get yesterday?

> Which countries bought the most yesterday?

> What were the proceeds on 1 September, app by app?

> Which apps are on this account, and what are their bundle IDs?

No dashboard, no export, no query language. You ask in the assistant you already use and the answer comes back with the account it came from.

## Connect App Store Connect

**1. Generate a TEAM key, not an individual one**

In App Store Connect go to Users and Access → Integrations → App Store Connect API. Stay on the Team Keys tab. Apple's individual keys cannot read Sales and Finance at all, so a key made there will not answer for sales however its role is set.

> Generating a team key requires the Admin role, so if that tab will not let you create one, somebody with Admin has to.

**2. Give the key a role wide enough for what you want to ask**

Apple decides what a key can reach from the role you pick here, and the role cannot be changed afterwards. Sales figures need a role with report access; reading your App Store reviews needs one that covers them. Admin covers everything HeyMetra reads.

> Worth knowing before you choose: an App Store Connect team key reaches EVERY app on the account whatever role it has — Apple offers no way to limit one to a single app.

**3. Download the .p8 file — this is your only chance**

Apple keeps no copy. If it is lost the key is gone and you generate a new one. Note the Key ID beside it and the Issuer ID shown above the list; the Issuer ID is the same for every key on the account.

**4. Copy your Vendor Number for sales figures**

It is in App Store Connect under Payments and Financial Reports, an eight-digit number at the top. Without it HeyMetra can still read your apps and your reviews; only sales reports need it.

**5. Paste all four into HeyMetra**

On the Connections screen choose App Store Connect. The Issuer ID and Key ID go in as they are, and the private key is the WHOLE .p8 file including its BEGIN and END lines. HeyMetra proves the key works before saving anything.

**6. Add HeyMetra to the assistant you use**

Claude, ChatGPT, Cursor or Codex, with the details HeyMetra gives you. The App Store Connect tools appear there once the connection is saved.

## Then add HeyMetra to your assistant

Add HeyMetra once and it is there in every conversation. The address is the same everywhere:

```
https://mcp.heymetra.com/mcp
```

### One command

```bash
npx add-mcp https://mcp.heymetra.com/mcp
```

[`add-mcp`](https://www.npmjs.com/package/add-mcp) is a third-party installer that writes the configuration for Claude Code, Codex, Cursor, Antigravity, VS Code and seventeen other agents. It infers the name from the address, so the server lands as `heymetra`. Run against this endpoint before it was written here.

### Or by hand

<details>
<summary><b>Claude</b> — Settings → Customize → Connectors → Add custom connector</summary>

Paste the address above into Settings → Customize → Connectors → Add custom connector.

_On Team and Enterprise plans only an owner can add it, under Organization settings._

Full walkthrough: [heymetra.com/mcp/claude/](https://heymetra.com/mcp/claude/)
</details>

<details>
<summary><b>ChatGPT</b> — Settings → Security and login → Developer mode, then chatgpt.com/plugins</summary>

Paste the address above into Settings → Security and login → Developer mode, then chatgpt.com/plugins.

_The endpoint has to include its /mcp path here._

Full walkthrough: [heymetra.com/mcp/chatgpt/](https://heymetra.com/mcp/chatgpt/)
</details>

<details>
<summary><b>Grok</b> — grok.com/connectors → New Connector → Custom</summary>

Paste the address above into grok.com/connectors → New Connector → Custom.

_XAI calls this “bring your own MCP”._

Full walkthrough: [heymetra.com/mcp/grok/](https://heymetra.com/mcp/grok/)
</details>

<details>
<summary><b>Perplexity</b> — Settings → Connectors → Custom connector → Remote</summary>

Paste the address above into Settings → Connectors → Custom connector → Remote.

_Perplexity documents it as a Pro, Max and Enterprise feature._

Full walkthrough: [heymetra.com/mcp/perplexity/](https://heymetra.com/mcp/perplexity/)
</details>

<details>
<summary><b>Claude Code</b> — claude mcp add --transport http</summary>

```bash
claude mcp add --transport http heymetra https://mcp.heymetra.com/mcp
```

_Or a .mcp.json in the project root; /mcp inside a session shows what connected._

Full walkthrough: [heymetra.com/mcp/claude-code/](https://heymetra.com/mcp/claude-code/)
</details>

<details>
<summary><b>Codex</b> — ~/.codex/config.toml</summary>

```toml
[mcp_servers.heymetra]
url = "https://mcp.heymetra.com/mcp"
```

_Under an [mcp_servers.<name>] section, then codex mcp login._

Full walkthrough: [heymetra.com/mcp/codex/](https://heymetra.com/mcp/codex/)
</details>

<details>
<summary><b>Cursor</b> — ~/.cursor/mcp.json, or .cursor/mcp.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "url": "https://mcp.heymetra.com/mcp" }
  }
}
```

_Leave the static OAuth fields empty — they exist for servers that cannot register themselves._

Full walkthrough: [heymetra.com/mcp/cursor/](https://heymetra.com/mcp/cursor/)
</details>

<details>
<summary><b>Antigravity</b> — ~/.gemini/config/mcp_config.json, or .agents/mcp_config.json in a project</summary>

```json
{
  "mcpServers": {
    "heymetra": { "serverUrl": "https://mcp.heymetra.com/mcp" }
  }
}
```

_The key is serverUrl, not url — the one every other JSON client spells differently._

Full walkthrough: [heymetra.com/mcp/antigravity/](https://heymetra.com/mcp/antigravity/)
</details>

## What it may and may not touch

App Store Connect is a read-only source — HeyMetra reads it to answer questions and never changes the account.

Permissions are switched on per connection, and one you leave off is a tool your assistant never sees.

| Permission | What it covers | Changes anything? |
|---|---|---|
| **Apps** | Read the apps on the account. | No, read only |
| **Sales** | Read daily sales and download reports. | No, read only |
| **Store listing** | Read your App Store page as it is written — the name, subtitle, keywords, promotional text and description, in every market. | No, read only |
| **Reviews** | Read the App Store reviews people wrote, their star ratings, and the replies you have already published. | No, read only |

<details>
<summary>What each permission lets an assistant do, in full</summary>

- Lists the apps on your App Store Connect account with their bundle IDs and SKUs.
- Reads what Apple PAID you for one of its fiscal periods, per currency and country — after commission, not sales.
- Reads one day of App Store sales: units, downloads and proceeds per app and country. Apple publishes yesterday's report at the earliest.
- Reads your App Store page as it is written — name, subtitle, keywords and promotional text, per market.
- Reads the App Store reviews for one app — the star ratings, what each reviewer wrote, and the replies you already published. It cannot reply.
</details>

## When something goes wrong

<details>
<summary>Your apps and sales answer, but asking about reviews is refused.</summary>

**Why:** The key's role does not cover customer reviews. Apple fixes what a key can reach when it is created and the role cannot be widened afterwards.

**Fix:** Generate a new team key with a wider role and paste it into this connection with the pencil. The old one can then be revoked in App Store Connect.

</details>

<details>
<summary>Sales are refused while everything else works.</summary>

**Why:** Either the key is an individual key, which Apple does not let read Sales and Finance at all, or the Vendor Number is missing from the connection.

**Fix:** Check the key was made on the Team Keys tab, and that the Vendor Number from Payments and Financial Reports is in the connection.

</details>

<details>
<summary>The private key is rejected when you paste it.</summary>

**Why:** The .p8 was pasted without its first and last lines, or reformatted by a text editor that folded the line breaks.

**Fix:** Open the file in a plain text editor and paste everything, including -----BEGIN PRIVATE KEY----- and the END line.

</details>

<details>
<summary>You cannot find the .p8 file to paste.</summary>

**Why:** Apple lets it be downloaded once and keeps no copy of it.

**Fix:** Generate a new key, download it immediately, and revoke the old one.

</details>

<details>
<summary>Today's sales are missing.</summary>

**Why:** Apple publishes one sales report per day, some hours after the day has ended, so the most recent one available is yesterday's.

**Fix:** Ask about yesterday or earlier. A day with no report yet is reported as not published, never as zero sales.

</details>

## What HeyMetra reads from App Store Connect

Connect with an App Store Connect team key and your MCP client gets three tools: the apps on the account with their bundle IDs and SKUs; one day of sales — units, proceeds and downloads per app and country; and the reviews people wrote, with their star ratings and the replies you have already published, so you can ask which complaints nobody has answered. Apple publishes one sales report per day and yesterday's is the newest, so a month is thirty calls rather than one; ask for the days you need. What the key can reach is decided by the role you give it when you create it. Read-only: no tool changes the account, and HeyMetra cannot reply to a review.

<details>
<summary>About App Store Connect</summary>

App Store Connect is Apple’s platform for managing your iOS apps and viewing sales, subscriptions, and download reports. It’s the source of truth for your Apple revenue and install numbers.
</details>

## One connection, not seven

The reason to read App Store Connect through HeyMetra rather than through a server that only knows App Store Connect is everything else it can answer in the same breath:

**Ads** — [Google Ads](https://heymetra.com/connectors/google-ads/) · [Meta](https://heymetra.com/connectors/meta-ads/)

**Analytics** — [Google Analytics 4](https://heymetra.com/connectors/google-analytics-4/) · [Google Search Console](https://github.com/zeisoft/google-search-console-mcp)

**Ecommerce** — [Shopify](https://heymetra.com/connectors/shopify/) · [Trendyol](https://github.com/zeisoft/trendyol-mcp) · [WooCommerce](https://github.com/zeisoft/woocommerce-mcp)

**Revenue & CRM** — [Stripe](https://heymetra.com/connectors/stripe/) · [HubSpot](https://heymetra.com/connectors/hubspot/) · [Zoho CRM](https://github.com/zeisoft/zoho-crm-mcp) · [Zoho SalesIQ](https://github.com/zeisoft/zoho-salesiq-mcp) · [Zoho Marketing Automation](https://github.com/zeisoft/zoho-marketing-automation-mcp)

**Mobile** — [AppsFlyer](https://github.com/zeisoft/appsflyer-mcp) · [RevenueCat](https://heymetra.com/connectors/revenuecat/) · [Adapty](https://github.com/zeisoft/adapty-mcp) · **App Store Connect**

**Channels** — [Slack](https://github.com/zeisoft/slack-mcp) · [Telegram](https://github.com/zeisoft/telegram-mcp)

The full catalogue is at [heymetra.com/connectors/](https://heymetra.com/connectors/).

## Links

- [App Store Connect connector page](https://heymetra.com/connectors/app-store-connect/)
- [HeyMetra](https://heymetra.com/) — what the product is
- [Setup for every assistant](https://heymetra.com/mcp/)
- [Security and limits](https://heymetra.com/security/)
- [Pricing](https://heymetra.com/pricing/)
- [HeyMetra's own repository](https://github.com/zeisoft/heymetra-mcp)

---

<sub>Built by <a href="https://zeisoft.com">Zeisoft</a>, who make HeyMetra. Not affiliated with App Store Connect. This README is generated from HeyMetra's live connector catalogue and refreshed daily; corrections are welcome as issues.</sub>
