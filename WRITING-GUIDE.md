# AutoConnect Blog — Writing Guide

This repo is the content source for the dynamic blog at autoconnect.rent.
Push JSON files here → articles appear on the site within 60 minutes (or instantly if the webhook is configured).

---

## File structure

```
index.json                        ← manifest: one entry per article per locale
images/                           ← blog images stored here
  beach-ksamil.jpg
  albania-roads.jpg
content/
  en/slug-in-english.json
  it/slug-in-italian.json
  fr/slug-in-french.json
  de/slug-in-german.json
  es/slug-in-spanish.json
  sq/slug-in-albanian.json
```

---

## Article JSON schema

```json
{
  "slug": "best-beaches-albania-2025",
  "lang": "en",
  "groupId": "best-beaches-albania-2025",
  "title": "Best Beaches in Albania for 2025",
  "excerpt": "Short description, 150 chars max. Used in cards and meta description.",
  "tag": "Travel",
  "image": "https://raw.githubusercontent.com/enxhips5/autoconnect-blog/main/images/your-image.jpg",
  "datePublished": "2025-06-01",
  "dateModified": "2025-06-01",
  "readingTime": 5,
  "keywords": ["Albania beaches", "best beaches Albania", "Albania summer"],
  "intro": "One paragraph opener shown as a pull-quote. Hook the reader here.",
  "sections": [
    { "title": "Section heading", "body": "Section body paragraph." },
    { "title": "Another heading", "body": "More text." }
  ],
  "tip": {
    "title": "Pro Tip",
    "body": "One actionable tip shown in a highlight box at the end."
  },
  "faq": [
    {
      "question": "Question that a traveller would actually Google?",
      "answer": "Direct, helpful answer in 2-3 sentences. Aim for voice-search friendly phrasing."
    },
    {
      "question": "Second common question about the topic?",
      "answer": "Answer with a practical detail or recommendation."
    },
    {
      "question": "Third question, ideally one an AI assistant would surface?",
      "answer": "Answer that gives a clear, factual response useful for featured snippets."
    }
  ]
}
```

**Rules:**
- `slug` must be unique per locale and URL-safe (lowercase, hyphens only)
- `groupId` links the same article across languages — use the same value for all translations of one article
- `image` — use the full GitHub raw URL: `https://raw.githubusercontent.com/enxhips5/autoconnect-blog/main/images/your-image.jpg` — upload the image to the `images/` folder in this repo first
- `readingTime` is an integer (minutes)
- `sections` can have 2–7 items; inline CTA is auto-inserted after the second section
- `excerpt` max 160 chars for SEO
- `keywords` — 3–6 short phrases; used in `<meta name="keywords">` and BlogPosting JSON-LD
- `faq` — exactly 3 Q&A pairs; rendered as a numbered section and as FAQPage JSON-LD (Google rich results + AI answer engine)
- FAQ questions should be phrased as a real user would type or speak them

---

## index.json entry format

Add one object per article per locale:

```json
{
  "slug": "best-beaches-albania-2025",
  "lang": "en",
  "groupId": "best-beaches-albania-2025",
  "title": "Best Beaches in Albania for 2025",
  "excerpt": "Short description, 150 chars max.",
  "tag": "Travel",
  "image": "https://raw.githubusercontent.com/enxhips5/autoconnect-blog/main/images/your-image.jpg",
  "datePublished": "2025-06-01",
  "readingTime": 5
}
```

---

## How to publish a new article

1. Write the JSON file (use the AI prompt below)
2. Save it to `content/[locale]/[your-slug].json`
3. Add an entry to `index.json`
4. Repeat for each language
5. Commit and push → site updates automatically

---

## AI prompt for writing articles

Copy and paste this prompt into Claude, ChatGPT, or any AI:

---

> **Prompt:**
>
> Write a blog article for AutoConnect Rental, a car rental company based at Tirana airport (Rinas), Albania. They serve tourists from Europe (UK, Italy, France, Germany, Spain) who want to explore Albania by car.
>
> **Article topic:** [DESCRIBE THE TOPIC HERE — e.g. "Top 5 beaches reachable by car from Tirana"]
> **Target language:** [LANGUAGE — e.g. English / Italian / French / German / Spanish / Albanian]
> **Target keyword:** [SEO KEYWORD — e.g. "best beaches Albania car"]
>
> Output a JSON object following EXACTLY this structure:
>
> ```json
> {
>   "slug": "[url-safe-slug-in-target-language]",
>   "lang": "[en|it|fr|de|es|sq]",
>   "groupId": "[same-value-for-all-language-versions]",
>   "title": "[SEO title, 50-60 chars, includes target keyword]",
>   "excerpt": "[Meta description, 140-155 chars, includes keyword, compelling]",
>   "tag": "[Travel | Tips | Guide | Destinations]",
>   "image": "/images/blog-albania-roads.jpg",
>   "datePublished": "[today's date YYYY-MM-DD]",
>   "dateModified": "[today's date YYYY-MM-DD]",
>   "readingTime": [estimated minutes as integer],
>   "intro": "[One strong hook paragraph, 2-3 sentences]",
>   "sections": [
>     { "title": "[H2 heading]", "body": "[Paragraph, 80-120 words]" },
>     { "title": "[H2 heading]", "body": "[Paragraph, 80-120 words]" },
>     { "title": "[H2 heading]", "body": "[Paragraph, 80-120 words]" },
>     { "title": "[H2 heading]", "body": "[Paragraph, 80-120 words]" },
>     { "title": "[H2 heading]", "body": "[Paragraph, 80-120 words]" }
>   ],
>   "tip": {
>     "title": "[Tip label, e.g. 'Pro Tip' in target language]",
>     "body": "[One practical tip, 1-2 sentences, relevant to car rental]"
>   },
>   "faq": [
>     {
>       "question": "[Question a traveller would type or speak — include the target keyword naturally]",
>       "answer": "[Direct answer, 2-3 sentences, phrased for featured snippets and voice search]"
>     },
>     {
>       "question": "[Second practical question about the topic]",
>       "answer": "[Helpful answer with a specific detail or recommendation]"
>     },
>     {
>       "question": "[Third question an AI assistant might surface about this topic]",
>       "answer": "[Clear factual response, ideally with a number or concrete advice]"
>     }
>   ],
>   "keywords": ["[primary keyword]", "[secondary keyword]", "[long-tail keyword]", "[location keyword]"]
> }
> ```
>
> Requirements:
> - Natural, helpful tone — not salesy
> - Mention AutoConnect Rental once in the intro or a section naturally
> - Include the target keyword in: title, first section heading, and once in the body
> - Sections should flow logically and give real value
> - Tip should be specific and actionable
> - FAQ: 3 questions only, phrased as real users speak/type them, answers optimised for Google featured snippets and AI answer engines (short, direct, factual)
> - keywords: 3-6 phrases, mix of short-tail and long-tail, relevant to the article topic and Albania car rental
> - Output valid JSON only, no markdown code block wrapping

---

## Webhook setup (one-time)

After creating the repo, go to **Settings → Webhooks → Add webhook**:

| Field | Value |
|-------|-------|
| Payload URL | `https://autoconnect.rent/api/revalidate` |
| Content type | `application/json` |
| Secret | *(the value of REVALIDATE_SECRET in Vercel)* |
| Which events | Just the `push` event |

This makes articles go live instantly after every push.
