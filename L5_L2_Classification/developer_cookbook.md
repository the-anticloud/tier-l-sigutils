# Developer Cookbook — L_SIGUTILS
**Stack:** Python 3.11, sigutils (C lib + Python bindings), numpy, scipy, PAX 27B, AIOSS_FORMAT
**Domain:** SigUtils: digital signal processing utilities for RF/SDR in Anticloud spectrum analysis

## Classify RF signal
```python
from l_sigutils import RFSignalClassifier

classifier = RFSignalClassifier(
    pax_model="./pax-27b-q4.gguf",
    aioss_chain="./sigutils.aioss"
)

iq_samples = sdr.read_samples(n=1024*256)  # IQ from SDR
result = classifier.classify(
    samples=iq_samples,
    center_freq_hz=433_920_000,
    sample_rate=2_400_000
)
print(f"Modulation: {result.modulation}")
print(f"Symbol rate: {result.symbol_rate:.0f} sps")
print(f"PAX: {result.pax_classification}")
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
