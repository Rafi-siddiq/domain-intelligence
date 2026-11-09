# Domain Intelligence: Age, WHOIS, DNS & Wayback

Check **any list of domains** in one run and get a full report for each: **domain age and registration date**, registrar, expiry date and status (RDAP, the official successor to WHOIS), **name servers and DNS records**, **email provider** (Google Workspace, Microsoft 365 and others), **SPF and DMARC policy**, the **first and last Wayback Machine capture**, the website's HTTP status, final URL, title and description, and the **SSL certificate** issuer and expiry. Export to JSON, CSV or Excel.

Every value comes from official, public sources: the domain registries' RDAP servers, DNS, the Internet Archive and the website itself. No login, no browser, no proxies.

## What can this domain checker do?

- 📅 **Domain age and WHOIS data:** registration date, age in years, last change, expiry date and days left, registrar and its IANA ID, registry status codes and DNSSEC.
- 🌐 **DNS records:** IPv4 and IPv6 addresses, name servers, MX hosts and all TXT records (site verifications included).
- ✉️ **Email setup:** which email provider the domain uses, whether SPF is published, and the DMARC policy (none, quarantine or reject).
- 🕰️ **Wayback Machine history:** first and most recent capture, with links to both. A first capture years before the registration date usually means the domain had an earlier owner.
- 🔒 **Website and SSL:** HTTP status, where the home page redirects to, page title and meta description, and the SSL certificate issuer, expiry and days left.
- 📋 **Paste anything:** domains, website URLs or email addresses. Each is reduced to its domain (`https://www.apify.com/store` → `apify.com`, `info@ycombinator.com` → `ycombinator.com`) and duplicates are checked once.
- 🆓 **Invalid entries are free.** You pay per domain report.

## Who uses it?

- **SEO and domain investors** checking domain age, history and expiry before buying expired or aged domains.
- **Sales and lead-generation teams** enriching company lists with email provider, website status and company age.
- **Fraud, trust and security teams** flagging newly registered domains, missing DMARC, expiring certificates and parked sites.
- **IT and agencies** auditing a portfolio of client domains for expiry dates, DNS and SSL.

## How to check domains

1. Add **Domains**, one per line (URLs and email addresses work too).
2. Optionally switch off sections you don't need (DNS, Wayback, website) for faster runs.
3. Click **Start** and download the results.

## Input example

```json
{
    "domains": ["stripe.com", "https://www.apify.com/store", "info@ycombinator.com", "bbc.co.uk"],
    "includeDns": true,
    "includeWayback": true,
    "includeWebsite": true
}
```

## Output example

A real result (some long lists shortened):

```json
{
    "resultType": "domain",
    "query": "https://www.apify.com/store",
    "domain": "apify.com",
    "registered": true,
    "createdAt": "2009-06-02T17:14:10.000Z",
    "domainAgeYears": 17.4,
    "updatedAt": "2026-05-16T16:53:04.000Z",
    "expiresAt": "2035-06-02T17:14:10.000Z",
    "daysToExpiry": 3127,
    "registrar": "Amazon Registrar, Inc.",
    "registrarIanaId": "468",
    "status": ["client transfer prohibited"],
    "nameservers": ["ns-1225.awsdns-25.org", "ns-1928.awsdns-49.co.uk", "ns-449.awsdns-56.com", "ns-839.awsdns-40.net"],
    "dnssec": true,
    "ipv4": ["18.164.96.125", "18.164.96.34", "18.164.96.121", "18.164.96.14"],
    "ipv6": ["2600:9000:2510:e600:9:a03e:6540:93a1"],
    "mxHosts": ["aspmx.l.google.com", "alt2.aspmx.l.google.com", "alt1.aspmx.l.google.com"],
    "mailProvider": "Google Workspace",
    "hasSpf": true,
    "spf": "v=spf1 a mx include:_spf.google.com include:mailgun.org include:amazonses.com include:19497222.spf05.hubspotemail.net -all",
    "dmarcPolicy": "reject",
    "dmarc": "v=DMARC1; p=reject; sp=reject; pct=100; rua=mailto:dmarc-reports@apify.com; ri=604800",
    "txtRecords": ["google-site-verification=XU737OZxx6NvGd3NQK9MRt98qxRMjx3RByq-O0cy16I", "..."],
    "waybackFirstCapture": "2007-05-31T10:15:38.000Z",
    "waybackFirstUrl": "https://web.archive.org/web/20070531101538/http://www.apify.com:80/",
    "waybackLastCapture": "2026-11-04T21:52:54.000Z",
    "waybackLastUrl": "https://web.archive.org/web/20261104215254/https://apify.com/",
    "httpStatus": 200,
    "finalUrl": "https://apify.com/",
    "https": true,
    "server": null,
    "title": "Apify: Marketplace of ready-to-run tools for AI",
    "metaDescription": "Thousands of tools to automate your business. Get real-time web data, track competitors, generate leads, and integrate your apps and AI agents.",
    "sslIssuer": "Amazon",
    "sslValidFrom": "2026-07-03T00:00:00.000Z",
    "sslValidTo": "2027-01-16T23:59:59.000Z",
    "sslDaysLeft": 68,
    "sslValid": true,
    "notes": [],
    "checkedAt": "2026-11-09T03:25:08.858Z"
}
```

A domain that isn't registered comes back with `"registered": false` and empty fields, which is also how you check whether a name is available.

## Use it from AI agents (Claude, ChatGPT, Cursor)

AI assistants can run this Actor as a tool through [Apify's MCP server](https://docs.apify.com/platform/integrations/mcp). Add this server URL to any MCP client:

```
https://mcp.apify.com?tools=rsiddiq95/domain-intelligence
```

Then just ask, for example: *"How old are these 20 domains, who are they registered with, and which ones have no DMARC policy?"* Agent runs cost the same per domain as runs from the console.

## How much does it cost?

Pay per domain report. See the **Pricing** tab. Invalid entries are free. A domain takes a few seconds; 1,000 domains take roughly 15 to 30 minutes with all sections on. The Wayback Machine is the slowest source, so switch it off when you don't need archive dates.

## Limitations

- Some country registries don't publish registration data over RDAP (for example `.io`, `.so`, `.es` and several others). For those, registration date, registrar and expiry are empty and the row says so in `notes`; DNS, email, Wayback and website data still work.
- Many registries hide the owner's name and contact details for privacy, so they aren't included.
- Subdomains are reduced to their registrable domain (`news.bbc.co.uk` → `bbc.co.uk`).
- Website title and SSL come from the home page as served to a normal visitor. Sites that block automated visits may show a 403 status.

## FAQ

**Is this WHOIS?**
RDAP is the official, structured replacement for WHOIS, run by the same registries, and it is what ICANN now requires for generic domains like .com, .net and .org.

**Something isn't working.**
Open an issue on the **Issues** tab with your input.

## Run it

This Actor runs on Apify: https://apify.com/rsiddiq95/domain-intelligence
