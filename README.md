# tlrc
Draft of a draft for TLRC - TOML Lyrics

Let's do one file to rule them all, lyrics.toml (or SONGNAME.toml), nothing else uses TOML for music to my knowledge so there should not be a problem.

Let's add ability to do multiple languages - we don't need to do it like subtitles for shows/movies are handled in video players, we can just add a new TOML section with a language mark.

We will support 4 things:
 * Plaintext lyrics
 * LRC (which extensions, if any?)
 * TLRC plaintext
 * TLRC synced

The rationale is that one might want to split things differently for karaoke lyrics as opposed to unsynced lyrics.

We want TLRC to do something akin to the LRC A2 extension.

We want TLRC to do something akin to the duet extension - we should be able to mark all the singers and assign them shorthands, so we know who is singing.

We want to be able to play multiple lines at once, in case two people are singing different lyrics at the same time - we will not only need start timestamps, but also end timestamps for those.

We want to be able to do italics and possibly bolding of the text.

We want to add "chapters", so we can say which part is chorus, which part is verse X, etc. This will enable nice splitting even for synchronized lines.

We want to be able to do a benign linebreak for synced lyrics, something that currently isn't very possible in LRC.

* Genius lyrics example: https://genius.com/Lord-aethelstan-die-with-me-lyrics
* Wikipedia on LRC: https://en.wikipedia.org/wiki/LRC_(file_format)

We probably want to keep the 10ms precision, as 1ms precision seems pointless.


TOML example:

```toml
[[test]]
TODO
```
