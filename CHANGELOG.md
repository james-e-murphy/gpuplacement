# Changelog

Earlier release candidate history predates this changelog.

## v1.0.0 (2026-07-17)

- Nebius H200 rows added: 4.50 on demand and 2.45 preemptible, published matches from the live price page. Named rows remain carbon-location proxies.
- B200 memory label corrected from 192GB to 180GB per the NVIDIA HGX B200 product carbon footprint summary and shipped OEM product guides.
- CoreWeave H200, B200 and L40S restored with on demand and spot derived from the current pricing page node rates; the stale L40S carried value of 1.40 was replaced by 2.25. A CoreWeave B300 spot only row was added at 4.48. A10 remains unavailable because the current page lists no A10 class product. Commitment fields stay empty with the advertised up to 60 percent reserved ceiling recorded. CoreWeave H100 and A100 minimum configuration derivations are unchanged and verified.
- RunPod H100 corrected to 2.99 on demand from the primary pricing page.
- Release identity unified: version and review date render from single constants and appear in the header, footer, CSV export and procurement print output.
- Evidence wording aligned: documentation now describes the amber diamond marker that the chart draws.
- Nebius commitment caveat recorded: advertised reservation savings of up to 35 percent are the ceiling for any future modeled Nebius commitment scenario.
