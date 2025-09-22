# Unveiling the Kitchen Secrets

---

Semestrálny projekt z princípov dátovej vedy v 3. ročníku. Skupina: Galková, Polašková, Bednáriková, Kováčová

---

## Úvod

Tento projekt vychádza z dát publikovaných v štúdii "The Cultural Diversity of Culinary Practice" [Yong-Yeol Ahn et al., 2011](https://www.nature.com/articles/srep00196?fbclid=IwZXh0bgNhZW0CMTEAAR5jxK20YaAdsan5F_9OSoRbOx9zHBb7HGKPuMQivwVUcAL6LV9nQuv-Ky7a2g_aem_7pUl6MBiKtyHXnqcm4o6nQ), ktorá skúma vzorce v kombináciách ingrediencií naprieč rôznymi regionálnymi kuchyňami. Štúdia zavádza koncept tzv. „flavor network“ (chuťová sieť), ktorá zachytáva zdieľané chuťové zlúčeniny medzi ingredienciami. Tento prístup poskytuje nový pohľad na kulinárske praktiky a ich rôznorodosť. Z tejto štúdie sme si práve vybrali dataset, ktorý poskytuje vzťahy medzi ingredienciami a jednotlivými regiónmi.

---

## Dáta

Dataset nám umožňuje odhaliť, ktoré ingrediencie sú globálne zdieľané, ktoré sú typické len pre určité oblasti a ako sú regióny kulinárne prepojené. Teda prepájame kultúru so sieťovou analýzou.

Dáta obsahujú zoznam receptov vo formáte CSV. Prvý stĺpec predstavuje názvy regiónov, zatiaľ čo nasledujúce stĺpce obsahujú ingrediencie používané v konkrétnych receptoch. S dátami sme pracovali v programovacom programe `Python` a graf vytvorili pomocou knižnice `NetworkX`.

Keďže vzťahy sú definované výlučne medzi regiónmi a ingredienciami, dáta môžu byť reprezentované ako bipartitný graf. Jednu partíciu tvoria regióny a druhú partíciu ingrediencie. Ak sa daná ingrediencia vyskytuje v recepte z určitého regiónu, je spojená s týmto regiónom hranou. Váha hrany vyjadruje počet receptov, v ktorých je ingrediencia použitá.

### Základné štatistiky

| Parameter                                    | Hodnota  |
|---------------------------------------------|----------|
| Celkový počet uzlov                          | 392      |
| Celkový počet hrán                           | 2641     |
| Počet regiónov (počet uzlov v partícii 0)   | 11       |
| Počet ingrediencií (počet uzlov v partícii 1)| 381     |
| Hustota siete                                | 0.6302   |
| Priemerný stupeň (Regióny - partícia 0)     | 240.09   |
| Priemerný stupeň (Ingrediencie - partícia 1)| 6.93     |

Bipartitný graf zobrazuje vzťahy medzi regiónmi a ingredienciami na základe prítomnosti jednotlivých ingrediencií v receptoch. Na ľavej strane grafu sú zobrazené regióny, ktoré sú odlíšené rôznymi farbami (spolu 11 regiónov). Na pravej strane grafu sa nachádzajú ingrediencie (spolu 381), ktoré sú zoradené do štyroch stĺpcov kvôli lepšej prehľadnosti.

### Štatistiky podľa regiónov

| Región              | Unikátne ingrediencie | Celkové ingrediencie | Počet receptov |
|--------------------|---------------------|-------------------|----------------|
| African            | 197                 | 3674              | 351            |
| EastAsian          | 242                 | 22498             | 2512           |
| EasternEuropean    | 198                 | 3196              | 381            |
| LatinAmerican      | 260                 | 27360             | 2917           |
| MiddleEastern      | 227                 | 5411              | 645            |
| NorthAmerican      | 354                 | 330618            | 41524          |
| NorthernEuropean   | 175                 | 1706              | 250            |
| SouthAsian         | 205                 | 6388              | 621            |
| SoutheastAsian     | 184                 | 5172              | 457            |
| SouthernEuropean   | 290                 | 37038             | 4180           |
| WesternEuropean    | 309                 | 21341             | 2659           |

![Bipartitný graf zobrazujúci regióny (naľavo) a ingrendiencie (vpravo). Hrana vyjadruje prítomnosť ingrediencie aspoň v jednom recepte v danom regióne.](images/graf_ukazka.png)

---

## Hlavné otázky

### Otázka č. 1: Aké sú dôvody, prečo Severná Amerika využíva väčšie množstvo ingrediencií a receptov v porovnaní s inými regiónmi?

Pri pohľade na bipartitný graf a základné štatistiky regiónov a ingrediencií je zrejmé, že Severná Amerika vyniká medzi svetovými regiónmi nielen počtom receptov, ale aj rozmanitosťou ingrediencií. Za hlavné faktory tejto rozmanitosti považujeme:

- Prvým dôvodom je kultúrna diverzita ako výsledok prisťahovalectva. Severná Amerika – predovšetkým USA a Kanada – je rajom prisťahovalcov z celého sveta. Každá komunita si priniesla svoje tradičné recepty, suroviny a chuťové preferencie. Výsledkom je gastronomická fúzia, kde vedľa seba existujú ingrediencie z Ázie, Európy, Latinskej Ameriky aj Afriky. Táto jedinečná zmes kultúr sa prirodzene odráža v počte a rôznorodosti ingrediencií, ktoré sa v regióne bežne používajú.
- Druhým dôvodom môžu byť ich menej prísne potravinové regulácie. V USA platí princíp, že látka môže byť používaná, pokiaľ neexistuje dôkaz o jej škodlivosti (tzv. GRAS – generally recognized as safe). Naopak, Európska únia uplatňuje princíp predbežnej opatrnosti, kde sa látka musí preukázateľne považovať za bezpečnú, aby mohla byť schválená. Tento rozdiel sa netýka samotných ingrediencií, ale chemických látok, ktoré sa v nich môžu nachádzať – napríklad konzervanty, farbivá či sladidlá. Tak sa môže stať, že určitá ingrediencia (napr. konkrétny druh sladidla alebo dochucovadla) je v Európe obmedzená alebo zakázaná práve kvôli zložkám, ktoré obsahuje, zatiaľ čo v USA je bežne povolená. To môže viesť k väčšiemu počtu rôznych ingrediencií evidovaných v amerických receptoch. [Time, 2024](https://time.com/7210717/food-additives-us-fda-banned-europe/), [CBS News, 2023](https://www.cbsnews.com/)
- Tretím možným faktorom je samotný dataset. Je možné, že dataset obsahuje výrazne viac severoamerických receptov v porovnaní s ostatnými regiónmi, čo prirodzene zvyšuje aj zaznamenaný počet tamojších ingrediencií. Tento dátový nepomer môže byť spôsobený vyššou digitalizáciou, popularitou amerických receptov online či angličtinou ako dominantným jazykom v dostupných zdrojoch.

![Porovnanie počtu receptov a unikátnych ingrediencií pre jednotlivé regióny](images/bar_plot.png)

![Regióny na základe počtu receptov a unikátnych ingrediencií a celkového počtu ingrediencií](images/bubble.png)

---

### Otázka č. 2: Aké sú rozdiely v receptoch medzi regiónmi, najmä v počte ingrediencií na recept?

Graf zobrazuje normalizovanú distribúciu počtu ingrediencií na recept v rôznych regiónoch. Na osi x pozorujeme počet ingrediencií na recept, zatiaľ čo os y zobrazuje frekvenciu výskytu daného počtu ingrediencií v danom regióne. Každá krivka zodpovedá inému regiónu a je zafarbená podľa priemeru počtu ingrediencií v danom regióne.  

![Normalizovaná distribúcia počtu ingrediencií na recept v regiónoch](images/pocet_recept.png)

Pozorujeme, že regióny Juhovýchodná Ázia a Afrika majú tendenciu používať v priemere väčší počet ingrediencií na recept, pričom ich distribúcie sú širšie, s výraznejšími vrcholmi v oblasti vyšších počtov ingrediencií. Naopak, regióny ako Severná Európa a Západná Európa majú tendenciu používať menší počet ingrediencií.  

![Top 5 ingrediencií naprieč regiónmi](images/top5.png)

---

### Otázka č. 3: Ktoré kuchyne si sú navzájom podobné a aké suroviny sú pre jednotlivé kuchyne jedinečné?

Z bipartitného grafu región–ingrediencia sme vytvorili váženú jednomódovú projekciu na uzloch regiónov. Hrana medzi dvoma regiónmi \(r_i,r_j\) má hmotnosť rovnú počtu ingrediencií, ktoré zdieľajú.  

**Jaccardova vzdialenosť** pre množiny ingrediencií \(I_i\) a \(I_j\):

$$
d_J(r_i, r_j) = 1 - \frac{|I_i \cap I_j|}{|I_i \cup I_j|}
$$

- \(d_J = 0\) znamená úplnú zhodu ingrediencií.  
- \(d_J = 1\) znamená úplnú odlišnosť.  

Hierarchické zhlukovanie ukázalo tri prirodzené skupiny kuchýň.

![Hierarchické zhlukovanie regiónov podľa Jaccardovej vzdialenosti ingrediencií](images/dendrogram.png)

![Bipartitný graf regióny vs. ingrediencie (farby podľa dominantného regiónu)](images/1_SV.png)

![Suroviny v jednotlivých regiónoch](images/regiony_vs_ingrediencie_sun.png)

---

### Otázka č. 4: Aké sú vzťahy medzi top 5 najpoužívanejšími ingredienciami z každého regiónu?

Projekcia bipartitného grafu na ingrediencie ukazuje spoločný výskyt top 5 ingrediencií medzi regiónmi.

- Uzly reprezentujú ingrediencie. Veľkosť uzla je úmerná váhe hrán.  
- Hrana medzi dvomi uzlami reprezentuje spoločný výskyt ingrediencií v rovnakých regiónoch. Hrúbka hrany je úmerná počtu regiónov.  

Farebné vlastnosti uzlov:

- **Excentricita (zelená):** Centrálne ingrediencie kombinované s inými, napr. cibuľa, pšenica, vajce, paradajky, olivový olej, kurkuma.  
- **Centralita blízkosti (fialová):** Najvyššia centralita má cesnak, čo naznačuje jeho časté spojenie s inými ingredienciami.  
- **Lokálny zhlukový koeficient (červené okraje):** Napr. vegetable oil, rice, fish, typické pre konkrétne regióny.  

![Projekcia bipartitného grafu na ingrediencie](images/graf_centrality.png)

![Prehľad štatistických metrík pre jednotlivé vrcholy](images/graf_prehlad.png)

---


## Záver

- Severná Amerika vyniká diverzitou receptov a ingrediencií, čo odráža prisťahovalecké vplyvy a liberálnejší prístup k prísadám.  
- Južná Európa a Juhovýchodná Ázia majú charakteristické lokálne suroviny a tradičné receptúry.  
- Regióny ako Afrika a Ázia používajú najviac ingrediencií na recept.  
- **Cesnak** sa ukázal ako najčastejšie kombinovaná ingrediencia – slúži ako most medzi kuchyňami.  
- Ingrediencie ako cesnak, cibuľa, olivový olej a ryža prepájajú väčšinu svetových kuchýň.

---

*Poznámka:* Všetky vizualizácie sú vytvorené v Pythone pomocou NetworkX a sú zahrnuté v repozitári.
