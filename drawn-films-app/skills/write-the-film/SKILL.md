---
name: write-the-film
description: Write a short animated film for Drawn Films from the person's own story or idea, as a plain screenplay, then take it through the Drawn Films tools to a finished 1080p video. Use whenever someone wants to make an animated film, short or video with Drawn Films (or the drawn-films tools).
---

# Write the film

Drawn Films draws and renders hand-drawn animated films on the Drawn Films server, through the app's plugin (`drawn-films-app`). You write and direct; its tools draw. Every tool answers in a line or two, so check before you write, and send small changes.

If the Drawn Films tools aren't there or say the key is wrong, the plugin needs their Drawn Films key from the app (Settings, then Connections), and their ElevenLabs key goes in the app too. Say which is missing, in one line, and wait.

## The order (keep to it)

1. **Check what we have** before writing: `menu` (our words) and `cast` (the people they can use, and their own). Write only with those people, places and things. Anything missing: the make-whats-missing skill.
2. **Write the screenplay** (below). Show it to the person and get their OK or changes. It's their story.
3. **Direct it** into film.json (the direct-it skill), in the house style (the house-style skill).
4. **Stills**: `stills(film=…)` returns one contact sheet and a `film_id`. Check it (the check-it skill) and fix only the shots that need it with `replace_shots`.
5. **Voices**: `voices(film_id)` voices the lines with the person's own ElevenLabs key (their credits).
6. **Render** only after the person says yes: it takes a while. `render(film_id)` waits and says where the video is (the app shows it in Films). If it says "still rendering", call it again: it never starts twice.
7. **Thumbnail**: offer one. `thumbnail(film_id, words=…)` draws it from the film (the thumbnail skill).

## The story

Simple and fast, like the hand-drawn shorts that go viral: one person, one idea, told in pictures.

- **Their story.** Build it on what the person lived or wants to say: keep their people, what happens, how it ends and any lines they wrote. A few words of idea get a whole story built from them. Ask one question only if you can't write it without the answer.
- **Portray the feeling, nothing else.** "Why life is so hard" is a film of that feeling, not a plot with errands. Every beat moves the story or deepens the feeling.
- **One person with one want.** Two or three people at most (pets don't count; a narrator can name more).
- **One or two places** from the menu.
- **One visual idea** you can say in a sentence, the picture the film keeps coming back to, a little changed each time (the boxes she never unpacks, the second mug on the table).
- **Big things you can read on screen**: a suitcase, a stack of boxes, a phone lighting up, an empty chair. Never a tiny thing the story hangs on (a ring, a key, a cookie) and never a crowd.
- **The hook**: the first 3 seconds stop a stranger scrolling. Open on something happening (the climax we'll come back to, a strange picture, a line mid-moment), never a room waking up or a title.
- **Want and stakes by 10 seconds.** The turn is caused by something we saw earlier. Every setup pays off: what we see early comes back changed.
- **The payoff lands on a picture we feel** (a hug, a door flung open, a laugh, a run), not a speech.
- **Emotion seen before it's named**: shaking hands, eyes on the empty chair. Nobody says "I'm lonely".
- **Lines**: 2 to 8 words, what people really say out loud, each said once in the film, never telling us what we can see.
- **Sense**: nobody knows what they couldn't know; each new person is clear at once; jumps in time or place are clear.
- **The length follows the story.** A minute is about 18 to 25 shots. If it runs out of things to show, it's shorter. Never pad.

What the medium can't do: words written on things can't be read on screen, so a note or sign that matters is heard in the reader's head while we see their face, and a phone message shows big on the phone's screen (direct-it's `texts`), never read aloud as well. Only people speak; animals act and make their own sounds. A scene has one time of day and one weather. No title or end card.

## The screenplay format

```
TITLE: <the hook in a few words>
FEELING: <the feeling it leaves>
STORY: <one sentence: who wants what, what's in the way, how it turns out>
PEOPLE: <each with who they are to the lead, and the cast id you'll use: Maya (the lead, teen-girl-1)>
THINGS: <every object someone holds, gives or uses, or the story turns on>

SCENE 1 | <where>, <time of day> | <seconds>s
MUSIC: <under 20 words: genre, instruments, energy, feeling; instrumental>
CARD: <a time card, only when a jump needs it: NEXT MORNING>
<what we see, one beat a line, present tense: each beat a new picture someone could draw>
SOUND: <a sound that matters>
NAME: <a line>
NARRATOR: <a line>
```

A line holds the screen about 2 seconds plus a quarter second a word; a beat with no line about 2 seconds.
