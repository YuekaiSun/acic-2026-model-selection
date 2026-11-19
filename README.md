# Choosing treatment-effect models before the truth is known

**Yuekai Sun · 2026 ACIC Data Challenge · Curated track**

Each participant in the benchmark received one of five randomized treatments. Our team had to estimate four effects relative to control and recommend an active treatment for each participant. The organizers released the true effects after submission.

[Read the executed notebook](ACIC_2026_Model_Selection.ipynb)

The notebook follows one dataset from observed outcomes to the eight submission files. Screening on held-out outcome predictions reduced 12 regressions to five final models. Taking the best nuisance regression in each of three clusters reduced the doubly robust grid from 25 to 15 pairs. We compared the resulting 30 causal learners on simulated trials and selected ensembles separately for squared effect error and treatment regret.

The historical run retained 12 learners for effect estimation and 11 for treatment choice on dataset 1. Across all 18 datasets, the frozen submission had mean conditional-effect RMSE 0.618 and mean active-arm regret 0.057 outcome units. Each dataset carries equal weight in these means.

## Run the notebook

Use Python 3.9 and run these commands from the repository root.

```sh
python -m pip install -r requirements.txt
python -m notebook ACIC_2026_Model_Selection.ipynb
```

**Run All** screens the full outcome library on dataset 1, runs a small fit spanning the S-, T-, X- and doubly robust families, and evaluates all 18 archived submissions. The small fit uses one plasmode and 30 out-of-bag bootstrap draws to illustrate the export.
The notebook also shows how to refit all datasets with 15 plasmodes, five-fold predictions, and 200 out-of-bag bootstrap draws per dataset.
These settings follow the restored paper implementation.
The exact historical environment and frozen-output generator remain unverified.
Reported competition metrics use the saved predictions and treatment recommendations.

## Data and methods

- `data/curated_data.zip` contains the 18 observed trial CSVs from the organizers’ Curated track.
- `data/members.csv` and `data/rankings.csv` contain ensemble membership and the top five learners per loss from the recorded team run.
- `data/submission.csv.gz` and `data/recommendations.csv.gz` contain the individual contrasts and active-arm choices from team submission 0002_03. `data/released.csv.gz` contains the corresponding organizer-released contrasts.

The challenge design is described by Perrett, Deshpande and Hill in *More Treatments More Problems: Designing the 2026 American Causal Inference Conference Data Challenge*.
