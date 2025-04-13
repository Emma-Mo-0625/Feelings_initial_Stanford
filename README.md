# Feelings_initial_Stanford

## Dataset Overview:
Emotional response data from 156 participants across 105 trials each. 

- The participants were shown various emotional images (negative, neutral, and positive)

- Their emotional responses were recorded for three different measures: Negative Emotional Response (Ineg), Positive Emotional Response (Ipos), and Arousal Response (Iaro).

## Data Structure:
- `dat`: A long-format dataset with 16,380 (156x105) observations and 9 variables.

- Each row represents a single observation of a participant's emotional response to a specific trial.

## Datasets:

`dat`:

- subj: Participant ID (156 unique participants).

- trial.num: Trial number (1 to 105).

- trial.val: Trial type (Negative, Neutral, Positive emotional images).

- sex: Participant's gender (Male, Female, Other).

- age: Participant's age.

- ethn: Participant's ethnicity.

- Ineg: Negative Emotional Response to the image (numerical score).

- Ipos: Positive Emotional Response to the image (numerical score).

- Iaro: Arousal Response to the image (numerical score).


`Iaro_wide, Ineg_wide, Ipos_wide` (wide-format datasets)

- Each with 156 participants across 105 trial conditions. 

- Ineg_wide: Contains Negative Emotional Response (Ineg) scores for all participants across the 106 trials.

- Ipos_wide: Contains Positive Emotional Response (Ipos) scores for all participants across the 106 trials.

- Iaro_wide: Contains Arousal Response (Iaro) scores for all participants across the 106 trials.

## Data Usage:

Explore how participants respond emotionally to various stimuli (negative, positive, neutral images) and to compare these responses across different trials and participant characteristics (e.g., gender, age, ethnicity).

Perform statistical analyses (e.g., ANOVA, regression analysis) to identify patterns and differences in emotional responses based on the trial type or participant demographics.

