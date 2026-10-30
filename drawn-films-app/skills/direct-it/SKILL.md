---
name: direct-it
description: Turn a Drawn Films screenplay into film.json shot by shot, using only the words the Drawn Films menu tool returns, then send it to the stills tool. Use after the screenplay is agreed, and whenever writing or changing a Drawn Films film.json.
---

# Direct it: the screenplay → film.json

The renderer draws exactly what you write, and only menu words draw. Call `menu` and `cast` first if you haven't this session. The stills tool refuses a film with a wrong word and lists every one to fix, so a first try costs little.

Keep every scene in order, every beat on screen and every line word for word. One shot a beat. Add no story.

## The file

```json
{
  "title": "Grandpa's Mug",
  "engine": "simple",
  "cast": [{"role": "maya", "character": "teen-girl-1"}, {"role": "grandpa", "character": "grandpa"}],
  "music": {"mood": "hopeful", "cues": [{"from": "s01", "feel": "soft piano, a quiet evening, tender"}]},
  "shots": [
    {"id": "s01", "place": "bedroom", "time": "evening", "camera": "establishing",
     "actors": [{"role": "maya", "at": 0.35, "facing": "right", "action": "look", "mood": "sad"}],
     "props": ["lamp"], "sounds": ["wind"], "light": "lamp-glow", "seconds": 2},
    {"id": "s02", "place": "bedroom", "time": "evening", "camera": "closeup", "focus": "maya",
     "actors": [{"role": "maya", "at": 0.35, "facing": "right", "action": "talk", "mood": "loving", "holds": "mug", "holds_colour": "brown"}],
     "line": {"role": "maya", "text": "Still warm.", "tags": "[softly]"}, "seconds": null, "light": "lamp-glow"},
    {"id": "s03", "place": "bedroom", "time": "evening", "camera": "insert", "focus": "mug",
     "actors": [{"role": "maya", "at": 0.35, "facing": "right", "action": "look", "mood": "loving", "holds": "mug", "holds_colour": "brown"}],
     "light": "lamp-glow", "seconds": 2}
  ]
}
```

- `engine`: `"simple"`. Always set it.
- `cast`: a short lowercase role for each person and the `cast` tool's id for who plays them. Each character once. Pets are cast like people.
- `music.mood`: a menu word; `cues`: one a scene, `from` its first shot, `feel` under 20 words, instrumental, never an artist or song. The music plays under the whole film (`music.style` `moments` instead: short cues with silence between).
- `captions`: `true` burns every spoken line in as it's said (for films watched with the sound off, Shorts).
- Shot ids run `s01`, `s02`, … in order. A shot added later between two is the one before plus a letter (`s03a`).

## A shot

Required: `id`, `place`, `time`, `camera`, `actors` (may be empty), and `seconds` (a number for a silent shot, `null` for a line shot). `focus`, `props`, `sounds`, `sfx` and `line` default to empty.

An actor: `role`, `at` (0.05 to 0.95 across the frame), `facing` (`left`, `right`, `front`, `back`), `action` (a menu action or one of their gestures, `menu(section="gestures")`), `mood`. Optional: `to` (where a walk or run ends), `target` (the role they look at, talk to, give to, hug), `holds` (one thing in hand), `holds_colour`, `outfit` (a menu outfit or a costume from `menu(section="costumes")`, written on every shot of theirs), `posture` (`sit`/`lie` when the action doesn't place them), `strength` (`soft`/`strong`), `then` (`{"at": seconds, "mood": <a mood>, "strength"?}`: their feeling turns partway through the shot; a second action is a second shot).
Rarer, for a moment the words above don't give: `sit_up` (sitting up in bed; `one_hand` keeps a phone in one hand), `z` (0..1, how far back toward the back wall), `keep_at` (exactly at `at`, even right behind someone), `face` (the face's own controls for the shot, numbers or `[[seconds, value], …]`: `circles` for dark circles, `reflect` for someone seen in the eyes, `lids` 1→0 waking up, `look_x`, `brow_in`, `smile`, `tears`…).

Optional on a shot: `move`, `light`, `weather`, `transition` (`whip`, `flash`, `dip`, `dissolve`, or one a film: `morph` matched framings, `focus` a rack focus, `zoom-through` with `transition_at` [x, y], `haze` smoke, `glow` a light leak, `glitch`), `card` (3 words at most), `caption` (the story's own words at the bottom, 12 at most, written in), `room`, `heap` ({`of`, `size`, `on`}), `setting`, `call` (the other end of a video call), `texts` (messages read on the phone's screen: `[{"from": <role>, "text": …}]`, 3 at most; an `insert` with `focus` `phone` shows the chat; never also a line), `door` (`[[seconds, degrees open], …]`: the room's door swings, a slam is open then 0), `front_door` (on a `hallway`: `[[seconds, 0..1], …]`), `eyes` (`true` on an `extreme-closeup`: just the eyes), `back`/`lift` (a `medium` further back, raised), `nudge` (`{"shift", "look", "dist", "lens"}`: the framing moved by hand), and one cinematic flag a film at most (the house-style skill).

## The rules the stills tool checks

- **One line a shot at most**: `{"role", "text", "tags"}`. A cast line plays on the speaker: camera `closeup`, `extreme-closeup` or `over-shoulder`, `focus` the speaker, their action `talk`.
- **Voice-over**: `line.role` `narrator`. Any camera; nobody in the shot `talk`s. There's no inner voice: a thought is shown in the face and in pictures, or said out loud.
- A silent close shot has one actor; a silent `over-shoulder` two. An `insert`'s `focus` is a prop in the shot or something someone `holds`.
- A shot without a line needs `seconds` (1.5 to 3; 4 only for a hug or a cry).
- **Pets never speak or hold things**: their moment is a sound in `sounds`, or one `sfx` like "a small dog barks twice".
- `props`: menu props, library objects, or things they made. Name a library or made object in `props` or `holds` and the server adds it to the film's `objects` for you.
- `sounds`: built-in sounds (free), each a name or `"name@seconds"` to land on its moment. Hands, steps, hugs and phone chats sound by themselves. `hits` (on a shot): up to 3 seconds where the camera jolts, with a sound timed there. `sfx`: at most one free-text sound a shot, made with the person's ElevenLabs key; use built-in sounds first.
- A place the menu doesn't have: an open place as the shot's `place` (`"place": "moon"`, a shared one or one they made: `menu(section="places")`). The server writes the whole place in. An older place made in parts is `"setting": "<name>"` with `place` the nearest place word.
- A gesture (theirs, made with `pose`) is an `action` like any other; a floating one (`base` `float`) drifts above the ground, so frame it in a wide or medium.
- A costume worn where it doesn't belong (an astronaut suit in a park) comes back as a question with the stills: ask the person; if it's meant, add `"on_purpose": ["astronaut@park"]` at the top of the film.
- Keep one `light` and `weather` through a scene; `time` is the same within a scene.
- Two people in a shot face each other (`facing`), each with `target` on the other.

## What actions do

- `walk`/`run` read in a wide or medium (with `to`); in a close-up they look like standing.
- `sit`, `slump`, `eat` take the nearest seat: name it in `props` (chair, bench, bed, sofa via a setting).
- `phone`: looking at it and scrolling (in bed with `posture: lie` it's held up). A phone in `props` with someone talking and nobody to talk to is a call at the ear. `call: "<role>"` makes it a video call with that face on the screen.
- `read`, `write`, `type` with `desk` in `props` sit at the desk. `open` opens a door, curtains (`target: window`), a box in `props`, or a held book.
- `give`/`take` hand over what's held to or from the `target`. `hug` with a `target`. `jump` is a hop for joy; a pet's `jump` rears up on its hind legs at its `target`.
- `thumbs-up`: a fist up, thumb up (best facing us, close). `pocket`: the phone slid into the front pocket. `write-board`: writing the number on a `board:<digits>w` whiteboard prop, `holds` `pen` (they walk to it; frame a `medium`, then an `insert` with `focus` `board`).
- A phone on a table lights up and buzzes with `sounds: ["buzz"]`. An `insert` on a `wall-clock` or `alarm-clock` shows time passing.

## Then

Send it: `stills(film=<the whole film.json>)`. Keep the `film_id` it gives. After that, change only what's needed: `stills(film_id=…, replace_shots=[…], remove_shots=[…])` redraws just those shots, so the film isn't sent again.
