# humanize-writing

A Claude Code skill that strips "AI slop" out of generated text — the formulaic openers, filler hedges, hashtag spam, and half-translated sentences that make readers instantly recognize machine-written content.

It was distilled from real failures in an automated content pipeline: the exact patterns readers caught in production, and the fixes that survived.

## What it does

- **Bans meta openers** — "In this article we'll dive into…" never survives. The first sentence delivers the event: subject + verb + what happened.
- **Bans filler and hedges** — "perhaps", "it's worth noting", "truly game-changing" get cut. The language matches the source's certainty, no reflexive softening.
- **Kills hashtag spam** — tags specific to the item, not the same generic set on every post.
- **Catches translation contamination** — when summarizing from another language, source-language words leak into the output. It flags the half-translated sentence before it ships.
- **Adds an enforcement loop for pipelines** — generate → validate against regex → retry up to 3 times → skip. Never force-publish; silence beats slop.

## Install

Copy the skill folder into your skills directory:

```bash
# Global (all projects)
cp -r humanize-writing ~/.claude/skills/

# Or per-project
cp -r humanize-writing .claude/skills/
```

Plain markdown, no dependencies. Works with the Claude Code CLI, the desktop app, and IDE extensions. The skill triggers automatically when you produce or review short-form content, or when you write a prompt/pipeline that generates it.

## A taste of the rules

> **Bad:** "This story covers the army's shocking torture admission!"
> **Good:** "The army admitted torturing a detainee in the border region."

> **Bad:** "Oyarzabal is perhaps the most impressive player in the squad."
> **Good:** "Oyarzabal is the standout name in Spain's World Cup squad."

Full rule set with bad/good pairs is in [`SKILL.md`](./SKILL.md).

## Part of a larger set

This is one of 34 production-tested Claude Code skills — SEO content systems, a zero-to-live website launch sequence, e-commerce growth automation, PayTR payment integration, an 8-layer security audit, and the daily dev workflow (review, commit, PR, changelog).

They came out of shipped websites and are in daily use building a multilingual marketplace. This one is free, on its own, forever.

- **The full bundle:** [hekimsoft.com](https://hekimsoft.com)
- **Built by Hekim Software** — AI consulting and custom software from Istanbul.

## License

MIT — see [LICENSE](./LICENSE). Use it, fork it, adapt it to your own pipeline.
