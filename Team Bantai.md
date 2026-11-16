# Metrica Sports - More Than a Hack 2027
## Football Possession Classification

### 1. Project objective
Predict the possession state for every frame of the Barcelona vs Athletic Club match.

Labels:
- H = Home team possession
- A = Away team possession
- D = Dead ball
- X = Other / unresolved state

### 2. Final candidate
File: Team Bantai.csv

- Total frames: 199,319
- Frame numbering: 0 to 199,318
- Columns: frame, label
- Official format validator: Passed

SHA256:
D444CAA1AEBB6FB58386033A5967C83302B8DD984EA91C86381BF208332702FF

### 3. Prediction method
The final candidate uses the official Metrica rule-based baseline with a smoothing half-window of 50 frames.

The method:
1. Reads the match tracking data and team metadata.
2. Identifies the tracked player nearest to the ball.
3. Assigns possession to that player's team.
4. Assigns D when the ball or a usable player assignment is unavailable.
5. Applies a centered majority-vote smoothing window with a 50-frame half-window (101 frames total).
6. Resolves ties according to the official baseline implementation.

No Random Forest model or learned probability threshold is used to generate this candidate.

### 4. Final label counts
- H: 72,957 (36.6%)
- A: 54,842 (27.5%)
- D: 71,520 (35.9%)
- X: 0 (0.0%)
- Total: 199,319

### 5. Reproduction command
Run from the project root:

python starter/baseline.py --window 50 --out results/final_candidate

Expected output file:

results/final_candidate/baseline_smooth50.csv

Copy that generated file to Team Bantai.csv to prepare the root-level submission file.

### 6. Validation
Command:

python evaluation/validate_submission.py Team Bantai.csv

The official validator reported:
- 199,319 rows
- Frame range 0 to 199,318
- Valid label values
- 669 reported possessions
- Mean possession duration: 7.6 seconds

This is a format check only. It does not establish prediction accuracy.

### 7. Development transparency and ground-truth use
Earlier exploratory development included Random Forest and hybrid experiments that used labels from the public five-minute ground-truth file. Those experiments and their outputs are excluded from this final candidate.

The submitted CSV is generated using the rule-based official Smooth50 baseline, not the Random Forest or hybrid workflow.

Public ground truth was used during earlier exploratory development. This history is disclosed here; the final candidate's eligibility should be confirmed with the organisers. No claim of full-match ground-truth evaluation is made.

### 8. Limitations
- The method depends on the available tracking data and ball visibility.
- Missing ball information can result in D predictions.
- The baseline does not explicitly model passes, tackles, or match context.
- Format validation does not measure prediction accuracy.
- No full-match ground-truth score is claimed.

### 9. Relevant source files
- starter/baseline.py
- evaluation/validate_submission.py
- Team Bantai.csv

### 10. Data and repository note
Do not publish match video, tracking files, tactical data, derived match data, or other restricted challenge data in the public source repository. Follow the official challenge submission instructions.

