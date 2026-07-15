---
name: humanize-writing
description: Use whenever producing or reviewing short-form content — news summaries, social posts, tweets, product blurbs, email subject lines, translations/summaries from a foreign-language source — or when writing/reviewing an AI prompt or code pipeline that generates such content. Removes "AI slop" - formulaic openers, filler hedges, hashtag spam, translation contamination — and enforces a validation loop for fully automated publishing pipelines.
---

# Humanize Writing — Anti-Slop Rules

Distilled from real production failures in an automated content pipeline: these are the exact patterns that made readers instantly recognize output as machine-written, and the fixes that survived contact with production.

## Banned Openers

A summary/post/tweet must NEVER open with a sentence *about the text itself* instead of the story. A real editor never writes these:

- "In this article…" / "This piece covers…" / "In today's news…"
- "Here's what you need to know about…" / "Let's dive into…"
- "BREAKING!" / "INTERESTING NEWS!" — generic all-caps + exclamation openers
- "According to reports, it has begun…" — vague sourcing as a crutch

**Rule:** The first sentence delivers the concrete event directly — subject + verb + what happened. No meta-introduction.

Bad: "This story covers the army's shocking torture admission!"
Good: "The army admitted torturing a detainee in the border region."

## Banned Filler & Hedges

Match the language's certainty to the source's certainty — no reflexive softening:

- "perhaps", "it seems", "arguably", "one could say", "may well be"
- "it's worth noting that", "importantly", "interestingly"
- Empty intensifiers: "truly", "incredibly", "absolutely game-changing"

## Punctuation Tells

Models overuse certain punctuation to the point that it reads as machine-written:

- **Em-dash overuse.** The em-dash is a real tool, but AI reaches for it reflexively. Three or more in a short passage is a tell. Prefer commas, periods, or parentheses; keep em-dashes rare and deliberate.
- **Arrow-and-colon lists in running prose** that isn't actually structured data ("the fix: X → Y → Z").

Bad: "The fix was simple — two lines — and it shipped, no issues at all."
Good: "The fix was two lines. It shipped with no issues."

For pipelines, add a density check: flag any short passage whose em-dash count crosses a set threshold and rewrite it.

Bad: "Oyarzabal is perhaps the most impressive player in the squad."
Good: "Oyarzabal is the standout name in Spain's World Cup squad."

## Hashtag / Tag Spam

Never append the same generic tag set to every post ("#News #Trending"). Choose tags specific to *this* item — names, teams, organizations, the actual topic. A generic tag is a last resort when nothing specific exists.

## Translation Contamination

When summarizing/translating from a foreign-language source, source-language words and structures leak into the output — producing half-translated, bilingual broken sentences. This is a distinct and equally damaging slop type.

**Rule:** Before finalizing, check each sentence: has an untranslated noun phrase, verb, or idiom leaked in? Established loanwords in the target language are fine ON THEIR OWN — but never doubled with the source word ("penalty kick shot"-style redundancy).
When unsure, apply the test: *would a reader who speaks only the target language understand this sentence without friction?*

## Enforcement: "Generate → Validate → Retry → Skip"

If you are writing a prompt or code pipeline that generates content, rules in the prompt alone are NOT enough — models (especially small/fast ones) regress into these patterns. Build a two-layer defense:

1. **In the prompt:** list the banned patterns explicitly with bad/good example pairs (as above).
2. **In code:** validate generated text against banned-pattern regexes before publishing.
3. On failure, **regenerate** — maximum 3 attempts.
4. **If all 3 attempts fail, skip that item entirely — never force-publish bad text.**
   Do not add a "use the best failed attempt" fallback; silence is better than publishing slop.

This loop applies both to automated pipelines and to your own output: before calling any text "done", actually check it against the banned lists above — don't just skim it.
