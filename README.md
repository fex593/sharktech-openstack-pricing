# public cloud computing providers: How the Pricing Really Stacks Up, Which Hidden Fees to Check, and When Sharktech's OpenStack Cloud Is the Smarter Pick

Most people searching for public cloud computing providers already know what a public cloud is. What they want is a straight answer on which provider deserves their money, and the first page of results mostly recycles the same AWS/Azure/GCP listicles while skipping the part that actually decides the bill: egress pricing, DDoS protection add-ons, and what happens when usage spikes past your plan.

Gartner projects public cloud end-user spending to hit $850 billion, a 21.3% jump from 2025, so the market isn't short of options below the hyperscalers. One that keeps coming up in independent testing is Sharktech, a Las Vegas infrastructure company founded in 2003 that runs its own network (AS46844) with data centers in Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam. Its Public Cloud product is built on OpenStack, every public IPv4 comes with 60 Gbps of DDoS protection baked into the base price, and the company's own positioning is blunt: its cloud claims at least 40% savings compared with the hyperscalers.

This article walks through how these providers actually differ, Sharktech's full plan table with verified pricing, the fee traps to check before you commit to anyone, and who should honestly pick something else.

> **Quick take:** for most readers comparing providers for real workloads — dev/staging servers, small production apps, game servers, anything that attracts traffic — Sharktech Public Cloud **Small** at **$39/month** (4 cores, 8 GB RAM, 300 GB SSD, 20 TB outbound bandwidth) is the sensible starting point. 60 Gbps DDoS protection and unlimited inbound traffic are included at every tier. [👉 Check Sharktech Public Cloud plans and current pricing](https://bit.ly/SharKtech)

## What actually separates public cloud providers from each other

Four things: the platform, the billing model, the network, and what's included versus metered.

The hyperscalers run proprietary platforms with enormous service catalogs — managed databases, AI pipelines, serverless functions. That's their strength, and if your team lives in those managed services, switching makes no sense. The trade-off is vendor-specific tooling and a billing model where data leaving the network costs extra.

Sharktech sits in the specialty-provider camp. Its Public Cloud runs full OpenStack APIs (Nova, Cinder, Swift, Neutron, Keystone), so your infrastructure code isn't married to one vendor's console. You can upload your own VM images and ISOs, deploy Kubernetes clusters from the panel, set up virtual routers, security groups, floating IPs, and load balancers, and you get native IPv6. You can run Linux or Windows VMs — Linux costs nothing extra, while Windows is bring-your-own-license, so factor that in if your stack needs it. Everything is self-managed: you get the keys, you run it.

The billing model is where it diverges sharply from the big names. You buy a resource pool, and the platform meters aggregate usage above that pool across your whole cloud. One pool can run a single 4-core production VM or split into several smaller dev boxes across any of the five data center locations. Storage comes in three tiers — HDD, SSD, and NVMe — and Sharktech publishes the performance gap for each: roughly 1.2 GB/s and 18,000 IOPS on NVMe, 350 MB/s and 6,000 IOPS on SSD, 120 MB/s and 3,000 IOPS on HDD. Put databases and latency-sensitive loads on NVMe, push backups to HDD at $0.00002/GB/hour instead of paying flash prices.

## Sharktech Public Cloud: every plan and current price

Four fixed tiers plus a custom option, priced in USD from $39 to $499 per month, all with hourly metering above the included allocation.

| Plan | vCPU / RAM | SSD Storage | Outbound Bandwidth | Base Price | Order |
| --- | --- | --- | --- | --- | --- |
| Small | 4 cores / 8 GB | 300 GB | 20 TB | $39.00/mo | [ Configure Small](https://portal.sharktech.net/aff.php?aff=1626&pid=602) |
| Medium | 8 cores / 16 GB | 800 GB | 20 TB | $79.00/mo | [ Configure Medium](https://portal.sharktech.net/aff.php?aff=1626&pid=603) |
| Large | 32 cores / 64 GB | 1,500 GB | 20 TB | $249.00/mo | [ Configure Large](https://portal.sharktech.net/aff.php?aff=1626&pid=604) |
| Enterprise | 64 cores / 128 GB | 5,000 GB | 20 TB | $499.00/mo | [ Configure Enterprise](https://portal.sharktech.net/aff.php?aff=1626&pid=605) |
| Custom | Configurable | Configurable | Configurable | From $51.82/mo | [ Request a custom quote](https://bit.ly/SharKtech) |

Those base specs aren't the ceiling. Each tier covers a scalability range — Small scales up to 16 vCPU and 32 GB RAM, Large up to 128 vCPU and 256 GB, Enterprise effectively without preset limits — and you can upgrade a subscription at any time without redeploying the environment. Every tier includes 1 public IPv4 (additional IPs are $1.50/month each) and 24/7 support. Usage above the included allocation bills hourly at published rates: $0.0025 per CPU core hour, $0.0035 per GB of RAM per hour, and the storage rates above. Outbound traffic past your 20 TB costs $0.002/GB, and inbound is free and unmetered. Enterprise gets slightly lower overage rates (CPU at $0.002/core hour, SSD at $0.000045/GB/hour).

The Custom option is a configure-it-yourself track: Sharktech's own example — 32 cores, 64 GB RAM, 2,400 GB SSD, 8 IPv4 addresses, 40 TB of bandwidth — prices out at $51.82/month as a starting figure. Your actual quote depends on what you assemble, and final pricing lands in the customer portal.

Two billing details worth internalizing before you pick a tier:

- **Small, Medium, and Large have resource ceilings; Enterprise has none.** A ceiling caps how much extra CPU/RAM/storage you can burst into — useful protection against surprise bills. But Sharktech is explicit that these are resource ceilings, and resource ceilings are not monetary spending caps. Your bill can still grow above base price through metered usage.
- **Storage bills for the full month even when a VM is powered off.** The platform estimates months at 730 hours. If you rotate test machines weekly, delete the attached storage, or it stays on the invoice.

If the Small tier's 4-core/8 GB pool matches your workload, that's where the math lands best — the included 300 GB SSD and 20 TB of outbound traffic cover what most single-purpose servers actually use, which means the $39 stays at $39. [👉 Configure the Small plan and see the live cost estimate](https://portal.sharktech.net/aff.php?aff=1626&pid=602)

## The costs that actually decide the comparison

Sticker price is the smallest part of the equation. Three line items decide whether a cheap-looking cloud stays cheap.

**Bandwidth direction.** Sharktech includes 20 TB of outbound traffic and doesn't meter inbound at all. Egress overage is a flat $0.002/GB. Hyperscalers invert this — inbound is cheap, outbound is the line item that generates support tickets, and their tiered egress pricing gets expensive fast for streaming, file hosting, or CDN-edge workloads. If your servers push more data than they receive, this single difference can outweigh a nominal hourly-rate gap.

**DDoS protection.** Industry-standard mitigation services typically run $20–100+/month as an add-on, and Sharktech's own comparison material points to AWS Shield Advanced starting at around $3,000/month as the hyperscaler equivalent. On Sharktech's Public Cloud, 60 Gbps of protection per IP is included at every tier, upgradeable to 100 Gbps. The mitigation system is proprietary, built in-house, and runs at the network edge before traffic reaches your machine. This isn't just a spec-sheet claim: a year-long thread on LowEndTalk concluded, "Sharktech successfully stopped the DDoS attacks. I was pleased!" For game servers, exchange fronts, or anything that attracts attackers, this is the feature that justifies the whole comparison.

**Overage behavior.** Small through Large have ceilings that stop runaway bursts, which functions as crude budget protection. Enterprise has no preset ceiling — that's a feature for scaling, and a liability if nobody watches the usage panel. The real-time metering dashboard exists precisely for this; check it in week one.

There's a fourth angle for anyone migrating a serious workload off a hyperscaler: the Enterprise tier's 64 cores, 128 GB RAM, and 5 TB SSD at $499/month gets harder to beat once you add back what the hyperscalers charge separately for equivalent DDoS coverage and egress. [👉 See the Enterprise plan configuration and pricing](https://portal.sharktech.net/aff.php?aff=1626&pid=605)

## What independent testing shows about performance

HostAdvice's reviewers put Sharktech's Public Cloud at **9.4/10** overall, with support scoring 9.5 and features 9.6. The platform carries a 99.999% uptime guarantee.

The network numbers are the headline. The reviewers' instance connected to a 10 Gigabit network with upload bursts exceeding 20 Gbps, and local datacenter latency measured 0.17 ms — close to the physical floor. As the reviewers put it, many competing cloud providers cap VM networking at 1–5 Gbps unless you pay for premium tiers. For bandwidth-heavy workloads, that gap is structural, not marginal.

Their deployment test also surfaced a practical detail: they spun up an Ubuntu VM with a 12 vCPU / 48 GB RAM flavor (e5v3.c12m34) in minutes through the panel — but the default boot volume is only 3 GB, and they had to expand it. If you deploy there, size your boot volume at creation instead of discovering this mid-install. Ticket responses came back in under 40 minutes, with a detailed knowledge base covering most standard questions.

## Who should skip Sharktech Public Cloud

Honesty time, because four constraints rule out a chunk of searchers:

1. **No refunds.** All payments are final, including setup fees and renewals. The only recourse is disputing a billing error within 30 days of the invoice date, and a successful dispute pays out as account credit — not cash back.
2. **No free trial.** Hourly billing softens this considerably — your first hour costs pennies — but there's no risk-free evaluation window in the traditional sense.
3. **It's self-managed.** There's no managed-database button or hands-on support tier. If nobody on your team enjoys being a sysadmin, this will feel like homework.
4. **Five locations only.** Los Angeles, Las Vegas, Denver, Chicago, Amsterdam. If your architecture needs dozens of global regions or a deep catalog of managed AI and analytics services, the hyperscalers are the right call and no amount of egress math changes that.

One more path worth mentioning: if your workload is a single predictable server rather than a multi-VM cloud, Sharktech's own SmartVPS line is the cheaper entry point. Annual billing cuts 50% automatically with no coupon, putting the entry plan at $3.98/month on the same DDoS-protected network, with the resource pool divisible into multiple VMs across the five locations. HostAdvice's separate VPS testing recorded over 6,000 4K random IOPS and sub-millisecond local latency on that platform.

## Promo codes and billing-cycle discounts

The largest discounts are automatic, and two recurring codes circulate on deal listings.

On SmartVPS, the billing cycle does the work on its own — quarterly takes 25% off, semi-annual 35%, annual 50%. No code entry, no expiring link.

For the cloud products, deal listings currently show two recurring promo codes: **Y5YET1Z9EK** for 10% off cloud virtual servers and bare metal servers (20% if you deploy in Amsterdam), and **WHTFALL** for 33% off the Cloud Virtual Data Center — that's the OpenStack-based cloud line, the same platform family as Public Cloud — listed at roughly $26.13/month after the discount. The fixed Public Cloud tiers also show billing-cycle discounts of 5%–15% for quarterly, semi-annual, and annual prepayment per current deal listings, so it's worth checking the checkout page for your chosen term before paying monthly. Codes do lapse — enter them at checkout and confirm the discounted price before paying, since every payment at Sharktech is final.

## FAQ

**Do the plan ceilings cap my total bill?**
No. Small, Medium, and Large ceilings cap how many extra resources you can burst into, but Sharktech states plainly that resource ceilings are not monetary spending caps. Metered usage above the included pool still bills at published rates.

**Does Sharktech offer refunds or a trial period?**
No refunds on any payment, and no free trial. Billing errors can be disputed within 30 days for account credit. The hourly billing model is the practical workaround: a test VM costs cents for its first few hours.

**What am I billed for when a VM is shut down?**
Storage. Compute stops metering when the machine is off, but attached volumes bill for the full month at the 730-hour estimate. Delete unused volumes.

**Does the cloud support Windows?**
Yes, both Linux and Windows VMs are supported. Linux images are free; Windows uses bring-your-own licensing, so either supply your own key or budget for one.

**Where can I deploy?**
Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam, all on Sharktech's own 40G/100G backbone. Pick the location nearest your end users to exploit that 0.17 ms local latency.

## Picking between them, in one pass

- Your team runs on managed services, needs many regions, or trains models → the hyperscalers' ecosystems justify their premiums, egress bills included.
- One predictable server, minimal budget → SmartVPS on annual billing at $3.98/month is the lowest-commitment entry.
- OpenStack primitives, DDoS-exposed services, or bandwidth-heavy delivery workloads → Sharktech Public Cloud, starting at Small/$39.
- Migrating a serious workload off a hyperscaler → Enterprise at $499 with 5 TB SSD and included 60 Gbps protection.

One last check before ordering: build your configuration in the cost calculator, confirm the estimated total in the portal, and remember the no-refund policy applies from the first invoice. If the numbers hold up, [👉 deploy Sharktech Public Cloud starting at $39/month](https://bit.ly/SharKtech) and let the first month's actual metered bill tell you more than any comparison chart.
