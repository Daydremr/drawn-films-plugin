---
name: house-style
description: The Drawn Films house style for directing a film shot by shot - pace, cameras, close-ups on lines, cutting on action, feelings in face, body and light, and the one big cinematic moment. Use while directing or fixing a Drawn Films film.json.
---

# The house style

Fast, readable, felt. A stranger should follow it with the sound off.

## Pace
- **A new picture about every 2 seconds.** Silent shots 1.5 to 2.5 s; 3 s (4 at most) only for the one big feeling, like a hug.
- A shot holds longer only while someone speaks (a line shot has `seconds: null`: its voice sets the length).
- **No empty beats**: no walking from A to B, no establishing shot the story doesn't need. Never two shots in a row that tell the same thing.
- **Something changes in every shot.** A shot where nothing happens is a frozen picture (Thirty-One Kilos, 30 Oct: a shocked face held 2 s, an open case 2.5 s, nothing moving). Each silent shot carries one change you can see: the feeling turns (`then` on the actor: `{"at": 1.0, "mood": "sad"}`, the smile falling, the shock turning to tears), the eyes dart (`face` `look_x` keyframes), a hand does something to a thing, a text lands on the phone (`texts`), a door opens, a number on the `board` drops. A reaction close-up is welcome when its face moves from one feeling to the next.
- **Sounds on every action, on its moment.** Hands, feet, hugs, sit-downs and phone chats make their own sounds when they happen. Write the rest in `sounds`, timed to the moment: `"thud@1.2"` lands 1.2 s in (a bag dropped, a door slammed, a buzz as the phone lights). A good film carries 3 to 8 timed sounds a shot; a silent action reads as dead.

## Cameras
- **A close-up on every line.** A cast line plays on the speaker: `closeup` (alone), `over-shoulder` (past the listener) or `extreme-closeup` (the one big feeling of the film). The speaker's action is `talk`.
- Mostly close and medium: close-ups about 35 to 40 % of shots, `medium` 25 to 30 %, `over-shoulder` 10 to 15 % in conversations, `insert` about 5 % (the thing that matters, before it pays off), `wide` and `establishing` together about 10 %.
- A wide only opens a new place (short) or shows a layout that matters (people coming and going, action across the room).
- Conversations alternate `over-shoulder` and `closeup`, so the two people are seen together, not only one face at a time. Reactions are short close-ups after something that earns one.
- **People look at each other, not at us.** A talker faces the one they talk to (`facing` toward them, `target` on them), so close-ups are three-quarter, never a row of faces straight at the lens. `front` is for a look at the audience on purpose, a thought, or someone alone with a feeling.
- **The thing is in the picture.** An action on a thing (`pick-up`, `open`, `put-down`, `give`) plays with the thing in `props` or `holds` and in frame: a `medium` or `insert` with the hand on it, never a close-up where the thing is out of shot.
- One special angle a scene at most: `top` (a table, a bed, a fall) or `low` (the hero beat: a win, a decision). Never on a scene's first shot.

## Cutting
- **Cut on action**: each shot follows from the one before: an action, then its reaction; a look, then what they see; a question, then the answer.
- Keep people where they were across cuts (the same `at`), facing each other with `target`. Someone who leaves walks out; someone who arrives walks in.
- A new place or time opens on a short `establishing` or `wide`; a place already shown can open on a `medium`. A `card` (3 words at most) only when the jump needs saying.

## Feelings in the face, the body and the light
- Every person in every shot has the `mood` they feel; `strength: strong` at the peak (sad becomes teary, cry sobbing), `soft` for quiet moments. In a wide the face is small, so the body carries it (sad slumps, proud stands tall, scared hunches).
- The emotional peak gets one held close-up (2.5 to 3 s) with `move: push-in`.
- **One light a scene** from its time and feeling: `gloomy` or `moonlight` in the low, `lamp-glow`, `golden-hour` or `sunrise` where it turns, `tense` or `dramatic` only where a scene turns. Never golden-hour or sunrise in rain or snow.
- **Every shot moves**: leave `move` out (the engine pushes in on close shots and drifts on wides) or pick one: `push-in` for a realisation, `pull-out` for loneliness or an ending, a pan to reveal, `handheld` for panic, `crash-in` for a shock or a punchline (the frame rushes in with a whoosh). `still` only for one comic beat in a film, never for a montage.
- **A hit shakes the camera**: a slam, a fall, a shock landing gets `hits: [seconds]` on the shot with its sound at the same second (`"sounds": ["slam@0.8"], "hits": [0.8]`). A few a film, never a habit.

## The inner meaning in pictures
- Show what it means without saying it: loneliness is someone small in a wide with space round them; a life piling up is a `heap` that grows across the film; a new start is a `room` going from `moving-in` to lived-in.
- **One object carries the film**, like a phone that keeps buzzing or a board counting down: it's in the first 8 seconds, it changes as the story moves (a number falls, a message arrives, a heap grows) and it pays off at the end.
- The film's one visual idea comes back changed at the end.
- Tell it with the phone when the story lives there: an `insert` with `focus` `phone` and `texts`, a message per shot landing, beats a line saying it.
- A `narrator` adds only what pictures can't (time passing, a number, what someone doesn't know).

## One big cinematic moment
- At most **one** effect in the whole film, on its biggest moment, and most films need none: `slowmo` (a silent 3 s shot of the key action), `letterbox`, `nightfall` (a day turning to night), a `whip` or `flash` transition, a `crane` onto a place, `circle`, `magnify`, `timer`, `viewfinder`.
- **Never `impact` or `trail`.** For a hit, use a camera move, a `flash` transition and a sound instead.
