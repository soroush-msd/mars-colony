# Terraforming Mars: Maximizing the Greenhouse Effect with Optimization

> Humanity's last stand isn't on Earth... it's on Mars.

---

## The Scenario: Year 4043

Earth is toast, quite literally. Centuries of pollution, overconsumption, and climate collapse have left our planet scorched and unlivable. The air is toxic. Crops have failed. Civilization? Hanging by a thread.

But all hope isn’t lost.

SpaceZ, the last functioning aerospace company, has one shot left. A bold mission to terraform Mars using every ounce of remaining knowledge and tech on Earth.

The mission is to generate enough greenhouse gases to warm the Red Planet and create a livable atmosphere fast.

<p align="center">
  <img src="https://github.com/user-attachments/assets/715ac1f2-9a6f-427a-aa73-bc4125ab75a7" alt="Mars Terraforming Stages" width="500"/>
  <br>
</p>

---

## Project Goal

This project uses **mathematical optimization** to **maximize the greenhouse effect** on Mars.

We simulate 100 different **terraforming processes** and calculate their impact on 5 key **greenhouse gases**, subject to 10 limited **resources** (like energy, water, and materials). Our goal: run these processes at optimal levels to **maximize atmospheric warming** while **respecting resource constraints** and maintaining a balanced gas mix.

---

## Optimization Formulation

We frame the problem as a **Linear Programming (LP)** model:

### Sets
- `I = {1,...,100}`: Terraforming stations/processes
- `J = {1,...,5}`: Greenhouse gases (e.g. CO₂, CH₄, N₂O, H₂O vapor, CF₄)
- `K = {1,...,10}`: Limited planetary resources

### Decision Variable
- `x_i`: Operation level (0 to 1) of each process `i`

### Objective Function
Maximize:
Z = ∑(i ∈ I) ∑(j ∈ J) g_ij * e_j * x_i

Where:
- `g_ij`: Amount of gas `j` produced by process `i`
- `e_j`: Effectiveness (warming potential) of gas `j`
- `x_i`: Operation level of process `i`

### Constraints
1. **Resource limits**: Total usage across all processes can't exceed the available supply of each resource.
2. **Operational bounds**: Each process has a minimum and maximum capacity.
3. **Gas balance**: Each type of gas must represent at least 10% of total gas production (we don’t want a one-gas atmosphere!)
4. **Non-negativity**: Operation levels can’t be negative.

> **Note**: To focus on model design and optimization logic, all parameters (gas production rates, resource availability, effectiveness scores, etc.) are synthetically generated using seeded random functions.

---

## Tools & Tech
- **Python**
- **[Pyomo](http://www.pyomo.org/)** for optimization modeling
- **GLPK** solver for solving the LP
- **NumPy & Pandas** for data handling

---

## Interpretation & Insights

After solving the model, we found:

- The optimization **maximized the total greenhouse effect** to an impressive value.
- Some processes (e.g., Process 16, 17, and 18) operated at nearly full capacity, clearly more effective or efficient.
- Certain resources (like Resource 3, 4, and 9) were fully utilized, these are **bottlenecks** limiting expansion.
- Some greenhouse gases were more dominant than others, but the **balance constraints** ensured a healthy atmospheric mix.
- **Sensitivity analysis** using **dual values** revealed which resources had the biggest impact on the final outcome, these are prime targets for scaling in future missions.

---

## Optimization Concepts Used

- **Linear Programming (LP)**: At the core of our mission, LP helps us decide how much each terraforming station should operate, given limited resources. It’s the perfect tool to handle continuous decisions with linear constraints and objectives.

- **Resource Allocation**: Mars isn’t generous, every drop of water, joule of energy, and scrap of material must be used wisely. We use optimization to distribute these limited planetary resources across competing processes for maximum atmospheric gain.

- **Balance Constraints**: Our model enforces a diverse mix of greenhouse gases, requiring each to contribute at least 10% to the total effect. This promotes long-term atmospheric stability (and a more Earth-like vibe).

- **Sensitivity Analysis (Duality)**: By analyzing dual variables, we uncover which constraints are most binding. If increasing a resource (like energy) leads to a higher objective value, it’s a critical bottleneck. These "shadow prices" guide strategic upgrades.

- **Dual Problem & Strong Duality**: For every optimization problem (the primal), there’s a corresponding dual. Solving both confirms that the optimal values match (Strong Duality), giving us confidence in the solution’s validity and uncovering deeper insights into constraint tightness.

- **Integer Programming (IP)**: In a more advanced mission phase, we introduce **binary or integer constraints**. For example, making a process all-or-nothing. This transforms the problem into a Mixed-Integer Linear Program (MILP), which is more realistic in some cases, but also harder to solve.

- **Relaxation**: To understand the trade-offs of using integer decisions, we relax them back to continuous variables and compare the outcomes. This shows how much "flexibility" we lose (or gain) when committing to binary decisions in our plan.

- **Parametric Sensitivity Analysis**: What happens if we tweak a single parameter, say, we increase the available solar energy? We rerun the model with 10–20 variations and track how the objective changes. This helps us understand which factors are game-changers for terraforming success.

---

## Future Work

- Add cost functions and budget trade-offs.
- Introduce time dynamics: what if we simulate year-by-year terraforming?
- Add uncertainty: what if some processes fail or some resources fluctuate?
- Improve with visualizations: heatmaps of resource usage, graphs of gas composition, etc.
