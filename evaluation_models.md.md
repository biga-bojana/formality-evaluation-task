\# Evaluation report: Formality detection models

\## Overview This project evaluates the ability of different approaches
to detect the formality level of text. The dataset includes examples
from both formal and informal sources, and the models tested include a
fine-tuned classifier, a zero-shot classifier, and an LLM-based
evaluation approach.

\## Dataset The test set was composed of 160 total samples: - 80
\*\*formal\*\* examples from the Enron Email Corpus which I think fairly
represented formal language. - 80 \*\*informal\*\* examples from
DailyDialog and TweetEval (emotion subset)

All samples were labeled as  \`formal\` or \`informal\`.

\## Models Evaluated

\### 1. Fine-tuned Classifier - \*\*Model:\*\*
\`LenDigLearn/formality-classifier-mdeberta-v3-base\` - \*\*Type:\*\*
Text classification - \*\*Label handling:\*\* Remapped \`neutral\`
predictions to \`formal\` I was trying to keep same  binary 2 label
consistency across all models, I tried it first with 3 labels(formal,
informal, neutral)  but the results were ambiguous in the confusion
matrix.

\### 2. Zero-shot Classifier - \*\*Model:\*\*
\`MoritzLaurer/deberta-v3-base-zeroshot-v2.0\` - \*\*Type:\*\* Zero-shot
classification using candidate labels: \`formal\`, \`informal\`

\### 3. LLM-as-a-Judge - \*\*Model:\*\* \`tiiuae/falcon-7b-instruct\` -
\*\*Type:\*\* Text generation used to verify model predictions -
\*\*Method:\*\* Prompted to respond with \"Correct\" or \"Incorrect\"
for each prediction

\## Evaluation Metrics - Accuracy - Precision / Recall / F1 (via
classification report) - Confusion matrix

\## Results Summary

\| Model \| Accuracy \| Notes \|
\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\--\|\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--\|
\| Fine-tuned DeBERTa \| 0.91 \| Strong performance \| \| Zero-shot
DeBERTa ZS \| \~0.73 \| Weaker on informal expressions \| \|
LLM-as-a-Judge \| -- \| Used for spot-checking \|

\## Observations - The fine-tuned model performed the best overall, with
strong accuracy and balanced classification. - The zero-shot model
handled many formal examples well but was less consistent on informal
and ambiguous cases. - LLM-as-a-Judge provided helpful qualitative
feedback on borderline examples.

\## Challenges - Finding large open datasets labeled for formality was
difficult; GYAFC corpus required permission that took a long time to
get. - Zero-shot models require careful candidate label phrasing. - Some
informal data (like tweets) can be ambiguous even for humans. - I tried
to include a 4th model rule based heuristic one, but I think it was
unnecessary for this task because  my model would need to include a lot
of informal words and I feel it would be an overkill for this task.
Because I was not woried about performance and computation data I used
already fined tuned models,  instead of maybe more light weight rule
based but one.

\## Possible next steps and improvement - Evaluate on longer documents
or structured messages. - Introduce a third class (neutral) and revisit
classification schema. - Use human-labeled gold standard data for more
reliable LLM judgment evaluation. -Try on languages other than English.

\-\--
