# MELD-Emotional-Detection

![image](https://github.com/user-attachments/assets/b1bba304-7ebb-4531-a81a-0250847867a7)
- The emotion label imbalance (especially dominance of neutral, joy) should be addressed during training — through class weighting, sampling, or loss adjustments.
- Utterances are diverse and speaker distribution is skewed (some characters dominate).
- Time-based and meta columns (like Episode, StartTime) can be dropped unless used for advanced modeling.
- Useful for understanding the context depth available in dialogue threads (Dialogue_ID, Utterance_ID).

![image](https://github.com/user-attachments/assets/d85c1788-5325-49c4-bfaf-5b3530d6852d)
| Variable Pair                    | Correlation | Interpretation                                                                                                                                                                                         |
| -------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Sr No. & Dialogue\_ID**        | **0.96**    | Very strong positive correlation — the Sr. No. (index) progresses almost linearly with Dialogue\_ID. This suggests data is sequentially ordered by dialogues.                                          |
| **Sr No. & Episode**             | 0.30        | Moderate positive correlation — Sr. No. slightly increases with episode number, again confirming chronological order.                                                                                  |
| **Dialogue\_ID & Episode**       | 0.35        | Somewhat correlated — higher Dialogue\_IDs tend to be from later episodes.                                                                                                                             |
| **Utterance\_ID & Episode**      | **−0.27**   | Weak negative correlation — utterance IDs tend to slightly decrease with higher episodes. Possibly due to shorter dialogues or fewer turns in later episodes.                                          |
| **Utterance\_ID & Dialogue\_ID** | −0.07       | Negligible/weak correlation — utterance index within a dialogue is not related to dialogue ID (which makes sense).                                                                                     |
| **Season & Others**              | Close to 0  | Very weak or no correlation — seasons are almost uncorrelated with Sr. No., Dialogue\_ID, or Episode. This could be due to interleaved or uneven distribution of scenes across seasons in this subset. |

- **High correlation between Sr. No. and Dialogue_ID** indicates that data rows are mostly ordered by dialogue progression.
- **Season and Episode** are not strongly correlated with most other variables, so you can treat them as **independent categorical/meta features**.
- **Utterance_ID is relatively independent**, which is good — modeling each utterance without strong bias from ordering is possible.
- There are **no redundant features** with perfect correlation (other than Sr. No. vs Dialogue_ID), so dimensionality reduction is optional.

