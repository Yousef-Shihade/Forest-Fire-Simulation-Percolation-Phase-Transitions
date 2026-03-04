# Stochastic Modeling: Forest Fire Percolation & Phase Transitions

## Project Overview
This project explores the mathematical and computational modeling of **Complex Systems**. Using a 2D Cellular Automaton, we simulate the spread of a forest fire to identify the **percolation threshold** ($p_c$)—the specific tree density at which a localized fire transitions into a system-wide catastrophe. This study highlights how small changes in individual components (tree density) can lead to non-linear, global shifts in system behavior.



## Research Objectives
* **Phase Transition Identification:** Locating the "tipping point" where a forest transitions from a resilient state to a high-contagion state.
* **Finite-Size Scaling:** Analyzing how the grid dimensions ($n$) influence the stability and determinism of the critical threshold ($p_{crit}$).
* **Monte Carlo Estimation:** Using 50+ stochastic trials per density increment to calculate the probability of survival across a continuous spectrum ($0.0 \leq p \leq 1.0$).
* **Resource Optimization:** Calculating the "Optimal Density" that balances forest lushness with fire safety to maximize post-fire tree survival.

## Technical Methodology

### 1. Cellular Automata Rules
The simulation is governed by a set of discrete local rules applied to a 2D lattice:
* **State Space:** Each cell $C(i, j)$ exists in $\Sigma = \{0, 1, 2, 3\}$ representing Empty, Tree, Burning, and Burned.
* **Ignition Logic:** The bottom boundary ($i = n-1$) is ignited to simulate a consistent fire front.
* **Propagation Rule:** For any cell $C(i, j) = 1$, it transitions to state $2$ if any neighbor in the **Von Neumann Neighborhood** ($\text{dist}_L \leq 1$) is in state $2$.


### 2. Scaling Analysis (The Finite-Size Effect)
A central finding of this study is that the critical density ($p_{crit}$) is **not invariant**; it scales with the size of the forest ($n$).
* **Small Grids ($n=25$):** Exhibit high variance and "fuzzy" transitions due to stochastic noise. The "Boundary Effect" dominates, leading to an underestimation of $p_{crit} \approx 0.490$.
* **Large Grids ($n=200$):** Show near-deterministic "Step Function" behavior. As $n \to \infty$, the system behavior converges toward the theoretical percolation threshold for a square lattice ($p \approx 0.5927$).

### 3. Computational Performance: NumPy vs. Native Python
To handle the high-dimensional requirements of $n=500$ grids, the project benchmarks two approaches:
* **NumPy Vectorization:** Utilizes boolean masking and `np.argwhere` to locate active fire fronts, significantly reducing $O(n^2)$ iteration overhead.
* **Native Python:** Implemented as a baseline for logic validation, using list copies to manage state transitions during time-steps.

### 4. Forester's Paradox & Optimization
We identified the "Forester's Paradox": while higher density ($p$) means more trees initially, it also increases "connectivity," facilitating total destruction. 
* **The Sweet Spot:** The simulation identifies a peak in the survival function (typically $p \approx 0.460$) where the forest is dense enough to be lush but sparse enough to act as a natural firebreak.



## Empirical Results Summary
| Grid Size ($n$) | Estimated $p_{crit}$ | Transition Sharpness | Reliability |
| :--- | :--- | :--- | :--- |
| **25** | ~0.490 | Low (Smooth) | Low (Stochastic) |
| **50** | ~0.550 | Moderate | Moderate |
| **100** | ~0.570 | High | High |
| **200** | ~0.580 | Very High (Step) | Convergent |

## Environmental & Practical Implications
The results suggest that in real-world forestry, maintaining a tree density just below the critical threshold is vital. Even a $1-2\%$ increase in density can transform a controllable local fire into a catastrophic event. This model supports the use of **controlled breaks** and **strategic thinning** to manually lower $p$ below $p_{crit}$.

## Technical Stack
* **Language:** Python 3.x
* **Numerical Computing:** NumPy (Matrix state management)
* **Data Visualization:** Matplotlib & Seaborn (Phase transition & optimization plots)
* **Model Type:** Stochastic Cellular Automata

## Project Materials
* **Simulation Notebook:** `Stochastic_Fire_Model.ipynb`
* **Research Presentation:** `Complex_Systems_Final_Slides.pdf`

## Author
**Yousef Shihade & Shada Essawi** | Computational Methods In Statistics B
University of Haifa
