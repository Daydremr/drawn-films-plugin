---
name: thumbnail
description: Make the YouTube thumbnail for a Drawn Films film with the thumbnail tool - pick the face, the one feeling and the 1-3 words, then check it at phone size. Use after a film is rendered, or whenever the person asks for a thumbnail or cover for their Drawn Films film.
---

# The thumbnail

`thumbnail(film_id, words, …)` draws a 1280×720 thumbnail with our engine, in the film's own look and characters, and saves it with the film's video. A new one replaces the last, so try two or three and keep the best.

What wins on YouTube, and what the tool already does: one big face, one strong feeling, a simple background, 1 to 3 big words beside the face, never on it.

## Pick the face

- **The lead**, at the film's biggest feeling: the moment the story turns, not the happy ending. A face before the payoff makes people click to find out.
- `role` picks whose face; `shot` picks the moment (default: their best close-up). Take a shot where they're alone, with the clothes and place the film is known for.
- `holds` adds the story's one clear prop to their hand (the ticket, the phone, the letter), only if it says the story at a glance. Leave it out otherwise. `holds: "none"` empties their hands when the shot's prop or hand crowds the face.

## Pick the feeling

- One feeling, big: `strength` is strong by default. Mostly `shocked`, `scared`, `sad`, `excited`, `angry`, `worried` or `happy`: feelings a stranger reads in half a second.
- The thumbnail's feeling can be bigger than the shot's, but never one the film doesn't have.

## Pick the words

- **1 to 3 words**, the hook, not the title: the title says the rest. Plain words people say: "SAY IT", "TOO LATE?", "WHO WROTE THIS".
- A question or a half-thought beats a summary. Never the film's ending.
- Never repeat the title word for word.

## Pick the rest

- `side`: where the words go (`right` by default; the face takes the other third). Use `left` if the face looks better on the right.
- `size`: `closeup` (head and shoulders, the default) or `big` (the face fills the height, for a strong close feeling).
- `background`: `place` (the shot's own, blurred: best when the place is the story) or `colour` (a bright colour picked to stand out from them: best for most feeds), or a colour name (`cobalt`, `sunny`, `coral`, `mint`, `pink`, `purple`) or `#RRGGBB`.

## Check it

Look at the picture the tool returns as if it were 2 cm wide on a phone: can you tell the feeling, and read the words? If the face is turned away, the feeling is unclear or the words are long, change one thing and call again. Show the person your best one or two and let them pick.
