# Sources and Data Provenance

**Ledger status:** Updated for `v1.0.0-rc3` on 2026-07-16. Every distinct provider/SKU assumption points to a primary source, an official dynamic pricing interface, or an explicit unverified/modeled classification. The rate conflicts identified in the first provider pass were corrected or visibly disclosed in rc3.

## A. Technical methodology sources

| ID | Input | Source | URL | Retrieved | Classification | Notes |
|---|---|---|---|---|---|---|
| EPA-EGRID-2023 | U.S. average regional grid factors | U.S. EPA, eGRID with 2023 data | https://www.epa.gov/egrid/detailed-data | 2026-07-16 | Published | Record the exact table and geographic mapping used for every displayed location. |
| NVIDIA-H100 | H100 memory, throughput and power | NVIDIA H100 product specifications | https://www.nvidia.com/en-us/data-center/h100/ | 2026-07-16 | Published/derived | Dense BF16/FP16 is derived from the applicable published figure; H100 SXM power is modeled at 700 W. |
| NVIDIA-H200 | H200 memory, throughput and power | NVIDIA H200 product specifications | https://www.nvidia.com/en-us/data-center/h200/ | 2026-07-16 | Published/derived | H200 uses H100-class dense compute and up to 700 W configurable TDP. |
| NVIDIA-HGX-B200 | B200 throughput and power | NVIDIA HGX B200 PCF Summary | https://images.nvidia.com/aem-dam/Solutions/documents/HGX-B200-PCF-Summary.pdf | 2026-07-16 | Published/derived | 36 PFLOPS FP16/BF16 is an eight-GPU sparsity figure; dense per-GPU value is 36 ÷ 2 ÷ 8 = 2.25 PFLOPS. |
| NVIDIA-DGX-B300 | B300 system throughput and power context | NVIDIA DGX B300 specifications | https://www.nvidia.com/en-us/data-center/dgx-b300/ | 2026-07-16 | Published/derived | Use system and per-GPU units carefully. |
| NVIDIA-HGX | B200/B300 eight-GPU throughput | NVIDIA HGX platform specifications | https://www.nvidia.com/en-us/data-center/hgx/ | 2026-07-16 | Published/derived | Use the exact table and footnote applicable to the release date. |

## B. Official provider source registry

The matrix in Section C uses these source IDs. A source URL is not, by itself, evidence that every value in the tool is current. Dynamic pricing interfaces require an exported result or dated screenshot with region, SKU, operating system, tenancy, purchase option and unit of sale.

| Source ID | Provider / construct | First-party source | Use in this release |
|---|---|---|---|
| AWS-OD | AWS EC2 On-Demand | https://aws.amazon.com/ec2/pricing/on demand/ | General official entry point. Save a Price List API or calculator snapshot for each SKU and region. |
| AWS-SP | AWS Savings Plans | https://aws.amazon.com/savingsplans/compute-pricing/ | Commitment construct source; exact effective rates require term and payment-option evidence. |
| AWS-SPOT | AWS EC2 Spot | https://aws.amazon.com/ec2/spot/pricing/ | Spot is AZ- and time-sensitive; preserve a timestamped snapshot. |
| AWS-P5 | AWS P5 product and published $55.04 p5.48xlarge example | https://aws.amazon.com/blogs/machine-learning/secure-short-term-gpu-capacity-for-ml-workloads-with-ec2-capacity-blocks-for-ml-and-sagemaker-training-plans/ | Supports $55.04/node ÷ 8 = $6.88/GPU-hour for the cited context; still verify the release-region rate. |
| AZ-API | Azure Retail Prices API documentation | https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices | Authoritative machine-readable interface. Store exact filtered JSON for every Azure SKU/region. |
| AZ-ENDPOINT | Azure Retail Prices API endpoint | https://prices.azure.com/api/retail/prices | Query source for pay-as-you-go and reservation records. |
| AZ-SPOT | Azure Spot Virtual Machines | https://azure.microsoft.com/en-us/pricing/spot-advisor/ | Spot rates/discounts are volatile; preserve date, region and SKU. |
| GCP-A3A4 | Google Cloud accelerator-optimized machine pricing | https://cloud.google.com/products/compute/pricing/accelerator-optimized | Official dynamic table for A2/A3/A4 families and consumption models. Save the relevant table rows. |
| GCP-CUD | Google Cloud committed use discounts | https://cloud.google.com/compute/docs/instances/committed-use-discounts-overview | Defines the commitment construct; exact rate must come from the pricing table or billing catalog. |
| GCP-SPOT | Google Cloud Spot VMs | https://cloud.google.com/compute/docs/instances/spot | Defines Spot provisioning; exact rate must be snapshotted. |
| OCI-LIST | Oracle Cloud Infrastructure price list | https://www.oracle.com/cloud/price-list/ | Official list-price source for GPU shapes. Preserve the exact shape row because the page changes. |
| LAMBDA | Lambda GPU cloud pricing | https://lambda.ai/pricing | Direct per GPU hour instance rates. Product size matters: the lowest values in the tool use the 8-GPU instance tier. |
| RUNPOD | RunPod GPU cloud pricing | https://www.runpod.io/pricing | Direct Pods rates. Distinguish Pods, Serverless, Clusters and Reserved Clusters. |
| CRUSOE | Crusoe Cloud pricing | https://www.crusoe.ai/cloud/pricing | Direct on demand GPU rates; current spot/reserved values are generally contact-sales. |
| NEBIUS | Nebius AI Cloud pricing | https://nebius.com/prices | Direct on demand and preemptible per GPU hour rates. |
| COREWEAVE-CLASSIC | CoreWeave Classic pricing | https://www.coreweave.com/pricing/classic | Public a-la-carte GPU, vCPU, RAM and storage prices plus minimum Virtual Server configuration rules. |
| COREWEAVE | CoreWeave current pricing | https://www.coreweave.com/pricing | Current product entry point; newer GPU prices may be quote based or not rendered in the public table. |

## C. Distinct provider/SKU rate assumptions in the utility

A row covers all listed tool region codes when the same price assumption is repeated. Values are dollars per GPU-hour. An em dash means the tool does not display a value for that mode.

| GPU | Provider | SKU / unit | Tool region codes | On-demand | 1-year | 3-year | Spot / preemptible | Source IDs | Validation result | Required caveat or action |
|---|---|---|---|---:|---:|---:|---:|---|---|---|
| B300 | RunPod | B300 Secure Cloud | rp-us-east; rp-us-west | 7.39 | :  | :  | :  | RUNPOD | On-demand: published match | Pods page directly lists $7.39/hr. Region labels are tool proxies, not rate-specific evidence. |
| B300 | Nebius | B300 SXM | nebius-us-east; nebius-us-central | 7.85 | :  | :  | 4.30 | NEBIUS | On-demand and preemptible: published matches | Named rows are carbon-location proxies; the public headline page does not substantiate region-specific price or inventory. |
| H200 | AWS | p5en.48xlarge /8 | us-east-1; us-west-2 | 7.91 | 5.14 | 3.56 | :  | AWS-OD; AWS-SP | Snapshot required | All displayed rates require official catalog/calculator export. Commitment values are modeled until term/payment evidence is attached. |
| H200 | GCP | a3-ultragpu /8 | us-central1; us-east4; us-west1 | 10.60 | 7.31 | 4.65 | 5.28 | GCP-A3A4; GCP-CUD; GCP-SPOT | Snapshot required | Save the exact A3 Ultra table row and provisioning model. Values are per node divided by eight. |
| H200 | OCI | BM.GPU.H200.8 /8 | oci-ashburn; oci-sanjose | 10.00 | 7.00 | 5.50 | 5.00 | OCI-LIST | On-demand row requires preserved snapshot; discounts are estimates | 1-year, 3-year and spot fields are generic modeled discounts, not published shape rates. |
| H200 | CoreWeave | H200 SXM5 | cw-us-east; cw-us-west | 6.31 | 4.10 | 2.84 | 2.62 | COREWEAVE; COREWEAVE-CLASSIC | No current public exact row identified | Do not mark any value verified. Replace with current quote/public row or set unavailable. |
| H200 | RunPod | H200 SXM | rp-us-east; rp-us-west | 4.39 | 3.29 | 3.29 | 2.55 | RUNPOD | On-demand: published match; other modes unsupported | Reserved Clusters are contact-sales; tool commitment/spot values are modeled and should be labeled or removed. |
| H200 | Crusoe | H200 HGX | crusoe-tx; crusoe-va | 4.29 | 3.43 | 2.57 | :  | CRUSOE | On-demand: published match; commitments unsupported | Current public page lists on demand $4.29 and contact-sales for spot. Commitment values are estimates. |
| B200 | AWS | p6-b200.48xlarge /8 | us-east-1; us-east-2; us-west-2 | 14.24 | 11.22 | 6.15 | 2.70 | AWS-OD; AWS-SP; AWS-SPOT | Snapshot required | Preserve official catalog records. Spot must include timestamp and AZ; commitment must include plan/term/payment. |
| B200 | GCP | a4-highgpu /8 | us-central1; us-east4 | :  | 11.12 | 7.09 | 4.28 | GCP-A3A4; GCP-CUD; GCP-SPOT | Snapshot required; construct mapping review | The tool intentionally has no on demand value. Verify whether each displayed mode corresponds to reservation, flex-start/DWS, CUD or Spot. |
| B200 | CoreWeave | HGX B200 | cw-us-east; cw-us-west | 8.60 | 5.59 | :  | 4.26 | COREWEAVE; COREWEAVE-CLASSIC | No current public exact row identified | All values require current public evidence or a dated quote. Do not infer current pricing from an older promo. |
| B200 | Lambda Labs | B200 SXM6 | lambda-us-east; lambda-us-west | 6.69 | :  | :  | :  | LAMBDA | On-demand: published match | The $6.69 rate is the 8-GPU tier; smaller instance sizes cost more per GPU. |
| B200 | RunPod | B200 Secure Cloud | rp-us-east; rp-us-west | 5.89 | 5.01 | :  | :  | RUNPOD | On-demand: published match; commitment unsupported | Reserved Clusters are contact-sales; $5.01 is not directly published on the current page. |
| B200 | Nebius | B200 SXM | nebius-us-east; nebius-us-central | 7.15 | :  | :  | 3.95 | NEBIUS | On-demand and preemptible: published matches | Corrected in rc3. Named rows are carbon-location proxies; no region-differentiated public price was identified. |
| L40S | AWS | g6e.2xlarge | us-east-1; us-west-2 | 2.02 | 1.41 | 1.01 | 0.81 | AWS-OD; AWS-SP; AWS-SPOT | Snapshot required | Node includes CPU/RAM; preserve exact region, OS and purchase option. |
| L40S | Azure | NVads L40S v5 | eastus; westus3 | 2.50 | 1.75 | 1.25 | 0.50 | AZ-API; AZ-ENDPOINT; AZ-SPOT | Snapshot required | Store filtered Retail Prices API JSON and confirm exact armSkuName and meter. |
| L40S | CoreWeave | L40S PCIe | cw-us-east; cw-us-west | 1.40 | 1.12 | 0.91 | 0.70 | COREWEAVE; COREWEAVE-CLASSIC | No current public exact row identified | Classic page retrieved in this pass did not expose an exact L40S row. Values remain unverified. |
| L40S | RunPod | L40S | rp-us-east; rp-us-west | 0.99 | 0.74 | 0.74 | 0.58 | RUNPOD | On-demand: published match; other modes unsupported | Current Pods page lists $0.99. Reserved rates are contact-sales; Community Cloud is not equivalent to Spot. |
| L40S | Crusoe | L40S | crusoe-tx; crusoe-va | 1.50 | 1.20 | 0.90 | :  | CRUSOE | On-demand: published match; commitments unsupported | Current page lists $1.50 on demand and contact-sales for spot. Commitment values are estimates. |
| H100 | AWS | p5.48xlarge /8 | us-east-1; us-east-2; us-west-2 | 6.88 | 4.47 | 2.97 | 3.37 | AWS-P5; AWS-SP; AWS-SPOT | On-demand derivation supported; other modes snapshot required | $55.04/node ÷ 8 = $6.88/GPU-hour for the cited AWS example. Reconfirm release region and save plan/spot evidence. |
| H100 | Azure | NC40ads H100 v5 | eastus; southcentralus; westus3 | 6.98 | 4.89 | 3.49 | 1.40 | AZ-API; AZ-ENDPOINT; AZ-SPOT | Snapshot required | Save exact API rows. Spot price must be dated and region-specific. |
| H100 | GCP | a3-highgpu-8g /8 | us-east4; us-central1; us-west1 | 11.06 | 7.67 | 4.86 | 4.74 | GCP-A3A4; GCP-CUD; GCP-SPOT | Snapshot required | Save exact table rows and divide node price by eight. Confirm attached CPU/RAM/storage treatment. |
| H100 | OCI | BM.GPU.H100.8 /8 | oci-ashburn; oci-phoenix; oci-sanjose | 10.00 | 7.00 | 5.50 | 5.00 | OCI-LIST | On-demand row requires preserved snapshot; discounts are estimates | 1-year, 3-year and spot values are generic modeled discounts, not published shape rates. |
| H100 | Lambda Labs | H100 SXM | lambda-us-east; lambda-us-west | 3.99 | 3.39 | 2.99 | :  | LAMBDA | On-demand: published match; commitments unsupported | $3.99 is the 8-GPU tier. Reserved pricing is contact-sales; commitment values are estimates. |
| H100 | CoreWeave | HGX H100 minimum a-la-carte configuration | cw-us-east; cw-us-west | 4.784 | 3.11 | 2.15 | 1.91 | COREWEAVE-CLASSIC | On-demand: derived minimum configuration; other modes modeled | $4.76 GPU + 1 vCPU at $0.01/hr + 2 GB RAM at $0.005/GB-hr + 40 GB NVMe at $0.07/GB-month ÷ 730. Named rows are carbon proxies. The resulting shape is a floor, not a representative production configuration. |
| H100 | RunPod | H100 SXM | rp-us-east; rp-us-west | 2.99 | 2.24 | 2.24 | 1.73 | RUNPOD | On-demand: published match; other modes modeled | Corrected in rc3. Reserved Clusters are contact-sales; commitment and interruptible values are scenario discounts, not provider offers. |
| H100 | Crusoe | H100 HGX | crusoe-tx; crusoe-va | 3.90 | 3.12 | 2.34 | :  | CRUSOE | On-demand: published match; commitments unsupported | Current page lists $3.90 on demand and contact-sales for spot. Commitment values are estimates. |
| H100 | Nebius | H100 SXM | nebius-us-east; nebius-us-central | 3.85 | :  | :  | 2.15 | NEBIUS | On-demand and preemptible: published matches | Named rows are carbon-location proxies unless region-specific availability evidence is attached. |
| A100 | AWS | p4d.24xlarge /8 | us-east-1; us-east-2; us-west-2 | 2.74 | 1.92 | 1.37 | 1.10 | AWS-OD; AWS-SP; AWS-SPOT | Snapshot required | Save exact catalog/calculator records. Instance includes eight GPUs and attached resources. |
| A100 | Azure | NC24ads A100 v4 | eastus; southcentralus | 3.67 | 2.57 | 1.83 | 0.73 | AZ-API; AZ-ENDPOINT; AZ-SPOT | Snapshot required | Save exact Retail Prices API rows and SKU/region mapping. |
| A100 | GCP | a2-ultragpu-1g | us-central1; us-east4 | 5.07 | :  | :  | 2.53 | GCP-A3A4; GCP-SPOT | Snapshot required | Confirm A2 machine shape and whether the displayed amount includes all mandatory machine resources. |
| A100 | OCI | BM.GPU.A100-v2 /8 | oci-ashburn; oci-phoenix | 5.00 | 3.50 | 2.75 | 2.50 | OCI-LIST | On-demand row requires preserved snapshot; discounts are estimates | Commitment and spot fields are generic modeled discounts. |
| A100 | Lambda Labs | A100 SXM 80GB | lambda-us-east; lambda-us-west | 2.79 | 2.37 | 2.09 | :  | LAMBDA | On-demand: published match; commitments unsupported | $2.79 is the 8-GPU 80GB SXM tier. Commitment values are estimates. |
| A100 | CoreWeave | A100 80GB NVLINK minimum a-la-carte configuration | cw-us-east; cw-us-west | 2.234 | 1.45 | 1.01 | 0.89 | COREWEAVE-CLASSIC | On-demand: derived minimum configuration; other modes modeled | $2.21 GPU + the same $0.0238356/hr minimum CPU/RAM/root-storage allocation. Named rows are carbon proxies. This is a floor, not a representative production configuration. |
| A100 | RunPod | A100 SXM | rp-us-east; rp-us-west | 1.49 | 1.12 | 1.12 | 0.87 | RUNPOD | On-demand: published match; other modes unsupported | Current Pods page lists $1.49. Reserved/alternative product prices are not equivalent to static 1-year/3-year/spot fields. |
| A100 | Crusoe | A100 80GB SXM | crusoe-tx; crusoe-va | 2.30 | 1.84 | 1.38 | :  | CRUSOE | On-demand: published match; commitments unsupported | Current page lists $2.30 on demand and contact-sales for spot. Commitment values are estimates. |
| A10G | AWS | g5.2xlarge | us-east-1; us-east-2; us-west-2 | 1.006 | 0.592 | 0.402 | 0.540 | AWS-OD; AWS-SP; AWS-SPOT | Snapshot required | Save exact region, OS, tenancy, plan and spot timestamp. |
| A10 | Azure | NC8ads A10 v4 | eastus; southcentralus | 1.430 | 1.100 | 0.858 | 0.264 | AZ-API; AZ-ENDPOINT; AZ-SPOT | Snapshot required | Save exact API rows; verify whether quoted spot value is current and available. |
| L4 proxy | GCP | g2-standard-4 | us-central1; us-east4; us-west1 | 0.707 | 0.445 | 0.318 | 0.311 | GCP-A3A4; GCP-CUD; GCP-SPOT | Snapshot required; hardware identity disclosed | Rc2 labels the tier `A10G / L4 (24GB)`. The GCP machine uses NVIDIA L4 and is included as a comparable 24GB alternative, not as an A10G SKU. |
| A10 | OCI | VM.GPU.A10.1 | oci-ashburn; oci-phoenix | 2.000 | 1.400 | 1.100 | 1.000 | OCI-LIST | On-demand row requires preserved snapshot; discounts are estimates | Official list-price row should be archived; other modes are modeled discounts. |
| A10 | CoreWeave | A10 on demand | cw-us-east; cw-us-west | 0.850 | 0.680 | 0.553 | 0.425 | COREWEAVE; COREWEAVE-CLASSIC | No current public exact row identified | Current public Classic page retrieved in this pass did not expose an A10 row. All modes remain unverified. |

## D. Evidence labels to use

Use these labels without softening them:

- **Published list price:** the provider directly displays the exact SKU, product and unit.
- **Derived from published node price:** arithmetic conversion from a directly published node/instance rate; state the divisor and attached resources.
- **Official dynamic snapshot required:** the provider publishes through an API, calculator or dynamic table; archive the exact result.
- **Estimated discount scenario:** a modeled rate, not a provider offer.
- **Conflict with current primary source:** the current official page differs from the tool.
- **No defensible public value identified:** set the field to unavailable or support it with a dated quote that can be reviewed.

### Required snapshot fields for hyperscalers

For AWS, Azure and Google Cloud evidence, preserve at minimum:

- provider and service;
- exact SKU/meter/machine type;
- region and, for Spot, availability zone where applicable;
- operating system, tenancy and any attached-resource assumptions;
- purchase option, term and payment option;
- currency and unit;
- retrieval timestamp;
- raw API/calculator output or screenshot;
- per-GPU derivation.

## E. Rc2 source-validation resolution and remaining findings

### Corrected or disclosed in rc3

1. **RunPod H100 SXM:** corrected from $3.29 to the current $2.99 published Pods rate. Other modes are labeled modeled.
2. **Nebius B200:** corrected from $5.50 to $7.15 on demand and added $3.95 preemptible.
3. **Nebius preemptible:** added B300 $4.30 and H100 $2.15.
4. **CoreWeave H100:** rebuilt as a $4.784 minimum a-la-carte configuration from the $4.76 GPU component plus minimum CPU, RAM and root storage.
5. **CoreWeave A100:** rebuilt as a $2.234 minimum configuration from the $2.21 GPU component plus the same ancillary minimum.
6. **GCP g2-standard-4:** the UI now calls the tier `A10G / L4 (24GB)` and identifies this row as L4.
7. **Modeled commercial discounts:** the tooltip, mobile ranking and CSV state the rate basis; modeled/unverified values receive an amber dashed chart halo.
8. **Regional proxy semantics:** corrected Nebius and CoreWeave rows explicitly state `carbon proxy` when the rate is not supported as region-specific.

### Still open before final v1.0.0

1. **Dynamic hyperscaler values:** exact dated AWS, Azure and Google Cloud API/calculator results must be committed.
2. **Unverified carried values:** remaining CoreWeave H200/B200/L40S/A10 and other carried rows require primary evidence or removal.
3. **Modeled commitment/spot values:** retain only where analytical scenario value is intentional; replace with current quotes for any submitted worked example.
4. **Regional availability:** a repeated national price must not imply that the SKU is available in each named location.
5. **Non-compute provenance:** egress, owned-infrastructure assumptions and carbon-region mappings remain separate release gates.

## F. Recommended repository evidence layout

```text
sources/
  2026-07-16/
    aws/
      p5.48xlarge-us-east-1-on demand.json
      ...
    azure/
      NC40ads-H100-v5-eastus-retail-prices.json
      ...
    gcp/
      accelerator-optimized-pricing.pdf-or-html
      ...
    provider-page-snapshots/
      runpod-pricing.pdf
      lambda-pricing.pdf
      crusoe-pricing.pdf
      nebius-pricing.pdf
      coreweave-classic-pricing.pdf
```

Do not rely only on live URLs. Pages and rates change; a release must remain auditable after publication.

## G. Remaining provenance work outside provider compute rates

This pass does not complete:

- egress rates and free allowances;
- colocation and corporate data-center components;
- hardware acquisition-cost assumptions;
- carbon-region mappings;
- quote-only provider SKUs;
- provider-specific taxes and currency effects.

## H. Release gate

Do not tag v1.0.0 until:

- the corrected rc3 values remain consistent across code, UI, CSV and this ledger;
- exact AWS, Azure and GCP snapshots are committed;
- every estimated discount is visibly labeled in the UI and exported data;
- duplicate regional proxy rows do not imply unsupported regional availability or price variation;
- source changes are recorded in `CHANGELOG.md`.
