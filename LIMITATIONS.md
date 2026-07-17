# Limitations

GPU Placement Explorer is a comparative scenario utility. Its outputs are directional and assumption-sensitive.

## Pricing and commercial limitations

- Public list prices may differ from negotiated rates, private offers, marketplace terms and enterprise agreements.
- Commitment estimates may omit payment timing, minimum quantities, exchange rates, taxes, support, software and ancillary services.
- Spot and preemptible prices and availability can change rapidly.
- A listed SKU may not be available in every displayed geography, quota tier or account.
- Node-level prices are sometimes divided by GPU count and therefore do not isolate CPU, memory, storage or networking value.
- CoreWeave H100 and A100 values use the minimum valid a-la-carte configuration. They are cost floors, not recommended or representative production shapes.
- An amber evidence marker identifies modeled, unverified or dynamic-snapshot-dependent rates; it does not validate availability or commercial eligibility.
- Egress depends on service, source, destination, tier, routing and free allowances; the model uses a simplified hourly allocation.

## Workload and operational limitations

- The model does not determine whether a workload is portable.
- It does not model data gravity, migration effort, orchestration changes, security review, compliance, sovereignty, resilience or fallback capacity.
- It does not predict queue time, provisioning latency, interruption frequency or replacement capacity.
- Published FLOPS do not predict achieved throughput, latency, token rate, training time or goodput.
- MFU, communication overhead, software efficiency and failure recovery must be validated separately.

## Owned-infrastructure limitations

- Hardware acquisition costs are editable scenario assumptions, not vendor quotes.
- Power and cooling components are scaled by GPU TDP from a baseline; density effects are simplified.
- Space, network, staffing, financing, taxes, spares, maintenance and residual value may not be fully represented.
- Hardware obsolescence and generation risk are not probabilistically modeled.
- Marginal-cost views can be misleading if shared fixed costs or capacity constraints are omitted.

## Carbon limitations

- The model uses average grid carbon intensity, not marginal emissions.
- The raw carbon axis is GPU nameplate power multiplied by grid intensity.
- Annual TCO carbon is an active use proxy scaled by utilization.
- Facility PUE, CPU/memory/network power, idle-power curves and embodied emissions are excluded.
- Provider renewable-energy contracts and market-based Scope 2 accounting are not represented.
- Regional values may use geographic proxies and should not be interpreted as facility-specific emissions.
- The output is not a corporate GHG inventory or assurance-ready calculation.

## Decision-use limitation

The utility should narrow the decision space and expose assumptions. It should not authorize procurement, architecture or sustainability decisions without current commercial quotes, workload telemetry, benchmark results and organizational constraints.

## Reporting errors

Report suspected calculation defects, stale provider data or unclear disclosures to `REPLACE_WITH_FEEDBACK_EMAIL`. Include the utility version and enough scenario detail to reproduce the issue.

