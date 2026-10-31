# Worked product decisions

These are hypothetical examples for reasoning, not benchmark results or advice
about a particular app. Treat any numbers as explicit assumptions.

## A drawing app: decide where the purchase belongs

**Facts:** A useful sketch can be made locally without a service cost. High
resolution exports and cloud collaboration are paid capabilities.

**Candidate A — purchase at launch:** simple entitlement gate; weak opportunity
to experience the editor. Reasonable only if acquisition already demonstrates
its value or there is another strong business constraint.

**Candidate B — purchase at export:** lets the customer experience drawing;
risks frustration if the export restriction appears only after an hour of work.
Show the export tiers before creation, keep the drawing saved on cancellation,
and offer any agreed free export. Login just before cloud purchase can bind the
transaction to a recoverable owner without blocking local exploration.

**Candidate C — free exports with a paid collaboration tier:** friendlier to solo
users; collaboration must justify recurring value. Define what happens when an
invited collaborator lacks a subscription and when the sponsor leaves.

**Example decision:** choose B, with an upfront explanation of export limits.
This accepts lower purchase exposure in exchange for evidence of value. Reject
silently deleting or locking the drawing after a cancelled purchase.

## Trials: compare cost and the opportunity to learn

Suppose an expensive operation costs $0.08, a user may perform 12 during a trial,
and 2,000 users are expected. The direct variable-cost envelope is
`0.08 × 12 × 2,000 = $1,920`, before retries, storage and support.
That calculation is a scenario, not a forecast. Compare it with a smaller sample
allowance or a reusable preview. If a hard ceiling matters, concurrent requests
and ambiguous charged outcomes must count before further work is admitted.

Ask when the customer can actually evaluate the product. A professional tool
used weekly may not reveal value during a trial that ends before a second use.
An instant export tool might be understood with one sample rather than a timer.

| Model | Eligibility authority | At the end | Important test |
|---|---|---|---|
| Free sample allowance | App's documented quota contract | Further paid action offers an upgrade | Relaunch and second device do not accidentally reset it |
| App-managed time window | App's documented clock/account policy | Access changes without an automatic store charge | Offline and clock manipulation follow the chosen contract |
| Store introductory trial | Store offer and purchase eligibility | Subscription follows the disclosed billing terms | Eligible and ineligible store accounts see truthful offers |

## Questions worth asking the owner

Ask a concrete choice, not a survey: “I found that creating a draft is local and
free. I recommend asking for payment at high-resolution export, while keeping
the draft on cancellation. Is preserving that free creation experience the
intended product contract?”

Do not ask for package IDs, current product names or whether a trial already
exists when you can inspect those facts. Do not silently choose prices, promise
free access or introduce a new data-retention policy.
