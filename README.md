# Gateway Tariff Calculator

Answer US import duty questions in Claude Code from a live tariff engine, with the
citation for every figure.

Built and maintained by [Gateway Lines](https://gatewaylines.com), an FMC-licensed NVOCC
and ocean freight forwarder, using the same tariff engine that prices our own shipments.

## Install

**Claude Code**

```
/plugin install gateway-tariff-calculator
```

**Gemini CLI**

```
gemini extensions install https://github.com/xcodesjs/gateway-tariff-plugin
```

**Any other MCP client**

Point it at `https://mcp.gatewaylines.com` and sign in when prompted. Claude and ChatGPT
both discover the sign-in automatically; see
[the setup guide](https://tariff.gatewaylines.com/mcp) for per-client steps.

## Access and sign-in

The first time a tool runs, your client opens a browser to a Gateway sign-in page. There are
two ways through it, and you pick one at that screen.

### Guest — 10 lookups per week, free

Enter an email address. Gateway sends a 6-digit code, you enter it, and you are connected.
No account, no card, nothing to set up.

The limit is 10 answered lookups per rolling 7 days, counted per address. It is a rolling
window, so the tenth lookup frees up exactly seven days after you made it, not at the end
of a calendar week.

Asking for candidate HTS codes does **not** count against it. When you give `landed_cost` a
product description instead of a code, it returns candidates for you to confirm and charges
nothing, because that is a question back to you rather than an answer.

### Gateway freight customer — unlimited

Choose **I ship with Gateway** and sign in with your app.gatewaylines.com account. The
weekly limit comes off entirely. The platform comes with the freight; Gateway earns on the
container, so the tools are not a subscription.

Not a customer yet? [Get a rate](https://gatewaylines.com/quote).

### How the sign-in works

Standard OAuth 2.1. Claude registers itself with Gateway automatically, sends you to the
browser to approve, and receives a scoped token. You never paste a key, a token, or a
header into a config file, and Gateway never sees a password you typed into Claude.

The token is scoped to the three read-only tariff tools and nothing else. Access tokens
expire after an hour and refresh silently. Disconnect from your AI assistant at any time to
stop it refreshing, or email privacy@gatewaylines.com to have outstanding tokens revoked
immediately.

## Tools

| Tool | What it does |
|---|---|
| `landed_cost` | Duty and landed cost for an HTS code and country of origin, including every trade action that stacks: Section 301, Section 232, Section 338, AD/CVD and the rest, plus government fees |
| `classify_hts` | Candidate HTS classifications for a product, with official descriptions and base rates |
| `policy_changes_since` | What changed in US trade policy and what takes effect next, each with its source |

All three are read only. The server holds no shipment, invoice or account data and cannot
change anything.

## What it does not do

`landed_cost` will not price a classification it guessed. Given a product description
rather than an HTS code it returns candidate lines and asks you to confirm one, because
the classification decides the duty and the tariff schedule classifies by what an article
IS, not what it is made of. That step is not charged.

It also refuses to price 4 and 6 digit headings, which carry no rate of their own.

## Accuracy

Figures come from the live US Harmonized Tariff Schedule and published trade actions, and
responses carry the legal reference: Federal Register document numbers, CBP CSMS
bulletins, USTR dockets, HTSUS notes.

They are planning estimates, not customs rulings. Classification is the importer's legal
responsibility. Confirm with a licensed customs broker before entry.

## Examples

```
What will it cost to import $62,000 of cotton t-shirts from India?
Find the HTS code for lithium ion batteries.
What changed in US trade policy since July 1?
I import metal patio furniture from Canada. Does anything change soon?
```

That last one shows the engine is date aware: it returns the duty owed today alongside
any scheduled change and its effective date.

## Privacy Policy

Full policy: <https://gatewaylines.com/privacy> (section 18 covers this connector).

**What is collected.** For guests, the email address you verify, plus each lookup: the
HTS code, country of origin and declared value you asked about, with the time and
originating IP address. For customers, the same lookup details against your account.

**What is not collected.** We do not receive your conversation. The server only ever sees
the specific arguments a tool is called with.

**How it is used.** Lookup records enforce the guest usage limit and let us detect abuse.
A verified guest email is added to our customer relationship records and may be used to
contact you about Gateway freight services; you can opt out at any time via the
unsubscribe link in any message or by emailing privacy@gatewaylines.com.

**Sharing.** Your AI assistant provider is a separate company with its own privacy policy
governing your conversation; Gateway has no access to it. Gateway uses a small number of
service providers to deliver the verification email and store the records above; they are
named in the full privacy policy linked at the top of this section.

**Retention.** Connector lookup records are kept for 24 months for abuse detection and
service analysis. Verification codes are deleted after 10 minutes. Access and refresh
tokens are stored as one-way hashes, never in readable form; access tokens expire after
one hour.

**Your controls.** Disconnect at any time from your AI assistant, which stops the client
refreshing. Email privacy@gatewaylines.com to have outstanding tokens revoked immediately,
or to request access, correction or deletion of your data.

**Contact.** privacy@gatewaylines.com

## Support

<https://help.gatewaylines.com>

## License and ownership

This repository contains only the plugin configuration: a manifest, a pointer to the
hosted server, and this documentation. There is no application code here.

The Gateway Tariff Calculator service, its tariff engine, and its underlying data are
proprietary to Gateway Lines and are **not** open source. You may use and redistribute the
configuration in this repository in order to connect to the service. Use of the service
itself is governed by <https://gatewaylines.com/terms>.

See [LICENSE](LICENSE) for the exact scope.
