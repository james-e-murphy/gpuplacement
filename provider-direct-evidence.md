# Provider Direct Evidence Index: 2026-07-16

This index records the primary pages used in the correction passes behind v1.0.0. Live pages can change; dated snapshots are tracked for v1.0.1 where source terms permit.

## RunPod

- Source: https://www.runpod.io/pricing
- Use in v1.0.0: H100 SXM Pods $2.99/GPU-hour; B300 $7.39; H200 $4.39; B200 $5.89; A100 SXM $1.49; L40S $0.99.
- Commercial caveat: Reserved Clusters are contact-sales. V1.0.0 commitment and interruptible fields derived from static discounts are labeled modeled scenarios, not provider offers.

## Nebius

- Source: https://nebius.com/prices
- Use in v1.0.0:
  - B300: $7.85 on demand; $4.30 preemptible.
  - B200: $7.15 on demand; $3.95 preemptible.
  - H100: $3.85 on demand; $2.15 preemptible.
  - H200: $4.50 on demand; $2.45 preemptible. Added for v1.0.0.
- Geographic caveat: the public headline prices are not evidence for each named U.S. row. V1.0.0 marks those rows as carbon-location proxies.
- Commitment caveat: Nebius advertises reservation savings of up to 35 percent without posting the discounted rates. V1.0.0 leaves Nebius commitment fields empty; any future modeled Nebius commitment scenario should treat 35 percent off the on demand rate as the ceiling.

## CoreWeave Classic

- General and minimum-configuration rules: https://www.coreweave.com/pricing/classic
- H100 and A100 GPU components: listed on the general Classic page above. The individual GPU child pages (/pricing/classic/hgx-h100 and /pricing/classic/a100-80gb-nvlink) returned 404 on 2026-07-16. Archive the general page when assembling the v1.0.1 evidence set.

### Minimum configuration calculation

CoreWeave Classic a-la-carte Virtual Servers require at least 1 GPU, 1 vCPU, 2 GB RAM and 40 GB root storage.

```text
Ancillary minimum hourly cost
= 1 × $0.01
+ 2 × $0.005
+ 40 × $0.07 ÷ 730
= $0.0238356/hour

H100 minimum configuration
= $4.76 + $0.0238356
= $4.7838356 ≈ $4.784/GPU-hour

A100 80GB minimum configuration
= $2.21 + $0.0238356
= $2.2338356 ≈ $2.234/GPU-hour
```

These are minimum valid configuration floors. Real workloads generally require substantially more CPU, RAM and storage.

## CoreWeave current platform: 2026-07-17

- Source: https://www.coreweave.com/pricing
- Provenance: page content provided directly by the author on 2026-07-17. Archive the page when assembling the v1.0.1 evidence set.
- Use in v1.0.0, per GPU rates derived from North America 8 GPU node prices:
  - H200: $6.31 on demand ($50.44/node); $2.62 spot ($20.93/node).
  - B200: $8.60 on demand ($68.80/node); $4.26 spot ($34.11/node).
  - L40S: $2.25 on demand ($18.00/node); $0.99 spot ($7.88/node, 0.985 exact).
  - B300: spot only, $4.48 ($35.84/node); on demand is contact sales.
- Commitment caveat: reserved capacity is contact sales with advertised discounts of up to 60 percent off on demand. Commitment fields stay empty; any future modeled CoreWeave commitment scenario should treat 60 percent off on demand as the ceiling.
- Egress: the page states no ingress, egress or transfer fees, confirming the free egress treatment already modeled for CoreWeave.
- Spec notes: the page lists 180GB VRAM for HGX B200, matching the corrected tier label, and 270GB for HGX B300, where the tier label keeps the NVIDIA 288GB specification.
- Regional caveat: the page prices by continent. Both named United States rows use the North America rate.
