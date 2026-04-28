# Ecosystem Population Dynamics Simulation
### A 7-species food-web extension of the Lotka–Volterra predator–prey model

Modelling how 7 trophic groups — **Plants, Herbivores, Omnivores, Carnivores, Scavengers, Saprophages, and Decomposers** — interact and stabilise (or oscillate) over time, by extending the classical 2-species Lotka–Volterra equations into a coupled system of 7 ODEs.

> Group academic project at **Hochschule Rhein-Waal** (Rhine-Waal University of Applied Sciences), supervised by **Prof. Dr. Frank Zimmer**, January 2025. Coursework later credited at Fachhochschule Südwestfalen.

---

## The question

The original Lotka–Volterra model has only two species (predator and prey). Real ecosystems don't. We wanted to know:

- What happens to predator–prey oscillations once you add **5 more trophic levels** that all interact with each other?
- Do the classic closed-orbit phase diagrams survive, or break?
- Which species dominate the system, and which become quietly essential?

## The model

Seven coupled ordinary differential equations, one per species. Each equation combines a **growth term** (food consumed), one or more **loss terms** (being eaten or decomposed), and an **intraspecific competition** term (`–x·N²`) that prevents unbounded growth. ~30 rate constants in total.

Solved numerically with `scipy.integrate.odeint` over `t ∈ [0, 500]` (2000 time-steps), starting from populations `[300, 250, 200, 100, 200, 400, 350]` (Plants → Decomposers).

The full equations and parameter table are in [`ecosystem.pdf`](./ecosystem.pdf).

## What we found

*(See `ecosystem.ipynb` for all 8 figures — GitHub renders the notebook in-browser.)*

- **Plants, herbivores and carnivores oscillate together** in classic predator–prey saw-tooth cycles — adding 4 extra species didn't break the core predator–prey rhythm.
- **Decomposers spike very early, then sync up** with the plant–herbivore–carnivore cycle once organic material from die-offs becomes available.
- **Omnivores, scavengers and saprophages decouple** from the main rhythm — these "in-between" trophic roles act as buffers rather than amplifiers.
- The **Plants vs Herbivores** phase diagram (Figure 4) shows the textbook closed-orbit cycle — confirming the classical Lotka–Volterra dynamic still holds for that pair even inside the larger system.
- The **Decomposers vs Saprophages** phase diagram is the most non-standard — a long sweep rather than a closed orbit, hinting at a slower nutrient-cycling regime layered underneath the faster predator–prey one.

In total the project produces **8 figures**: 1 combined population-vs-time chart and 7 phase diagrams (Plants↔Herbivores, Herbivores↔Carnivores, Omnivores↔Carnivores, Omnivores↔Herbivores, Decomposers↔Saprophages, Scavengers↔Saprophages, Plants↔Carnivores).

## Limitations (and what we'd do next)

- **No real ecological data fitted.** All ~30 rate constants are chosen by hand. The model demonstrates *qualitative* behaviour, not quantitative predictions for any specific ecosystem.
- **No sensitivity analysis.** A natural next step is to vary each parameter ±20% and see which ones the system is fragile to — this would identify which species/relationships are "load-bearing".
- **No stochasticity.** Real populations face random shocks (disease, weather). Adding noise terms and re-running would test whether the oscillations are robust or knife-edge.

## Run it yourself

```bash
git clone https://github.com/Pritom-byte/ecosystem-population-dynamics-simulation.git
cd ecosystem-population-dynamics-simulation
pip install -r requirements.txt
jupyter notebook ecosystem.ipynb
```

Then open `ecosystem.ipynb` and run all cells.

## Files

| File | Contents |
|---|---|
| `ecosystem.ipynb` | The simulation — all parameters, equations, and 8 plots. |
| `ecosystem.pdf` | Full 15-page write-up: introduction, derivation of all 7 equations, parameter table, results discussion, references. |
| `requirements.txt` | `numpy`, `scipy`, `matplotlib`. |

## Built with

`Python` · `NumPy` · `SciPy` (`odeint`) · `matplotlib` · `Jupyter`

## Authors

- **Pritom Mazumder** — [GitHub](https://github.com/Pritom-byte) · [LinkedIn](https://www.linkedin.com/in/pritxm/)
- **Dip Dutta**
- **Kaushik Shankar Roy**

Supervised by **Prof. Dr. Frank Zimmer**, Hochschule Rhein-Waal, January 2025.

## References

13 references in `ecosystem.pdf` — Lotka (1925), Volterra (1926), Wangersky (1978), Hsu/Ruan/Yang (2015), Wang & Zou (2020), and others on Lotka–Volterra extensions, food-web modelling, and decomposer–producer interactions.
