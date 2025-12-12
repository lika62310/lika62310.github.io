---
title: "Analyse af fitness- og vejrdata"
date: 2025-09-11
tags: [data-science]
---
Mål: visualisering af sammenhænge vha. matplotlib; sammenligning af data fra flere datasæt. 
Ved hjælp af motionsdata (skridt) og vejrdata fra DMI ønskes undersøgt, om der findes en sammenhæng mellem vejret på en given dag og antal skridt gået.

Ressourcer: https://pandas.pydata.org/pandas-docs/stable/index.html, https://matplotlib.org, stack overflow, https://www.dmi.dk/friedata/observationer

## 1. Import af data + indledende oprydning

Som det første importeres alle nødvendige biblioteker, og datasættene indlæses. Fitness-dataen er hentet fra Sunhed-appen på iOS. 
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/4b6e1ded-b12a-463c-9ad2-d6944e608ec6" />
Før at dataen kan bruges til at udforske problemstillingen, er vi nødt til at rydde op i dataframen - her ligger vi ud med at fjerne alle umiddelbart irrelevante kolonner, får herved et bedre overblik over datasættet:
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/3c395828-9212-49b3-8ba5-d2150af3e4d2" />
Allerede er vi tættere på, men da vi er ude efter værdier for skridt, må dataframen filtreres ned til udelukkende at indeholde rækker, hvor værdien 'type' er 'HKQuantityTypeIdentifierStepCount' - lignende kunne gøres med bl.a. HKQuantityTypeIdentifierDistanceWalkingRunning eller HKQuantityTypeIdentifierFlightsClimbed for at få afstanden eller hastigheden.
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/a0be6d27-e880-42d0-8765-b7fd8d640dd9" />
Med dataframen nu i en brugbar udformning, kan vi med fordel også fjerne kolonnerne type og unit, som ikke længere tilbyder yderligere information, samt to af datoværdierne, her startDate og endDate. 

Endelig ønsker vi at få vist antal skridt **per dag**, hvilket vi kan gøre ved at gruppere at gruppere værdierne i creationDate-kolonnen efter dato (...efter en konvertering til datetime):

<img width="90%" alt="image" src="https://github.com/user-attachments/assets/9943cd4d-274e-4f52-af48-8cde1bfa8129" />


### 1.2 import af temperaturdata

Al vejrdata er hentet fra DMI som CSV-filer - én for hver måned (fra vejrstation Abed, som er tættest på hvor hovedparten af skridtene er gået :)). Da vi ønsker al dataen samlet, konkatenerer vi filerne til én dataframe som de indlæses. Herudover fjernes de to tomme kolonner, og DateTime-kolonnen konverteres. 
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/e03ac7e1-e585-4cf6-8b79-7ea67b0c1e79" />

Som det ses, indeholder datasætten temperaturobservationer per timebasis; vi har til analysen brug for dem på dagsbasis. Her kunne man gruppere dataene efter data, som vi har gjort med skridt-dataen, og taget en gennemsnit per dag (evt. kun på dagtimer). I stedet har jeg valgt at tage alle målinger fra kl. 12, da jeg ved at det er ved dette tidspunkt der primært er blevet gået, og derfor de vejrforhold der er interessante for analysen. Dette gøres her:
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/b9dcf499-93c2-414b-b349-8edb1e81445b" />


## 2. Begyndende visualisering - oversigt over skridt over tid

Før vi begynder at sammenligne de to datasæt, kunne det være interessant at se lidt på skidt-datane alene. Til at starte med, kan vi se, om der en udvikling i daglige skridt over et år ved hjælp at et linjediagram.
<img width="625" height="59" alt="image" src="https://github.com/user-attachments/assets/c551044d-dafa-487d-ae39-935fdd035a02" />
<img width="996" height="572" alt="image" src="https://github.com/user-attachments/assets/b268f0f2-7a34-4ae6-a7bc-6dead9a3934c" />
Diagrammet viser store udslag i antal skridt, men foreslår dog - som forventet - en tendens mod kortere ture i de kolde måneder, og længere hen ad foråret og sommeren. 
For at undersøge dette videre, kan vi se på det samtlige skridtantal på månedsbasis:
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/72928bc8-f7bb-4a8f-a9e8-180f3d852733" />
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/4c6e65d8-4b3b-4137-b3e7-fd2f9558f576" />
Det skarpe fald vi ser efter august, skyldes at kun første uge af september er medtaget (da analysen er foretaget i start september), samt et par dage fra december 2024, hvor optællingen er opstartet. Fjerner vi disse, og medtager kunne hele måneder ser linjediagrammet således ud:

<img width="90%" alt="image" src="https://github.com/user-attachments/assets/57d67f6c-308a-4d68-a1ef-ba7fc0e39c43" />
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/3db96f54-0ec9-4ea1-b42f-5299571ee68a" />
og bekræfter altså en stigning i løbet at året. 

Foruden udviklingen, kan en fordeling af skridt per måned visualiseres ses ved hjælp af et søjlediagram:
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/7316941e-f0e1-4b8c-8af8-83441bb7186c" />


## 3. Kombineret visualisering - er der en sammenhæng mellem vejrforhold og antal skridt gået?

Fordelingen af skridt pr. måned vist i 2. foreslår en klar sammenhæng imellem antal skridt gået og temperatur, i det det umiddelbart er i forårs- og sommermånederne, der er gået mest. Dette kan vi undersøge videre vha. det indlæste vejrdata, og se om der er en faktisk sammenhæng.
Da vi ønsker at se sammenhængen mellem to forskellige datapunkter, er et scatterplot det åbenlyse værktøj. 

For nemt at kunne sammenligne de to datasæt, samler vi dem til én dataframe med et join på datakolonnen (efter en tilretning af DateTime-kolonnen til samme dataformat ved at fjerne klokkeslættet, samt en omdøbning af creationdate til DateTime) 
<img width="735" height="329" alt="image" src="https://github.com/user-attachments/assets/b9fe9b30-c818-444a-9fe7-5e45d816dac0" />

Herfra kan vi nemt oprette et scatter plot:
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/e6deb14a-19de-470c-b277-fbf48a5da46a" />
Diagrammet ser ud til vise en svag positiv sammenhæng mellem antal skridt gået og temperaturen, som forventet. For at gøre dette klarere, vil vi gerne indsætte en regressionslinje:

<img width="90%" alt="image" src="https://github.com/user-attachments/assets/70e6f31c-0d10-4b09-a778-a6ec4582a0e7" />
... og vi får en fejl. Da en mulig grund til dette kunne være, at datasættet indeholder NaN-værdier et sted, er dette værd at undersøge. 

<img width="90%" alt="image" src="https://github.com/user-attachments/assets/3a4233bf-1be8-4b03-841e-6aa847d31209" />
Her viser et check på isnull, at der *er* NaN-værdier i en af kolonnerne, og en filtrering af disse værdier viser, at vi har tre dage uden en temperatur-værdi. Dette kunne løses på flere måder, bl.a. ved at sætte NaN-værdier til 0, eller erstattet dem med en forventet gennemsnitsværdi. I stedet vælger vi at fjerne dem, da de er jævnt fordellet over sættet, og vi har nok værdier til, at det ikke påvirker resultatet. 

Med datasættet renset for NaN-værdiet, forsøger vi igen at lave en regressionslinje...
<img width="789" height="692" alt="image" src="https://github.com/user-attachments/assets/91b2d75d-c7e7-4883-a1cc-483d845fedc1" />
...og det virker! Nu kan vi klart se, at der *er* en sammenhæng mellem højere temperaturer og flere skridt. 

## 4. Yderligere vejrforhold & visualisering

DMIs frie data indeholder ikke kun temperaturobservationer, men derimod en lang vifte af parametre, som der ligeledes kunne være interessante at kigge på. Herfra er der valgt vind og nedbør.

Processen fra 1.2 gentages for begge af disse til indlæsning og oprydning af datasættene, hvorefter de for lethedens skyld samles (samtidig med at kolonnen 'value' omdøbes til det mere sigende 'Skridt'; herudover foretages null-tjek og oprydning, ikke vist):
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/aa5515e1-6502-4b0e-a8f0-8a66bd538f10" />

og der oprettet scatterplots for at illustrere sammenhængen:

<img width="90%" alt="image" src="https://github.com/user-attachments/assets/887acbee-c0ef-418a-bdd7-c615f76762d4" />
<img width="740" height="659" alt="image" src="https://github.com/user-attachments/assets/1b527da6-3039-459e-a29b-056d95ecd71c" />

Diagrammet for vindhastighed ser ud til at vise en svag negativ sammenhæng (færre skridt gået ved højere vindhastigheder), mens nedbørsdiagrammet primært viser, at hovedparten af datapunkterne ligger på 0 mm. Vælger vi at fjerne disse, ser diagrammet således ud (inkl. regressionslinje):
<img width="686" height="520" alt="image" src="https://github.com/user-attachments/assets/ebda5acb-ea25-4a0b-b730-69a25b901e5f" />
som virker til også at vise en negativ sammenhæng, som dog kan skyldes en større afvigelse - fjerner vi afvigelsen (punktet ved ~16 mm), får vi dette diagram
<img width="683" height="539" alt="image" src="https://github.com/user-attachments/assets/19696483-4b3a-4049-995d-795caa2ecc1f" />
som *ikke* foreslår en sammenhæng mellem nedbør og antal skridt gået. Dette kan skyldes at der ikke er nogen sammenhæng, eller at datasættet er for lille til at vise den (i det det ikke har regnet de fleste af dagenene, og primært kun i små mængder). 

Ift. vindhastigheden, viser indsættelsen af en regressionslinje en lille negativ sammenhæng, dog mindre end sammenhængen mellem temperatur og skridt.
<img width="90%" alt="image" src="https://github.com/user-attachments/assets/20989d31-c039-4583-8efb-8edb0b97e3f3" />

---

Udbytte: Formålet med forsøget var at kunne visualisere sammenhænge og arbejde med flere datasæt; dette er opnået, samtidig med at en større kompetence indenfor dataforberedelse og -oprydning er opnået. Herudover større fortrolighed ned python-fejlmeddelelser samt vellykket søning efter både fejlløsning og nye funktioner. 
