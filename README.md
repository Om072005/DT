# DT

Scraped the list of companies by creating my own scraper , only 6 of them could qualify for greater than 65 score in Basket B types companies , currently not included LinkedIn (via SerpAPI) and others which requires specialized APIs.

Basic architecture 

```mermaid
flowchart TB

    A["Start: config.py<br>{CITY} + {SEGMENT}"]

    B["Stage 1 — scrape universe<br>(target: 75–100 companies)<br><br>
    MCA21 registry • IndiaMART / DGFT • LinkedIn / SerpAPI • Trade directories"]

    C["Stage 2 — enrich each company<br><br>
    Website scan • Founder LinkedIn • News & job posts"]

    D["Stage 3 — hard exclusion check (EX-01 to EX-09)<br><br>
    Trader / service / generic pharma • PE-owned / subsidiary • >₹500Cr"]

    H["disqualified.csv"]

    E["Stage 4 — Federer scoring (0–100)"]

    E1["C1<br>Manufacturer<br>20 pts"]
    E2["C2<br>City presence<br>10 pts"]
    E3["C3<br>Differentiated<br>20 pts"]
    E4["C4<br>Technical DM<br>20 pts"]
    E5["C5<br>Tailwind<br>15 pts"]
    E6["C6<br>Growth<br>15 pts"]

    F["Score filter<br><br>Keep only Federer Score ≥ 80<br>Target: 25 companies"]

    G["federer_companies_{CITY}_{SEGMENT}.csv"]

    A --> B
    B --> C
    C --> D

    D --> H
    D --> E

    E --> E1
    E --> E2
    E --> E3
    E --> E4
    E --> E5
    E --> E6

    E1 --> F
    E2 --> F
    E3 --> F
    E4 --> F
    E5 --> F
    E6 --> F

    F --> G
```
