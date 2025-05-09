# Multimodal Sentimental Analysis - Keerthana S

## Motivation - Why did you pick this topic?
I chose the topic of Multimodal Sentiment and Emotion Analysis using the MELD (Multimodal EmotionLines Dataset) because understanding human emotions across multiple modalities—such as speech, text, and visual cues—is crucial for developing emotionally intelligent AI systems. MELD is particularly compelling because it is built on dialogues from the popular TV series Friends, which is rich in expressive interactions, diverse emotional contexts, and realistic conversational flow. This makes it an ideal benchmark for studying real-life emotions and sentiment in a natural, engaging setting. By analyzing data from Friends, the project connects technical research with a culturally relevant and widely understood reference point. Furthermore, building models that can interpret such complex human emotions accurately has immense potential in applications like mental health support, conversational agents, and personalized user experiences.


## How does it connect with past and current work done in Multimodal learning (a short (recent) historical perspective)?
Multimodal learning has evolved rapidly over the past decade, driven by the growing availability of data that combines text, audio, and visual modalities. Early work focused on unimodal sentiment analysis using text (e.g., Twitter sentiment classifiers), but researchers soon recognized that real human communication includes facial expressions, voice tone, and context. Datasets like IEMOCAP and CMU-MOSEI laid the foundation for integrating these modalities. The introduction of MELD, derived from the Friends TV series, marked a significant advancement by providing rich, multi-speaker, context-aware dialogues with aligned modalities. Recent transformer-based architectures such as Multimodal Transformers, MMT, and FLAVA have further enhanced the ability to fuse diverse inputs effectively. Our work builds on these advances by applying and evaluating such models on MELD, bridging the gap between controlled academic datasets and real-world conversational dynamics.

## Learning from This Work
Working on this project has provided deep insights into the complexities and advantages of multimodal learning. One major takeaway is that incorporating multiple modalities—text, audio, and visual—significantly improves the ability to understand human emotions and sentiments in conversations, especially in real-world settings like TV dialogues. By exploring the MELD dataset, derived from the Friends series, I gained hands-on experience with preprocessing heterogeneous data, aligning modalities, and designing models that can capture context across turns and speakers. I also learned that challenges like speaker dependency, sarcasm, and ambiguous emotion expression make real-life emotion recognition much harder than isolated text classification. Furthermore, training models revealed the importance of balancing model complexity with overfitting risk, and I developed skills in evaluating model performance beyond accuracy—using confusion matrices, loss curves, and validation metrics to understand where models struggle. Overall, this work strengthened both my technical proficiency in multimodal machine learning and my appreciation for the nuances of human communication.




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


<img width="412" alt="image" src="https://github.com/user-attachments/assets/5e7f239f-7933-4eab-ab7c-185eddf61fe7" />

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




## What Surprised me?
One of the most surprising aspects of this project was how significantly context and modality influenced emotion recognition accuracy. Initially, I expected that textual information alone would be sufficient for most emotion predictions. However, as I delved deeper, I realized that many emotions expressed in dialogues—especially from the Friends series where sarcasm, humor, and tone play a major role—were nearly impossible to detect accurately from text alone. For instance, the same sentence could express different emotions depending on the speaker’s tone or facial expression. Additionally, I was surprised by how imbalanced the datasets were—certain emotions like "neutral" or "joy" dominated, while others like "disgust" or "fear" were rare, making it harder for the model to learn them well. Lastly, I found it intriguing that even state-of-the-art models like BERT could overfit quickly on small, unbalanced emotion datasets, which highlighted the importance of proper regularization, validation, and careful model selection in emotion recognition tasks.

## What can be the scope for the improvement?
While this project demonstrates the potential of using transformer-based models like BERT for textual emotion classification in dialogue, there is significant scope for enhancement. Firstly, incorporating multimodal data—such as audio tone, facial expressions, and speaker gestures—would drastically improve emotion recognition accuracy, especially in context-rich conversations like those in Friends. Future work could integrate modalities from the MELD dataset beyond text (like audio and video), enabling more nuanced understanding. Secondly, data augmentation techniques could help address class imbalance, particularly for underrepresented emotions like "disgust" and "fear." Model-wise, experimenting with multitask learning or hierarchical models (that consider speaker turns and dialogue context) may better capture dependencies across utterances. Additionally, applying domain adaptation or few-shot learning approaches could help the model generalize better to new dialogue styles or unseen domains. Finally, enhancing real-time performance and interpretability—using tools like LIME or SHAP—would make such systems more robust and useful in real-world applications like mental health analysis, customer service, or virtual agents.


## References
https://affective-meld.github.io/
https://arxiv.org/pdf/1810.02508.pdf
