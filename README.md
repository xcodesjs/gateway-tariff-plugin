# Gateway Tariff Calculator

Answer US import duty questions in Claude Code from a live tariff engine, with the
citation for every figure.

Built and maintained by [Gateway Lines](https://gatewaylines.com), an FMC-licensed NVOCC
and ocean freight forwarder, using the same tariff engine that prices our own shipments.

## Install

```
/plugin install gateway-tariff-calculator
```

On first use Claude opens a browser to sign in. Guests verify an email address and get
10 lookups per week; Gateway freight customers sign in with their account for unlimited
access. Nothing is pasted into a config file.

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

## License

MIT. See [LICENSE](LICENSE).
