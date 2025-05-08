# MELD-Emotional-Detection

![image](https://github.com/user-attachments/assets/b1bba304-7ebb-4531-a81a-0250847867a7)
- The **emotion label imbalance** (especially dominance of neutral, joy) should be addressed during training — through class weighting, sampling, or loss adjustments.
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

![image](https://github.com/user-attachments/assets/8e970221-6b29-4482-8d23-bc1e58cbfeb6)
- **Dominant Speakers**: Joey, Chandler, Ross
- **Dominant Emotion/Sentiment**: Neutral (emotion & sentiment)
- **Class Imbalance**: Strong, especially in emotion labels
- **Season/Episode Coverage**: Focused around S4–S5, specific episodes
- **Dialogue Structure**: Fewer utterances toward the end of dialogues


![image](https://github.com/user-attachments/assets/3339d475-ff79-40c4-89d8-cd5ee07ea6d9)
- **Sr No. and Dialogue_ID** are **strongly positively correlated (0.97)**, which makes sense as dialogue IDs likely increase sequentially with row numbers.
- **Utterance_ID** has **very low or near-zero correlation** with most other variables, suggesting that the number of utterances per dialogue varies and is not tied to order, season, or episode.
- **Season and Episode** show a **strong negative correlation (-0.78)**, indicating that higher seasons tend to contain lower episode numbers in this subset, or vice versa—this could be due to selective episode sampling in the test set.
- **Sr No./Dialogue_ID and Season** show **moderate positive correlations (~0.32-0.34)**, meaning rows and dialogues are somewhat aligned with season progression.
- **Episode is negatively correlated** with several features, including Sr No., Dialogue_ID, and Season, highlighting some inverse structuring in how the data is distributed.



<img width="506" alt="image" src="https://github.com/user-attachments/assets/5e7f239f-7933-4eab-ab7c-185eddf61fe7" />
- **Sr No.** shows an even spread, suggesting uniform sampling across the dataset.
- **Utterance (text)** values are all unique or nearly unique, indicated by the flat, low-height histogram. These are specific spoken lines from the dialogues.
- **Speaker** distribution reveals that a few characters dominate the dialogue—such as "Chandler" and "The woman", while others like "Ross" and "Phoebe" appear less frequently.
- **Emotion** is clearly imbalanced, with **'neutral'** being the most common emotion by a large margin, followed by **'happy'**, while emotions like **'sad', 'disgust', and 'anger'** are rare.
- **Sentiment** shows a skew toward **'neutral'**, followed by **'positive'**, and relatively fewer **'negative'** samples.
- **Dialogue_ID** distribution suggests several short dialogues, with a few occurring more frequently.
- **Utterance_ID** indicates that most dialogues consist of a small number of utterances (1–5), with few reaching higher counts.
- **Season** and **Episode** are unevenly distributed; some seasons (e.g., Season 5) and episodes dominate, indicating possible data collection bias or focus on select episodes.
- **StartTime** shows all values are unique or nearly so, reinforcing that each utterance is from a distinct time point in an episode.


<img width="412" alt="image" src="https://github.com/user-attachments/assets/85ceac2c-e155-45db-a38d-58fe384868d2" />

**1. Strong Positive Correlations**:
    - **Sr No. and Dialogue_ID (0.98)**: These two fields are highly correlated, suggesting that dialogue IDs increase almost linearly with the serial number—possibly due to the dataset being ordered by dialogues.
    - **Season and Episode (0.95)**: There's a very strong correlation between the season and episode columns, indicating that episodes are sequentially distributed within seasons and perhaps across the dataset.
    - **Sr No. and Dialogue_ID are also strongly negatively correlated with Season and Episode** (around -0.83 and -0.68 respectively), implying that lower dialogue IDs occur in later seasons/episodes, or vice versa.

**2. Weak or No Correlation**:
    - **Utterance_ID shows very low correlation with all other fields**, implying that the number of utterances per dialogue varies independently and doesn’t follow a strong trend across other features.

**3. Negative Correlations**:
    - **Sr No. and Season (-0.83), and Dialogue_ID and Season (-0.84)**: This could suggest that the data may be ordered such that earlier dialogue IDs and serial numbers are associated with later seasons—possibly due to sorting strategy used during dataset creation.
