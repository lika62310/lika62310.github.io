---
title: "Forsøg med web scraping"
date: 2025-10-10
tags: [data-science]
---

Mål: indsamling af data fra websider vha. biblioteker som BeautifulSoup og selenium
Ressourcer: https://pypi.org/project/beautifulsoup4/, https://pypi.org/project/selenium/, https://www.robotstxt.org/

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
Med requests- BeautifulSoup-bibliotekerne kan en sides html-indhold hentes og filtreres, som ses gjort her (hvor User-Agent i headeret hjælper til, at komme forbi fejlbeskeder):

<img width="751" height="468" alt="image" src="https://github.com/user-attachments/assets/ec96e9bb-5879-4d44-a153-279bb158a56e" />

BeautifulSoup kan blandt andet sortere igennem outputtet efter specifikke elementer. Her findes alle h2-overskrifter i artiklen: 

<img width="863" height="145" alt="image" src="https://github.com/user-attachments/assets/0c200d4f-479f-4fea-9d8b-f79e27b34b1e" />


### 3. Dynamisk loaded indhold
Ved dynamisk loaded indhold (f.eks js), kan selenium-biblioteket i stedet tages i brug. 
Her har jeg forsøgt at hente en liste af cd'er fra gucca.dk. Først importeres selenium-biblioteket og webdriver, hvorefter der sættes en instans af webdriver, som venter, til siden er loadet og alle elementer er indlæst. Herefter findes alle produkt-elementer, som det loopes igennem efter titel og pris, som gennem i en liste. Til sidst lukkes driveren, og produktlisten koverteres til en dataframe. Selectors er funder ved brug af inspect-værktøjet på siden, der scrapes (...og en mængde trial & error).

<img width="899" height="687" alt="image" src="https://github.com/user-attachments/assets/d5ae6f54-2ebb-4ce5-bc7f-a4d98bfcebf9" />

Også her kan der med fordel loopes igennem flere sider, for at indhente flere varer. 
I dataframen ses nu, at 'price'-kolonnen både indeholder pris og lagerstatus, hvilket kan rettes ved et splitte kolonnen i to. Det samme er gjort med den oprindelige 'title'-kolonne, som deles i titel, kunstner og type. 

<img width="790" height="192" alt="image" src="https://github.com/user-attachments/assets/8d268dab-0324-43a4-be6b-03515e3312f8" />

### 4. Etik og sikkerhed

De fleste sidder har en robots.txt-fil - en Robots Exclusion Protocol - som specifirerer hvilke dele af der må scrapes, hvilket user-agents, der har adgang, eventuelle crawl-delays mm. Filen er offentlig tilgængelig, hvorfor den ikke bør indeholde følsomme oplysninger. Protokollen fungerer som udgangspunkt efter et princip om frivillig compliance, men det er best practice at følge robots.txt. 

Et eksempel på en robots.txt, der ikke tillader adgang:

  User-agent: *
  Disallow: /

Her står stjernen (*) for alle user agents, mens / dækker alle stier. Alternativt en fil der ikke tillader adgang til specifikke sider eller fra en specifik bot:

  User-agent: *
  Disallow: /auth/
  Disallow: /login/

  User-agent: BadBot
  Disallow: /


