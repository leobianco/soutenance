# Second year presentation

The goal is just to present the problem that you are currently working on.

## (5min) Part I: Introduction and previous work

### The problem of robust estimation (1m)

Samples $X_1, ..., X_n \sim p_\theta$ => "Adversary" *perturbs* samples into $\tilde{X}_1, ...,\tilde{X}_n$ => propose $\hat{\theta} = f(\tilde{X}_1, ..., \tilde{X}_n)$ s.t. $d(\hat{\theta}, \theta) -> 0$ w.h.p.

Motivation: find estimators that do not crucially depend on the assumption that the data comes *exactly* from the generative model (deal with mispecification).

### Some perturbation models (0.5m)

- Huber contamination: sample from the mixture model $(1-\gamma) p_\theta + \gamma q$, where $q$ is a different density.
- Strong contamination model: replace a fraction $\gamma n$ of nodes arbitrarily. May be adversarial on the sample.
- Many other types: oblivious contamination model: add a number of arbitrary nodes *before* seing the sample.
  etc.

### Previous work on robust statistics (1m)

- 70s: Huber et al. established minimax rates for their model.
- Problem of *efficient* robust estimation of the mean of a gaussian in high dimensions (strong contamination) remained open. => robust =/= efficient.
- 2019: robust gaussian mean estimation solved by filtering or convex optimisation.
- 2021: gaussian mixture models.
- 2021: Acharya proposes a *filtering* approach to estimate the parameter of an $ER(p)$.

### Previous work on SBM (2m)

- You have $n$ nodes belonging to $K$ communities, and you connect nodes from the same community with probability $p$ and nodes from different communities with probability $q$.
- (Uncorrupted) SBM: 2010s => density thresholds for different tasks.
- Non-rigorous SBMs: modularity
- Rigorous SBMs: variational methods (Bickel), spectral methods (Laplacian, Non-backtracking matrix), SDP methods.
- Key idea in robustness for random graphs: spectral methods are faster but generally fail, while SDPs are slower but provably robust.
- Spectral robustness: Stephan / Massoulié approach can only take up a negligible amount of perturbation.
- Success of SDPs: Cai pioneer work classifies the inliers well; Moitra's SDP essentially achieves the minimax rates of the uncorrupted case. Tommaso proposed an SDP based on the Sum-of-Squares technique that is robust to node or edge corruptions.

### Our question (0.5m)

- Point #1: these approaches **require knowledge of the true parameters** to work.
- Point #2: these approaches are **not doable** in practice.

=> Can we also *efficiently* and *robustly* *estimate* the connectivity parameters?

## (10min) Part 2: Our approach

### (3min) The filtering method

CITE DIAKONIKOLAS

- 1st intuition from gaussian case: the only way that outliers can deviate the mean is by grouping together at some region of the sphere.
- 2nd intuition from gaussian case: outliers in random directions do not affect the mean and become impossible to detect => instead of focusing on finding *all* outliers we focus on finding *bad* outliers.
  Their proposed method: filtering.

### (3min) Acharya

Acharya took this idea and procceeded in a similar way: focus on finding nodes that make the spectral norm deviate.

Estimation bound

Algorithm for reducing the norm.

### (4min) Our approach

Our case: similar idea, but now *misclassified* nodes, besides outliers, can also bring the spectral norm up.

Estimation bound

Algorithm proposed

Problem: initialization must not be too bad => good clustering algorithm => requires parameters! "Solution": using Cai.
Problem: re-clustering at each step can be expensive. "Solution": ignore this for a moment.
Real problem: lowering spectral norm (removing misclassified nodes may introduce new misclassifications)
Real problem: even if the proof works, this algorithm will be slow.

Future directions:

* Speeding-up: using simulated annealing or other approximate solution techniques?
* Control of the spectral norm: Sum-of-Squares type proof.
