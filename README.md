# Social Network Analysis — COVID-19 Twitter

> Mapping the COVID-19 conversation on Twitter during the pandemic using graph theory and social network analysis.

---

## Group Members

| NRP | Name |
|---|---|
| 5025221257 | Syarif Sanad |
| 5025231151 | Mirza Syahrizal Fathir |
| 5025231309 | Aditya Fieansyah Putra Pratama |
| 5025231199 | Felda Ega Fadhila |

---

## Project Overview

This project analyzes the **COVID-19 Twitter social network** to understand how information spreads and who drives the conversation during a global pandemic. We construct a directed weighted graph from 179,108 tweets collected between **July 24 – August 30, 2020**, all tagged with `#covid19`.

The core question we set out to answer:

> *"Was COVID-19 Twitter a global conversation — or just isolated echo chambers?"*

Our findings show it was overwhelmingly the latter.

---

## Dataset

- **Source:** [Kaggle — COVID-19 Tweets](https://www.kaggle.com/datasets/gpreda/covid19-tweets?resource=download)
- **File:** `covid19_tweets.csv`
- **Size:** 179,108 tweets, 13 columns
- **Period:** July 24, 2020 → August 30, 2020
- **Key columns:** `user_name`, `text`, `date`, `user_followers`, `user_verified`, `user_location`

---

## Methodology

### Pipeline Overview
```
Raw CSV
  └── Edge Extraction (retweet, mention, hashtag)
        └── Graph Construction (directed, weighted)
              └── Centrality Metrics (PageRank, betweenness, degree)
                    └── Community Detection (Louvain)
                          └── Sentiment Analysis (VADER)
                                └── Visualization (Pyvis, Matplotlib)
                                      └── Echo Chamber Analysis
```

### Steps
| Step | Description |
|---|---|
| 1 | Install & import libraries |
| 2 | Load & inspect dataset |
| 3 | Define text extraction helpers |
| 4 | Extract retweet, mention & hashtag edges |
| 5 | Build directed weighted user–user graph |
| 6 | Attach node attributes (followers, verified, location) |
| 7 | Compute centrality metrics |
| 8 | Export node attribute table |
| 9 | Compute network structural metrics |
| 10 | Louvain community detection |
| 11 | Label node structural roles |
| 12 | VADER sentiment analysis |
| 13 | Build hashtag co-occurrence network |
| 14 | Temporal edge analysis |
| 15 | Generate visualizations |
| 16 | Build interactive Pyvis network |
| 17 | Echo chamber analysis |
| 18 | Community profiling |
| 19 | Export final summary |

---

## Key Results

### Network Statistics
| Metric | Value |
|---|---|
| Total nodes (users) | 69,069 |
| Total edges (interactions) | 73,791 |
| Network density | 0.000015 |
| Communities detected | 10,389 |
| Modularity score | **0.8867** |
| Avg clustering coefficient | 0.0000 |

### Top 5 Influencers by PageRank
| Rank | Account | PageRank |
|---|---|---|
| 1 | realdonaldtrump | 0.01314 |
| 2 | youtube | 0.00236 |
| 3 | who | 0.00213 |
| 4 | borisjohnson | 0.00156 |
| 5 | joebiden | 0.00131 |

### Echo Chamber Finding
```
Intra-community edges : 91.7%   Strong echo chamber signal
Inter-community edges :  8.3%
```

### Top 5 Communities
| Community | Size | Sentiment | Identity |
|---|---|---|---|
| 4 | 5,919 | -0.096 (negative) | US anti-Trump political cluster |
| 3 | 3,091 | +0.082 (positive) | Indian government & media cluster |
| 13 | 2,915 | -0.019 (neutral) | UK COVID & Brexit cluster |
| 0 | 2,376 | ~0.000 (neutral) | General US COVID news cluster |
| 7 | 1,859 | +0.058 (positive) | Global health & media cluster |

---

## Tech Stack

| Tool | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `networkx` | Graph construction and metrics |
| `python-louvain` | Community detection |
| `vaderSentiment` | Sentiment analysis |
| `pyvis` | Interactive network visualization |
| `matplotlib` / `seaborn` | Static charts |
| `tqdm` | Progress tracking |


---
## Visualizations

### 1. Top 20 Influencers by PageRank
> Who dominates the COVID-19 Twitter conversation?

![Top 20 Influencers](<img width="1190" height="590" alt="image" src="https://github.com/user-attachments/assets/a4120474-8296-4b31-a3aa-476d7d031095" />)

> `realdonaldtrump` leads with a PageRank **6x higher** than the second-ranked account. CNN is the only verified account in the top 10.

---

### 2. Community Sizes (Louvain)
> How many users belong to each detected community?

![Community Sizes](<img width="989" height="390" alt="image" src="https://github.com/user-attachments/assets/befecf1b-a747-47a3-896e-742ecf45ca01" />
)

> Community 4 (US political cluster) is the largest with 5,919 users — nearly double the size of the second largest community.

---

### 3. Sentiment vs. In-degree
> Does negativity drive reach?

![Sentiment vs In-degree](<img width="858" height="490" alt="image" src="https://github.com/user-attachments/assets/1f98fa80-0c6f-40b2-af8c-7a3ebe05e596" />
)

> The single bright dot at the top is `realdonaldtrump` — highest in-degree (~4,000), near-neutral sentiment. No clear correlation between negativity and reach was found.

---

### 4. Weekly Retweet Edge Volume
> How did network activity change over time?

![Temporal Edge Growth](<img width="989" height="390" alt="image" src="https://github.com/user-attachments/assets/efacd68b-4203-4502-85fb-1b9c95a86378" />
)

> Activity peaked in **week 33 (August 10–16)** corresponding to major COVID news events, then declined sharply — confirming the conversation was news-cycle driven.

---

### 5. Interactive Network (Pyvis)
> Top 300 users by PageRank — colored by community, sized by influence.

![Interactive Network](![Uploading image.png…](<img width="1874" height="747" alt="image" src="https://github.com/user-attachments/assets/9d0c23bc-4c42-48f4-8316-be42afd8caee" />
))


---
## Key Insights

1. **Trump is the gravitational center** — referenced 6x more than the WHO, dominating every cluster regardless of political leaning.
2. **91.7% echo chamber rate** — COVID Twitter was not a global conversation. It was five parallel monologues in isolated ideological bubbles.
3. **Broadcast, not conversation** — near-zero clustering coefficient confirms users talk AT influencers, not WITH each other.
4. **Sentiment does not drive reach** — no correlation between negative sentiment and high in-degree, disproving the outrage-amplification hypothesis.
5. **India cluster is the most institutional** — Community 3 has 50.1% verified accounts, the highest of any community.
