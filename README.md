# Beat Lab — four AI music guides

Public guides for composing music with the Beat Lab engine. Each guide is
available as Markdown and plain text through GitHub Pages:

| Guide | Purpose | Files |
|---|---|---|
| Score language | Authoritative JSON syntax, supported sounds, parameters, and validation | [Markdown](https://instush.github.io/beatlab-guide/music-guide.md) · [Plain text](https://instush.github.io/beatlab-guide/music-guide.txt) |
| Sound principles | Sound design, low end, compression, and mixing | [Markdown](https://instush.github.io/beatlab-guide/electronic-music-principles.md) · [Plain text](https://instush.github.io/beatlab-guide/electronic-music-principles.txt) |
| Genres | Stylistic identity and genre-specific composition choices | [Markdown](https://instush.github.io/beatlab-guide/electronic-music-genres.md) · [Plain text](https://instush.github.io/beatlab-guide/electronic-music-genres.txt) |
| Composition | Motifs, development, form, and relationships between musical events | [Markdown](https://instush.github.io/beatlab-guide/electronic-music-composition.md) · [Plain text](https://instush.github.io/beatlab-guide/electronic-music-composition.txt) |

The score-language guide defines what the engine accepts. The other three guides
advise musical decisions within that contract.

Supporting documentation includes the [score-language reference](https://instush.github.io/beatlab-guide/docs/music-reference.md)
and [JSON Schema](https://instush.github.io/beatlab-guide/docs/music-score.schema.json).

**Edit guide content in the Beat Lab app repository.** The score-language guide
is generated there; the other three guides are maintained there as authored
documents. Its `npm run publish-guide` command synchronizes the public copies,
so edits to those copies here are overwritten on the next publish.

Only guides and their supporting documentation are public. The engine source,
application, samples, and research pipeline are not included in this repository.
