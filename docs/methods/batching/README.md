# Batching independent retrievals

## Method

Fetch several small, known-needed facts in one tool/model request when the results are independent. This can reduce round trips and repeated fixed prompt overhead.

## Caution

Do not batch unrelated large files or multi-step work into one giant context. Larger batches may overflow context or force a strong model to process irrelevant material.
