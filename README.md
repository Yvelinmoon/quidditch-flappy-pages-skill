# Quidditch Flappy Pages Skill

This repository contains a Codex skill for generating and publishing a Harry Potter themed Quidditch Flappy Bird page.

Files:
- `SKILL.md`: the skill instructions for an online agent
- `index.html`: the standalone game template the skill customizes

What the skill does:
- Triggers when the active character is in the Harry Potter world and reaches the Quidditch pitch
- Reads `soul.md` to extract character identity and appearance
- Rewrites the rider in the bundled game so the character matches the profile
- Publishes the result to `https://claw-{bot_name}-pages.talesofai.com/...`

The game template is intentionally a single HTML file so the published page can be deployed as a standalone artifact.
