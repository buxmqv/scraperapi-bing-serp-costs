# Bing SERP API: What ScraperAPI Charges per Search, What 1,000 Searches Really Cost, and Which Plan Fits (Full Plan Table)

ScraperAPI bills a Bing SERP request at **25 credits**, the same rate it charges for Google and 25 times what a standard page costs. That one number settles most of the buying decision: 1,000 Bing searches consume 25,000 credits, and at the Scaling tier ($475/month for 5,000,000 credits) that works out to roughly **$2.38 per 1,000 searches**. Everything below follows from that: the full plan table, the credit math at 1,000, 10,000 and 100,000 searches, what a Bing response actually contains, and the checks worth running before you point a production rank tracker at it.

> **Quick pick:** running a rank tracker or SEO tool at 100,000+ Bing SERPs a month, Scaling is the tier with clear published numbers (5,000,000 credits, 200 concurrent threads, $475/month or $427.50/month billed annually). Under about 40 Bing searches a month, the free plan's 1,000 credits already covers you.
> 👉 [See ScraperAPI's current plans and per-credit pricing](https://www.scraperapi.com/pricing?fp_ref=coupons)

## How ScraperAPI's seven plans differ

Every self-serve tier charges the same 25 credits per Bing SERP request, subdomains included. What changes between tiers is the monthly credit allowance, the price per credit and the concurrency limit. The table below covers the billing rules that actually move your monthly bill, because those are the differences that decide whether an overage pauses your pipeline or quietly upgrades you into the next tier.

| Plan | Auto-upgrade | Pay-as-you-go | Credit rollover | Annual discount | Purchase |
| --- | --- | --- | --- | --- | --- |
| Hobby | Opt-in | Not available | None | 10% | [Hobby plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | Opt-in | Not available | None | 10% | [Startup plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | Opt-in | Not available | None | 10% | [Business plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | Opt-in | Available | None | 10% | [Scaling plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | Opt-in | Available | None | 10% | [Professional plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | Not available | Available | None | 10% | [Advanced plan pricing](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Not available | Available | None | Custom | [Enterprise pricing contact](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Confirmed numbers behind that table: the free plan gives **1,000 credits a month with 5 concurrent threads**; a new account starts with a **7-day trial of 5,000 credits, no credit card**; Scaling carries **5,000,000 credits and 200 concurrent threads at $475/month, or $427.50/month billed annually ($5,130/year, $570 saved)**. Allowances and prices for the tiers between free and Scaling sit on the pricing page, and per-credit cost improves as you move up, which is the usual reason to jump a tier rather than top up. Advanced is the highest self-serve plan, so auto-upgrade stops there.

## What 25 credits per Bing request costs at 1,000, 10,000 and 100,000 searches

Divide your monthly Bing volume into the credit allowance and the answer falls out. The conversions below use the Scaling rate, the only tier where both the allowance and the price are published.

| Bing SERP requests per month | Credits consumed | Where that lands |
| --- | --- | --- |
| 40 | 1,000 | free plan, used up entirely |
| 200 | 5,000 | the 7-day trial allowance |
| 1,000 | 25,000 | ~$2.38 on Scaling |
| 10,000 | 250,000 | ~$23.75 on Scaling |
| 100,000 | 2,500,000 | ~$237.50, half of Scaling's allowance |
| 200,000 | 5,000,000 | fills Scaling, $475/month |

Two adjustments matter more than the table.

The first is add-ons. Rendering (`render=true`), premium proxies (`premium=true`) and bot-protection bypass each add 10 credits on top of the 25, so a Bing request that needs rendering costs 35 credits, not 25. Geotargeting, sessions, device type, output format and auto parsing add nothing.

The second is tier position. $2.38 per 1,000 is the marginal rate at 5,000,000 credits. On the smaller tiers the per-credit price is higher, so the same 1,000 Bing searches cost more there. If you are costing out a small pilot, price it off the tier you will actually buy, not off Scaling.

## What a Bing request actually returns

ScraperAPI treats Bing SERP requests as their own billing category, priced identically to Google and inclusive of subdomains, and auto parsing is free of credit cost. The structured endpoint ScraperAPI documents in detail is the Google SERP one, which returns parsed data, takes a `START` offset instead of a page number, and does not accept a `num` parameter. It bills at the same 25 credits.

For Bing specifically, the field schema is the thing to verify rather than assume. Run 15 or 20 queries during the trial across a brand term, a commercial term and something that triggers an AI-generated answer, then check whether the payload gives you what your product needs: organic position, title, link and snippet; paid results; a knowledge panel; related searches; and, if you are selling AI visibility, whether any Bing Copilot or AI summary content appears at all. If your rank tracker has to report "we rank #3 including the AI answer above us", confirm that element exists before you build the parser around it.

## Which plan fits which workload

A daily rank tracker at 5,000 keywords tracking Bing runs 150,000 requests a month, or 3,750,000 credits. Scaling covers it with about 1.25 million credits spare for ad-hoc checks and other scraping. At 10,000 keywords daily you need 7.5 million credits, which is past Scaling's allowance, so you are into Professional or Advanced, or into pay-as-you-go on Scaling at a fixed per-credit rate up to a monthly cap you set.

Smaller jobs map cleanly too. A one-off audit of 200 queries fits inside the 7-day trial's 5,000 credits. Weekly spot checks of a few dozen keywords fit on the free plan at 40 searches a month. Mixed workloads need the credit table rather than the request count: a standard product page is 1 credit, Amazon is 5, a Bing SERP is 25, LinkedIn is 30.

If your volume is spiky, say a nightly batch plus a burst when a client asks for a fresh pull, pay-as-you-go is the feature that matters, and it is available from Scaling upward but not on Hobby, Startup or Business.

## Where ScraperAPI stops fitting

The 25-credit rate is the honest limit of this option. If Bing SERP data is your only workload and you buy it at volume, a dedicated SERP vendor is cheaper: DataForSEO publishes $0.0006 per SERP on its Standard queue ($0.6 per 1,000), $0.0012 on Priority and $0.002 live ($2 per 1,000), counting one SERP as 10 results. Against ScraperAPI's roughly $2.38 per 1,000 at Scaling, that is a real gap for a pure rank-tracking pipeline. ScraperAPI earns its place when Bing is one of several sites in the same product and you would rather run one integration and one bill than two vendors.

Three billing behaviours to plan around. Credits do not roll over, and the balance resets when the subscription renews, so size the plan to your peak month. Exceeding your concurrency limit returns a 429 and the request is refused rather than queued, with no extra charge, which means concurrency, not credits, is often the real ceiling during a nightly run. And geotargeting is documented at country level, so if you need city-level or GPS-level Bing results, confirm coverage first.

The refund policy is a genuine 7-day, no-questions-asked guarantee, which pairs well with the trial: build a real response parser inside that window and you will know whether the Bing payload is enough.
👉 [Start the 7-day trial with 5,000 credits](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Six checks that apply to any Bing SERP API

These come from documented behaviour across the category, and they are the questions that separate a usable Bing feed from one that quietly reports the wrong rank.

1. **Offset or page number?** SerpApi's `first` parameter is an offset into the organic results, where `first=10` moves the tenth result to the front, not a page index. Do not assume a fixed number of results per page, and set a hard stop when no further organic results come back.
2. **Is caching billed?** SerpApi serves a one-hour cache when every parameter matches and does not count cached searches against the monthly quota. Ask the same question of any provider, because a cache that is billed changes your cost model for repeated keyword pulls.
3. **Async or synchronous?** SerpApi's `async` submits and returns later through an archive API, and cannot be combined with `no_cache`. If your pipeline batches overnight, asynchronous submission may be the difference between finishing and timing out.
4. **`rank_group` or `rank_absolute`?** DataForSEO draws the distinction clearly: `rank_group` is position within a group of identical elements, `rank_absolute` is position across the whole page including the features above. Reporting a snippet-less "#3" from a page that opens with an AI answer and two ads is how rank trackers end up disagreeing with what the client sees.
5. **Do location codes carry over from Google?** They do not map one to one, and language fallbacks differ by market. Pull the supported list from the provider rather than reusing your Google configuration.
6. **Is the AI answer tracked separately?** DataForSEO exposes an `ai_overview` block with its own sources, and treats "which domains appear in the AI answer" as a different question from "which domains rank organically". If Copilot visibility is part of what you sell, this needs its own field, not a guess.

## Questions buyers actually ask

**Is Bing a dedicated SERP API on ScraperAPI, or general scraping?** Bing SERP requests are their own pricing category at 25 credits, separate from the 1-credit standard page rate, and auto parsing costs nothing extra. The detailed structured-data documentation I could verify covers the Google SERP endpoint, so treat the Bing field schema as something to confirm in a trial response rather than something to assume from the Google docs.

**How do I check the cost of a specific URL before scraping?** Use the Domain Cost Estimator in the dashboard, set `max_cost` on a scrape to cap any single request, and read the `sa-credit-cost` header on every response to see what it actually consumed.

**What happens when credits run out mid-month?** On Hobby through Professional, opt-in auto-upgrade moves you to the next tier; without it, scraping pauses until credits renew. From Scaling upward, pay-as-you-go keeps requests running at a fixed per-credit rate up to a cap you set.

## The decision rule

Under 40 Bing searches a month: stay on the free plan. A one-off audit under 200 queries: use the 7-day trial. A daily Bing rank tracker up to 5,000 keywords: Scaling, roughly $2.38 per 1,000 searches, with room to spare. Beyond that: pay-as-you-go on Scaling or a conversation with sales, because the arithmetic crosses 5 million credits. And if Bing SERP data is literally the only thing you will ever pull, compare a dedicated SERP vendor's $0.6 to $2 per 1,000 before you commit.

One thing to confirm before paying: run 15 real queries in the trial and check that the Bing payload includes every element your product reports on, including whatever Bing shows above the first organic result. That single test decides more than any plan comparison.
👉 [Compare ScraperAPI plans and start with 5,000 free credits](https://www.scraperapi.com/pricing?fp_ref=coupons)
