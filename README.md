# vultr vs vast.ai: is Vast.ai actually cheaper? What Vultr's H100 and B200 page prices leave out (full plan table, L40S head-to-head, $300 credit)

Vast.ai was renting the L40S 48GB at $0.53/hr on 12 November 2026. Vultr lists the same card at $1.67/hr, a 212% gap on the one GPU both providers had available that day. The H100 comparison is messier: Vultr's pricing page shows $2.30 per GPU-hour, Vultr's own public API quotes $2.99 on-demand for the same 8-GPU node, and $2.30 happens to be exactly the preemptible rate. Which of those two numbers you quote decides who wins the table.

So this comparison pulls the billing terms apart: what each headline price is a measurement of, the smallest unit you can actually buy, and the charges that show up after the first invoice.

> **Quick pick.** Vultr's L40S 48GB at $1.67/hr (16 vCPU, 180 GB RAM, 1.20 TB storage, 10 TB transfer included) is the entry point for a fixed-spec box at a published rate. A100 80GB PCIe at $2.40/hr is the step up when a model needs 80 GB per card. Neither provider has a free plan. 👉 [Check the current L40S 48GB hourly rate](https://www.vultr.com/pricing/?ref=9738262-9J)

## Vultr's full GPU lineup and what each plan costs

Vultr publishes per-GPU prices, but several plans are sold as whole multi-GPU nodes, and the smallest purchase differs row by row. That column matters more than the hourly figure.

| Plan | Per-GPU hourly | Minimum purchase | vCPU / RAM per GPU | Order |
| --- | --- | --- | --- | --- |
| L40S 48GB | $1.67 | 1 GPU (2, 4 and 8-GPU configs at the same per-GPU rate) | 16 vCPU / 180 GB | [L40S 48GB pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| A40 48GB | $1.71 | 1 GPU (4-GPU node $6.849/hr total) | 24 vCPU / 120 GB | [A40 48GB pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| RTX 4090 24GB | $0.78 | 1 GPU | not published in the checked feed | [RTX 4090 pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| A100 80GB PCIe | $2.40 | 1 GPU (8-GPU PCIe node $19.178/hr total) | 12 vCPU / 120 GB | [A100 80GB PCIe pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| A100 80GB SXM (HGX) | from $2.80 | 8-GPU node | not published | [HGX A100 pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| H100 80GB SXM (HGX) | $2.30 page / **$2.99 API on-demand** ($2.30 preemptible) | 8-GPU node | 27 vCPU / 239.25 GB | [HGX H100 pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| B200 192GB (HGX) | $3.50 page / **$8.50 API on-demand** ($3.20 preemptible) | 8-GPU node | 31 vCPU / 353.25 GB | [HGX B200 pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| GH200 | $1.99 | single-GPU instance | not published | [GH200 pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |
| MI355X 288GB | $2.59 | 8-GPU node ($20.72/hr total) | not published | [MI355X pricing](https://www.vultr.com/pricing/?ref=9738262-9J) |

Vultr's GPU prices come from its pricing page and its public plans endpoint, checked 17 October 2026; the bare-metal per-GPU figures and the GH200 and MI355X rows were cross-checked against a tracker last updated 5 October 2026. Vultr also lists MI300X 192GB and MI325X 256GB instances, and two third-party feeds disagree on both (one shows $1.85 and $2.00 per GPU-hour, another $3.99 and $4.62), so price those two on the page before you budget.

## What Vast.ai's price tag is a median of

Vast.ai is a marketplace. Independent hosts list machines, and the number in the marketing table is the median of those listings, not a rate the company sets. Checked 2 November 2026:

| GPU | Median | Cheapest listing | Listings counted |
| --- | --- | --- | --- |
| RTX 4090 24GB | $0.47/hr | $0.14/hr | 635 |
| RTX 5090 32GB | $0.73/hr | $0.39/hr | 941 |
| L40S 48GB | $0.73/hr | $0.33/hr | 93 |
| A100 80GB SXM4 | $0.80/hr | $0.40/hr | 72 |
| H100 80GB SXM | $2.40/hr | $1.73/hr | 63 |
| B200 192GB | $8.63/hr | $6.25/hr | 23 |

A 4090 at $0.47/hr is the middle of 635 offers that start at $0.14. Getting the cheap end means reading host specs, checking reliability signals and accepting that the machine is someone else's. Vast's own documentation of the trade-off is candid: hardware quality varies by host, there is no enterprise SLA or uptime guarantee, and Interruptible instances can be reclaimed at any time. Per-second billing and no minimum commitment are genuine advantages for short jobs, and the consumer-card selection (3090, 4090, 5090) has no equivalent on Vultr.

Vultr's column is the other arrangement: one price per plan, same specs, dedicated VRAM and NVMe, across 30+ locations, with an outbound transfer allowance on every instance. You pay for not shopping.

## Three things Vultr's page price doesn't tell you

### The page price and the API price disagree

For the HGX H100 node, Vultr's page presents $2.30 per GPU-hour. The public plans endpoint returns the same node at $23.92/hr, which is $2.99 per GPU, with `deploy_ondemand=false`, plus a preemptible rate of $18.40/hr ($2.30 per GPU). The identical $2.300 figure appears in Vultr's bare metal section, where "starting from" is defined as pre-paid contract terms.

The B200 row is worse. The page shows $3.50 per GPU-hour; the API returns $68.00/hr per node, or $8.50 per GPU, with a preemptible rate of $25.60/hr ($3.20 per GPU). A 143% difference between two numbers published by the same company.

Treat the page figures as floors and budget the API figures. If your plan needs a firm number before approval, open the deploy screen and read the rate there.

### H100 and B200 sell by the eight

$2.30 sounds like a card you can rent for an afternoon. It isn't. Both plans are 8-GPU nodes: the H100 node carries 216 vCPU, 1,914 GB RAM and 640 GB of GPU memory, the B200 node 248 vCPU and 2,826 GB RAM. At the API on-demand rate the H100 node costs $23.92/hr and the B200 node $68.00/hr. At the page rates, $18.40/hr and $28.00/hr.

Single-GPU rentals exist on Vultr, on L40S, A40 and A100 PCIe. If your work fits in 48 GB or 80 GB of VRAM, those are the plans to compare, and the eight-GPU question never comes up.

### The preemptible rate is doing the marketing

$2.30 is the H100 preemptible rate. Preemptible capacity can be taken back, which puts it in the same category as Vast's Interruptible tier. Comparing Vultr's preemptible number against Vast's on-demand median flips the ranking depending on which two cells you pick. Compare like with like: on-demand against on-demand, reclaimable against reclaimable.

👉 [See the on-demand rate on the H100 deploy page before you commit](https://www.vultr.com/pricing/?ref=9738262-9J)

## L40S 48GB: the one clean head-to-head

Same-day checks on 12 November 2026 found one GPU both providers were renting: the NVIDIA L40S 48GB. Vast.ai's cheapest live community rate was $0.53/hr. Vultr's list price was $1.67/hr. Vultr costs about 3.2x more, and even against Vast's L40S median of $0.73/hr it is roughly 2.3x.

Two caveats belong next to that number. The $0.53 is a community rate, from a host whose machine can be reclaimed or go offline, not an on-demand booking with a service guarantee. And the comparison covers one GPU; Vast carries dozens more models, Vultr's catalog is narrower.

What $1.67 buys on Vultr: 16 vCPU, 180 GB RAM, 1.20 TB of storage, 10 TB of monthly transfer, a fixed spec in a chosen region, hourly billing with no commitment, and a bill you can predict from the pricing page.

## Where Vast.ai is the right call

Work that can be killed and resumed at a checkpoint belongs on a marketplace. Hyperparameter sweeps, batch inference over a large corpus, dataset preprocessing, a fine-tune you can restart from the last saved step: interruption costs you time, not the run.

Short jobs also favour per-second billing. A 25-minute inference job billed by the second on Vast and by the hour on Vultr is a straightforward difference, and Vast's Interruptible tier pushes the rate lower still.

Then there is hardware you cannot get elsewhere in this comparison. RTX 3090, 4090 and 5090 rentals at consumer prices, plus B300 and GB200-class machines, show up on the marketplace. If you want to test whether a 24 GB card is enough before renting an A100, Vast is the cheap way to find out.

## Where Vultr earns the extra dollar

Pay Vultr when the hourly rate is not the variable you are optimising. A production inference endpoint that has to answer requests in a specific country is one case: 30+ locations and a fixed per-instance transfer allowance (0.5 to 15 TB per month, $10/TB beyond) let you put the GPU near users and forecast the bandwidth line. A marketplace host's location and egress terms vary by host.

Pay Vultr when the spec has to stay the same between runs. Benchmarking two model versions on identical vCPU, RAM and storage removes a variable that marketplace renting reintroduces every time you pick a different machine.

Pay Vultr if the GPU needs neighbours. Managed PostgreSQL at $60/mo, object storage at $18/mo, Redis at $15/mo and a load balancer at $10/mo sit in the same account and the same regions as the GPU. That is a real convenience for a small team shipping an application, and it is not something Vast sells.

One thing to settle before regulated data goes anywhere near either provider: Vast.ai publishes SOC 2 Type II, HIPAA and GDPR statements on its own compliance page. Vultr's do not appear in the compliance trackers checked for this article, which means no public statement was found, not that certification is absent. Ask Vultr directly and get the scope in writing if HIPAA or a DPA matters to you.

## The $300 credit: what is confirmed and what isn't

Vultr has no free plan. New customers can get a promotional credit advertised at $300, and the terms are thinner than the banner suggests. Nothing in the sources checked confirms three things you would want to know: whether GPU instances qualify, how long the credit stays valid, and whether it stacks with other offers.

Community threads about the offer describe it as a time-limited trial credit unlocked after adding a payment method, with at least one user reporting it would not apply to GPU deployments. Treat that as anecdote and read the terms on the checkout screen.

The arithmetic is still worth doing, because it tells you how far a credit of that size goes if GPUs are eligible. At API on-demand rates, $300 covers about 12.5 hours of a single H100 node at $23.92/hr, roughly 4.4 hours of a B200 node at $68.00/hr, or about 180 hours of an L40S at $1.67/hr. For a one-off training run, the L40S plan is where a credit of that size actually stretches. Add the payment method before deploying so the credit lands on the account.

👉 [Start on the L40S 48GB plan and confirm the credit applies at checkout](https://www.vultr.com/pricing/?ref=9738262-9J)

## Before you deploy, check these six things

1. The on-demand rate on the deploy screen, not the marketing table, for any H100 or B200 plan.
2. Whether your job needs one GPU or eight, since H100 and B200 only come as nodes.
3. The region, and whether the transfer allowance covers your egress.
4. Whether the job survives interruption. If yes, compare Vast's Interruptible tier and Vultr's preemptible rate. If no, pay for on-demand on either side.
5. Whether the credit is applied to the account before the first instance starts.
6. For Vast, the specific host: specs, reliability history and location, since the median price is not a product.

## The decision rule

If the job can be checkpointed and resumed, run it on Vast.ai and put the savings into more runs. If the job has to finish on schedule, needs a fixed spec in a named region, or has to sit beside a managed database and object storage you already operate, pay Vultr's rate and stop shopping hosts.

For most small teams the practical split is both: Vast for experiments and batch work, Vultr for the endpoint that serves users. If you are starting with one provider and one plan, the L40S 48GB at $1.67/hr is the least risky place to begin, because the price on the page is the price you are charged.

👉 [Check Vultr's current L40S 48GB and A100 80GB hourly prices](https://www.vultr.com/pricing/?ref=9738262-9J)
