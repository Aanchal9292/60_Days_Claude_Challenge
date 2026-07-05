🌍 Day 9/60 — #ABTalksAIChallenge
Today's build: a Personal Environmental Health Analyzer — a fully interactive dashboard tracking air + water quality across 12 cities, centered on my home region: Modinagar and Hapur, UP.
What it does:
📊 Live-sourced AQI, PM2.5 & PM10 for 12 NCR/Western UP cities
💧 Water quality scores grounded in peer-reviewed Hindon River WQI research
🧾 A computed Environmental Health Score (0–100) with A–F grades for Air, Water & Overall
🎛 Interactive filters, 5 live charts, city cards, and a personalized health-impact deep-dive
The most interesting thing I learned wasn't technical — it was in the data itself:
Air and water pollution don't move together in this region. Meerut and Gurugram both have only moderate AQI, but score in the 30s–40s on water quality because groundwater along the Hindon corridor is hard, high-TDS, and fluoride-affected. A "good air day" tells you nothing about whether your water is safe.
A key discipline moment: Modinagar has no official CPCB monitoring station. Instead of letting the AI fabricate a clean number, I had it transparently interpolate from the two nearest stations (Ghaziabad + Meerut) and flag that everywhere in the app. Anti-hallucination discipline isn't just for resumes — it applies to environmental data too.
Biggest takeaway: the data-gathering shaped the story more than the code did. The real insight (air ≠ water pollution) only surfaced because I pushed past the obvious AQI-only build and dug into the actual river-basin research for where I live.
🔗 Full dashboard + Day 9 learning journal in the comments/portfolio.
#AI #ClaudeAI #DataAnalysis #EnvironmentalHealth #BuildInPublic #60DayChallenge #AIforGood
@Anthropic @ABTalks on AI @Anil Bajpai