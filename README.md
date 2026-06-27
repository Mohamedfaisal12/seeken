# What Mythos changes for your country selection research

**Anthropic's Claude Mythos Preview — announced April 7, 2026 and currently restricted to 52 organizations under Project Glasswing — is the most capable AI model ever built.** It is not an incremental improvement. SWE-bench Pro jumped 24 points over Opus 4.6. Math proof-solving went from 42% to 98%. Multimodal code reasoning more than doubled. Long-context reasoning doubled. Chart comprehension went from 62% to 86% without tools, 79% to 93% with them. This is a capability discontinuity, and it means that the architecture of your entire country selection stack — GDELT sentiment pipeline, T2 Master dataset, momentum reversal predictor, transaction cost framework, LoopPilot autoresearch — can be rethought from the ground up. Not optimized. Rethought. Below is a map of what becomes possible and what you should build first.

---

## Your current stack is strong but fragmented

Based on everything documented in your research system, here is what you are running today:

**Data layer.** The T2 Master dataset covers 34 countries from February 2000 to present with **53 pre-computed factors** at daily and monthly frequency. The T2_Optimizer file stores 82 factor quintile net returns. GDELT sentiment flows through a pipeline of GKG 15-minute ZIP downloads → country_day parquet files → 30-day rolling z-score signals including tone_dispersion_z, country_news_risk, and foreign_tone_z. This covers your 34-country equity rotation universe and draws on the BBVA and Zhang academic literature for signal construction.

**Prediction layer.** The Momentum Reversal Predictor is a binary classifier using regime variables — EPU, GPR, BIS credit data, OECD CLI, sovereign CDS spreads, and term spreads — run through a two-stage quick-eval/walk-forward funnel. The Sonnet/Opus autoresearch loop (via LoopPilot) iterates on model configurations. Your trailing 60-month factor momentum baseline runs at roughly **6.5% annualized**.

**Execution layer.** Transaction costs are modeled through Almgren-Chriss with VIX-regime conditioning, using a Bloomberg ETF transaction cost estimator for a 27-country ETF universe. The IBKR MCP server connects to your broker.

**The gaps are real.** Your GDELT pipeline processes English-language news about 34 countries but misses domestic-language narratives. Your 53 factors are static — no autonomous discovery or retirement mechanism. The regime variables (EPU, GPR, CDS, CLI) are macro proxies, not causal structures. Factor timing lives in "fuzzy" folders, suggesting the approach is still exploratory. And the entire stack requires significant human orchestration across disconnected tools. Each component works. The integration between them does not scale.

---

## Mythos capabilities that rewrite the constraints

Here are the specific Mythos benchmarks that matter for your work, and what each unlocks:


| Capability                   | Mythos                    | Opus 4.6 | What it means for you                                                                                        |
| ---------------------------- | ------------------------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| **SWE-bench Pro**            | 77.8%                     | 53.4%    | Can build and debug entire data pipelines — GDELT ingestion through backtesting — autonomously               |
| **USAMO math proofs**        | 97.6%                     | 42.3%    | Formal derivation of factor properties, optimization constraints, statistical test construction              |
| **SWE-bench Multimodal**     | 59.0%                     | 27.1%    | Reads Bloomberg screens, PDF research tables, central bank charts, scatter plots directly                    |
| **GraphWalks BFS (256K-1M)** | 80.0%                     | 38.7%    | Reasons coherently across your entire T2 dataset description, full codebases, multiple papers simultaneously |
| **CharXiv chart reasoning**  | 93.2%                     | 78.9%    | Extracts quantitative claims from financial charts with near-human accuracy                                  |
| **Terminal-Bench 2.0**       | 82.0% (92.1% extended)    | 65.4%    | Sustained multi-hour autonomous terminal sessions — building, testing, iterating code                        |
| **SWE-bench Multilingual**   | 87.3%                     | 77.8%    | Code reasoning across Python, R, C++, plus natural-language financial analysis in 30+ languages              |
| **BrowseComp**               | 86.9% (4.9× fewer tokens) | 83.7%    | Dramatically cheaper autonomous web research — key for scanning news, academic papers, data sources          |
| **OSWorld computer use**     | 79.6%                     | 72.7%    | Can operate Bloomberg Terminal, Excel, IBKR TWS through GUI interaction                                      |


**Key specs**: 1M token context window (same nominal size as Opus 4.6 but with **2× effective reasoning quality** within that window), 128K max output tokens, adaptive thinking that dynamically allocates compute to harder problems. Pricing is **$25/$125 per million input/output tokens** — 5× Opus 4.6, reflecting the computational intensity. Currently restricted; prediction markets put broader availability at ~73% by June 2026. Anthropic has stated Mythos-class capabilities will come to a future Opus release with additional safeguards.

The compound effect of these improvements is what matters. A model that can simultaneously read charts, write complex code, reason through proofs, maintain coherence across million-token contexts, and run for hours in terminal sessions is not a better chatbot. **It is an autonomous research associate.**

---

## 20 transformative ideas, organized by what they unlock

### Autonomous research agents

**1. The self-running hypothesis factory**

Mythos supervises an end-to-end loop: generate a country selection hypothesis from economic theory or anomaly detection → write the feature engineering code → run the backtest on T2 data → evaluate with proper out-of-sample controls and deflated Sharpe ratios → write up the result → generate the next hypothesis informed by what was learned. Academic work from February 2026 (arxiv 2603.14288, "Beyond Prompting: Autonomous Factor Investing via Agentic AI") demonstrates this is already feasible with current models using "economic regularization" to prevent data mining. Mythos-level capabilities make it robust enough to trust.

*What it unlocks:* Continuous factor discovery without human-in-the-loop. Your 53 factors were curated over years. Mythos could evaluate 500 candidates per week.
*Why impossible before:* Opus 4.6 at 53.4% SWE-bench Pro fails too often on complex multi-file backtesting code. At 77.8%, Mythos crosses the reliability threshold for autonomous pipeline construction.
*First experiment:* Give Mythos your T2 dataset schema, existing factor definitions, and three academic papers (Ehsani & Linnainmaa on factor momentum, Zaremba on cross-country ML, one GDELT paper). Ask it to generate 20 novel country-level factors with economic rationale, implement backtests, and rank by information coefficient. Time it. Compare the top 5 against your existing 53.

**2. Multi-week autoresearch campaigns that replace your LoopPilot loop**

Your current Sonnet/Opus autoresearch harness runs a momentum reversal predictor through quick-eval and walk-forward stages. With Mythos, this becomes a multi-week autonomous campaign: the model maintains a research journal, tracks which configurations were tested, identifies diminishing returns, pivots to new approaches when stuck, and produces a final research report with code, results, and recommendations. Terminal-Bench shows Mythos can sustain coherent execution over 4+ hour sessions at 92.1% accuracy.

*What it unlocks:* You describe a research question ("Can we improve the momentum reversal predictor by adding central bank communication features?") and walk away for a week. Mythos runs hundreds of experiments, documents everything, and hands you a finished analysis.
*Why impossible before:* Extended autonomous operation required coherence that Opus 4.6 couldn't maintain. Answer thrashing — the model contradicting its own earlier work — occurred frequently. Mythos reduces this by 70%.
*First experiment:* Task Mythos with improving your momentum reversal predictor's accuracy by 2 percentage points, giving it access to the full T2 dataset, regime variable definitions, and a week of compute. Constrain it to document every experiment in a structured log. Compare its best model against your current production model.

**3. Autonomous academic paper replication factory**

Feed Mythos a queue of factor investing papers — Asness on value, Moskowitz on time-series momentum, Novy-Marx on quality, Harvey's factor zoo critique — and have it autonomously replicate each paper's core results on your T2 dataset. For each replication, it reports: does the factor work in your universe? Has it decayed? Does it survive transaction costs at your Almgren-Chriss estimates?

*What it unlocks:* A systematic audit of every published country-level factor against your actual investable universe, completed in days rather than months.
*Why impossible before:* Paper replication requires reading the paper (multimodal — tables, equations, figures), writing the code, handling data mismatches, and interpreting results. The 59% SWE-bench Multimodal (vs 27.1%) and 93.2% CharXiv are the specific capability jumps that make this feasible.
*First experiment:* Start with Ehsani & Linnainmaa (2022) on factor momentum — the paper most directly relevant to your 6.5% annualized baseline. Have Mythos replicate their Table 2 results using your T2 data. Verify whether their 51 basis points per month after positive years holds in your 34-country universe.

---

### Multimodal intelligence

**4. Central bank PDF reading at scale**

Every month, your 34 countries produce monetary policy statements, financial stability reports, and inflation reports — many as PDFs with embedded charts, tables, and non-English text. Mythos can ingest these directly. The IMF has already demonstrated (Working Paper 2025/109) that LLM analysis of 74,882 central bank documents across 169 countries predicts future rate movements. Your current regime variables (term spreads, EPU) are downstream proxies for what's in these documents. Go upstream.

*What it unlocks:* A "directional communication index" per country that captures monetary policy stance, forward guidance shifts, and financial stability concerns directly from source documents — not lagging market-derived proxies.
*Why impossible before:* Central bank PDFs contain charts (dot plots, fan charts), tables, and text in native languages. Opus 4.6 at 61.5% CharXiv without tools couldn't reliably extract quantitative claims from these charts. Mythos at 86.1% can.
*First experiment:* Collect the last 12 months of monetary policy statements from 10 countries in your universe (mix of DM and EM). Have Mythos extract: policy direction, confidence language, risk assessment, and quantitative forecasts. Build a monthly "hawkishness score" per country. Test whether this score predicts next-month country equity returns better than your current term spread signal.

**5. Bloomberg terminal reading and dashboard monitoring**

OSWorld-Verified at 79.6% means Mythos can operate computer GUIs — clicking, typing, navigating. Combined with CharXiv chart reasoning at 93.2%, it can read Bloomberg screens, extract data from proprietary terminals, interpret risk dashboards, and execute trades through IBKR TWS. Your existing IBKR MCP server handles programmatic access; Mythos adds the visual layer.

*What it unlocks:* A monitoring agent that watches Bloomberg screens for anomalies across your 34-country universe — unusual option skew, sudden spread widening, volume spikes — and alerts you with interpretation, not just numbers.
*Why impossible before:* Computer use at 72.7% (Opus 4.6) was too unreliable for financial operations where clicking the wrong button has real consequences. The 7-point improvement matters at the margin.
*First experiment:* Set up a sandboxed Bloomberg terminal environment. Have Mythos navigate to your 34-country equity monitor, take screenshots at market close, and produce a daily "anomaly report" highlighting countries where today's factor behavior deviates significantly from the 30-day rolling mean. Compare its alerts against your existing z-score signals.

**6. Multimodal sell-side research synthesis**

Your research desk receives PDFs from Goldman, Morgan Stanley, JPM, BBVA. These contain charts, tables, and narrative analysis that currently require human reading. Mythos processes the entire document — extracting quantitative forecasts from tables, interpreting charts, and synthesizing narrative claims into structured data.

*What it unlocks:* Automated extraction of consensus and contrarian views from sell-side research across your entire country universe, updated as reports arrive.
*Why impossible before:* LAB-Bench FigQA went from 75.1% to 89.0%. The difference between 75% and 89% accuracy on figure interpretation is the difference between "useful but needs checking" and "reliable for automated extraction."
*First experiment:* Take 20 recent sell-side country research reports. Have Mythos extract: GDP forecast, earnings growth forecast, recommended weight, key risk factors. Compare against Bloomberg consensus. Measure extraction accuracy.

---

### Cross-lingual sentiment intelligence

**7. Native-language financial news processing for all 34 countries**

Your GDELT pipeline processes English-language news about countries. But the **domestic narrative** — Korean editorials on chaebol reform, Turkish commentary on lira policy, Brazilian analysis of fiscal dynamics — lives in local languages. Academic work shows culture-specific sentiment markers (Chinese "cutting leeks" = bearish retail sentiment) are destroyed by translation. Mythos at 87.3% SWE-bench Multilingual suggests dramatically improved cross-lingual reasoning.

*What it unlocks:* A "sentiment divergence" signal: when domestic-language sentiment turns negative while English GDELT remains neutral, insiders know something the global market hasn't priced. This is a genuine informational edge.
*Why impossible before:* Processing financial news in 34 languages with domain-specific cultural nuance required models that maintained financial reasoning quality across distant language pairs. Previous models degraded sharply — cross-lingual financial sentiment accuracy dropped to 46% for English-Japanese pairs.
*First experiment:* Pick 5 countries where your GDELT English sentiment has the lowest predictive power. Collect local-language financial news (Nikkei for Japan, Folha de São Paulo for Brazil, Hürriyet for Turkey, Dong-A Ilbo for Korea, Kommersant for Russia). Have Mythos score sentiment directly in the source language. Compute the divergence between local-language sentiment and your existing GDELT tone_dispersion_z. Test whether this gap predicts next-month country returns.

**8. Real-time cross-lingual event detection**

Go beyond sentiment. Have Mythos agents monitoring local-language news detect specific event types — capital control rumors, regulatory changes, political instability signals, corporate governance scandals — in real time across all 34 countries. GDELT's GKG codes events but its automated translation and coding introduce noise. A frontier model reading the source text directly is higher fidelity.

*What it unlocks:* Event-driven risk signals with **hours** of lead time over English-language GDELT, especially for EM countries where translation lag is longest.
*Why impossible before:* Required near-native financial comprehension in 34 languages simultaneously, with the coding ability to update risk scores in real time.
*First experiment:* Run a parallel pipeline for 3 months: your existing GDELT event detection alongside Mythos reading local-language RSS feeds for 10 countries. Compare: How often does Mythos detect a material event before GDELT captures it? What's the average lead time?

---

### Causal reasoning and counterfactual analysis

**9. Causal factor graphs replacing correlation matrices**

Your 53 factors are evaluated by correlation with returns. But correlation is not causation, and this is why factors decay — you're trading patterns that were never causal to begin with. Causal discovery algorithms (PC, FCI, CD-NOTS for non-stationary data) can learn directed causal graphs from your T2 data. Mythos's 97.6% math reasoning means it can implement do-calculus, evaluate Markov equivalence classes, and critically assess whether discovered causal edges make economic sense.

*What it unlocks:* A factor library where each factor has a documented causal pathway, not just a historical correlation. Causal factors should be more robust across regimes because they capture the mechanism, not just the symptom.
*Why impossible before:* Causal discovery on macro data is notoriously hard — it requires integrating domain knowledge constraints, handling confounders, and reasoning about whether results make economic sense. This is a joint coding + math + domain reasoning task that Opus 4.6 couldn't reliably execute.
*First experiment:* Use the causal-learn Python library to run the PC algorithm on 30 years of monthly data: your 53 factors plus country equity returns for 10 countries. Have Mythos evaluate the discovered graph, flag edges that are likely confounded, and identify the 5 strongest causal pathways from factors to returns. Test whether a portfolio using only causally validated factors outperforms the full 53-factor model out-of-sample.

**10. Counterfactual scenario generation for stress testing**

Move beyond historical replay for stress testing. A variational autoencoder (MacroVAE, presented at ACM ICAIF 2025) can generate realistic but never-observed macro scenarios: "What would have happened to your portfolio if China experienced a hard landing while the Fed was cutting?" Mythos builds the VAE, validates it against historical episodes, and generates thousands of counterfactual scenarios.

*What it unlocks:* Stress testing against scenarios that haven't happened yet — the specific combination of shocks your portfolio is most vulnerable to.
*Why impossible before:* Building a calibrated generative model for multi-country macro scenarios requires substantial mathematical and coding capability working together.
*First experiment:* Build a MacroVAE conditioned on 5 macro variables (GDP growth, inflation, rates, trade balance, VIX) for your 34 countries. Generate 1,000 counterfactual scenarios. Identify the 10 scenarios where your current portfolio has the worst drawdown. These are your blind spots.

---

### Agent architectures

**11. The virtual country investment committee**

Create a multi-agent debate system — 4 to 6 specialized Mythos agents that argue about country allocations in structured rounds. Research from November 2025 (Wu et al.) shows that multi-agent debate with heterogeneous agents achieves ~90% correction rates through "productive initial chaos" — genuine disagreement that converges to better decisions. Your agents: a Macro Bull, a Macro Bear, a Quant Factor agent presenting T2 rankings, a Geopolitical Risk agent reading GDELT data, and a Transaction Cost agent vetoing trades that don't clear your Almgren-Chriss hurdle.

*What it unlocks:* An auditable reasoning trace for every allocation decision — you can read the debate transcript and understand exactly why each country was over- or under-weighted. This is something no optimizer gives you.
*Why impossible before:* Previous models couldn't maintain specialized domain reasoning through multi-round debates on complex financial topics. The debate degenerated into agreement after one round.
*First experiment:* Implement a 4-agent debate for a single rebalancing decision. Give each agent access to different data (macro, factors, sentiment, costs). Have them debate the top 5 and bottom 5 countries. Compare the consensus portfolio against your systematic ranking. Track for 6 months.

**12. Adversarial portfolio wargaming**

Borrowed from military operations research: train a "Red Force" agent to find the specific combination of macro shocks that maximally damages your current portfolio. A "Blue Force" agent then adapts allocations to be robust against Red's attacks. Red uses curiosity-driven reinforcement learning to discover **novel** failure modes — combinations you've never stress-tested. Military AI achieves 91% Red Force win rates in tactical scenarios by finding unexpected strategies.

*What it unlocks:* Automated discovery of your portfolio's blind spots, including scenarios no human analyst would think to test.
*Why impossible before:* Setting up the multi-agent RL environment — defining state spaces, reward functions, scenario calibration — requires substantial systems engineering. Mythos at 93.9% SWE-bench can build this end-to-end.
*First experiment:* Simplified version: Blue allocates across 10 countries using your factor signals. Red controls a latent regime variable. Train Red to maximize Blue's drawdown over 100K episodes. Examine which scenarios Red discovers most frequently. These are your real risks.

**13. Country-specialist agent swarm with regional expertise**

Deploy permanent Mythos agents assigned to specific countries or regions. Each agent continuously monitors its assigned countries — reading local news, tracking regime variables, analyzing factor exposures, and updating a "country view" document. When rebalancing time arrives, the swarm reports in simultaneously, and a coordinator agent synthesizes their views into allocation recommendations.

*What it unlocks:* 34-country coverage depth that currently requires a team of human analysts. Each agent maintains persistent context about its countries — political calendars, regulatory pipelines, corporate earnings seasons.
*Why impossible before:* Sustained, reliable autonomous monitoring agents require the long-context and agentic reliability that only Mythos-level capabilities provide.
*First experiment:* Deploy 5 country agents (one each for Japan, Brazil, India, Germany, South Africa) for 3 months. Each produces a weekly report. Compare their risk assessments against your GDELT z-scores and factor signals.

---

### Novel data integration

**14. Satellite-based GDP nowcasting as a country factor**

Night lights intensity predicts quarterly GDP with a 1.55% elasticity in emerging markets. During COVID, satellite-predicted India GDP contraction (-24%) matched actual (-23.9%), beating every investment bank. More importantly, autocratic regimes inflate GDP by 15-30% (Martinez finding) — satellite data detects this. For your EM countries, this is a **fraud detection signal**.

*What it unlocks:* A "true GDP growth" estimate for every country in your universe, available monthly, that detects statistical manipulation by governments. This is alpha in countries where official data lies.
*Why impossible before:* Integrating satellite imagery, cleaning it, extracting signals, and connecting to your equity rotation framework requires an engineering pipeline that Mythos can build autonomously.
*First experiment:* For 10 EM countries, build a monthly signal using VIIRS Black Marble night light data (freely available from NASA). Compare satellite-implied GDP growth vs. official GDP. Where they diverge, test whether the satellite estimate better predicts next-quarter equity returns.

**15. Shipping and port throughput as trade flow nowcasting**

Container port satellite imagery predicts world stock returns (Nature, 2023). For a country rotation strategy, real-time shipping data — container throughput at major ports, ship-tracking data from MarineTraffic — gives you trade flow information weeks before customs data appears.

*What it unlocks:* Real-time trade flow signals for export-dependent countries (Korea, Taiwan, Germany, Chile). When shipping volumes drop before the market knows, you reduce exposure.
*Why impossible before:* Processing satellite imagery and AIS ship-tracking data, cleaning it, and integrating with your T2 framework required custom engineering that wasn't worth the human capital investment.
*First experiment:* Use MarineTraffic or VesselFinder API data for the top 5 export-dependent countries in your universe. Build a monthly "trade flow momentum" signal from container ship counts at major ports. Test as an additive factor in your T2 model.

**16. Google Trends as real-time consumer/macro sentiment**

The OECD Weekly Tracker uses Google Trends with neural networks to nowcast GDP growth across countries. Search terms like "bankruptcies," "economic crisis," "unemployment," and "mortgage" are strong predictors. The European Commission combines GDELT + Google Trends for EU27 country monitoring.

*What it unlocks:* A weekly frequency signal (vs. your monthly T2 rebalancing) that captures consumer distress in real time. Particularly valuable for detecting turning points before they show up in official macro data.
*Why impossible before:* Country-by-country Google Trends data requires language-specific search term selection, seasonal adjustment, and careful normalization. Mythos can handle the multilingual term selection and pipeline construction.
*First experiment:* For 10 countries, pull Google Trends data for "economic crisis" (translated per country). Build a monthly z-score. Test whether extreme readings predict next-month country equity returns, especially at turning points.

---

### Self-improving factor systems

**17. The factor factory with automatic retirement**

Inspired by FactorMiner (February 2026): a self-evolving system that uses the "Ralph Loop" — retrieve relevant knowledge → generate candidate factors → evaluate rigorously → distill lessons into memory. The critical innovation: the system also **retires** decaying factors, detecting when a once-profitable signal has been arbitraged away. Your 53 factors are static. Some are almost certainly dead.

*What it unlocks:* A living factor library that grows when opportunities emerge and shrinks when they disappear. Addresses the "factor zoo" problem — Harvey et al.'s critique that most published factors are false positives.
*Why impossible before:* Autonomous factor discovery that resists p-hacking requires economic regularization (each proposed factor must have a plausible mechanism), strict OOS testing, and the judgment to distinguish signal from noise. Mythos's combined math + coding + reasoning capabilities enable this.
*First experiment:* Give Mythos your 53 factors and their full history. Ask it to: (1) identify the 10 factors with the strongest decay in the last 5 years, (2) propose 10 replacement candidates with economic rationale, (3) backtest the replacements with proper controls, (4) recommend a revised factor library. Compare the revised library's out-of-sample performance.

**18. Meta-research: Mythos auditing your own research history**

Have Mythos study which of your past models worked and why. Feed it your research logs, backtesting results, and model configurations. Ask it to identify patterns: What type of factors decay fastest? Which regime variables are actually predictive vs. noise? Where do your walk-forward results diverge most from in-sample performance? This is the most underappreciated application — **using AI to understand your own decision-making biases**.

*What it unlocks:* Structural insights about your research process — not just your models. Maybe your two-stage funnel is too aggressive at stage 1. Maybe EPU adds noise rather than signal. Maybe factor momentum works for value but not momentum factors.
*Why impossible before:* Required coherent reasoning across your entire research archive — hundreds of experiments, configurations, and results — within a single context. The doubled long-context performance (GraphWalks 80% vs 38.7%) is what makes this tractable.
*First experiment:* Give Mythos your momentum reversal predictor's full history: every walk-forward period, every regime variable configuration, every performance metric. Ask it to identify the single change that would most improve performance. Test it.

---

### Real-time regime intelligence

**19. Continuous regime detection agent**

Replace your static regime variable set (EPU, GPR, BIS, OECD CLI, CDS, term spreads) with a persistent Mythos agent that continuously monitors all of these plus: central bank communications (in native languages), political event calendars, sanction announcements, trade policy changes, and GDELT sentiment shifts. The agent maintains a probabilistic regime estimate (risk-on, risk-off, transition) for each country and the global environment, updating in real time.

*What it unlocks:* Regime detection that responds to events within hours, not at monthly rebalancing frequency. When the Turkey coup attempt happened in 2016, your monthly z-scores took weeks to fully reflect it. A continuous agent would have flagged it from GDELT within minutes.
*Why impossible before:* Required sustained autonomous operation with multimodal monitoring (news text, data feeds, charts) and reliable regime probability estimation. Mythos's extended operation capability (92.1% Terminal-Bench with 4-hour timeouts) and multi-tool orchestration make this viable.
*First experiment:* Run a continuous Mythos agent monitoring GDELT + your regime variables for 5 countries over 3 months. Have it produce hourly regime probability estimates. Compare its regime calls against your monthly regime classifications. Measure how much earlier the continuous agent detects regime transitions.

**20. Financial contagion modeled as epidemic network**

From epidemiology: model your 34 countries as nodes in a network with edges weighted by trade links, banking exposures, and capital flows. "Infection" = crisis or drawdown. Compute a **Financial R₀** — the reproduction number of a crisis in your network. When R₀ > 1 for a crisis cluster, the crisis will spread; de-risk aggressively. When R₀ < 1, buy the recovery. Graph Neural Networks trained on historical crises (Asian 1997, GFC 2008, European debt 2011, COVID 2020) learn the transmission dynamics.

*What it unlocks:* A contagion-aware country allocation model that separates endogenous country risk from contagious network risk — a signal your current framework completely lacks.
*Why impossible before:* Building a GNN-based financial contagion model requires graph architecture code, transmission parameter calibration from sparse crisis data, and interpretation of whether inferred contagion pathways match economic logic. The compound requirement of advanced coding + graph reasoning + domain judgment exceeded previous model capabilities.
*First experiment:* Build a 34-country network using BIS banking statistics and IMF DOTS trade data. Implement a basic SIR-style model where "infection" = MSCI country drawdown > 15%. Train on 1990-2020 crises. Test whether the model's contagion probability improves upon GDELT sentiment for predicting which country falls next.

---

## How your workflow changes

The shift is from **Arjun as researcher using AI tools** to **Arjun as research director supervising AI researchers**. Concretely:

**Today:** You design experiments, write specifications, run LoopPilot, review results, iterate manually. The bottleneck is your time. With 53 factors across 34 countries and 6 regime variables, the combinatorial space of possible experiments vastly exceeds what one person can explore.

**With Mythos:** You describe research programs in natural language ("Investigate whether adding central bank communication hawkishness scores to the momentum reversal predictor improves accuracy, controlling for existing regime variables, using proper walk-forward validation"). Mythos designs the experiments, writes the code, runs the analysis, documents the results, and presents recommendations. You review, challenge, and redirect. **Your role shifts from execution to judgment.**

The practical architecture: a persistent Mythos orchestrator connected via MCP to your IBKR server, GDELT pipeline, T2 parquet files, and research document store. It maintains a research backlog, prioritizes experiments by expected information value, and runs them autonomously. You interact through a research journal that it updates daily.

For GMO specifically: the volume and rigor of research output scales dramatically. What currently takes you months of solo work — testing whether a new factor adds value across 34 countries with proper transaction cost controls — becomes a multi-day automated campaign. This means more ideas tested, faster iteration, and a research audit trail that satisfies institutional due diligence.

---

## Bold speculation: things that sound crazy but might be possible

**Mythos as portfolio manager.** Not co-pilot. Manager. Give it your investment mandate, risk constraints, transaction cost model, and data feeds. Have it manage a paper portfolio for 6 months with full autonomy — generating views, constructing positions, executing rebalances, and writing monthly reports explaining its decisions. If it outperforms your systematic model, you have a philosophical problem. This is probably **18 months away** from being trustworthy enough, but the capability exists today.

**A "world model" for macro.** Climate scientists couple AI emulators of separate physical systems (atmosphere, ocean, land) through shared latent spaces. Build the financial equivalent: separate emulators for monetary dynamics, trade flows, commodity cycles, and political risk, coupled through learned representations. The WOW Project at KIT does this for Earth systems. Nobody has tried it for macro. The technical barrier — building and debugging the coupling architecture — is exactly what Mythos's 93.9% SWE-bench removes.

**Factor investing with zero human-generated hypotheses.** Let Mythos conduct open-ended exploration of your T2 data guided by Bayesian surprise — prioritizing findings that most violate its priors. No starting hypotheses. No factor zoo. Just: "Here is 25 years of country-level data. Find what predicts returns and tell me why." This inverts the entire research paradigm from theory-first to discovery-first. The risk is data mining. The mitigation is Mythos's ability to self-impose economic regularization and critically evaluate its own discoveries.

**Cross-domain causal transfer.** Use Mythos to identify causal structures from climate science, epidemiology, and network science that have unexplored financial analogs. Phase transitions in physical systems may map to market regime switches. Herd immunity thresholds may explain when momentum crashes. Predator-prey dynamics may model the relationship between value and growth factor premia. These sound like metaphors. With formal causal discovery tools and Mythos-level mathematical reasoning, they can be tested as hypotheses.

**Automated essay writing in your voice.** Feed Mythos your published work, GMO white papers, and research memos. Have it draft a quarterly country outlook piece in your analytical style, grounded entirely in autonomous research it conducted on your T2 data and GDELT signals. You edit and publish. Your intellectual output scales by 5-10×.

**Real-time natural-language portfolio construction.** You say: "I'm worried about Turkey's CDS spread widening and want to reduce EM exposure but maintain carry. Don't exceed 50 basis points in transaction costs." Mythos translates this into optimized position changes, checks them against your Almgren-Chriss model with current VIX conditioning, routes orders through IBKR MCP, and provides a full audit trail of the optimization. Voice-to-execution in under a minute, with mathematical rigor you can verify.

**The research desk that never sleeps.** A permanent Mythos installation that integrates your T2 quant signals, GDELT sentiment, central bank communications, satellite data, Google Trends, and breaking news into a unified daily country briefing for all 34 markets. It detects anomalies, flags regime transitions, proposes allocation changes, and writes the investment case — every morning before you open your laptop. This is not one idea. It is the convergence of all 20 ideas above into a single system. It is probably buildable within 12 months of Mythos becoming generally available.