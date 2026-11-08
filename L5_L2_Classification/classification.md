# L5 Narrow / L2 General Classification — L_SIGUTILS
**Platform:** Anticloud | **Tier:** TIER_8_RF_MESH_DEFENSE | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
L_SIGUTILS provides low-level RF signal processing utilities for Anticloud: FM/AM demodulation, channel equalization, modulation classification, and signal parameter estimation. Narrow scope: Anticloud RF signal processing for spectrum analysis.

## L2 General
L2 General: L_SIGUTILS is the DSP foundation for all Anticloud SDR processing. L_OPENWEBRX and L_RETICULUM both depend on L_SIGUTILS for modulation analysis.

## PAX 27B Integration
PAX 27B classifies detected signals: 'Modulation pattern matches 802.15.4 (ZigBee) at 2.4GHz, RSSI -68dBm — likely IoT sensor in building. Not anomalous.'

## AIOSS Audit Chain
Every signal analysis (baseband samples hash + modulation detection result hash + signal parameters hash + PAX classification) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
ITU-R SM.329 (spurious emissions). FCC Part 15. Passive receive only.
