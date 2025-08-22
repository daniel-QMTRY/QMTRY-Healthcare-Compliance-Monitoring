# QMTRY-Healthcare-Compliance-Monitoring
Audit-ready healthcare compliance pipeline—dbt + Great Expectations + Streamlit—with a one-click GitHub Action that produces a downloadable evidence bundle for CMS, HIPAA, and NCQA/HEDIS.

# Healthcare Compliance Monitoring — Demo Pipeline 🚀🛡️

> 🔥 **Compliance just got a glow-up!** Turn audit dread into one-click triumph with this reproducible powerhouse. CMS, HIPAA, NCQA/HEDIS? We've got you covered – audit-ready reports, downloadable evidence, and a snazzy Streamlit portal that'll make execs high-five you. No more boring binders; hello, automated awesomeness! 💼✨

![Run Compliance Demo](https://github.com/daniel-QMTRY/healthcare-compliance-demo/actions/workflows/compliance_demo.yml/badge.svg)  <!-- Adjust repo name if needed -->

## 🎯 Why This Matters (For Buyers & Auditors – No Yawns Allowed!)
Compliance isn't a chore – it's your secret weapon! 🦸‍♂️  

- **One-Click Credibility Boost** 🚀: GitHub Action fires up the whole shebang: ingest seeds → dbt transforms → Great Expectations validations → **Evidence Bundle packaging** → interactive dashboard publishing. Boom – instant trust!
- **Audit Evidence on Demand** 📂: Grab a zip with Data Docs, validation wins/fails, metadata, and configs. Perfect for shutting down auditor questions with style.
- **PHI-Free Fun Zone** 🔒: Demo runs on synthetic data (deterministic and drama-free) – safe for public demos. Swap in real stuff when you're ready to rock.
- **Governance Superpowers Baked In** 🧠: dbt tests + exposures trace lineage and ownership. Quality gates? Visible, repeatable, and ready to impress!

Say goodbye to manual mess and hello to automated audits that actually excite! 😎

## 📦 What You Get (The Treasure Chest of Compliance Goodies) 🎁
- **Streamlit “Compliance Home” Portal** 🏠: Exec-friendly front door with HIPAA, CMS, NCQA tiles packed with punchy talking points. Latest run summaries (pass/fail vibes), quality-measure tables (demo PDC), and a **⬇ Download Evidence Bundle** button that'll save your day.
- **Evidence Bundle (Zip Magic)** 📦: Stuffed with Great Expectations **Data Docs** site, validation results, run_summary.json – RFP and audit ammo, ready to deploy!
- **Transforms + Tests Galore** 🛠️: dbt (DuckDB) models for staging + PDC summaries. schema.yml loaded with not_null/unique tests + an exposure linking straight to your Streamlit dashboard.

All this in a neat package – because compliance should feel like a win, not a workout! 🏆

## 🏗️ Architecture (At a Glance – Visual Vibes!) 🔍
Picture this: A seamless flow from data to dashboards, dodging compliance pitfalls like a ninja. Here's the Mermaid magic:

```mermaid
flowchart LR
  A[Seeded Demo Data\n(CSV)] --> B[dbt (DuckDB)\nmodels + tests]
  B --> C[Great Expectations\ncheckpoint + Data Docs]
  B --> D[Measures Table\n(quality_measures)]
  C --> E[Evidence Bundle\n(Zip Artifacts)]
  D --> F[Streamlit\nCompliance Home]
  E -. download .-> F
```

Simple, scalable, and seriously slick! 🌟

## 🚀 Quickstart (Local Demo – Zero to Hero in Minutes!) ⚡
Fire up your compliance engine locally – no cape required!

```bash
# 1) Create and activate a virtual env 🛡️
python -m venv .venv && source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 2) Install deps 📦
pip install -r pipelines/compliance_monitoring/requirements.txt

# 3) Build the DuckDB models with dbt 🏗️
export DUCKDB_PATH=pipelines/compliance_monitoring/demo.duckdb
dbt seed --project-dir pipelines/compliance_monitoring/dbt --profiles-dir pipelines/compliance_monitoring/dbt
dbt run  --project-dir pipelines/compliance_monitoring/dbt --profiles-dir pipelines/compliance_monitoring/dbt

# 4) Run data quality checks & generate Data Docs 🔍
python pipelines/compliance_monitoring/scripts/run_gx.py

# 5) Package the evidence bundle (zip) 🎁
python pipelines/compliance_monitoring/scripts/package_evidence.py

# 6) Launch the Streamlit portal 📊
streamlit run pipelines/compliance_monitoring/streamlit_app.py
```

* **Evidence Bundle Location:** `pipelines/compliance_monitoring/artifacts/evidence_bundle.zip` – Your audit lifesaver!  
* **Data Docs (Local Peek):** Open `pipelines/compliance_monitoring/artifacts/gx_site/index.html` for the full scoop.

## 🌐 One-Click Demo in GitHub (Cloud Magic!) ☁️
1. Push this repo to GitHub. 📤  
2. Head to Actions → Run Compliance Demo → Hit "Run workflow." 🏃‍♂️  
3. Grab the Artifacts → `compliance_artifacts` (includes your shiny Evidence Bundle).  
4. Slap this badge on your README (swap in your org/repo):  
   ```md
   ![Run Compliance Demo](https://github.com/daniel-QMTRY/healthcare-compliance-demo/actions/workflows/compliance_demo.yml/badge.svg)
   ```

Watch it run and feel the power! 💥

## 🗂️ Folder Structure (Where the Magic Hides) 🗺️
```
pipelines/compliance_monitoring/
├─ data/seed/                     # Demo CSVs (no PHI – synthetic superstars!) 📊
├─ dbt/
│  ├─ models/{staging,marts}/     # DuckDB models – transform like a boss 🔧
│  ├─ models/schema.yml           # Tests + Streamlit exposure – governance goals 🧠
│  ├─ seeds/                      # Mirrored seeds for dbt seeding
│  ├─ dbt_project.yml
│  └─ profiles.yml                # DuckDB profile – easy swaps!
├─ great_expectations/
│  ├─ expectations/meds_basic.yml # Quality suites – expect greatness! ✅
│  ├─ checkpoints/compliance_checkpoint.yml
│  └─ great_expectations.yml
├─ scripts/
│  ├─ run_gx.py                   # Runs checkpoint + spits out run_summary.json 📝
│  └─ package_evidence.py         # Zips artifacts into evidence_bundle.zip 🎉
├─ artifacts/                     # Runtime goodies (Data Docs, zip, etc.) 🗃️
└─ streamlit_app.py               # Your Compliance Home portal – execs' new BFF! 🖥️
```

Organized chaos? Nah – pure efficiency! 📁

## 📊 What the Streamlit Portal Shows (Sneak Peek of the Wow Factor!)
- **HIPAA / CMS / NCQA Tiles** 🏆: Crisp, non-techy language that'll make anyone nod approvingly.
- **Latest Run Panel** ⏰: Timestamp + GX success flag – green means go!
- **Quality Measures Table** 📈: Demo PDC per patient/class – metrics that matter.
- **Evidence Section** 📥: One-click Download Evidence Bundle – because who has time for emails?

Pro Tip: Host Streamlit at https://demo.yourdomain.com. Embed in WordPress via iframe or link out with flair! (Elementor Attributes: rel|noopener noreferrer; aria-label|Open Compliance Demo (opens in new tab)). 🚀

## 🔄 Swapping Demo Data for Real Pipelines (Level Up Time!)
- Ditch CSV seeds for your real feeds – seamless swap! 🔄  
- Point dbt to your warehouse (Snowflake/BigQuery/Redshift/Databricks) via profiles.yml.  
- Beef up Great Expectations: Add row counts, keys, integrity, freshness checks.  
- Expand for CMS audits, HEDIS outputs, and PHI handling – we're ready when you are!

## 🔐 Security & PHI Stance (Demo Edition – Safety First!)
- **Synthetic Data Only** 🛡️: No real PHI – demo-safe and shareable.  
- **Artifacts Stay Local** 📍: Unless you push 'em, they're yours alone.  
- **PHI Mode Unlock** 🔓: Run in HIPAA stacks, lock down access, TLS/KMS everything, audit logs galore. De-ident (Safe Harbor/Expert) and policies? Plug 'em in next!

Compliance without compromise – thrilling, right? 😄

## ❓ FAQ (Quick Hits for Curious Minds)
**Can this run without DuckDB?**  
Absolutely! Swap profiles to your warehouse – dbt doesn't skip a beat.  

**What’s in the Evidence Bundle?**  
Data Docs, validation results, run_summary.json – RFP gold and audit pre-read perfection!  

**How do I show lineage?**  
Add OpenLineage/Marquez (docker-compose up) and emit from dbt/orchestrator – this repo's wired for it.  

## 📜 License
MIT (or your fave) – see [LICENSE](LICENSE). Free to fork and fly! 🕊️

## 📫 Maintainer
QMTRY.ai – Healthcare data engineering & compliance analytics wizards. 🧙‍♂️  
Questions or integration vibes? Hit us at hello@qmtry.ai. Let's make compliance cool together! 🌟
