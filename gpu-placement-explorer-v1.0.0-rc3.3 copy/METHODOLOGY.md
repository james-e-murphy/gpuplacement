# Methodology

**Utility:** GPU Placement Explorer  
**Methodology version:** 1.0.0-rc3  
**Review date:** 2026-07-16  
**Author:** REPLACE_WITH_FULL_PROFESSIONAL_NAME

## 1. Purpose

GPU Placement Explorer is a comparative scenario model. It helps a practitioner identify economically plausible placement options and understand which assumptions drive the ranking. It does not predict a universally optimal provider or architecture.

The model uses the GPU as its principal capacity unit and expresses rates on a per GPU hour basis. Workload-specific benchmarking, availability, quota, data residency, reliability and contractual terms remain external decision inputs.

## 2. Data classifications

Each model input should be classified in the source ledger as one of the following:

- **Published:** copied from a public primary rate card or specification.
- **Derived:** calculated directly from a published value, such as dividing an eight-GPU node price by eight.
- **Estimated:** a transparent scenario assumption where a public value is unavailable.
- **Carried:** retained from an earlier verification pass and not re-verified for the current release.
- **User-entered:** supplied or edited by the practitioner.
- **Unavailable:** no defensible public value was identified; the option is not plotted for that pricing mode.

Published, derived and estimated values must not be presented with the same evidentiary status.

### 2.1 Rate evidence presentation

Release candidate rc3 attaches an evidence label to each provider/GPU/pricing-mode combination. The label appears in the tooltip, mobile ranking and CSV. Modeled, unverified and dynamic-snapshot-dependent values receive an amber dashed chart halo.

The halo communicates evidence quality only. It does not mean that a value is economically unattractive or that the provider is unreliable.

### 2.2 CoreWeave minimum-configuration derivation

CoreWeave Classic prices GPU, CPU, RAM and storage components separately. Rc2 uses the minimum valid a-la-carte Virtual Server configuration as a comparable floor:

```text
Minimum configuration rate
= GPU component
+ 1 vCPU × $0.01/vCPU-hour
+ 2 GB RAM × $0.005/GB-hour
+ 40 GB NVMe root disk × $0.07/GB-month ÷ 730 hours/month
```

This produces approximately $4.784/GPU-hour for HGX H100 and $2.234/GPU-hour for A100 80GB NVLINK. These are minimum configuration floors, not representative production configurations.

## 3. Cost model

### 3.1 Displayed rate

For a selected GPU, region and pricing mode, the chart displays the corresponding per GPU hour rate:

```text
Displayed rate = selected pricing field + hourly egress allocation
```

Pricing fields are:

- `cost`: on demand
- `committed`: one year commitment
- `committed3yr`: three year commitment
- `spot`: interruptible or preemptible

Where a provider has no defensible public value for the selected mode, the option is omitted rather than assigned a synthetic zero.

### 3.2 Egress

Monthly egress is converted to an hourly scenario allocation after deducting the provider's modeled free allowance:

```text
Chargeable GB/month = max(0, selected GB/month - free allowance)
Hourly egress allocation = chargeable GB/month × rate/GB ÷ 730
```

This is a presentation allocation. Actual egress charges depend on destination, service, tiering and negotiated terms.

### 3.3 Owned-hardware amortization

The hardware component of colocation and corporate-data-center cost is calculated as:

```text
Hardware amortization per GPU-hour = system acquisition cost ÷ GPU count ÷ amortization hours
Amortization hours = selected years × 8,760
```

Power and cooling assumptions are scaled relative to a 700 W H100-class baseline using the selected GPU's modeled TDP. Space and network components are not density-scaled. This is a disclosed simplification.

## 4. TCO model

The TCO panel accepts a portfolio mix across on demand, committed and spot capacity.

Let:

- `u` = utilization from 0 to 1
- `wOD`, `wCOM`, `wSPOT` = normalized pricing-mix weights
- `rOD`, `rCOM`, `rSPOT` = per GPU hour rates
- `g` = GPU count
- `h` = horizon in years

The blended hourly cost is:

```text
Blended $/GPU-hour = rOD × wOD × u
                   + rCOM × wCOM
                   + rSPOT × wSPOT × u
```

The committed segment is billed at 100 percent because the model treats it as purchased capacity. On-demand and spot segments scale with consumed hours.

```text
TCO = (blended $/GPU-hour + hourly egress allocation)
      × GPU count × 8,760 × horizon
```

The provider row uses the lowest-cost eligible region for that provider. Region detail remains available below the provider result.

### 4.1 Commitment break-even

For a pure committed-versus-on demand comparison, the displayed utilization threshold is:

```text
Break-even utilization = committed rate ÷ on demand rate
```

This threshold excludes switching costs, minimum quantities, payment timing, capacity risk and performance differences.

## 5. Carbon model

### 5.1 Carbon per GPU-hour

The raw chart uses average grid carbon intensity and GPU nameplate power:

```text
gCO2 per GPU-hour = grid intensity (gCO2/kWh) × GPU TDP (kW)
```

This is an IT-load comparative proxy. It currently excludes:

- facility PUE
- CPU, memory, storage and network power
- idle-power curves
- embodied emissions
- marginal-emissions effects
- provider renewable-energy contracting and market-based accounting

### 5.2 Annual carbon in the TCO panel

The release candidate patch scales annual carbon by the utilization input:

```text
Annual active use carbon proxy (tCO2e)
= gCO2/GPU-hour × GPU count × 8,760 × utilization ÷ 1,000,000
```

This is not a Scope 2 inventory. It is a consistent comparative proxy for active GPU use under the model's assumptions.

## 6. Performance-efficiency view

The optional per-FLOP view uses published dense BF16/FP16 hardware throughput:

```text
Compute per dollar = published dense TFLOPS ÷ $/GPU-hour
Compute per carbon = published dense TFLOPS ÷ kgCO2/GPU-hour
```

These ratios compare hardware specifications. They do not incorporate model FLOP utilization, goodput, batch size, communication overhead, failures or software efficiency.

For decision-grade unit economics, practitioners should separately estimate:

```text
Effective cost per useful unit
= billed capacity cost ÷ (occupancy × model utilization × successful-work goodput)
```

The current utility directly models occupancy/utilization at the capacity level but does not calculate workload specific MFU or goodput.

## 7. Geographic carbon mapping

Every plotted location must document how its displayed grid-intensity value was mapped. The preferred hierarchy is:

1. data-center-specific disclosed factor, where independently auditable;
2. eGRID subregion;
3. balancing authority;
4. state or regional proxy;
5. explicit scenario assumption.

The release ledger must record the mapping level and should not imply city-level precision when a broader regional proxy is used.

## 8. Validation protocol

Before tagging a release:

1. Hand-check one cost scenario for each pricing mode.
2. Hand-check one egress scenario with and without a free allowance.
3. Hand-check one owned-hardware amortization scenario.
4. Hand-check one carbon calculation for each GPU TDP class.
5. Confirm annual carbon responds to utilization.
6. Confirm committed cost remains fully billed when utilization changes.
7. Confirm share links restore every encoded input.
8. Confirm CSV and print outputs state their units and release version.

## 9. Change control

A new release is required when any of the following materially changes:

- provider rates or pricing constructs;
- GPU specifications;
- grid-intensity data;
- formulas or treatment of utilization;
- source classifications;
- model scope or disclosed exclusions.

## 10. Corrections and reproducibility reports

Methodology questions, reproducibility issues and proposed source corrections should be sent to `REPLACE_WITH_FEEDBACK_EMAIL`. Reports should identify the utility version, calculation or assumption at issue, expected result, observed result and supporting evidence.

