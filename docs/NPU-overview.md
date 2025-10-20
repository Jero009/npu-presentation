# NPU-learning — ključne točke

1. Pregled — kaj je NPU (kratka definicija)
2. Zgodovina in kontekst — zakaj so se pojavili, kdaj so postali pomembni
3. Glavni strojni gradniki — Processing Elements (PE), systolične matrike, on‑chip SRAM, DMA, NoC
4. Ključne operacije — MAC, GEMM, konvolucije, tenzorji; kje se porabi največ FLOP‑ov
5. Arhitekture in podatkovni pretoki — systolic, spatial/dataflow, tensor cores; kompromisi (fleksibilnost vs učinkovitost)
6. Številčni formati in kvantizacija — FP32/FP16/bfloat16, INT8/INT4; PTQ vs QAT; kalibracija
7. Programska veriga (toolchain) — train → export (ONNX/TF) → optimize (quantize/prune/fuse) → compile → runtime (TFLite, ONNX Runtime, TVM, vendor SDK)
8. Merila uspešnosti — latency, throughput, TOPS, TOPS/W, memory bandwidth, realistični benchmarki
9. Primeri uporabe — mobilne naprave, edge/IoT, kamere, speech/keyword spotting, strežniške/edge rekomendacije
10. Prednosti in slabosti v primerjavi s CPU/GPU — poraba energije, latenca, ops‑coverage, fleksibilnost
11. Praktične omejitve in izzivi — podpora operatorjem, omejitve pomnilnika, razhroščevanje in profiliranje, natančnost po kvantizaciji
12. Mini‑projekti za učenje (predlogi)
    - Projekt A (začetni): Izvozi majhen model (npr. MobileNetV2) v ONNX/TFLite.
    - Projekt B (vmesni): Naredi post‑training quantization v INT8, izmeri vpliv na natančnost.
    - Projekt C (ciljni): Kompiliraj kvantiziran model za NPU (vendor toolchain ali TVM) in izmeri latenco.
13. Viri za nadaljnje učenje — dokumentacija (TFLite, ONNX, TVM), vendor SDK, arhitekturnni članki
14. Naslednji korak — izberi poglavje (številka 1–13) za poglobljen zapis, diagram in praktično nalogo

Priložena slika (tvoj mind‑map)
![NPU mindmap](assets/npu-mindmap.png)

Opomba: naloži priloženo sliko v repozitorij pod potjo assets/npu-mindmap.png, da se prikaže v dokumentu.
