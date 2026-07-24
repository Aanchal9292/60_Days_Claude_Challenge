Day 28/60 — Building in Public 🏥

Today's build: a Hospital Admission Readiness Simulator — putting you in the seat of a Hospital Admission Coordinator, juggling PA status, insurance, bed assignment, documentation, physician orders, and consent — all at once, all in real time.

No dashboard greets you on load. You start where coordinators actually start: an empty intake form. Provider, attending physician, diagnosis, admission type, PA status. Only after you submit does the real complexity show up.

What this one taught me:

🔹 Readiness isn't one number — it's a weighted system. PA status carries the heaviest weight (25%), followed by documentation and physician orders (20% each). Miss one, and the whole score stalls — no shortcuts.

🔹 Some gaps can't be worked around. A denied PA on an ICU admission is modeled to cap readiness below 70%, no matter how many other boxes get checked. Some risks are structural, not administrative — and the tooling should say so honestly.

🔹 Observation status is its own animal. Every Observation admission surfaces the CMS 2-Midnight Rule note automatically — different cost-sharing, different SNF eligibility, mandatory MOON notification for Medicare patients. Easy to overlook, expensive to miss.

🔹 Utilization Review is a discipline, not a rubber stamp. Modeling the UR role meant naming what it actually does: concurrent review, denial-risk identification, and checking documentation against InterQual and Milliman criteria — especially for Acute MI and CHF, where medical necessity thresholds are strict.

🔹 "Not Ready" should be actionable, not just a red flag. Below 90%, the simulator doesn't just say no — it lists exactly what's missing, what to do next, and which risks remain open.

Healthcare operations run on dozens of quiet, high-stakes decisions like this one. Simulating them — instead of just describing them — makes the stakes, and the process, click.

#ABTalksAIChallenge #Day28 #HealthcareTech #HealthIT #PriorAuthorization #MedicalWorkflow #AI #WebDevelopment #BuildInPublic #LearningInPublic #SoftwareEngineering #HealthTech