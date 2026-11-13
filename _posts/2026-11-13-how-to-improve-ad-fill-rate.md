---
title: "How to Improve Ad Fill Rate: A 2026 Practical Guide"
description: "Learn how to improve ad fill rate with 5 proven fixes: geographic targeting, frequency caps, format optimization, latency reduction, and mediation setup."
date: 2026-11-13
permalink: /how-to-improve-ad-fill-rate/
layout: post
image: /assets/images/how-to-improve-ad-fill-rate.png
tags: [monetization, fill-rate, adtech]
---

## Stop Guessing, Start Diagnosing

Low fill rate is a symptom, not the disease.

Ad fill rate is the percentage of ad requests that return an ad: `Filled Ad Impressions / Total Ad Requests × 100`. When that number drops, revenue drops with it. But chasing fill rate in isolation is a mistake I see constantly.

*The numbers in this article are illustrative examples, not benchmarks, unless a source is cited.*

The goal isn't to diagnose "low fill rate." The goal is to find *why* demand sources aren't competing for your inventory.

I've audited dozens of monetization stacks over the past few years. The root cause is almost never what teams assume. It's rarely "bad traffic" or "the market is down." It's usually one of five specific, fixable issues that get overlooked because teams focus on dashboard averages instead of digging into segmented data.

Let's walk through them.

## The 5 Real Reasons for Low Fill Rate

### 1. Geographic Demand Mismatch

**Problem:** Your user base is concentrated in a Tier-2 or Tier-3 geography where your primary ad networks have weak demand.

I've seen apps with 85% fill in the US and 22% fill in Southeast Asia. The global average looks "okay" at 60%, so no one investigates. Meanwhile, half your impressions are going unfilled—and it's entirely preventable.

**Solution:**

**Audit Your Demand Partners.** Do they specialize in your key geos? A network strong in North America may have no presence in APAC. Check their case studies and publisher testimonials for geographic mentions.

**Segment Your Waterfalls.** Create specific waterfalls or bidding groups for key countries or regions. Prioritize networks with strong local advertiser relationships in those geos. Don't run a single global waterfall and expect it to work everywhere.

**Analyze Your Data.** Use your mediation platform's reporting to compare network fill rates *by country*. The data will tell you exactly where the demand gaps are. I start every audit by pulling a fill rate report segmented by the top 10 countries. The pattern is usually obvious within 30 seconds.

For more context on regional mobile trends, see the [latest mobile market trends by region](https://sensortower.com/blog).

### 2. Overly Restrictive Frequency Caps or Pacing

**Problem:** You've set aggressive frequency caps—say, 1 interstitial per user per hour—or strict pacing rules in your ad placements.

While intended to protect UX, this can starve your ad requests. The mediation platform might have an ad to show, but your own rules prevent the request from even being made. I've seen this cut fill rate by 30% without anyone realizing it.

**Solution:**

**A/B Test Your Capping Rules.** Is there a material difference in retention between a cap of 1/hour vs. 2/hour? Let the data decide, not assumptions. Run a controlled test for two weeks and compare D1 and D7 retention alongside revenue per user.

**Segment by User Engagement.** Consider relaxing caps for highly engaged users who are less likely to churn. A user who's completed 50 levels is not the same as someone on level 3.

**Focus on Placement Logic.** Instead of a global time-based cap, trigger ads based on meaningful in-app events—level complete, task finished, session end. This often feels more natural to the user and increases the number of eligible ad opportunities.

### 3. Ad Format Mismatch

**Problem:** You're requesting an ad format that has limited demand.

For example, you're trying to fill a 300×250 MREC placement, but the top-performing networks in your waterfall primarily focus on rewarded video or full-screen interstitials. The format itself becomes the bottleneck.

**Solution:**

**Standardize Formats.** Stick to IAB-standard ad formats—320×50 banners, standard interstitials, rewarded video—which have the deepest and most liquid demand pools. Custom sizes or unusual placements fragment demand.

**Consult Network Specs.** Check the documentation for your top 3-5 demand sources. What formats do they *excel* at filling? Prioritize those. If a network's strength is rewarded video, don't expect them to fill your banner inventory at the same rate.

**Introduce High-Demand Placements.** If your app can support it, adding a rewarded video placement can significantly increase overall fill and revenue, as demand for this format is consistently high. According to [high-performing ad formats in mobile gaming](https://www.pocketgamer.biz/news/), rewarded video consistently shows the strongest fill and eCPM across most geos.

### 4. Technical Latency & SDK Timeouts

**Problem:** Your ad request times out before a demand source can return a bid.

This is a silent killer of fill rate. If your mediation platform's timeout is set to 800ms, but a key network in a specific region consistently takes 1000ms to respond, you're leaving money on the table. The network never gets a chance to bid.

**Solution:**

**Audit Your SDKs.** Ensure all network SDKs and mediation adapters are updated to the latest versions. Version mismatches are a common cause of technical failure. I've seen a single outdated adapter drop fill by 15% because it was throwing silent errors.

**Review Timeout Settings.** Check your mediation platform's global and network-specific timeout settings. *Illustrative example:* Start with a baseline of 1.5–2 seconds and test downwards, monitoring both fill rate and ad load latency. Don't blindly copy another app's settings.

**Use Network Monitoring Tools.** Many mediation platforms provide tools to diagnose SDK health and response times. Use them. AppLovin MAX, for instance, has a network performance report that shows average response time per network. If a network is consistently over 1.5 seconds, it's a candidate for removal or de-prioritization.

For more on this, see the [impact of latency on auction dynamics](https://mobiledevmemo.com/).

### 5. Suboptimal Waterfall or Bidding Configuration

**Problem:** Your waterfall is poorly structured.

You might have networks with historically low eCPMs and low fill rates placed at the top, blocking healthier networks below them from getting a chance to fill the impression. Or, in a bidding setup, you haven't enabled enough bidders to create real competition.

I once audited a stack where the #1 network in the waterfall had a 40% fill rate and a $2 eCPM. The #4 network had a 75% fill rate and a $3.50 eCPM. The ordering was based on "brand trust," not data. Fixing this alone lifted revenue by 22%.

**Solution:**

**Prune Your Waterfall.** *Remove non-performing ad sources.* A waterfall with 5 healthy, responsive networks is better than one with 15, where 10 of them are dead weight adding latency. I typically recommend keeping 4-6 networks in the waterfall layer and moving everything else to bidding.

**Re-order Based on *Real* eCPM.** Don't rely on a network's "brand name." Use your own data from the last 7-14 days to rank networks based on their actual eCPM performance in that specific ad unit. Mediation platforms can auto-optimize this, but you should still audit it manually.

**Embrace Bidding.** If you're still running a pure waterfall, it's time to migrate. In-app bidding allows all demand sources to compete simultaneously, which inherently increases competition and the probability of getting a fill. For more on this, see [how ad mediation platforms work](https://www.adjust.com/blog/).

## The Strategic Solution: Mastering Ad Mediation

Ad mediation is not just a tool. It's the central control panel for implementing all the fixes above.

Mediation platforms let you manage multiple demand sources—ad networks, exchanges, DSPs—from a single SDK integration. Instead of hard-coding one network's SDK and hoping it performs, you integrate a mediation SDK once, connect several networks behind it, and let the mediation layer route each ad request to whichever source is currently paying the most or has an ad available.

The two dominant approaches are **waterfall** and **in-app bidding**. Understanding the difference is critical.

### Waterfall vs. In-App Bidding: A Quick Gut Check

| Feature | Waterfall | In-App Bidding |
|---------|-----------|----------------|
| **Logic** | Sequential (daisy-chain) | Parallel (simultaneous auction) |
| **Ranking** | Based on *historical* eCPM | Based on *real-time* bid price |
| **Latency** | Can be high due to multiple sequential calls | Generally lower (one call to mediation) |
| **Revenue Potential** | Good, but can leave money on the table | Highest, as it ensures the top bidder always wins |
| **Best For** | Simple setups; networks that don't support bidding | Maximizing competition and revenue |

Waterfall is easier to set up, but it's fundamentally inefficient. In-app bidding is where the industry has moved, and for good reason.

### My Personal Checklist for Auditing a Mediation Stack

When I'm asked to audit a poorly performing ad stack, I don't just look at the fill rate number. I follow a specific process to uncover the "why."

**1. Check the Health Report.** What does the mediation platform say? Are all SDKs and adapters green? This is my first stop. Any red flags here must be fixed before anything else. A single misconfigured adapter can silently kill 20% of your demand.

**2. Analyze the Top 5 Geos.** I immediately segment reporting by the top 5 countries. Where is the fill rate dropping? This tells me if it's a global technical problem or a regional demand problem. If fill is 85% in the US and 30% in India, the issue is demand, not tech.

**3. Review the Bidding-to-Waterfall Ratio.** How much of the revenue is coming from bidders vs. the waterfall? If 90% is still from the waterfall, there's a huge opportunity to enable more bidders and increase competition. I've seen apps lift revenue by 40% just by migrating their top 3 waterfall networks to bidding.

**4. Look at Latency Reports.** I check the average response time per network. Any network consistently responding over 1.5 seconds is a candidate for removal or de-prioritization, as it's hurting the entire stack. Slow networks don't just lose their own auctions—they delay everyone else's.

**5. Compare Ad Unit Performance.** Is the low fill rate specific to one ad unit—banners, for example—while others like rewarded are healthy? This points to a format-specific demand issue. The solution might be as simple as adding a new format or swapping a poorly performing placement.

## The Balancing Act: Why a 100% Fill Rate Isn't the Goal

Here's something most teams get wrong: **optimizing for fill rate alone is a mistake.**

Fill rate and eCPM often have an inverse relationship. Setting price floors to zero might get you 100% fill, but your revenue could plummet because you're selling impressions for pennies.

The ultimate north-star metric is **ARPDAU** (Average Revenue Per Daily Active User). The goal is to maximize total revenue per user, not just one component metric. ARPDAU = (Ad Impressions per DAU × Fill Rate × eCPM) ÷ 1,000.

A "healthy" fill rate is a *balanced* one. For a mature app, a fill rate of 80-90% with a high eCPM is often more profitable than a 98% fill rate with a rock-bottom eCPM. Here is the math with 10,000 daily ad requests (illustrative):

- Option A: 85% fill at a $12 eCPM = 8,500 impressions = 8.5 thousand x $12 = $102.
- Option B: 98% fill at a $6 eCPM = 9,800 impressions = 9.8 thousand x $6 = $58.80.
- Higher fill, lower revenue: Option A earns about 73% more ($102 vs $58.80) with fewer impressions.

That is why fill rate alone is a false signal. What matters is fill rate combined with eCPM and how many impressions each user actually sees.

For more on this, see the [relationship between fill rate, eCPM, and ARPDAU](https://mobiledevmemo.com/).

## Conclusion: From Reactive Fixes to Proactive Optimization

Improving fill rate is a systematic process of *diagnosing* specific issues—geography, caps, tech, configuration—*strategically managing* your stack via mediation, and *balancing* for overall revenue (ARPDAU).

The five root causes I've outlined—geographic demand mismatch, overly restrictive frequency caps, ad format mismatch, technical latency, and suboptimal waterfall or bidding configuration—account for the majority of fill rate problems I see in the field. Fix these, and you'll see immediate improvement.

But don't stop there. Treat your monetization stack not as a "set it and forget it" system, but as a dynamic product that requires regular audits and optimization. The best-performing apps I've worked with review their mediation stack monthly, run A/B tests quarterly, and adjust their strategy as demand patterns shift.

That's how you turn fill rate from a problem into a lever for sustainable revenue growth.

---

**About the author:** I'm a mobile growth consultant helping app developers scale UA and monetize better — DSP, offerwall, and programmatic, mainly in SEA and LATAM. [Let's connect on LinkedIn](https://www.linkedin.com/in/mika-lee-0a920044a/)
