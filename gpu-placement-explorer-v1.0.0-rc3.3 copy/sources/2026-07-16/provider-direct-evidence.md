# Provider Direct Evidence Index :  2026-07-16

This index records the primary pages used for rc2 corrections. Live pages can change; final v1.0.0 should archive dated snapshots where source terms permit.

## RunPod

- Source: https://www.runpod.io/pricing
- Rc2 use: H100 SXM Pods $2.99/GPU-hour; B300 $7.39; H200 $4.39; B200 $5.89; A100 SXM $1.49; L40S $0.99.
- Commercial caveat: Reserved Clusters are contact-sales. Rc2 commitment and interruptible fields derived from static discounts are labeled modeled scenarios, not provider offers.

## Nebius

- Source: https://nebius.com/prices
- Rc2 use:
  - B300: $7.85 on demand; $4.30 preemptible.
  - B200: $7.15 on demand; $3.95 preemptible.
  - H100: $3.85 on demand; $2.15 preemptible.
- Geographic caveat: the public headline prices are not evidence for each named U.S. row. Rc2 marks those rows as carbon-location proxies.

## CoreWeave Classic

- General and minimum-configuration rules: https://www.coreweave.com/pricing/classic
- H100 GPU component: https://www.coreweave.com/pricing/classic/hgx-h100
- A100 GPU component: https://www.coreweave.com/pricing/classic/a100-80gb-nvlink

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
