# tlrc
Draft of a draft for TLRC - TOML Lyrics

Let's do one file to rule them all, lyrics.toml (or SONGNAME.toml), nothing else uses TOML for music to my knowledge so there should not be a problem.

Let's add ability to do multiple languages - we don't need to do it like subtitles for shows/movies are handled in video players, we can just add a new TOML section with a language mark.

We will support 4 sections:
 * Plaintext lyrics
 * LRC with both known extensions
 * TLRC "plaintext"
 * TLRC synced

The rationale is that one might want to split things differently for karaoke lyrics as opposed to unsynced lyrics.

We want TLRC to do something akin to the LRC A2 extension, i.e. fullblown karaoke.

We want TLRC to do something akin to the duet extension - we should be able to mark all the singers and assign them shorthands, so we know who is singing.

We want to be able to play multiple lines at once, in case two people are singing different lyrics at the same time - we will not only need start timestamps, but also end timestamps for those.

We want to be able to do italics and possibly bolding of the text.

We want to add "chapters", so we can say which part is chorus, which part is verse X, etc. This will enable nice splitting even for synchronized lines.

We want to be able to do a benign linebreak for synced lyrics, something that currently isn't very possible in LRC.

* Genius lyrics example: https://genius.com/Lord-aethelstan-die-with-me-lyrics # TODO (Martin): when finalizing examples do not use macabre songs
* Wikipedia on LRC: https://en.wikipedia.org/wiki/LRC_(file_format)

We probably want to keep the 10ms precision, as 1ms precision seems pointless.

Avoid redefining data that should already be present in the file metadata - verify all the common formats support whatever tag we are no longer providing, as compared to LRC.

Let's standardize (s)LRC (core) and e(LRC) (core+a2+duet), since the standard seems to currently live on Wikipedia of all places.

Force chronological order(?).

TOML example:

```toml
[spec]
name = "TLRC"
version = "0.1-draft"

[track]
title = "Die With Me (Example)"        # optional if player can read from media tags
# Artists are tagged as one letter, followed by a pipe character with their full name
# In this example, lyrics can use L, N, or LN tags, where LN would be a duet
artists = ["L|Lord Æthelstan", "N|Nyanners"] # optional (duet example)
# https://datatracker.ietf.org/doc/html/rfc5646.html
language_default = "en"                # BCP-47 code for default language

[lyrics.en]

# 1) Plaintext lyrics (unsynced, simple). No formatting support.
[lyrics.en.plain]
text = """
[Verse 1]
I will stand where shadows meet the sea,
and whisper “stay” — if you’ll stay with me.

[Chorus]
Hold your breath and count to three,
"""

# 2) Raw LRC variants for compatibility (verbatim strings; players can use as-is)
[lyrics.en.lrc]
slrc = """
[ar:Lord Æthelstan & Nyanners]
[ti:Die With Me]
[00:12.30]I will stand where shadows meet the sea,
[00:17.10]and whisper "stay" — if you’ll stay with me.
[00:23.00]Hold your breath and count to three,
"""

# 3) TLRC "plaintext" (unsynced but structured: chapters, styling, inline singer tags(?))
[lyrics.en.tlrc.plain]

# 4) TLRC synced (rich, structured; supports concurrency, chapters, singer assignment, soft linebreaks)
[lyrics.en.tlrc.synced]


```
