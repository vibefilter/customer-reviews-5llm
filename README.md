---
license: cc-by-4.0
language:
  - en
pretty_name: Customer Reviews by Five Language Models
size_categories:
  - 1K<n<10K
task_categories:
  - text-classification
tags:
  - customer-reviews
  - sentiment
  - synthetic
  - llm-generated
  - evaluation
configs:
  - config_name: default
    data_files: data/reviews.jsonl
---

# Customer Reviews by Five Language Models

1000 fictional customer reviews for a fictional online shop, written by five language models: Claude, ChatGPT, Gemini, Grok and Mistral. Each review is labelled by topic and mood by the model that wrote it.

The set was made as test data for [Vibefilter](https://github.com/vibefilter/filament), a Filament plugin that filters tables by a plain-English statement, and it is the data behind its demo. It is useful anywhere you need realistic, varied, labelled review text: testing classifiers, comparing models, or filling a demo app.

> **Note on use.** The reviews were generated with Claude, ChatGPT, Gemini, Grok and Mistral. Outputs of these services may be subject to their providers' terms of use. The dataset is intended for testing, evaluation and demos; please check those terms before using it to train models.

## Files

| File | What it is |
|---|---|
| `data/reviews.jsonl` | the 1000 reviews, one JSON object per line |
| `data/reviews.csv` | the same data as CSV |
| `prompt/review-prompt-v4.md` | the final version of the prompt the models were given |

## Fields

| Field | Type | Meaning |
|---|---|---|
| `id` | integer | 1–1000 |
| `text` | string | the review |
| `product` | string or null | the product the review is about; null when it names none |
| `topic` | string | what the review is mainly about: `shipping`, `support`, `bug`, `price`, `quality`, `feature_request` |
| `mood` | string | the author's tone: `angry`, `neutral`, `satisfied` |
| `model` | string | which model wrote it: `claude`, `chatgpt`, `gemini`, `grok`, `mistral` |
| `batch` | integer | the generation batch (1–24), each run in a new chat |

Example:

```json
{"id": 1, "text": "Arrived two days later than promised, but the box was intact and everything inside was fine.", "product": "Nova X2 blender", "topic": "shipping", "mood": "neutral", "model": "chatgpt", "batch": 1}
```

## What's in it

| Model | Reviews |
|---|---|
| Mistral | 216 |
| Grok | 215 |
| Claude | 215 |
| Gemini | 206 |
| ChatGPT | 148 |

- **Moods:** angry 322, neutral 347, satisfied 331.
- **Topics:** quality 183, price 175, shipping 167, feature request 164, support 163, bug 148.
- **Products:** six physical products (Nova X2 blender, Echo Mini speaker, Lift standing desk, Burr coffee grinder, Glow smart lamp, Pace running watch), three apps (mobile app, web dashboard, desktop app) and a Pro subscription. 230 reviews name no product.
- **Hard cases on purpose:** sarcasm ("Great job team, the desktop app just ate my unsaved filter set. Love losing twenty minutes of work :)"), happy ALL CAPS, polite complaints, reviews touching two topics, typos and non-native English.

The shop, its products and all customers are made up. Reviews that mentioned real people, brands or places were removed.

## How it was made

- **Prompt.** One prompt describes the shop, the six topics and three moods with labelling rules, and asks for 50 reviews per run as JSON Lines. It went through four versions: v1 quoted example sentences, which every model copied; v2 and v3 replaced them with rules and a growing list of overused ideas to avoid; v4 added a stricter ban on real names. The final version is in `prompt/`.
- **Models.** All five were used through their chat apps, one batch of 50 per run, always in a new chat. Claude ran as Claude Opus 5.5 (medium effort); ChatGPT on the free plan's default model; Gemini as 3.6 Flash; Grok in Expert mode; Mistral in the Le Chat app ("Work" mode). Where the app doesn't show the exact model version, it is not known.
- **Collection.** 24 batches, 1223 raw reviews (Grok 300, Mistral 271, Claude 250, Gemini 250, ChatGPT 152), collected on 2026-09-28.
- **Checks after every batch:** valid JSON and label values, no software product in a shipping or quality review, exact and near duplicates, style statistics.
- **Selection to 1000,** without looking at any classifier's answers, so the hard cases stayed in: every review with a real name (19) or a logical error (14) was removed, then 45 near-duplicates, then 145 random cuts that kept the models, topics and moods balanced. Nothing was edited by hand.

### The models write differently

Claude writes long, messy, human-sounding reviews with lowercase, CAPS and emoji. Grok is terse and blunt. ChatGPT writes tidy, customer-service-like sentences and labels mild complaints as angry. Gemini is uniform and tends to repeat itself. Mistral writes long, detailed reviews and sometimes labels clearly upset customers `neutral`. Mixing them gives a set that reads as if many different people wrote it.

## The labels are not ground truth

Each label is the opinion of the model that wrote the review. No label was changed. Many reviews are genuinely ambiguous ("Took 9 days instead of 3–5. Works fine though." — neutral or satisfied?), and two people would disagree on them too. Treat the labels as one rater's view.

As a reference point, TypeSafe's Jev model (`jev-1.13.0`) was run on all 1000 reviews as a second, independent rater:

| | Agreement with the labels |
|---|---|
| Topic | 980 / 1000 |
| Mood, threshold 0.6 | 833 / 1000 |
| Mood, threshold 0.7 | 847 / 1000 |
| Mood, threshold 0.8 | 861 / 1000 |

Angry and satisfied were never swapped. Most disagreements sit on the line between neutral and mildly satisfied. Mood agreement by writer at 0.7: Claude 93%, Grok 88%, Gemini 82%, Mistral 80%, ChatGPT 79%. These are agreement figures between two raters, not accuracy.

## License

The dataset is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Please see the note on use above.

## Citation

```
Horváth, András (2026). Customer Reviews by Five Language Models. https://github.com/vibefilter/customer-reviews-5llm
```
