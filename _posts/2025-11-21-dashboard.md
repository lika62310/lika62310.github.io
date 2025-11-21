---
title: "Projekt - dashboard & travlhed"
date: 2025-11-21
tags: [projekt, data-science]
---
En oversigt over booking- og analytics-elementer i LazyCatz-projektet.

### Travlhed ved booking
Når en kunde opretter en ny booking, indikeres efter valgt dato og tid om der forventes at være travlt på dette tidspunkt, hvilket kunden kan bruge til at vælge det rette tidspunkt. Travlheden sættes (ved kald til /Booking/BusyInfo-endpointet), når både dato og tidspunkt er valgt, og opdateres dynamisk hvis en ny værdi vælges.

<img width="739" height="532" alt="image" src="https://github.com/user-attachments/assets/785638e6-a2c4-461c-8397-4fe6bc1c28a9" />

<img width="623" height="344" alt="image" src="https://github.com/user-attachments/assets/1e7b6ff6-ee53-4bc2-83f4-9384e3d76a3b" />

Travlheden udregnes baseret på historik data efter ugedag og tidspunkt på dagen (f.eks. fredage kl. 12), men ville ved en større mængde data også kunne tilpasse til at medregne årstid eller helligdag som evt. faktor, samt evt. tilstande specifikke for caféen som arrangementer el. lign. 
Grundet den typiske daglige bookingmængde i datasættet er tærsklen for travlhed her sat til 4, men kunne med fordel i stedet sættes til en bestemt procent af caféens reelle kapacitet (efter samtale med PO).
<img width="699" height="283" alt="image" src="https://github.com/user-attachments/assets/ac718ad4-8a1a-4ccf-8439-74d560010ba3" />

### Dashboard
På sidens analyse-dashboard, findes en række diagrammer over tendenser relateret til caféen.

#### Oversigt over udviklingen af bookinger over tid
<img width="830" height="515" alt="image" src="https://github.com/user-attachments/assets/ffa7415a-01bf-41fd-8359-e2a6d4d39414" />

Det første diagram, er et kurvediagram, som viser tendensen i bookinger over tid, vist som den som antal gæster i alt pr uge. Her kan ses, hvor vidt det går fremad eller tilbage for caféen ift. mængden af besøgende, og der kan vurderes om der er behov for evt. initiativer for at øge mængden af bookinger.

<img width="483" height="264" alt="image" src="https://github.com/user-attachments/assets/9e601132-0cea-4945-b7e5-77ac3c9f2ff5" />
<img width="613" height="167" alt="image" src="https://github.com/user-attachments/assets/f7b3e57e-27eb-40a3-9c89-41f2fa981acf" />

For at oprette diagrammet er listen af bookinger gruperet på uge-basis (for at gøre diagrammet mere overskueligt), hvorefter det samtlede antal gæster (pr. booking) optælles, og listen sorteres efter dato, for at kunne vise udviklingen over tid. 

#### Bookinger fordelt på ugedag
<img width="889" height="547" alt="image" src="https://github.com/user-attachments/assets/3b66e241-cfbe-4751-9f32-aa69fe1cc0e9" />

Herefter ses et søjlediragram, som viser fordelingen af antal bookinger fordelt over ugens dage, som kan give indsigt i, hvornår der kan forventes at være specielt travlt, især ift. vagtplanlægning. Herudover kan der ses, om eventuelle arrangementer (infoaftener, fredags-quiz, osv.) bidrager til at trække flere ind på de dage.
Dataen er her grupperet efter ugedag, hvorefter den gennemsnitlige mængde gæster per. dag er udregnet og listen grupperet efter ugedag man-søn. 

#### Bookinger fordelt på tidspunkt
<img width="80%" alt="image" src="https://github.com/user-attachments/assets/68cbe197-c67d-4bdb-acfb-518a107429f1" />

På doughtnut-diagrammet ses fordelingen af bookinger over tidspunkt på dagen, hvilket kan give indsigt i spidsbelastningen og bruges både til planlægning og til at få indsigt i caféen målgruppe - kommer folk primært om morgenen eller om eftermiddagen? Hvor meget skal der fokuseres på sene arrangementer?
For at gøre visningen mere overskuelig, vises tispunkterne i tre-timers intervaller (morgen, middag, osv.), og fokuserer derfor på de bredere trends fremfor timevisning. Her kan for eksempel ses, at den største gruppe af kunder kommer om formiddagen (efterfulgt af tidlig eftermiddag), mens der ikke er særligt travlt tidligt om morgenen og om aftenen. 

<img width="410" height="264" alt="image" src="https://github.com/user-attachments/assets/37f7c607-bee1-4467-9918-cca05cc7020e" />


#### Gennemsnitlig gruppestørrelse
<img width="45%" alt="image" src="https://github.com/user-attachments/assets/f12e527b-d1da-445b-9a22-fe72aafe57f4" />
<img width="42.8%" alt="image" src="https://github.com/user-attachments/assets/7e296565-6239-40f3-9faa-fbdccaba126d" />

Her kan fordelingen af bookingernes gruppestørrelse ses, enten som et histogram eller som et kurvediagram (ved skift af visningen). Dette giver ligeledes indsigt i caféens målgruppe, og hvilke slags grupper det giver mest mening for caféen at fokusere på og rette deres tilbud imod (også ift. til pladser og borde)- er det store eller små selskaber? Enkeltpersoner? 
Her ses klart, at der kommer flest to- og tremands-grupper, og at derhefter bliver færre jo større gruppen bliver. Derfor vil der give mest mening for caféen at fokusere på de mindre grupper.

<img width="713" height="301" alt="image" src="https://github.com/user-attachments/assets/2d1ff627-a5ec-4ca7-859b-7333b66baafa" />

#### Travlhed/gruppestørrelser fordelt på tidspunkt/dag
<img width="1459" height="891" alt="image" src="https://github.com/user-attachments/assets/261aa7a1-6c10-4714-ad47-1e2ed833ca47" />
<img width="1374" height="706" alt="image" src="https://github.com/user-attachments/assets/de65747f-4c8a-4d70-acbe-dcc871cda006" />

Som det sidste ses et matrix-diagram, som viser den forventede belastning over en gennemsnitlig uge. Her kan der hurtigt ses, hvilke dage og tidspunkt, hvor der er mest travlt - igen her ses der f.eks. en tendes mod travlhed omkring middag og eftermiddag, mens der de fleste dage er mindre travlt om morgenen og om aftenen (f.eks. er torsdag den eneste dag, hvor der er travlt kl. 20, hvilket igen kan bruges til planlægning eller til at bekræfte, at f.eks. quiz-arrangementer virker). 
Skiftes visningen, ses i stedet den gennemsnitlige gruppestørrelse på samme tidspunkter, som f.eks. kan vise om større grupper er mere tilbøjelige til at dukke op på visse tidspunkter.
Her er bookingerne blevet gruperet efter ugedag og tidspunkt, hvor antal bookinger (eller gennemsnitlig grupperstørrelse, alt efter visning) på tidspunktet repræsenteres ved cellens farve.

<img width="748" height="438" alt="image" src="https://github.com/user-attachments/assets/e091b68f-c4c5-4762-8ade-6fe4577ff826" />
<img width="595" height="186" alt="image" src="https://github.com/user-attachments/assets/8b8a77f1-beec-4b9d-944f-5ac1b07bdd8c" />

### Andre mulige visualiseringer

Grundet begrænsningerne af det nuværende datasæt, beskæftiger disse visualiseringer sig primært med booking af travlhed, men med et udviget datasæt der bl.a. også analyseres:
- Fastholdelse (og effektiviteten af loyalitetsprogram) - hvad er mængden af faste kontra nye kunder? Hvordan bidrager loyalitetsprogrammet til at fastholde kunder? (før/efter sammenligning, sammenhæng mellem fastholdelse og point optjent ved køb/spil, ...)
- Sammenhæng mellem gruppestørreler og bestillingsstørrelse - hvilke gruppestørrelse giver størst indtening pr. person? Hvilket segment skal der fokuseres på?
- Udnyttelse af kapacitet - hvor tit er der fyldt?
- Menuudvikling - hvad på menuen bestilles mest? Hvornår? Salg af sæsonvarer, virkning af tilbud, success af nye varer osv.
- Katte - hvilke katte er mest populære?
- Web analytics - hvilken adfærd udviser brugerne på siden? Bidrager siden til at fastholde kunder og erhverve nye?

