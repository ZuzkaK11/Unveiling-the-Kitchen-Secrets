# Odhaľovanie tajomstiev kuchyne

**Autorky:** Kristína Galková, Jana Poľašková, Simona Bednariková, Zuzana Kovačová
---

## Úvod

Tento projekt vychádza z dát publikovaných v štúdii ["The Cultural Diversity of Culinary Practice"](https://www.nature.com/articles/srep00196?fbclid=IwZXh0bgNhZW0CMTEAAR5jxK20YaAdsan5F_9OSoRbOx9zHBb7HGKPuMQivwVUcAL6LV9nQuv-Ky7a2g_aem_7pUl6MBiKtyHXnqcm4o6nQ) (Yong-Yeol Ahn et al., 2011), ktorá skúma vzorce kombinácií ingrediencií naprieč rôznymi regiónmi. Štúdia zavádza koncept „flavor network“ (chuťová sieť), ktorá zachytáva zdieľané chuťové zlúčeniny medzi ingredienciami.

---

## Dáta

Dataset obsahuje zoznam receptov vo formáte CSV. Prvý stĺpec predstavuje regióny, ostatné stĺpce ingrediencie. Dáta sme spracovali v **Python** a vizualizovali pomocou knižnice **NetworkX**.

Vzťahy medzi regiónmi a ingredienciami sú reprezentované ako **bipartitný graf**:  
- Jedna partícia: regióny  
- Druhá partícia: ingrediencie  
- Hrana spája ingredienciu s regiónom, ak sa v recepte v danom regióne vyskytuje.  
- Váha hrany = počet receptov s danou ingredienciou.

### Základné štatistiky grafu

| Parameter                                    | Hodnota  |
|---------------------------------------------|----------|
| Celkový počet uzlov                          | 392      |
| Celkový počet hrán                           | 2641     |
| Počet regiónov (partícia 0)                 | 11       |
| Počet ingrediencií (partícia 1)             | 381      |
| Hustota siete                                | 0.6302   |
| Priemerný stupeň (Regióny - partícia 0)     | 240.09   |
| Priemerný stupeň (Ingrediencie - partícia 1)| 6.93     |

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

---

## Hlavné otázky

### 1. Prečo Severná Amerika využíva väčšie množstvo ingrediencií a receptov?

- **Kultúrna diverzita:** prisťahovalci z rôznych častí sveta priniesli vlastné recepty a ingrediencie.
- **Potravinové regulácie:** USA majú liberálnejší prístup k povoleniu ingrediencií (GRAS), zatiaľ čo EU uplatňuje princíp predbežnej opatrnosti.
- **Dataset:** väčší počet dostupných severoamerických receptov môže zvýšiť zaznamenaný počet ingrediencií.

**Vizualizácie:**  
- Porovnanie počtu receptov a unikátnych ingrediencií (bar plot)  
- Bubble plot regiónov podľa počtu receptov a ingrediencií

### 2. Rozdiely v počte ingrediencií na recept medzi regiónmi

- Normalizovaná distribúcia počtu ingrediencií ukazuje, že regióny ako Juhovýchodná Ázia a Afrika používajú viac ingrediencií.  
- Severná a Západná Európa majú tendenciu používať menej ingrediencií.

### 3. Podobnosť a jedinečnosť kuchýň

- **Jaccardova vzdialenosť** meria podobnosť regionálnych ingrediencií (0 = úplne rovnaké, 1 = úplne odlišné).  
- Hierarchické zhlukovanie odhalilo tri prirodzené skupiny kuchýň:  
  1. Východná + Severná Európa  
  2. Afrika, Juh Ázia, Blízky východ  
  3. Latinská Amerika + Severná Amerika, Južná + Západná Európa  

- **Unikátne ingrediencie:** Durian, galanga, holy basil pre Juhovýchodnú Áziu; brusnice, sleď, sladké drievko pre Severnú Európu.

### 4. Vzťahy top 5 ingrediencií z každého regiónu

- Projekcia bipartitného grafu zobrazuje kombinácie ingrediencií podľa regiónov.  
- **Uzly:** ingrediencie, veľkosť = váha hrán  
- **Hrany:** spoločný výskyt ingrediencií medzi top 5 v rôznych regiónoch  
- **Farby uzlov:**  
  - Zelená: excentricita (centrálne ingrediencie)  
  - Fialová: centralita blízkosti (často kombinované ingrediencie, napr. cesnak)  
  - Červené okraje: lokálny zhlukový koeficient  

---

## Záver

- Severná Amerika vyniká diverzitou receptov a ingrediencií, čo odráža prisťahovalecké vplyvy a liberálnejší prístup k prísadám.  
- Južná Európa a Juhovýchodná Ázia majú charakteristické lokálne suroviny a tradičné receptúry.  
- Regióny ako Afrika a Ázia používajú najviac ingrediencií na recept.  
- **Cesnak** sa ukázal ako najčastejšie kombinovaná ingrediencia – slúži ako most medzi kuchyňami.  
- Ingrediencie ako cesnak, cibuľa, olivový olej a ryža prepájajú väčšinu svetových kuchýň.

---

*Poznámka:* Všetky vizualizácie sú vytvorené v Pythone pomocou NetworkX a sú zahrnuté v repozitári.
