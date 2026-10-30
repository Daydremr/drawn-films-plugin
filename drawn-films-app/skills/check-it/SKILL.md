---
name: check-it
description: Check a Drawn Films contact sheet from the stills tool for framing, continuity and pace, then fix only the shots that need it. Use every time the stills tool returns a sheet.
---

# Check the contact sheet

The stills tool returns one sheet: each still with its shot id, camera, focus and the start of its line, plus anything the engine noticed. Look at it the way a viewer with the sound off would.

## Shot by shot

- **Can you tell what's happening?** The thing that matters is big enough to see; if it's small, add an `insert` of it or hold it in a `medium`.
- **Faces**: a face close-up shows the face. If it's hidden (hair, turned away, behind something), set `facing` toward the camera side or `front`, or change the camera.
- **The feeling reads**: the face and the body show the `mood`. Too faint: `strength: strong`, a closer camera, or a light that fits.
- **Lines** are on the speaker's close-up, mouth visible.
- **Nothing broken**: people overlapping (spread their `at`), someone floating who shouldn't be or cut off at the frame edge, a prop in the wrong place. Fix what the "Noticed" list names first.
- **A question with the sheet** ("an astronaut suit in a park: on purpose?"): put it to the person, never decide it yourself. Meant: add the pair to the film's `on_purpose`. Not meant: change the outfit or the place.

## Across shots

- **Continuity**: people stay on the same side (`at`) and face the same way across cuts in a scene; what they hold stays in hand until it's put down or handed over; the same outfit, light, weather and time through a scene.
- **Pace**: a new picture about every 2 seconds. Two shots in a row that look or tell the same: change the camera, or cut one. An empty beat (someone just standing): cut it.
- **The story reads in pictures**: the hook in the first shots, the want by about 10 seconds, the setup seen before its payoff.

## Fixing

- Fix only the shots that need it: `stills(film_id=…, replace_shots=[the changed shots])` redraws just those, `remove_shots=[ids]` cuts. `only=[ids]` redraws without changes.
- Show the person the sheet and say in a line what you changed. Stills are free and unlimited, so two or three rounds are fine; stop when it reads.
- A moment the engine can't draw: the make-whats-missing skill. Never swap or drop something without telling the person.
- When it reads: `voices(film_id)` (it uses their ElevenLabs credits), then ask before `render`.
