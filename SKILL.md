---
name: quidditch-flappy-pages
description: Trigger when the active character is in the Harry Potter world and arrives at the Quidditch pitch. Read soul.md to extract the character identity and appearance, customize the bundled Quidditch Flappy index.html so the rider matches those traits, then publish the standalone page to claw-{bot_name}-pages.talesofai.com and return the direct URL.
---

# Quidditch Flappy Pages

Use this skill when the character is already in the Harry Potter world and the scene specifically reaches the Quidditch pitch.

This skill ships a single-file Flappy Bird style page in [index.html](./index.html). The page is meant to be customized in-place, published as a standalone HTML file, and then shared back as a direct URL.

## Trigger

Trigger when all of the following are true:
- The active character is acting inside the Harry Potter world.
- The scene or user request involves the Quidditch pitch, Quidditch match, Quidditch training, or flying through the stadium.
- The task is to generate or publish the playable web page, not just discuss it.

## Required Inputs

Before editing the page, read the current character profile from `soul.md`.

Preferred lookup order:
- A `soul.md` path explicitly mentioned in the current task or workflow.
- A nearby `soul.md` in the active workspace if one exists.
- The current runtime's active character profile file if one is exposed by the agent environment.

Extract at minimum:
- Character name
- Key visual traits
- Costume / color cues
- Accessories or symbols
- Tone or status cues that should affect posture or styling

## Bot Name

You must resolve `bot_name` yourself. Use this order:
- The current conversation context if the bot is addressed as `@name`
- The current agent or bot identity in workspace context
- The deployment hostname if one is already implied in nearby files or prior messages

Do not ask the user for `bot_name` unless all of the above fail.

## Page Edit Rules

Edit the bundled [index.html](./index.html) directly.

Required changes:
- Keep the gameplay rules equivalent to Flappy Bird.
- Keep the Quidditch background image and full-window presentation.
- Rewrite the rider in `drawPlayer()` so the character matches the `soul.md` appearance.
- Update visible text if the character identity should appear in the title or overlay copy.
- Keep the page standalone: one HTML file, no extra assets bundled into the skill folder.

Character rendering guidance:
- Prefer readable silhouette over fine detail.
- Use 2 to 5 high-signal traits from `soul.md`, not every trait.
- Make the character recognizable at game scale by prioritizing hair, headwear, face shape, dominant costume colors, and one signature accessory.
- If the character is non-human or highly stylized, adapt the rider into a simplified airborne version rather than forcing realism.

## Publish Flow

Publish the final file as a standalone page on the claw pages host for the active bot.

Required URL pattern:
- `https://claw-{bot_name}-pages.talesofai.com/{page_name}.html`

Suggested output filename:
- `quidditch-flappy-{character_slug}.html`

If `bot_name` resolves to `openclaw` and the filename resolves to `quidditch-flappy-yongzheng.html`, the final public URL should be:
- `https://claw-openclaw-pages.talesofai.com/quidditch-flappy-yongzheng.html`

Deployment requirements:
- Publish the page as a direct standalone HTML page, not as an embedded app route.
- Use the runtime's available publish or pages deployment workflow.
- Return the direct public URL, not an internal path or repo path.

## Output

When finished, provide:
- A one-line summary of which character traits were applied
- The final public URL

Do not dump the whole HTML unless explicitly asked.
