# User Guide

## 1. Define the scenario

Select the GPU type and quantity. Use the smallest realistic decision unit: a workload, service, training run or stable workload class.

## 2. Select a workload and pricing construct

The workload-type bands are decision prompts rather than automated recommendations:

- Unpredictable, experimental or peak workloads generally begin with on demand.
- Predictable workloads may justify commitment analysis.
- Interruptible workloads may qualify for spot or preemptible capacity.

Operational eligibility should override price. Do not include interruptible capacity for a workload that cannot checkpoint or recover within its service requirements.

## 3. Limit the feasible providers

Use provider filters to remove options that are not available, approved or operationally realistic. A mathematically attractive option is not a placement candidate until quota, region, security, data and support constraints are satisfied.

## 4. Add egress

Select a monthly egress scenario or enter a custom amount. The tool deducts the modeled free allowance and converts the remaining monthly cost to an hourly allocation for comparison.

## 5. Read the chart

In the raw view:

- vertical position represents effective per GPU hour cost for the selected pricing mode;
- horizontal position represents modeled carbon per GPU-hour;
- moving toward lower cost and lower carbon is directionally preferable, subject to workload constraints.

Hover over a point to inspect SKU, region, rate, rate basis, carbon and egress details.

An amber dashed halo means the rate is modeled, unverified or dependent on a fresh dynamic pricing snapshot. It does not indicate provider quality. Treat a modeled value as a scenario assumption and replace it with your current quote before making a decision.

The per-FLOP view divides published dense throughput by cost and carbon. Treat it as a hardware-efficiency view, not a workload benchmark.

## 6. Use the assumptions panel

Open the assumptions panel before relying on a result. Replace defaults with:

- current provider quotes;
- applicable commitment terms;
- organization-specific egress assumptions;
- actual hardware purchase costs;
- appropriate facility costs;
- a documented regional carbon factor.

Modified fields are scenario inputs. Preserve them with the share or export functions.

## 7. Use the TCO calculator

Enter observed utilization and a portfolio pricing mix. The model treats on demand and spot as pay-per-use and committed capacity as fully billed.

Review:

- blended rate;
- monthly cost;
- horizon TCO;
- lowest-cost region within each provider;
- commitment break-even utilization;
- active use carbon proxy.

A commitment threshold below observed utilization is a screening signal, not an approval. Include payment timing, capacity risk, migration effort and workload performance in the final business case.

## 8. Export and reproduce

- Use **Share this view** to preserve scenario inputs in a URL.
- Use **Export CSV** to retain the compared rows, units and rate-evidence classification.
- Use **Save PDF / Print** for a review artifact.
- Record the utility release and retrieval date with every exported decision artifact.

## 9. Validate before deciding

For shortlisted placements, obtain current quotes and run representative benchmarks. Validate achieved throughput, reliability, interruption behavior, data movement, operational support and organizational policy.

## 10. Report feedback or corrections

Send questions, bug reports, data corrections or methodology feedback to `REPLACE_WITH_FEEDBACK_EMAIL`.

Include the utility version and, where possible, a shared scenario URL or exported CSV. For rate or carbon-data corrections, include the provider/SKU or displayed location, the value in question, the retrieval date and a primary source.

