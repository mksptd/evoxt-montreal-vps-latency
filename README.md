# Montreal VPS: how much latency you actually get, what $2.99–$47.99/month buys, and which tier to pick

A Montreal VPS puts Quebec and eastern Ontario users somewhere between 5 and 15 ms from your server. vShield advertises under 5 ms across Quebec, Sable Servers about 5 ms in-province and 8 ms into Ontario, Sucura Networks roughly 13 ms to Toronto and under 15 ms across greater Montreal. Evoxt's ladder starts at $2.99/month for a 512 MB machine, and the tier most projects should actually buy, VM-2 with 2 cores and 4 GB, is $11.99/month.

What follows is the full lineup, which rungs are worth their price and which aren't, and the two things that decide whether a Montreal box feels fast: how the latency figure was measured, and what the monthly price leaves out.

> **Quick pick.** VM-2 (2 vCore, 4 GB RAM, 30 GB storage, $11.99/month) covers a storefront, a small SaaS app or a game server for a handful of players. If the machine only runs a bot, a DNS resolver or a two-person VPN, VM-0.5 at $2.99 does the same job for $9 less every month.
> 👉 [See every Evoxt plan and its current price](https://bit.ly/EvoXt)

## The full Evoxt lineup

Nine plans, priced in USD and billed monthly. There is no hourly billing option anywhere in the list.

| Plan | vCPU / RAM | Storage | Price (USD/mo) | Order |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 vCore / 512 MB | 5 GB | $2.99 | [ Get VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 vCore / 1 GB | — | $4.99 | [ Get VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 vCore / 2 GB | 20 GB | $5.99 | [ Get VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 vCore / 2 GB | 20 GB | $6.95 | [ Get VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 vCore / 4 GB | 30 GB | $11.99 | [ Get VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 vCore / 4 GB | 30 GB | $14.99 | [ Get VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 vCore / 8 GB | 60 GB | $23.99 | [ Get VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 vCore / 8 GB | 60 GB | $29.99 | [ Get VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 vCore / 16 GB | 80 GB | $47.99 | [ Get VM-8](https://bit.ly/EvoXt) |

Prices are before whatever tax your billing address attracts. A dash marks a figure the listing doesn't publish in the same form as the rest of the ladder, so confirm it on the order screen rather than trusting a comparison table.

Every rung includes the same management stack: automatic weekly offsite backups at no extra charge, IPv4 plus IPv6, a layer-3 firewall you configure from the panel without touching SSH, browser VNC, VM cloning, monitoring charts and API access. None of that is gated behind the expensive plans, which is unusual at this price and worth factoring in when you compare a $6 plan here against a $6 plan elsewhere.

## Which tier earns its price

The bottom two rungs are not small websites. 512 MB and 1 GB of RAM will run a WireGuard endpoint, an uptime monitor, a cron-driven bot, a DNS node or a lightweight proxy. Put a WordPress install with a few plugins on VM-0.5 and you'll be debugging the OOM killer instead of your site.

VM-1 at $5.99 is the cheapest plan with 2 GB, and single-core is the honest description of what you get for it. For $0.96 more, VM-1.5 keeps the same RAM and disk and adds a second core. That extra dollar is the best value jump in the entire table if anything on your box spawns worker processes.

VM-2 at $11.99 is where a real workload starts: 2 cores, 4 GB, 30 GB. A WooCommerce store with a few hundred products, a Node or Django API with a Postgres instance on the same box, a Minecraft server for five friends, all fit. The same logic applies one step up: VM-3 adds two more cores to the same 4 GB for $3, which matters for build jobs and concurrent PHP workers, not for memory-hungry databases.

From VM-4 upward you're buying RAM and disk more than cores. Docker stacks with several services, a database that has outgrown shared memory, a modded game server with a big world, or a CI runner. VM-6 and VM-8 are for teams consolidating several small VMs into one bigger machine.

One caveat on the headline spec. Evoxt's pitch is clock speed, with a stated 3.5 GHz floor and turbo up to 6.0 GHz, against the 2.3–2.4 GHz shared cores that budget clouds typically run. VPSBenchmarks' grading of these plans is less flattering on throughput: VM-1 scores E for raw CPU power and D for network performance, with B for web performance and disk I/O; VM-2 scores C for web performance, D for raw CPU, C for network. High clocks help single-threaded work like rendering a page or ticking a game loop. They don't turn one core into four.

## Latency: the number that matters is not the one on the sales page

Montreal providers quote latency in ways that aren't comparable, and the gap between them is bigger than the gap between the cities.

EDIS Global publishes a Speedtest run from its Montreal platform to a Beanfield server in Montreal: 18,466 Mbps down, 8,995 Mbps up, 0.62 ms idle latency. That is a machine in a rack talking to another machine in the same city over a 2×10 Gbps uplink. It proves the port isn't the bottleneck. It tells you nothing about what a shopper in Quebec City or a player in Toronto experiences. Sucura's numbers are the user-side kind: about 13 ms to Toronto, 60–70 ms to Calgary, 75–85 ms to Vancouver, under 15 ms across greater Montreal, Laval, Longueuil and the South Shore.

Both figures are real. They answer different questions, and sales pages rarely say which one they're quoting.

The way to settle it for your own users: ask for a test IP or a looking glass before you order, then run MTR or traceroute from the networks your users are actually on, at the hour your traffic peaks. EDIS makes this easy by publishing test addresses and 100 MB and 1 GB speed files, and other hosts will hand over a test IP on request. Two racks in the same city can differ by several milliseconds to the same destination because of transit and peering, so the city name on the order form is the start of the measurement, not the end of it.

For Evoxt specifically, the location is chosen in the deploy console, and the company runs 18 data centres across four continents. Whether the Canadian location is available for the exact plan you want is a question the order screen answers in one view. If Quebec data residency is a legal requirement for your project rather than a preference, get that confirmed in writing before you pay, because a provider's country list can change and a VM can be migrated.

## What the monthly price leaves out

Currency first. Evoxt bills in USD. Sucura Networks also quotes USD ($7.50/month, or $0.010/hour). EDIS Global quotes EUR and says so, along with "excl. VAT," which means the €4.99 entry plan is not the number that lands on your card. vShield ($12.99/month) and Axion.host ($5.99/month) both print a dollar sign without saying which dollar. Across a year, a currency mismatch plus a VAT line can outweigh the difference between two plans you were comparing.

Billing cycle second. Evoxt is monthly only, so a machine you need for three days costs a month. Sucura bills hourly from about $0.010/hour, which is the better shape for migration tests and one-off jobs. EDIS gives a free month on annual terms and runs a traffic pool that doesn't expire, letting you move unused transfer between VMs.

Bandwidth third. Evoxt gives each VM a monthly transfer allowance, 2 TB on a 2-core/4 GB instance, and throttles rather than bills once you pass it. That's a predictable cost model, but throttling is still throttling: if you're serving video or running a busy download mirror, an unmetered plan like Axion's or vShield's 1 Gbps unmetered line is the more sensible buy.

## What Evoxt does not include

Three gaps matter depending on what you're building.

There's no DDoS mitigation on the plans. VPSBenchmarks' feature record lists DDoS protection as absent for Evoxt, and nothing in the plan list contradicts it. In Montreal that's a real difference: Sucura bundles SucuraGuard on every VM with 2 Tbps+ of scrubbing across nine PoPs and sub-second detection, vShield includes enterprise mitigation on all plans, and Sable includes it too. If you run a game server, a public API or anything that attracts volumetric attacks, budget for a reverse proxy or accept the exposure.

There's no hourly billing and no reverse DNS in the published feature set, and the CPU model is hidden from the guest. Hidden silicon is normal for budget providers, but it means you can't verify the 3.5 GHz claim from inside the VM the way you can with a host that exposes the model string.

Payment options are credit card, PayPal and Bitcoin. No Interac, no SEPA transfer.

## How the Montreal field compares

Reference points from providers selling into the same city, for calibration rather than endorsement:

| Provider | Montreal entry price | Billing | What stands out, and the catch |
| --- | --- | --- | --- |
| vShield | from $12.99/mo (currency not stated) | Monthly | Under 5 ms across Quebec, explicit Law 25 and PIPEDA wording, 1 Gbps unmetered, Windows Server 2025 with RDP included |
| Sucura Networks | $7.50 USD/mo or ~$0.010/hr | Monthly or hourly | 10 Gbps port on every VM, 5–25 TB transfer, free DDoS, per-hour billing |
| EDIS Global | €4.99/mo excl. VAT | Monthly or annual | 2×10 Gbps uplinks, traffic pool that never expires, 24-hour free location switch |
| Axion.host | $5.99/mo (currency not stated) | Monthly | Unmetered traffic, up to 2 Gbps shared port, 12 tiers up to 24 vCore |
| Sable Servers | Not published | — | ~5 ms Quebec, ~8 ms Ontario, Windows requires your own licence |

Sable's Windows policy is the one to read twice. Their Windows VPS is bring-your-own-licence, while vShield bundles Server 2025 with RDP, EDIS offers Server 2025/2022/2019 and Windows 10/11 images, and Evoxt lists Windows among standard OS options rather than as a paid add-on. On a $20/month VM, a licence can be the largest line item after the server itself, so compare Windows-inclusive prices against Windows-plus-licence prices, not the sticker on the Linux plan.

## Three costs that show up after signup

**Upgrade ceilings.** EDIS caps a single VM at 8 vCPU, 24 GB RAM and 500 GB of total storage, RAM and CPU changes need a full shutdown, and after a storage upgrade you expand the partition and filesystem yourself. That's fine if you know it on day one and painful on the day your database outgrows it. Evoxt allows upgrades from the admin console, which is the smoother path for a machine that grows.

**Compliance wording.** vShield states plainly that data never leaves Canadian territory and ties that to Quebec's Law 25 and federal PIPEDA, and publishes a Quebec registration number (NEQ 1179528642). Sucura uses softer language: "Canadian-operated infrastructure" that "aligns with data residency discussions." One is a claim about legal posture, the other is a claim about where the operator is based. If you're handling health records or public-sector data, read the exact sentence a host uses and get the stronger version into your contract.

**Cross-city networking.** If your setup splits a database and an application across provinces, Sable lets one account run Halifax and Montreal machines joined by a private WireGuard network, so replication traffic stays off the public internet. Most single-region hosts can't do that without a VPN you build yourself.

## Before you pay

Match the plan to the workload, not to the spec sheet you'd like to have. A bot, a resolver or a personal VPN: VM-0.5 at $2.99. A small site or an API with a database: VM-2 at $11.99. A Docker stack, a modded game server or a CI runner: VM-4 at $23.99 and up. Anyone who needs bundled DDoS mitigation or per-hour billing should look at Sucura instead, and anyone who needs a Windows licence included should confirm how Evoxt prices it for the plan they want.

Three checks before the card comes out. Confirm the Canadian region and the exact plan in the deploy console, not just on the marketing page. Get a test IP and run MTR from where your users actually are, at peak time. And decide in advance how you'll handle an attack, because Evoxt's plan price doesn't include mitigation.

👉 [Compare the full Evoxt lineup and start a Montreal deployment](https://bit.ly/EvoXt)
