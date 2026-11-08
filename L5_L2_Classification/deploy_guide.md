# Deploy Guide — L_SIGUTILS
**Tier:** TIER_8_RF_MESH_DEFENSE | **Stack:** Python 3.11, sigutils (C lib + Python bindings), numpy, scipy, PAX 27B, AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, sigutils (C library, requires compile), numpy 1.26+, scipy 1.13+. SDR dongle.

## Environment
RTL-SDR or HackRF. sigutils C library compiled. 4GB RAM. CPU for DSP.

## AIOSS Integration
```bash
aioss init --module L_SIGUTILS --output ./l_sigutils.aioss
aioss append --chain ./l_sigutils.aioss --payload ./output.bin --module L_SIGUTILS
aioss verify --chain ./l_sigutils.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="L_SIGUTILS",
    aioss_chain="./L_SIGUTILS.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./L_SIGUTILS.aioss --verbose
python -m L_SIGUTILS.tests.smoke
```
