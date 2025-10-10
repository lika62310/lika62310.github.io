---
title: "Forsøg med web scraping"
date: 2025-10-10
tags: [data-science]
---

Mål: indsamling af data fra websider vha. biblioteker som BeautifulSoup og selenium

Web scraping er en hurtig og effektiv måde at indsamle store mængder data. I python understøttes dette af flere biblioteker ...

### 1. Tabeller
read_html()-funktionen i pandas-biblioteket finder samtlige tabeller på en given liste, og gemmer dem som en list af dataframes. 
Dette har jeg brugt, til at forsøge at hente lister af mest givne pigenavne på årsbasis fra https://www.behindthename.com/top/lists/denmark/2024. Kaldet returnerer en liste dataframe, hvoraf listen med pigenavne er den tredje. 
<img width="844" height="347" alt="image" src="https://github.com/user-attachments/assets/a1befb9c-0320-4254-a3fd-44c55b9dd3bf" />
Herefter har jeg itereret i gennem flere sider (år), for at samle det til én dataframe:

<img width="803" height="374" alt="image" src="https://github.com/user-attachments/assets/b6b15871-5a90-40ba-8cc3-09a075f4078d" />
<img width="793" height="311" alt="image" src="https://github.com/user-attachments/assets/3cf1aadc-e7de-47e0-9a8a-ca917115d9f9" />
...og ryddet lidt op i dataframen (omdøbt kolonner og fjernet unødvendige rækker):

<img width="521" height="242" alt="image" src="https://github.com/user-attachments/assets/34d9a401-ced8-4714-8ff2-6db01e24c677" />
Herfra er datasættet klar til brug til f.eks. analyse af navnetrends over tid el.lign.

### 2. Statisk indhold

### 3. Dynamisk loaded indhold
Ved dynamisk loaded indhold (f.eks js), kan selenium-biblioteket i stedet tages i brug. 
Her har jeg forsøgt at hente en liste af cd'er fra gucca.dk. Først importeres selenium-biblioteket og webdriver, hvorefter der sættes en instans af webdriver, som venter, til siden er loadet og alle elementer er indlæst. Herefter findes alle produkt-elementer, som det loopes igennem efter titel og pris, som gennem i en liste. Til sidst lukkes driveren, og produktlisten koverteres til en dataframe. 
<img width="899" height="687" alt="image" src="https://github.com/user-attachments/assets/d5ae6f54-2ebb-4ce5-bc7f-a4d98bfcebf9" />



