---
title: "Intro til Data Science"
date: 2025-08-25
tags: [data-science]
---

Under emnet Data Science & Analytics, vil jeg undersøge hvordan data kan **indsamles**, **forberedes** og **analyseres** for at udlede relevant information. Arbejdet med data science kan foregår i en cyklus bestående af:

### 1. Problemformulering
Her defineres, hvad målet og scopet for problemet er - hvad skal dataen bruges til? Denne fase er retningsgivende for hele projektet, idet det er herfra, hvor der bestemmes hvilken data er relevant, og i henhold til hvilken resultater valideres. 

### 2. Indsamling af data
I denne fase indsamles den nødvendige data der skal bruges til at kunne arbejdes med opgaven. Dette kan ske f.eks. gennem spørgeskemaer, målinger eller vha. web-scraping. Den indsamlede data kan være kategorisk (kvalitativ data, bestående at en begrænset mængde værdier, f.eks. 'afventer, i gang, gennemført'; kan være nominal (ikke-rangeret, værdier ikke direkte relateret) eller ordinal (rangeret - som en vurdering eller karakter)) eller ikke-kategorisk/numerisk (kvantitativ data, *ikke* bestående af afgrænsede værdier, f.eks. aldre eller datoer). Kategorisk data analyseres som oftest ved deskriptiv statistik, f.eks. ved søjle- eller cirkeldiagrammer, mens numerisk data kan analyseres ift. ting som gennemsnit, maksima/minima og standardafvigelser med f.eks. histogrammmer og boksplot.

### 3. Forberedelse af data
Efter indsamling af data, tilpasses det og 'ryddes op', så det er klar til brug af analyse. Dette består blandt andet i, at fjerne irrelevant data, arbejde med anomalier og null-værdier og evt. konverteringer. Processen kan opdeles i **dataintegration** (samling af data fra flere kilder til ét datasæt), **dataresning** (retning af fejl, f.eks. at fjerne dubletter, håndtere evt. manglende data og null-værdier, retning af formatering), **datatransformation** (transformation af daten til et brugbart format ift. analysen, herunder konvertering, skalering og normalisering), **datareduktion** (udvælgelse af de dele af datasættet, der er relevant for analysen, ved datasæt med mange kolonner eller egenskaber), **diskretisering af data** (grupering af data i kategorier eller intervaller til brug i analysen), og **datasampling** (ved store datasæt, at udvælge en mindre del til analyse, med samme karakteristikker som hele datasættet)

### 4. Dataanalyse
Under dataanalysen bruges den nu forberedte data til at udlede indsigter efter problemet ved brug af statistiske eller matematiske metoder. I analysen findes mønstre, tendenser og sammenhænge i dataen. 

### 5. Datarapportering
Når dataen er analyseret og resultaterne er fundet, skal de kommunikeres til evt. interessenter, f.eks. PO og domæneeksperter. Dette kan f.eks. gøres grafisk, ved hjælp af datavisualiseringsværktøjer, med det formål at vise mønstre og tendenser. 
