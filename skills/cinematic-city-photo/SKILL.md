---
name: cinematic-city-photo
description: Use when generating, transforming, recoloring, restyling, or revising warm cinematic urban photography, editorial travel covers, or film-like street photography, including when supplied images serve as edit targets or visual references for that style. Do not use for unrelated illustration, product photography, studio portrait retouching, video color grading, or camera-buying advice.
---

# Cinematic City Photo

Create one believable vertical travel-documentary photograph with restrained cover typography. Preserve the people, place, and story before applying the style.

## Required image workflow

**REQUIRED SUB-SKILL:** Load and follow `imagegen` before creating or editing any image. Use its built-in `image_gen` path for every generation, edit, typography pass, and visual revision unless its documented fallback conditions apply. For a local edit target, inspect it with `view_image` before invoking `image_gen`. Do not substitute prose, SVG, HTML, or manual pixel editing for an image-tool result.

## Route the request

Choose one mode before drafting the image instruction:

- **Generate:** No edit target exists, or supplied images are only style, composition, mood, or subject references. Do not ask for a source image.
- **Edit:** The user wants an existing image changed. If the edit target is not available, ask the user to attach it; this is the only mode in which a missing source image blocks the first pass.
- **Revise:** The user requests a change to the latest result. Treat that result as the edit target and apply only the requested delta. Preserve every unrelated approved choice, including identity, location, story, framing, grade, title wording, and layout.

Default to one moderate-strength vertical **4:5** image. For edits, reach 4:5 with a safe moderate crop; if that would remove protected content, use restrained non-destructive edge extension consistent with the visible scene instead. Do not silently retain a non-4:5 frame. Titles are enabled unless the user requests a title-free result.

## Load only what the mode needs

1. Read [references/style-bible.md](references/style-bible.md) for every request.
2. For **edit** and **revise**, also read [references/editing-rules.md](references/editing-rules.md).
3. When titles are enabled, also read [references/typography.md](references/typography.md).
4. From [references/prompt-recipes.md](references/prompt-recipes.md), read only the closest scene section: Street, Architecture, Transit, Coast, Storefront, or Seasonal foliage. For a genuine crossover, read at most two sections plus Blended Scenes.

## Analyze before invoking the tool

For edits and revisions, inventory prominent people, recognizable location and cultural cues, the central action, focal vehicles or objects, meaningful signs, source light direction, geometry, and safe negative space. When preservation is ambiguous, protect all prominent people and the main location. Never infer or invent a city; if location is uncertain, use a mood- or scene-based title.

Build this internal brief in exactly this order:

```text
Mode: generate | edit | revise
Preserved elements: people, place, story, signs, focal objects, approved prior choices
Allowed changes: generate/edit — requested direction plus moderate crop, perspective, plausible light, minor cleanup, and depth as applicable; revise — requested delta only, with every unrelated approved choice locked
Scene recipe: one primary recipe; optional compatible secondary recipe
Composition: observed editorial geometry, protected focal content, safe negative space
Light: believable direction and warm/cool relationship
Palette: plausible warm gold/amber against restrained teal-green shadows and neutral blacks
Texture: subtle grain, gentle roll-off/halation, controlled contrast and vignette
4:5 framing: vertical; retain prior framing on revision unless requested otherwise
Title/subtitle: exact concise English title plus small uppercase subtitle, placement, color; or disabled
Negative constraints: identity/place/story drift, invented city, implausible color, HDR, fake bokeh, excess glow/grain, malformed or colliding text
```

Use the user's exact requested wording when provided. Keep the prompt specific to visible or requested facts; do not introduce unsupported landmarks, brands, people, weather, vehicles, seasons, or events.

## Generate and inspect

Before every `image_gen` call, label each needed input image as **edit target**, **style reference**, or **latest revision result**. Use `referenced_image_paths` when every needed image has a local path; otherwise use the smallest `num_last_images_to_include` that includes all needed attached, conversation-visible, or previously generated images, up to the tool limit. Never provide both mechanisms. If neither can include every needed image, ask the user to reattach the missing images.

1. Invoke `image_gen` for one first-pass image. For edits, repeat all preservation invariants in the tool prompt. For revisions, name the requested delta and explicitly lock everything else.
2. Inspect the result for:
   - recognizable human identity, age range, body shape, expression, and pose;
   - preserved location, cultural details, central story, focal transit/object, and meaningful signs;
   - correct vertical 4:5 framing and moderate transformation;
   - plausible palette, skin, sky, foliage, water, shadows, texture, and light direction;
   - exact, legible title/subtitle and collisions with faces, focal objects, vehicles, signs, landmarks, or story action.
3. If identity, location, palette, framing, or collision checks fail, make one targeted revision when the tool permits, then inspect again. Do not reset approved content while correcting one defect.

## Typography failures

If generated lettering is malformed, misspelled, illegible, or crowded, keep or recreate a clean title-free image and use a separate `image_gen` edit pass that changes only typography. Follow the placement and no-safe-area fallback in [references/typography.md](references/typography.md). If supported tooling still cannot place reliable text without obscuring protected detail, deliver the clean image title-free and state the limitation briefly.

## Deliver

Return the image inline. For a workspace-bound result, also save it in the requested or project location according to `imagegen` and report the path. Add a concise note containing:

- the selected mode and title rationale (or why the image is title-free);
- the main preservation/style choices;
- useful supported revision directions, such as lighter/stronger grade, reduced warmth, title rewrite or movement, crop refinement, or correction of a specific drift.
