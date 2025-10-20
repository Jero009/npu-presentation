```markdown
# Spoznavanje NPU-jev — učni zapiski

Namen
- Ta dokument je vodnik za samostojno učenje in zapiski, ki ti bodo pomagali spoznati, kaj je Neural Processing Unit (NPU), zakaj je pomemben in kako dobiti praktične izkušnje. Priporočeno je delati po vrstnem redu; izberi eno temo naenkrat za poglobljeno učenje in vaje.

Kazalo
1. Pregled — Kaj je NPU  
2. Zakaj NPU-ji obstajajo  
3. Matematika in osnovni pojmi  
4. Strojni gradniki NPU-jev  
5. Arhitekture in načini pretoka podatkov  
6. Številčni formati in kvantizacija  
7. Programska skladba in orodja  
8. Metrične uspešnosti in merjenje zmogljivosti  
9. Primeri uporabe in dejanski izdelki  
10. Praktični vidiki pri uvajanju  
11. Praktična pot (korak za korakom mini projekti)  
12. Dodatna literatura in viri  
13. Slovarček

---

1) Pregled — Kaj je NPU
- Definicija: NPU (Neural Processing Unit) je specializiran strojni pospeševalnik, zasnovan za izvajanje izračunov nevronskih mrež (matrične množitve, konvolucije, aktivacijske funkcije, tenzorski postopki) bolj učinkovito (v smislu latence, prepustnosti in porabe energije) kot splošni CPU.
- Enostavna analogija: CPU = vsestranski pripomoček, GPU = kuhinja z mnogimi kuharji (splošna paralelna obdelava), NPU = stroj za peko kruha, izjemno optimiziran za eno vrsto naloge.
- Cilj: Po tem razdelku znaš v eni povedi razložiti, kaj NPU počne in zakaj se razlikuje od CPU/GPU.

2) Zakaj NPU-ji obstajajo
- Nevronske mreže temeljijo na ponavljajočih se jedrnih računskih jedrih (GEMM, konvolucije, elementarne operacije). CPU-ji so prilagodljivi, vendar neučinkoviti za te ponavljajoče vzorce; GPU-ji so dobri za goste paralelne izračune, a porabijo več energije in imajo drugačne omejitve pomnilnika.
- NPU-ji so optimizirani za energijsko učinkovito inferenco (včasih tudi nekatere oblike učenja) z nizko latenco na napravah (telefoni, kamere, IoT) ali v strežnikih z omejitvami porabe.
- Ključni gonilniki: avtonomija baterije, toplotne omejitve, aplikacije, ki potrebujejo nizko latenco, in cena na enoto inferenc.

3) Matematika in osnovni pojmi
- Matrična množitev (GEMM): gradnik gostih plasti in številnih transformacij.
- Konvolucija: drseče okno z množenjem in seštevanjem (CNN) — razumi im2col v primerjavi z direktno konvolucijo.
- MAC (multiply-accumulate): osnovna operacija, ki jo pospešujejo NPU-ji (pomnoži in seštej).
- Tenzor: večdimenzionalno polje (oblika, osi) in pogosti razporedi (NCHW proti NHWC).
- Redkost in pruning: ničelne uteži/aktivacije se lahko izkoristijo za pospešek in varčevanje z energijo.
- Cilj: Prepoznati, katere operacije porabijo največ FLOP-ov v modelu.

4) Strojni gradniki NPU-jev
- Processing Elements (PE): majhne računske enote, ki izvajajo MAC operacije.
- Systolične matrike: 2D mreža PEs, ki si ritmično prenašajo podatke za ponovno uporabo operandov in zmanjšanje potrebo po dostopu do zunanjega pomnilnika.
- On-chip SRAM / scratchpad: hitro lokalno pomnilnik za ploščice aktivacij in uteži.
- DMA in streaming enote: upravljanje premikov podatkov med DRAM in on-chip pomnilnikom.
- Interconnect / network-on-chip (NoC): usmerjanje podatkov med PEs in pomnilnikom.
- Cilj: Razumeti vlogo on-chip pomnilnika in zakaj premikanje podatkov pogosto prevlada nad samo računskimi stroški.

5) Arhitekture in načini pretoka podatkov
- Systolične arhitekture (TPU-podobno): odlično za goste matrične množitve z visoko stopnjo ponovno uporabe podatkov.
- Prostorski/dataflow pospeševalniki: preslikava operatorjev prostorsko na strojno opremo za zmanjšanje odvečnega premikanja podatkov.
- Vektorski/tensor motorji: široke vektorske enote in specializirane instrukcije (pogosto v GPU-jih z tensor jedri).
- Kompromisi: fleksibilnost proti vrhunski učinkovitosti; nekateri dizajni optimizirajo nizke šarže (latenca), drugi velikanske šarže (prepustnost).
- Cilj: Našteti vsaj dve stilski arhitekturi ter razumeti njune kompromise.

6) Številčni formati in kvantizacija
- Plavajoča vejica: FP32 (trening), FP16 / bfloat16 (mešano treniranje / inferenca).
- Celi števili: INT8, INT4 — pogosti za inferenco za zmanjšanje pomnilniških zahtev in povečanje gostote izračuna.
- Vrste kvantizacije:
  - Post-training quantization (PTQ): pretvorba že naučenega modela v nižjo natančnost.
  - Quantization-aware training (QAT): simulacija kvantizacije med treningom za boljšo natančnost.
- Kalibracija: zbiranje reprezentativnih vhodov za izračun skal in ničelnih točk.
- Cilj: Vedeti, kdaj uporabiti PTQ vs QAT in tipične kompromise med natančnostjo in učinkovitostjo.

7) Programska skladba in orodja
- Potek: Train (PyTorch/TensorFlow) -> Export (ONNX, SavedModel) -> Optimize (kvantiziraj, obreži, združi) -> Compile to target -> Run on device (runtime).
- Primeri orodij: TensorFlow Lite, ONNX Runtime, Apache TVM, vendor kompilatorji in SDK-ji (Qualcomm, Apple, Huawei).
- Vendor runtime-i običajno nudijo seznam podprtih operatorjev in mehanizme za fallback na CPU.
- Cilj: Razumeti glavne korake pri selitvi modela iz raziskovalnega okolja na NPU runtime.

8) Metrične uspešnosti in merjenje zmogljivosti
- TOPS / TOPS/W: surova operativna prepustnost in energetska učinkovitost.
- Latenca proti prepustnosti: odzivni čas za posamezne zahteve (real‑time aplikacije) in prepustnost za serijsko obdelavo.
- Pomnilniška prepustnost in kapaciteta on-chip: lahko omejujeta zmogljivost, če je premikanje podatkov veliko.
- Realistično merjenje: uporabiti celotno latenco modela, vključiti predobdelavo in testirati s predstavitvenimi vhodnimi podatki.
- Cilj: Vedeti, katere metrike so pomembne za tvojo uporabo in katere pastmi se izogniti pri benchmarkih.

9) Primeri uporabe in dejanski izdelki
- Pogoste uporabe: obdelava slike na napravi (prepoznavanje obrazov, segmentacija), prepoznavanje govora, ključne besede, AR/ML na kamerah, priporočilni sistemi na robu.
- Primeri NPU-jev: Apple Neural Engine (ANE), Google Edge TPU / Cloud TPU, Qualcomm Hexagon NPU, Intel Movidius (VPU), Huawei Ascend.
- Cilj: Prepoznati, kateri ponudnik/platforma je primerna za tvojo ciljno napravo.

10) Praktični vidiki pri uvajanju
- Podpora operacijam: nekatere naprave ne podpirajo vseh operatorjev; potrebni so fallbacki ali preoblikovanje modela.
- Omejitve pomnilnika: modeli se lahko delijo/ploščijo (tiling/chunking), da se prilegajo on-chip pomnilniku.
- Razhroščevanje in profiliranje: vendor orodja so ključna za odkrivanje ozkih grl.
- Kompromisi pri natančnosti: vedno testiraj natančnost po kvantizaciji in optimizacijah.
- Cilj: Zavedati se običajnih težav pri prenosu modelov na NPU.

11) Praktična pot (priporočeni mini projekti)
- Projekt A (začetni): Zaženi vnaprej naučen majhen slikovni klasifikator na CPU/GPU in ga izvozi v ONNX.
- Projekt B (vmesni): Uporabi post-training kvantizacijo v INT8 in oceni spremembo natančnosti in velikosti.
- Projekt C (cilj NPU): Kompiliraj kvantiziran model z vendor orodjem ali TVM za emulator ali napravo; izmeri latenco in porabo.
- Koraki za Projekt B (primer):
  1. Izberi model (npr. MobileNetV2).
  2. Izvozi v ONNX / TFLite.
  3. Izvedi PTQ (TFLite converter ali ONNX Runtime orodje).
  4. Ovrednoti natančnost na validacijskem sklopu.
- Cilj: Dokončati vsaj Projekt A ali B za pridobitev praktičnih izkušenj.

12) Dodatna literatura in viri
- Dokumentacija TensorFlow Lite (kvantizacija, Edge TPU vodiči)  
- ONNX in ONNX Runtime dokumentacija  
- Apache TVM vodiči (kompilacija za pospeševalnike)  
- Google TPU arhitekturni članki in pregledi pospeševalnikov DNN  
- Vendor SDK dokumentacija (Apple ANE, Qualcomm, Huawei)  
(Povezave lahko dodamo v ločeno references/ mapo.)

13) Slovarček (kratko)
- MAC: Multiply-Accumulate  
- GEMM: General Matrix-Matrix multiplication  
- QAT: Quantization-Aware Training  
- PTQ: Post-Training Quantization  
- TOPS: Tera Operations Per Second  
- SRAM: Static RAM (on-chip)  
- DMA: Direct Memory Access

Naslednji korak
- Povej, katero poglavje (številka 1–13) želiš, da razširim naslednje z bolj podrobnimi zapiski, diagrami in praktično vajo. Lahko tudi pripravim PowerPoint diapozitiv za izbrano poglavje.
```
