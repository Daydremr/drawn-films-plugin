---
name: make-whats-missing
description: What to do when a Drawn Films story needs something the menu doesn't have - map the word, use a library stand-in, show it like a film-maker, make a new object, place or costume with the make tool, make a move with the pose tool, make a person with the character tool, or ask the Drawn Films team for it. Use when a person, place, thing or move in the story isn't on the Drawn Films menu.
---

# Make what's missing

Make or request only what the story really needs, and never swap or drop something without telling the person.

## The order

1. **Map the word.** `menu(words=["zoom", "sunset", "thermos", "dance"])` says which of our words it is, a library object, or that we can't draw it yet. Free.
2. **A library object.** About 200 things are drawn already: `menu(section="objects")`. A close one that tells the story the same way is fine (a thermos is a `water-bottle`); say so to the person.
3. **A move a body can do in a few poses** (a salute, waving both arms, hands over the face, floating in space): make it with `pose` (below).
4. **Show it like a film-maker.** A big full-body move (a backflip, a dance, a fight) is shown, not animated: cut to the face, show the start and the result, a `whip` transition, the sound. A backflip becomes a crouch, a whip, and her landing with a grin.
5. **A place**: first the shared open places (`menu(section="places")`: the moon, a spaceship, under the sea, a castle hall, a cave), then make one (below). **An object**: make it (below). Each is drawn for you to check and saved for every film.
6. **A costume** (an astronaut, a knight): first the shared ones, `menu(section="costumes")` then make one (below). Everyday clothes are the menu's outfits.
7. **A person** who isn't in `cast`: make them with `character`, from the closest ready person (body, skin, hair, face, clothes and colours). Call it without changes for that person's options, then with changes to see them, show the person the picture, and save with a name once they like it; then they're in `cast`. For one film only, the closest character in the right outfit or costume is fine too. Say what you did. Never send a person through `request`.
8. **Anything else**: `request(what, kind, why)` sends it to the Drawn Films team, who build the most asked each month.

## Make an object

`make(kind="object", name="thermos", describe="a tall steel-blue thermos with a black cup lid", parts={…})`

`parts` is `{"where", "grip", "parts": [...]}`, built from simple 3D shapes, flat colour, light from the upper left:

- The object's frame is in metres: x to the right, y up from its base (nothing below 0), z toward the viewer (its front faces +z). Real sizes: a mug is 0.1 m tall, a guitar 1 m long.
- Each part: `shape` (`box`, `rounded-box`, `cylinder`, `ball`, `cone`, `ring`, `lathe`, `extrusion`), `at` (the part's middle [x, y, z]; a lathe's base middle; an extrusion's outline origin), `size` (full [width, height, depth]), `turn` (degrees about x, y, z), `colour` ("#rrggbb"), `finish` (`matte` mostly, `glossy` for ceramic or plastic, `glass`, `metal`, `glow` only for a flame, bulb or screen: it lights the scene).
  - `cylinder` and `cone` stand upright; `taper` is the top's width as a share of the bottom's (1 straight).
  - `rounded-box` takes `round` (0 to 1).
  - `ring` is a torus lying flat (width = outer diameter, height = tube thickness); turn [90, 0, 0] stands it up.
  - `lathe`: `profile` = [[radius, height], …] from the bottom up, spun round the upright axis (bottles, vases, cups, lamp shades, flames).
  - `extrusion`: `outline` = [[x, y], …] going round once (a guitar body, a leaf, a sign), 16 to 40 points for curves, given `depth`.
- Usually 4 to 14 parts, at most 24. The silhouette and the parts that say what it is, in proportion, overlapping a little so nothing floats. No tiny detail.
- `where`: `table`, `floor`, `wall` or `held`. For held, `grip`: `{"style": "wrap" | "hang" | "pinch" | "palm", "at": [x, y, z]}` (wrap: upright in a fist, like a torch; hang: from the hand, like a bag; pinch: thin, like a card; palm: on the open hand, like a cake), `at` where the hand closes. Otherwise `grip` is null.

```json
{"where": "held", "grip": {"style": "wrap", "at": [0, 0.13, 0]}, "parts": [
  {"shape": "cylinder", "at": [0, 0.12, 0], "size": [0.08, 0.24, 0.08], "turn": [0, 0, 0], "colour": "#2f6f8f", "finish": "metal", "taper": 1},
  {"shape": "cylinder", "at": [0, 0.265, 0], "size": [0.074, 0.05, 0.074], "turn": [0, 0, 0], "colour": "#222222", "finish": "glossy", "taper": 0.92},
  {"shape": "ring", "at": [0, 0.045, 0], "size": [0.084, 0.01, 0.084], "turn": [0, 0, 0], "colour": "#cfd6dc", "finish": "metal"}]}
```

Look at the picture. If it doesn't read as the thing at a glance, fix the parts and call `make` again with the same name. Then name it in a shot's `props` or `holds`.

## Make a place

`menu(section="places")` gives the place format: a sky (with stars and up to 3 big bodies, the Earth among them), far scenery, a ground with its texture, a room's walls and openings, the light, drifting air, and up to 12 big pieces built from parts. Then `make(kind="place", name="moon-base", describe="…", parts={the place in that format})`.

- Make it read at a glance: the sky and the ground first (they're most of every frame), then one to three big things that say where we are (the Earth in a black sky, a big window onto space), off to the sides or far behind, where the people don't stand.
- `nearest` is the menu place word an older engine draws instead; `is` says what kind of place it is (`moon`, `space`, `castle`…), for the fit question below.
- It comes back with a person standing in it in a wide, a medium and a close-up. If it doesn't read, fix it and make it again with the same name.
- Use it on a shot as `"place": "moon-base"`. The server writes the whole place in and its nearest place word for you.
- Older places made in parts (`"setting": "<name>"`) still work.

## Make a move (gestures)

`menu(section="gestures")` gives the gesture format: 2 or 3 key poses (where each hand goes, the elbow, the hand's shape, the body and head, the face, when each lands), which the engine eases between on the person's own body. Then `pose(word="wave-both", gesture={…}, outfit="astronaut")`.

- `base`: `stand`, `sit`, `lie`, or `float` for feet off the ground, drifting slowly, limbs loose (an astronaut in space: two slow `soft` poses with a loop).
- It comes back as a strip: the start, halfway to each pose, each pose as it lands. Check the hands are where they should be and the move reads; fix the numbers and `pose` again with the same word.
- Use it on a shot as `"action": "wave-both"`, in a wide or medium so the body shows. A big full-body move (a cartwheel, a fight) is still shown the film-maker's way, or requested.

## Does it fit?

Costumes say where they belong, and places what they are. The stills tool asks when a costume is worn somewhere it doesn't belong ("an astronaut suit in a park: on purpose?"). It never blocks: ask the person. If it's meant (a costume party, a dream), add the pair to the film's top-level `"on_purpose": ["astronaut@park"]`; else change the outfit or the place.

## Make a costume

`menu(section="costumes")` gives the costume format (pieces pinned to the body, so it bends with every action) and the costumes they can already wear. Then `make(kind="costume", name="knight", describe="…", parts={the costume in that format})`.

- Make it read at a glance, like a costume in a picture book: its silhouette first, then the one to four markers that say what it is, big and in strong colours. No tiny detail.
- Worn solid things (a helmet's visor, a sword) are object-library names, or carry their own `parts` in the object format above.
- It comes back drawn standing, sitting, running and side-on. If it doesn't read, fix it and make it again with the same name.
- Wear it with `"outfit": "knight"` on every shot of that person.
