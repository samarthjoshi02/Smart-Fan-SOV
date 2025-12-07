Smart Fan Share of Voice (SoV) Analysis for Atomberg

In today’s competitive consumer appliance market, online visibility and customer perception play a crucial role in shaping brand success. As part of the Atomberg Data Science & AI Internship assignment, this project focuses on developing a comprehensive analytical system that measures the Share of Voice (SoV) and Share of Positive Voice (SoPV) for smart fan brands, with the objective of understanding Atomberg’s relative position in digital spaces. The project combines data collection, natural language processing (NLP), and analytical modeling to produce clear insights, visualizations, and a professional two-page report summarizing findings.

The core goal of the project is to quantify how frequently Atomberg and its competitors are mentioned across top search results and online videos, how positively they are portrayed, and how relevant each mention is to smart fan–related queries. To achieve this, a complete end-to-end pipeline was built using Python and industry-standard tools. The pipeline begins with generating a set of high-intent keywords such as “smart fan,” “best smart fan,” “smart fan review,” and “Atomberg smart fan.” These queries reflect the phrases that consumers typically search when exploring purchases or comparisons. Using SerpAPI, the system collects structured Google Search results for these keywords, including titles, snippets, URLs, and metadata.

In addition to web data, the project integrates information from YouTube, a platform with tremendous influence in consumer decision-making. Through the YouTube Data API, the system retrieves videos related to smart fans and extracts meaningful engagement metrics like views, likes, and comments. This allows the model to factor in not only textual relevance but also user interactions — an important signal of public interest and brand popularity.

Once data is collected, the next challenge is to extract the complete content from each webpage. Since many articles vary in structure and format, the project uses a hybrid approach combining Newspaper3k for readable article extraction and BeautifulSoup as a fallback for content parsing. This ensures that even non-standard pages yield meaningful text for analysis. The extracted content, along with the original metadata, forms the enriched dataset used for deeper NLP processing.

The NLP phase consists of three major components. First, the system identifies brand mentions using robust pattern matching, ensuring detection of brands like Atomberg, Havells, Crompton, Orient, and Bajaj across titles, snippets, and article bodies. Next, the project applies a transformer-based sentiment analysis model to evaluate whether each mention is positive, negative, or neutral. Finally, the semantic relevance of each document to smart fan–related queries is measured using SentenceTransformer embeddings. By comparing embedding vectors, the system identifies which articles or videos are truly relevant to the topic, filtering out noise and ensuring accuracy in final scoring.

To compute Share of Voice, the project introduces a weighted scoring model that balances multiple signals: engagement, relevance, and sentiment. Engagement is treated as a strong indicator of public attention; sentiment reflects consumer perception; and relevance ensures that only genuinely smart fan–related content influences results. The final weight for each document is calculated using a composite equation that amplifies meaningful content while minimizing low-impact or irrelevant mentions.

After scoring all documents, the results are aggregated brand-wise to produce two key metrics: Share of Voice, which measures overall online presence, and Share of Positive Voice, which highlights how much of the discussion is favorable. These results are visualized using clean, professional bar charts and incorporated into a two-page PDF report generated using the ReportLab library. The report summarizes the entire analysis, highlights brand performance, and provides strategic recommendations for strengthening Atomberg’s online visibility.

The findings generated through this project offer valuable insights for marketing, product positioning, and customer engagement. For example, Atomberg may have strong presence on YouTube due to high-engagement reviews, but competitors might dominate SEO-driven listicles and buying guides. Such insights can guide tailored marketing strategies like producing comparison content, improving long-tail keyword SEO, or partnering with influencers.

Overall, this project demonstrates the integration of data engineering, NLP modeling, API-based data collection, and business-oriented analysis. It successfully transforms scattered online content into structured intelligence, producing actionable insights that can support strategic decision-making. Beyond fulfilling the assignment requirements, the project reflects an ability to design end-to-end analytical systems, work with real-world APIs, extract and clean text at scale, apply modern NLP techniques, and communicate findings through polished reports and visualizations — a strong demonstration of readiness for a Data Science & AI role.

Smart-Fan-SoV — Share of Voice for Smart Fans (Atomberg Assignment)
*Project goal:* Build a small, reproducible Python pipeline that collects web and YouTube content about
smart fans, analyzes menƟons, senƟment and engagement, and computes a composite Share of Voice
(SoV) and Share of PosiƟve Voice (SoPV) for Atomberg vs compeƟtors. This repo contains the code, data
outputs, visualizaƟons and a two-page submission-ready report.

Table of contents
1. Project overview
2. What you’ll get (deliverables)
3. Tech stack & third-party services
4. Prerequisites
5. Project structure (files & folders)
6. ConfiguraƟon (.env)
7. Setup — install & prepare environment (Windows / macOS / Linux)
8. How to run — step-by-step commands
9. What each script does (detailed)
10. Output files & where to find them
11. Tips, tuning & common troubleshooƟng
12. Ethics, rate limits & TOS notes
13. How to extend (ideas)
14. ContribuƟon & license
15. Contact
16. 
1. Project overview:
 This project collects top search results and YouTube videos for queries like smart fan, extracts the
text (Ɵtles, snippets, arƟcle bodies), runs NLP (menƟon detecƟon, senƟment, embeddings),
computes a composite SoV per brand, visualizes results, and generates a polished two-page PDF
report for submission.
 It is designed to be simple to run locally in a reproducible virtual environment (Windows-friendly
instrucƟons included).

3. Deliverables:
- Source code: src/ (scripts & modules)
- Data dump: data/ (raw JSON, enriched JSON, scores, charts, PDF)
- Two-pager submission PDF: data/two_pager.pdf or data/report_atomberg.pdf
- OpƟonal: atomberg_submission.zip (zip of deliverables)

3. Tech stack & third-party services
- Python 3.10+ (tested on Python 3.13)
- Libraries: requests, beauƟfulsoup4, newspaper3k (fallback), spacy, transformers, sentencetransformers, torch, matplotlib, seaborn, reportlab, python-dotenv, tqdm, faiss-cpu
(opƟonal)
- APIs: SerpAPI (Google SERP) and YouTube Data API v3 (video metadata)
- Local tools: VS Code recommended

4. Prerequisites
- Python 3.10+ installed
- Git (opƟonal)
- API keys: SERPAPI_KEY and YT_API_KEY (create accounts and copy keys)
- Reasonable internet connecƟon

5. Project structure
smart-fan-sov/
├─ .env # local config (not commiƩed)
├─ .giƟgnore
├─ README.md
├─ requirements.txt
├─ src/
│ ├─ __init__.py
│ ├─ config.py
│ ├─ collect_serp.py
│ ├─ collect_youtube.py
│ ├─ fetch_content.py
│ ├─ nlp_uƟls.py
│ ├─ scoring.py
│ ├─ visualize.py
│ └─ generate_report.py
├─ data/
│ ├─ serp_raw.json
│ ├─ serp_enriched.json
│ ├─ youtube_raw.json
│ ├─ scores.json
│ ├─ sov_chart.png
│ ├─ sopv_chart.png
│ └─ two_pager.pdf (or report_atomberg.pdf)
└─ run_pipeline.sh

7. ConfiguraƟon (.env)
- Create a .env file at project root (DO NOT commit it).
Example:
SERPAPI_KEY=your_real_serpapi_key_here
YT_API_KEY=your_real_youtube_api_key_here
N_RESULTS=50
- N_RESULTS controls how many results to fetch per query (default 50). Lower to save quota.
- Keep .env secret; it is ignored by .giƟgnore.

7. Setup - install & prepare environment
cd C:\path\to\smart-fan-sov
python -m venv .venv
.venv\Scripts\AcƟvate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
python -m spacy download en_core_web_sm
If newspaper3k throws lxml.html.clean errors, run:
pip install lxml_html_clean
pip install "lxml[html_clean]"

9. How to run - step-by-step (recommended sequence)
Note: run each block from project root while the venv is acƟve.
*Collect SERP results (Google via SerpAPI)*
- python -m src.collect_serp
This saves data/serp_raw.json.
*Collect YouTube results*
- python -m src.collect_youtube
This saves data/youtube_raw.json.
*Fetch arƟcle content (enrich web results)*
- python -m src.fetch_content
This creates data/serp_enriched.json.
*(OpƟonal) Run NLP uƟliƟes test*
python - <<'PY'
from src.nlp_uƟls import detect_brand_menƟons, compute_senƟment, semanƟc_relevance_score
print(detect_brand_menƟons("Atomberg is great, Crompton is okay"))
print(compute_senƟment("I love this fan. It saves a lot of electricity."))
print(semanƟc_relevance_score("smart fan", "Atomberg smart fan saves energy"))
PY
*Compute SoV scores*
- python -m src.scoring
This writes data/scores.json.
*Visualize*
- python -m src.visualize
Generates data/sov_chart.png and data/sopv_chart.png.
*Generate two-pager PDF*
- python -m src.generate_report
Creates data/two_pager.pdf (or data/report_atomberg.pdf if you renamed).
*(OpƟonal) Zip submission*
PowerShell:
Compress-Archive -Path data\two_pager.pdf, data/scores.json, src, README.md -DesƟnaƟonPath
atomberg_submission.zip -Force

9. What each script does (detailed)
- src/config.py — Loads .env and shared configs (queries, brands, file paths).
- src/collect_serp.py — Uses SerpAPI to fetch Google organic results for query variants; stores
compact records in data/serp_raw.json.
- src/collect_youtube.py — Uses YouTube Data API to search query variants and fetch video
staƟsƟcs; saves data/youtube_raw.json.
- src/fetch_content.py — For each web result in serp_raw.json, extracts arƟcle content with
newspaper3k (fallback to BeauƟfulSoup), writes data/serp_enriched.json.
- src/nlp_uƟls.py — Brand menƟon detecƟon (regex), senƟment (transformer pipeline),
embeddings & relevance (sentence-transformers).
- src/scoring.py — Normalizes engagement/relevance/senƟment, computes per-result weight,
aggregates brand-level SoV and SoPV, writes data/scores.json.
- src/visualize.py — Creates bar charts sov_chart.png & sopv_chart.png.
- src/generate_report.py — Generates 2-page PDF (Page 1: tech & methodology; Page 2: SoV
values, charts, recommendaƟons).
- run_pipeline.sh — convenience orchestraƟon shell (You can adapt to your environment).

10. Output files & descripƟon
- data/serp_raw.json — raw SERP rows (Ɵtle, link, snippet)
- data/serp_enriched.json — same rows plus content (arƟcle body extracted)
- data/youtube_raw.json — raw YouTube results with staƟsƟcs
- data/scores.json — final computed SoV & SoPV per brand (JSON)
- data/sov_chart.png / data/sopv_chart.png — charts used in PDF
- data/two_pager.pdf (or report_atomberg.pdf) — final submission-ready two pages

11. Tips, tuning & troubleshooƟng
*Common issues*
- ImportError: lxml.html.clean: install lxml_html_clean or use BeauƟfulSoup-only fallback.
- ModuleNotFoundError: No module named 'dotenv': run pip install python-dotenv.
- PowerShell errors running here-doc (python - <<'PY'): use python -c "..." one-liner or create a
small .py script and run python file.py.
- SerpAPI returns 401 Unauthorized: check .env and make sure SERPAPI_KEY is correct and
acƟve.
- Rate limits (429): reduce N_RESULTS, add larger Ɵme.sleep() in collectors, or throƩle
queries.
- Many empty arƟcle contents: pages might be JS-rendered; consider Selenium headless
browser for heavy JS pages (more setup).
- Pylance warnings in VS Code: ensure VS Code interpreter is set to .venv\Scripts\python.exe;
restart VS Code.
*Tuning*
- Adjust ALPHA_ENG and BETA_MENTION in src/scoring.py to emphasize engagement or
coverage.
- Tune N_RESULTS in .env for larger/smaller samples.
- Swap senƟment model for more nuanced probability outputs and use score weighƟng
instead of mapping to -1/0/1.

12. Ethics, rate limits & TOS notes
- Use official APIs when available (SerpAPI, YouTube Data API). Scraping public websites may
violate some sites’ TOS — follow robots.txt and rate-limits.
- Don’t publish or expose private user data from comments without anonymizaƟon.
- Always cite sources if using direct quotes or large content extracts in public materials.

13. How to extend (ideas)
- Add X/TwiƩer and Instagram scraping (requires API or approved scraping approach).
- Store results in a Ɵme-series DB (Postgres / MongoDB) and track SoV over Ɵme.
- Add an automated scheduler (GitHub AcƟons / Cloud FuncƟon) to run weekly SoV reports.
- Replace sentence-transformers with an on-premise embedding service or vector DB
(Pinecone) for scale.
- Build a small web dashboard (Streamlit / Dash) for interacƟve exploraƟon.

14. ContribuƟng & license
- Suggested workflow: fork → branch → PR. Make sure to remove your .env from commits.
- License: MIT (add LICENSE if you want to publish). If you want, I can add a standard LICENSE
file.

15. Contact
Email: samarthsj2005@gmail.com
Linkedin: [hƩps://www.linkedin.com/in/samarth-joshi020305/]
Github: [hƩps://github.com/samarthjoshi02] 
