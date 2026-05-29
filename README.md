# DT

Scraped the list of companies by creating my own scraper , only 6 of them could qualify for greater than 65 score in Basket B types companies , currently not included LinkedIn (via SerpAPI) and others which requires specialized APIs.

Note : it may take a few seconds for the diagrams to load

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



Question 2: The 1000-Company Proposal

Approach to building a list of ICP-qualified companies would combine automated scraping, data enrichment, scoring, and verification. First, I would collect a large company universe from MCA21, DGFT, TradeIndia, IndiaMART, industry directories, and other publicly available databases, while also using specialized APIs where available. The scraper would gather company names, websites, locations, and industry information. Next each company would be enriched using website analysis, LinkedIn data, founder profiles, and business directories. Key qualification signals would include industry relevance, manufacturing activity, import/export presence, technology adoption, growth indicators, and revenue signals. These attributes would be converted into an ICP score based on the target profile requirements. Companies above the qualification threshold would move to the verification stage. Quality assurance would be performed by cross-checking data across multiple sources to reduce false positives and missing information. The process would run iteratively, refining scoring rules whenever verification reveals classification errors. The final output would be a verified dataset of approximately 1,000 ICP-qualified companies exported in CSV and JSON formats.

```mermaid
flowchart TD

    A[Company Discovery & Scraping]

    A1[MCA21]
    A2[DGFT]
    A3[TradeIndia]
    A4[IndiaMART]
    A5[Industry Directories]
    A6[Specialized APIs<br/>LinkedIn / SerpAPI]

    A1 --> A
    A2 --> A
    A3 --> A
    A4 --> A
    A5 --> A
    A6 --> A

    A --> B[Filter & Enrichment]

    B --> B1[Website Analysis]
    B --> B2[LinkedIn Profile]
    B --> B3[Founder Information]
    B --> B4[Industry Classification]
    B --> B5[Import / Export Activity]
    B --> B6[Manufacturing Signals]
    B --> B7[Technology Adoption]
    B --> B8[Growth Indicators]
    B --> B9[Revenue Signals]

    B --> C[ICP Scoring Engine]

    C --> D[Qualification Threshold]

    D --> E[Quality Assurance & Verification]

    E --> E1[Cross-Source Validation]
    E --> E2[Duplicate Detection]
    E --> E3[False Positive Removal]
    E --> E4[Missing Data Checks]

    E --> F[Final Qualified Companies]

    F --> G[CSV Export]
    F --> H[JSON Export]
```










