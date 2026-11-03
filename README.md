# econ5200-lab10-causal-logic

# Causal Logic and DAGs: Diagnosing Bad Controls

## Objective

I used directed acyclic graphs (DAGs) to show when adding a control variable to a regression fixes an estimate and when it makes the estimate worse.

## Methodology

- Ran a regression with a control caused by both the treatment and the outcome (a collider) and compared the estimate and R-squared with and without it. The true effect was zero.
- Tested whether a control measured before treatment can still bias the estimate. The true effect was zero.
- Separated a total effect from a direct effect through a mediator, using simulated data with a true total effect of 4.0 and a true direct effect of 1.0.
- Compared the LaLonde job-training experiment's benchmark with an observational estimate built from CPS controls, before and after covariate adjustment.
- Used a `dag_utils.py` module that finds valid adjustment sets from a DAG.
- Asked an AI to propose controls for a job-training study and checked its set against the study's DAG. I revised my prompt once and checked the new set the same way.
- <!-- Delete this bullet if you skipped the Extension --> Tested how strong an unobserved confounder would need to be to change my estimate.

## Key Findings

| Analysis | Result | Truth |
|---|---|---|
| Collider control | Estimate moved from -0.012 to -0.593; R-squared rose to 0.585 | 0 |
| Pre-treatment control | -0.201 | 0 |
| Total effect (mediator) | -0.004	 | 4.0 |
| Direct effect (mediator) | 1.0 | 1.0 |
| LaLonde, observational with CPS controls | $-8,498 before adjustment, $699 after | Experimental benchmark: $1,794 |
| AI-proposed controls, first set | 3.622 | 4.0 |
| AI-proposed controls, revised prompt | 4.047 | 4.0 |

- **Collider:** Adding the collider raised R-squared even though the true effect was zero, so a higher R-squared did not mean a better model.
- **Pre-treatment control:** A control measured before treatment still biased the estimate. Being measured earlier does not make a variable a safe control.
- **Mediator:** The total effect and the direct effect differ, and which one I get depends on whether I control for the mediator.
- **AI-proposed controls:** I checked the AI's suggestions against the DAG instead of trusting them.
