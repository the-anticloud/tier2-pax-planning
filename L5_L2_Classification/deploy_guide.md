# Deploy Guide — PAX_PLANNING
**Stack:** Python 3.11, PDDL, PAX 27B, networkx (plan DAG), AIOSS_FORMAT | Air-gap capable

## Prerequisites
Anticloud core stack installed. PAX 27B weights (pax-27b-q4.gguf). AIOSS_FORMAT.

## Install
```bash
pip install anticloud-pax-planning
```

## AIOSS Integration
```bash
aioss init --module PAX_PLANNING --output ./pax_planning.aioss
```

## Air-Gap
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(model_path="./pax-27b-q4.gguf", module="PAX_PLANNING",
                     aioss_chain="./pax_planning.aioss",
                     classification="L5_NARROW_L2_GENERAL")
```

## Verification
```bash
aioss verify --chain ./pax_planning.aioss --verbose
python -m pax_planning.tests.smoke
```
