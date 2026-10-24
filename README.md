# Student Exam Score Prediction (Linear Regression)

Predicting exam scores from study hours and other factors, using the Kaggle
[Student Performance Factors](https://www.kaggle.com/datasets/lainguyn123/student-performance-factors)
dataset (6,607 students).

## What I did
- Cleaned the data: removed 1 row with an impossible score (101 on a 0-100 scale)
- Explored distributions and the hours vs. score relationship
- 80/20 train/test split (random_state=42)
- Compared four models: Hours-only linear, degree-2 polynomial,
  4 numeric features, and all features (categoricals one-hot encoded)

## Results (test set)
| Model | MAE | RMSE | R² |
|---|---|---|---|
| Linear (Hours only) | 2.419 | 3.156 | 0.247 |
| Polynomial (deg 2) | 2.415 | 3.154 | 0.248 |
| Hours + Sleep + Attendance + Physical Activity | 1.422 | 2.226 | 0.625 |
| All features | 0.478 | 2.041 | 0.734 |

Hours-only equation: Score = 61.5 + 0.286 × Hours_Studied

## Key takeaways
- Hours studied alone explains ~25% of score variance. Each extra hour
  is associated with ~0.29 more points.
- Polynomial regression added almost nothing: the relationship is
  essentially linear.
- Adding Attendance gives the biggest jump. Sleep contributes very little.
- With all features, typical error is under 0.5 points (MAE). RMSE is much
  higher (2.04) because of a few students (~0.6% of the test set) whose
  scores the model badly under-predicts. Nothing in their other columns
  explains it, so I kept them in the reported results.
- These are associations in one (likely synthetic) dataset, not proof
  that any factor causes higher scores.

## Files
- `student_exam_score_prediction.ipynb`: full analysis
- `requirements.txt`: libraries used

## How to run
1. Download `StudentPerformanceFactors.csv` from the Kaggle link above
   and put it in the same folder as the notebook.
2. `pip install -r requirements.txt`
3. Open the notebook and run all cells.

## Next steps
Cross-validation, a tree-based model for comparison, and investigating
the unexplained high scorers.
