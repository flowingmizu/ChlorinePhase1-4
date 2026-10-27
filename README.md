# Chlorine Breakpoint Lab

**A Mizuverse Labs virtual lab** · *Stay curious. Stay clear.*

An interactive, browser-based virtual lab that teaches water treatment students how the **chlorine demand / breakpoint curve** works. Students add chlorine to a beaker of water and watch what each dose does at the molecular level. Iron rusts, ammonia forms chloramines, chloramines break down into N₂ bubbles, and free chlorine finally kills the microbes. Students then measure the results with a DPD test and build the breakpoint curve from their own data.

🔗 **Live demo:** `https://flowingmizu.github.io/<repo-name>/Chlorine_Breakpoint_Simulator.html`

---

## Who it's for

- Water and wastewater treatment students (community college programs, certificate courses)
- High school science and environmental enrichment programs
- Instructors who want a visual, hands-on demand test without lab chemicals

## Learning flow

Each of the six waters follows the same Mizuverse lab rhythm:

1. **Pre-lab quiz (5 questions):** check what students already know, with explanations and rewards
2. **Virtual lab:** set a dose, add chlorine, watch the beaker, wait out the contact time, run DPD tests
3. **Analysis (5 questions):** *why* questions, *what could the operator do better*, and math using the student's **own lab results**
4. **Next water:** the next scenario unlocks

## Scenarios

| # | Water | Key idea | Analysis math |
|---|---|---|---|
| 1 | Standard surface water | The four phases; free vs total chlorine | Demand, theoretical breakpoint dose |
| 2 | Groundwater well | Long Phase 1 from Fe²⁺, Mn²⁺, H₂S; why aerate first | Phase 1 demand, lbs/day |
| 3 | Spring snowmelt (4 °C) | Cold water slows chloramine destruction; contact time | Demand, CT |
| 4 | Autumn rain (runoff ammonia) | Taller hump; plants stuck in Phase 2 after storms | Breakpoint dose, lbs/day |
| 5 | Summer algae bloom (pH 8.8) | HOCl vs OCl⁻; good residual but weak kill | % HOCl, mg/L of real HOCl |
| 6 | Clean water, no ammonia | No hump without ammonia; why every plant runs its own test | Demand, dose for a target free residual |

## Features

### Virtual lab
- **Animated beaker** where each dot represents 0.1 mg/L of chlorine
  - Fe²⁺ → orange rust · Mn²⁺ → black MnO₂ · H₂S → sulfur
  - NH₃ + chlorine → NH₂Cl (monochloramine)
  - Chloramine destruction → N₂ gas bubbles
  - Free chlorine shown as HOCl (solid) vs OCl⁻ (hollow), split by pH
  - 8 microbes that die only when there is enough strong chlorine
- **Live breakpoint curve** that draws itself next to the beaker as chlorine is added, with phase zones, the peak, and the breakpoint
- **"Where did the chlorine go?"** bar showing chlorine used by reducing agents, used by organics, held as chloramine, destroyed in Phase 3, or left free
- **Two ways to dose:** keep adding chlorine to one beaker to walk through Phases 1→4, or start a fresh sample for each dose like a real bench test
- **Contact time** options (10 / 30 / 60 min) that change the curve shape
- **DPD free and total tests** with pink color vials
- **Lab notebook** with observations, plus a coach that suggests which phase to test next

### Extra modules
- **1 · Build the curve:** enter doses, read DPD results, calculate combined chlorine and demand, then mark the phases on the chart
- **2 · Zone detective:** identify the phase from free/total readings, pH, odor and free ammonia, plus a "which side of the hump?" challenge
- **3 · Calculations:** randomized demand, combined chlorine, Phase 1, peak and breakpoint problems with worked solutions
- **Curve viewer:** an animated reference curve with sliders for ammonia, iron, manganese, H₂S, pH, temperature and contact time

### Gamification
- **My Lab** equipment collection (15 items) earned through quizzes and missions
- Scenario progress with ✓ for complete and ★ for a perfect analysis
- Progress saved in the browser

## Chemistry model

All chemistry lives in one pure-JavaScript object, `ChlorineModel`, which has no DOM access so other sims can reuse it.

| Rule | Value used |
|---|---|
| Phase 1 demand | 0.64·Fe²⁺ + 1.3·Mn²⁺ + 2.1·H₂S + 5.0·NO₂-N (mg/L as Cl₂); Mn reacts slowly below pH 8.5 |
| Combined peak | ≈ 5 : 1 Cl₂ : NH₃-N |
| Breakpoint | 7.6 : 1 theoretical; 8–10 : 1 practical (set per scenario) |
| Phase 3 speed | Temperature- and contact-time-dependent; incomplete destruction shifts the breakpoint higher |
| Free chlorine split | HOCl fraction = 1 / (1 + 10^(pH − 7.5)) |
| DPD | ±0.03 mg/L noise; reading free chlorine late adds a false-high error from monochloramine |

The full list of assumptions is in the **Model assumptions** panel at the bottom of the app.

> ⚠️ **Educational use only.** This is a simplified teaching model. It is not intended for operational dosing or regulatory decisions. Always run a bench demand test on your own water and follow your state and local requirements.

## Running it

No build step and no install.

**Locally:** download `Chlorine_Breakpoint_Simulator.html` and open it in any modern browser.

**On GitHub Pages:**
1. Upload `Chlorine_Breakpoint_Simulator.html` to the repository (rename it to `index.html` if you want it to be the site's home page).
2. Go to **Settings → Pages**, set the source to the `main` branch, root folder.
3. Open `https://flowingmizu.github.io/<repo-name>/`.

An internet connection is needed for Chart.js, which loads from cdnjs. Everything else is inline.

## Tech

- Single self-contained HTML file (HTML + CSS + vanilla JavaScript)
- [Chart.js 4.4.1](https://www.chartjs.org/) for charts
- HTML Canvas for the beaker animation
- `localStorage` for progress (wrapped in try/catch so the app still works from `file://` and in private windows)

### Saved data keys

| Key | Contents |
|---|---|
| `mizuverse.chlorineLab.progress.v1` | Quiz scores, scenario progress, notebook results, equipment |
| `mizuverse.chlorineCurve.v1` | The latest test result (dose, contact time, temperature, pH, free / combined / total, HOCl fraction, phase, microbes killed), saved for the upcoming **Contact Time Lab** |

## Roadmap

- [ ] **Contact Time Lab:** CT and log-inactivation simulator that reads `mizuverse.chlorineCurve.v1` and reuses `ChlorineModel`
- [ ] Troubleshooting scenario: "normal day vs today" log, including decayed sodium hypochlorite
- [ ] Final summary quiz and printable study notes (QR link)
- [ ] Operator mode: plant dosing, chloramination ratio control

## About Mizuverse Labs

Mizuverse Labs builds visual virtual labs, math modules and study infographics for water treatment students, instructors and operators. Other labs in the series include the **Jar Test Simulator**, the **Alkalinity Titration Simulator** and the **Stock Solution Training Simulator**.

## License

© 2026 Mizuverse Labs. All rights reserved.
