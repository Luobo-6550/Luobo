# Editing Rules and Preservation Checks

## Preservation Hierarchy

Protect, in order:

1. Prominent human **identity**, age range, body shape, expression, and pose.
2. **Location** landmarks and cultural details: architecture, transit, streets, storefronts, signage, logos, and local visual cues.
3. The central story: the event, relationship, action, or focal transit object that makes the source frame meaningful.
4. Secondary background detail, which may be simplified only when it does not change the first three priorities.

When priorities conflict, **preserve** the higher one. If preservation is ambiguous, protect all prominent people and the main location by default.

## Moderate Transformation Boundary

Default to a single vertical **4:5** result at **moderate** strength. Permitted changes are:

- Crop and perspective improvements that retain the people, place, and story.
- When a safe crop cannot reach 4:5, restrained edge extension derived from visible border context; keep protected people, place, and story unchanged, do not invent a landmark or event, and do not silently retain a non-4:5 frame.
- Plausible relighting that respects scene geometry and source-direction cues.
- Minor distraction cleanup in the secondary background.
- Added depth through subtle haze, reflection, foreground layering, or controlled color separation.
- Wardrobe-color adjustment only when it does not alter identity, role, or meaning.

Do not replace the subject, alter a prominent person's body or pose, relocate the scene, invent or remove key landmarks, or change the central event. For a revision, apply only the requested delta and **preserve** all other approved identity, place, story, aspect-ratio, and layout decisions unless the user requests otherwise.

## Typography-Safe Edits

Inspect negative space before adding a concise English title and small uppercase subtitle. Keep both away from faces, key subjects, focal vehicles, storefronts, signs, landmarks, and the story action. If no safe area exists, try a smaller clear edge placement; otherwise deliver a clean image and add typography in a separate pass. Do not make a safe area by erasing meaningful people or place details. If rendered text is malformed or illegible, use the clean-image/separate-typography fallback.

## Final Inspection

Before delivery, check:

- Framing remains 4:5 and the transformation is moderate.
- Human identity and pose are recognizable; location and cultural cues remain specific.
- The central story has not shifted; secondary cleanup did not remove important evidence.
- Gold/amber light, restrained warm colors, teal-green shadows, neutral blacks, and subtle grain remain plausible; reject orange skin, radioactive foliage, heavy HDR, fake bokeh, excess glow, or heavy grain.
- Title/subtitle is legible, correctly placed, and free of collisions; revise once when the tool permits.
