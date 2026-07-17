# GPU Placement Explorer

GPU Placement Explorer is an open source decision support utility for comparing GPU workload placement across public cloud, neocloud, colocation and corporate data-center options.

It is designed for FinOps practitioners, engineers, architects, procurement teams and sustainability stakeholders who need to expose the assumptions behind GPU placement decisions rather than compare hourly rates in isolation.

## Current release

- Application: `index.html`, a single self contained file with no build step
- Status: `v1.0.0`, the submitted release
- Rate/source review date: 2026-07-17

## What the utility evaluates

- GPU type and count
- Provider and region or explicit carbon-location proxy
- On-demand, one year commitment, three year commitment and interruptible pricing
- Evidence basis for each displayed rate
- Workload utilization and portfolio pricing mix
- Data-egress assumptions
- Owned-hardware amortization and facility cost components
- Average grid carbon intensity
- Published hardware throughput ratios

## Rate evidence in v1.0.0

Every displayed rate is assigned an evidence basis. Hover over a point, inspect the mobile ranked view or export CSV to see the classification.

- **Published list price:** exact SKU and unit shown by the provider.
- **Derived:** direct arithmetic from a published node price or minimum valid configuration.
- **Official dynamic snapshot:** sourced from a provider API, calculator or changing table and requires a dated archived result.
- **Modeled discount scenario:** an analytical assumption, not a provider offer.
- **Unverified carried value:** retained for scenario continuity but not release-grade evidence.

An amber diamond marker on a chart point marks modeled, unverified or dynamic-snapshot-dependent values. It is an evidence warning, not a cost or performance judgment.

## Use the hosted utility

Live site: `REPLACE_WITH_FULL_CUSTOM_DOMAIN_URL`

Source repository: `REPLACE_WITH_FULL_GITHUB_REPOSITORY_URL`

Release tag: `v1.0.0`

## Run locally

The application is a self contained HTML file with no build step.

1. Download `index.html` from the repository or the v1.0.0 release.
2. Open it in a modern browser.
3. For consistent local sharing and browser behavior, serve the directory with a simple local web server, for example:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/`.

## Suggested practitioner workflow

1. Select the GPU type and count.
2. Select a workload type and corresponding pricing construct.
3. Limit the visible providers to options that are operationally feasible.
4. Add expected egress.
5. Inspect cost, carbon and rate evidence by provider and region.
6. Open the TCO calculator and enter observed utilization, not planned utilization.
7. Replace defaults with current quotes and organizational assumptions.
8. Export the scenario and record the utility release used.
9. Validate shortlisted options with workload benchmarks, availability checks and commercial review.

See [USER-GUIDE.md](USER-GUIDE.md) for detailed usage, [METHODOLOGY.md](METHODOLOGY.md) for calculation logic, [SOURCES.md](SOURCES.md) for provenance, and [LIMITATIONS.md](LIMITATIONS.md) for model boundaries.

## FinOps Framework alignment

Primary capability:

- Architecting & Workload Placement

Supporting capabilities:

- Planning & Estimating
- Rate Optimization
- Usage Optimization
- Sustainability
- Unit Economics
- Automation, Tools & Services

## Important disclosure

This is a scenario model, not a procurement quote, emissions inventory or substitute for workload testing. Rates may include published, derived, dynamically retrieved, carried or explicitly modeled values. Carbon calculations use average grid intensity and GPU nameplate power and exclude facility PUE, other system power, embodied emissions and marginal-emissions effects. Published FLOPS are hardware specifications and do not predict achieved workload throughput.

The `A10G / L4` tier deliberately groups comparable 24GB accelerators; Google Cloud `g2-standard-4` uses an NVIDIA L4 and is not an A10G SKU.

## Versioning

The companion practitioner brief should identify the exact release and commit used for its examples. Material pricing, source or methodology changes should produce a new tagged release and changelog entry.

## Licensing

- Software: Apache License 2.0
- Companion practitioner brief: CC BY 4.0
- Third-party data: remains subject to the original source terms


## Visual position

The utility uses the same restrained navy, teal, white space, and editorial typography as the related research papers and author site. It names its FinOps Framework alignment without using Foundation logos or implying Foundation endorsement.

## Feedback and corrections

Questions, bug reports, source corrections and methodology feedback are welcome at `REPLACE_WITH_FEEDBACK_EMAIL`.

For a useful report, include the utility version, shared scenario URL or exported CSV where available, the affected provider/SKU or calculation, and a supporting primary source for pricing or data corrections.

## Author

James E. Murphy
