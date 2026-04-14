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

## Cover Image

Before finalizing the page, generate a 16:9 scene image through `neta-creative`.

Requirements for the image step:
- Do not ask the user whether an image is needed. Generate it by default.
- The scene must show the current character actively flying, training, or competing in Quidditch.
- Keep the scene aligned with the Harry Potter world and the Quidditch pitch setting.
- Use the appearance cues from `soul.md` so the character in the image matches the rider rendered in the page.
- Capture and keep the final public image URL returned by `neta-creative`.

The image URL is required for page metadata and social sharing.

## Bot Name

You must resolve `bot_name` yourself. Use this order:
- The current conversation context if the bot is addressed as `@name`
- The current agent or bot identity in workspace context
- The deployment hostname if one is already implied in nearby files or prior messages

Do not ask the user for `bot_name` unless all of the above fail.

## Page Edit Rules

Edit the bundled [index.html](./index.html) directly.

Required changes:
- Fill the page metadata placeholders after the image URL is available.
- Keep the gameplay rules equivalent to Flappy Bird.
- Keep the Quidditch background image and full-window presentation.
- Rewrite the rider in `drawPlayer()` so the character matches the `soul.md` appearance.
- Update visible text if the character identity should appear in the title or overlay copy.
- Keep the page standalone: one HTML file, no extra assets bundled into the skill folder.

Metadata requirements:
- Fill `og:title`, `og:description`, `og:image`, `og:url`
- Fill `twitter:title`, `twitter:description`, `twitter:image`
- Keep `og:type=website` and `twitter:card=summary_large_image`
- Make the title and description specific to the current character's Quidditch scene
- Use the generated `neta-creative` image URL for both `og:image` and `twitter:image`
- Use the final public page URL for `og:url`

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
- Important runtime hint: the pages service and the workspace share the same NAS-backed storage. In practice, placing the finished HTML file into `/home/node/.openclaw/workspace/pages/` is enough for it to sync to the pages service automatically.
- When using that sync path, ensure the filename exactly matches the final URL suffix you intend to return.
- Return the direct public URL, not an internal path or repo path.

Recommended execution order:
1. Read `soul.md`
2. Resolve `bot_name`
3. Call `neta-creative` to generate a 16:9 Quidditch scene image
4. Capture the final image URL
5. Rewrite the rider and metadata in `index.html`
6. Publish the standalone HTML page
7. Return the final page URL

## Output

When finished, provide:
- A one-line summary of which character traits were applied
- The generated image URL
- The final public URL
- A short publish confirmation that states the standalone HTML has already been placed on the pages-sync path and is ready to open

Do not dump the whole HTML unless explicitly asked.
