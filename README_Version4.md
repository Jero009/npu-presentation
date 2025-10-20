```markdown
# npu-presentation

Ta repozitorij vsebuje zapiske, diapozitive in demo materiale za krajšo predstavitev o Neural Processing Units (NPU).

Struktura repozitorija
- slides/             — izvorni diapozitivi (PowerPoint outline in generirana .pptx)
- docs/               — podrobnejši zapiski in govorne opombe
- assets/             — diagrami in slike
- notebooks/          — Jupyter zvezki za poskuse in demo primere
- .github/workflows/  — CI (opcijsko) za izdelavo diapozitivov ali izvoza v PDF

Kako uporabljati
1. Odpri ta repozitorij v brskalniškem urejevalniku (že si tukaj).
2. Uredi diapozitive v slides/ (imamo PowerPoint outline in lahko ustvarimo .pptx).
3. Ustvari vejo za spremembe:
   git checkout -b feature/slide-intro
4. Uporabi spletni urejevalnik ali lokalno git za commit in push:
   git add .
   git commit -m "Add initial slides and notes"
   git push origin feature/slide-intro
5. Odpri Pull Request na GitHubu, recenziraj in združi v main.

Pomoč
Če želiš, mi reci "generate .pptx" in pripravim PowerPoint datoteko, ki jo lahko preneseš in naložiš v slides/intro.pptx.
```