```markdown
# Predstavitev NPU — PowerPoint osnutek

Diapozitiv 1 — Naslov
- Naslov: Uvod v NPU
- Podnaslov: Neural Processing Units — kaj so in zakaj so pomembni
- Predavatelj: Jero009

Diapozitiv 2 — Kaj je NPU?
- Definicija: Neural Processing Unit (namenjena pospeševanju nevronskih mrež)
- Kratek seznam: MAC operacije, tenzorski izračuni, nizka poraba za inferenco

Diapozitiv 3 — Zakaj NPU-ji?
- Energetska učinkovitost (TOPS/W)
- Nizek odzivni čas (latenca) za lokalno inferenco
- Primeri uporabe: mobilne naprave, edge, IoT, strežniška inferenca

Diapozitiv 4 — Temeljni gradniki
- Matrične množitve / MAC matrike, on-chip SRAM, DMA, vzorci pretoka podatkov
- Številčni formati: FP16, bfloat16, INT8, INT4

Diapozitiv 5 — Arhitekture
- Systolične matrike, prostorski/dataflow pospeševalniki, vektorski/tensor motorji

Diapozitiv 6 — Programska skladba
- Treniraj -> izvozi (ONNX/TensorFlow) -> optimiziraj (kvantiziraj/obreži) -> kompiliraj -> runtime

Diapozitiv 7 — Primeri uporabe in ponudniki
- Apple ANE, Google Edge TPU, Qualcomm NPU, Intel Movidius, Huawei Ascend

Diapozitiv 8 — Praktične stvari
- Podpora operacijam, kompromisi kvantizacije, omejitve pomnilnika, orodja za razhroščevanje

Diapozitiv 9 — Načrt demonstracije
- Pretvori majhen klasifikator v TFLite/ONNX, kvantiziraj v INT8, zaženi na emulatorju ali napravi

Diapozitiv 10 — Naslednji koraki / Viri
- Povezave do TFLite, ONNX Runtime, TVM in relevantnih člankov
```
