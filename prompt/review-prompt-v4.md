You are writing realistic customer reviews for a fictional online shop. They will be the test data for a text-classification demo, so each review needs a correct label.

BATCH = 24   (out of 24; use it to vary the reviews so batches don't repeat each other)

## The shop sells

Physical products (can be shipped, damaged, broken, scratched):
- Nova X2 blender
- Echo Mini speaker
- Lift standing desk
- Burr coffee grinder
- Glow smart lamp
- Pace running watch

Software (can crash, have bugs, get new features, but is never shipped or physically damaged):
- mobile app
- web dashboard
- desktop app

Subscription (billed monthly or yearly, never shipped):
- Pro subscription

## Labels

`category`: what the review is MAINLY about. Pick exactly one:
- `shipping`: delivery, courier, packaging, delays, lost parcels. Physical products only.
- `support`: customer service, agents, hotline, email replies, refunds handled by support.
- `bug`: software errors, crashes, broken updates, sync or login problems. Software only.
- `price`: price, fees, billing, charges, discounts, value for money.
- `quality`: physical build, durability, materials, how well the product works. Physical products only.
- `feature_request`: missing features, suggestions, wishes. Mostly software.

`mood`: the author's overall tone:
- `angry`: clearly upset, frustrated, furious or bitterly sarcastic. Mild annoyance ("a bit slow", "getting old") is NOT angry, it is `neutral`.
- `neutral`: factual, mild, mixed, or a plain question or suggestion. A problem that ended fine ("late, but everything was intact") is `neutral` only if the author sounds indifferent; if they sound relieved or happy, it is `satisfied`.
- `satisfied`: clearly pleased, grateful or enthusiastic. A feature wish is `satisfied` only if the author also clearly praises the product.

## What to write

Write exactly 50 reviews:
- Spread them evenly: about 8 per category, and about a third per mood.
- Make them sound like real people wrote them. Vary:
  - length: from 3 words to 6 sentences,
  - style: casual, formal, rambling, blunt,
  - a few typos, missing punctuation, ALL CAPS, emoji, non-native English,
  - details: dates, order problems, what they used the product for, comparisons with competitors.
- Include some hard cases:
  - sarcasm: praise words used bitterly. Label it by what the author really feels, so it is `angry`.
  - enthusiastic ALL CAPS or exclamation marks that express joy, not anger. These are `satisfied`.
  - reviews touching two topics. Label the main one.
  - polite complaints (`neutral` or `angry`, depending on tone).
- Keep every review physically and logically possible:
  - no shipping or scratches for software or subscriptions,
  - no "super fast delivery" that took two weeks,
  - numbers must fit the tone.
- Name the product in about 70% of the reviews, and leave it implicit in the rest.
- Don't use real names of people, brands, apps, operating systems, browsers, shops or places (no agent names like "Sarah", no iOS, Android, Chrome, Windows, Amazon, city or state names). Say "my phone", "the browser", "a support agent" instead. Don't include any personal data.
- Don't reuse sentence templates. Every review should read as if a different person wrote it.
- Invent your own situations. These ideas are already overused, so skip them or find a clearly new angle: dark mode, CSV export, offline mode, being charged twice, login loops, crashes after an update, a dented box with an intact product, "arrived next day", a sunrise mode for the lamp, a desk that wobbles at full height, scheduled report emails, keyboard shortcuts, reordering home-screen cards or widgets, a price hike announced in an email that went to spam, student discounts, a notification badge that doesn't clear, "tracking said delivered but nothing arrived", support copy-pasting the FAQ, a memory leak or high RAM use, custom heart-rate zones, a family or team plan, different notification sounds, a hidden handling fee at checkout, a parcel left out in the rain, a desk delivered in two separate boxes.

## Output format

Output only JSON Lines, one review per line, with no other text and no code fence:

{"text": "…", "product": "Burr coffee grinder", "category": "quality", "mood": "angry"}

Set `product` to the product's name from the lists above, or to `null` if the review doesn't make clear which product it is about.
