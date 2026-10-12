# BEATLAB — THE COMPLETE GUIDE: SYNTAX, SOUND, GENRE, COMPOSITION

One document, four parts. It is the four Beat Lab guides concatenated in
reading order, each reproduced verbatim, so nothing here differs from the
standalone files; attach this one file instead of four.

  PART 1  SYNTAX       the score language — AUTHORITATIVE   (music-guide.md)
  PART 2  SOUND        sound design and mix — advisory       (electronic-music-principles.md)
  PART 3  GENRE        style identity — advisory             (electronic-music-genres.md)
  PART 4  COMPOSITION  motif, development, form — advisory   (electronic-music-composition.md)

HOW THE PARTS RELATE

- Part 1 alone defines what compiles: fields, legal values, limits, sounds,
  routing, automation, and how to author ex_ synth and exd_ drum voices. Its
  response contract (Part 1, section A.1) governs the final answer: the reply
  is the score JSON and nothing else.
- Parts 2-4 advise musical judgment. Where any of them seems to describe a
  capability that Part 1 does not list, Part 1 wins: translate the intention
  into supported fields instead of inventing one.
- An explicit user instruction overrides every default in Parts 2-4.
- Reading order: Part 1 before writing any JSON. Then Part 3 for what the
  requested style must get right, Part 2 for how to build and mix the sounds
  it needs, and Part 4 for how the material develops into a piece.
- Each part keeps its own numbering and cross-references; a reference to
  "the score guide" or "music-guide.md" means Part 1.


===============================================================================
PART 1 OF 4 — SYNTAX: THE SCORE LANGUAGE (AUTHORITATIVE)
Standalone file: music-guide.md
===============================================================================

# BEATLAB EXTERNAL SCORE — COMPILER TARGET

You are composing directly for the Beatlab audio engine.

The musical request defines what the piece should communicate. This document
defines the executable score language and the sound-producing world available
to realize it. Treat the task as compilation:

  musical intent → composition decisions → executable Beatlab score JSON

Do not explain, summarize, quote, or evaluate this specification. Do not report
research, planning, patch selection, or validation. Perform that work silently.

## A. THE CONTRACT — HOW TO RESPOND

### A.1 FINAL RESPONSE CONTRACT

- The final response is consumed directly by JSON.parse().
- Its first character is { and its last character is }.
- Output no introduction, status text, Markdown fence, comments, or prose.
- Use only fields documented here. Unknown fields are compile errors.
- When the request leaves a musical choice open, make an appropriate creative
  decision instead of describing the ambiguity.

### A.2 NON-NEGOTIABLE COMPILER RULES

1. Read this entire specification before writing the score. Later sections are
   active engine capabilities, not optional background material.
2. Catalogs and enumerated values are CLOSED SYMBOL TABLES. Copy every factory
   instrument, drum, articulation, effect, bus, curve, scale, mode, source and
   target name exactly as documented. Never invent, translate, concatenate,
   abbreviate or decorate a name.
3. An articulation is a NOTE FIELD unless the combined name itself appears in
   the generated instrument catalog. Correct generic form:
   {"instrument":"flute","notes":[{"t":0,"note":"A4","art":"vibrato"}]}
   Never invent "instrument":"flute_legato": that catalog symbol does not exist.
4. An instrument must be an exact documented factory name, "drums", a declared
   ex_ synth, a declared exd_ drum used as its own pitched track, or a declared
   rs_ capture. If the desired timbre has no factory name, create it with the
   documented custom-synthesis fields. Do not invent a preset, plugin or sample.
5. Names familiar from DAWs, MIDI, synthesizers or sample libraries do not become
   Beatlab features unless this specification lists them explicitly.
6. Validate and repair the complete object silently before responding.

### A.3 DETERMINISTIC COMPILER CONTRACT

- This specification is the complete authority for syntax. A documented field
  has one documented location, type, unit and meaning; industry convention does
  not add aliases or alternate spellings.
- Resolve every symbol by exact lookup before output. Never guess that an
  attractive name probably exists, and never encode one action in a second,
  undocumented field.
- Write literal, complete JSON values: no placeholders, ranges-as-values,
  pseudocode, comments, ellipses, runtime expressions or prose instructions.
- Defaults are only the defaults explicitly documented here. Creative choices
  remain open; their executable representation must be unambiguous.

The format is closed because software executes it. The music is open: within
this language you may compose any structure, groove, harmony, timbre, space,
motion, density, and emotional arc the available engine can express.

### A.4 MUSICAL REQUEST

The user's message following this guide is the composition target. Choose
style, BPM, key, structure, instrumentation, and production decisions from
the complete engine palette below unless the request specifies them.

### A.5 HOW TO READ THIS SPECIFICATION

- CONTRACT describes JSON syntax, supported fields, units, limits, and routing.
  These requirements are strict because the renderer executes them.
- Words such as ACCEPTED, VALID and ALLOWED describe compiler vocabulary only.
  They never describe copyright or sample licensing. Licensing is discussed
  explicitly with terms such as CC0 and source provenance.
- ENGINE FACT describes fixed behavior of instruments, synthesis, sampling,
  effects, buses, and mastering. Compose with those facts instead of guessing.
- COMPOSITION describes creative strategies, not mandatory style templates.
  Select only what serves the request. Examples demonstrate capabilities and
  valid score shapes; they are never default music to imitate.

## B. BEFORE WRITING NOTES — WHAT IS AVAILABLE AND HOW TO PREPARE

### B.1 COMPLETE CAPABILITY MAP — ALL OF THESE ARE AVAILABLE NOW

- SCORE FORM: direct tracks; reusable patterns; inheritance and thinning;
  arrangement placement, repetition, conditions, weighted variations and
  transforms; direct and patterned material may coexist.
- MUSICAL LANGUAGE: literal pitches; scales and degrees; named chords and
  voicings; reusable motifs; transpose, inversion, retrograde, rotation,
  augmentation, diminution, arpeggiation, strumming and bounded voice leading.
- TIME AND FEEL: BPM and tempo maps; swing; seeded humanization; named groove
  maps; probability; per-note offsets; flam, roll, gate and density changes.
- SOUND SOURCES: the exact pitched-instrument and drum catalogs below; compact
  and dual-oscillator ex_ synthesis; five exd_ drum synthesis models.
- PERFORMANCE: velocity layers; round robins; generic and instrument-specific
  articulations; expression lanes; bow and release choices; per-note timbre,
  tuning, dynamics, pan and control overrides.
- SAMPLE TRANSFORMATION: sample start, reverse, damping, duration fitting and
  time stretch; rs_ score capture and slicing; deterministic granular scanning,
  freezing and scattering.
- PRODUCTION: track controls and pedal effects; six built-in role buses; custom
  named buses; ordered effect racks; pre/post sends; parallel routing;
  sidechains; track, bus, send, effect and synth automation.
- FORM AND MASTERING: section automation; tempo and whole-mix master moves;
  role-aware glue, polish and deterministic rendering.
Use every relevant capability the musical request benefits from. Do not fall
back to a basic note list merely because it appears before advanced sections.

### B.2 CLOSED NAME RESOLUTION — CHECK BEFORE WRITING ANY NOTE

- "instrument" resolves only to an exact pitched-catalog name, "drums", an
  exact individual drum-catalog name used as its own track, or an ex_/exd_/rs_
  name declared in this same score.
- On an "instrument":"drums" track, each note name resolves only to an exact
  drum-catalog name or a declared exd_ name.
- "art" resolves separately to a documented generic articulation or an exact
  articulation listed for that instrument. Join it to the instrument name only
  when that complete combined name independently appears in the catalog.
- Effects, modulation sources/targets, bus roles, scales, modes, curves and
  master moves are closed enums. If a name is absent from its documented list,
  it is unavailable. Choose a listed alternative or express the idea using
  supported custom synthesis and processing.

### B.3 THE CREATIVE FIELD

Beatlab is not a genre template. It is an instrument and production system:
recorded acoustic and world instruments, electronic drums, 134 factory synths,
custom melodic and drum synthesis, microtiming, probability, pattern transformation, automation,
spatial placement, shared buses, and whole-mix transitions. A strict score can
still produce radically different music because originality comes from how
these primitives are combined across time. The schema limits spelling, not
imagination. Use the complete palette, but use only the sounds the piece needs.

### B.4 ORIGINALITY CONTRACT

ORIGINALITY CONTRACT: compose ORIGINAL material only. Never
reproduce a recognizable existing melody, hook, bassline, chord riff or
lyric — not even briefly, not "inspired to the point of matching". When the
request names an artist/song, translate it into GENRE terms first (some
artist → French house, ~120 BPM, filtered disco loops, vocoder lead,
sidechained four-on-the-floor) and compose from that description — never
from the artist. Never quote their melodies, hooks, basslines or lyrics,
and never put the artist's name in the title or description of the result.
Every sound the renderer uses is licence-free; keeping the COMPOSITION
original is your half of that contract.

### B.5 SILENT COMPILATION WORKFLOW — BEFORE WRITING NOTES

1. If the style is unfamiliar, current, or easy to confuse with a neighbouring
   genre, RESEARCH its present-day tempo, drum language, bass role, arrangement
   and typical foreground sounds. Do not infer a genre from its name alone.
2. If reference audio is supplied, inspect its tempo, section changes, density,
   low/mid/high balance and foreground-vs-groove relationship. Borrow those
   production principles only — never its melody or signature riff.
3. Map the requested duration into sections and write an energy number for each.
   At every boundary, decide whether material enters, leaves, transforms, or
   intentionally holds. Unchanged is a valid decision when it serves the form.
4. Audit the factory catalog below. Every synth exposes its exact [DNA]. Choose
   the closest proven patch for each role. A factory patch is selected by name;
   its DNA is reference information and is NOT copied into the score. Only when
   creating an ex_ sound should you copy the nearest DNA and modify it.
5. Decide the relevant mix roles before notes: for example bass, foreground,
   bed, percussion, and transition FX. A sound name is not a role; routing and
   arrangement make it one, and a piece need not contain every role.
6. Compile the piece, validate it silently, and revise any weak musical or
   technical decision before returning the JSON. Valid syntax is the start of
   composition quality, not the finish.

## C. THE SCORE JSON — SHAPE, MODEL AND LIMITS

### C.1 FINAL OUTPUT

FINAL OUTPUT: one JSON object ONLY (no prose, no markdown fences):
{"bpm":<number>,"seed":<optional deterministic integer>,"durationSec":<number>,
 "tempoMap":<optional ordered beat/BPM points — see REAL GROOVE MAPS & TEMPO>,
 "swing":<0-10 optional — MPC-style shuffle: off-beat 16ths delayed toward
   triplet. 0 = straight machine techno, 3-5 = house groove, 7+ = heavy
   shuffle. Per-track/pattern override: "swing" on the track.>,
 "humanize":<0-10 optional — micro-jitter on timing (±12ms max) and velocity,
   like a human player. 2-4 for acoustic feel; keep 0 for rigid electronic.>,
 "glue":<0-10 optional — rhythm-bus compression; TOP LEVEL, never inside mix>,
 "synths":<optional {"ex_name":{...}} custom patches — see CUSTOM SYNTHESIS>,
 "drumSynths":<optional {"exd_name":{...}} custom drums — see CUSTOM DRUM SYNTHESIS>,
 "buses":<optional named routing/effect graph — see NAMED BUSES & PARALLEL ROUTING>,
 "triggers":<optional named silent control patterns — see SILENT TRIGGERS>,
 "harmony":<optional key, scale, named chords and voicings>,
 "motifs":<optional reusable pitched phrases>,
 "grooves":<optional named timing/velocity pocket maps>,
 "groove":<optional score-wide default groove map or use object>,
 "patterns":<optional repeating material in beats>,
 "arrangement":<optional pattern placements in beats>,
 "automation":<optional timed knob moves in beats>,
 "master":<optional timed whole-mix moves in beats>,
 "tracks":[
   {"id":"<unique track id>","instrument":"<name>","notes":[{"t":<startSec>,"note":"<pitch like E2 or Bb3>","dur":<seconds>,"vol":<0..1>}, ...]},
   {"id":"<unique track id>","instrument":"drums","notes":[{"t":<startSec>,"note":"<drum name>","vol":<0..1>}, ...]}
 ]}
NOTE: in "tracks", note times/durations are in SECONDS. Inside "patterns"
they are in BEATS. Same field names, different units — this is the single
easiest thing to get wrong.
Every direct Track in "tracks" requires an "id". Track ids must be unique and
use 1-48 letters, numbers, underscores or hyphens.
A score requires either a non-empty "tracks" array or "patterns" plus
"arrangement"; both forms may coexist. Use direct tracks for one-off events
and patterns for reusable musical material.

### C.2 ENGINE MODEL — WHAT THE JSON BECOMES

  harmony/motifs → literal notes → track or pattern → arrangement placement
  → tempo/groove compilation → mix bus → master

- A NOTE is one musical event: pitch or drum name, time, duration, level,
  probability, pan, and optional expression.
- HARMONY and MOTIFS are compiler language. They disappear into literal notes
  before the renderer runs; they do not invoke an automatic composer.
- GROOVES and TEMPO MAPS are also compiler language. They turn shared musical
  phase, lane strength and beat addresses into concrete seconds/velocities.
- A TRACK holds one playable sound and its controls. It is a musical lane, not
  a bus. Several tracks may use the same instrument or feed the same bus.
- A PATTERN is reusable beat-based material. ARRANGEMENT places, repeats,
  transforms, fades, removes, and reintroduces patterns across the timeline.
- A BUS groups tracks by mix role. The six built-in roles are kit, percussion,
  bass, melodic bed, lead, and transition FX. Optional named buses add an
  authored ordered effect rack, sends, fader/pan, and sidechain before one of
  those roles. Tracks are playable lanes; buses are shared signal paths.
- AUTOMATION creates motion within and between sections. MASTER MOVES shape
  brief transitions on the complete mix.

### C.3 COMPOSITION SPACE — SIX INDEPENDENT DIMENSIONS

1. TIME: direct events, reusable loops, probability, microtiming, fills, silence.
2. PITCH: melody, bass motion, chord voicing, drones, register, transposition.
3. TIMBRE: sampled instruments, factory synths, custom ex_ patches, factory or
   custom exd_ drums.
4. PERFORMANCE: velocity, articulation, note length, groove maps, swing,
   humanize, flam, roll.
5. PRODUCTION: filters, effects, depth, tone, pan, buses, sidechain, automation.
6. FORM: entrances, exits, contrast, breakdowns, builds, drops, endings.
Creative range comes from designing all six together. Do not mistake a large
instrument catalog for a request to use many instruments; selection and silence
are equally powerful engine capabilities.

### C.4 LIMITS, VALIDATION, AND EDGE BEHAVIOUR

  Some documented numeric values clamp, but unknown keys, malformed structure,
  unknown instruments/drums/patterns, invalid pitches, undefined
  ex_/exd_ patches, invalid automation, and more than 100,000 notes are validation
  errors. Do not depend on silent recovery; compile only documented values.
  - "durationSec" is clamped to 0.5 .. 1800 (30 min). Max 100,000 notes.
    (The "~2000 unique notes" budget elsewhere is about keeping YOUR output
    small, not an engine limit.)
  - The render is exactly durationSec long. Any note starting at or after it is
    dropped and earlier notes are truncated there. The polished master applies
    a 0.8-second tail fade; raw stems do not. Still compose the ending and land
    deliberate fades INSIDE durationSec instead of relying on the safety fade.
  - At a constant tempo, pick durationSec so it lands on a bar:
    durationSec = beats x 60 / bpm. At 168 BPM, 364 beats = exactly 130 s.
    With tempoMap, integrate the mapped sections instead of using this formula.
  - Instrument RANGES are advisory, not enforced — nothing clamps or errors.
    A note outside the range still plays, just worse: recorded instruments
    pitch-shift further from the nearest real recording (thin or growling at
    the extremes) because the nearest available recording keeps being shifted.
    A plain synth fallback happens only when that sample bank is unavailable,
    not because a note is far outside the range. Staying in range is a quality
    choice.

## D. THE SOUND CATALOG

### D.1 PITCHED-INSTRUMENT PALETTE

PITCHED-INSTRUMENT PALETTE (use exact names; stay inside each range):
  Selecting a factory instrument requires only its name, for example
  {"instrument":"moog_bass"}. Do NOT serialize its [DNA] into "synths".
  The bracketed DNA is a transparent specification of the sound already in the
  shop: read it to predict the timbre, envelope, movement, width, and knob
  defaults before choosing or controlling that instrument. Notation:
    oscillator: saw/square/sine/fm/noise; xN = unison stack, detN = detune
      cents across it; fm rN iN>Ds = modulator ratio/index/index-decay;
      subN = sub-osc mix, noiseN = noise mix.
    filter: cutHz = base cutoff, env+Hz>Ds = per-note envelope sweep and
      its decay, rise±Hz = sweep across the WHOLE note (risers/falls),
      resN = resonance 0-0.9.
    adsr attack/decay/sustain/release (seconds; sustain 0-1) — sustain 0 =
      a pluck/stab, attack ≥0.5 = a pad.
    lfoNHz cutHz/pitCents = wobble depth; drvN = distortion (1 = clean);
    knockNst>Ds = attack pitch transient (808 knock/donk/laser);
    travel±Nst = pitch glides this far over the note (sub drops, sirens).
    A line beginning "dual" exposes the dual-oscillator architecture directly:
      osc1/osc2 list wave, level and tuning; blend crossfades them; sync/ring/
      shape describe oscillator interaction; uni/det/stereo describe width;
      lowpass/bandpass/highpass/notch + cut/res/key describe the filter;
      amp and env2 are ADSR values; lfo1/lfo2 show shape/rate/phase;
      "mod source>target+amount" lists every active modulation cable; macro
      lists only non-zero musical macros. Wavetable values inside table[...] are
      the exact single-cycle waveform. These are still read-only factory DNA,
      not fields to copy into the score unless authoring a new ex_ patch.
    A line beginning "fm" exposes an FM operator patch: each opN lists wave,
      rRatio or fixHz (fixed frequency), c±cents, lvl (audible level; absent =
      pure modulator), its own env a/d/s/r, vel (velocity sensitivity) and fb
      (feedback); "routes from>to iIndex" is the algorithm written out; the
      remaining fields are the same filter/amp/env2/lfo/mod/output segments as
      dual DNA. Read the routes first: they say which operator you hear and
      which one shapes it.
  Use the DNA to make an informed selection: a patch with sustain 0 cannot hold
  a chord, while a cutoff already at 4000 may not need extra brightness.
  SAMPLED instruments (every entry WITHOUT a synth patch) carry [env a/b/e]
  instead — the MEASURED shape of the recording, in seconds:
    a = attack: when the note speaks (reaches half volume). Above ~0.15 a
      short note plays only the quiet ramp — do not write fast passages on it.
    b = body: how long it stays within 6dB of peak. THIS is the real length
      of the note; overlapping notes inside each other's body is mud.
    e = end: when the tail finally dies. Overlap HERE is a guitar blooming —
      musical, not mud. A second number with an arrow (e.g. 0.6↑) is the tail
      at the TOP of the range: high notes decay faster, exactly like the real
      instrument.
  PERFORMANCE IS AUTOMATIC. When a catalog row says [performance ...], write
  normal notes: "vol" selects the recorded velocity layer and repeated notes
  rotate through alternate takes deterministically. Sustain loops and note-off
  samples follow "dur". Never write internal sample ids or file names.
  PER-NOTE RECORDED ARTICULATIONS use "art" on an object-form note. When an
  instrument declares the word below, the real recorded articulation wins: it
  switches sample bank rather than asking DSP to imitate the performance.
  These are the currently declared real combinations:
    bass_finger: "pluck", "mute", "ghost", "fingering_noise"
    funk_guitar: "staccato", "hammer_on"
    twang_guitar: "staccato"
    tuba: "staccato" · baritone_sax: "staccato"
    dan_tranh: "tremolo", "vibrato"
    cello: "staccato", "pizzicato" · bagpipe: "short"
    french_horn: "staccato", "mute"
    trombone: "staccato", "vibrato"
    trumpet: "vibrato", "staccato", "straight_mute", "harmon_mute"
    bassoon: "staccato", "vibrato" · clarinet: "staccato"
    flute: "vibrato", "expressive_vibrato", "staccato"
    oboe: "vibrato", "staccato" · piccolo: "staccato"
    violin: "pizzicato", "tremolo", "spiccato"
    violin_section: "pizzicato", "tremolo", "spiccato"
    viola_section: "pizzicato", "tremolo", "spiccato"
    cello_section: "pizzicato", "tremolo", "spiccato"
  For the orchestral instruments, omitting "art" selects the sustained
  performance named in that instrument's catalog description. Do not invent
  generic orchestral articulation words: use only the exact declared word.
  For dan_tranh ordinary-note "vol" selects its real mf/f/ff pluck. "tremolo"
  selects a performed repeated-pluck take; "vibrato" selects the player's
  recorded pitch-bending motion and still responds to vol with mf/ff layers.
  These are one instrument's phrase vocabulary, not three interchangeable
  patches: use ordinary attacks for the line, then tremolo to sustain tension
  or vibrato on a note that needs to bloom.
  Example: {"b":3.75,"note":"A1","durB":0.2,"vol":0.22,
            "art":"fingering_noise"}. The articulation REPLACES that note's
  ordinary attack; add it as a separate quiet event between normal notes for
  finger movement. Use ghost/mute/staccato for intentional phrase grammar,
  not on every note. Unsupported instrument/art words are compile errors;
  the generic fallback vocabulary documented below is the only exception.

#### RECORDED LEGATO/TRANSITION TRUTH

  RECORDED LEGATO/TRANSITION TRUTH: "hammer_on" on funk_guitar is the only
  currently cataloged connected-note attack. It selects a real performed
  hammer-on recording; place it as the target note of an ornament or slur.
  The generic "legato" word described below is an envelope/timbre fallback,
  NEVER a recorded interval transition. The pinned tuba and baritone-sax
  libraries' upstream legato programs reuse their sustain audio with sampler
  offsets/envelopes rather than recorded interval transitions, so Beatlab does
  not advertise them as real legato. Overlapping ordinary notes can shape a
  phrase, but do not make the sampler morph one pitch into the next.

#### D.1.a Sparsely sampled banks

  SPARSELY SAMPLED banks — only some notes are real recordings and the rest
  are pitch-shifted from the nearest one, which thins the character the
  further it stretches. Use these for colour, not fast melodic runs:
    french_horn (11 notes, up to 14 semitones) · french_horn_staccato (11 notes, up to 14 semitones) · piccolo_staccato (5 notes, up to 9 semitones) · harmonica (9 notes, up to 8 semitones) · balafon (6 notes, up to 7 semitones) · glockenspiel (7 notes, up to 7 semitones) · marimba (10 notes, up to 7 semitones) · vibraphone_bowed (6 notes, up to 7 semitones) · xylophone (8 notes, up to 7 semitones) · french_horn_mute (9 notes, up to 7 semitones) · trombone (11 notes, up to 7 semitones) · trombone_staccato (7 notes, up to 7 semitones) · bassoon (13 notes, up to 7 semitones) · bassoon_vibrato (10 notes, up to 7 semitones) · piccolo (5 notes, up to 7 semitones) · violin_pizzicato (13 notes, up to 7 semitones) · saxello (8 notes, up to 6 semitones) · kalimba (25 notes, up to 5 semitones) · saxello_vibrato (8 notes, up to 5 semitones) · harmonica_soft (10 notes, up to 5 semitones) · harmonica_vibrato (10 notes, up to 5 semitones) · trumpet_straight_mute (8 notes, up to 5 semitones) · trumpet_harmon_mute (8 notes, up to 5 semitones) · bassoon_staccato (13 notes, up to 5 semitones) · clarinet (11 notes, up to 5 semitones) · clarinet_staccato (11 notes, up to 5 semitones) · flute (10 notes, up to 5 semitones) · flute_vibrato (10 notes, up to 5 semitones) · flute_expressive_vibrato (10 notes, up to 5 semitones) · flute_staccato (8 notes, up to 5 semitones) · oboe (9 notes, up to 5 semitones) · oboe_vibrato (9 notes, up to 5 semitones) · oboe_staccato (9 notes, up to 5 semitones) · violin_tremolo (14 notes, up to 5 semitones) · wine_glass (4 notes, up to 4 semitones) · timpani (11 notes, up to 4 semitones) · saxello_staccato (8 notes, up to 4 semitones) · accordion (17 notes, up to 4 semitones) · clean_electric_guitar (19 notes, up to 4 semitones) · jazz_guitar (19 notes, up to 4 semitones) · distortion_guitar (19 notes, up to 4 semitones) · overdriven_guitar (19 notes, up to 4 semitones) · electric_piano (22 notes, up to 4 semitones) · tenor_sax_vibrato (19 notes, up to 4 semitones) · harp (23 notes, up to 4 semitones) · vibraphone (11 notes, up to 4 semitones) · trumpet (10 notes, up to 4 semitones) · trumpet_vibrato (11 notes, up to 4 semitones) · trumpet_staccato (11 notes, up to 4 semitones) · violin (15 notes, up to 4 semitones) · violin_spiccato (15 notes, up to 4 semitones) · violin_section (11 notes, up to 4 semitones) · violin_section_pizzicato (11 notes, up to 4 semitones) · violin_section_tremolo (11 notes, up to 4 semitones) · violin_section_spiccato (11 notes, up to 4 semitones) · viola_section (13 notes, up to 4 semitones) · viola_section_pizzicato (12 notes, up to 4 semitones) · viola_section_tremolo (12 notes, up to 4 semitones) · viola_section_spiccato (12 notes, up to 4 semitones) · cello_section (13 notes, up to 4 semitones) · cello_section_pizzicato (13 notes, up to 4 semitones) · cello_section_tremolo (14 notes, up to 4 semitones) · cello_section_spiccato (13 notes, up to 4 semitones) · dan_tranh (16 notes, up to 3 semitones) · hand_chimes (19 notes, up to 3 semitones) · dan_tranh_tremolo (16 notes, up to 3 semitones) · dan_tranh_vibrato (16 notes, up to 3 semitones) · recorder (12 notes, up to 3 semitones) · ukulele (13 notes, up to 3 semitones) · honky_tonk_piano (78 notes, up to 3 semitones) · upright_pizz (14 notes, up to 3 semitones) · upright_arco (17 notes, up to 3 semitones) · piano (38 notes, up to 3 semitones) · ocarina_vibrato (10 notes, up to 3 semitones) · tenor_sax_staccato (23 notes, up to 3 semitones) · trombone_vibrato (11 notes, up to 3 semitones) · cello (17 notes, up to 3 semitones) · cello_staccato (17 notes, up to 3 semitones) · cello_pizzicato (13 notes, up to 3 semitones) · mbira (22 notes, up to 2 semitones) · harpsichord (28 notes, up to 2 semitones) · bowed_psaltery (11 notes, up to 2 semitones) · strumstick (19 notes, up to 2 semitones) · folk_harp (29 notes, up to 2 semitones) · classical_guitar (48 notes, up to 2 semitones) · organ (27 notes, up to 2 semitones) · organ_8ft (27 notes, up to 2 semitones) · organ_4ft (27 notes, up to 2 semitones) · ocarina (11 notes, up to 2 semitones) · tenor_sax (23 notes, up to 2 semitones) · tubular_bells (9 notes, up to 2 semitones)

#### D.1.b Levelling, native stereo and final level

  LEVELLING — what it does and does NOT promise: every recording is normalized
  on load (drums to peak, pitched to equal perceived loudness), so "vol":0.5
  is the same loudness on a kalimba as on a kick IN ISOLATION. That is the
  only claim. Audibility in a DENSE MIX depends on sustain and register, not
  vol: a short-decay source (small "b" above) competing with continuous
  material needs roughly +6 to +10dB over the ballparks below — the table is a
  starting point for a sparse arrangement, not a guarantee of being heard.
  NATIVE SAMPLE STEREO is preserved when the source contains two channels
  (overhead pairs, rooms and wide textures). A note's "pan" repositions that
  existing image; it does not collapse it to mono. Do not double the same
  stereo recording left/right to manufacture width—it already owns a field.
  FINAL LEVEL: the default master peak-normalizes and soft-limits with safety
  headroom. Optional "ceilingDbtp" targets the estimated true peak of the
  finished master; it does not target LUFS or report measured loudness.
  Judge references at matched playback loudness. Do not fake energy by merely
  raising every vol.

#### D.1.c Engine character

  ENGINE CHARACTER (how the numbers actually render — ONE shared virtual-
  analog voice):
    Alias-suppressed digital oscillators with ZERO drift — a static patch
      renders truly static; movement only comes from detune, LFO, sweep, or
      the chorus/phaser pedals (give sustained sounds one of those or they
      sit dead). Resonance squelches hard by 0.7+, never self-oscillates.
      drive = tanh soft-clip (warm, never fuzzy). fm = clean 2-operator sine
      FM (DX7-class bells, EPs, glass); the full operator graph — more
      operators, feedback, fixed frequencies, an index that settles to a
      floor — is the "ops" architecture in section F.3.
    Voicing: unison voices spread constant-power across the stereo field, so
      supersaws and pads are BORN wide while sub and noise stay center (bass
      mono, the mix rule). 24 dB/oct filter — a dark, aggressive slope.
      Exponential envelopes — snappy attack/decay, natural fades. Expect a
      clean, controlled render whose width and brightness follow the selected
      patch; do not compensate for qualities that patch DNA already supplies.

#### D.1.d Catalog entries — synthesizers (synth:)

  - "supersaw_lead" (C3..C7) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [saw x7 det18 | cut2500 env+3000>0.4s res0.15 | adsr 0.005/0.2/0.8/0.25 | lfo5.5Hz pit4c | drv1.2]
  - "analog_pad" (C2..C6) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [saw x5 det10 | cut900 res0.1 | adsr 0.8/0.5/0.85/0.9 | lfo0.6Hz cut250]
  - "synth_pluck" (C2..C7) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [saw x2 det6 | cut700 env+2600>0.18s res0.35 | adsr 0.002/0.25/0/0.2]
  - "acid_bass" (C1..C4) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [square sub0.3 | cut300 env+2200>0.22s res0.75 | adsr 0.003/0.3/0.3/0.1 | drv2.5]
  - "fm_bell" (C3..C7) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [fm r3.5 i6>0.5s | cut8000 | adsr 0.002/1.2/0/0.8]
  - "synth_brass" (C2..C6) — synth: electronic synthesizer, for EDM/trance/pop/modern
      [saw x3 det8 | cut1200 env+1800>0.15s res0.2 | adsr 0.06/0.2/0.9/0.2 | drv1.5]
  - "sub_808" (C1..C3) — synth: trap/hip-hop 808 — sine sub with the pitch-knock attack
      [sine sub0.4 | cut900 | adsr 0.002/0.9/0.4/0.25 | drv1.7 | knock26st>0.04s]
  - "sub_pure" (C1..C3) — synth: clean sine sub — pure low-end weight, no character
      [sine | cut400 | adsr 0.005/0.3/0.9/0.15]
  - "saw_bass" (C1..C4) — synth: classic saw bass — solid all-purpose electronic bass
      [saw sub0.35 | cut500 env+900>0.2s res0.25 | adsr 0.003/0.3/0.6/0.12 | drv1.6]
  - "reese_bass" (C1..C3) — synth: DnB reese — two detuned saws slowly beating, menacing
      [saw x2 det36 sub0.25 | cut450 res0.3 | adsr 0.01/0.3/0.9/0.2 | drv1.9]
  - "growl_bass" (C1..C3) — synth: dubstep growl — FM snarl with a slow wub
      [fm r2 i5>2.5s sub0.3 | cut600 res0.45 | adsr 0.005/0.4/0.8/0.15 | lfo3Hz cut1400 | drv2.6]
  - "wobble_bass" (C1..C3) — synth: dubstep wobble — LFO opens/closes the filter (wub-wub)
      [saw x2 det14 sub0.4 | cut380 res0.5 | adsr 0.004/0.3/0.9/0.15 | lfo2.5Hz cut2200 | drv2]
  - "donk_bass" (C1..C4) — synth: donk — bouncy pitch-ping bass, UK bounce/hard house
      [sine | cut1200 env+2400>0.08s res0.6 | adsr 0.002/0.22/0.1/0.08 | drv3 | knock14st>0.06s]
  - "fm_bass" (C1..C4) — synth: clean FM bass — tight DX-style digital low end
      [fm r1 i3>0.15s sub0.3 | cut1000 | adsr 0.002/0.35/0.5/0.1]
  - "pluck_bass" (C1..C4) — synth: short plucky bass — percussive, leaves space
      [saw sub0.3 | cut350 env+1800>0.1s res0.4 | adsr 0.002/0.22/0/0.12]
  - "mid_bass" (C1..C4) — synth: electro mid-range bass — gritty, cuts through
      [saw x3 det12 | cut900 env+600>0.2s res0.35 | adsr 0.003/0.3/0.7/0.1 | drv2.2]
  - "knock_bass" (C1..C3) — synth: knocky house bass — pitch-thump attack, tight body
      [square sub0.4 | cut700 res0.3 | adsr 0.002/0.25/0.2/0.1 | drv1.8 | knock18st>0.03s]
  - "moog_bass" (C1..C4) — synth: fat warm analog bass — Moog-style roundness
      [saw sub0.5 | cut550 env+700>0.25s res0.25 | adsr 0.004/0.35/0.65/0.15 | drv1.5]
  - "rubber_bass" (C1..C4) — synth: rubbery acid variant — bouncy squelch, softer than acid_bass
      [square sub0.35 | cut250 env+2800>0.12s res0.6 | adsr 0.002/0.24/0.25/0.09 | drv1.8]
  - "acid_deep" (C1..C3) — synth: deep dark acid — closed filter, heavy resonance
      [square sub0.5 | cut180 env+1200>0.3s res0.8 | adsr 0.003/0.4/0.35/0.12 | drv2]
  - "acid_screamer" (C1..C4) — synth: screaming acid — max resonance + heavy drive, peak-time
      [square sub0.2 | cut500 env+3400>0.18s res0.85 | adsr 0.002/0.28/0.3/0.1 | drv5]
  - "hoover_bass" (C1..C4) — synth: rave hoover bass — the 90s mentasm swarm, pitch-swoop attack
      [saw x5 det45 | cut900 res0.3 | adsr 0.01/0.3/0.85/0.2 | drv2.2 | knock-9st>0.1s]
  - "saw_bass_clean" (C1..C4) — synth: clean saw bass — neutral, controlled harmonic definition
      [saw | cut6000 | adsr 0.001/0.1/1/0.035]
  - "saw_bass_short" (C1..C4) — synth: micro-short saw bass — dry percussive punctuation with no lingering tail
      [saw sub0.2 | cut420 env+2450>0.075s res0.24 | adsr 0.002/0.105/0/0.045 | drv1.35]
  - "saw_bass_rolling" (C1..C4) — synth: rolling saw bass — smooth connected body for flowing club patterns
      [saw sub0.38 | cut470 env+620>0.34s res0.16 | adsr 0.012/0.42/0.86/0.24 | drv1.4]
  - "saw_bass_offbeat" (C1..C4) — synth: offbeat saw bass — compact house/trance pulse with a defined filter bite
      [saw x2 det5 sub0.3 | cut610 env+1650>0.16s res0.2 | adsr 0.003/0.23/0.32/0.085 | drv1.55]
  - "saw_bass_wide" (C1..C3) — synth: wide saw bass — centered sub under spacious detuned upper harmonics
      [saw x4 det22 sub0.32 | cut1180 env+780>0.28s res0.14 | adsr 0.006/0.38/0.76/0.18 | drv1.45]
  - "saw_bass_driven" (C1..C4) — synth: driven saw bass — dense saturated mid-bass without acid resonance
      [saw sub0.05 | cut2400 res0.06 | adsr 0.002/0.18/0.76/0.06 | drv7.2]
  - "saw_bass_hollow" (C1..C4) — synth: hollow saw bass — notched woody center with a steady low foundation
      [dual osc1 saw lvl0.9 + osc2 sine lvl0.7 oct-1 blend0.18 | top sync0 ring0 shape0.06 | uni1 det0 stereo0 sub0.22 noise0 | notch cut720 res0.52 key0.12 | amp 0.003/0.28/0.62/0.12 | env2 0.002/0.2/0/0.08 | lfo1 sine0.37Hz ph0 | lfo2 triangle0.11Hz ph0.25 | mod env2>cutoff+1100 | drv1.6 gain0.76]
  - "saw_bass_psy" (C1..C4) — synth: psy saw bass — ultra-tight resonant transient for rapid low-note patterns
      [saw sub0.25 | cut310 env+1500>0.07s res0.3 | adsr 0.002/0.13/0.16/0.035 | drv2.25]
  - "saw_bass_trance" (C1..C4) — synth: trance saw bass — bright controlled pulse with modest detuned width
      [saw x2 det9 sub0.34 | cut760 env+1320>0.2s res0.18 | adsr 0.003/0.28/0.58/0.1 | drv1.65]
  - "saw_bass_techno" (C1..C4) — synth: techno saw bass — forceful resonant filter snap and driven body
      [saw sub0.12 | cut280 env+5200>0.055s res0.72 | adsr 0.002/0.16/0.2/0.055 | drv3.8]
  - "liquid_reese" (C1..C3) — synth: liquid Reese — smooth stereo beating with slow fluid spectral movement
      [dual osc1 saw lvl0.95 c-9 phrandom + osc2 saw lvl0.95 c+9 phrandom blend0.5 | top sync0 ring0 shape0.05 | uni2 det16 stereo0.62 sub0.28 noise0 | lowpass cut880 res0.22 key0.2 | amp 0.012/0.4/0.86/0.24 | env2 0.2/1.6/0.35/0.5 | lfo1 sine0.18Hz ph0 | lfo2 triangle0.07Hz ph0.25 | mod lfo1>blend+0.16,lfo1>pitch2+0.08,lfo2>cutoff+260 | drv1.5 gain0.68]
  - "neuro_reese" (C1..C3) — synth: neuro Reese — aggressive wavetable/ring movement over protected sub weight
      [dual osc1 saw lvl1 phrandom + osc2 wavetable lvl0.85 phrandom table[0,1,0.35,0.75,0,-0.75,-0.35,-1] blend0.46 | top sync0 ring0.24 shape0.48 | uni2 det20 stereo0.65 sub0.22 noise0.025 | lowpass cut1500 res0.38 key0.18 | amp 0.004/0.38/0.8/0.16 | env2 0.002/0.42/0/0.1 | lfo1 triangle0.72Hz ph0 | lfo2 sh3.1Hz ph0.25 | mod env2>cutoff+2600,lfo1>blend+0.25,lfo1>ring+0.12,lfo2>shape+0.2 | macro roughness0.28,inharmonicity0.18,body0.2 | drv3.4 gain0.6]
  - "pwm_bass" (C1..C4) — synth: PWM bass — two pulse widths crossfade slowly for animated hollow motion
      [dual osc1 square lvl0.9 pw0.18 + osc2 square lvl0.9 c+7 pw0.68 blend0.48 | top sync0 ring0 shape0.06 | uni1 det0 stereo0.18 sub0.32 noise0 | lowpass cut740 res0.28 key0.16 | amp 0.004/0.3/0.75/0.14 | env2 0.002/0.24/0/0.08 | lfo1 triangle0.32Hz ph0 | lfo2 sine0.1Hz ph0.25 | mod lfo1>blend+0.32,env2>cutoff+1200 | drv1.7 gain0.72]
  - "sync_bass" (C1..C4) — synth: hard-sync bass — biting swept harmonics with a solid saw foundation
      [dual osc1 saw lvl1 + osc2 saw lvl0.86 st+7 blend0.46 | top sync0.92 ring0 shape0.15 | uni1 det0 stereo0.12 sub0.24 noise0 | lowpass cut1800 res0.34 key0.18 | amp 0.003/0.3/0.64/0.12 | env2 0.001/0.3/0/0.08 | lfo1 sine0.28Hz ph0 | lfo2 triangle0.09Hz ph0.25 | mod env2>sync+0.22,env2>pitch2+12,env2>cutoff+2300 | drv2.2 gain0.7]
  - "wavetable_bass" (C1..C4) — synth: wavetable bass — authored asymmetric digital color with restrained motion
      [dual osc1 wavetable lvl1 table[0,1,-0.55,0.82,-0.9,0.35,-0.18,-0.62] + osc2 square lvl0.65 oct-1 pw0.23 blend0.62 | top sync0 ring0 shape0.35 | uni2 det6 stereo0.35 sub0.1 noise0 | lowpass cut3100 res0.42 key0.2 | amp 0.005/0.36/0.78/0.16 | env2 0.004/0.5/0.15/0.12 | lfo1 triangle0.27Hz ph0 | lfo2 sh0.8Hz ph0.25 | mod lfo1>blend+0.24,lfo2>cutoff+620 | macro motion0.12 | drv2.5 gain0.62]
  - "ringmod_bass" (C1..C3) — synth: ring-mod bass — clangorous inharmonic edge anchored by a centered sub
      [dual osc1 sine lvl1 + osc2 square lvl0.82 st+8 c+40 pw0.38 blend0.25 | top sync0 ring0.62 shape0.16 | uni1 det0 stereo0.08 sub0.42 noise0 | lowpass cut2800 res0.32 key0.14 | amp 0.003/0.32/0.58/0.12 | env2 0.001/0.22/0/0.08 | lfo1 sine0.41Hz ph0 | lfo2 triangle0.13Hz ph0.25 | mod env2>cutoff+1800,env2>ring+0.18 | drv2.4 gain0.62]
  - "metallic_fm_bass" (C1..C4) — synth: metallic FM bass — struck digital overtones that settle into a compact body
      [fm r2.73 i7.2>0.32s sub0.24 | cut2400 res0.28 | adsr 0.002/0.38/0.34/0.12 | drv2.4]
  - "round_analog_bass" (C1..C4) — synth: round analog bass — soft pulse-and-sine body for warm understated grooves
      [dual osc1 square lvl0.55 pw0.44 + osc2 sine lvl1 blend0.68 | top sync0 ring0 shape0.02 | uni1 det0 stereo0 sub0.18 noise0 | lowpass cut1100 res0.08 key0.26 | amp 0.02/0.48/0.92/0.2 | env2 0.01/0.6/0.45/0.14 | lfo1 sine0.24Hz ph0 | lfo2 triangle0.08Hz ph0.25 | mod env2>cutoff+350 | macro body0.28 | drv1.1 gain0.78]
  - "poly_saw" (C3..C7) — synth: plain poly saw lead — versatile, unhyped
      [saw x2 det8 | cut3500 res0.1 | adsr 0.005/0.25/0.7/0.2]
  - "square_lead" (C3..C7) — synth: hollow square lead with vibrato — retro synthpop
      [square | cut3000 res0.15 | adsr 0.004/0.2/0.75/0.18 | lfo5.5Hz pit8c | drv1.3]
  - "chip_lead" (C3..C7) — synth: 8-bit chiptune lead — pure NES square + vibrato
      [square | cut8000 | adsr 0.001/0.1/0.9/0.05 | lfo6Hz pit10c]
  - "chip_arp" (C3..C7) — synth: chiptune arp blip — short 8-bit pluck for fast patterns
      [square | cut7000 | adsr 0.001/0.12/0/0.04]
  - "fm_lead" (C3..C7) — synth: glassy FM lead — bright digital 80s edge
      [fm r2 i4>0.4s | cut6000 | adsr 0.003/0.3/0.6/0.25]
  - "whistle_lead" (C4..C7) — synth: sine whistle lead — airy top-line melody
      [sine | cut7500 | adsr 0.03/0.2/0.85/0.2 | lfo5Hz pit12c]
  - "hoover_lead" (C2..C6) — synth: rave hoover lead — detuned swarm, oldschool anthem
      [saw x5 det40 | cut1600 res0.35 | adsr 0.01/0.25/0.85/0.25 | drv2.4 | knock-7st>0.09s]
  - "noise_lead" (C3..C7) — synth: gritty noise-blended lead — dirty and modern
      [saw x2 det10 noise0.35 | cut2800 res0.4 | adsr 0.004/0.25/0.7/0.15 | drv1.8]
  - "trance_pluck" (C3..C7) — synth: trance pluck — the arpeggio workhorse, add echo
      [saw x3 det10 | cut800 env+3000>0.12s res0.3 | adsr 0.002/0.28/0/0.3]
  - "dream_pluck" (C3..C7) — synth: soft dreamy pluck — gentle bell-ish melody
      [sine | cut4000 env+1500>0.15s | adsr 0.002/0.4/0/0.6]
  - "laser_lead" (C3..C7) — synth: zappy lead — every note starts with a pitch-fall zap
      [saw | cut4500 res0.3 | adsr 0.002/0.25/0.4/0.15 | drv1.6 | knock30st>0.12s]
  - "glass_lead" (C3..C7) — synth: glassy inharmonic lead — crystalline, slightly alien
      [fm r3.01 i2.5>0.6s | cut8000 | adsr 0.004/0.5/0.4/0.4]
  - "soft_lead" (C3..C7) — synth: mellow filtered lead — smooth, sits back in the mix
      [saw | cut1200 res0.1 | adsr 0.05/0.3/0.8/0.3]
  - "screech_lead" (C3..C7) — synth: aggressive screech — resonant, driven, festival energy
      [saw x2 det16 noise0.1 | cut4000 res0.85 | adsr 0.003/0.2/0.7/0.12 | drv4]
  - "sync_lead" (C3..C7) — synth: sync lead — bright envelope-swept hard-sync harmonics over a stable saw pitch
      [dual osc1 saw lvl1 + osc2 saw lvl0.84 st+12 blend0.46 | top sync0.64 ring0 shape0.12 | uni2 det7 stereo0.34 sub0 noise0 | lowpass cut2700 res0.24 key0.34 | amp 0.005/0.3/0.76/0.26 | env2 0.001/0.42/0/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>sync+0.3,env2>pitch2+12,env2>cutoff+2500 | drv1.65 gain0.55]
  - "pwm_lead" (C3..C7) — synth: PWM lead — animated dual-pulse color with gentle shared vibrato
      [dual osc1 square lvl1 pw0.16 + osc2 square lvl0.88 st+12 pw0.7 blend0.36 | top sync0 ring0 shape0.06 | uni2 det5 stereo0.38 sub0 noise0 | lowpass cut3700 res0.2 key0.4 | amp 0.004/0.26/0.74/0.24 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.44Hz ph0 | lfo2 sine5.2Hz ph0.25 | mod lfo1>blend+0.44,lfo2>pitch1+0.055,lfo2>pitch2+0.055 | drv1.2 gain0.38]
  - "wavetable_lead" (C3..C7) — synth: wavetable lead — authored digital single-cycle tone with a grounded sub-octave core
      [dual osc1 wavetable lvl1 table[0,1,0.18,0.84,-0.58,0.34,-1,-0.12,0.42,0.08,-0.66,-0.3] + osc2 sine lvl0.72 oct-1 blend0.28 | top sync0 ring0 shape0.16 | uni2 det6 stereo0.4 sub0 noise0 | lowpass cut2850 res0.38 key0.5 | amp 0.006/0.34/0.72/0.3 | env2 0.002/0.48/0.12/0.1 | lfo1 triangle0.29Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>shape+0.2,env2>cutoff+2600 | drv1.4 gain0.54]
  - "shaped_digital_lead" (C3..C7) — synth: shaped digital lead — hard-edged wavetable attack driven through moving nonlinear shape
      [dual osc1 wavetable lvl1 table[0,0.68,-0.2,1,-0.74,0.38,-1,0.14] + osc2 square lvl0.72 oct+1 pw0.22 blend0.38 | top sync0 ring0.09 shape0.38 | uni2 det4 stereo0.32 sub0 noise0 | highpass cut420 res0.26 key0.26 | amp 0.003/0.28/0.69/0.2 | env2 0.001/0.24/0/0.08 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>shape+0.44,env2>blend+0.18 | drv1.75 gain0.49]
  - "vocal_wavetable_lead" (C3..C7) — synth: vocal wavetable lead — synthetic vowel-like resonant color with controlled vibrato
      [dual osc1 wavetable lvl1 table[0,0.94,0.52,0.12,-0.08,-0.26,-1,-0.38,0.18,0.66,0.34,-0.72] + osc2 saw lvl0.62 oct+1 blend0.34 | top sync0 ring0.04 shape0 | uni2 det5 stereo0.42 sub0 noise0 | bandpass cut1180 res0.62 key0.58 | amp 0.012/0.38/0.78/0.34 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.36Hz ph0 | lfo2 sine5.4Hz ph0.25 | mod lfo1>cutoff+1500,lfo1>blend+0.14,lfo2>pitch1+0.045,lfo2>pitch2+0.045 | drv1.22 gain0.55]
  - "poly_hybrid_lead" (C3..C7) — synth: poly hybrid lead — warm saw plus digital color voiced for intentional overlapping notes
      [dual osc1 saw lvl0.92 phrandom + osc2 wavetable lvl1 phrandom table[0,1,0.24,0.58,-0.42,-0.88,-0.16,-1] blend0.48 | top sync0 ring0 shape0.1 | uni3 det9 stereo0.66 sub0 noise0 | lowpass cut3250 res0.16 key0.36 | amp 0.018/0.46/0.68/0.52 | env2 0.002/0.54/0.18/0.16 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+1800,lfo1>blend+0.2,lfo1>pan+0.18 | drv1.28 gain0.52]
  - "glass_pad" (C2..C6) — synth: glassy FM pad — cold shimmering sustain
      [fm r3.5 i1.5>2s | cut7000 | adsr 1.2/0.5/0.8/1.5]
  - "dark_pad" (C2..C6) — synth: dark closed-filter pad — brooding low atmosphere
      [saw x5 det12 | cut400 res0.2 | adsr 1/0.5/0.85/1.2]
  - "air_pad" (C3..C7) — synth: airy breath pad — wide, bright, almost noise
      [saw x6 det25 noise0.15 | cut6000 res0.05 | adsr 1.5/0.5/0.8/1.8]
  - "ice_pad" (C3..C7) — synth: icy hollow pad — slow cold movement
      [square x4 det14 | cut3000 | adsr 0.9/0.4/0.85/1.3 | lfo0.3Hz cut300]
  - "choir_pad" (C2..C6) — synth: synthetic choir — vowel-ish resonance, human-adjacent
      [saw x6 det20 | cut1400 res0.5 | adsr 0.8/0.4/0.9/1 | lfo4.5Hz pit3c]
  - "strings_pad" (C2..C6) — synth: synth strings — the JP/Juno ensemble sound
      [saw x7 det15 | cut2500 res0.1 | adsr 0.6/0.4/0.9/0.8]
  - "shimmer_pad" (C3..C7) — synth: shimmering pad — fast gentle sparkle on top
      [saw x6 det22 | cut4000 | adsr 1/0.4/0.85/1.4 | lfo6Hz cut800]
  - "space_pad" (C2..C6) — synth: vast slow space pad — sci-fi nebula
      [saw x6 det30 | cut2000 | adsr 1.8/0.5/0.85/2 | lfo0.2Hz cut1200]
  - "evolving_pad" (C2..C6) — synth: evolving pad — filter opens across the whole note
      [saw x5 det15 | cut700 rise+2500 res0.2 | adsr 1/0.5/0.9/1.2]
  - "nostalgia_pad" (C2..C6) — synth: tape-warble pad — 80s VHS nostalgia
      [saw x4 det10 | cut1500 | adsr 0.7/0.4/0.85/1 | lfo0.8Hz pit7c]
  - "dark_drone" (C1..C4) — synth: ominous drone — sub-heavy held tone, dread
      [square sub0.6 | cut250 res0.15 | adsr 0.5/0.3/1/1]
  - "warm_poly_pad" (C2..C6) — synth: warm poly pad — softly driven analog saw-and-pulse bed with slow breathing motion
      [dual osc1 saw lvl1 phrandom + osc2 square lvl0.72 c-7 phrandom pw0.42 blend0.34 | top sync0 ring0 shape0.04 | uni4 det11 stereo0.76 sub0 noise0 | lowpass cut1750 res0.1 key0.3 | amp 0.68/1.1/0.86/1.45 | env2 0.002/0.4/0/0.1 | lfo1 sine0.13Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>blend+0.12,lfo1>cutoff+620 | macro body0.08 | drv1.12 gain0.54]
  - "pwm_pad" (C2..C6) — synth: PWM pad — wide vintage pulse cloud animated by slow complementary-width crossfade
      [dual osc1 square lvl1 phrandom pw0.14 + osc2 square lvl0.92 c+8 phrandom pw0.64 blend0.5 | top sync0 ring0 shape0 | uni5 det13 stereo0.86 sub0 noise0 | lowpass cut2650 res0.16 key0.26 | amp 0.82/1.2/0.82/1.7 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.18Hz ph0 | lfo2 sine0.07Hz ph0.25 | mod lfo1>blend+0.48,lfo2>pan+0.38 | drv1 gain0.32]
  - "wavetable_motion_pad" (C2..C6) — synth: wavetable motion pad — authored digital cycle moving against an octave analog layer
      [dual osc1 wavetable lvl1 phrandom table[0,1,0.28,0.76,-0.08,-0.46,-1,-0.22,0.12,0.58,0.16,-0.34] + osc2 saw lvl0.78 oct+1 phrandom blend0.42 | top sync0 ring0 shape0.12 | uni4 det14 stereo0.9 sub0 noise0 | notch cut3100 res0.32 key0.22 | amp 1.05/1.4/0.84/1.9 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.11Hz ph0 | lfo2 sh0.37Hz ph0.25 | mod lfo1>blend+0.4,lfo1>cutoff+2400,lfo2>shape+0.14,lfo2>pan+0.26 | macro air0.12 | drv1.12 gain0.47]
  - "swarm_pad" (C2..C6) — synth: swarm pad — dense six-voice detuned analog field with slow opposing pitch drift
      [dual osc1 saw lvl1 c-9 phrandom + osc2 saw lvl0.94 c+11 phrandom blend0.5 | top sync0 ring0 shape0.06 | uni6 det34 stereo1 sub0 noise0 | lowpass cut2250 res0.14 key0.27 | amp 0.58/1/0.9/1.5 | env2 0.002/0.4/0/0.1 | lfo1 sine0.09Hz ph0 | lfo2 triangle0.17Hz ph0.25 | mod lfo1>pitch1+0.035,lfo1>pitch2-0.042,lfo2>cutoff+920 | drv1.18 gain0.43]
  - "spectral_pad" (C3..C7) — synth: spectral pad — airy sine-and-digital harmonics wandering through a resonant band
      [dual osc1 sine lvl1 phrandom + osc2 wavetable lvl0.86 oct+1 phrandom table[0,0.36,1,0.42,-0.12,-0.58,-0.92,-0.2,0.18,0.62,0.06,-1] blend0.52 | top sync0 ring0.08 shape0 | uni3 det7 stereo0.82 sub0 noise0 | bandpass cut2250 res0.36 key0.48 | amp 1.25/1.5/0.76/2.1 | env2 0.002/0.4/0/0.1 | lfo1 sine0.08Hz ph0 | lfo2 sh0.21Hz ph0.25 | mod lfo1>blend+0.24,lfo2>cutoff+1900,lfo1>pan+0.46 | macro air0.22 | drv1 gain0.7]
  - "tension_pad" (C2..C6) — synth: tension pad — close dissonant interval and moving ring color for suspense without noise chaos
      [dual osc1 sine lvl1 phrandom + osc2 square lvl0.66 st+1 c+18 phrandom pw0.29 blend0.4 | top sync0 ring0.2 shape0.1 | uni3 det8 stereo0.78 sub0 noise0 | notch cut1320 res0.48 key0.2 | amp 1.4/1.2/0.9/2.2 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.07Hz ph0 | lfo2 sh0.16Hz ph0.25 | mod lfo1>ring+0.24,lfo1>cutoff+980,lfo2>pan+0.42 | macro roughness0.08 | drv1 gain0.51]
  - "textural_machine" (C2..C6) — synth: textural machine — pitched digital core inside deterministic granular-feeling noise motion
      [dual osc1 noise lvl0.72 pink + osc2 wavetable lvl1 oct+1 phrandom table[0,1,-0.18,0.52,-0.82,0.24,-1,0.08] blend0.72 | top sync0 ring0.04 shape0.24 | uni3 det9 stereo0.9 sub0 noise0.08 | highpass cut720 res0.3 key0.18 | amp 0.46/1.1/0.88/1.45 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.27Hz ph0 | lfo2 sh1.7Hz ph0.25 | mod lfo1>blend+0.28,lfo1>cutoff+1900,lfo2>shape+0.28,lfo2>pan+0.5 | macro roughness0.2,air0.22 | drv1.3 gain0.42]
  - "synth_keys" (C2..C6) — synth: generic synth keys — comping chords, clean
      [saw x2 det6 | cut2800 res0.1 | adsr 0.003/0.4/0.5/0.25]
  - "saw_chords" (C2..C6) — synth: detuned saw chords — the future-bass/pop chord sound
      [saw x6 det18 | cut2400 env+2000>0.22s res0.18 | adsr 0.006/0.35/0.45/0.3]
  - "rave_stab" (C2..C6) — synth: 90s rave stab — big detuned hit, one-shot chords
      [saw x5 det20 | cut1500 env+2500>0.1s res0.3 | adsr 0.002/0.25/0/0.15 | drv2]
  - "house_stab" (C2..C6) — synth: classic house organ stab — short and punchy
      [square x3 det10 | cut1600 env+1200>0.08s res0.4 | adsr 0.002/0.2/0/0.12]
  - "ep_keys" (C2..C6) — synth: FM e-piano — DX7 ballad keys
      [fm r1 i1.5>0.8s | cut5000 | adsr 0.002/0.8/0.3/0.4]
  - "op_tine_piano" (C2..C6) — synth: FM operator e-piano — two tine stacks, velocity opens the click
      [fm op1 sine r1 lvl1 env 0.002/2.4/0.2/0.5 + op2 sine r1 env 0.002/1.6/0.25/0.3 vel0.6 + op3 sine r1 c+4 lvl0.55 env 0.002/1.8/0.15/0.5 + op4 sine r14 env 0.001/0.12/0/0.1 vel0.8 | routes 2>1 i1.6,4>3 i0.9 | uni1 det0 stereo0 sub0 noise0 | lowpass cut9000 res0 key0 | amp 0.002/2.5/0.25/0.45 | env2 0.002/0.4/0/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | drv1 gain0.7]
  - "op_feedback_bass" (C1..C4) — synth: feedback FM bass — self-modulating operator with a saw edge over a sine sub
      [fm op1 sine r1 lvl1 env 0.002/0.5/0.6/0.15 fb0.55 + op2 sine r1 env 0.002/0.18/0.3/0.1 vel0.7 + op3 sine r0.5 lvl0.5 | routes 2>1 i2.4 | uni1 det0 stereo0 sub0 noise0 | lowpass cut2600 res0.1 key0.3 | amp 0.002/0.4/0.75/0.15 | env2 0.002/0.4/0/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | drv1.6 gain0.75]
  - "op_glass_bell" (C3..C7) — synth: FM operator bell — 3.5:1 inharmonic stack over a detuned octave partial
      [fm op1 sine r1 lvl1 + op2 sine r3.5 env 0.001/0.9/0.08/0.5 vel0.5 + op3 sine r2 c+6 lvl0.4 env 0.001/1.4/0/0.6 + op4 sine r7.01 env 0.001/0.25/0/0.2 | routes 2>1 i4.2,4>3 i1.2 | uni1 det0 stereo0 sub0 noise0 | lowpass cut16000 res0 key0 | amp 0.001/2.2/0/1 | env2 0.002/0.4/0/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | drv1 gain0.6]
  - "organ_keys" (C2..C6) — synth: synth organ — sustained drawbar-ish tone
      [sine sub0.8 noise0.02 | cut6000 | adsr 0.005/0.1/1/0.08]
  - "clav_keys" (C2..C6) — synth: funky clav — snappy filtered bite
      [saw x2 det7 | cut1500 env+4200>0.05s res0.28 | adsr 0.001/0.22/0.08/0.08 | drv1.6]
  - "music_box" (C4..C7) — synth: music box — delicate toy chimes, lullaby
      [fm r4.2 i3>0.5s | cut7000 | adsr 0.001/0.7/0/1]
  - "pizz_synth" (C2..C6) — synth: synth pizzicato — dry short pluck, suspense pulses
      [saw | cut900 env+1200>0.05s res0.2 | adsr 0.001/0.15/0/0.08]
  - "stab_brass" (C2..C6) — synth: brass hit — short driven orchestra-stab energy
      [saw x4 det12 | cut1400 env+1600>0.12s res0.2 | adsr 0.01/0.25/0/0.15 | drv2]
  - "space_keys" (C2..C6) — synth: celestial poly keys — soft core with a clear octave-lit attack
      [dual osc1 sine lvl1 + osc2 saw lvl0.48 st+12 blend0.28 | top sync0 ring0 shape0.04 | uni2 det6 stereo0.32 sub0 noise0 | lowpass cut4200 res0.12 key0.25 | amp 0.008/0.65/0.42/0.42 | env2 0.002/0.45/0.12/0.2 | lfo1 sine0.17Hz ph0 | lfo2 triangle0.07Hz ph0.25 | mod env2>cutoff+1500,lfo1>blend+0.05 | drv1.15 gain0.68]
  - "space_keys_glass" (C3..C7) — synth: glass space keys — struck crystalline ring that settles into a quiet tone
      [dual osc1 sine lvl1 + osc2 sine lvl0.75 st+19 c+4 blend0.38 | top sync0 ring0.28 shape0.02 | uni2 det3 stereo0.38 sub0 noise0 | notch cut4200 res0.3 key0.35 | amp 0.002/0.9/0.18/0.65 | env2 0.001/0.38/0/0.18 | lfo1 sine0.21Hz ph0 | lfo2 triangle0.09Hz ph0.25 | mod env2>ring+0.35,env2>cutoff+2400 | drv1 gain0.62]
  - "space_keys_dark" (C2..C6) — synth: dark space keys — hollow notched body for restrained minor chords
      [dual osc1 square lvl0.68 pw0.33 + osc2 sine lvl1 blend0.62 | top sync0 ring0 shape0.03 | uni1 det0 stereo0 sub0.08 noise0 | notch cut950 res0.52 key0.18 | amp 0.018/0.7/0.55/0.48 | env2 0.004/0.5/0.25/0.2 | lfo1 sine0.16Hz ph0 | lfo2 triangle0.06Hz ph0.25 | mod env2>cutoff+900 | macro body0.08 | drv1.3 gain0.68]
  - "space_keys_air" (C3..C7) — synth: air space keys — pitched sine body breathing through moving pink-noise air
      [dual osc1 sine lvl1 + osc2 noise lvl0.35 pink blend0.18 | top sync0 ring0 shape0 | uni2 det2 stereo0.45 sub0 noise0.02 | lowpass cut5200 res0.08 key0.25 | amp 0.025/0.85/0.3/0.6 | env2 0.15/1.2/0.2/0.4 | lfo1 sine0.23Hz ph0 | lfo2 triangle0.11Hz ph0.25 | mod lfo1>cutoff+700,lfo2>pan+0.28 | macro air0.15 | drv1 gain0.62]
  - "space_keys_shimmer" (C3..C7) — synth: shimmer space keys — bright octave particles above an articulate key strike
      [dual osc1 sine lvl1 + osc2 wavetable lvl0.8 st+12 table[0,1,0.2,0.72,0,-0.72,-0.2,-1] blend0.42 | top sync0 ring0.06 shape0.04 | uni3 det7 stereo0.55 sub0 noise0 | highpass cut180 res0.06 key0.35 | amp 0.004/0.75/0.28/0.7 | env2 0.002/0.65/0/0.2 | lfo1 sine5.4Hz ph0 | lfo2 triangle0.12Hz ph0.25 | mod lfo1>pitch2+0.05,env2>blend+0.25 | macro air0.08 | drv1 gain0.58]
  - "space_keys_tape" (C2..C6) — synth: tape space keys — compact warm poly tone with slow imperfect pitch drift
      [saw x3 det7 | cut2100 env+850>0.42s res0.08 | adsr 0.015/0.7/0.42/0.4 | lfo0.7Hz pit9c | drv1.3]
  - "space_keys_orbit" (C2..C6) — synth: orbit space keys — sustained chord body circles the stereo field without losing its onset
      [dual osc1 sine lvl0.9 + osc2 saw lvl0.55 st+7 c-4 phrandom blend0.35 | top sync0 ring0 shape0.06 | uni2 det8 stereo0.7 sub0 noise0 | lowpass cut3200 res0.18 key0.3 | amp 0.012/0.8/0.5/0.55 | env2 0.05/1.5/0.3/0.3 | lfo1 sine0.31Hz ph0 | lfo2 triangle0.13Hz ph0.25 | mod lfo1>pan+0.75,lfo2>blend+0.22,env2>cutoff+1400 | drv1.2 gain0.64]
  - "space_keys_hologram" (C3..C7) — synth: hologram space keys — shifting wavetable reflections with a moving spectral notch
      [dual osc1 wavetable lvl1 table[0,1,0.15,0.65,-0.2,-1,-0.1,-0.55] + osc2 square lvl0.6 st+12 ph0.25 pw0.21 blend0.48 | top sync0 ring0.12 shape0.22 | uni3 det5 stereo0.58 sub0 noise0 | notch cut3600 res0.48 key0.3 | amp 0.006/0.7/0.32/0.5 | env2 0.001/0.9/0.1/0.25 | lfo1 triangle0.43Hz ph0 | lfo2 sh2.7Hz ph0.25 | mod lfo1>blend+0.25,lfo2>shape+0.16,env2>cutoff+2200 | drv1.4 gain0.56]
  - "space_keys_alien" (C3..C6) — synth: alien space keys — controlled inharmonic ring color that remains chromatically playable
      [dual osc1 sine lvl1 + osc2 square lvl0.7 st+13 c+17 pw0.37 blend0.32 | top sync0 ring0.42 shape0.1 | uni1 det0 stereo0 sub0 noise0 | notch cut1800 res0.36 key0.4 | amp 0.003/0.55/0.24/0.45 | env2 0.001/0.3/0/0.15 | lfo1 sine0.38Hz ph0 | lfo2 triangle0.19Hz ph0.25 | mod env2>ring+0.3,lfo1>pitch2+0.11,lfo2>cutoff+650 | drv1.5 gain0.56]
  - "space_keys_frozen" (C3..C7) — synth: frozen space keys — cold wavetable facets with a deliberate icy tail
      [dual osc1 wavetable lvl1 table[0,0.55,1,0.2,-0.45,-0.15,-1,-0.35] + osc2 sine lvl0.85 st+12 blend0.4 | top sync0 ring0.08 shape0.04 | uni3 det4 stereo0.5 sub0 noise0 | lowpass cut6500 res0.18 key0.42 | amp 0.035/0.95/0.26/0.75 | env2 0.002/1.1/0.05/0.3 | lfo1 triangle0.15Hz ph0 | lfo2 sine0.47Hz ph0.25 | mod env2>cutoff+3200,lfo1>blend+0.12,lfo2>pan+0.22 | drv1 gain0.58]
  - "warm_poly_keys" (C2..C6) — synth: warm poly keys — softly driven saw-and-pulse chords with a natural filter touch
      [dual osc1 saw lvl1 phrandom + osc2 square lvl0.72 c-5 phrandom pw0.43 blend0.38 | top sync0 ring0 shape0.05 | uni3 det8 stereo0.5 sub0 noise0 | lowpass cut2450 res0.12 key0.34 | amp 0.012/0.62/0.62/0.42 | env2 0.002/0.46/0.15/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+1350 | drv1.22 gain0.63]
  - "pwm_keys" (C2..C6) — synth: PWM keys — contrasting pulse widths crossfade into a breathing vintage-poly tone
      [dual osc1 square lvl1 pw0.18 + osc2 square lvl0.9 c+4 pw0.67 blend0.48 | top sync0 ring0 shape0 | uni2 det5 stereo0.34 sub0 noise0 | lowpass cut3150 res0.2 key0.3 | amp 0.008/0.5/0.58/0.32 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.31Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>blend+0.42,env2>cutoff+900 | drv1.12 gain0.36]
  - "phase_keys" (C2..C6) — synth: phase keys — near-unison oscillators beat through a slowly moving spectral notch
      [dual osc1 sine lvl1 + osc2 sine lvl0.92 c+17 ph0.21 blend0.5 | top sync0 ring0.08 shape0.03 | uni2 det3 stereo0.48 sub0 noise0 | notch cut2100 res0.34 key0.38 | amp 0.018/0.72/0.5/0.48 | env2 0.002/0.4/0/0.1 | lfo1 sine0.19Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>cutoff+1250,lfo1>pan+0.24 | drv1 gain0.67]
  - "morphed_keys" (C2..C6) — synth: morphed keys — moving blend between warm analog saw and an authored digital cycle
      [dual osc1 saw lvl0.88 phrandom + osc2 wavetable lvl1 phrandom table[0,0.92,0.35,1,-0.18,-0.82,-0.28,-1] blend0.46 | top sync0 ring0 shape0.13 | uni3 det7 stereo0.58 sub0 noise0 | notch cut3300 res0.28 key0.3 | amp 0.014/0.7/0.46/0.5 | env2 0.004/0.8/0.1/0.2 | lfo1 triangle0.23Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>blend+0.36,env2>shape+0.22,env2>cutoff+1700 | drv1.18 gain0.59]
  - "tape_keys" (C2..C6) — synth: tape keys — warm low-index electric tone with slow pitch wear
      [fm r1 i0.72>2.1s | cut2950 env+520>0.58s res0.08 | adsr 0.018/0.72/0.56/0.48 | lfo0.41Hz pit9c | drv1.12]
  - "bell_keys" (C3..C7) — synth: bell keys — playable struck-sine keyboard with a brief inharmonic flash
      [dual osc1 sine lvl1 + osc2 sine lvl0.86 st+19 c+9 blend0.35 | top sync0 ring0.18 shape0 | uni2 det2 stereo0.4 sub0 noise0 | highpass cut260 res0.14 key0.45 | amp 0.002/1.35/0.08/0.82 | env2 0.001/0.46/0/0.12 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>ring+0.5,env2>pitch2+0.09 | drv1 gain0.61]
  - "dub_chord" (C2..C6) — synth: dub chord — dark filter-envelope stab designed to bloom into external echo
      [dual osc1 saw lvl1 phrandom + osc2 square lvl0.7 oct-1 phrandom pw0.36 blend0.36 | top sync0 ring0 shape0.08 | uni3 det9 stereo0.5 sub0 noise0 | lowpass cut540 res0.38 key0.22 | amp 0.004/0.68/0.08/0.72 | env2 0.001/0.32/0/0.1 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+3900 | drv1.5 gain0.61]
  - "detroit_chord" (C2..C6) — synth: Detroit chord — futuristic analog-digital fifth color with a fast resonant opening
      [dual osc1 saw lvl0.9 phrandom + osc2 wavetable lvl1 st+7 phrandom table[0,1,0.08,0.64,-0.48,-0.15,-1,-0.32] blend0.47 | top sync0 ring0.06 shape0.12 | uni3 det6 stereo0.62 sub0 noise0 | lowpass cut1180 res0.3 key0.3 | amp 0.008/0.52/0.18/0.46 | env2 0.002/0.38/0/0.12 | lfo1 triangle0.16Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+4300,lfo1>blend+0.12 | drv1.35 gain0.56]
  - "rhythmic_filter_keys" (C2..C6) — synth: rhythmic filter keys — held chords articulate themselves through repeating filter motion
      [dual osc1 saw lvl1 + osc2 square lvl0.64 oct+1 pw0.27 blend0.35 | top sync0 ring0 shape0 | uni2 det5 stereo0.36 sub0 noise0 | lowpass cut760 res0.44 key0.32 | amp 0.006/0.5/0.78/0.18 | env2 0.002/0.4/0/0.1 | lfo1 triangle2Hz ph0 | lfo2 square4Hz ph0.25 | mod lfo1>cutoff+4100,lfo2>blend+0.13 | drv1.22 gain0.58]
  - "signal_pulse" (C3..C7) — synth: signal pulse — narrow electronic beacon animated by square filter steps
      [dual osc1 saw lvl0.86 + osc2 square lvl1 oct+1 pw0.32 blend0.34 | top sync0 ring0 shape0.06 | uni2 det5 stereo0.32 sub0 noise0 | lowpass cut1250 res0.38 key0.42 | amp 0.006/0.4/0.76/0.16 | env2 0.002/0.4/0/0.1 | lfo1 square4Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>cutoff+3200,lfo1>blend+0.12 | drv1.28 gain0.5]
  - "cloud_pulse" (C2..C6) — synth: cloud pulse — wide analog-digital cloud with drifting filter and stereo cycles
      [dual osc1 saw lvl0.82 phrandom + osc2 wavetable lvl1 oct+1 phrandom table[0,0.42,1,0.18,-0.22,-0.7,-1,-0.1] blend0.58 | top sync0 ring0 shape0 | uni5 det17 stereo0.9 sub0 noise0 | notch cut2800 res0.24 key0.25 | amp 0.12/0.8/0.82/0.7 | env2 0.002/0.4/0/0.1 | lfo1 triangle1.35Hz ph0 | lfo2 sine0.21Hz ph0.25 | mod lfo1>cutoff+3600,lfo1>blend+0.2,lfo2>pan+0.62 | macro air0.16 | drv1 gain0.48]
  - "metallic_pulse" (C2..C6) — synth: metallic pulse — clocked ring-modulation color for mechanical melodic patterns
      [dual osc1 square lvl0.9 pw0.31 + osc2 sine lvl1 st+17 c+15 blend0.34 | top sync0 ring0.38 shape0.14 | uni1 det0 stereo0.36 sub0 noise0 | bandpass cut2350 res0.46 key0.44 | amp 0.003/0.48/0.7/0.16 | env2 0.002/0.4/0/0.1 | lfo1 square3Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod lfo1>ring+0.36,lfo1>cutoff+2300 | drv1.45 gain0.58]
  - "random_pan_keys" (C2..C6) — synth: random-pan keys — articulate octave keys hopping through deterministic stereo positions
      [dual osc1 saw lvl0.84 phrandom + osc2 sine lvl1 oct+1 phrandom blend0.42 | top sync0 ring0 shape0 | uni2 det5 stereo0.62 sub0 noise0 | lowpass cut3900 res0.12 key0.38 | amp 0.009/0.66/0.48/0.42 | env2 0.002/0.52/0.08/0.1 | lfo1 sine0.2Hz ph0 | lfo2 sh0.82Hz ph0.25 | mod lfo2>pan+0.88,env2>cutoff+1450 | drv1 gain0.58]
  - "rhythmic_organ" (C2..C6) — synth: rhythmic organ — drawbar-like body with repeating harmonic and filter movement
      [dual osc1 sine lvl1 + osc2 square lvl0.64 oct+1 pw0.5 blend0.32 | top sync0 ring0 shape0 | uni1 det0 stereo0.3 sub0.28 noise0 | lowpass cut1850 res0.32 key0.42 | amp 0.006/0.1/1/0.1 | env2 0.002/0.4/0/0.1 | lfo1 square3Hz ph0 | lfo2 triangle0.16Hz ph0.25 | mod lfo1>blend+0.3,lfo1>cutoff+2100,lfo2>pan+0.28 | drv1.18 gain0.59]
  - "wooden_pluck" (C2..C7) — synth: wooden pluck — compact hollow body with a short struck-filter attack
      [dual osc1 square lvl0.78 pw0.38 + osc2 sine lvl1 oct-1 blend0.44 | top sync0 ring0 shape0.08 | uni1 det0 stereo0.16 sub0 noise0 | bandpass cut780 res0.38 key0.62 | amp 0.002/0.34/0/0.16 | env2 0.001/0.11/0/0.05 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+2100,env2>shape+0.18 | drv1.38 gain0.65]
  - "metallic_pluck" (C3..C7) — synth: metallic pluck — inharmonic sine ring that flashes brightly then clears
      [dual osc1 sine lvl1 + osc2 sine lvl0.92 st+14 c+23 blend0.32 | top sync0 ring0.42 shape0 | uni1 det0 stereo0.36 sub0 noise0 | highpass cut420 res0.2 key0.46 | amp 0.001/0.72/0/0.52 | env2 0.001/0.2/0/0.08 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>ring+0.42 | drv1 gain0.57]
  - "rubber_pluck" (C2..C6) — synth: rubber pluck — resonant elastic twang with a tiny downward pitch settle
      [dual osc1 square lvl1 pw0.29 + osc2 sine lvl0.82 oct-1 blend0.34 | top sync0 ring0 shape0.12 | uni1 det0 stereo0.18 sub0.08 noise0 | lowpass cut390 res0.58 key0.48 | amp 0.002/0.29/0.03/0.14 | env2 0.001/0.18/0/0.06 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+3600,env2>resonance+0.18 | drv1.65 gain0.61 knock+5st>0.055s]
  - "resonant_ping" (C3..C7) — synth: resonant ping — tuned sine impulse excited by a brief noise click
      [dual osc1 sine lvl1 + osc2 noise lvl0.46 white blend0.18 | top sync0 ring0 shape0 | uni1 det0 stereo0.28 sub0 noise0 | bandpass cut1320 res0.82 key0.8 | amp 0.001/0.58/0/0.38 | env2 0.001/0.08/0/0.04 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+4200 | drv1 gain0.82]
  - "pitch_env_hit" (C2..C6) — synth: pitch-envelope hit — melodic electronic strike falling rapidly into its written note
      [dual osc1 saw lvl0.82 + osc2 sine lvl1 oct-1 blend0.52 | top sync0 ring0 shape0.08 | uni1 det0 stereo0.12 sub0 noise0 | lowpass cut2100 res0.26 key0.35 | amp 0.001/0.26/0/0.13 | env2 0.001/0.13/0/0.05 | lfo1 sine0.2Hz ph0 | lfo2 triangle0.1Hz ph0.25 | mod env2>cutoff+3900 | drv1.4 gain0.61 knock+28st>0.075s]
  - "laser_zap" (C2..C6) — synth: laser zap — steep pitch fall, sci-fi/transition accent
      [saw | cut6000 res0.4 | adsr 0.001/0.3/0/0.1 | knock48st>0.09s]
  - "sub_drop" (C1..C3) — synth: sub drop — the note falls an octave+ below, EDM drop marker
      [sine sub0.5 | cut800 | adsr 0.01/0.3/0.9/0.4 | travel-24st]
  - "pitch_riser" (C2..C5) — synth: tonal riser — pitch + filter climb across the whole note
      [saw x3 det15 | cut1200 rise+3000 res0.3 | adsr 0.2/0.3/1/0.3 | travel+12st]
  - "siren" (C3..C6) — synth: siren — slow pitch wail, alarm/ragga air-horn energy
      [square | cut3000 | adsr 0.05/0.3/1/0.3 | lfo1.2Hz pit700c | drv1.5]
  - "white_noise" (C1..C7) — synth: noise wash layer — pitch ignored, one long note
      [white-noise | cut1800 res0.2 | adsr 0.4/0.3/1/1.2]
  - "pink_wash" (C1..C7) — synth: smooth dark noise bed — pitch ignored, one long note
      [pink-noise | cut3000 res0.1 | adsr 1.2/0.3/1/1.5]
  - "noise_riser" (C1..C7) — synth: uplifter — filter opens across the note; note length = rise length
      [white-noise | cut350 rise+6000 res0.45 | adsr 0.15/0.3/1/0.5]
  - "noise_fall" (C1..C7) — synth: downlifter — bright to dark across the note (after-drop exhale)
      [white-noise | cut6500 rise-6000 res0.35 | adsr 0.01/0.3/1/0.8]
  - "vinyl_crackle" (C1..C7) — synth: vinyl crackle texture bed — lofi warmth, pitch ignored
      [crackle-noise | cut6000 | adsr 0.05/0.3/1/0.3]
  - "sub_drone" (C0..C3) — synth: deep sub-bass drone bed — pitch sets the root
      [sine sub0.8 | cut300 | adsr 0.4/0.3/1/0.8]
  - "metallic_drone" (C1..C5) — synth: metallic drone — slow inharmonic ring movement for industrial or cinematic beds
      [dual osc1 sine lvl1 phrandom + osc2 square lvl0.72 st+7 c+31 phrandom pw0.34 blend0.38 | top sync0 ring0.42 shape0.12 | uni2 det4 stereo0.66 sub0 noise0 | bandpass cut840 res0.5 key0.28 | amp 1.25/1/0.94/2.4 | env2 0.002/0.4/0/0.1 | lfo1 triangle0.065Hz ph0 | lfo2 sh0.22Hz ph0.25 | mod lfo1>ring+0.28,lfo1>cutoff+920,lfo2>pan+0.36 | drv1.3 gain0.49]
  - "swarm_drone" (C1..C5) — synth: swarm drone — very wide detuned analog mass with a protected low fundamental
      [dual osc1 saw lvl1 c-13 phrandom + osc2 saw lvl0.94 c+16 phrandom blend0.5 | top sync0 ring0 shape0.08 | uni6 det48 stereo1 sub0.16 noise0 | lowpass cut690 res0.3 key0.18 | amp 1.7/1.1/1/2.8 | env2 0.002/0.4/0/0.1 | lfo1 sine0.055Hz ph0 | lfo2 triangle0.12Hz ph0.25 | mod lfo1>pitch1+0.06,lfo1>pitch2-0.07,lfo2>cutoff+780,lfo2>pan+0.32 | macro body0.16 | drv1.24 gain0.43]
  - "pitched_ambience" (C2..C6) — synth: pitched ambience — stable sine center suspended inside slowly moving pink air
      [dual osc1 sine lvl1 phrandom + osc2 noise lvl0.72 pink blend0.3 | top sync0 ring0 shape0 | uni3 det6 stereo0.94 sub0 noise0.04 | highpass cut310 res0.16 key0.32 | amp 1.8/1.4/0.9/3 | env2 0.002/0.4/0/0.1 | lfo1 sine0.08Hz ph0 | lfo2 sh0.3Hz ph0.25 | mod lfo1>blend+0.2,lfo1>pan+0.58,lfo2>cutoff+760 | macro air0.32 | drv1 gain0.46]
  - "circuit_bent_texture" (C2..C6) — synth: circuit-bent texture — deterministic stepped digital glitches that remain chromatically playable
      [dual osc1 square lvl0.9 pw0.11 + osc2 wavetable lvl1 st+5 table[0,1,-0.72,0.18,0.84,-1,0.36,-0.24] blend0.5 | top sync0 ring0.28 shape0.34 | uni2 det7 stereo0.72 sub0 noise0.08 | bandpass cut1680 res0.56 key0.38 | amp 0.028/0.72/0.76/0.62 | env2 0.002/0.4/0/0.1 | lfo1 square1.7Hz ph0 | lfo2 sh4.3Hz ph0.25 | mod lfo1>blend+0.3,lfo1>ring+0.2,lfo2>shape+0.34,lfo2>cutoff+2100,lfo2>pan+0.46 | macro roughness0.3 | drv1.55 gain0.4]

#### D.1.e Catalog entries — sampled instruments

  - "balafon" (C#3..F5) — West African balafon — earthy wooden marimba  [env 0.01/0.02/0.64]
  - "kalimba" (G1..C#6) — African kalimba (thumb piano), real Tanzanian recording  [env 0.1/0.12/1.5]
  - "mbira" (A#1..A4) — Zimbabwean mbira — buzzy spirit-music plucks  [env 0/0.22/5.11]
  - "dan_tranh" (B1..B4) — Vietnamese dan tranh zither — real plucks with performed tremolo and pitch-bending vibrato  [env 0.01/0.21/3.94,1.56↑] [performance 3 velocity layers]
  - "hand_chimes" (C3..C6) — hand chimes — glassy sustained bell tones  [env 0.01/0.58/3.57]
  - "didgeridoo_drone" (C4..C4) — performed didgeridoo drone — fixed natural pitch; trigger C4, use dur to trim the 10-15 second take  [env 0.01/9.32/12.32] [performance 3 round robins]
  - "didgeridoo_phrase" (C4..C4) — performed didgeridoo rhythmic phrase — fixed natural pitch; trigger C4 and leave space for the 11-15 second gesture  [env 0.01/8.38/11.52] [performance 5 round robins]
  - "ocean_drum" (C4..C4) — performed ocean-drum wash — unpitched texture; trigger C4 and use dur to shape the 22-38 second motion  [env 28.26/36.3/37.4] [performance 3 round robins]
  - "recorder" (F3..E5) — baroque alto recorder — warm breathy sustained woodwind  [env 0.02/15.85/16.26]
  - "harpsichord" (A#0..E5) — English harpsichord — crisp plucked keyboard with real key-release noises  [env 0.02/0.31/5.24,2.24↑] [performance note-off samples]
  - "bowed_psaltery" (A#3..F#5) — bowed psaltery — narrow, ancient singing-string tone  [env 0.78/2.55/5.86]
  - "wine_glass" (D#4..D5) — rubbed wine glasses — fragile glass harmonics with real note-off decays  [env 1/20.57/20.58] [performance note-off samples]
  - "glockenspiel" (G4..C7) — orchestral glockenspiel — bright metal bells with three recorded dynamics  [env 0.01/0.07/3.75] [performance 3 velocity layers]
  - "timpani" (C2..C4) — orchestral timpani hits — 11 tuned regions, three real dynamics and two alternate strikes  [env 0/0.15/6.56,1.71↑] [performance 3 velocity layers, 2 round robins]
  - "strumstick" (D3..A5) — three-string Strumstick — real finger-plucked, dulcimer-like folk tone with three dynamics  [env 0.01/0.37/4.35,1.07↑] [performance 3 velocity layers]
  - "folk_harp" (C2..G#6) — small folk harp — intimate, shorter plucks with two real dynamics across a dense diatonic map  [env 0.01/0.22/6.67,1.23↑] [performance 2 velocity layers]
  - "saxello" (A#3..E6) — Saxello — high-register saxophone color with non-vibrato, staccato and performed vibrato  [env 0.02/4.13/4.76] [performance 2 velocity layers]
  - "saxello_staccato" (A#3..D6) — Saxello staccato — short tongued high-sax attacks in up to two dynamics  [env 0.02/0.08/0.36] [performance 2 velocity layers]
  - "saxello_vibrato" (A#3..D#6) — Saxello with naturally performed vibrato  [env 0.01/3.1/6.33]
  - "accordion" (B2..G5) — Hohner button accordion — tuned stereo sustains with authored loops and real key-release recordings  [env 0.07/1.9/1.9] [performance sustain loop, note-off samples]
  - "classical_guitar" (G1..C6) — Spanish classical guitar — intimate nylon-string plucks recorded by the FreePats project  [env 0.03/0.18/2.24,0.84↑]
  - "ukulele" (A#3..D6) — tenor ukulele — coherent 24-bit plucks plus separate body-tap and muted-chuck percussion  [env 0/0.08/1.97,1.07↑]
  - "jazz_guitar" (B1..D6) — processed Fender electric guitar — warm rounded jazz-amplifier tone with four alternate attacks and two dynamics through E4  [env 0.02/0.33/7.31,2.53↑] [performance 2 velocity layers, 4 round robins]
  - "distortion_guitar" (B1..D6) — processed Fender electric guitar — dark, dense high-gain tone with four alternate attacks and two dynamics through E4  [env 0.01/1.52/9.62,4.26↑] [performance 2 velocity layers, 4 round robins]
  - "overdriven_guitar" (B1..D6) — processed Fender electric guitar — brighter overdriven tone with four alternate attacks and two dynamics through E4  [env 0/3.58/7.89,2.87↑] [performance 2 velocity layers, 4 round robins]
  - "honky_tonk_piano" (G0..C8) — historic Francis Bacon player piano — wide stereo honky-tonk character recorded at the player's head  [env 0.01/0.1/7.32,1.24↑]
  - "tagelharpa" (D2..F4) — bass tagelharpa, hard-plucked — dry Nordic folk strings with six alternate takes  [env 0.1/0.13/0.97] [performance 6 round robins]
  - "tuba" (F1..G3) — solo tuba sustain — real low brass for orchestral, jazz and cinematic weight  [env 0.03/5.35/5.71] [performance sustain loop]
  - "tuba_staccato" (F1..G3) — solo tuba staccato — four dynamics and three alternate attacks for rhythmic brass  [env 0.04/0.89/1.18] [performance 4 velocity layers, 3 round robins]
  - "baritone_sax" (C2..G#4) — 1926 baritone saxophone sustain — two real dynamics, smoky and weighty  [env 0.02/5.2/5.2] [performance 2 velocity layers, sustain loop]
  - "baritone_sax_staccato" (C2..G#4) — baritone saxophone staccato — four dynamics and alternate tongued attacks  [env 0.01/0.14/0.48] [performance 4 velocity layers, 3-4 round robins]
  - "bass_finger" (C1..C4) — electric bass, fingered — real recording, the standard funk/pop/rock bass  [env 0.07/0.11/2.21] [performance 4 round robins]
  - "bass_pluck" (C1..C4) — electric bass, hard pluck — brighter attack, cuts through  [env 0.03/0.09/3.25,1.4↑] [performance 4 round robins]
  - "bass_mute" (C1..C4) — electric bass, palm-muted — the thumpy motown/dub short note  [env 0.02/0.13/1.67] [performance 4 round robins]
  - "bass_ghost" (C#1..C4) — electric bass ghost notes — pitched percussive thumps between real notes (the funk pocket)  [env 0.03/0.04/1.74] [performance 4 round robins]
  - "funk_guitar" (E2..D6) — electric guitar, clean twang — real recording; add wah/drive fx for funk/rock  [env 0.02/0.56/4.06,1.4↑] [performance 3 velocity layers, 2-4 round robins, note-off samples]
  - "funk_guitar_stac" (E2..D6) — electric guitar staccato chick — THE muted funk 'chicka' scratch, write it in 16ths  [env 0.02/0.07/0.46] [performance 4 round robins]
  - "funk_guitar_hammer" (E2..D6) — electric guitar hammer-on — legato ornament into a note  [env 0/0.34/3.74,2.22↑] [performance 2 round robins, note-off samples]
  - "twang_guitar" (E2..D6) — electric baritone guitar — darker surf/spaghetti-western twang  [env 0.02/0.97/2.27,1.35↑] [performance 3 velocity layers, 2-4 round robins, note-off samples]
  - "twang_guitar_stac" (E2..D6) — baritone guitar staccato — dark muted chugs  [env 0.02/0.02/0.8] [performance 4 round robins]
  - "prepared_guitar" (E2..C5) — electric guitar plucked behind the bridge — brittle metallic prepared-string color  [env 0.02/0.02/1.01] [performance 2 round robins]
  - "upright_pizz" (A0..C4) — upright double bass, plucked — real recording, jazz/rockabilly walking bass  [env 0.01/0.03/3.94] [performance 4 velocity layers, 4 round robins]
  - "upright_arco" (A0..A4) — upright double bass, bowed — dark cinematic low sustains  [env 0.09/5.74/5.74] [performance 3 velocity layers, down/up bows, sustain loop]
  - "piano" (A#0..C8) — Kawai grand piano — four real dynamics with natural key-release recordings  [env 0.02/0.23/12.23,1.06↑] [performance 4 velocity layers, note-off samples]
  - "electric_piano" (C0..C7) — Yamaha TX81Z FM electric piano — three real velocity layers  [env 0/0.27/6.21,2.34↑] [performance 3 velocity layers]
  - "organ" (C2..E6) — Renaissance pipe organ, full registration — real room recordings  [env 0.02/5.73/6.02]
  - "organ_8ft" (C2..E6) — Renaissance pipe organ, 8-foot stop — foundational unison register in real room recordings  [env 0.03/7.65/8.22]
  - "organ_4ft" (C3..E7) — Renaissance pipe organ, 4-foot stop — bright octave register in real room recordings  [env 0.02/5.99/6.5]
  - "harmonica" (C4..C7) — Hohner Special 20 harmonica — natural sustains and note-off recordings  [env 0.07/4.06/4.39] [performance note-off samples]
  - "harmonica_soft" (C4..C7) — Hohner Special 20 harmonica, softly performed  [env 0.11/5.17/5.63] [performance note-off samples]
  - "harmonica_vibrato" (C4..C7) — Hohner Special 20 harmonica with performed vibrato  [env 0.7/4.86/5.63] [performance note-off samples]
  - "ocarina" (A4..C#6) — typical clay ocarina — natural sustains and note-off recordings  [env 0.03/5.87/6.14] [performance note-off samples]
  - "ocarina_vibrato" (A4..C6) — typical clay ocarina with performed vibrato  [env 0.03/8.14/8.74] [performance note-off samples]
  - "tenor_sax" (G#2..E6) — tenor saxophone, non-vibrato sustain — two real dynamics  [env 0.04/7.42/7.87] [performance 2 velocity layers]
  - "tenor_sax_staccato" (G#2..E6) — tenor saxophone, short tongued staccato  [env 0.04/0.16/0.54] [performance 2 velocity layers]
  - "tenor_sax_vibrato" (A#2..D6) — tenor saxophone with performed vibrato  [env 0.09/1.52/7.47]
  - "harp" (E1..F7) — concert harp — two real pluck dynamics across its full register  [env 0.03/0.15/10.35,0.89↑] [performance 2 velocity layers, up to 2 round robins]
  - "marimba" (F2..C7) — orchestral marimba — soft, medium and loud real strikes  [env 0.01/0.18/1.86,0.95↑] [performance 3 velocity layers, up to 3 round robins]
  - "tubular_bells" (C4..E5) — orchestral tubular bells — real soft and forceful chime strikes  [env 0.01/0.76/12.53] [performance 2 velocity layers]
  - "vibraphone" (F3..E6) — orchestral vibraphone — soft and hard mallets with real dynamics  [env 0.01/1.55/10.12,5.56↑] [performance 3 velocity layers, up to 2 round robins]
  - "vibraphone_bowed" (A3..E6) — bowed vibraphone — long glassy metal sustains  [env 1.61/6.18/15,8.89↑]
  - "xylophone" (G4..C8) — orchestral xylophone — soft, medium and hard mallet recordings  [env 0/0.03/0.7,0.41↑] [performance 2 velocity layers, 2-4 round robins]
  - "french_horn" (A1..F5) — solo French horn — warm orchestral brass with sustain, staccato and a real muted performance  [env 0.18/10.77/14,7.89↑] [performance 4 velocity layers]
  - "trombone" (A#1..F4) — solo tenor trombone — orchestral brass with sustain, staccato and performed vibrato  [env 0.14/15.01/15.49] [performance 3 velocity layers]
  - "trumpet" (E3..C6) — solo trumpet — real open, vibrato, staccato, straight-muted and Harmon-muted performances  [env 0.03/18.06/19.02] [performance 2 velocity layers]
  - "bassoon" (A#1..D#5) — solo bassoon — woody low woodwind with sustain, staccato and performed vibrato  [env 0.19/7.67/8.55] [performance 2 velocity layers]
  - "clarinet" (D3..F#6) — solo clarinet — focused orchestral reed with long sustain and real staccato attacks  [env 0.22/7.54/9.07] [performance 3 velocity layers]
  - "flute" (C4..C7) — solo concert flute — non-vibrato sustain plus vibrato, expressive vibrato and staccato  [env 0.14/12.34/12.9,5.6↑] [performance 2 velocity layers]
  - "oboe" (A#3..F6) — solo oboe — penetrating double-reed tone with sustain, vibrato and staccato  [env 0.13/8.81/9.83] [performance 2 velocity layers]
  - "piccolo" (G4..G6) — solo piccolo — brilliant high woodwind with sustain and staccato recordings  [env 0.1/7.58/8.23]
  - "violin" (G3..C7) — solo violin — naturally vibrated arco with real pizzicato, tremolo and spiccato  [env 1.53/12.16/14.27] [performance 2 velocity layers]
  - "violin_section" (G3..D6) — orchestral violin section — sustained vibrato, pizzicato, tremolo and spiccato  [env 2.07/9.44/10.57] [performance 2 velocity layers]
  - "viola_section" (C3..D6) — orchestral viola section — sustained vibrato, pizzicato, tremolo and spiccato  [env 1.49/5.39/9.4] [performance 2 velocity layers]
  - "cello_section" (C2..F5) — orchestral cello section — sustained vibrato, pizzicato, tremolo and spiccato  [env 0.36/7.63/8.67] [performance 3 velocity layers]
  - "cello" (C2..C6) — solo cello sustain — four performed dynamics and alternating bow takes  [env 0.28/3.56/3.57] [performance 4 velocity layers, down/up bows]
  - "cello_staccato" (C2..C6) — solo cello staccato — four performed dynamics and up to four alternate attacks  [env 0.16/0.36/0.83] [performance 4 velocity layers, 3-4 round robins]
  - "cello_pizzicato" (C2..C5) — solo cello pizzicato — four alternate plucks at every recorded root  [env 0/0.06/2.06,0.68↑] [performance 4 round robins]
  - "bagpipe" (G3..C7) — Karoryfer Squidpipes bagpipe — clean sustained chanter recordings; write a separate held note for a drone  [env 0.05/5.5/5.54]
  - "bagpipe_short" (G3..C7) — Karoryfer Squidpipes bagpipe — four alternate short attacks at every chromatic root  [env 0.02/0.11/0.41] [performance 4 round robins]
  - "clean_electric_guitar" (B1..D6) — processed Fender electric guitar — dedicated clean amplifier tone with four alternate attacks and two dynamics through E4  [env 0.02/0.3/8.13,3.17↑] [performance 2 velocity layers, 4 round robins]

### D.2 DRUMS

DRUMS (a track with "instrument":"drums"; note = one of):
  kick, snare, snare_soft, hat_closed, hat_open, crash, tom, e_kick, e_kick_deep, e_snare, e_clap, e_hat_closed, e_hat_open, e_tick, hand_clap, finger_clap, finger_snap, stomp, chest_thump, hat_pedal, hat_half_open, hat_three_quarter, hat_splash, ride, ride_bell, snare_rimshot, snare_cross_stick, snare_flam, snare_buzz, snare_muted, timbale_hi, timbale_lo, cuica_muted, cuica_open, snare_tight, snare_dry_muted, snare_prepared, snare_spring, snare_brush, snare_stir_long, snare_stir_long_light, snare_stir_short, snare_stir_short_light, china_cymbal, cymbal_stack, cymbal_stack_edge, sizzle_ride, sizzle_ride_edge, sizzle_ride_bell, bongo_hi, bongo_lo, conga, conga_slap, darbuka, darbuka_tek, frame_drum, cajon, agogo_hi, agogo_lo, cabasa, claves, cowbell, guiro, shaker, tambourine, tambourine_shake, triangle, triangle_mute, woodblock, gong, sleigh_bells, log_drum_hi, log_drum_lo, didgeridoo_bark, didgeridoo_short, didgeridoo_tap, suspended_cymbal_hit, suspended_cymbal_bell, suspended_cymbal_stick, suspended_cymbal_bowed, cymbal_swell_1_5s, cymbal_swell_2s, cymbal_swell_4s, cymbal_swell_7_5s, suspended_cymbal_scrape, mark_tree_up, mark_tree_down, mark_tree_fast_up, mark_tree_slow_up, mark_tree_slow_down, mark_tree_random, bell_tree, vibraslap, anvil, brake_drum, brake_drum_bowed, finger_cymbals, flexatone, flexatone_fast, flexatone_long, flexatone_extra_long, flexatone_slap, ratchet_crank, ratchet_fast, ratchet_slow, slapstick, ukulele_body_tap, ukulele_chuck, castanets, maracas_forward, maracas_backward

#### LONG TAILS

  LONG TAILS (seconds of ring after the hit — do NOT put these on a fast
  pattern unless you want a wash; shorten with "dur"): gong 30.79s · mark_tree_random 21.45s · suspended_cymbal_bowed 15.87s · sizzle_ride_edge 15.3s · snare_stir_long 15s · cymbal_swell_7_5s 14.98s · mark_tree_fast_up 13.22s · flexatone_extra_long 12.49s · cymbal_swell_4s 11.87s · suspended_cymbal_hit 11.6s · mark_tree_slow_up 11.22s · snare_stir_long_light 11s · snare_stir_short 11s · mark_tree_slow_down 10.73s · cymbal_swell_1_5s 10.31s · cymbal_swell_2s 9.87s · mark_tree_down 9.87s · ratchet_slow 9.29s · flexatone_long 8.96s · crash 8.48s · china_cymbal 8.29s · snare_stir_short_light 8s · suspended_cymbal_stick 7.94s · ratchet_fast 7.86s · mark_tree_up 7.76s · sizzle_ride 7.65s · suspended_cymbal_scrape 7.55s · suspended_cymbal_bell 7.25s · ride 6.72s · finger_cymbals 6.34s · hat_three_quarter 6.24s · brake_drum_bowed 5.24s · ride_bell 5.21s · triangle 4.58s · bell_tree 4.32s · flexatone_fast 4.32s · sizzle_ride_bell 4.11s · hat_splash 4.03s · flexatone 3.56s · vibraslap 2.87s · kick 2.46s · snare_cross_stick 2.32s · didgeridoo_bark 2.06s · hat_open 2.04s

#### FIXED RECORDED MIC PERSPECTIVES

  FIXED RECORDED MIC PERSPECTIVES (not a note key): overhead: hat_pedal, hat_half_open, hat_three_quarter, hat_splash, ride, ride_bell, snare_rimshot, snare_cross_stick, snare_flam, snare_buzz, snare_muted, timbale_hi, timbale_lo, cuica_muted, cuica_open, snare_tight, snare_dry_muted, snare_prepared, snare_spring, snare_brush, snare_stir_long, snare_stir_long_light, snare_stir_short, snare_stir_short_light · close: china_cymbal, cymbal_stack, cymbal_stack_edge, sizzle_ride, sizzle_ride_edge, sizzle_ride_bell
  Core families — pick the vocabulary that serves the performance:
  * acoustic kit (kick, snare, snare_soft, hat_closed, hat_open, crash, tom):
    real recorded drums — rock, pop, jazz, cinematic.
  * electronic kit (the e_* names): synthesized 808/909-style — techno,
    trance, house, EDM. e_kick 4-on-the-floor, e_clap on backbeats,
    e_hat_closed off-beat 8ths, e_tick for minimal percussion.
  * WORLD PERCUSSION (real recordings): Latin/Brazil — bongo_hi/bongo_lo,
    conga, conga_slap, cajon, agogo_hi/agogo_lo, cabasa, claves, cowbell,
    guiro, shaker, castanets, maracas_forward, maracas_backward, tambourine,
    tambourine_shake; Middle East — darbuka,
    darbuka_tek, frame_drum; Africa — log_drum_hi/log_drum_lo; orchestral/
    far-east color — triangle, triangle_mute, woodblock, gong, sleigh_bells;
    plucked-string performance — ukulele_body_tap, ukulele_chuck.
    Layer them as groove spice (bossa: shaker 8ths + claves 2-3 clave +
    agogo; Middle-East: darbuka dum-tek patterns; samba: agogo + cabasa).
    maracas_forward/backward are the two physical stroke directions: alternate
    them for a natural continuous shake. castanets rotate 16 real strikes and
    suit sparse Spanish/flamenco accents better than a constant hi-hat role.
  * BODY PERCUSSION (real human performances): hand_clap, finger_clap,
    finger_snap, stomp, chest_thump. These are not electronic substitutes:
    use them for organic backbeats, ensemble layers, intimate pulses, and
    physical accents. hand_clap/finger_clap/stomp/chest_thump carry recorded
    soft and hard layers; all five rotate 4-12 alternate takes automatically.
  * EXTENDED ACOUSTIC DRUMS (one coherent overhead-mic performance):
    hat_pedal, hat_half_open, hat_three_quarter, hat_splash, ride, ride_bell,
    snare_rimshot, snare_cross_stick, snare_flam, snare_buzz, snare_muted,
    timbale_hi, timbale_lo, cuica_muted, cuica_open. These are distinct playing
    techniques, not synonyms for the basic kit. Velocity automatically chooses
    up to 16 recorded dynamics; repeated hats/rides/timbales/cuicas rotate
    3-7 alternate takes. Rides are cymbals but never join the hi-hat choke group.
  * SNARE CHARACTERS (one coherent overhead-mic collection): snare_tight is
    short and controlled; snare_dry_muted is damped; snare_prepared is an
    altered deep drum; snare_spring adds a conspicuous metallic rattle; and
    snare_brush is a real brush strike. They carry 6-7 recorded dynamics and
    four alternate hits per layer. snare_stir_long/long_light/short/short_light
    are 8-15 second performed brush circles, each with three alternate takes:
    place them as sparse continuous motion and use a note object with "durB"
    when the stir must stop before its natural recording ends.
  * CYMBAL COLOURS (one close-mic collection): china_cymbal is a broad,
    trashy inverted crash; cymbal_stack is a dense, clattering center strike
    and cymbal_stack_edge is its more explosive edge. sizzle_ride carries a
    sustained rivet haze, sizzle_ride_edge opens into wash, and
    sizzle_ride_bell gives a focused metallic ping above that haze. "vol"
    chooses 4-10 recorded dynamics and repeated hits rotate 3-4 alternate
    takes. Use the China/stack as deliberate accents or transitions; the
    sizzle bow/bell can keep spacious time. Use "durB" only when the natural
    ring must be cut for an arrangement boundary.

#### RECORDED MIC POLICY

  RECORDED MIC POLICY: the catalog's overhead/close labels are fixed source
  facts, not interchangeable effects. No "mic" note key exists because the
  selected families contain one coherent registered perspective each. Use
  depth/tone/EQ/reverb for placement; do not invent unavailable mic channels.
  * ACOUSTIC COLOURS AND TRANSITIONS (real performed gestures):
    didgeridoo_drone, didgeridoo_phrase and ocean_drum are instrument tracks;
    trigger their only natural-pitch key C4. They rotate long recorded takes,
    so use them as sparse foreground/texture events, not as keyboard parts.
    didgeridoo_bark/didgeridoo_short/didgeridoo_tap are compact percussion.
    suspended_cymbal_hit/bell/stick choose recorded dynamics from "vol";
    suspended_cymbal_bowed and suspended_cymbal_scrape are dark tension colors.
    cymbal_swell_1_5s/cymbal_swell_2s/cymbal_swell_4s/cymbal_swell_7_5s name
    the recorded rise time: start one that many seconds before the boundary so
    its crest lands on the cut/drop. mark_tree_up/down/fast_up/slow_up/
    slow_down/random, bell_tree and vibraslap are directional punctuation,
    not repeating timekeepers.
    anvil, brake_drum, slapstick and finger_cymbals are real orchestral accent
    recordings, not substitutes for a normal kick, snare or hi-hat. "vol"
    selects the recorded strength where layers exist. brake_drum_bowed is a
    6-7 second metallic tension gesture. flexatone/flexatone_fast are roughly
    4 seconds, flexatone_long is 8-9 seconds, flexatone_extra_long is roughly
    12.5 seconds, and flexatone_slap is a compact accent. ratchet_crank is a
    1-2 second turn; ratchet_fast/ratchet_slow are performed 7-10 second rolls.
    Start a timed gesture early when its motion must arrive at a boundary; do
    not trigger it on the boundary and expect its ending there. For any long
    drum-name gesture that must stop early, use a note object with "durB";
    compact drum strings have no duration slot. Example:
    {"b":0,"note":"mark_tree_random","vol":0.5,"durB":8}.
  Any single drum may ALSO be a track of its own ("instrument":"e_kick")
  and used like an instrument; add "note" to tune the hit — a track of
  pitched e_kick notes (C1, Eb1, ...) IS the classic 808 bassline. Tuned
  toms ("instrument":"tom" with notes) give cinematic pulses.

### D.3 SYNTH KNOBS

SYNTH KNOBS (SYNTHESIZER instruments ONLY — the ones marked "synth:" above;
recorded instruments have no knobs). EVERY synth sound — all the basses,
leads, pads, keys, stabs and FX — takes the same knob set, so pick the
closest named character first, then bend it:
  Add "controls" on the track — each knob 0-10, like a real synth front
  panel (TB-303 / microKorg / Moog); omit a knob to keep the patch default
  (the default is visible in the patch's [DNA] line above):
    cutoff (filter brightness — 2=dark/closed, 5=half open, 6-8=present and
      bright, 10=fully open. Do not equate audible with bright: a darker part
      can speak through register, arrangement space, envelope, and level.)
    resonance (filter squelch/whistle — the acid ingredient, 7-9 for acid)
    envMod (how far the filter sweeps per note — plucky wow)
    attack, decay, sustain, release (shape: pluck = low sustain + short
      decay; pad = high attack/release)
    drive (distortion: 0 clean, 5 warm, 9 screaming)
    detune (stereo width/thickness — supersaw trance = 6-8)
    sub (sub-oscillator weight one octave down — bass power)
    noise (breathy/gritty texture)
    lfoRate + wobble (rhythmic filter wub — dubstep/electro; wobble 5-8)
    vibrato (pitch wobble)
    sweep (filter opens/closes across the WHOLE note — risers, evolving pads)
    pitchDrop (attack pitch transient — 808 knock / donk / zap character;
      3 subtle knock, 8 full laser)
  The TRACK EFFECTS below go in the SAME "controls" object.
  Per-note overrides: "c":{...} on a note — ramping "c":{"cutoff":2→9}
  across a bar writes the classic acid filter sweep. "slide":1 on a note
  glides its pitch from the previous note (TB-303 slide).
  Example acid line:
    {"instrument":"acid_bass","controls":{"cutoff":3,"resonance":8,"envMod":7,"drive":5,"echo":3},
     "notes":[{"t":0,"note":"A1","dur":0.22,"vol":0.9},
              {"t":0.25,"note":"A1","dur":0.22,"vol":0.5,"slide":1,"c":{"cutoff":5}},
              {"t":0.5,"note":"C2","dur":0.22,"vol":0.8,"c":{"cutoff":7}}]}

## E. PERFORMING THE NOTE

### E.1 PER-NOTE EXPRESSION — PERFORM THE NOTE, NOT ONLY ITS PITCH

  Any synth, sampled instrument or drum object-form note may add "expr". Each
  lane is an array of [phase,value] points. Phase is normalized across the
  authored note duration: 0 is its beginning and 1 is note-off; the final
  value holds through a synth release or recorded tail. Use 2..32 points. The
  first phase MUST be 0 and the last MUST be 1, phases must be strictly
  increasing, and interpolation is linear.

  {"b":0,"note":"F4","durB":3,"vol":0.65,
   "expr":{
     "gain":[[0,.4],[.25,.85],[.8,.8],[1,.55]],
     "pitchCents":[[0,-18],[.2,0],[.8,7],[1,0]],
     "pan":[[0,-.15],[1,.2]],
     "vibrato":[[0,0],[.6,0],[.78,.35],[1,.2]],
     "timbre":[[0,.3],[.55,.5],[1,.7]]
   }}

  The five lanes are independent and optional:
    gain        0..2 multiplier on authored vol. It combines with volTo,
                the compact form for one linear swell.
    pitchCents  -2400..2400 cents added continuously. Small scoops/falls around
                ±10..200 cents stay phrased; octave-scale moves intentionally
                expose resampled/accelerated texture, especially on recordings.
    pan         -1..1 OFFSET added to the note's static pan and clamped. Keep
                bass ownership centered unless moving it is the concept.
    vibrato     0..1 depth, mapped to 0..40 cents at a fixed natural 5.2Hz.
                Delay its entrance instead of putting full vibrato at phase 0.
    timbre      0=dark, .5=neutral, 1=bright. Below neutral closes a continuous
                filter; above it adds bounded presence. This shapes the existing
                voice—it does not select or manufacture a different recording.

  Expression runs on the completed voice, so the same language shapes factory
  synths, ex_ synths, real samples, sample releases and drums. pitchCents and
  vibrato continuously resample a recorded voice; extreme upward bends can
  consume its finite source sooner. Curves are deterministic and never add
  random performance decisions.

  "art" also accepts exactly eight GENERIC performance shorthands on any note:
    legato    softer connected envelope/color; not interval morphing
    tenuto    sustained, even weight
    staccato  short duration with a decisive release
    accent    bright, strong attack that settles
    ghost     quiet, dark under-statement
    mute      shortened, damped decay
    breathy   soft attack and restrained color; it does not invent breath noise
    bend      a fixed scoop-in and small ending lift
  A generic articulation expands into ordinary duration/expression data. If a
  sampled instrument declares that same word in the recorded list above, the
  real recorded articulation wins and the fallback is not applied. An explicit
  expr lane replaces the matching shorthand lane but leaves its other lanes in
  place. The generic fallback does not become a new recording and never claims
  a performed technique that the sample supplier did not provide. For a unique
  phrase, write expr directly; use art when its stable shorthand means exactly
  what the line needs.

#### RECORDED BOW AND RELEASE POLICY

  RECORDED BOW AND RELEASE POLICY is automatic by default:
    upright_arco and cello alternate their real down/up bows without changing velocity.
    Use "bow":"down" or "bow":"up" only when phrase direction matters;
    directed bows keep a separate counter and do not disturb later automatic
    alternation. Other instruments reject "bow" because they declare no such
    recordings. A bank with [performance note-off samples] plays its authentic
    release when "dur" ends. "release":"none" suppresses that recording for
    a deliberately gated/cut gesture; "natural" is the default. A release
    choice on a bank/note with no real note-off recording is a compile error.

#### SAMPLE SHAPING

  SAMPLE SHAPING uses object-form notes on RECORDED instruments only, after
  velocity/articulation/take selection:
    "sampleStart": source seconds to skip before playback (>=0)
    "reverse": true plays the chosen main take backwards
    "damp": 0..10 removes high frequencies (0=open, 10=muffled)
  Example: {"b":15.5,"note":"C4","durB":0.5,"vol":0.35,
            "sampleStart":0.18,"reverse":true,"damp":4} can turn a cymbal or
  texture tail into a dark pickup. Reverse bypasses forward sustain loops and
  note-off releases; sampleStart skips from the reversed beginning too. Use
  these for deliberate pickups, reversed swells, fragments and shadow hits,
  not random novelty on every event. Placing them on a synth is a compile error.

#### PITCH-INDEPENDENT TIME FITTING

  PITCH-INDEPENDENT TIME FITTING is opt-in on a recorded object-form note:
    "stretch":"fit" requires an explicit "dur"/"durB" and fits the selected
    real take to exactly that musical span WITHOUT lowering pitch when it is
    made longer or raising pitch when shortened. Pitch selection happens
    first; one deterministic waveform-matched grain plan then serves both
    stereo channels. Use it to land a drone, phrase, swell, cymbal drag, brush stir
    or other texture on a bar boundary. Moderate fits around 0.5x-2x sound most
    natural; extreme ratios are accepted but intentionally become granular texture.
    "fit" bypasses a sustain loop because it reshapes the whole main take;
    an authentic forward note-off still starts at the written duration. Reverse
    still bypasses that release. Loops are cleaner for indefinitely held notes;
    fit is for preserving the beginning, development and ending of a recording.
    Any other stretch word, a missing duration, or use on a synth is a compile
    error. Example: {"b":0,"note":"C4","durB":8,"vol":0.4,
                    "stretch":"fit"} makes a performed texture fill two bars.

#### ENGINE FACT

  ENGINE FACT: WITHOUT "stretch":"fit", "dur" can only SHORTEN an ordinary
  one-shot. It can extend a bank only when that row explicitly says
  [performance sustain loop].
  Compose recorded parts accordingly:
  * An unlooped recording stops at its measured [env] end. If you need a chord
    held longer than that, choose a cataloged loop-capable bank or a synth patch
    (analog_pad, glass_pad, evolving_pad, strings_pad...). Writing dur:8 on an
    ordinary one-shot never manufactures six extra seconds of sound.
  * DECAYING instruments (guitar, piano, marimba, kalimba — tiny b, long e):
    trigger and let them ring. Omit "dur" for the natural decay, or set it to
    damp the note early. This is how the real instrument behaves.
  * SUSTAINING one-shots (cello, organ, bagpipe, harmonica — b close to e): "dur"
    sets the length only up to that recording's measured [env] end.
  * NEW ACOUSTIC STRING/REED COLOURS: accordion has authored sustain loops
    and real key-release recordings, so written duration controls a held
    bellows tone cleanly. classical_guitar is the real nylon-string acoustic
    choice; do not substitute an electric guitar when the brief asks for it.
    ukulele is a bright, compact plucked instrument, not a generic guitar
    preset. Its physical body knock and muted strum are separate drum names
    ukulele_body_tap and ukulele_chuck; place those on a drums track when the
    same player should add an organic rhythmic layer.
  * NEW AMPLIFIED GUITAR/KEY COLOURS: clean_electric_guitar is a dedicated
    clean-amplifier Fender tone; jazz_guitar is warmer and rounder for comping
    and single-note jazz lines. overdriven_guitar is the brighter, biting gain
    tone; distortion_guitar is the darker, denser high-gain alternative. All
    four rotate four real attacks, and "vol" selects soft/loud recordings
    through the low and middle register. Write plausible guitar phrases, riffs
    and power-chord voices rather than piano-like block chords.
    honky_tonk_piano is a historic player piano with a wide, imperfect saloon
    character; choose ordinary piano for a clean grand sound.
  * REAL PIPE-ORGAN REGISTRATIONS: organ is the recorded full Renaissance
    registration. organ_8ft is the foundational unison stop; organ_4ft is the
    brighter stop whose pipes speak one octave above the corresponding key.
    JSON pitches always describe SOUNDING pitch. For an authentic two-stop
    registration, voice organ_4ft one octave above organ_8ft, or choose organ
    when the already-recorded full registration is the better musical answer.

## F. SOUND DESIGN — NEW INSTRUMENTS FROM THE SCORE

### F.1 CUSTOM SYNTHESIS — BUILD A NEW INSTRUMENT WHEN THE PALETTE NEEDS ONE

  Factory patches are finished instruments selected by name. A custom patch is
  a new instrument blueprint encoded under top-level "synths". Use this path
  when the request needs a signature timbre the factory palette cannot supply,
  not merely because custom numbers appear more creative.

  Every custom name is required to start with "ex_"; tracks then use that name
  as their instrument. The compact single-oscillator fields are the same DNA
  shown in the factory catalog, written as JSON. All are optional except osc;
  out-of-range values are compiler errors and are never clamped:
    osc "saw"|"square"|"sine"|"fm"|"noise" (required) ·
    noiseColor "white"|"pink"|"crackle" · unison 1-8 · detuneCents 0-100 ·
    fmRatio 0.25-12, fmIndex 0-12, fmDecay sec · sub 0-1 · noise 0-1 ·
    cutoff 30-16000 Hz (above ~8k the filter is effectively open — brightness
    past that comes from the oscillator, not the cutoff) ·
    cutoffEnv 0-8000 Hz · filterDecay sec · res 0-0.9 ·
    cutoffRise ±12000 Hz (sweep across the whole note) ·
    attack/decay/release sec, sustain 0-1 ·
    lfoRate Hz, lfoCutoff Hz (wobble), lfoPitch cents (vibrato) ·
    lfoShape "sine"|"sh" (sh = sample-and-hold: the LFO STEPS to a new
    random level each period instead of sweeping — with lfoCutoff it can
    create modular, non-repeating texture) ·
    drive 1-8 (1 = clean) · gain 0-1 ·
    pitchDropSemis ±48 + pitchDropSec (attack knock/donk/laser) ·
    pitchRiseSemis ±48 (pitch glides this far over the note).

#### CUSTOM PATCH WORKFLOW — START FROM FACTORY DNA, NOT RANDOM NUMBERS

  find the closest factory sound, copy its represented fields into the ex_
  definition, then make purposeful changes whose audible effect serves the
  composition. Preserve important envelope/filter motion unless changing the
  sound class is intentional. For example, a saw stab with a static lowpass is
  a flat buzz that may read as chiptune; saw_chords/rave_stab uses cutoffEnv +
  filterDecay so every hit opens and closes.
  Knobs, the pedalboard and automation work on ex_ sounds, with two routing/
  effect details: declare "bus":"bass" when an ex_ patch is the bass role, and
  synth "drive" is voice saturation rather than the pedalboard drive described
  below. Example:
    {"synths":{"ex_growl":{"osc":"fm","fmRatio":2,"fmIndex":7,"fmDecay":2,
       "cutoff":500,"res":0.5,"sub":0.3,"attack":0.005,"decay":0.4,
       "sustain":0.8,"release":0.2,"drive":3}},
     "tracks":[{"id":"GROWL_TRACK","instrument":"ex_growl","notes":["0 A1 0.45 0.9"]}]}
  This workflow opens the entire synthesizer without discarding the accumulated
  design knowledge in the factory palette. A factory patch is a selection; an
  ex_ patch is an authored instrument.

### F.2 DUAL-OSCILLATOR SYNTHESIS — USE A NEW TOPOLOGY, NOT MORE RANDOM NUMBERS

  The compact shape above is the right tool for one-oscillator subtractive
  sounds and the simplest two-operator FM (one ratio, one index, one decay;
  more than that is section F.3). Factory sounds whose [DNA] begins "dual" use the expanded architecture
  below internally. Use this shape only when the musical idea specifically needs
  two oscillator identities, sync, ring modulation, a non-low-pass filter, an
  authored wavetable, multiple modulators or coordinated macro movement. Define
  osc1 and osc2 inside the same top-level "synths" bank; their presence selects
  this structure automatically, and the track still uses its ex_ name. Compact
  and dual-oscillator factory/custom patches may coexist in one score.

#### DUAL-OSCILLATOR SHAPE

  DUAL-OSCILLATOR SHAPE (osc1 and osc2 are required; other fields have safe defaults):
    {"osc1":{...},"osc2":{...},
     "blend":0.5,"sync":0,"ring":0,"shape":0,
     "filter":{...},"amp":{...},"env2":{...},
     "lfo1":{...},"lfo2":{...},"mod":[...],"macros":{...}}

#### EACH OSCILLATOR

    wave "sine"|"saw"|"square"|"triangle"|"noise"|"wavetable" (required) · level 0-1.
    Triangle: odd harmonics falling fast (softer than square, rounder than
      saw) — flutes, soft leads, sub-layers, chip-style basses.
    Pitched waves: octave integer -4..4 · semitones -24..24 ·
      fineCents -100..100 · phase "reset"|"random" · phaseOffset 0..1 cycle.
    Square only: pulseWidth 0.05..0.95.
    Noise only: noiseColor "white"|"pink"|"crackle"; pitch/phase fields are
      rejected because they would do nothing.
    Wavetable only: table = 8..64 finite values, each -1..1, describing ONE
      repeating cycle. The compiler removes DC and peak-normalizes that cycle;
      playback uses linear interpolation. This is authored waveform synthesis,
      not sample playback and not the granular source deferred to section 9.

#### OSCILLATOR TOPOLOGY AND OUTPUT

    blend 0..1 (0=osc1, 1=osc2) · sync 0..1 (osc1 hard-resets osc2; requires
      two pitched oscillators) · ring 0..1 (crossfades toward osc1×osc2) ·
    shape 0..1 (bounded tanh waveshaping) · sub 0..1 · noise 0..1 ·
    unison integer 1..6 · detuneCents 0..100 · stereo 0..1 ·
    drive 1..8 (1 clean) · gain 0..1.
    Oscillators run 2x oversampled. Blend uses power compensation, unison uses
    constant-power stereo placement, resonance/nonlinear stages are compensated,
    and a final attenuation-only peak guard catches extreme valid combinations.

  FILTER, ENVELOPES AND LFOs:
    filter {"mode":"lowpass"|"bandpass"|"highpass"|"notch",
            "cutoff":30..16000 Hz,"res":0..0.9,"keytrack":0..1}
    amp and env2 each use {"attack":0.001..4 sec,"decay":0.005..8 sec,
      "sustain":0..1,"release":0.005..8 sec}. amp shapes level; env2 is a
      separate modulation source and does nothing until routed deliberately.
    lfo1 and lfo2 each use {"shape":"sine"|"triangle"|"square"|"sh",
      "rateHz":0.01..40,"phase":0..1}. "sh" draws seeded held values.
    cutoffRise -12000..12000 Hz and pitchRiseSemis -48..48 move across the
      whole note. pitchDropSemis -48..48 + pitchDropSec 0.01..0.5 make the
      attack knock/scoop. These exact fields remain available beside macros.

#### COMPILER-ACCEPTED MODULATION MATRIX

  COMPILER-ACCEPTED MODULATION MATRIX — maximum 8 routes:
    {"source":"env2"|"lfo1"|"lfo2",
     "target":"pitch1"|"pitch2"|"blend"|"sync"|"ring"|"shape"|
              "cutoff"|"resonance"|"pan",
     "amount":<signed depth>}
    Amount units follow the destination: pitch1/pitch2 ±48 SEMITONES; cutoff
    ±12000 HZ; resonance ±0.9; blend/sync/ring/shape/pan ±1. Values add, then
    clamp to the safe destination range each sample. A pitch route to a noise
    oscillator or a sync route involving noise is a compile error, not a
    silent matrix cable.
    The target list above is complete. "amplitude", "amp", "volume" and
    "gain" are NOT synth-matrix destination names. For audible volume pulsing,
    use track controls.tremolo or route the track through a named-bus tremolo
    effect; both act after the synth voices are mixed. This is a compiler/DSP
    boundary, not a licensing rule.

#### MUSICAL MACROS

  MUSICAL MACROS — optional 0..1 additions, NEVER replacements for exact fields:
    motion: slow lfo1 filter/pitch movement plus lfo2 blend/pan movement ·
    roughness: coordinated waveshape, ring and a small noise edge ·
    inharmonicity: offsets osc2 by up to 6.93 semitones and raises ring texture ·
    air: opens the filter by up to 3000 Hz and adds quiet high-passed stereo air ·
    body: adds up to 0.35 of a centered sub fundamental.
  Macro behavior is fixed, bounded and documented so words remain repeatable.
  Use a macro for a broad musical direction, then exact fields/routes for the
  detail that defines the patch. All five macros are deterministic.

#### ENGINE STARTER DNA FOR DUAL-OSCILLATOR SYNTHS

  ENGINE STARTER DNA FOR DUAL-OSCILLATOR SYNTHS — copy the closest factory [DNA] or ROLE, rename it
  and make purposeful changes. The examples below are blueprints rather than
  registered factory sounds:
    "ex_dual_bass":{
      "osc1":{"wave":"sine","level":1},
      "osc2":{"wave":"square","level":0.55,"octave":-1},
      "blend":0.28,"sub":0.5,
      "filter":{"mode":"lowpass","cutoff":520,"res":0.18,"keytrack":0.15},
      "amp":{"attack":0.004,"decay":0.4,"sustain":0.82,"release":0.18},
      "drive":2.2,"gain":0.78}
    "ex_dual_pad":{
      "osc1":{"wave":"saw","level":0.9,"phase":"random"},
      "osc2":{"wave":"wavetable","level":0.8,"phase":"random",
        "table":[0,0.8,1,0.25,-0.2,-0.7,-1,-0.35]},
      "blend":0.5,"unison":5,"detuneCents":20,"stereo":0.95,
      "filter":{"mode":"notch","cutoff":1800,"res":0.2,"keytrack":0.3},
      "amp":{"attack":0.38,"decay":0.7,"sustain":0.9,"release":0.8},
      "lfo1":{"shape":"sine","rateHz":0.22,"phase":0},
      "macros":{"motion":0.55},"gain":0.58}
    "ex_dual_pluck":{
      "osc1":{"wave":"square","level":0.8,"pulseWidth":0.22},
      "osc2":{"wave":"sine","level":0.7,"octave":1},"blend":0.35,
      "filter":{"mode":"bandpass","cutoff":650,"res":0.62,"keytrack":0.65},
      "amp":{"attack":0.002,"decay":0.22,"sustain":0,"release":0.12},
      "env2":{"attack":0.002,"decay":0.14,"sustain":0,"release":0.08},
      "mod":[{"source":"env2","target":"cutoff","amount":6200}],"gain":0.78}
    "ex_dual_sync_lead":{
      "osc1":{"wave":"saw","level":1},
      "osc2":{"wave":"saw","level":0.8,"semitones":12},
      "blend":0.48,"sync":0.68,"shape":0.18,"unison":2,"detuneCents":8,
      "filter":{"mode":"highpass","cutoff":380,"res":0.28,"keytrack":0.2},
      "amp":{"attack":0.006,"decay":0.25,"sustain":0.72,"release":0.24},
      "env2":{"attack":0.001,"decay":0.35,"sustain":0,"release":0.1},
      "mod":[{"source":"env2","target":"sync","amount":0.3}],
      "drive":1.8,"gain":0.65}
    "ex_dual_air":{
      "osc1":{"wave":"noise","level":0.8,"noiseColor":"pink"},
      "osc2":{"wave":"wavetable","level":0.35,"octave":2,
        "table":[0,1,0.2,-0.3,0.1,-1,-0.2,0.35]},"blend":0.72,
      "filter":{"mode":"highpass","cutoff":4200,"res":0.1,"keytrack":0},
      "amp":{"attack":0.08,"decay":0.4,"sustain":0.62,"release":0.35},
      "macros":{"air":0.6,"motion":0.25},"gain":0.48}
    "ex_dual_bell":{
      "osc1":{"wave":"sine","level":1},
      "osc2":{"wave":"sine","level":0.9,"semitones":5,"fineCents":23},
      "blend":0.5,"ring":0.82,
      "filter":{"mode":"bandpass","cutoff":5100,"res":0.35,"keytrack":0.5},
      "amp":{"attack":0.002,"decay":1.1,"sustain":0,"release":0.7},
      "macros":{"inharmonicity":0.72},"gain":0.62}

  The same 16 track controls and per-note "c" overrides documented above work
  on dual-oscillator and FM operator patches: cutoff/resonance, ADSR, envMod, drive, detune,
  sub/noise, LFO rate, wobble, vibrato, sweep and pitchDrop. Pedal effects and
  automation remain outside the voice for every synth shape. Dual-oscillator
  and compact definitions both reject unknown fields. Dual definitions also
  reject nonsensical nested combinations and more than eight routes.

#### TIMBRE MUST MATCH INTENT

  - Exposed square waves, clean sine/FM plinks, rapid high-register arpeggios
    and equal-velocity one-finger melodies readily read as 8-bit, music-box or
    keyboard-demo material. Use them only when that character is requested.
  - For contemporary club music, make a hook RHYTHMIC before making it busy:
    a short syncopated 1-3 pitch cell, moving-filter stab, texture or vocal-space
    gesture. Do not let a bright keyboard patch continuously narrate the track.
  - Do not stack a factory unison patch, maximum detune and heavy chorus by
    reflex. The 2020 voice is already stereo; extra widening can smear attacks.

### F.3 FM OPERATOR SYNTHESIS — WRITE THE ALGORITHM, NOT A PRESET NUMBER

  The compact "fm" oscillator is one fixed pair: a sine modulating a sine with
  one ratio, one index and one index decay that always falls to zero. When
  the sound needs more — an index that settles to a floor instead of dying, a
  second stack for a tine click, feedback edge, a fixed-frequency formant,
  saw or square operators, velocity opening the brightness — define "ops"
  inside the same top-level "synths" bank. Presence of ops selects this
  architecture; the track still uses its ex_ name. Compact, dual and operator
  patches may coexist in one score. This is the DX7 / Operator model: every
  classic "algorithm" is one particular route list below, written out so the
  model can read which operator is heard and which one shapes it.

#### OPERATOR SHAPE

  OPERATOR SHAPE (ops is required; everything else has safe defaults):
    {"ops":[{...},{...}],"routes":[{"from":2,"to":1,"index":3}],
     "filter":{...},"amp":{...},"env2":{...},
     "lfo1":{...},"lfo2":{...},"mod":[...]}

#### EACH OPERATOR (1..6, numbered by array position starting at 1)

    wave "sine"|"triangle"|"saw"|"square" (default sine; a saw or square
      modulator is already rich, so keep its index low) ·
    ratio 0.125..32 = frequency as a multiple of the note (default 1), OR
    fixedHz 0.1..20000 = an absolute frequency that ignores the note, slide,
      vibrato and every pitch envelope (formants, sub-audio modulators that
      act as extra LFOs, inharmonic clang). ratio and fixedHz are mutually
      exclusive on one operator ·
    detuneCents -100..100 (two carriers 4-8 cents apart = chorus) ·
    level 0..1 = how much of this operator reaches the audio output (default
      0: a pure modulator). An operator may both sound and modulate ·
    env {"attack","decay","sustain","release"} = this operator's OWN
      envelope. It multiplies both its audible level and its modulation
      strength, so an envelope on a modulator IS the index envelope. Omitted
      = constant. A partial object inherits attack 0.002, decay 0.3,
      sustain 0, release 0.2 ·
    velocity 0..1 = how much note volume ("vol") scales this operator
      (0 = none). On a modulator, louder notes get brighter — the DX7 feel ·
    feedback 0..1 = self phase modulation: 0.2-0.4 thickens a sine, 0.5-0.7
      turns it saw-like, 0.9+ is harsh noise-edge.

#### ROUTES — THE ALGORITHM, WRITTEN EXPLICITLY

    {"from":<modulator op>,"to":<carrier op>,"index":0..12}  (up to 12)
    The graph must be acyclic: 3>2 plus 2>1 is a stack, 2>1 plus 3>1 is a
    parallel pair into one carrier, two independent pairs are two stacks
    summed at the output. A cycle is a compile error, a self-route is a
    compile error (use feedback), and an operator with level 0 that is not
    the "from" of any route is a compile error — it would be silent for no
    reason. index is the modulator's peak phase deviation in radians when its
    envelope is at 1:
      0.3-1.5 warmth and body · 2-4 bright keys and basses ·
      5-8 bells, tines and metal · 9-12 noise-like.
    Ratio decides character: integer ratios (1, 2, 3, 0.5) are harmonic and
    pitched; non-integer (1.41, 3.5, 7.01) are bells and metal; a ratio of
    10 or more on a modulator with a 50-150 ms envelope is a click or tine.
    Array order does not matter; the compiler sorts the graph.

#### POST CHAIN — THE SAME FIELDS AS A DUAL PATCH

    sub 0..1 · noise 0..1 · unison integer 1..4 · detuneCents 0..100 ·
    stereo 0..1 · drive 1..8 · gain 0..1 · cutoffRise · pitchDropSemis +
    pitchDropSec · pitchRiseSemis ·
    filter {"mode","cutoff","res","keytrack"} defaults to lowpass at
      16000 Hz, res 0 — OPEN, because operators make their own brightness.
      Lower it only to tame a bright stack or for a deliberate filter move ·
    amp = whole-voice ADSR (defaults 0.005/0.3/0.7/0.2); operator envelopes
      shape timbre inside it · env2 (0.005/0.3/0/0.2) is a modulation source
      and does nothing until routed · lfo1/lfo2 as in dual patches.
    Operators run 2x oversampled, feedback is averaged for stability, and the
    final attenuation-only peak guard catches extreme valid combinations.

#### COMPILER-ACCEPTED MODULATION MATRIX — maximum 8 routes

    {"source":"env2"|"lfo1"|"lfo2",
     "target":"pitch"|"index"|"feedback"|"cutoff"|"resonance"|"pan",
     "amount":<signed depth>}
    pitch ±48 SEMITONES moves every ratio operator together (fixedHz ones
    stay) · index ±1 scales EVERY route index (+1 doubles, -1 silences the
    modulators): lfo1>index is timbral wobble, env2>index is one global
    brightness envelope on top of the per-operator ones · feedback ±1 ·
    cutoff ±12000 HZ · resonance ±0.9 · pan ±1. Values add, then clamp.
    "amplitude", "volume" and "gain" are not targets here either; use the
    operators' own env, the amp envelope, or a track tremolo.

#### ENGINE STARTER DNA FOR FM OPERATOR SYNTHS

  ENGINE STARTER DNA FOR FM OPERATOR SYNTHS — the factory op_ sounds are the
  reference graphs (read their [DNA]); the blueprints below show the moves,
  not registered sounds. Rename and change on purpose:
    "ex_op_epiano":{
      "ops":[
        {"ratio":1,"level":1,"env":{"attack":0.002,"decay":2.4,"sustain":0.2,"release":0.5}},
        {"ratio":1,"env":{"attack":0.002,"decay":1.6,"sustain":0.25,"release":0.3},"velocity":0.6},
        {"ratio":1,"detuneCents":4,"level":0.55,"env":{"attack":0.002,"decay":1.8,"sustain":0.15,"release":0.5}},
        {"ratio":14,"env":{"attack":0.001,"decay":0.12,"sustain":0,"release":0.1},"velocity":0.8}],
      "routes":[{"from":2,"to":1,"index":1.6},{"from":4,"to":3,"index":0.9}],
      "amp":{"attack":0.002,"decay":2.5,"sustain":0.25,"release":0.45},"gain":0.7}
    "ex_op_settling_bass":{
      "ops":[
        {"ratio":1,"level":1,"feedback":0.4},
        {"ratio":1,"env":{"decay":0.07,"sustain":0.4,"release":0.1},"velocity":0.7},
        {"ratio":0.5,"level":0.45}],
      "routes":[{"from":2,"to":1,"index":5.9}],
      "filter":{"cutoff":3200,"keytrack":0.3},
      "amp":{"attack":0.002,"decay":0.3,"sustain":0.8,"release":0.12},"drive":1.5,"gain":0.75}
    "ex_op_formant_pad":{
      "ops":[
        {"ratio":1,"level":0.9},
        {"ratio":2,"detuneCents":-6,"level":0.6},
        {"fixedHz":640,"env":{"attack":1.2,"decay":2,"sustain":0.7,"release":1.5}},
        {"fixedHz":3.1,"env":{"attack":0.6,"decay":1,"sustain":1,"release":1}}],
      "routes":[{"from":3,"to":1,"index":1.4},{"from":3,"to":2,"index":0.8},{"from":4,"to":3,"index":0.6}],
      "unison":3,"detuneCents":12,"stereo":0.9,
      "amp":{"attack":0.9,"decay":1,"sustain":0.85,"release":1.4},"gain":0.55}
    "ex_op_metal_pluck":{
      "ops":[
        {"ratio":1,"level":1,"env":{"attack":0.001,"decay":0.6,"sustain":0,"release":0.3}},
        {"ratio":3.5,"env":{"attack":0.001,"decay":0.35,"sustain":0,"release":0.2},"velocity":0.5},
        {"wave":"saw","ratio":1.41,"env":{"attack":0.001,"decay":0.09,"sustain":0,"release":0.05}}],
      "routes":[{"from":2,"to":1,"index":4.5},{"from":3,"to":2,"index":1.1}],
      "lfo1":{"shape":"sine","rateHz":5.5,"phase":0},
      "mod":[{"source":"lfo1","target":"pitch","amount":0.08}],
      "amp":{"attack":0.001,"decay":0.7,"sustain":0,"release":0.3},"gain":0.7}
    The second blueprint is the two-sine lesson with the missing piece: the
    modulator's env (decay 0.07, sustain 0.4) makes every note start bright
    and SETTLE to 40% of index 5.9 instead of fading to a pure sine.
    The third shows what fixedHz is for: operator 3 is a 640 Hz formant that
    stays put while the chord moves, and operator 4 at 3.1 Hz is sub-audio,
    so it slowly wobbles that formant's depth like a third LFO.

  The same 16 track controls and per-note "c" overrides work on operator
  patches (vibrato lands on the shared pitch target). Exact automation
  synth.cutoff/resonance/drive works; synth.index 0..4 is operator-only and
  multiplies every route index while notes are held. The dual-only
  automation targets (blend/sync/ring/shape/pitch1/pitch2) are compile errors
  on operator patches. Unknown fields, cycles, self-routes, duplicate routes,
  a silent patch and more than 6 operators, 12 routes or 8 matrix routes are
  all compile errors, never silent repairs.

### F.4 CUSTOM DRUM SYNTHESIS — DESIGN THE TRACK'S RHYTHMIC IDENTITY

  Factory drums are finished voices selected by name. When none has the needed
  body, transient, dirt, material or decay, define a bounded electronic drum
  under top-level "drumSynths". Every name MUST start with "exd_". A hit in a
  normal drums track then uses only that name:
    {"drumSynths":{"exd_wood":{...}},
     "tracks":[{"id":"DRUM_TRACK","instrument":"drums","notes":[{"t":0,"note":"exd_wood","vol":0.9}]}]}
  The definition is compiled once and reused by every hit. This is sound design,
  not a license to add layers automatically: use it only when the custom voice
  gives the composition a clearer rhythmic fingerprint than a factory choice.

#### FIVE MODELS

  FIVE MODELS ("model" is required):
  * "kick": swept sine body + transient click + colored noise. Soft woody,
    tight club, long sub, knock and thud are different settings of this model.
  * "membrane": tuned three-mode drum skin + damping + transient/noise. Use for
    synthetic toms, hand-drum-like hits and pitched resonant percussion.
  * "clap": 1-8 staggered colored-noise bursts plus optional low body. Burst
    spacing and spread make one compact snap or a loose dusty group.
  * "noise": density-controlled short grains through colored noise. Use for
    shakers, sand, closed/open synthetic hats and granular percussion.
  * "metal": 2-8 freely inharmonic partial ratios + damping + transient/noise.
    Use for bells, steel clicks, alien cymbals and tuned metallic punctuation.

#### COMMON FIELDS

  COMMON FIELDS (all optional after model; omitted fields use safe defaults):
    bus "kit"|"perc" (default kit; perc bypasses kick-keyed drum glue; an
    explicit Track/Pattern bus overrides this patch default) ·
    duration 0.01-4 sec (default HARD generated-audio length; note dur/durB
    replaces it up to the 4-sec custom-hit limit; longer decays and late clap
    bursts are truncated) ·
    gain >0 and <=1 · drive 1-8 (1 clean) ·
    highpassHz 0-12000 · lowpassHz 100-18000 (highpass MUST be lower) ·
    decayVar 0-0.5 · toneVar 0-0.5.
  Variation is small PER-HIT movement around the written DNA, generated from
  the score seed. The same score renders identically; changing the seed changes
  the variation. decayVar selects a decay multiplier uniformly from 1-value to
  1+value. toneVar chooses the same kind of factor for spectral details: it
  multiplies filter and click frequencies, shifts dark/bright noise filtering,
  and moves metal partial ratios away from or toward 1.

#### MODEL FIELDS

  MODEL FIELDS — only write fields belonging to that model:
  * kick: tuneHz 20-300 · pitchStartHz 20-3000 · pitchDecay 0.001-1 sec ·
    body/click/noise 0-1 · bodyDecay/noiseDecay 0.003-4 sec ·
    clickHz 100-16000 · noiseColor "dark"|"white"|"bright" ·
    pitchVarCents 0-100 (uniform ± cents on the body pitch).
  * membrane: tuneHz 20-2000 · pitchStartHz 20-4000 · pitchDecay 0.001-1 ·
    body/click/noise 0-1 · bodyDecay/noiseDecay 0.003-4 · damping 0-1 ·
    clickHz 100-16000 · noiseColor "dark"|"white"|"bright" ·
    pitchVarCents 0-100.
  * clap: bursts 1-8 · spacingMs 1-40 · spread 0-1 (after the first burst,
    seeded timing looseness up to 45% of spacing*spread and level looseness up
    to 30%*spread) · noise/body 0-1 · noiseDecay 0.003-1 · bodyDecay 0.003-1 ·
    tuneHz 20-2000 · noiseColor "dark"|"white"|"bright" ·
    pitchVarCents 0-100 (optional tonal body only). spread is NOT stereo width.
  * noise: noise 0-1 · noiseDecay 0.003-4 · density 1-300 expected grains/sec ·
    noiseColor "dark"|"white"|"bright" · choke "none"|"closed"|"open".
    Closed/open joins the existing physical hi-hat choke only on the kit bus;
    use choke none + bus perc for a free-ringing shaker. pitchVarCents is not a
    noise field because this model has no pitched component.
  * metal: tuneHz 20-4000 · partials = 2-8 strictly ascending frequency
    MULTIPLIERS of tuneHz, each 0.25-32 ·
    body/click/noise 0-1 · bodyDecay/noiseDecay 0.003-4 · damping 0-1 ·
    clickHz 100-16000 · noiseColor "dark"|"white"|"bright" ·
    pitchVarCents 0-100. Earlier/lower partials render louder and longer.
  Out-of-range numbers, non-integer clap bursts, wrong types/enums, unknown
  keys, fields from the wrong model and patches with no audible source are
  COMPILE ERRORS. Output is finite and peak-guarded; there is no feedback path
  an authored patch can destabilize.

#### ENGINE STARTER DNA

  ENGINE STARTER DNA — copy the closest recipe, RENAME it, then change only
  parameters whose audible job you understand. These are working blueprints,
  not mandatory sounds and not extra factory names:
    "exd_woody_kick":{"model":"kick","duration":0.32,"tuneHz":52,
      "pitchStartHz":170,"pitchDecay":0.028,"bodyDecay":0.19,"click":0.16,
      "clickHz":2800,"noise":0.04,"lowpassHz":7200,"drive":2.2,"gain":0.9}
    "exd_dusty_clap":{"model":"clap","duration":0.24,"bursts":4,
      "spacingMs":11,"spread":0.5,"noiseColor":"dark","noiseDecay":0.055,
      "body":0.1,"tuneHz":165,"highpassHz":420,"lowpassHz":7200,"gain":0.75}
    "exd_grain_shaker":{"model":"noise","bus":"perc","duration":0.18,
      "density":95,"noiseDecay":0.14,"noiseColor":"bright",
      "highpassHz":4200,"lowpassHz":15000,"decayVar":0.08,"gain":0.55}
    "exd_tuned_skin":{"model":"membrane","bus":"perc","duration":0.42,
      "tuneHz":145,"pitchStartHz":180,"pitchDecay":0.045,"bodyDecay":0.3,
      "damping":0.4,"noise":0.14,"noiseDecay":0.055,"gain":0.72}
    "exd_steel_hit":{"model":"metal","bus":"perc","duration":0.55,
      "tuneHz":410,"partials":[1,1.39,1.87,2.62,3.31],"damping":0.42,
      "bodyDecay":0.38,"click":0.06,"noise":0.04,"highpassHz":180,
      "lowpassHz":12500,"toneVar":0.04,"gain":0.7}
  To tune one custom drum melodically, make it its OWN track with
  "instrument":"exd_name". C4 plays its authored tuning; other note names
  transpose it relative to C4. In a drums track it plays at authored tuning.
  A note's dur/durB may shorten or extend that hit, up to 4 sec. Patch fields
  themselves are fixed for the score; make a second intentional definition for another drum
  character, and use track effects/automation for arrangement-scale motion.

### F.5 INTERNAL RESAMPLING — TURN THIS COMPOSITION INTO ITS OWN INSTRUMENT

  A top-level "resamples" definition makes a bounded temporary recording of
  material already authored in the same score. Its name MUST start with rs_.
  Nothing is downloaded, written to disk, or added to the permanent catalog.

  Capture one exact track lane (a top-level patterns key identifies a pattern-generated lane; give a
  direct track an "id"):
    "resamples":{
      "rs_kit":{"source":{"track":"KIT"},"fromBeat":0,"beats":4,
                "slices":{"gridBeats":0.25}}
    }
  Or capture a complete mix path with "source":{"bus":"perc"}. Legal built-in
  bus names are kit, perc, bass, bed, lead and fx; a declared named bus is valid
  too. Track capture is after that track's inserts/fader/pan and before its bus.
  Bus capture includes every PRE-RESAMPLE track feeding it and a named bus's
  rack/fader/routing, but excludes built-in polish, master processing, and the
  shared hall/plate returns. This exact boundary keeps a saved score repeatable.

  fromBeat/beats address the source timeline and follow tempoMap exactly. Every
  capture implicitly exposes region "all". One optional "slices" object adds
  ONE of these plans:
    "slices":{"gridBeats":0.25}
      Consecutive numbered regions 0,1,2...; tempo ramps produce exact unequal
      seconds where necessary while every boundary stays on the authored grid.
    "slices":{"regions":{"kick":[0,0.5],"answer":[2,3.5]}}
      Named [startBeat,endBeat] ranges RELATIVE to the capture.
    "slices":{"transients":{"threshold":0.18,"minGapMs":70,"max":24}}
      Numbered deterministic attacks from short-window level rises. threshold
      is .01..1, minGapMs 10..2000, max 1..128. Region 0 always exists; later
      counts depend on the captured sound, so use this on clearly authored
      attacks rather than guessing at a dense or ambiguous source.

  The capture name is now a temporary instrument. C4 plays its captured pitch;
  other notes transpose it by ordinary sample resampling. "region" selects
  "all", a named range, or a numeric grid/transient slice:
    {"instrument":"rs_kit","notes":[
      {"t":8,"note":"C4","region":6,"dur":0.18,"stretch":"fit","vol":0.7},
      {"t":8.25,"note":"G4","region":2,"dur":0.18,"stretch":"fit",
       "reverse":true,"damp":3,"vol":0.55}
    ]}
  Reorder/retrigger slices by writing their note order, gate with dur, repeat
  through patterns, reverse with reverse:true, and separate pitch from duration
  with stretch:"fit". sampleStart, damp, art and expr remain available because
  an rs_ note enters the same sampled-note performance layer. This is authored
  transformation, not an automatic remix.

### F.6 GRANULAR rs_ NOTES — SCAN, FREEZE, AND SCATTER A CAPTURE

  Put "granular" on an rs_ track/pattern as its default, or on one note as an
  override. Every granular note needs explicit positive dur/durB; do NOT add
  stretch:"fit" because granular playback already makes pitch and duration
  independent. Example:
    {"instrument":"rs_chord","bus":"fx",
     "granular":{
       "grainMs":95,
       "density":[[0,8],[.45,30],[1,14]],
       "overlap":.72,
       "scan":[[0,.05],[.6,.85],[1,.3]],
       "positionJitter":.04,"pitchJitterCents":18,
       "window":"hann","stereoScatter":.75
     },
     "notes":[{"t":24,"note":"C4","region":"all","dur":4,"vol":.4,
       "expr":{"gain":[[0,0],[.15,.8],[.8,.7],[1,0]]}}]}

  grainMs          10..500, maximum source-fragment length.
  density          1..200 grains/second, or 2..32 [phase,value] points.
  overlap          0..0.95 maximum adjacent-grain overlap. To respect a low
                   value, the engine may shorten the audible grain below grainMs.
  scan             source position 0..1, as one number or a phase curve.
  freeze           optional source position 0..1; replaces scan with one point.
  positionJitter   0..1 deterministic per-grain displacement across the region.
  pitchJitterCents 0..1200 deterministic per-grain pitch spread.
  window           "hann" | "triangle" | "tukey".
  stereoScatter    0..1 deterministic per-grain pan spread; native stereo uses
                   the same grain schedule and keeps its two recorded channels.
  Phase is 0..1 across that note; density and scan therefore ARE their own
  continuous automation. Curves start at phase 0, end at 1, increase strictly,
  and interpolate linearly. freeze, reverse scan, sparse grains, tiny fragments
  and octave transposition are deliberate sound-design extremes, not defaults.

#### DEPENDENCY AND COST CONTRACT

  DEPENDENCY AND COST CONTRACT: all captures are rendered from one pre-resample
  pass, so an rs_ track can never feed any capture and definition order cannot
  change audio. Recursive/self sources are compile errors. Maximum 16 captures,
  32 seconds each, 120 captured seconds total, 128 slices per capture, and 120
  seconds of overlapping explicit regions per capture. One granular note is at
  most 120 seconds; a complete score may schedule at most about 250,000 grains.
  Every grain choice derives from seed;
  the temporary audio lives only for this render.

## G. MIX AND ROUTING

### G.1 TRACK EFFECTS — A SHARED PRODUCTION RACK FOR EVERY SOUND

  Put these keys in "controls" on recorded instruments, drum tracks,
  single-drum tracks, and synths. Each knob is 0-10; omission means off.
    drive (recorded instruments/drums: pedalboard distortion/overdrive — 3-4
      crunchy rhythm guitar, 6-7 rock lead, 9 heavy. Synth/ex_ tracks are the
      exception: the same key controls per-voice tanh saturation and is NOT
      blended by "wet". clean_electric_guitar + drive is the electric rock guitar)
    crush (bitcrusher/lofi grit: 3-4 dusty lofi-hiphop drums, 7+ broken 8-bit)
    chorus (widens/doubles: dream-pop clean guitar 4-6, thicken pads 3)
    flanger (jet swoosh — swept comb filter with feedback: psychedelic
      drums/pads 4-6, 8+ full jet pass; slower+deeper than phaser)
    phaser (slow swirl: funk guitar, psychedelic keys, moving pads 3-6)
    tremolo (tempo-synced volume flutter: surf guitar 6-8, vintage-amp 3-4)
    wah (envelope AUTO-WAH — the funk pedal: loud notes open the filter,
      quiet ones close it, so the PLAYING drives it; 5-7 funk clav/guitar
      16ths, 3-4 subtle talk on a bass. Pairs with drive: wah runs first)
    eqLow / eqMid / eqHigh (3-band EQ in dB, −12..+12, 0=flat: low shelf
      200Hz / peak 800Hz / high shelf 4kHz). For masking: when
      chords bury the bass, carve eqLow −4 on the chords instead of
      turning them down. Cuts beat boosts.
    lowpass / highpass (DJ filter, 0=open..10=closed/thin — works on
      recorded instruments too; "res" adds squeal)
    reverb (per-track space ON TOP of the shared room: intimate 0-2,
      singing lead 4-5, ambient wash 8-10)
    plate (a SECOND space: bright + dense where reverb's hall is long +
      dark. Snare/clap shine 3-5, vocal-style sheen on a lead 4-6. Using
      reverb on the bed and plate on the hook puts them in different
      rooms — instant separation)
    echo (tempo-synced dotted-8th delay: 2 subtle depth, 6 dubby)
    tape (analog tape character: gentle rounding, low warmth, soft top,
      a hint of wobble. A production option for clean digital
      sources — 3-4 on the whole musical body, 6-8 for lofi/vintage)
    punch (transient shaper — more attack on every note front, no
      threshold to think about: 4-6 makes drums/plucks/keys hit harder,
      8+ aggressive. The opposite of smooth)
    smooth (slow musical leveler: evens a performance out without eating
      note fronts — bass 3-5, keys/leads 4-6. Often preferable to squash when
      melodic phrasing and note attacks should survive.)
    squash (fast aggressive smasher: drums 4-6 = dense and in-your-face,
      8+ with wet 3-4 = the parallel-crush trick. Too much on melody
      flattens it — that is what smooth is for)
    vinyl (record-player lofi: bandwidth narrows, slow pitch wobble,
      seeded crackle. 3-4 dusty warmth, 7+ old-record haze. Pairs with
      crush for full lofi-hiphop texture)
    pump (source-onset ducking — the house/trance "breathe"; put 5-8 on
      pads/washes/sub_drone and always declare the exact PumpSource[] in
      pumpFrom; sections without source notes do not duck)
    wet (wet/dry mix for ALL the effects above at once: 10/omit = fully
      processed as usual, 5 = half processed half clean in parallel, 0 =
      bypass. Parallel processing: heavy drive 8-9 with wet 3-4 =
      thick grit UNDER a still-clean signal ("New York" style) — where
      drive 4 alone just sounds mildly dirty. Also crush 8 wet 3 for lofi
      texture without destroying the part.
      IMPORTANT — "wet" DOES NOT COVER EVERYTHING: lowpass, highpass and
      pump are excluded from the blend and always act at full strength. So
      "wet":2 does not soften a filter or a sidechain, only the colour
      effects (recorded-source drive/crush/chorus/echo/tremolo/...). Shared
      reverb/plate sends, depth/tone placement and synth voice drive are also
      outside the blend. A track at lowpass 8 wet 2 is still fully filtered;
      a synth at drive 8 wet 2 is still fully driven.)
  Recipes: rock rhythm = clean_electric_guitar drive 5 · surf = tremolo 7 reverb 4 ·
  lofi beat = crush 4 on the drums track + vinyl_crackle layer · dub =
  echo 7 on offbeat chords · dream pop = chorus 6 reverb 6 on clean_electric_guitar ·
  funk = wah 6 drive 3 on clav_keys 16ths · psych-rock = flanger 6 on the
  whole drums track for one section (a classic tape-flange drum break) ·
  REAL-BAND funk/soul = bass_finger line + bass_ghost thumps (p0.6, between
  the real notes) + funk_guitar_stac "chicka" 16ths + bass_mute for motown ·
  jazz/rockabilly = upright_pizz walking quarters · dark cinema =
  upright_arco low sustains + twang_guitar melody.

### G.2 MIX & STEREO — COMPOSE THE STAGE IN THE FIRST DRAFT

  A score contains its production decisions. Assign low-frequency ownership,
  spectral space, depth, and width while writing rather than after overcrowding
  the arrangement.
  - Masking: first decide which parts own the low end. In a bass-led mix, the
    kick/bass system usually owns the region below ~180Hz; carve competing
    chords, pads, or leads with eqLow -6..-9 before merely turning them down.
    IF YOU CARVE eqLow, VOICE THE CHORD
    ROOT ABOVE ~C3 (131Hz) — the shelf sits at 200Hz, so a chord rooted at
    Bb2 loses the very note that names it and the ear re-reads the chord as
    its own upper structure (a Bbmaj7 voiced low reads as Dm7). Carving the
    low end and "keep the root and 3rd present" cannot both be satisfied down
    there; move the voicing up, or leave eqLow alone on that part. If a full section is mostly low-end
    rumble, the sub/bass are too loud (sub layers ~0.3 vol) — not the
    chords too quiet.
  - Width: in most bass-led mixes, anchor kick, sub, bass and snare/clap near
    the CENTER. Distribute supporting material around them: spread chord voices
    per note (pan -0.3/-0.1/+0.1/+0.3
    across the voicing), alternate lead phrases between sides (track pan
    0.2 vs -0.2), place paired percussion opposite (shaker 0.55, congas
    -0.55). chorus 5-6 / detune 6 on pads adds width on top.
  - When width supports the concept, use an intentionally wide harmonic layer
    (panned chord voices or a detuned pad) and contrast it with centred anchors.
    A narrower breakdown followed by restored width is one way to enlarge a
    drop; width is a form decision, not a mandatory layer in every section.

### G.3 ROUTING — CONNECT MUSICAL TRACKS TO MIX ROLES

  Every track/pattern may explicitly choose any built-in bus: "kit", "perc",
  "bass", "bed", "lead", or "fx". An explicit bus ALWAYS wins over the
  instrument's automatic role. Omit bus for the sensible default: kit drums go
  to kit, hand percussion to perc, recognized basses to bass, ordinary musical
  layers to bed, and recognized transitions to fx.
  Cross-routing is open by design. A synth through kit can gain drum-like punch;
  a drum through bed can become softer harmonic texture. Make that choice for
  an audible reason: kit has punchy drum glue, bed has supporting melodic
  levelling, and lead preserves foreground presence. A bus changes processing,
  not what notes the instrument is allowed to play. Unknown names still fail.
  "bus":"kit" — main drum-role processing: punch, glue and low-mid cleanup.
  "bus":"bed" — supporting melodic processing for chords, pads and textures.
  "bus":"bass" — dedicated low-end levelling, minimal room send, included in
    top-level glue with drums+percussion. Factory bass synths (acid_bass,
    moog_bass, knock_bass, reese_bass, sub_808/sub_pure/sub_drone, etc.) route
    here automatically. Transition-only sub_drop routes to the FX bus instead.
    A custom ex_ bass MUST declare it because the engine cannot infer musical
    role from arbitrary patch names. Without it, the patch is treated as a
    melodic bed: wrong EQ/compression, too much room and absent from bass glue.
  "bus":"lead" — the designated foreground identity; see FOREGROUND IDENTITY
    below. Stronger than a label: it changes tone/dynamics and makes the bed
    yield while that part speaks.
  "bus":"fx" — transition material. Factory noise_riser/noise_fall,
    pitch_riser and sub_drop route here automatically; custom sweeps need it.
  "bus":"perc" — hand percussion (normally automatic from drum names).

### G.4 NAMED BUSES & PARALLEL ROUTING — BUILD A PURPOSEFUL SIGNAL FLOW

  Named buses are OPTIONAL. Use the built-in roles above for ordinary tracks;
  declare top-level "buses" only when the piece needs a shared authored rack,
  a parallel return, exact effect automation, or a named sidechain source.
  A track/pattern enters one by writing "bus":"music" (the declared name):
  "buses":{
    "music":{"role":"bed",
      "effects":[
        {"id":"carve","type":"eq","low":-5,"mid":-1,"high":2,"mix":1},
        {"id":"echo","type":"delay","timeBeats":0.5,"feedback":0.32,"mix":0.18}
      ],
      "sends":[{"id":"dirt_feed","to":"parallel_dirt","amount":0.25,"tap":"post"}],
      "sidechain":{"from":[{"track":"KICK"}],"amount":5,"attackMs":8,"releaseMs":240},
      "fader":1,"pan":0},
    "parallel_dirt":{"role":"bed",
      "effects":[{"id":"grit","type":"drive","amount":6,"mix":1}],
      "sends":[],"fader":0.45,"pan":0}
  }

#### BUS CONTRACT

  - Maximum 16 named buses; each name/id is lowercase [a-z][a-z0-9_], maximum
    32 characters. kit/perc/bass/bed/lead/fx/hall/plate/master are reserved.
  - "role" is "kit"|"perc"|"bass"|"bed"|"lead"|"fx". It says which
    existing mix role receives the completed bus. This preserves Beatlab's
    role-specific drum, bass, bed, lead, and transition processing.
  - "effects" is an ORDERED rack, maximum 16. The array order is audible:
    drive→filter is not filter→drive. Author the order deliberately. A
    multi-band EQ is just several bell/shelf entries in a row:
      "effects":[
        {"id":"sub","type":"shelf","mode":"low","freq":60,"gain":2.5},
        {"id":"mud","type":"bell","freq":320,"gain":-4,"q":1.4},
        {"id":"click","type":"bell","freq":4500,"gain":3,"q":1.2}
      ]
    Each band has its own id, so its freq and gain can be swept independently
    from top-level "automation". Bell bands also support q automation;
    shelf bands have no q parameter.
  - "sends" is maximum 8. A send to another named bus creates a parallel path:
    the source bus still continues to its role while a copy feeds the target.
    "tap":"pre" copies the bus input BEFORE its ordered rack and fader/pan;
    "tap":"post" copies the completed bus AFTER them. "to":"hall" or
    "plate" feeds Beatlab's existing shared space instead of a named bus.
  - "fader" 0..1 and "pan" -1..1 act after the rack and sidechain. Defaults
    are 1 and 0. effects/sends default to empty arrays.
  - "sidechain.from" is an array of 1-16 SidechainSource objects. Each object
    has exactly one of track, pattern, instrument, drumHit, trigger, or bus.
    track/pattern/instrument follow completed post-fader audio; bus follows one
    declared custom bus (not built-in kit/bed/etc.); drumHit and trigger create
    fixed control pulses at exact events. Several sources use the strongest
    detector level at each sample, so array order has no effect and audio
    sources cannot phase-cancel each other. amount 0..10; attackMs 1..200;
    releaseMs 10..2000.
  - Sends and bus-keyed sidechains must form a DAG. Feedback/circular routing
    is rejected as a routing cycle. Every target/source/id must already exist.

#### DUCKABLE EFFECT RETURN

  A custom bus is also the effect-return object. To duck only reverb or delay,
  send the dry bus to a dedicated return bus, put one wet-only effect there
  ("mix":1), and put sidechain on that return bus. The dry source stays
  untouched while the wet tail falls under the detector and rises in its gaps.
  Built-in hall/plate returns are intentionally simple and cannot be sidechain
  targets; use a named custom return whenever return ducking is required.

#### SAFE EFFECT TYPES AND NATIVE PARAMETER RANGES

    eq       low/mid/high -12..12 dB, mix 0..1
             Fixed 200 Hz / 4 kHz crossover. A broad tone control, NOT
             surgical: it cannot target a frequency. Use bell for that.
    bell     freq 20..18000 Hz, gain -24..24 dB, q 0.1..18, mix 0..1
             ONE parametric peaking band. This is how you cut a specific
             frequency: {"id":"mud","type":"bell","freq":320,"gain":-4,"q":1.4}.
             q ~0.7-1.5 is a wide musical curve; q 6+ is surgical.
             Chain several bells (each with its own id) to build a full EQ.
    shelf    mode "low"|"high", freq 20..18000 Hz, gain -24..24 dB, mix 0..1
             Everything below (low) or above (high) the corner moves together.
             Weight under a kick: {"id":"wt","type":"shelf","mode":"low",
             "freq":60,"gain":2.5}.
    drive    amount 0..10, mix 0..1
    crush    amount 0..10, mix 0..1
    tape     amount 0..10, mix 0..1
    chorus   rateHz 0.01..10, depth 0..1, feedback -0.9..0.9, mix 0..1
    phaser   rateHz 0.01..10, depth 0..1, feedback -0.9..0.9, mix 0..1
    delay    timeBeats 0.0625..4, feedback 0..0.92, mix 0..1
    reverb   size 0..1, damping 0..1, tone -1..1, mix 0..1
    filter   mode "lowpass"|"highpass", cutoff 30..16000 Hz,
             resonance 0..0.9, mix 0..1
    width    amount 0..2 (0=mono, 1=unchanged, 2=double side; no mix field)
    tremolo  rateHz 0.01..20, depth 0..1, mix 0..1
  Unknown effect fields are errors. Use modest wet levels on a serial music
  bus; use a send plus a quieter parallel bus when the dry identity must remain.

### G.5 CONTINUOUS LAYERS & TEXTURES — MOTION, AIR, AND ENVIRONMENT

  Each bed is usually one long note spanning bars. These layers can make a
  sparse score feel inhabited without adding another foreground melody.
  white_noise / pink_wash — noise beds; add
    "controls":{"pump":6,"pumpFrom":[{"drumHit":"e_kick"}]} so they
    breathe with that exact kick, "sweep":5 to slowly open.
  noise_riser — the uplifter into a drop: one note whose dur IS the rise
    (e.g. 8 beats ending exactly at the drop). noise_fall = the exhale after.
  vinyl_crackle — lofi texture bed. sub_drone — deep root-note foundation.
  Texture recipes (quiet, wide, deliberately boring — they carry the FEEL):
    air pad — a long soft chord (analog_pad/glass_pad) on its own track with
      "wet":10,"reverb":8,"eqLow":-8 at vol ~0.15: pure atmosphere, the
      chord is felt, not heard.
    ghost echo — duplicate a lead PHRASE on its own track with "wet":10,
      "echo":8, vol ~0.2 (optionally panned opposite the lead): the melody
      answers itself from another room.
    ear candy — tiny high blips/FM ticks (or an ex_ patch) with p0.25 +
      "echo":5, panned wide: sparse one-shot sparkle that keeps long loops
      alive without adding a melody.
    burble — an ex_ sustained patch with lfoShape:"sh" + lfoCutoff 800-2000:
      the filter STEPS randomly like a modular sample-and-hold, motion
      without rhythm.
  Starting practice: supporting textures often sit at vol 0.1-0.25 with eqLow
  carved out of a bass-led mix; give beds pump plus an exact pumpFrom when
  source-triggered breathing belongs to the groove. Give a texture a purposeful lifecycle rather than
  adding it automatically. Duck, expose, transform, remove, or fade it as the
  form requires; "fader" automation can take it to 0 over the final 4-6 beats.

### G.6 RHYTHM GLUE

RHYTHM GLUE (top-level "glue":0-10): a mix-bus compressor over drums+percussion+
  bass TOGETHER — one gain curve on all three, so the rhythm section moves
  as one object. 3-5 is a useful starting range for a tight, produced low end;
  0/absent is off. Its audible purpose is cohesion, not automatic quality.

MASTER CEILING (top-level "ceilingDbtp":-9..0): targets the estimated TRUE
  PEAK of the finished master, in dBTP. Omit it and the master keeps its
  default soft-clipped landing (near -3 dBFS). The renderer can raise or
  lower the finished level to reach this target; it does not target LUFS or
  report measured loudness. Use a finite JSON number from -9 through 0;
  malformed or out-of-range values are errors, never clamped or ignored.
  -1 is a common streaming target. This is a reconstruction estimate, not a
  guarantee of an exact continuous-time peak or compliance with an external
  delivery specification. For such a specification, verify the exported WAV
  with the required meter. Sample peak alone can miss inter-sample overshoots.

### G.7 TRACK-PUMP SIDECHAIN

TRACK-PUMP SIDECHAIN: "pump" 0-10 is the duck depth. Every static or automated
  pump requires "pumpFrom", an array of 1-16 exact public source selectors;
  there is no hidden kick or internal-voice fallback:
    {"pump":8,"pumpFrom":[{"drumHit":"e_kick"}]}
  Each selector object has EXACTLY ONE property:
    {"track":"KICK_TRACK"} — one top-level Track by its id.
    {"pattern":"KIT"} — every arranged placement of that patterns key.
    {"instrument":"glass_lead"} — every Track/Pattern globally using that
      exact InstrumentName, including a declared ex_/exd_/rs_ key.
    {"drumHit":"conga"} — every occurrence of that exact DrumHitName inside
      drums lanes or single-drum lanes, including a declared exd_ key.
    {"trigger":"four_floor"} — every event in that exact top-level silent
      Trigger, with no instrument or audible output.
  Several selectors combine their onsets; array order has no effect. For
  example [{"drumHit":"e_kick"},{"drumHit":"conga"}] ducks on both.
  Names resolve from the generated instrument/drum catalogs and declarations,
  never from the renderer's internal kick/snare/tick voice groups.

#### SILENT TRIGGERS

  Top-level "triggers" is Dictionary<string, Trigger>. A Trigger is a compact
  control-only repeating pattern; it never renders sound:
    "triggers":{"four_floor":{"lenBeats":4,"hits":[0,1,2,3],
      "placements":[{"atBeat":0,"repeat":8},{"atBeat":48,"repeat":8}]}}
  lenBeats is the cycle length. hits are unique local beat positions from 0
  inclusive to lenBeats exclusive. placements put the cycle on the global beat
  timeline; repeat defaults to 1. The example triggers for 32 beats, leaves a
  16-beat breakdown gap, then resumes at beat 48. Reference it with
  {"trigger":"four_floor"} in pumpFrom or a custom Bus sidechain.from.

#### PUMP SHAPE

  PUMP SHAPE (controls next to pump, all 0-10): "pumpRelease" = how long the
  duck takes to recover (0≈0.15 beats tight, 10=1.5 beats long exhale;
  absent = 0.6 — the classic house breath), "pumpHold" = ms held FULLY
  ducked before recovering (6-10 = the EDM "gap" where the mix vanishes on
  each kick), "pumpShape" = recovery curve (low = even ramp, high = stays
  ducked then snaps back late). Big-room pump: "pump":8,
  "pumpFrom":[{"drumHit":"e_kick"}],"pumpHold":7,"pumpRelease":8.
  Subtle disco glue: "pump":4,"pumpFrom":[{"pattern":"KIT"}],
  "pumpRelease":3.

### G.8 FOREGROUND IDENTITY

FOREGROUND IDENTITY ("bus":"lead" on the track — an authoring decision the
engine cannot infer): the renderer sees instruments and notes, not musical
importance. Put "bus":"lead" on the track carrying the designated foreground:
a melody, riff, rhythmic signature, featured performance, or other recurring
identity. The bus compresses it less, centres it, lifts its presence and ducks
ONLY the melodic bed by up to 3dB while it speaks. That is audible behavior,
not metadata. Do not also make it excessively loud, mark several parts as lead,
or add depth:"front" automatically; stacking all three is how a keyboard-like
line takes over the record. Choosing compelling material matters more than
routing it, and routing cannot rescue a part that was never going to carry:
  * Match the source envelope to the phrase. A held line needs a sustaining
    source; a small "b" (vibraphone is 0.08s) cannot hold it against a dense
    break. But a rhythmic hook may deliberately be a short blip/stab. Do not
    turn every hook into a sustained keyboard line merely to keep it audible.
  * If the foreground and harmony mask each other in the same register, bus
    assignment alone will not fix it. Separate them by register, rhythm,
    envelope, pan, or tone; an octave of pitch separation is one option.
  * Give it enough recurrence to establish identity, or make deliberate rarity
    part of the form. A phrase heard once is normally an event, not a hook.
  - Start with one lead-bus track. Use more only when the foreground is truly
    an ensemble or has a second voice; marking everything erases the hierarchy.
  - Leave supporting parts unmarked. A chord, pad, string, or guitar may use
    the lead bus when it genuinely is the featured identity rather than a bed.
  - "bus":"fx" is the same idea for transition material (sweeps, noise, hits):
    no glue, allowed to swamp the mix for a second. "riser" and "impact"
    instruments go there on their own — you only need this for, say, a synth
    track that is really a whoosh.

### G.9 DEPTH & TONE — OPTIONAL SPATIAL AND SPECTRAL PLACEMENT

DEPTH & TONE — OPTIONAL SPATIAL AND SPECTRAL PLACEMENT (the engine maps these
words to tuned values, so use the documented words rather than inventing
numbers):
  "depth":"front"|"back" — front-to-back placement. "front" = closer (a touch
    louder, presence lift): the hook, a solo. "back" = further away (quieter,
    darker, more room): pads, textures, echoes of the theme. Absent = mid.
    Depth contrast can clarify a crowded scene. Use "front" only when extra
    proximity is needed; do not automatically combine it with bus:"lead".
    Push selected atmosphere back and leave neutral parts at mid depth.
  "tone":"dark"|"warm"|"bright" — spectral character. "dark" rolls the top
    off (moody, distant), "warm" adds body and softens the top (soul, lofi),
    "bright" opens the top (modern pop sheen). Absent = neutral. Contrast is
    the tool: a bright hook over a warm bed separates them for free.

### G.10 MIX BALANCE — MAKE THE INTENDED HIERARCHY AUDIBLE

- Everything you write is heard THROUGH everything else. A short part at vol
  0.3 under a dense kick at 0.9 may be inaudible rather than subtle. Treat
  these ballparks as initial calibration, then judge envelope and context:
    kick/snare 0.8-0.95 · bass 0.7-0.85 · bus:lead hook 0.5-0.7
    chords/pads 0.45-0.6 · percussion (bongo/conga/tambourine/shaker) 0.6-0.8
    hats 0.35-0.55 · fx/risers/noise 0.3-0.5 · sub layers (sub_pure/
    sub_drone under a real bass) 0.25-0.35 — sub energy adds up FAST
- Percussion is not automatically background. If bongos carry the groove,
  they may need 0.6+.
  And do NOT then scale them down again with arrangement "vol" — those
  multiply (0.55 note x 0.6 arrangement = 0.33 = gone). Pick one place to
  set the level.
- DECIDE THE ROLE, then pick from the right row — the two rows above conflict
  for anything that is percussive AND quiet by design, and splitting the
  difference is how a layer ends up 30dB under the mix, audible only in the
  intro where nothing else plays:
  * RHYTHMIC — the listener should be able to follow this part (glitch
    percussion, a click layer, a shaker groove): 0.6+, same as any percussion.
    It is a rhythm part that happens to be small, not a texture.
  * TEXTURE — should colour the mix without being individually audible (noise
    beds, room tone, pads under everything): 0.1-0.25.
  Decide which role applies before setting level; ambiguity here usually means
  the arrangement has not assigned the part a clear purpose yet.
- IN A DENSE, BASS-LED MIX, chords and stabs usually need spectral separation:
  cutoff 6-8 is a useful starting range. Below ~5, some repeating chord stacks
  accumulate low-mid energy and mask percussion or foreground parts. A dark
  repeating chord is still valid—voice it away from the bass, carve eqLow, or
  thin the surrounding arrangement so the darkness remains intentional.
- Leave holes. If every bar has drums + bass + chords + clav + keys + shaker
  + tambourine playing, nothing is audible and nothing feels like it arrives.
  Mute a layer for 8 bars; bring it back and it reads as an event.

## H. COMPOSING — MATERIAL, TIME, FORM AND MOTION

### H.1 MOTIF & HARMONY COMPILER — DEVELOP RELATIONSHIPS, NOT COPIED NOTE LISTS

  This optional layer gives the score musical memory. You still compose the
  motif, harmony, register, transformations and placements; the compiler only
  expands those decisions into ordinary notes. Literal "Bb3" pitches remain
  valid everywhere and require no harmony block, so chromatic, atonal and
  sound-design writing is unchanged.

  1. DECLARE TONALITY, CHORDS, AND REUSABLE VOICINGS at top level:
    "harmony":{
      "tonic":"F","scale":"dorian","octave":4,
      "voicings":{"wide":[-1,0,0,1],"lifted":[0,0,1,1]},
      "chords":{
        "i7":{"tones":["^1","^3","^5","^7"],"voicing":"wide",
               "range":["F2","F5"]},
        "IV7":{"tones":["^4","^6","^1","^3"]}
      }
    }
    - tonic is a pitch CLASS such as "F", "Bb", or "C#" (default C). octave
      is the default register for a degree without its own @octave (default 4).
    - scale defaults to major and is exactly one of:
      major, ionian, minor, natural_minor, aeolian, harmonic_minor,
      melodic_minor, dorian, phrygian, lydian, mixolydian, locrian,
      pentatonic_major, pentatonic_minor, blues, chromatic.
      For another tuning vocabulary, replace scale with "pitchSet": an
      ascending list of 1-12 unique semitone offsets beginning at 0, e.g.
    [0,1,4,6,7,10]. It is octave-repeating; this is a pitch-set language,
      not microtonal tuning.
    - A scale degree is "^" + optional b, bb, #, or ## + an integer from 1
      through 13. "^1", "^3", "^b7", "^#4", "^9" are valid. Append @octave
      from -1 through 8 when the register must be explicit: in F, "^1@4" = F4
      and "^9@3" = G4.
      Degree tokens work in pitched compact strings and note objects.
    - A chord is an EXPLICIT authored tone list; Beatlab does not guess chord
      quality from a name. Tones may be degrees or absolute notes. The public
      name ("i7", "sunset", "A_alt") is only an ID you reuse.
    - A voicing is one integer OCTAVE offset per chord tone, each -4..4. A
      named voicing may be reused by many chords; a chord may instead write
      the array directly. Its length must equal the number of tones.
    - Optional chord range is an ascending absolute [low,high]. maxLeap 0..48
      limits each connected voice when a later chord event uses voiceLead.

  2. WRITE ONE MOTIF, THEN PLACE ITS ID IN PITCHED PATTERNS:
    "motifs":{
      "hook":{"lenBeats":4,"notes":[
        "0 ^1@4 0.4 0.80","0.5 ^2@4 0.4 0.72",
        "1 ^3@4 0.4 0.76","1.5 ^5@4 0.8 0.82"]},
      "answer":{"extends":"hook","transform":{"retrograde":true,
                                                   "diatonic":-1}}
    },
    "patterns":{
      "HOOK":{"instrument":"synth_pluck","motif":"hook","lenBeats":4,
              "controls":{"cutoff":5},"bus":"lead"},
      "ANSWER":{"instrument":"synth_pluck","motif":"answer"}
    }
    Motif notes use BEATS and the pitched compact-note grammar. A motif may
    extend another: it inherits the parent notes, APPENDS any child notes, then
    applies its transform to the merged phrase. Circular extends is an error.
    A pattern may add ordinary notes beside "motif"; motifTransform applies to
    the combined pitched material. Motifs never belong on a drum pattern.

  3. TRANSFORM EACH PLACEMENT WITHOUT REWRITING THE PHRASE:
    "arrangement":[
      {"pattern":"HOOK","atBeat":0},
      {"pattern":"HOOK","atBeat":4,
       "motifTransform":{"diatonic":2}},
      {"pattern":"HOOK","atBeat":8,
       "motifTransform":{"invert":true,"octave":1,"rhythm":0.5,
                         "range":["Bb4","F5"],"maxLeap":7}},
      {"pattern":"HOOK","atBeat":12,
       "motifTransform":{"chord":"IV7","voiceLead":true,
                         "range":["F4","F5"],"maxLeap":7}}
    ]
    The same motifTransform object is accepted on a motif definition, a pitched
    pattern, or one arrangement placement:
      diatonic  integer -64..64 scale steps (+1 moves ^1 to ^2)
      chromatic integer -96..96 semitones
      invert    true mirrors the scale-degree contour around the FIRST note
      retrograde true mirrors note positions inside lenBeats
      octave    integer -8..8, applied after other pitch movement
      rhythm    0.0625..16 multiplier for local positions AND durations
      register  integer -1..8, default octave for unresolved degree tokens
      chord     one defined chord name; harmonic context for voiceLead
      voiceLead true snaps each melodic pitch to a nearby tone of chord
      range     ascending absolute [low,high], satisfied by octave movement
      maxLeap   0..48 semitones between successive melodic notes. This is a
                HARD CEILING, not a requested jump: maxLeap:15 still chooses
                the closest allowed note and merely permits a move up to 15.
                For connected chord voices, 5-7 is tight/smooth, 8-12 is a
                normal wider allowance, and 13-24 is deliberately dramatic.
                Values above 24 belong to explicit register displacement or
                sound-design gestures, not routine voice leading. Use the
                smallest value you KNOW is feasible inside range; if the exact
                voicing has not been checked, omit maxLeap instead of guessing.
    A transform is deterministic and inspectable. The exact compiler order is:
      resolve degrees/chords → retrograde → rhythm → inversion → diatonic move
      → chromatic move → octave → chord-tone voice leading → range/maxLeap.
    The older arrangement "transpose" is a final chromatic shift after this
    layer. On an arrangement placement, rhythm changes the played phrase but
    NOT the pattern's repeat interval; repeat remains lenBeats apart.

  4. PLAY A NAMED CHORD AS A STRUM OR ARPEGGIO with note-object form:
    {"b":0,"chord":"i7","octave":3,"durB":1.5,"vol":0.55,
     "voicing":"wide","strumMs":20}
    {"b":2,"chord":"IV7","octave":3,"durB":1.5,"vol":0.50,
     "arp":{"order":"up","stepBeats":0.25,"octaves":0,"gate":0.8}}
    - chord and note are mutually exclusive. octave/voicing may override the
      chord defaults. strumMs is -500..500; positive rolls written order,
      negative rolls the opposite direction while keeping the event start.
    - arp order is up|down|upDown|asWritten|random; stepBeats is 1/128..16,
      octaves is 0..3 ADDITIONAL copies, gate is 0.05..1 of each step. random
      order is repeatable from top-level seed; it never uses unseeded randomness.
    - "voiceLead":true on a chord event moves each written chord voice by
      OCTAVES toward the same-index voice of the preceding chord event,
      respecting the event's or chord's range/maxLeap. On the first chord it
      only applies range. Before setting maxLeap, compare those paired voices
      after their allowed octave moves. Example: D3→Bb3 needs 8 semitones, so a
      ceiling of 7 is impossible even though both notes are inside the range.
    - These chord objects also work in direct tracks. b/durB are still beats
      in patterns; t/dur are seconds in tracks, while arp.stepBeats always
      remains musical beats and strumMs always remains milliseconds.

  USE THIS LANGUAGE WHEN RELATIONSHIPS MATTER. It is especially valuable for
  a hook that returns changed, a progression with controlled voicings, an
  answer phrase, reharmonization, or scale-aware register changes. It is not
  a requirement to force every absolute bass note, drum hit, drone, chromatic
  approach note, or one-off effect through theory syntax. Unresolved degrees,
  missing chords/motifs, wrong voicing lengths, impossible ranges/maxLeap, and
  circular motif definitions are compiler errors, not silent fallbacks.

### H.2 REAL GROOVE MAPS & TEMPO — DESIGN AN INTERLOCKING POCKET

  swing is one shuffle control and humanize is seeded variation. A groove map
  is different: it is an authored repeating relationship of timing and force.
  One map can make a kick lean lightly, percussion speak fully and bass sit
  between them while all three agree about the cycle. The compiler applies
  the map; it never invents a genre groove for you.

  1. DEFINE A NAMED CYCLE at top level. This is a four-beat, 16-step example:
    "grooves":{"pocket16":{
      "meter":[4,4],"stepsPerBeat":4,"phaseBeat":0,
      "timingMs":[0,12,-7,20, -4,16,-10,24, 2,11,-6,19, -3,15,-9,28],
      "velocity":[1.08,.82,.96,1.12, 1,.78,.94,1.15,
                  1.06,.8,.98,1.1, .96,.76,.92,1.18],
      "accent":[.2,-.1,0,.15, .1,-.15,0,.2, .1,-.1,0,.15, .05,-.2,0,.25]
    }},
    "groove":"pocket16"
    - meter is [numerator,denominator]. stepsPerBeat counts grid steps per
      QUARTER-NOTE beat: 4=sixteenths, 2=eighths, 3=triplet eighths. The cycle
      has numerator * 4 / denominator * stepsPerBeat values. Therefore 4/4 at
      4 has 16 values; 6/8 at 4 has 12. Every supplied array must have EXACTLY
      that count. At least one of timingMs, velocity or accent is required;
      omitted arrays mean all 0 timing, all 1 velocity or all 0 accent.
    - timingMs is one signed -250..250 millisecond displacement per step.
      velocity is a direct 0..2 multiplier. accent is -1..1 additional force;
      its factor is 1 + accent*0.5. The full target on one step is therefore
      velocity[step] * (1 + accent[step]*0.5).
    - phaseBeat is the ABSOLUTE score beat where step 0 begins (default 0), not
      a delay. Repeats and lanes keep reading that same phase. To deliberately
      restart a new meter at beat 64, use phaseBeat:64 on every lane that must
      lock to it.
    - Limits: at most 64 maps; names are 1-64 letters/numbers/_/-; numerator
      1..32; denominator 1|2|4|8|16; stepsPerBeat 1..16; maximum 256 steps.
      Unknown fields in a groove definition, use object or tempo point are
      errors, so a misspelled timing instruction cannot disappear silently.

  2. APPLY ONE MAP AT DIFFERENT LANE STRENGTHS:
    "patterns":{
      "KICK":{"instrument":"drums","lenBeats":4,
              "groove":{"map":"pocket16","amount":.25,
                         "timing":1,"velocity":.7},"notes":[...]},
      "SHAKER":{"instrument":"drums","lenBeats":4,
                "groove":{"map":"pocket16","amount":1},"notes":[...]},
      "BASS":{"instrument":"bass_finger","lenBeats":4,
              "groove":{"map":"pocket16","amount":.55},"notes":[...]}
    }
    A groove binding is either the map name, true (inherit, same as leaving it out), false (opt out), or an object containing:
      map       named map; may be omitted when a parent/default already chose it
      amount    0..1 master blend for BOTH timing and velocity (default 1)
      timing    0..1 extra timing-only blend (default 1)
      velocity  0..1 extra velocity/accent-only blend (default 1)
      phaseBeat optional phase override for this use
    amount blends timing from 0ms toward timingMs and force from x1 toward the
    target multiplier; timing/velocity then trim their respective halves.
    This preserves one authored identity without forcing every lane equally.

  3. OVERRIDE BY SECTION WITHOUT DUPLICATING NOTES:
    "arrangement":[
      {"pattern":"KICK","atBeat":0,"repeat":8},
      {"pattern":"KICK","atBeat":32,"repeat":8,
       "groove":{"amount":.65}},
      {"pattern":"SHAKER","atBeat":0,"repeat":16},
      {"pattern":"BASS","atBeat":0,"repeat":16}
    ]
    Resolution is top-level groove → pattern/track groove → arrangement-entry
    groove. A later object inherits the selected map and overrides only named
    fields. Write false to opt a track/pattern/placement out; after false, a
    later object must name map again before it can set amounts. Select another
    map to change pocket by section. Pattern inheritance also inherits groove
    unless the child overrides it.

  4. OPTIONAL TEMPO MAP — BEAT ADDRESSES REMAIN MUSICAL:
    "bpm":120,
    "tempoMap":[
      {"atBeat":0,"bpm":120,"curve":"linear"},
      {"atBeat":32,"bpm":124,"curve":"step"},
      {"atBeat":64,"bpm":122}
    ]
    - 1..128 points, strictly increasing; the first atBeat MUST be 0. BPM is
      30..300. If top-level bpm is present, it must equal tempoMap[0].bpm.
    - curve belongs to the point and describes movement FROM it to the next:
      step holds its BPM; linear changes BPM continuously across musical beats.
      The compiler integrates that ramp exactly instead of approximating every
      beat with the starting tempo.
    - Pattern starts/durations, beat-addressed automation and master moves all
      convert through this map. Direct-track t/dur remain authored SECONDS;
      if a groove affects a direct track, its beat phase is inferred through
      the inverse tempo map.
    - The normalized renderer still has one initial BPM clock. Renderer effects
      whose own rate/delay is specified in beats use the initial/top-level BPM;
      tempoMap moves events and automation, but does not continuously retime an
      echo or other beat-clocked effect. Avoid a tempo ramp when exact changing
      delay-grid tracking is the central musical requirement.

  5. TIMING ORDER, SAFETY, AND DIAGNOSTICS:
    tempo grid → reusable groove → authored note off + lane lateMs and ornaments
    → swing → seeded humanize. Swing and every groove lane read the original
    authored beat, so an early shaker does not accidentally change cycle step.
    Notes between defined grid steps use the nearest groove step; for exact
    interlocking results, author rhythmic events on the declared subdivision.
    Groove timing is clamped to 45% of the local subdivision, which prevents
    adjacent grid events from crossing even under a tempo ramp. Events moved
    before score start clamp to t=0. These recoveries appear in top-level
    _warnings on the expanded score; do not design by relying on a clamp.

  Compose the map for the requested music after research. Do not paste the
  example as a universal Afro/Latin/funk preset: the numbers ARE the pocket.
  Good maps can leave anchors nearly straight while giving subdivisions a
  deliberate push/pull and strength contour. Audition the relationship among
  lanes, not each lane in isolation, and keep authored @ms/off for meaningful
  exceptions rather than correcting a poorly designed map note by note.

### H.3 PATTERNS & ARRANGEMENT — WRITE MUSICAL IDEAS ONCE, THEN DIRECT THEIR FORM

  Instead of only "tracks", you may add:
  "patterns": {"<ID>": {"instrument":"<name>", "lenBeats":<n>, "controls":{...},
               "notes":[ ... times/durs in BEATS ... ]}, ...}
  "arrangement": [{"pattern":"<ID>","atBeat":<n>,"repeat":<n>,
                   "vol":<mul, optional>,"transpose":<semitones, optional>}, ...]
  - repeat plays the pattern back-to-back (lenBeats apart); vol scales the
    whole instance (quiet intro = same pattern, vol 0.6); transpose shifts
    pitched notes (lift the chorus +5).

#### WHERE EVERY KEY IS ACCEPTED

  WHERE EVERY KEY IS ACCEPTED (a pattern accepts nearly everything a track does —
  don't hoist a knob up to a plain track just because you weren't sure):
    on a PATTERN or a TRACK (identical meaning on both):
      instrument · controls · swing · humanize · groove · bus · depth · tone · pan
      lateMs · flamMs · choke · granular · notes
    on a TRACK only:
      id
    on a PATTERN only:
      lenBeats · extends · omit · only · motif · motifTransform
    on an ARRANGEMENT entry:
      pattern · atBeat · repeat · vol · volFrom · volTo · transpose · motifTransform · groove
      transform · condition · variations
    on an AUTOMATION entry:
      track OR bus · knob OR param · optional effect/send · points OR lfo · res
    on a NOTE (object form):
      t/b · note · dur/durB · vol · volTo · pan · p · c · slide · flam
      roll · off · art · expr · sampleStart · reverse · damp · stretch · bow · release ·
      region · granular · chord · octave · voicing · strumMs · arp · voiceLead · range · maxLeap
    at TOP LEVEL:
      bpm · tempoMap · seed · durationSec · swing · humanize · groove · grooves ·
      glue · synths · drumSynths · buses · resamples · harmony · motifs · patterns · arrangement ·
      automation · master · tracks
  Anything not on the pattern/track/note lists is IGNORED SILENTLY — it will not raise an error,
  so a misspelled key simply does nothing. Check spelling against this list.
  Exception: custom-definition fields obey their own contracts above. Compact synth
  definitions ignore unknown keys;
  dual-oscillator synth and custom-drum unknown/wrong-model fields are errors specifically
  to prevent inaudible sound-design instructions.
  - EVOLUTION with "extends": a pattern may inherit another and only ADD:
    "KIT2":{"extends":"KIT","notes":["0.25 e_hat_closed 0.35", ...]} is KIT
    plus extra hats. Chain them (KIT → KIT2 → KIT3) and arrange
    KIT ×8 → KIT2 ×8 → KIT3 ×16 — the track GROWS while you only write the
    additions. Combine with staggered track entries (bass enters at beat 32,
    pads at 64, lead at 96) — that entrance staircase IS the arrangement of
    real techno/house.
    THINNING with "omit" / "only" — the subtractive half. "extends" adds
    notes; these two take them away, BY BEAT, after the merge:
    "STAB":{"extends":"CHD","only":[0]}      = the chord, downbeat only
    "SPARSE":{"extends":"KIT","omit":[1,3]}  = the kit minus the backbeat
    So ONE progression covers both densities: write the busy version once,
    then "only" it down for the breakdown. Without this you write the same
    chords twice and burn hundreds of notes on duplication.
    They apply to the MERGED note list, so they compose down a chain, and
    they match a beat exactly (0.5 hits the note at 0.5, not the one at 0.75).
    A pattern with neither is additive exactly as before.
    Still true: an extending pattern with no "omit"/"only" can only ever be
    DENSER than its parent, so a track built purely by adding can never come
    down — which is how a piece ends up with no dynamics at all.
    An extending pattern may also override single knobs:
    "EP2":{"extends":"EP1","controls":{"cutoff":6}} = same notes, brighter
    (knobs MERGE — you only write the one that changed).
  - INSTANCE FADES: "volFrom":0.5,"volTo":1 on an arrangement entry ramps
    the volume across the whole instance (all its repeats) — the creeping
    8-bar build without writing the pattern twice.
  - COMPACT note strings (preferred inside patterns — saves space).
    THE WHOLE GRAMMAR, so you never have to guess an ordering:
      pitched:  "<beat> <note> <durBeats> <vol> [pan]"
      drums:    "<beat> <name> <vol> [pan]"
      tokens:   p<0-1> | flam | roll<N> | @<±ms>
    The optional trailing number IS per-note pan (-1..1). Named tokens may sit
    ANYWHERE after the first two fields — they are stripped before the
    positional numbers are read — so "0 C4 1 0.8 -0.5 p0.7" and
    "0 C4 1 0.8 p0.7 -0.5" are the same note. Examples:
      "0 A1 0.5 0.9"                pitched, centred
      "0 e_kick 0.9"                drum
      "2 shaker 0.4 0.6"            drum, panned right
      "3.5 snare 0.7 roll6 @12"     roll into beat 4, 12ms late
      "0 C4 1 0.8 -0.35 p0.6"       pitched, left, plays 60% of repeats
    Append "p0.7" to a note = 70% chance it plays, re-rolled on EVERY repeat
    of the pattern — ghost hats/percussion with p0.5-0.8 make a long loop
    breathe instead of cloning ("3.75 e_hat_closed 0.3 p0.6").
    More note tokens (drums): "flam" = grace hit just before the main one
    ("2 snare 0.8 flam"; "flamMs":10-40 on the pattern sets the spacing —
    tight 10 = one fat hit, wide 40 = an audible drag); "rollN" = N-hit buzz
    INTO the hit across a half beat ("3.5 snare 0.7 roll6" = snare roll into
    beat 4). "@ms" on ANY note nudges timing ("1 snare 0.8 @15" = 15ms
    late). Track-level pocket: "lateMs":12 on a pattern/track pushes ALL its
    notes late — laid-back snare/bass against a straight kick is the
    difference between a groove and a grid.

#### HI-HAT CHOKE

    HI-HAT CHOKE (automatic): a closed-hat hit CUTS a ringing open hat, like
    one physical hi-hat — so "e_hat_open on the offbeat, e_hat_closed on the
    beat" gives the classic house "tss-t" for free. Set "choke":false on the
    pattern/track only if you WANT open hats ringing through.
    Use object form {"t":...} when a note needs "slide", "c", "volTo", "art", "expr",
    "sampleStart", "reverse", "damp", "stretch", "bow", "release", "region", or "granular"
    (mid-note swell: gain ramps note.vol → volTo across the note's length —
    string/pad crescendos, fading a phrase; works on recorded instruments).
  - STEREO: "pan":-1..1 on any pattern/track places it in the stereo field
    (per-note pan = optional last number in the compact string). Bongos at
    -0.4, shaker at 0.4, hats slightly off-center — width contributes to
    separation and motion; bass-led club mixes usually keep kick and sub near
    center, while other styles may organize the field differently.

  - "tracks" (times in SECONDS) still works alongside, for one-off events:
    risers into drops, impacts, crashes, a special fill.
  Example:
    "patterns":{"KIT":{"instrument":"drums","lenBeats":4,
                  "notes":["0 e_kick 0.9","1 e_clap 0.7","2 e_kick 0.9","3 e_clap 0.7","0.5 e_hat_closed 0.4","1.5 e_hat_closed 0.5","2.5 e_hat_closed 0.4","3.5 e_hat_closed 0.5"]},
                "BASS":{"instrument":"acid_bass","lenBeats":8,"controls":{"cutoff":4,"resonance":8,"envMod":6},
                  "notes":["0 A1 0.5 0.9","1 A1 0.5 0.6","2 C2 0.5 0.8","3 A1 0.5 0.6","4 E2 0.5 0.9","5 D2 0.5 0.7","6 C2 0.5 0.8","7 G1 0.5 0.7"]}},
    "arrangement":[{"pattern":"KIT","atBeat":0,"repeat":32},
                   {"pattern":"BASS","atBeat":16,"repeat":10},
                   {"pattern":"BASS","atBeat":96,"repeat":4,"transpose":5}]

### H.4 PATTERN DEVELOPMENT — DIRECT REPETITION WITHOUT COPYING NOTES

  An arrangement entry can develop one source pattern differently on each
  repetition. These fields are compiler instructions: they disappear after
  expansion, leaving ordinary notes that every renderer, stem, piano roll and
  mix path already understands.

  "arrangement":[
    {"pattern":"PHRASE","atBeat":0,"repeat":8,
     "condition":{"alternate":"odd"}},
    {"pattern":"PHRASE","atBeat":0,"repeat":8,
     "condition":{"alternate":"even","last":false},
     "transform":{"reverse":true,"rotate":.5,"gate":.7,
                  "diatonic":1,"accent":[1.15,.85]}},
    {"pattern":"PHRASE","atBeat":0,"repeat":8,
     "condition":{"last":true},
     "transform":{"density":2,"accent":[1.2,.8]}}
  ]
  Those three placements are disjoint: the original phrase plays on odd
  passes, the directed answer plays on even non-final passes, and the same
  authored notes become a denser final fill on pass 8. No duplicate pattern
  or invented melody is hidden behind the syntax.

  TRANSFORM accepts ONLY these fields:
    reverse    boolean. Reverse onset groups across their EXISTING rhythmic
               positions; notes sharing an onset move together, so chords and
               layered hits do not break apart.
    rotate     signed beats. Circularly move starts inside lenBeats. A value of
               .5 moves the phrase by one eighth note without moving the next
               repeat's downbeat.
    stretch    1/16..16. Multiply local starts and explicit durations. It does
               NOT change lenBeats or repeat spacing; starts that reach the
               boundary are omitted, which can deliberately leave air.
    invert     boolean scale-aware contour inversion around the first pitch.
    diatonic   integer -64..64 scale steps. invert and diatonic require a
               top-level harmony context, even when source notes are absolute.
    chromatic  integer -96..96 semitones.
    octave     integer -8..8 octaves.
    density    0..4. Below 1, deterministically thin whole onset groups; above
               1, retrigger each group at even divisions before the next onset
               (or boundary). The pitch content is repeated, never invented.
    gate       .05..4 multiplier for EXPLICIT dur/durB after stretch/density;
               it cannot manufacture sustain for a note with no duration.
    accent     1..128 velocity multipliers, each 0..2, cycling over the final
               chronological onset groups. Groups remain internally balanced.

  The operation order is fixed and audible:
    reverse → rotate → stretch → pitch → density → gate → accent → bound
  Harmony/motif resolution happens before this sequence. Arrangement
  "transpose" is a final chromatic shift after it. Every transformed start is
  kept inside [0,lenBeats), and explicit duration is clipped at the boundary:
  transformed events never cross that repetition's lenBeats boundary. Pattern
  stretch therefore changes the phrase played, never the arrangement clock.

  CONDITION selects repetitions using one-based counting:
    first      true selects only pass 1; false excludes pass 1
    last       true selects only the final pass; false excludes it
    everyNth   integer 1..256 selects N, 2N, 3N...
    alternate  "odd" or "even"; pass 1 is odd
  Supplied condition fields combine with AND. A last-pass fill is simply
  "condition":{"last":true}. If several arrangement entries address the same
  beats and their conditions overlap, they ALL play; make selectors disjoint
  when alternatives rather than layers are intended.

  For seeded variation inside one placement:
    {"pattern":"PHRASE","atBeat":32,"repeat":8,
     "transform":{"gate":.8},
     "variations":[
       {"weight":3,"transform":{"rotate":0}},
       {"weight":1,"transform":{"rotate":.5,"octave":1}}
     ]}
  variations is one mutually-exclusive weighted group: exactly one authored
  transform is selected on each active repetition, and its fields override
  the base transform. It accepts 1..16 entries; weight defaults to 1 and must
  be positive. Selection and density thinning/expansion derive from:
    score seed + pattern + placement + repetition
  The same saved JSON always expands identically. Changing seed can change
  choices. A note's p probability is rolled afterward from that same stable
  identity, independently of the variation choice.

  Use transformations to make recurrence intentional: question/answer,
  register lift, shortened release, subtraction, controlled ratchets and a
  boundary fill. Weighted variation is colour, not form by itself; important
  arrivals should use explicit conditions so the musical decision is certain.
  Invalid ranges, unknown transform/condition/variation fields, pitch moves on
  drums, or scale-aware moves without harmony are compile errors rather than
  silent no-ops.

### H.5 AUTOMATION — TURN STATIC MATERIAL INTO A PERFORMANCE ACROSS TIME

  There are TWO forms. Use exact "param" automation for held-note synth motion,
  named-bus effects/sends, or native-unit fader/pan. Use the compact "knob"
  form for the simple 0..10 synth front panel, per-note volume, and the three
  continuous track processors lowpass/highpass/pump.

#### EXACT CONTINUOUS FORM

  EXACT CONTINUOUS FORM — one normalized path in native engine units:
    track parameter:
      {"pattern":"PAD","param":"synth.cutoff","points":[[16,350],[48,9000,"scurve"]]}
    bus effect parameter:
      {"bus":"music","effect":"echo","param":"feedback","points":[[32,0.18],[64,0.62]]}
    bus send amount:
      {"bus":"music","send":"dirt_feed","param":"amount","points":[[32,0.1],[64,0.45]]}
    bus fader/pan:
      {"bus":"parallel_dirt","param":"fader","points":[[48,0.15],[64,0.55,"exp"]]}

#### EXACT RULES

  - Supply exactly ONE of "track" or "bus". "effect"/"send" are bus-only
    selectors and are mutually exclusive. IDs must match declared objects.
  - Every point value uses the parameter's NATIVE range—never the compact
    knob form's 0..10 scale. The bus effect ranges are the table in NAMED BUSES.
    Values outside the selected parameter's range are errors; they are not
    silently clipped.
  - Exact track params:
      track.fader 0..1 · track.pan -1..1
      synth.cutoff 30..16000 Hz · synth.resonance 0..0.9 · synth.drive 1..8
      dual-oscillator only: synth.blend/sync/ring/shape 0..1,
                            synth.pitch1/synth.pitch2 -48..48 semitones
      FM operator only: synth.index 0..4 (1 = as written; multiplies every
                            route index)
    Dual-oscillator-only targets require every note on that target to use an ex_
    patch with osc1 and osc2; synth.index requires an ex_ patch with ops. They
    change oscillator topology continuously WHILE a note is held.
  - Exact bus params without an effect/send selector: fader 0..1, pan -1..1,
    sidechain.amount 0..10 (only when that bus declares a sidechain).
    With "send", the only param is amount 0..1. With "effect", use a parameter
    listed for that effect type (including mix where available).
  - A point's third element "linear"|"exp"|"log"|"scurve"|"step" shapes the
    segment INTO that point, on every exact target. Before a BusSweep's first
    point, the declared bus/effect/send value remains active. After the last
    point the value holds. Several entries on one target merge into one
    time-sorted envelope; to HOLD across a gap, start the later entry at the
    held value. Conflicting BusSweep points at one beat are errors, independent
    of automation array order.
  - An exact target may replace "points" with
    "lfo":{"atBeat":<start>,"beats":<length>,"period":<beats per cycle>,
    "depth":<full width>,"center":<native value>}.
    Center is REQUIRED because native ranges differ. The compiler bakes at
    most 64 points per target. Its full excursion must fit the target range,
    and it returns to center at its ending beat. Use an effect's own rateHz for
    long repetitive modulation and exact LFO for finite arrangement gestures.
  - RENDER RATE: effects run every audio sample. Exact envelope targets update
    every 64 samples (about 1.45ms at 44.1kHz) and glide with 8ms smoothing,
    including step moves, so held notes, delay time, filters, sends, faders,
    and sidechains move without zipper clicks. Browser, serial offline, and
    chunked offline rendering share this same evaluator.

#### KNOB AUTOMATION FORM

  KNOB AUTOMATION FORM — front-panel 0..10 moves and three continuous
  track processors:
  "automation":[{"pattern":"<top-level patterns key>","knob":"<name>",
                 "points":[[32,4],[64,8]]}, ...]
  Every Sweep has EXACTLY ONE target property:
  - "track":"<Track.id>" = one direct top-level Track only.
  - "pattern":"<top-level patterns key>" = every placement of that exact Pattern.
  - "instrument":"<instrument name>" = every direct Track and arranged
    Pattern using that instrument, regardless of bus.
  Never put two or three target properties on one Sweep.
  "points" = keyframes [beat, value, curve?] — at least 2, beats ascending;
  the value interpolates between them. ONE entry holds the whole move:
  [[0,2],[32,8],[64,8],[96,3]] = open over 8 bars, sit, then close.
  - Synth knobs (cutoff/resonance/detune/…): stamped per note at the note's
    beat, held after the last point. The 32-bar filter-open on a chord
    stab: {"pattern":"CHD","knob":"cutoff","points":[[0,2],[64,8]]}.

#### THE HOLD IS PERMANENT

    THE HOLD IS PERMANENT: after the last point the knob stays at that value
    for the rest of the piece on every track selected by that Sweep. End the
    keyframes where you want the knob to LIVE.
  - A SECOND entry on the same target merges by time. Start it at the value
    the knob already holds and the move joins seamlessly; start it anywhere
    else and you get exactly what you wrote: a JUMP at its first beat.
  - "lowpass"/"highpass" (0=open, 10=closed/thin): a SAMPLE-ACCURATE
    continuous sweep that works on EVERY instrument — recorded disco bass,
    guitar chops, whole drum tracks. This is the French-house filter move:
    open up over 16 bars = {"pattern":"BASSGTR","knob":"lowpass",
    "points":[[0,8],[64,0]]} (8→0 opens; 0→8 closes).
    These DJ-filter cutoffs are compact "knob" targets, not exact "param"
    targets. Add "res":0-10 to one lowpass/highpass entry and that FILTER's
    resonance changes at the entry's first point: res 5-7 is the classic
    dramatic sweep, 0 is the polite one. The value then holds for that exact
    track + filter until a later sweep supplies another "res"; omitting it
    retains the current value. Lowpass and highpass keep independent states,
    and every track starts independently. "res" on pump, a synth knob, or an
    exact param is an ERROR, never ignored. A static "controls.res" is the
    optional starting baseline for both filters; without it each starts at 0.
  - TARGET SCOPE IS EXPLICIT. {"track":"LEAD_TRACK",...} selects only the
    direct Track whose "id" is "LEAD_TRACK". {"pattern":"CHD",...} selects
    only the Pattern at patterns.CHD across all of its placements; Patterns
    extending CHD are separate targets. {"instrument":"glass_lead",...}
    selects every direct Track and arranged Pattern using glass_lead, even
    when they route to different buses.
  - "vol": multiplier ramp (0.5→1 = 16-bar crescendo), stamped per note.
  - "pump" is also SAMPLE-ACCURATE on every instrument: it rides duck depth
    over time, bringing the sidechain in toward the drop and out for the
    breakdown. The target lane must still declare pumpFrom in controls.
    Continuous fades and stereo moves use exact native-unit
    "track.fader" and "track.pan" above; "knob":"fader" and "knob":"pan"
    are not fields in this language.
  - A point's third element shapes the segment INTO it: "exp" (slow start,
    RACES at the end — useful for a sweep accelerating into a drop), "log"
    (fast start, eases in), "scurve" (smooth), "step" (hold, then jump at
    that beat). Default "linear". {"pattern":"BASS","knob":"lowpass",
    "points":[[48,8],[64,0,"exp"]],"res":6} = the French-house riser done
    right. Works on every knob; per-note synth knobs sample the shaped path
    at each note's onset, so use lowpass/highpass when continuous motion
    between notes matters.
  - KNOB LFO — a tempo-synced value oscillation, allowed ONLY on the three
    sample-accurate knobs above (lowpass / highpass / pump).
    NEVER on synth knobs — "wobble", cutoff, resonance etc. take a
    "points" instead (and "wobble" is itself an LFO already; ramp
    its depth, don't LFO it). Replace "points" with
    "lfo":{"atBeat":<start>,"beats":<length>,"period":<beats per cycle>,
    "depth":<width>,"center":<resting value>} — a sine wobble over the window.
    {"pattern":"BASS","knob":"lowpass","lfo":{"atBeat":32,"beats":16,
    "period":0.5,"depth":6,"center":5}} = half-beat wobble for 4 bars.

#### UNITS

    UNITS: lowpass/highpass/pump LFO values use the compact 0..10 scale
    (depth 6 = ±3, center 5 = mid-travel). Omit "center" and the processor
    rests at mid-travel. Exact fader/pan LFOs use their native 0..1/-1..1
    ranges and REQUIRE center, as described in EXACT RULES.
  Static forms also exist as track knobs: "lowpass":4 / "highpass":3 in
  any track's "controls" (they're pedalboard fx, so they work on recorded
  instruments — filter the real bass, not just synths).

### H.6 MASTER MOVES — TIMED TRANSITIONS ON THE COMPLETE MIX

  "master":[{"fx":"killLow","atBeat":64,"beats":4}, ...]
    killLow  — cut all bass for the window, slam back at the end (a house/club
               transition: kill 2-4 beats before the drop, return ON it)
    killHigh — underwater filter-down (everything above ~600Hz gone)
    tapeStop — playback slows+drops to silence across the window (1-2 beats;
               place a fresh section right after — the jump-cut IS the effect)
    stutter  — beat-repeat: the window's first slice loops for the window
               ("unitBeats":0.25 default = 16th-note stutter)
    narrow   — pull the stereo image toward MONO for the window (smooth in and
               out). One breakdown move is to narrow the image, then restore
               full width ON the drop so the room appears to open.
    open     — extra-wide image for the window: a drop or a final chorus that
               must feel BIGGER than the ones before it. Mono-safe (phones
               and club subs hear the same mix).
  Use sparingly—often one or two deliberate moves in the whole piece—at
  transitions whose contrast justifies processing the complete mix.

### H.7 RICHNESS & VARIATION — DESIGN CONTRAST PER SECTION, NOT PER PIECE

  - Layer count is one richness dial. As a starting reference, 3-4 simultaneous
    layers reads sparse and 6-8 reads full, but one sound can be enormous and
    twelve can be transparent. Let register, envelope, and spectral density
    decide. Avoid running the maximum stack for the whole piece unless mass is
    the concept.
  - DOUBLE for thickness: the same line on a second instrument an octave up
    at vol ~0.4; bass doubled by sub_drone roots; a doubled synth with
    detune 6-8 = the supersaw wall.
  - A common clarity strategy is one busy foreground element at a time: while
    it speaks, supporting layers simplify; in its rests, percussion or a
    counter-phrase answers. Dense polyphony is also possible when register,
    rhythm, and tone keep its voices intelligible.
  - REPEAT vs VARY: 70/30 is a useful starting ratio, not a law. Groove
    elements often repeat more than foreground material because recurrence
    makes a pocket legible. Use extends-patterns for forms such as A A A' B,
    where A' adds one meaningful change. Reserve fills and simultaneous large
    changes for boundaries that need emphasis; restraint makes them register.

### H.8 ENERGY ARC — COMPOSE CHANGE, ANTICIPATION, RELEASE, AND RETURN

  Sketch energy 1-10 over the timeline, e.g. EDM: intro 3 → build 6 →
  drop 9 → breakdown 2 → build 7 → final drop 10 → outro 3.
  OPTIONS FOR RAISING energy: add layers one entrance at a time; raise
  hat density (4ths → 8ths → 16ths); noise_riser spanning the last 8 beats
  ENDING exactly at the drop; arrangement "vol" creeping 0.7 → 0.85 → 1;
  transpose +5 on a later return; place a fill before, or an impact on, a
  selected section boundary. Choose the moves that belong to the style.

#### LAYER COUNT ALONE DOES NOT RAISE MEASURED LEVEL

  LAYER COUNT ALONE DOES NOT RAISE MEASURED LEVEL — read this with "glue"
  below. More layers hit the glue compressor harder, so it clamps harder, and
  a section can end up LESS dynamic as it gets denser: the arc you wrote is
  real in the score and cancelled in the render. What actually moves level
  across sections is arrangement "vol" creep, transpose, and register — so
  pair every staircase of entrances with a vol step, and keep the thin
  sections genuinely thin (fewer layers, not quieter ones) so the dense ones
  have somewhere to arrive.

#### HOW BIG A VOL STEP

  HOW BIG A VOL STEP: above its threshold the glue compressor divides written
  section contrast by (1.5 + 0.25 x glue). So at a common glue 4 that is
  2.5:1 — a 2 dB step in arrangement "vol" arrives as 0.8 dB, which nobody
  hears. To land ABOUT 2 dB of real separation between sections, step "vol"
  by roughly x1.3 (e.g. 0.7 → 0.9 → 1.0), not x1.05. At glue 8 you need
  ~x1.5. If you want the arc to survive untouched, keep glue at 0-2 and
  separate the sections by arrangement instead.
  OPTIONS FOR DROPPING energy: remove the selected pump-source notes (pumped layers then stop
  breathing automatically — the release the dancefloor feels); keep pads +
  one melodic element; noise_fall as the exhale; thin drums to ticks/shaker.
  Chill genres (lofi, ambient): keep the arc nearly flat — one added shaker
  at bar 17 reads as an event.
  THE ENDING is a composed moment, not an accidental truncation. It may be a
  cadence, deconstruction, tail, hard cut, or DJ-friendly outro. Land the
  chosen gesture inside durationSec; use fader automation when coordinated
  silence or a shaped tail serves it.

### H.9 EMOTION — TRANSLATE FEELING INTO ENGINE DECISIONS

  These are starting vectors, not emotion formulas. Context can invert any
  association; choose the combination that serves the requested scene or song.
  happy/uplifting — major key, 100-128bpm, bright cutoff, octave doubles.
  sad/longing — minor, 60-90bpm, sparse, reverb 5+, low register, space.
  tense/dark — minor over a held drone root, chromatic neighbor tones,
    phaser/tremolo unease, dissonant pad held too long on purpose.
  epic — slow harmonic rhythm (one chord per 2-4 bars), tuba/sub_drop +
    crash, wide detune, arc rising to 10.
  nostalgic/lofi — crush + vinyl_crackle, swing 3-5, mellow 7th chords.
  dreamy — chorus + reverb 6+, whole-note pads, humanize 3, soft vol.
  The strongest emotional tool is SPACE — what you leave OUT: fear and
  longing live in rests and low density; joy lives in rhythmic density.

### H.10 COMPOSITION PRACTICE — MUSICAL JUDGMENT INSIDE THE CONTRACT

- A practical score uses 3 to 16 musical tracks, but density is an artistic
  choice: four carefully differentiated lanes can feel complete, while a rich
  arrangement may use 10+ tracks whose entrances never all coincide.
- Maintain one dominant low-frequency role at a time so kick, bass, sub, and
  low percussion remain intelligible. Harmony may be pad, drone, guitar, keys,
  strings_pad, sparse stabs, or deliberate absence.
- Choose a foreground identity when the piece needs one: melodic phrase,
  rhythmic motif, vocal-space gesture, instrumental performance, or signature
  texture with rests. A keyboard melody is one option, never an automatic layer.
- Establish a coherent harmonic language. One key is the simplest strategy;
  modal writing, chromatic color, borrowed chords, and modulation are available
  when they are deliberate and audible. Chords are simultaneous notes at one t.
- VOICE CHORDS FOR THE INTENDED READ. When direct harmonic clarity matters,
  start with an audible root and 3rd; for example, Cm7 = C-Eb-G-Bb. Extensions,
  rootless voicings, clusters, ambiguity, and a moving bass are available when
  that color is intentional. Register and arrangement determine whether such
  complexity reads as richness or vagueness.
- The beat grid is the reference: beat = 60/bpm seconds. Establish the pulse
  with grid-aligned events, then use swing, lateMs, @ms, humanize, probability,
  flam, and roll for intentional feel rather than accidental imprecision.
- Drum grammar follows the style. Four-on-the-floor kick, backbeat clap, and
  offbeat hats are available house tools—not universal defaults. Breakbeats,
  sparse pulse, polyrhythm, acoustic performance, and percussion-led grooves
  are equally valid uses of the engine.
- Follow the requested sections, or design a form when none is specified.
  Change energy through entry, exit, density, register, rhythm, timbre, space,
  and level. Compose the ending inside durationSec.
- Humanize when the performance calls for it: vary repeated-hit level and
  timing for organic feel; keep equality and rigid timing when machine intent
  is part of the music.
- Drum vol is EXPRESSIVE, not just loudness: it selects how hard the real
  drummer hits (soft vol = brushy quiet strike, high vol = full slam). The
  available expressive range is roughly ghost notes 0.25, groove 0.5, accents
  0.9; use the portion that matches the performance.

### H.11 LONG-FORM MOTION — REPEAT WITH PURPOSE

- Repetition creates identity and hypnosis; change creates direction. Decide
  which one the request needs. When a section should evolve, every 4-8 bars use
  one meaningful move: change voicing, remove the pattern for a bar, automate
  the filter, change arrangement "vol", transpose an instance, or alter rhythm.
  In deliberately minimal music, an unchanged pattern may be the concept—but
  surrounding entrances, exits, space, and timbre must make that choice legible.
- Two or three variants of the same pattern (CHORD_A / CHORD_B) alternating
  costs almost nothing in tokens and is the whole difference.

- Repetition is FREE via patterns — keep the UNIQUE notes you write to ~2000;
  the expanded total (patterns × repeats) may be far larger. For long pieces
  (60s+), use patterns so the response remains compact and complete.

## I. BEFORE RETURNING THE SCORE

### I.1 SILENT PRE-OUTPUT VALIDATION — REPAIR BEFORE RETURNING THE SCORE

- CONTRACT: JSON.parse() succeeds; every name resolves in its closed symbol
  table; only documented keys are present; top-level glue is not nested under
  mix; pattern timing is in beats and direct-track timing is in seconds; the
  deliberate ending lands inside durationSec.
- SOUND: factory instruments are referenced by name, not copied into "synths".
  Every ex_ patch has a factory-DNA starting point and intentional changes.
  Every dual-oscillator ex_ patch starts from the closest dual-oscillator role
  blueprint and uses that topology because the sound needs it, not merely to
  look sophisticated.
  Every exd_ drum starts from the closest engine starter DNA, uses the right
  model/bus/choke role, and changes only parameters with a musical purpose.
- STYLE: an unfamiliar/current genre has been researched and translated into
  groove, arrangement, sound hierarchy, and production—not merely named.
- TASTE: no keyboard, square/FM, toy, retro, bagpipe, or orchestral
  voice leads unless the request or musical concept calls for that character.
- ROLES: bass, foreground identity, beds, percussion, and transitions are
  distinct. Every ex_ bass declares "bus":"bass"; only a genuine foreground
  part declares "bus":"lead"; routing, depth, and level do not overstate it.
- ROUTING: every named bus has a deliberate role and ordered rack; every send,
  effect automation selector, and sidechain source resolves; the graph is
  acyclic. Parallel buses preserve the dry identity intentionally rather than
  duplicating sound by accident. Exact automation uses native parameter units.
- ARC: the requested form is audible. Where a boundary should change energy,
  entry, exit, density, filter, width, rhythm, register, or silence carries the
  change; a riser alone does not substitute for arrangement.
- MOTIF: any foreground hook has intentional rhythm, contour, recurrence, and
  space rather than filler notes or an aimless walk across a keyboard.
- MIX: low-frequency ownership is intentional; competing parts are separated;
  stereo has a coherent centre and sides; textures and full-density passages
  have the lifecycle the concept requires rather than running by default.
- VERIFY: when rendering or audio analysis is available, use it. Check section
  contrast, spectral balance, foreground dominance, ending, and technical
  validity. Revise until the music and the score both satisfy the request.
- RESPONSE: return only the repaired JSON object required by the opening
  FINAL RESPONSE CONTRACT. Do not output this checklist or describe compliance.

### I.2 A COMPLETE 60-SECOND SCORE

A COMPLETE 60-SECOND SCORE (copy this SHAPE, never these notes). 128 BPM,
128 beats = exactly 60 s, four 8-bar sections: intro / build / drop / outro.
Nine patterns and twelve arrangement entries carry the whole piece — note how
the drop reuses the intro's chords rather than restating them, how KITQ and
CHDQ are the SAME patterns thinned with "only", and how each section steps
"vol" by ~x1.3 so the arc survives the glue.

{"bpm":128,"durationSec":60,"swing":2,
 "patterns":{
  "KIT":{"instrument":"drums","lenBeats":4,"notes":[
    "0 e_kick 0.95","1 e_hat_closed 0.35","1 e_clap 0.75",
    "2 e_kick 0.95","3 e_hat_closed 0.35","3 e_clap 0.75"]},
  "KIT2":{"extends":"KIT","notes":["1.5 e_hat_open 0.3","3.5 e_hat_closed 0.3 p0.7"]},
  "KITQ":{"extends":"KIT","only":[0,2]},
  "BASS":{"instrument":"reese_bass","lenBeats":8,"controls":{"cutoff":3},"notes":[
    "0 A1 0.75 0.9","1.5 A1 0.25 0.6","2 A1 0.5 0.8",
    "4 F1 0.75 0.9","5.5 F1 0.25 0.6","6 G1 1 0.85"]},
  "CHD":{"instrument":"saw_chords","lenBeats":8,"depth":"back",
    "controls":{"cutoff":4,"reverb":3},"notes":[
    "0 A3 1.5 0.5","0 C4 1.5 0.5","0 E4 1.5 0.5",
    "2 A3 1.5 0.45","2 C4 1.5 0.45","2 E4 1.5 0.45",
    "4 F3 1.5 0.5","4 A3 1.5 0.5","4 C4 1.5 0.5",
    "6 G3 1.5 0.5","6 B3 1.5 0.5","6 D4 1.5 0.5"]},
  "CHDQ":{"extends":"CHD","only":[0,4]},
  "HOOK":{"instrument":"glass_lead","lenBeats":8,"bus":"lead","notes":[
    "0 E5 1 0.62","1.5 C5 0.5 0.55","2 A4 1.5 0.62",
    "4 F5 1 0.62","5.5 E5 0.5 0.55","6 C5 2 0.65"]},
  "RISE":{"instrument":"noise_riser","lenBeats":8,"bus":"fx","notes":["0 A4 8 0.5"]}
 },
 "arrangement":[
  {"pattern":"CHDQ","atBeat":0,"repeat":4,"vol":0.7},
  {"pattern":"KITQ","atBeat":16,"repeat":4,"vol":0.8},
  {"pattern":"KIT","atBeat":32,"repeat":8,"vol":0.9},
  {"pattern":"CHD","atBeat":32,"repeat":4,"vol":0.9},
  {"pattern":"BASS","atBeat":32,"repeat":4,"vol":0.9},
  {"pattern":"RISE","atBeat":56,"repeat":1},
  {"pattern":"KIT2","atBeat":64,"repeat":8},
  {"pattern":"CHD","atBeat":64,"repeat":4},
  {"pattern":"BASS","atBeat":64,"repeat":4},
  {"pattern":"HOOK","atBeat":64,"repeat":4},
  {"pattern":"KITQ","atBeat":96,"repeat":8,"volFrom":0.8,"volTo":0.3},
  {"pattern":"CHDQ","atBeat":96,"repeat":4,"vol":0.7}
 ],
 "automation":[
  {"pattern":"CHDQ","knob":"lowpass","points":[[0,7],[32,2,"exp"]]},
  {"pattern":"BASS","knob":"cutoff","points":[[32,2],[64,7],[96,7],[120,2]]},
  {"pattern":"HOOK","param":"track.pan","lfo":{"atBeat":64,"beats":32,"period":8,"depth":0.6,"center":0}},
  {"pattern":"KITQ","param":"track.fader","points":[[112,1],[128,0]]}
 ],
 "master":[{"fx":"killLow","atBeat":60,"beats":4},{"fx":"narrow","atBeat":96,"beats":8}],
 "glue":3
}

### I.3 ORDER DOES NOT MATTER

ORDER DOES NOT MATTER in "arrangement", "automation" or "master" — every
entry carries its own absolute beat, so the engine places it correctly
whatever order you emit. Group them however is clearest to write (by section,
as above, or by instrument) and don't spend effort sorting. The one ordering
that IS real is inside a pattern's "notes": nothing requires it, but keeping
each pattern in beat order is how you notice a gap you didn't intend.


===============================================================================
PART 2 OF 4 — SOUND: ELECTRONIC MUSIC PRODUCTION PRINCIPLES (ADVISORY)
Standalone file: electronic-music-principles.md
===============================================================================

# Electronic Music Production Principles

> **Use with the Beat Lab score guide.** That document is authoritative on syntax —
> what fields exist, what values are legal, how a score compiles. This one is
> advisory on musical judgment: tempo, kick design, low end, groove, harmony,
> arrangement, mix targets. Where the two disagree about what is *possible*, the
> score guide wins. This document never overrides an explicit user instruction.

A working reference for a model composing electronic music. These are **additional
principles, not ground truth** — craft conventions that hold often enough to be useful
defaults, and that should yield to an explicit instruction, a genre that works
differently, or a deliberate aesthetic choice.

Every numeric value here is a *starting point with a reason attached*. Prefer the
reasoning to the number: when a rule says "107 ms", what it means is "one sixteenth
note at 140 BPM" — recompute it for the actual tempo rather than copying the figure.

**Scope and bias.** Derived from a techno-centric body of instructional material
(see [Provenance](#provenance)). Rules marked `[techno]` are style-specific;
unmarked rules generalize across four-on-the-floor electronic genres and usually
beyond. Where a claim rests on a single measured demonstration it is marked
`[measured]` — reproducible in principle, but one source's measurement.

---

## 1. Tempo and genre frame {#tempo}

Tempo is the first decision because it sets every time-derived value downstream —
envelope decays, delay times, compressor releases, choke lengths.

| Genre | BPM | Signature traits |
|---|---|---|
| House / melodic techno | 120–125 | Off-beat hats, longer chord tails, swing |
| Techno | 125–135 | Tight kick decay, 909-derived palette, minimal harmony |
| Hard techno / bounce | 140–155 | Distorted kick, rumble low end, sparse harmony |
| Hip-hop / trap | 70–90 (or 140–170 half-time) | Long 808 tails, sampled drums |

**Derived values at a glance.** One sixteenth note = `15000 / BPM` ms.

| BPM | 1/16 | 1/8 | 1/4 | 1 bar (4/4) |
|---|---|---|---|---|
| 124 | 121 ms | 242 ms | 484 ms | 1.94 s |
| 128 | 117 ms | 234 ms | 469 ms | 1.88 s |
| 140 | 107 ms | 214 ms | 429 ms | 1.71 s |
| 150 | 100 ms | 200 ms | 400 ms | 1.60 s |

Use this table constantly. A great many "feel" parameters are simply grid values in
disguise.

---

## 2. The kick {#kick}

In four-on-the-floor genres the kick is not one element among many — it is the
track's spine, its loudest event, and the thing every other low-frequency decision
is made relative to. Build it deliberately.

### 2.1 Synthesis from first principles

A kick is three things stacked: **a pitched body, a pitch envelope, an amplitude
envelope.** A bare sine at 50 Hz is a hum; the envelopes are what make it a drum.

```
body      = sine at the target fundamental (~50 Hz typical)
pitchEnv  = 150 Hz -> 50 Hz, falling over ~50 ms   # this IS the attack
ampEnv    = attack 0.8 ms, hold 0-25 ms, decay 100-550 ms
click     = short noise/transient burst, first ~5 ms
```

The pitch envelope does the perceptual work. A fast drop from roughly 3× the
fundamental down to the fundamental reads as "impact" because it imitates a
physical drumhead losing tension. Too slow and it becomes a tom; too fast and it
disappears into the click.

### 2.2 The amplitude envelope is the genre dial

Attack stays sub-millisecond almost everywhere (0.8 ms). **Hold and decay carry the
genre:**

- `hold 25 ms, decay 100 ms` — techno. Short, punchy, leaves the bar open for a
  bassline. `[techno]`
- `decay 550 ms` — 808-style. Long, boomy, *becomes* the bassline and therefore
  forbids a separate one in the same register.

This is the single most consequential kick parameter. Choosing a 550 ms decay is
choosing not to have an independent bass part below ~80 Hz.

### 2.3 Layering: three bands, three jobs

Rather than one synthesized kick, build three layers that each own a frequency band
and a slice of time:

| Layer | Band | Role | Typical level |
|---|---|---|---|
| Sub | low-passed at 120 Hz | weight | loudest |
| Punch | 110 Hz – 5 kHz | chest impact | mid |
| Click | high-passed at 2.5 kHz, ~30 ms long | attack | ~−16 dB under full kick `[measured]` |

**The handoff matters more than the layers.** Where punch ends and tail begins, the
envelopes must *overlap*, not abut. A 10 ms gap between them carves a hole of
roughly 25 dB in the envelope; about 7 ms of overlap reduces that dip to ~5 dB.
`[measured]` Start the tail a few milliseconds before the punch finishes.

Process each layer separately, then soft-clip them together on a single bus — same
peak, more apparent weight. Match the tail's pitch to where the punch lands; the
same punch with a different tail is, perceptually, a different kick.

### 2.4 Tuning the kick to the track

A kick is a pitched event, and if its pitch disagrees with the bass root the two
*beat* against each other — the low end audibly swings in level while the bass note
sustains, which reads as an uneven, amateurish bottom end.

**Procedure:**
1. **Find** — the kick's pitch is the strongest spectral peak of its body in the
   25–120 Hz band.
2. **Compare** — against the bass root, or the track's key.
3. **Tune** — retune the kick to the bass root.
4. **Check polarity** — after tuning, flip the phase and keep whichever is louder.

Worked example `[measured]`: a kick ringing at 50.8 Hz (G♯1) against a 55 Hz (A1)
bass sits 1.4 semitones out. Level-matched, the low-end swing across the bass note
measures 15.8 dB clashing versus 0.2 dB once tuned. Polarity inversion on the same
pair moved the low end by 12.5 dB — worth one A/B every time.

Side effect to anticipate: pitching a kick up shortens it. Two semitones up ended
the kick about 8% sooner (400 → 368 ms), while the click barely moved.

Three valid fixes, in order of preference: retune the kick, choose a kick that
already fits, or retune the bass.

### 2.5 Processing for hard genres `[techno]`

Distortion on the full kick destroys the sub. Instead, **send only the top of the
kick into distortion and leave the sub dry.**

- Clip the send for weight — at +9 dB drive, roughly +7.7 dB more loudness at the
  same peak, with energy above 2 kHz up 3.5 dB. `[measured]`
- Blend the distorted send about 9 dB under the dry kick.
- EQ *before* the clipper chooses what gets distorted; EQ *after* trims fizz and
  low mids.
- Clip before you limit — same loudness for far less limiter work.
- Past roughly +27 dB drive the punch is gone. Distortion trades transient for
  density; past a point there is no transient left to trade.

### 2.6 Making a kick survive small speakers

Phone and laptop speakers reproduce almost nothing below ~130–150 Hz. A pure sub
kick is *silent* on them.

The fix is harmonic, not level-based: saturate to generate overtones above the
cutoff. A 50 Hz fundamental driven ~9.5 dB produces partials at 150, 250 and 350 Hz
— the listener's ear reconstructs the missing fundamental from the harmonic series.
Keep the clean sub underneath and blend a saturated copy (around 75% drive,
25% blend) rather than distorting the whole kick.

### 2.7 Kick EQ: three moves

Resist the urge to sculpt extensively. Three moves cover most cases:

| Move | Setting | Purpose |
|---|---|---|
| Cut mud | −4 dB @ 320 Hz | removes boxiness |
| Lift click | +3 dB @ 4.5 kHz | cuts through the mix |
| Add weight | +2.5 dB low shelf @ 60 Hz | fills the bottom |

In this engine those are three bands chained on one bus — `bell` for the first two,
`shelf` for the third. The older three-band `eq` effect has fixed crossovers and
gain only, so it cannot place a move at a frequency; reach for `bell`:

```json
"effects":[
  {"id":"mud","type":"bell","freq":320,"gain":-4,"q":1.4},
  {"id":"click","type":"bell","freq":4500,"gain":3,"q":1.2},
  {"id":"weight","type":"shelf","mode":"low","freq":60,"gain":2.5}
]
```

---

## 3. The low end: kick versus bass {#low-end}

Kick and bass both want roughly 80 Hz. Unmanaged, they mask each other and the mix
turns to mush. Five rules resolve nearly all of it.

**1. Split them with EQ.** Decide which source owns the sub. Typically the kick
owns it; carve the bass at the kick's fundamental (e.g. −14 dB, Q 1.4, at 80 Hz).
Ownership is a decision, not a compromise — refusing to decide is what creates mud.

**2. Sidechain the bass to the kick.** Fast attack (~1 ms), short release (~90 ms),
6–8 dB of reduction. The critical constraint: **the bass must be back up before the
next note.** Ducking is a timing tool, not a loudness tool. A release that outlasts
the gap between hits stops the groove breathing.

**3. Keep the sub mono.** Crossover at 120 Hz: mono below, stereo above. Wide low
frequencies partially cancel on mono playback (club subs, phone speakers) and the
weight simply vanishes. Keep width high *above* the crossover — the rule costs
nothing in perceived stereo image.

This engine has **no frequency-dependent width**: the `width` effect is broadband
(0 = mono, 1 = unchanged, 2 = double), and a bus split into a mono low path and a
wide high path does not separate cleanly — a 12 dB/oct crossover leaks enough bass
into the wide path to undo the point. So apply the rule at the source instead:
leave low material centred. Don't pan kicks or sub basses, and don't put `width`
above 1 on any bus carrying them. Widen the hats, percussion, pads and effects
returns, where there is no weight to lose.

**4. Saturate the bass** for the same reason as the kick (§2.6). Keep the clean sub;
blend harmonics on top.

**5. Check three systems** — headphones, monitors, phone. Each lies differently:
headphones exaggerate bass by around +5 dB with no room contribution; rooms distort
the low end most of all. The phone check is not optional, it is where most listening
happens.

---

## 4. Drums and groove {#groove}

### 4.1 Build order

Introduce elements one lane at a time, each establishing before the next arrives:
**kick → hats → clap → percussion.** A four-on-the-floor kick with slightly more
weight on beat 1; hats carrying speed; clap on 2 and 4 as the backbone; percussion
last, as detail.

### 4.2 The off-beat grid

On a 16-step bar, beats fall on steps 1, 5, 9, 13. **Steps 3, 7, 11, 15 are the
off-beat eighths** — and that position recurs constantly: off-beat hats, off-beat
rides, chord stabs between kicks. It is the defining rhythmic signature of house and
techno. When something feels rhythmically inert, placing it on 3/7/11/15 is the
highest-yield single edit.

### 4.3 Techniques that create motion without new elements

- **Ghost notes.** Quiet hits just before the beat at velocity 48–60 (against ~100
  for main hits), choked by the main hit. Ghost notes are a velocity-and-choke
  technique; played loud they are just more notes.
- **Open-hat choke.** Open hat on the off-beat, cut by the next closed hat. The tail
  length is a grid value — one sixteenth (107 ms at 140 BPM), not a taste setting.
- **Flam.** Layer a second clap 13 ms late. Under ~20 ms an offset reads as *width*,
  not as a separate rhythmic event. Above it, it becomes a double-hit.
- **Velocity ramps.** Take a clap from velocity 36 to 124 over 4 bars. Tension
  entirely through dynamics, nothing added.
- **Three over four.** A hit every 3 sixteenths against a 4/4 grid: the accent walks
  and the cycle only realigns with the bar after 3 bars. The cheapest source of
  sustained motion in a loop, and it requires editing nothing after you place it.
- **Tom fills.** Pitched percussion walking down (+7 to −5 semitones over 8 steps),
  placed in bar 4 of a 4-bar phrase. Descending pitch reads as falling energy.

---

## 5. Harmony and bass {#harmony}

### 5.1 Key and progression defaults

A minor is the default working key for this idiom, with two progressions covering
most ground: **Am–F–C–G** (open, anthemic) and **Am–Dm–E–Am** (i–iv–V–i, darker and
more resolved).

**Harmonic minor is the main lever.** Raising the 7th (G → G♯ in A minor) turns the
v chord from Em into **E major**, creating a true leading tone and a strong pull home.
This single accidental is responsible for most of the "dark electronic" harmonic
flavour.

**Deceptive cadence:** build the pull with E major, then land on F instead of Am. The
expectation is created and deliberately not satisfied, so the track keeps moving —
useful precisely because looped music cannot rely on a final cadence.

### 5.2 Chord colour

Same roots, different extensions, different mood:

- Root position — plain, stable
- Voice leading — move the nearest note, not the whole shape
- Seventh chords — jazzier, more tension
- **Add9 voicings** (Am9, Fadd9, Cadd9, Gadd9) with the 9th on top — wide, emotional
- Spread voicing — more space between voices, bigger
- Off-beat stabs — short chords on steps 3/7/11/15, one step long

### 5.3 Bass patterns

Five archetypes: root notes, off-beat, rolling, octave, groove.

- **Rolling** `[techno]` — 1/16 notes in a kick-bass-bass-bass figure.
- **Walk down** — roots descending stepwise (A–G–F–E) so the bass spells the
  progression rather than restating each root.
- **Approach notes** — one step before the chord change, a note leading by a step
  into the next root. Placed at step 15, it makes the change feel inevitable.
- **Three-step loop** — a figure repeating every 3 sixteenths, phasing against the bar.
- **Octave jumps / stacked fifth** — two voices at +7 semitones for a power or Reese
  bass.
- **Pedal note** — hold one bass note for 4 bars while chords move above it
  (Am/A, F/A, C/A, G/A). Tension without touching the groove.
- **Dub treatment** — pure sine sub, roughly 3 notes per chord, lots of space. Genre
  here is expressed through *density and timbre*, not different theory.

### 5.4 Melody and lead

- **Contour: one peak per phrase.** An arch shape with a single highest note. Two
  peaks read as two competing melodies.
- **Place the climax in bar 3** of a 4-bar phrase — roughly three-quarters through,
  not at the start and not at the very end.
- Call and response, a repeating motif, landing on chord tones, and leaving space
  are the remaining levers.
- **Repeat, then change:** play the phrase twice and alter only the last beat.
  Repetition establishes the idea; the altered ending prevents fatigue.

### 5.5 Arps and pads

- Arp patterns: up, up-and-down, **octave (order 1-8-5-8)**, gated, three-over-four.
  The octave jump is what makes an arp read as electronic rather than classical.
- **Common tone:** hold one note (e.g. C5) on top while the voices below move
  through the progression. A fixed top note glues a progression together.
- **Rhythmic pad:** cut a sustained chord into a pattern — ~5 hits per bar, each 2–3
  steps long. A pad does not have to be a drone.
- Pad envelope reference: attack 550 ms, sustain 75%, release 0.9 s. A pluck and a
  pad can be the same chord through the same synth, differing *only* in envelope.

---

## 6. Synthesis {#synthesis}

### 6.1 The four blocks

Oscillator → filter → envelope → LFO. Almost every synth is this, elaborated.

**Harmonic content by waveform:** sine = 1 partial (pure); saw = all partials
(bright, buzzy); square = odd partials only (hollow). Choose the waveform by how
much spectrum you need the filter to remove later.

### 6.2 Wavetables

A wavetable here is **one** cycle, written as a short list of values. You are
drawing a waveform, not morphing between stored frames — so the table is a
*spectrum you author*, the one timbre reachable neither from sine, saw, square
nor triangle. That is what justifies it; the shape itself is the creative act.

If you have read about 256-frame tables with a position knob as the timbre axis,
that is a different architecture. This engine has **no position axis**, and
nothing modulates one.

- **Resolution is a brightness control.** Values are joined by straight lines, so
  a short table is angular and buzzy, a long one smooth and closer to its ideal.
  Reach for few points when you want harmonics, many when you want purity.
- **Absolute numbers don't survive.** The compiler removes DC and peak-normalizes
  the cycle, so only the shape carries: offsetting or scaling every value changes
  nothing. Set loudness on the oscillator's level, not in the table. A table of
  identical values is rejected — it would be silence.
- **Movement is a separate decision.** A single-cycle table is a fixed timbre, so
  motion comes from the rest of the patch: crossfade the table against a second
  oscillator, bend it with waveshaping, or hard-sync and ring-modulate it — then
  drive any of those from an envelope or LFO rather than leaving them static.

See the syntax guide for the field names, limits and the modulation matrix.

### 6.3 FM

One oscillator (the modulator) pushes the phase of another (the carrier). Below
about 20 Hz that is vibrato; at audio rate it creates **sidebands** — new partials
above and below the carrier — which is where bells, tines, FM basses and electric
pianos come from. The engine has two ways in: the compact `fm` oscillator is one
sine pair with a ratio, an index and an index decay that always falls to zero;
the operator architecture (`ops` + `routes`) is the DX7 / Operator model, and it
is the one to reach for when any of the points below matter.

- **Ratio** determines harmonicity. Integer ratios (1:1, 2:1, 0.5:1) give
  pitched, musical tones; non-integer ratios (1.41, 3.5, 7.01) give bells and
  metal; a ratio of 10 or more on a modulator with a 50–150 ms envelope is a
  click or a tine, not a tone.
- **Index** determines how much spectrum is generated. Roughly: 0.3–1.5 adds
  warmth, 2–4 is a bright keyboard or bass, 5–8 is bells and metal, 9–12 is
  noise-like. Index is a radian value, so the same number means the same
  brightness at any ratio.
- **Envelope the index — and give it a floor.** A falling index (peak ~5.9,
  decaying over 70 ms, resting at 0.4) gives a bright attack settling into a
  purer sustain; the rest value is the sustain of the *modulator's own* envelope.
  A floor of zero is a sine after the attack, which reads as a plink; a floor of
  0.3–0.5 keeps a held note alive. This one trick is most of what makes FM
  basses, bells and electric pianos work.
- **Velocity on the modulator, not just the carrier.** Letting note volume scale
  a modulator's output means accents get brighter rather than merely louder —
  the thing that makes an FM electric piano feel played.
- **Stacks and pairs are different sounds.** A→B→C (a modulator modulating a
  modulator) sharpens into metal fast; two pairs summed at the output (the
  electric-piano layout: a body pair plus a detuned pair with a tine click) stay
  musical at higher total brightness. Two carriers 4–8 cents apart is the FM
  chorus.
- **Feedback** is a self-modulating operator: 0.2–0.4 thickens a sine, 0.5–0.7
  turns it saw-like without a filter, 0.9 and above is a harsh edge.
- **Fixed-frequency operators** hold an absolute pitch while the note moves: a
  formant that stays at 640 Hz across a chord, or a 3 Hz operator used as an
  extra slow modulator on a modulator.

See the syntax guide for the field names, limits and the route rules.

---

## 7. Dynamics and compression {#compression}

### 7.1 What the controls actually do

- **Threshold** — the level above which reduction begins. Below it, nothing happens.
- **Ratio** — how hard it pulls down above the threshold. 4:1 is a general default;
  12:1 and above is ducking or effect territory.
- **Knee** — hard knee switches abruptly at the threshold; soft knee eases in.
- **Makeup gain** — restores the level compression removed.

**This engine does not expose any of those four.** It offers compression as
amount knobs (0–10) with the decisions already made inside: `squash` (fast,
aggressive), `smooth` (slow program-dependent leveling), `glue` (one mix-bus
compressor over drums + percussion + bass together), `punch` (transient
enhancement) and `pump` (onset-triggered ducking). That is a deliberate design,
not a missing feature: a threshold in dB is meaningless without hearing the signal
level, so a value guessed blind either does nothing or destroys the take, whereas
every value of an amount knob yields a sane result. Read §7.1 to understand what
the knobs are doing; reach for the knobs to do it.

### 7.2 Attack and release are the whole instrument

**Attack decides how much transient survives.** Sub-millisecond attack (0.3 ms)
catches the very first click, shrinking the transient — the drum becomes softer and
rounder. On drums, start between **10 and 30 ms** and deliberately let the transient
through, compressing what follows it.

**Release must resolve before the next hit.** A 700 ms release at 140 BPM never
recovers between hits and the groove stops breathing; ~110 ms (one sixteenth at that
tempo) tracks the groove. Release is a tempo value, not a taste value.

This engine agrees with that second rule to the point of enforcing it: the only
release control it exposes, `pumpRelease`, is specified **in beats** (0.15–1.5),
not milliseconds, so a duck cannot drift out of time when the tempo changes. For
attack there is no parameter — `punch` adds transient rather than letting you
choose how much to eat, which is the same decision from the other side.

### 7.3 Always compare level-matched

Compression lowers peaks; makeup raises everything. Compared un-matched, compression
always sounds "better" because it is simply louder. Level-matched, the honest
description is: *same loudness, but the quiet detail steps forward.* Judge it that
way or you are not judging compression at all.

### 7.4 Compressor character

At identical settings and matched level, the topology still changes the sound:

| Type | Character | Typical use | In this engine |
|---|---|---|---|
| VCA | clean, precise, transparent | the general-purpose workhorse | — |
| FET | fast, aggressive | drums, snare edge | `squash` |
| Opto | smooth, slow, breathing release | vocals, bus glue | `smooth` |
| Vari-Mu | warm, glue | mix bus | `glue` (top-level) |

There is no topology to select here, and the two poles that actually matter —
fast-and-aggressive versus slow-and-gentle — are the two knobs. Asking for "an
Opto on the bus" means writing `smooth`.

### 7.5 Two structural uses

- **Parallel compression** — duplicate, crush the copy (20:1, 0.5 ms attack), blend
  it ~35% under the dry. Keeps the transient *and* adds weight, which serial
  compression cannot do simultaneously.
  *Here:* send the source bus to a second bus (`"tap":"post"`), put `squash` high
  on that return, and set the return's `fader` to the blend. The send amount and
  the return fader together are the "35%".
- **Sidechain** — a compressor keyed from another track. Kick ducking a pad at 12:1
  with 200 ms release makes room rhythmically. See §3 for the bass case, and §9 for
  ducking reverb returns.
  *Here:* a bus `sidechain` block names its sources explicitly (`{"track":"KICK"}`,
  `{"drumHit":"e_kick"}`, or a silent `trigger`), with `amount` 0–10 and
  `attackMs`/`releaseMs`. Per-track, `pump` + `pumpFrom` does the same job. There
  is no implicit kick detection — the key is always declared.

---

## 8. Movement and automation {#automation}

A loop that feels boring usually does not need more elements — it needs movement.
Every automation move is defined by five things: **parameter, start value, end
value, length in bars, and curve shape.** The curve is the shape of the line between
two points, and it matters as much as the endpoints.

| Move | Parameters | Effect |
|---|---|---|
| Ramp per bar | cutoff 260 Hz → 6.5 kHz, length 1 bar, sawtooth | reads as groove |
| Same ramp over 4 bars | — | reads as a build |
| Resonance ride | cutoff rising, resonance 0.2 → 0.85 peaking at bar 3 | peak in the middle, then back off |
| Noise riser | band-pass filter rising to 7.1 kHz **and** volume −7.8 → +24 dB | build-up (two lanes, not one) |
| Reverb throw | send normally 0, spiked for one hit at beat 16, long decay | fills a turnaround without washing the groove |
| EQ bell sweep | gain +14 dB, q 5, freq 200 Hz → 6 kHz over 4 bars | reads as "leaving" |

Units here are native, not percentages: `resonance` runs 0–0.9, a send `amount`
0–1, a bell's `gain` ±24 dB and its `q` 0.1–18. Sweep a band by giving it an id and
naming that id as the automation target — `freq`, `gain` and `q` all move:

```json
"buses":{"music":{"effects":[{"id":"sweep","type":"bell","freq":200,"gain":14,"q":5}]}},
"automation":[{"bus":"music","effect":"sweep","param":"freq","points":[[0,200],[16,6000]]}]
```

Note the pattern: the *same* cutoff ramp is a groove element at one bar and a build
at four. Length is what assigns meaning, which is why automation should be written
against the arrangement, not against taste.

Autoduck as an alternative to sidechain compression: rather than a compressor, draw
the duck curve directly — 1/4 sync, −24 dB depth, dip shape. A drawn curve is
deterministic and shapeable in ways a detector's envelope is not.

### 8.1 A whole arrangement from bus moves alone

Automation is not only decoration on top of an arrangement — it can *be* the
arrangement. One unchanging loop at 140 BPM, routed to four buses (drums: kick /
clap / hats; music: bass / arp / pad; reverb: the wash; delay: the echo), produces a
full intro → grow → build → drop → break → outro structure with **no change to a
single note**: `[measured]`

| Section | The only thing that moves |
|---|---|
| Grow | music-bus low-pass opens 200 Hz → 6 kHz over 2 bars |
| Build | music-bus high-pass rises to 1.5 kHz **and** reverb return lifts +13 dB — the lows drop out, the wash swells |
| Drop | both filters reset; music bus ducked 9 dB from the kick, recovering in 214 ms; one delay throw at a dotted eighth (321 ms) |
| Break | drum-bus high-pass climbs 120 Hz → 900 Hz, then off — the kick *leaves* without muting anything |
| Outro | music-bus low-pass closes 6 kHz → 200 Hz (−3 dB point at 338 Hz); highs fade, bass and kick remain |

Both time values are grid values again: 214 ms is an eighth note at 140 BPM, 321 ms
a dotted eighth. Same rule as §1 — recompute, don't copy.

Why this matters beyond the trick: **it separates arrangement from composition.**
The material stays fixed and only mixer state moves. For generative or live use that
is the cheaper and safer axis — a parameter move cannot produce a wrong note, a
truncated tail, or a seam, and a section can be rewritten without regenerating any
musical content.

---

## 9. Arrangement {#arrangement}

### 9.1 Structure

A DJ-friendly skeleton, with sections landing on 16- and 32-bar boundaries:

```
INTRO 16 bars    kick + hats only — let the DJ mix in
GROOVE           bass and percussion enter
UP               build: filters open, noise rises, kick may drop out
DROP   32 bars   full energy, crash on entry
BREAK            kick and clap out; ride, percs, atmosphere
UP               second build, usually shorter
DROP 2           variation, not repetition
OUTRO            strip back to kick + hats for the next DJ
```

### 9.2 The governing rule

**Reset the ear every 16 bars.** Something must change on each 16-bar boundary — an
element enters or leaves, a filter opens, a variation appears. Attention decays on
roughly that cycle, and a drop that sounds identical for 32 bars stops functioning
as a drop.

### 9.3 Section craft

- **Intro:** restraint is functional, not stylistic — it exists so the track can be
  beat-matched.
- **Build:** add movement, not sounds. Filter sweeps, velocity ramps, risers,
  snare rolls. Pulling the kick out lets the loop float and makes the return land.
- **Drop:** vary it internally — polyrhythms, automation, percussion changes.
- **Outro:** mirror the intro. Descending pitch (tom fills walking down) and
  thinning texture signal the end and hand the mix cleanly to the next track.

---

## 10. Mix and master targets {#mix}

### 10.1 Mix

1. **Gain stage first.** Every channel to around −10 dBFS before any processing.
2. **High-pass everything that isn't kick or bass.** Only those two are allowed below
   100 Hz; everything else gets a high-pass at ~150 Hz with a 24 dB/oct slope.
   This one move resolves most low-mid congestion.
3. **Duck the reverb return from the kick** (−8.5 dB, 160 ms release), not only the
   bass. Keeps the space without smearing the transient.
4. **Target around −6 dBFS peaks and −18 LUFS** before mastering — leave the limiter
   something to work with.

### 10.2 Master

| Parameter | Value |
|---|---|
| Ceiling | −1.0 dBTP |
| Limiter gain reduction | ~4 dB |
| Integrated loudness | −8 LUFS (club target) |

**dB and LUFS measure different things, and conflating them costs loudness.** dB
(peak / dBTP) is how high the signal gets at any instant. LUFS is how loud it *feels*
averaged over time, per ITU-R BS.1770 / EBU R128, where 1 LU = 1 dB. Two masters can
peak identically and still differ by more than 10 LUFS — which is why peak metering
alone tells you nothing about perceived loudness.

Choose the target by destination, because platforms normalize on playback:

| Destination | Integrated target | Peak |
|---|---|---|
| Club / DJ playback | −8 LUFS | −1.0 dBTP |
| Spotify (normal), SoundCloud | −14 LUFS | below −1 dBTP |
| Spotify "loud" / "quiet" settings | −11 / −19 LUFS | — |
| EBU R128 broadcast | −23 LUFS | — |
| Apple, YouTube, Tidal, Amazon, Deezer | no published music figure | — |

Mastering a streaming release to −8 LUFS buys nothing but distortion: the platform
turns it down to −14 anyway, and you arrive quieter *and* more squashed than a
master made for the target. Chase a master that sounds good, not a number.

*Platform figures checked 11 Oct 2026; these policies change, so verify before
relying on them.*

**In this engine you can set the ceiling but not read the loudness.** Top-level
`ceilingDbtp` (−9..0) sets the true-peak ceiling of the finished master; omit it
and the master soft-clips to wherever it lands, near −3 dBFS, which is not a
delivery spec. There is no loudness readout, so the LUFS targets above are
something to *compose toward* — arrangement density, how hard the bus is driven,
how much the limiter is asked to do — not a number you can check and correct.

Use true peak, not sample peak, as the ceiling: a render can sit at −3.0 dBFS by
sample and still reach −2.2 dBTP between samples, and it is the inter-sample
value that clips a consumer decoder.

### 10.3 Delivery

MP3 is lossy perceptual coding: a masking model keeps what is audible and discards
masked content permanently — at 128 kbps, the large majority of the data. Master
from WAV, and if you must check codec damage, listen to the top end and to reverb
tails, which is where it shows first.

---

## 11. Quick reference {#quickref}

```
KICK        sine ~50 Hz; pitch 150->50 Hz over 50 ms; attack 0.8 ms
            hold 25 ms / decay 100 ms  [techno]
            decay 550 ms               [808]
            click: HP 2.5 kHz, 30 ms, -16 dB under
            layers overlap ~7 ms (never gap)
            tune body to the bass root; then check polarity
            EQ: -4 dB@320, +3 dB@4.5k, +2.5 dB shelf@60

LOW END     kick owns sub; carve bass -14 dB Q1.4 at kick fundamental
            sidechain: 1 ms attack, 90 ms release, 6-8 dB
            mono below 120 Hz
            saturate for speakers that can't reproduce the fundamental

GROOVE      off-beat = steps 3, 7, 11, 15
            ghost notes velocity 48-60
            flam 13 ms = width
            open hat tail = one 1/16
            3-over-4 realigns every 3 bars

HARMONY     A minor; Am-F-C-G or Am-Dm-E-Am
            harmonic minor: G -> G#, v -> V (E major)
            deceptive: E major -> F
            melody: one peak, in bar 3

COMPRESS    drums: attack 10-30 ms, release = one 1/16
            parallel: 20:1, 0.5 ms, blend 35%
            always compare level-matched
            this engine: amounts 0-10, not threshold/ratio
              squash = fast+aggressive   smooth = slow leveling
              glue = mix bus             punch = add transient
              pump + pumpRelease (BEATS) = ducking

EQ          this engine: bell {freq, gain, q} and shelf {mode, freq, gain}
            chained on a bus; the 3-band "eq" cannot target a frequency

AUTOMATE    (parameter, start, end, bars, curve)
            1 bar = groove; 4 bars = build
            bus moves alone can carry a whole arrangement:
              grow = LP opens / build = HP up + reverb send up
              break = HP the drum bus / outro = LP closes

ARRANGE     16-bar intro, 32-bar drop, reset the ear every 16 bars

MIX         stage -10 dBFS; HP everything but kick/bass at 150 Hz 24 dB/oct
            pre-master -6 dBFS / -18 LUFS
            master -1 dBTP ceiling, -8 LUFS club / -14 LUFS streaming
            dB = peak, LUFS = felt loudness; they are not interchangeable
            this engine: "ceilingDbtp" sets the true-peak ceiling;
              there is no loudness readout, so compose toward the
              LUFS target rather than measuring against it
```

---

## Provenance {#provenance}

Synthesized from a body of short-form instructional material on electronic music
production — 64 lessons across 17 series, covering kick synthesis, compression,
low-end management, synthesis fundamentals, MIDI arrangement, music theory, FX
automation, arrangement and mastering. Values marked `[measured]` come from
level-matched demonstrations shown in that material.

*Working draft under test. Source attribution is tracked separately and will be
restored before this document is treated as published work.*

The material is techno-weighted and reflects one practitioner's conventions. It is
offered here as craft defaults, not as acoustic law. Where this guide and a specific
instruction disagree, the instruction wins.


===============================================================================
PART 3 OF 4 — GENRE: ELECTRONIC MUSIC GENRES (ADVISORY)
Standalone file: electronic-music-genres.md
===============================================================================

# Electronic Music Genres

> **Third of four.** The Beat Lab score guide is authoritative on *syntax* — what
> fields exist, what compiles, and how to author instruments (`ex_`) and drum
> voices (`exd_`) from oscillators up. `electronic-music-principles.md` is
> advisory on *sound* — kick synthesis, low end, compression, mix targets. This
> one is advisory on *genre* — what a style has to get right to be recognisable.
> `electronic-music-composition.md` is advisory on *composition* — motif,
> development, form, and why one event follows another.
> Where any two disagree about what is *possible*, the score guide wins. None of
> them overrides an explicit user instruction.

## How to use this — read this part first {#how-to-use}

**This document deliberately does not tell you which sounds to use.** It gives,
per genre, the small number of things that must be true, and leaves everything
else to you. That is not an omission:

- **Name no patch, build the sound.** The score guide's workflow is to read the
  nearest factory DNA as *reference*, then author an `ex_` or `exd_` voice and
  change it on purpose. A genre entry here tells you what the sound must *do*
  — "plucked and pitched, sliding up into each downbeat", "clipped, mono,
  brutal" — so you can synthesise toward that target. Picking a factory patch
  because a document named it is how every track in a genre ends up identical.
- **Tempo is a range because the sources disagree.** Where this says
  `110–128 · centre 125 · 19 sources`, nineteen tutorials were examined and they
  chose values across that whole span. Treat the range as the genre's real
  freedom and the centre as a default, not a rule.
- **Two or three constraints, then invent.** A genre is defined by a handful of
  invariants — usually something about the groove, and which element is allowed
  to be the protagonist. Satisfy those and the track will read as the genre no
  matter how unfamiliar the individual sounds are. That is the whole point: the
  constraints are what let you be strange safely.
- **`≠` lines are confusion guards.** Several genres share a tempo and differ by
  one decision. Those lines name the decision.

**What a genre entry does not constrain**, unless it says so: the melody, the
chord progression, the specific timbres, the instrument count, the arrangement
length, or whether you honour the convention at all. Deliberate departure is a
musical choice; accidental sameness is not.

---

## The shared form {#form}

Nearly every genre below is built on one structure. It is worth knowing because
it is *assembly order*, not content — it constrains nothing about how a track
sounds.

**Build the loudest section first.** Across the corpus the order is: the drop's
drums → bass → chords/pads → leads → ear candy and FX; *then* the intro and
build-up, assembled by subtracting and filtering what already exists; *then* the
breakdown and second section, made by varying the first. Writing front-to-back
tends to invent intro material that never pays off.

**Sixteen bars is the unit.** Elements enter on 8- or 16-bar boundaries, never
mid-phrase. A main section is typically two 16-bar halves, and **the second half
adds** rather than replaces — one more percussion layer, a counter-melody, an
answering voice. `[291 of 303 sources]` This is the most universal practice
observed, more consistent than sidechaining. Two identical halves read as
unfinished.

**Section markers.** A cymbal on the downbeat of each 8-bar phrase is the
default `[24 sources say 8 bars; 3 say 4; 1 says 16]`. Risers into a section,
falls out of one, and a short noise gesture whenever a new element enters.

**The breakdown is defined by the absence of ducking.** Same material, no
kick, no duck. That contrast *is* the section.

### Six ways to make a repeated part survive 32 bars {#movement}

Genres differ in which of these they favour; all are cheaper than new material,
and all are parameter movement rather than notes:

1. **A filter sweep across the whole section** — the most common by far.
2. **Velocity driving the filter** — write accents, and the accents open the
   filter. Turns a flat 16th pattern into a performance.
3. **Pitch glide or bend** — on a bass or lead. Some genres (drum & bass, phonk)
   use this *instead* of filter movement.
4. **A gate locked to the tempo** — or to triplets, for a cross-rhythm.
5. **A volume shape per bar** — this is what makes big chord stacks breathe.
6. **Automating a send** — delay or reverb amount as an arrangement curve.

### The low end, which every genre agrees on {#low-end}

- **One element per band.** The split between the main bass and the sub sits
  near **60–70 Hz**: high-pass the bass there and let the sub own below it.
- **Mono below ~200 Hz.** Width down there costs rather than pays.
- **Duck depth is a per-element decision, not a global setting** — and this is
  the single most consequential mix choice in these styles. Three tiers recur:
  **deep** for bass and sub (they must vacate completely); **shallow** for
  chords, pianos and pads (they should stay present and merely breathe); and
  **barely anything** for a fast lead, which a full duck would erase. Using one
  depth everywhere is the commonest way a mix in these genres goes flat.
  One source states the reasoning for the shallow case exactly: *"I don't want
  the kick to duck so much of the piano… a really minimal sidechain effect keeps
  the piano prominent."*
- **Prefer sends to inserts** for reverb and delay on ducked material, or the
  duck eats the tail and the space disappears.

Nothing in the corpus ever changes key or tempo mid-track. All variation is by
element, register, filter and rhythm.

---

# HOUSE {#house}

The family the others borrow from. Four-on-the-floor, 110–128, minor, swung.
**What distinguishes a house sub-genre is almost never the drums — it is which
element is allowed to be the protagonist, and how hard the kick ducks the rest.**

### House {#house-core}
`125` · minor · **1 source** · the baseline the rest are variations on.
**Groove** — kick on every beat, clap on the backbeat, open hat off the beat,
closed hats as the pulse, shaker and percussion for texture. Swing on.
**Feel** — plain, functional, warm.

### Deep house {#deep-house}
`110–128` · centre **125** · minor · **19 sources** — the best-attested genre here.
**Groove** — **a soft kick, never punchy**; this single choice separates it from
tech house more than tempo does. Claps often held back to the ninth bar. Two
bass parts. Percussion deliberately lazy and behind the beat.
**Carries it** — **the chords**, with the root doubled an octave down for weight.
**Feel** — warm, unhurried, late-night, vocal-led, spacious.
**≠ tech house** — same tempo; that one has a hard kick and promotes the hats.

### Tech house {#tech-house}
`120–128` · centre **126** · minor · **13 sources**
**Groove** — **swing is the genre**, and it goes in before any melodic part:
*"if we increase the swing we get that perfect tech house groove."* Hats in
several layers including a quiet "filler" layer. A rolling, repetitive bass whose
**pitch bends** rather than sweeps.
**Carries it** — the hi-hat groove, plus **ear candy as a requirement**: many
small odd sounds, each panned differently, all sharing one delay return.
*"Tech house uses a lot of ear candy to keep the listener hooked."*
**Feel** — dry, bouncy, percussive, witty.

### Bigroom house {#bigroom-house}
`128` (all nine sources agree) · minor · **9 sources**
**Groove** — deliberately sparse: kick and clap and very little else, plus toms
and sweep transitions. A shouted vocal used as a structural marker.
**Carries it** — one very short melody, made enormous.
**Feel** — blunt, stadium-sized, knowingly simple. The restraint is the craft:
few elements, each maximal.

### Slap house {#slap-house}
`124–128` · centre **126** · minor · **7 sources**
**Groove** — **the bass slides up into each downbeat.** Five of seven sources
describe producing this by reversing the note's attack; the gesture, not the
method, is the genre. Claps a quarter of the way into the section.
**Carries it** — the bass.
**Feel** — glossy, bouncy, radio-ready, vocal-forward.

### Bass house {#bass-house}
`100–128` · centre **128** (dark variants at 100–115) · minor · **6 sources**
**Groove** — **the bass is the lead instrument and plays the melody**; drums stay
out of its way. Often three bass voices, each EQ'd to own a different band.
**Carries it** — the bass, and the vocal: *"vocals take a main part"* — one
phrase, three distinct processings, used at different points.
**Feel** — aggressive, metallic, dirty, playful.

### Future house {#future-house}
`116–128` · centre **128** · **6 sources**
**Groove** — **the melody is written with uneven note lengths and pitch glides**:
*"make sure to use notes with different lengths and pitch bends."* That rhythmic
irregularity is the hook, not the timbre.
**Carries it** — a lead with a hard plucked transient.
**Feel** — rubbery, bright, clipped, bouncy.

### Afro house {#afro-house}
`120` (all five agree) · minor · **5 sources**
**Groove** — **the claps come off the four-on-the-floor grid.** Stated outright:
*"instead of putting them on the four-on-the-floor groove, place them like this
to create that afro house groove."* Two separate percussion passes. Chords played
slightly off the beat for a hand-played feel.
**Carries it** — the percussion ensemble, with soft piano underneath.
**Feel** — soft, mellow, natural, unhurried. *"Afro house is very mellow."*
**If it feels busy** — halve the speed of the chord progression rather than
thinning the percussion.

### Melodic house {#melodic-house}
`120–128` · centre **126** · minor · **5 sources**
**Groove** — rolling bass; the arpeggio gets the **lightest** duck of anything,
because a deep one *"won't give that crispy sound."*
**Carries it** — an arpeggio and a piano in dialogue.
**Feel** — euphoric, wide, driving but pretty.

### Lo-fi house {#lo-fi-house}
`120–122` · minor · **4 sources**
**Groove** — everything except the kick is colour-degraded *as a group*; the kick
is degraded separately. Degradation is an instrument here, not a mix fault.
**Carries it** — damaged piano chords; a spoken-word vocal as texture.
**Feel** — dusty, nostalgic, imperfect, hazy.

### Minimal house {#minimal-house}
`122–128` · centre **124** · minor · **4 sources**
**Groove** — few elements, so **performance carries it**: randomised velocities
across the percussion, a mono kick with its lows dampened. Everything but the
kick summed to one bus with its unneeded lows removed, for clarity.
**Carries it** — the groove itself, with one recurring melodic motif.
**Feel** — dry, spacious, hypnotic, restrained.

### Progressive house {#progressive-house}
`128` · minor · **3 sources**
**Groove** — long phrases; the lead withheld until late.
**Feel** — patient, widescreen, building.

### Tribal house {#tribal-house}
`126` · minor · **2 sources**
**Groove** — **drums are the main element.** One source switches the percussion
to **triplets in the main section only**, keeping it straight elsewhere, so the
drop is marked by a metric change. Percussion panned hard apart.
**Carries it** — percussion, plus an acoustic melody — guitar or flute.
**Feel** — earthy, driving, ritual.

### Stutter house {#stutter-house} · also called euphoric house
`128` · minor · **2 sources**
**Groove** — **one tempo-locked gate applied to the lead *and* the chords *and*
the pads**, so the whole track breathes as a single organism.
**Feel** — euphoric, chopped, pulsing.

### Classic house {#classic-house}
`122–126` · minor · **2 sources**
**Groove** — **the bass is a played bass guitar, not a synth**: *"in most classic
house songs bass guitars are used instead of synthesized basses."* Organ and
piano stabs above.
**Feel** — raw, warm, human, early-90s.

### Disco house {#disco-house}
`126` · minor · **2 sources**
**Groove** — **build your own sample rather than looping a record**: write an
8-bar section, colour it, print it, pitch it down, chop it up. Note that pitching
the sample transposes the track with it.
**Carries it** — the chopped loop.
**Feel** — filtered, euphoric, retro, looped.

### Soulful house {#soulful-house}
`124–126` · minor · **2 sources**
**Carries it** — soft electric piano chords: *"the backbone of soulful house."*
**Order matters** — *"it's easier to work when you have a vocal before laying
down the chords."* Find the voice first, then harmonise to it.
**Feel** — warm, gospel-tinged, generous.

### Ambient house {#ambient-house}
`120–126` · minor · **2 sources**
**Groove** — pads first, kick later; **delay does the work reverb usually does**.
**Feel** — washed, weightless, slow-moving.

### Speed house {#speed-house}
`150` · minor · **2 sources**
**Groove** — a bass-house bass at 150, on the root. The corpus warns:
*"you can use additional loops but don't overcrowd it."*
**Feel** — frantic, hard, rave-leaning.
**Worth stealing** — one source gives the intro a completely different mood
(soft piano) from the drop, and bridges the two with a single vocal gesture.

### Piano house {#piano-house}
`126` · minor · **1 source**
**Carries it** — a bright piano, which gets **the lightest duck in the track** so
it stays prominent rather than pumping. Two answering bell lines: one on the
chords' top notes, one on their roots.
**Feel** — euphoric, bright, old-rave.

### Tropical house {#tropical-house}
`115` · **G major** — one of very few major keys in the corpus · **1 source**
**Carries it** — an acoustic guitar melody; a saxophone takes over in the second
half.
**Feel** — breezy, warm, major-key, unhurried.

### Organic house {#organic-house}
`~124` · minor · **1 source**
**Groove** — field recordings used as elements; a 16th-note plucked bed; "filler"
drums added specifically to defeat repetition, plus a mid-section fill.
**Feel** — natural, textured, patient.

### Ethnic house {#ethnic-house}
`120` · minor · **1 source**
**Groove** — claps on alternate beats, rolling closed hats, rides on every half
beat.
**Carries it** — a non-Western plucked instrument, with the melody built from
**the chords' top notes and root notes**.
**Feel** — modal, hypnotic, warm.

### Italo house {#italo-house}
`120` · minor · **1 source**
**Groove** — a strict 4-bar entry ladder. **The melody walks up and down the
scale stepwise in a groovy rhythm** rather than leaping.
**Carries it** — funky organ pads.
**Feel** — naive, sunny, retro-European.

### Pop house {#pop-house}
`120` · minor · **1 source**
**Groove** — *"the main element of pop house is vocals."* Written vocal-first,
with a mini build-up inside the intro.
**Feel** — clean, bright, radio.

### Brazilian bass {#brazilian-bass}
`128` · minor · **1 source**
**Carries it** — the bass, bouncy and crunchy, with the same slide-up-into-the-
downbeat gesture as slap house.
**Feel** — swaggering, minimal, bass-forward.

### Phonk house {#phonk-house}
`110` · minor · **1 source**
**Carries it** — a cowbell melody over house drums.
**Feel** — sleazy, swung, lo-fi.

### Melbourne bounce {#melbourne-bounce}
`128` · minor · **1 source**
**Groove** — an off-beat bass that is **deliberately not ducked**: *"I didn't
sidechain it because it doesn't interfere with the kick."* A useful reminder that
ducking is for overlap, not ritual.
**Feel** — bouncy, blunt, festival.

### Also in this family
**Summer house** `124–126` · bright piano house, roots doubled down an octave ·
**2 sources**. **Dark club banger** `115` · slow, menacing, bass-house-leaning ·
**1 source**. **EDM pop** `90` · festival production at half-time pop tempo ·
**1 source**.

---

# TECHNO {#techno}

115–150, minor, and the family with the most transferable technique. Where house
promotes a melodic element, techno promotes **the low end and the groove**, and
builds its interest from parameter movement rather than parts.

### Techno {#techno-core}
`126–134` · centre **126** · minor · **6 sources**
**Groove** — **the low end is two parts, not one.** A continuous sub-bed derived
from the kick's own tail, ducked by the very kick that produced it, so the kick
punches through something otherwise unbroken; and above it a **mono mid-bass with
its lows removed**, because the kick and the bed already own them. *"Techno
usually has two types of bass."* Strict 8-bar entry ladder. A second, much
quieter hat layer for character. Reverb-drenched clap "fills" that blend rather
than read as a backbeat.
**Carries it** — **two leads answering each other**, never one line.
**Feel** — relentless, mechanical, dark, physical.
**Note on ducking** — techno often locks the duck to the *tempo* rather than to
the kick signal, for a stated reason: the long kick tail would otherwise
over-compress the bass. The tradeoff is that a tempo-locked duck keeps pumping
where there is no kick, so it has to be switched off by hand in quiet sections.

### Acid techno {#acid-techno}
`134–150` · centre **140** · minor · **5 sources**
**Carries it** — a single resonant sliding line, and the corpus gives three rules
for writing one: **move in octave jumps** (*"the secret to a great acid bassline
is to do octave jumps"*); **link note velocity to the filter** so the accent
pattern *is* the filter pattern; then **sweep the cutoff across the section** on
top of that.
**Feel** — squelchy, liquid, hypnotic, rave.

### Melodic techno {#melodic-techno}
`125–132` · centre **126** · minor · **5 sources**
**Groove** — *"melodic techno uses a lot of different sounds instead of one lead
melody — create around **four or five call-and-response melodies** using
different sounds."* Not a lead with backing: a conversation in which no voice
dominates.
**Feel** — cinematic, melancholy, wide, patient.
**≠ minimal techno** — five answering voices, against one idea opened by filter.

### Minimal techno {#minimal-techno}
`124–126` · centre **125** · minor · **4 sources**
**Groove** — one idea, opened by a filter across 32 bars. Movement comes from
automation, not from new notes. Percussion velocity varied deliberately.
**Feel** — hypnotic, dry, patient, spacious.

### Dub techno {#dub-techno}
`115–120` · centre **120** · minor · **3 sources**
**Groove** — *"dub techno uses a lot of different types of delays, so change the
delay type on each element."* Effects *are* the composition. Reverb is wet-only
with its decay shortened so it only just overlaps the next hit. **Foley** —
water, footsteps — used as atmosphere: *"to create a great dub techno
atmosphere, use any kind of Foley sound."*
**Carries it** — chord stabs, built from several voices, with **a different
filter value on each hit** so no two chords feel the same.
**Feel** — submerged, vast, grey, slow.

### Hypnotic techno {#hypnotic-techno}
`128–140` · centre **128** · minor · **3 sources**
**Groove** — the thesis is one sentence: *"since this is hypnotic techno and **we
need all the elements to move**, we'll automate the pitch of the hi-hats."*
Everything is modulated, including things normally left static.
**Carries it** — a **one-note** lead: hold the root, let velocity drive the
filter, and play it rather than draw it. The melody is the performance.
**Feel** — circular, immersive, trance-like.

### Industrial techno {#industrial-techno}
`140–150` · centre **150** · minor · **3 sources**
**Groove** — the kick is processed to destruction and in one source **replaces
the bass entirely**. Percussion deliberately ruined, then pitched up to sound
metallic. **Dissonance built from minor seconds and bare dyads**, not from
altered chords.
**Feel** — brutal, metallic, airless.

### Tribal techno {#tribal-techno}
`134–140` · centre **140** · minor · **3 sources**
**Groove** — a large percussion ensemble plus ethnic loops; cymbals every 16 bars
here rather than 8.
**Worth stealing** — the build-up changes mood completely, to soft recorded piano
chords, before returning.
**Feel** — ritual, driving, physical.

### Dark techno {#dark-techno}
`126–140` · centre **133** · **harmonic minor** · **2 sources**
**Colour** — stated plainly: *"when making dark music it's ideal to use harmonic
minor scales."*
**Groove** — three bass voices. **Distort the reverb itself** — reverb as a sound
source rather than a space.
**Feel** — menacing, filmic, heavy.

### Deep techno {#deep-techno}
`126` · minor · **2 sources**
**Groove** — quiet and reverb-dependent; claps only in the second half; pads only
in the last 16 bars. The lead is introduced by a filter opening across 16 bars.
**Feel** — submerged, nocturnal, restrained.

### Ambient techno {#ambient-techno}
`115–120` · minor · **2 sources**
**Groove** — kick demoted, pads promoted, no lead at all. Long attacks.
**Feel** — weightless, cold, spacious.

### Hard techno {#hard-techno}
`150` · minor · **2 sources** — the industrial kick treatment at speed, with the
sub-bed doing all the low-end work. **Feel** — punishing, fast, raw.

### Hardgroove techno {#hardgroove-techno}
`140–145` · minor · **2 sources** — rolling percussion and a groove-first bed
rather than a melodic top. **Feel** — rolling, tribal, relentless.

### Driving techno {#driving-techno} · also called peak time
`128–130` · minor · **2 sources**
**Carries it** — *"as our main driving element, we need some driving and powerful
arps."* Arpeggios, not a lead, propel the track.
**Feel** — propulsive, bright-dark, peak-time.

### The smaller techno genres
**90s techno** `126` — organ and synth stabs as period markers; raw, rave,
nostalgic · **1 source**. **Progressive techno** `126` — long arcs, lead withheld
very late · **1 source**. **Underground techno** `140` — raw and mid-focused,
minimal atmosphere · **1 source**. **Organic techno** `122` — acoustic percussion
and field recordings over a soft kick · **1 source**. **Ethnic techno** `120` —
non-Western percussion and melodic instrument on the techno frame · **2 sources**.
**Afro tech** `120` — afro house's off-grid claps with a techno low end ·
**1 source**. **Dreamy techno** `120` — pads and vocals placed *before* the bass,
which tells you where the weight sits · **1 source**. **Bigroom techno** `106–128`
— bigroom architecture, techno kick · **2 sources**. **Techno metal** — distorted
guitar material on the techno frame · **1 source, no captions, treat as a
sketch**. **Liminal techno** — the creator's own coinage · **1 source**.

---

# TRANCE AND PSY {#trance}

128–150, minor without exception, and **138 is the single most common tempo in
the whole corpus** (15 sources across six sub-genres). Long sections: *"usually a
trance track has long drops like 32 bars."* Two bass parts are standard — one
supplying 16th-note motion, one supplying weight.

### Psytrance {#psytrance}
`138–145` · centre **138** · minor, and **harmonic minor** for dark material ·
**6 sources**
**Groove** — a rolling 16th bass line that **moves by semitones rather than scale
steps**: *"use semitones when doing note changes to get that dark, trance-like
vibe."* The same applies to the lead. Chromatic neighbour-motion is the signature.
**Colour** — *"the trick to making these kinds of dark melodies is to use
harmonic minor scales."* Dark pads voiced in **adjacent semitones** rather than
thirds.
**Feel** — dark, propulsive, psychedelic, relentless.
**Worth stealing** — two sources re-time the *entire* second section into
triplets as the variation, instead of swapping sounds.

### Uplifting trance {#uplifting-trance}
`132–138` · centre **138** · minor · **5 sources**
**Groove** — **starts from the melody, before any drum.** Three of five sources
open with the tune and bring drums in to support it. High pads on the chords'
root notes create the suspense.
**Carries it** — the melody, unambiguously.
**Feel** — euphoric, emotional, soaring — major-feeling despite being minor.

### Trance {#trance-core}
`138–140` · minor · **4 sources** — the family baseline.
**Groove** — **two claps on purpose**: one reverberant, one snappy, with the
reverberant one printed so its tail can't smear into the next hit. Swing noted
explicitly. A piano doubling the chords with added notes.
**Feel** — hypnotic, widescreen, driving.

### Progressive trance {#progressive-trance}
`132–138` · centre **134** · minor · **3 sources**
**Groove** — slower and restrained; *"the main element in this drop will be
percussion"* — the only entry in the family where percussion leads. The big lead
is withheld until very late.
**Feel** — patient, hypnotic, deep.

### Trance bigroom {#trance-bigroom}
`138` · minor · **3 sources** — bigroom's drop architecture with trance's melodic
content. Swing added at the tempo stage. Transition gestures treated as structural
punctuation, placed whenever a new part enters.

### The smaller trance genres
**Tech trance** `140` — techno's weight and restraint with the trance 16th bass ·
**2 sources**. **Acid trance** `150` — the resonant sliding line promoted to lead ·
**1 source**. **Classic trance** `138` — the 90s template: stabbed chords, a
simple diatonic tune, much less layering · **1 source**. **Dream trance** `140` —
a piano hook as the lead, soft pads, minimal percussion; wistful · **1 source**.
**Melodic trance** `128` — the uplifting recipe with the lead thinned and the
piano promoted · **1 source**. **Electro trance** `134` — trance form with an
electro-house bass timbre · **1 source**. **Techno trance** `140` — techno kick
and groove, trance melodic content and section lengths · **1 source**.
**Psy techno** `128` — psytrance's semitone motion at techno density ·
**1 source**.

---

# BASS, BREAKS AND GLOBAL GROOVES {#bass-breaks}

**These are the genres that are not four-on-the-floor, and that changes
everything.** In house, every sub-genre shares a kick pattern and differs in its
lead. Here **the kick pattern *is* the identity** — get it wrong and no amount of
correct instrumentation rescues it. Ducking also matters less, because a sparse
kick leaves less overlap to clear. And two genres have no drop at all.

### Drum & bass {#drum-and-bass}
`165–175` · centre **170** · minor · **5 sources**
**Groove** — **snare on every other beat**, plus filler and ghost snares to make
the pattern breathe. Snares chosen for a noise tail. All drums except the kick
summed to one bus and their lows removed as a group.
**Carries it** — **the bass, written as a dialogue**: *"two bass patterns, the
call and the response, with a lot of different-sounding basses"* — and a
deliberate **silence between them** to hand over. Movement comes from **pitch
bend, not filter**.
**Feel** — rolling, cavernous, urgent.

### Future bass {#future-bass}
`145–150` · centre **150**, felt half-time · minor · **4 sources**
**Carries it** — one chord stack, and **a volume shape per bar is its signature**:
the chords breathe in and out rather than sustaining. "Filler" chords fill the
gaps between.
**Feel** — lush, wobbling, emotional, candy-bright.

### Future bounce {#future-bounce}
`126–128` · **3 sources**
**Groove** — *"a little tip when creating a bass for future bounce is taking some
notes an octave up — it'll add an awesome bouncy feeling."* Octave displacement
of an existing line, not a new rhythm. Swing on.
**Feel** — rubbery, bright, playful.

### Trap {#trap}
`140`, or **`70` felt half-time** · minor, and **Phrygian** for the phonk-leaning
variant · **3 sources**
**Groove** — **randomise the hi-hat velocities**: *"to make them sound a bit
authentic."* The low bass is ducked *by* the kick, not the reverse. Keep it simple.
**Feel** — spacious, heavy, sparse, patient.
**Worth stealing** — the outro is made by halving the whole track's note rate.

### Jersey club {#jersey-club}
`135` · minor · **1 source** — the clearest "the kick pattern is the genre" case.
**Groove** — *"make a four-to-the-floor kick pattern, and **move the fourth kick
backwards**, and add another."* A bed-squeak sample as the signature texture.
Vocal chops with **hard cuts**, no crossfades.
**Carries it** — chopped vocal, answered by **pads that are the chords cut in
half**, so they call and respond with the kicks.
**Feel** — bouncy, cheeky, club.

### UK garage {#uk-garage}
`134` · minor · **1 source**
**Groove** — *"increase the swing of these drums to give them that classic garage
groove."* Three bass voices, one of them wobbling.
**Feel** — swung, soulful, nocturnal.

### Breakcore {#breakcore}
`175` · minor · **1 source**
**Groove** — a chopped-up classic break, irregular rather than gridded.
**The contrast is the genre** — very fast drums under slow, sweet harmony.
**Feel** — chaotic over gentle.

### Moombahton {#moombahton}
`100–115` · centre **110** · minor · **4 sources**
**Groove** — **percussion creates the groove**, before any other element. The
bass **follows the kick's rhythm with free pitch** — rhythmically locked,
melodically loose.
**Carries it** — a wind instrument: flute or trumpet.
**Feel** — heavy, sunny, swaggering.
**If the chords feel wrong** — double the roots an octave down and change their
rhythm, which is what the corpus does.

### Phonk {#phonk}
`120–126` · centre **125** · **Phrygian** — the only family in the corpus built
on it · **3 sources**
**Carries it** — **a cowbell melody**, following the bass's rhythm; doubled an
octave up for the second section.
**Groove** — a sliding bass plus a distorted low bass; the drums themselves
saturated *"to make that phonk punch."*
**Feel** — sleazy, hazy, menacing, swung.

### Afrobeat {#afrobeat}
`95–100` · minor · **2 sources** — **no drop, and no build-up.**
**Form** — verse → pre-chorus → chorus → outro. The corpus switches vocabulary
mid-tutorial to say so. **The kick does not arrive until the chorus**; the verse
runs on rim shots, off-beat snares and percussion.
**Groove** — a played bass guitar, not a synth. **Notes nudged off the grid** for
naturalness. The melody changes between sections rather than repeating.
**Feel** — buoyant, warm, loose, live.
**The most likely way to get this wrong** is to apply the drop grammar to it.

### Reggaeton {#reggaeton}
`~100` · **1 source** — also no drop.
**Groove** — the beat comes from **percussion**, with **the kick low-passed
beneath it** so it supports rather than leads.
**Carries it** — a flute melody, and a vocal **edited to fit the melody** rather
than the reverse.
**Feel** — swung, sultry, percussive.
**Outro** — made by *removing* elements, not adding them.

---

# HARD DANCE {#hard-dance}

128–175. **The dividing line is not tempo — it is that the kick stops being a
drum and becomes the lead instrument.** It is synthesised rather than chosen,
often pitched across the pattern, usually mono and clipped. And a full duck
leaves nothing audible between kicks, so these genres duck shallowly or not at
all.

### Hardstyle {#hardstyle}
`150` · minor · **2 sources**
**Groove** — **the kick is manufactured, then played as a pitched instrument**:
*"an essential part in hardstyle is tuning the kick to different notes."* The
bass follows the kick's pattern rather than its own.
**Worth stealing** — *"we are not going to use the lead for the first drop"* —
the screech lead is withheld and the first section filled with FX instead.
**Feel** — euphoric and brutal at once, anthemic.

### Hard trance {#hard-trance}
`145–150` · minor · **2 sources** — trance's melodic stack at hard-dance tempo,
with two bass parts. **Feel** — driving, euphoric, hard.

### Gabber {#gabber}
`175` · minor · **1 source**
**Groove** — the kick clipped and **made mono**; **kick rolls *are* the groove**,
not a pattern laid over it. Self-described: *"a very simple and minimalistic
genre"* — five drum elements, one bass, two leads.
**Feel** — brutal, minimal, relentless.

### Happy hardcore {#happy-hardcore}
`170` · **B major** — the corpus's clearest major-key statement · **1 source**
**Colour** — *"since we're making a happy song, it's good to work on a major
scale."*
**Groove** — when a second kick is layered for its highs, **the main kick's
transient is removed** so the two attacks don't stack into a click.
**Feel** — giddy, euphoric, nostalgic.

### Hypertechno {#hypertechno}
`150` · minor · **1 source**
**Carries it** — **a piano**, at 150. That combination is the genre.
**Feel** — euphoric, fast, bittersweet.

### Aggrotech {#aggrotech}
`128` — house tempo, the slowest here by a wide margin · minor · **1 source**
**Carries it** — **the vocal**, deliberately destroyed through two distortion
stages in series.
**Feel** — industrial, gothic, mechanical.

### Hard psy {#hard-psy}
`155` · minor · **1 source** — psytrance machinery at hardstyle tempo. The lead
is **a single shot every four bars**, punctuation rather than melody. Strict
8-bar entry ladder. **Feel** — dark, punishing, hypnotic.

### Speedcore {#speedcore}
**1 source** — the reductio: **no bass part at all**, because a second low-passed
kick does that job. Kick on every beat with rolls.
**Worth stealing** — *"I want a complete vibe shift after the drop"*: the break
resolves into slow piano chords. The hardest genre here ends in a ballad.

### Also in this family
**Artcore gabber** `175` — a gabber kick under melodic material · **1 source**.
**Hardbass** `160` — pitched bounce bass, shouted vocal · **1 source, no
captions**. **Techno metal** — see techno.

---

# RETRO AND CHILL {#retro}

90–128, and the family that inverts the house/techno defaults in three ways:
**it is slow** (the only genres below 108); **the snare, not the clap, is the
backbeat**, usually drenched in reverb; and **colour is an element** — tape,
vinyl, bit-reduction applied as deliberate choices rather than polish. It is the
only family where damaging the signal is the point.

### Synthwave {#synthwave}
`90` (three sources independently chose 90) · minor · **4 sources**
**Groove** — **a reverb-heavy snare as the backbeat**, plus ghost snares; the
melody arrives only in the second half.
**Carries it** — three bass layers, which is the real signature: a 16th-note
line, a brighter layer above it, and a stab.
**Feel** — nostalgic, neon, cinematic, patient.

### Darksynth {#darksynth}
`100` · **harmonic minor, diminished, or major bebop** · **2 sources**
**Colour** — the one genre where the scale *is* the lesson: *"some good scales to
make dark songs are diminished, harmonic minor and major bebop."*
**Carries it** — four stacked leads, each given a **slow ±4-semitone pitch
drift** — stated as the trick that makes them *"darker and more dreadful."*
**Groove** — swing on the hats; percussion specifically to defeat repetition.
**Feel** — menacing, filmic, propulsive.

### Synth pop {#synth-pop}
`100` · minor · **2 sources**
**Groove** — built around a vocal **from the first bar**, and **the lead waits for
the vocal to stop** before entering.
**Feel** — bright, 80s, wistful.

### Lo-fi {#lo-fi}
`108–120` · minor and major · **2 sources**
**Groove** — colour first, then the parts. Build-ups are deliberately almost
absent: *"there's not much for a build-up."*
**Remix method** — find an acapella, **read its key and tempo and match the
project to it**, then build underneath.
**Feel** — dusty, intimate, imperfect.

### Vaporwave {#vaporwave}
`90` · minor · **1 source**
**Groove** — the processing *is* the genre. A saxophone in the second half; a
rare explicit 4-bar outro; a filter sweep across the whole master.
**Worth stealing** — a piano doubling **both** the chords and the melody,
*"to add more depth to the sound as a whole."*
**Feel** — hazy, ironic, decayed.

### Italo dance {#italo-dance}
`128` · minor · **1 source**
**Groove** — the corpus's only vocoder build, constructed *before* any other
element. The melody **walks up and down the scale** in a groovy rhythm.
**Feel** — naive, euphoric, European.

### Eurobeat {#eurobeat}
`170` · minor · **1 source**
**Carries it** — *"the most important element is the brass riff."* Everything
else serves it; the bass plays its root notes; the intro is the same riff
simplified.
**Groove** — fills and cymbals **every 4 bars**, twice the usual rate — that is
what makes it feel fast.
**Feel** — breathless, cheesy, relentless.

### Seasonal {#seasonal}
`115–125` · often **major** · **4 sources across families**
Not a sound but a treatment, and there is one real idea in it: **take a thematic
sound and give it a structural job** — a bell used as the fall out of a section,
rather than as decoration. Major keys cluster here.

---

## Provenance {#provenance}

Distilled from the complete "Tutorials" playlist of the YouTube channel **D34N**
— **308 tutorials, about 55 hours**, published roughly 2020–2025, grouped into
the genres above. One producer walking through a complete track per video at a
consistent altitude: tempo, element inventory, build order, section arrangement,
and a processing note per element.

**How it was read, and the limit that matters most.** From the channel's own
English captions (303 of 308 videos have them) plus each video's creator-typed
title, description and chapter list. Tempo and key were extracted mechanically
rather than by eye — **288 videos state a tempo**, 186 declare a key — so the
ranges here are measured, not estimated.

**The videos themselves were not watched.** Captions carry what was *said*; the
piano roll, the plugin windows and every numeric value were *shown*. So this
document is reliable about **what a genre contains, in what order, and what must
be true of its groove**, and carries **no note-level material and no parameter
values** — those were on screen. When a source says "add some EQ to take off the
lows", the frequency is not recoverable here. For numbers, use
`electronic-music-principles.md`, which was read from on-screen slides and is
strong exactly where this is weak.

**Other limits.**
- One practitioner's conventions, and a house/techno-weighted playlist (167 of
  308 videos). Source counts are given per genre precisely so you can weigh them:
  **45 genres rest on a single video** and should be treated as one person's one
  take, not as the genre's definition.
- Genre names are the creator's. Several are his coinages rather than established
  categories.
- Quoted phrases are his words with machine-transcription errors corrected.
- Five videos have no captions and are marked as sketches.

**This document describes conventions, not requirements.** It is strongest used
as a check — "does my track satisfy the two or three things that make this genre
recognisable?" — and weakest used as a specification. Where it and a specific
instruction disagree, the instruction wins.


===============================================================================
PART 4 OF 4 — COMPOSITION: ELECTRONIC MUSIC COMPOSITION & CREATIVE DEVELOPMENT (ADVISORY)
Standalone file: electronic-music-composition.md
===============================================================================

# Electronic Music Composition & Creative Development

> FOURTH BEAT LAB GUIDE: COMPOSITIONAL INTELLIGENCE
> Intended companion to music-guide.txt, electronic-music-principles.txt,
> and electronic-music-genres.txt. This guide answers WHY musical material
> exists, WHAT happens next, and HOW ideas evolve into a coherent piece.
>
> AUTHORITY: music-guide.txt alone defines executable Beat Lab JSON syntax,
> field names, units, supported sounds, transforms, and validation rules.
> The production-principles guide advises sound and mix decisions; the genre
> guide advises stylistic identity. This document advises composition.
> An explicit user's artistic request overrides every default in this guide.
> If a technique cannot be represented faithfully in Beat Lab, translate its
> intention into supported events, patterns, automation, or sound design.
> NEVER invent score fields, instruments, effects, or transform names.
>
> STATUS: practical compositional heuristics, not laws or empirical guarantees.
> Examples are original sketches, not existing songs to copy. The recommendations
> are intentionally genre-flexible, and can be ignored for artistic reasons.

===============================================================================
0. THE PRIME DIRECTIVE: COMPOSE RELATIONSHIPS, NOT INVENTORIES
===============================================================================

A collection of excellent sounds is not necessarily a composition. A composition
makes events feel related across time. One rhythmic accent anticipates another;
a melody returns in an altered form; a quiet interval makes an impact matter;
a bass note changes how a held chord feels; a sound gradually becomes something
else while preserving a recognizable trait.

Do not ask only: "What should I add?" Ask:

  - What is the piece about musically, not verbally?
  - What is its smallest recognizable identity?
  - What is stable enough for the listener to learn?
  - What changes, and why does that change matter?
  - Which voice is the protagonist right now?
  - What does the listener expect at this moment?
  - Should that expectation be confirmed, delayed, redirected, or denied?
  - Could subtraction make the next event more meaningful?

A USEFUL COMPOSITIONAL BALANCE:
  identity + development + contrast + timing + restraint.

None of these must be maximized. A hypnotic piece may rely on minimal contrast;
a chaotic IDM passage may temporarily hide identity; an ambient piece may make
timbre its only evolving voice. Success means purposeful decisions, not a high
score on every dimension.

THREE TIMESCALES must communicate:
  MICRO:  an onset, gap, accent, inflection, or sound transformation.
  MESO:   a phrase, answer, fill, 4- to 16-bar development, or local turn.
  MACRO:  the emotional trajectory, recurring theme, sections, return, ending.

If micro-events are fascinating but no phrase exists, the result is busy.
If phrases are well made but nothing changes at scale, it is an extended loop.
If the form is dramatic but material lacks identity, it is a trailer of effects.

===============================================================================
1. THE COMPOSITIONAL BLUEPRINT (INTERNAL PLAN, NOT JSON)
===============================================================================

Before authoring executable notes, make a short private design plan.
This is a thinking aid. Do not emit blueprint labels as score fields.

  Intent:          one sentence about the listening experience.
  Center:          the thing a listener should recognize after 20 seconds.
  Anchor:          the repeated, trustworthy element (beat, bass, chord, timbre).
  Instability:     the element free to mutate or surprise.
  Motif DNA:       2-6 events or a short rhythm, interval, or timbral gesture.
  Harmonic world:  tonal center, modal/pitch collection, pedal, or deliberate none.
  Rhythmic world:  pulse and subdivision, plus one meaningful source of friction.
  Palette roles:   foreground / response / foundation / atmosphere / punctuation.
  Emotional arc:   3-7 scene words, not merely increasing loudness.
  Transformation:  how at least one idea changes across scenes.
  Return:          when a familiar idea returns and what has changed around it.
  Ending:          resolution, withdrawal, interruption, or purposeful openness.

EXAMPLE BLUEPRINT (inventive jungle/IDM, not a production preset):
  Intent:       warm human swing with flashes of anxiety and immense air.
  Anchor:       a low, elastic two-bar bass gesture.
  Instability:  chopped breaks that interrupt rather than obscure the bass.
  DNA:          three close notes plus one wide upward leap; final beat absent.
  Harmony:      ambiguous minor ninth colors; one brief sharpened seventh.
  Scenes:       curious -> playful -> uneasy -> weightless -> fractured -> tender.
  Return:       original bass gesture heard under altered, spacious chords.
  Ending:       drums vanish, bass completes a previously unfinished answer.

An original track need not use all these slots literally. A single-note drone
can supply a center; a moving spectral texture can serve as a motif.

CONSTRAINTS CREATE CHOICE:
Pick 2-3 productive constraints (for instance, "one main melodic cell," "bass
never hits with the snare," and "only the final section reveals the full chord").
Avoid 15 constraints that turn musical decisions into bureaucracy.

===============================================================================
2. MUSICAL IDENTITY: MAKE A SMALL IDEA WORTH RETURNING TO
===============================================================================

2.1 MOTIF DNA

A motif is shorter than a melody. It may be an interval shape, rhythm, accent,
articulation, texture, or a coordinated event across instruments. Prefer a clear
2- to 6-event seed over a long, shapeless line.

Describe a motif using several independent fingerprints:
  RHYTHM:     onset gaps (e.g., short-short-long-rest).
  CONTOUR:    up, up, down; or level, leap, descent.
  INTERVALS:  neighboring notes versus distinctive leaps.
  REGISTER:   where it lives and how far it spans.
  ACCENT:     which event matters, not only which is loudest.
  TIMBRE:     attack, brightness, noise, decay, pitch movement.
  SPACE:      dry/near versus reverberant/far; narrow versus diffuse.
  NEGATIVE:   the missing beat or deliberately withheld note.

ORIGINAL NOTE CELL (illustrative, not a full JSON score):
  A4 (short) -> C5 (short) -> B4 (longer) -> [rest] -> E5 (brief)
  Intervals: +3, -1, +5 semitones.
  Narrative: rising curiosity, hesitation, then a surprising leap.

Identity can persist if only ONE fingerprint survives a transformation.
A bass may inherit the melody's rhythm without inheriting its pitches;
a snare fill may echo its accent contour; a filtered noise burst may use
its attack-and-rest profile.

2.2 STRONG VERSUS GENERIC MATERIAL

A strong seed often has one memorable asymmetry: a displaced accent, unequal
phrase halves, one leap among steps, an unexpectedly long silence, or a note
whose harmonic meaning changes on repeat. "Strong" does not mean complicated.

Try two alternate seeds; listen imaginatively or render each alone and in its
intended accompaniment. Choose for recognizable character, not note count.
A two-note seed may be stronger than a sixteen-note solo.

2.3 THE RECOGNITION TEST

Could the listener recognize the idea if the instrument, register, or harmony
changed? If not, give the seed a more decisive feature; do not automatically
make it louder or longer.

2.4 THE NEGATIVE MOTIF

A characteristic absence can be as identifiable as a played note. For example,
leave the last eighth of every second bar open, then fill that gap only at a
turning point. The "missing" slot becomes a promise that can be answered.

===============================================================================
3. DEVELOP IDEAS INSTEAD OF ACCUMULATING NEW ONES
===============================================================================

A composition can become complex by exploring ONE idea through many contexts.
Treat addition of a new instrument as only one possible operation.

3.1 TRANSFORMATION FAMILIES

PITCH:
  transpose; invert contour; alter one interval; change register;
  move from scale notes to neighboring chromatic notes; retain a common tone.

RHYTHM:
  displace the whole phrase; shift one accent; truncate; lengthen a final note;
  halve/double the note rate; delete an onset; turn notes into rests.

PHRASE:
  fragment; repeat just the opening; answer the ending; sequence a fragment;
  compress its second half; delay the expected completion.

HARMONY:
  reharmonize the same melody; hold a pedal under changing upper voices;
  keep the chord but change its bass; move one inner voice by a semitone.

TIMBRE:
  transfer the phrase to another sound; change attack before brightness;
  replace pitches with noise while keeping rhythm; diffuse the phrase in echo.

ROLE:
  change lead into countermelody; melody into bass; bass rhythm into hi-hats;
  fill into a call; foreground sound into background memory.

SPACE:
  dry motif -> distant motif -> silent ghost of motif -> dry return.

3.2 FOUR WAYS TO KEEP IDENTITY DURING CHANGE

  A. Keep rhythm, vary pitch.
  B. Keep contour, vary timing.
  C. Keep only the first gesture, invent a new ending.
  D. Keep timbral/accent signature while moving the idea between voices.

Make the changed dimension prominent and the preserved dimension audible.
If both are obscured by the arrangement, the relationship exists on paper only.

3.3 PARALLEL VS. CUMULATIVE VARIATION

PARALLEL: derive alternatives A1, A2, A3 from a fixed seed A0; choose them as
siblings. Good for recognizable periodic returns.

CUMULATIVE: A0 -> A1 -> A2 -> A3, each retaining some changes from the last.
Good for a transformation that ends somewhere surprising but still has ancestry.

COMBINATION: establish A0; evolve through A1-A3; then restore A0 in a new
instrument or harmonic setting. That creates recognition *after* change.

3.4 THE ONE-MEANINGFUL-CHANGE EXERCISE

From a 2-bar seed, compose four 2-bar descendants:
  Version 1: move ONE accent off the beat.
  Version 2: keep Version 1, replace ONE note with a rest.
  Version 3: keep Version 2, move the highest note up a minor third.
  Version 4: keep Version 3, make the answer a different instrument.

Listen at each stage. If Version 2 already says what is needed, stop there.
The purpose is quality of change, not completing every exercise.

3.5 COUNTERFACTUAL TEST

When adding a variation, ask: "If I removed this transformation, what musical
meaning would be lost?" If the answer is "almost none," simplify or replace it.
Not every bar needs a mutation. A stable loop can make later mutation meaningful.

===============================================================================
4. INVENTIVE RHYTHM: MAKE INDEPENDENT TIMES FEEL RELATED
===============================================================================

Rhythmic interest comes from relationships between pulses, onsets, rests,
accents, durations, timbres, and phrase boundaries. Density is only one axis.
Complexity that obscures the underlying pocket may be useful momentarily, but
is not inherently better.

4.1 BUILD A RHYTHMIC HIERARCHY

For most groove-based pieces distinguish:
  PULSE:       the stable reference listeners can locate.
  BACKBONE:    kick/snare or a comparable recurring pattern.
  MOTION:      hats, shakers, arps, ghost subdivisions.
  FRICTION:    syncopations, displaced hits, cross-accents.
  PUNCTUATION: fills, holes, reversals, rare interruptions.

Not every layer should compete to define the beat. A very complex top rhythm
can work over a simple bass anchor; if the drum part is unstable, the bass can
be the stable reference instead. In ambient music the hierarchy may be implied
by event spacing rather than a kick.

4.2 WRITE RESTS FIRST

Choose the beats where NOTHING should interrupt the lead or bass. Design the
remaining percussion around that space. Intentional gaps give syncopation its
meaning; endless sixteenths can flatten every surprise.

EXAMPLE: a 16-step bar (steps 0-15, zero-indexed) with an implied 4/4 pulse.
  Reference quarter-note pulses: 0,4,8,12.
  Bass onsets:                 0,3,7,10,14.
  Important empty slot:       12 (leave the obvious beat open).
  Percussion answer:          12 or 13, only in the fourth repetition.

This is an abstract rhythmic sketch. Choose actual sound names and valid Beat
Lab fields from the score guide.

4.3 ACCENT PATTERNS ARE NOT THE SAME AS NOTE POSITIONS

A run of constant sixteenths becomes a groove when accents express a shape.
Try 3+3+2 accents across eight sixteenths: strong at 0, 3, and 6; repeat over
the next eight. The notes between can be quiet or absent.

Allow three adjacent layers to disagree:
  kick anchors quarters;
  hats emphasize 3+3+2;
  snare suggests a half-time or backbeat frame.

If the cross-accent makes the downbeat ambiguous, decide whether ambiguity is
the musical objective. Restore one shared accent when grounding is needed.

4.4 RHYTHMIC QUESTIONS AND ANSWERS

An answer is meaningful when it relates to the question. Options:
  - repeat its short-long rhythm one subdivision later;
  - answer a busy fill with a single low hit;
  - answer a high register phrase with a low rhythmic echo;
  - fill the question's characteristic silence;
  - end the answer early to create another question.

Do not respond to every call. Occasional unanswered gestures make later
responses more memorable.

4.5 CROSS-RHYTHM, POLYRHYTHM, AND PHASE

Different concepts, different musical results:
  CROSS-ACCENT: a 3-unit accent grouping against regular 4-beat expectations.
  POLYRHYTHM: simultaneous differing beat divisions across the same span,
              e.g., three evenly spaced onsets during two quarter-note beats.
  POLYMETER: distinct metric cycles sharing a pulse, e.g., a 3-beat phrase
             against a 4-beat phrase; their downbeats realign after 12 beats.
  PHASED LOOPS: similar patterns with different lengths, starting phases, or
                subdivisions whose composite changes across time.

An on-grid 3-sixteenth repeating pattern against a 16-sixteenth bar moves its
accent relative to bar lines and returns after 3 bars because lcm(3,16)=48
sixteenths. This is NOT the same as a 3-against-4 subdivision of one beat.

Calculate realignment before using long phase cycles. For integer cycle lengths
measured in the same subdivision, composite cycle = lcm(lengths). If the
composite would exceed the intended section, let the listener experience a
partial drift rather than forcing an artificial "resolution." Note that
re-triggering a pattern each bar may reset its phase: to preserve drift, place
it continuously or explicitly schedule its offsets.

4.6 MICROTIMING WITH A FUNCTION

Differentiate:
  STRUCTURAL syncopation = onsets placed at meaningful subdivisions.
  PERFORMANCE looseness = small timing and velocity deviations around them.

Keep the structural position audible before adding jitter. Humanization does
not automatically create swing, and randomizing each note independently can
destroy a pocket. Prefer correlated decisions: a recurring snare slightly late,
a ghost pickup consistently early, a bass attack leaning into one syncopation.

4.7 BREAKBEAT/JUNGLE-SPECIFIC DEVELOPMENT

For a complex break, preserve a recognizable backbeat reference, then choose
which part to re-cut. Develop via:
  - moving one kick pickup while the snare anchor stays fixed;
  - replacing one expected snare with a ghost + following accent;
  - short snare or hat retriggers that terminate cleanly before a major hit;
  - slicing an existing phrase into a new onset order;
  - one-beat rests that expose the bass;
  - alternating a tight/dry bar with an airy/reverberant response.

Busy fills should usually be periodic events, not the default every bar.
For aggressive experimental work, deliberately break that convention, but
restore a legible relationship somewhere else (bass pulse, motif, harmonic hold).

4.8 RHYTHMIC DEVELOPMENT OVER FOUR PASSES

  Pass 1: define the groove identity, with space.
  Pass 2: change one ghost accent.
  Pass 3: answer a bass phrase with a short percussion fragment.
  Pass 4: remove or interrupt the expected hit before the next section.

The fourth pass need not be loudest. A missing kick can create more anticipation
than another roll.

===============================================================================
5. MELODY AS GESTURE, MEMORY, AND EXPECTATION
===============================================================================

A good melody needs more than legal scale notes. It needs temporal shape,
important notes, boundaries, and a reason to continue.

5.1 INVENT A CONTOUR BEFORE CHOOSING NOTES

Examples:
  arch:         low -> higher -> peak -> return.
  question:     three rising events -> silence.
  fall/repair:  leap down -> small steps up.
  orbit:        one repeated center -> neighbor -> return.
  fracture:     short motif -> shortened echo -> only final interval.

Then choose intervals, scale, and rhythm that support the shape. Avoid automatic
stepwise wandering or equally sized notes unless stasis is intentional.

5.2 MAKE ONE NOTE MATTER

Give a melodic focal event a distinct property: longer duration, strong arrival,
harmonic tension, unusual register, conspicuous dryness, or the only non-scale
tone. The focal event need not be loud. Surround it with enough simplicity for
the listener to locate it.

5.3 WRITE PHRASE PUNCTUATION

Phrases can "breathe" through rest, held note, timbral decay, or an answer from
another voice. Do not end every 4-bar idea with a drum fill. The melody can
resolve while the harmony remains open, or the harmony can resolve while the
melody stays suspended; these are distinct expressive choices.

5.4 MELODIC MOTION AGAINST HARMONY

  CHORD TONES can sound anchored at strong structural moments.
  APPROACH TONES can add direction before an arrival.
  NEIGHBOR TONES can make a sustained note feel alive.
  SUSPENSIONS can retain a note as the chord beneath it changes.
  CHROMATIC APPROACH can intensify an arrival by a semitone.

These are choices, not constraints. Modal, atonal, blues, and experimental
language need not enforce classical resolutions.

5.5 INTERVALS HAVE CONTEXT, NOT FIXED EMOTIONS

A minor second can read as menace, tenderness, comedy, or ornament according to
register, rhythm, timbre, harmonic support, and repetition. Avoid mapping each
interval to one rigid emotion. Build the desired feeling from several interacting
conditions.

5.6 MELODY WITHOUT A TRADITIONAL LEAD

A melody can be implied by a succession of changing filter peaks, percussive
pitches, chord top voices, or contrasting timbres. A strong track may have no
continuous lead instrument. If the bass already sings, do not add a lead merely
to fill a conventional role.

===============================================================================
6. HARMONY AS EMOTIONAL MOTION, NOT CHORD DECORATION
===============================================================================

Harmony includes pitch collection, chord quality, bass relationship, register,
voicing, rate of change, and the possibility of NO explicit chords. Emotion is
rarely determined by chord names alone.

6.1 FOUR INDEPENDENT HARMONIC DECISIONS

  COLOR:       what pitches/intervals sound together?
  DIRECTION:   where do individual voices move?
  RHYTHM:      when does harmonic meaning change?
  BASS:        what fundamental or pedal does the listener hear beneath it?

Before writing a chord progression, try a two-voice relationship or a pedal.
Two moving notes over a bass can say more than four large block chords.

6.2 COLOR WITHOUT CLICHE

Useful options when they fit the intent:
  - add9 and minor9 for richness without a compulsory heroic progression;
  - suspended 2nds/4ths to defer clear major/minor identity;
  - major7 and #11 colors for a floating, luminous instability;
  - dominant altered tones or a carefully voiced b9 for a short sharp threat;
  - quartal voicings to reduce familiar triadic gravity;
  - modal pedals (Dorian, Phrygian, Lydian) to sustain a characteristic world;
  - mixed modal colors to shift a mood without changing the tonic.

Avoid stacking extensions by default. Complexity that masks the melody is not
sophistication. A three-note voicing in a useful register often wins.

6.3 VOICE LEADING PRODUCES CONTINUITY

Try holding a shared note while one other voice moves a semitone. If a chord
changes completely each bar, the result may sound like unrelated "nice chords."
Small internal motion can connect remote harmonies, especially when the bass
supplies the dramatic shift.

SIMPLE ORIGINAL EXAMPLE, in an A-centered world:
  Chord 1: Am(add9)  = A C E B
  Chord 2: Fmaj7(#11) = F A C E B
  Chord 3: E7(b9)   = E G# B D F
  Return:  Am(add9) = A C E B

The first two share A, C, E, and B; their distinct bass/color changes meaning
with remarkably little upper-voice movement. The third introduces G# and F
against E for sharper dominant tension. The fourth restores A and C. These
voicings can be thinned and octave-spaced; do not play every note in the same
register. This is one expressive path, not a universal recipe.

6.4 HARMONIC RHYTHM IS A COMPOSITIONAL LEVER

One chord lasting eight bars can be deeply active if:
  the bass shifts, an upper voice approaches a dissonance, a lead changes mode,
  or a filter reveals previously hidden overtones.

Conversely, changing chords every beat can create urgency or instability.
Design chord-change timing in relation to melodic questions and section arcs;
do not change chords just because four bars passed.

6.5 HARMONIC AMBIGUITY

Ways to make touching and unsettling coexist:
  - omit thirds, allowing major/minor uncertainty;
  - preserve one tender melodic tone over a darker moving bass;
  - alternate a consonant shared-tone voicing with one close dissonance;
  - let a stable pedal remain while upper notes drift outside its mode;
  - delay resolution until after the drums vanish.

Make the ambiguous moment audible. A complex chord beneath a dense break may
be experienced as color, not as an identifiable harmonic event. Give it air.

6.6 HARMONIC SURPRISE WITHOUT RANDOM CHORDS

Establish a harmonic expectation first. Then alter one thing:
  expected chord, different bass;
  expected cadence, neighboring chord;
  expected third, suspended fourth;
  expected resolution, a held dissonance;
  expected minor mode, one borrowed brighter note.

A surprise is effective because it differs from a learned context, not because
its notes are rare. Once a surprise repeats, it can become part of the identity.

6.7 WHEN NOT TO WRITE CHORDS

An unresolved drone, a pitched-noise field, a one-note bass groove, or an
atonal percussion dialogue may supply all the needed harmonic world. Adding a
progression could weaken such music. Choose harmony's presence deliberately.

===============================================================================
7. BASS AS AN ACTIVE COMPOSER
===============================================================================

The bassline is not merely the root notes of a progression or a low-frequency
mixing problem. It can carry rhythm, motif identity, implied harmony, and
emotional direction.

7.1 DEFINE THE BASS'S JOB

  FOUNDATION:  repeat a small, reliable note/shape.
  COUNTERPOINT: answer kick and melody using independent timing.
  HARMONIC:    change chord interpretation through inversions and pedals.
  HOOK:        become the track's primary memorable phrase.
  TENSION:     withhold the expected root, move by a semitone, or use register leaps.

One bassline can change jobs by section. Do not force a separate sub and a
melodic bass if one instrument handles both roles successfully.

7.2 BASS + DRUMS = ONE COMPOSITE RHYTHM

First inspect kick and bass onsets together. Ask which notes reinforce the beat,
which answer the kick, and which reserve silence for the snare. The listener
hears their combination, not two isolated patterns.

THREE RELATIONSHIPS:
  Lock:      bass and kick begin together for impact.
  Interlock: bass fills the kick's gaps for propulsion.
  Contradict: bass displaces the perceived downbeat for friction.

Use more than one relationship across the track. A lock after extended
interlocking can feel like a payoff without a new sound.

7.3 THE "FAT" BASS NEEDS A RHYTHMIC SILHOUETTE

A powerful Moog-like bass can be playful if its rests and note lengths breathe.
Try varied gate lengths, two adjacent notes as a pickup, one longer rounded
note, and an octave or fifth leap only where it creates a phrase accent.
Do not put long sub tails under every busy kick; design the time relationship
and production together.

7.4 BASS AS A RECURRING CHARACTER

Write one bass answer that is withheld until the final act. The bass may start
by asking a question and end by completing it. This can make an almost
non-melodic dance track feel composed rather than looped.

===============================================================================
8. SOUND DESIGN AS COMPOSITION
===============================================================================

A sound can change what a phrase MEANS, not merely how polished it sounds.
Timbral development is especially useful when harmonic content is minimal.

8.1 TIMBRE CAN CARRY A MOTIF

Represent a short musical identity through:
  noisy -> pitched -> noisy;
  dull -> bright -> sudden mute;
  hard attack -> soft tail -> reversed-like anticipation;
  dry pulse -> diffuse echo -> dry pulse;
  three short resonant hits followed by a long silence.

If pitch disappears but the gesture remains recognizable, the timbre itself is
part of the composition.

8.2 ORCHESTRATE A TRANSFORMATION

A meaningful timbral arc might be:
  Scene 1: muffled, distant fragment.
  Scene 2: clearer transient reveals its rhythm.
  Scene 3: full pitch reveals it is related to the bass motif.
  Scene 4: the sound breaks into noisy fragments.
  Scene 5: a sparse, dry version returns with emotional intimacy.

The reveal is a compositional event. Merely automating a filter from 2 to 8
because the section is a build is not the same as an authored reveal.

8.3 CONTINUITY ACROSS RADICAL TIMBRE CHANGES

Preserve at least one fingerprint: rhythmic placement, contour, attack pattern,
register, spectral envelope, or spatial direction. For strong rupture, let the
new sound be unfamiliar first; later expose the shared fingerprint.

8.4 SPACE IS A NARRATIVE DIMENSION

  Near:       dry, clear, sharply localized.
  Far:        lower direct/reverberant ratio, blurred onset, diffuse image.
  Huge:       sparse events with long tails and broad stereo support.
  Intimate:   few voices, modest tails, audible transients and note endings.

These are perceptual tendencies, not direct mappings from one numeric setting.
The most "airy" section is often the one where fewer things play. Long reverb
on every active channel usually produces fog rather than openness.

8.5 DESIGN CONTRASTING DEPTH PLANES

Try three layers with different musical roles:
  FRONT:  tight break and articulate bass.
  MID:    short chord stabs or a small answering synth.
  BACK:   sparse, sustained harmonic or textural residue.

Create intimacy/scale by moving a recognizable idea between planes. When the
bass stops, distant material may suddenly become foreground without changing
level. Prefer this to simply making the pad louder.

8.6 THE "GLITCH" MUST SPEAK

Classify each glitch as one of:
  ECHO:        repeats a recognizable motif fragment.
  INTERRUPTION: interrupts an expected event.
  ANSWER:      responds to another voice.
  TRANSITION:  announces a structural turn.
  TEXTURE:     deliberately nonsemantic, supporting motion or atmosphere.

If all glitches are equally random, none functions as punctuation. Make a few
specific glitches recur or transform; let the remaining ones be subordinate.

8.7 SOURCE-TO-SOURCE TRANSFORMATION

A strong idea is to make one sound seem to emerge from another: pitched
percussion whose resonant frequency gradually becomes the bass's next note,
or a melodic fragment that becomes stuttering percussion while retaining its
rhythm. In Beat Lab, realize this with supported synthesis, note expression,
sampled/resampled transformations, and automation where available. Never assume
an undocumented morphing engine or arbitrary plugin exists.

===============================================================================
9. MUSICAL INTERACTION: INSTRUMENTS AS CHARACTERS
===============================================================================

The voices should not all describe the same downbeat in parallel. Decide how
they cooperate, compete, answer, or temporarily ignore each other.

9.1 GIVE EACH VOICE A VERB

Instead of instrument-only labels, assign a job:
  bass: PROPOSES a rhythmic phrase;
  break: INTERRUPTS or COMPLETES it;
  chords: REINTERPRET its emotion;
  texture: REMEMBERS a fragment;
  lead: QUESTIONS or CONTRADICTS the harmony.

The labels are planning concepts, not new JSON properties.

9.2 CALL AND RESPONSE, FOUR VARIANTS

  DIRECT:      an instrument repeats another's rhythm at a new pitch.
  INCOMPLETE:  the answer starts correctly but stops early.
  CONTRARY:    the answer moves down when the call moves up.
  RECONTEXT:   the same gesture appears over a different chord or bass note.

An answer needs audible space. A second voice playing continuously under the
first is counterpoint, not necessarily a response.

9.3 COUNTERPOINT WITHOUT ACADEMIC COMPLEXITY

Write one interesting line. Add the second in the *holes* of the first.
Check whether the two have distinct rhythmic contours and whether occasional
simultaneous arrivals matter. Change register or timbre when their attacks
mask one another.

Avoid both extremes:
  perfect doubling everywhere -> no independence;
  complete independence everywhere -> no conversation.

Occasional convergence (same accent, shared target pitch, matched silence)
can supply satisfying structure after independent movement.

9.4 HOCKET AND VOICE TRANSFER

Distribute successive events of one composite melody among different sounds:
  Synth A: notes 1 and 4.
  Synth B: notes 2 and 5.
  Plucked percussion: notes 3 and 6.

No single instrument contains the whole phrase; the ear assembles it across
timbres. Works best when the events are clear, non-overlapping, and share a
common rhythmic intent. Deliberately break the alternation once to announce a
section change.

9.5 CONTRARY MOVEMENT

When the bass rises, an upper voice can descend; when percussion becomes denser,
harmony can simplify; when sounds become brighter, the chord can turn darker.
These contradictions can make the music psychologically richer than having
every parameter rise toward the same drop.

9.6 PROTAGONIST ROTATION

At any moment, identify what is foreground. Rotate attention purposefully:
  bass-led groove -> percussion-led conversation -> harmonic reveal -> bass
  and percussion reunion.

Not every section needs a new instrument. Existing material can assume the
foreground by removing competitors.

===============================================================================
10. MUSICAL STORYTELLING ACROSS SECONDS AND MINUTES
===============================================================================

Arrangement is not only a sequence of intro, build, drop, break, outro.
It is the management of memory, tension, attention, time, and return.

10.1 TREAT SECTIONS AS SCENES

Each scene should have an event or condition that justifies its existence.
Helpful scene verbs: introduce, withhold, establish, destabilize, expose,
transform, contradict, suspend, reconcile, dissolve.

For each scene, choose:
  What does the listener already know?
  What new relationship becomes audible here?
  What remains unchanged to make the new thing legible?
  What question will the next scene answer?

10.2 USE MULTIPLE ENERGY AXES

Energy is not a single 1-to-10 loudness slider. Track at least:
  rhythmic density / intensity;
  harmonic tension / stability;
  spectral brightness;
  dynamic intensity;
  motion / change rate;
  spaciousness / intimacy.

These axes can move in opposing directions. A quiet, almost empty section may
be the most emotionally tense; a loud beat can be harmonically stable and
comforting. Do not equate "climax" with "all tracks at maximum density."

10.3 EXPECTATION HAS TO BE LEARNED

A delayed snare only surprises if earlier passes trained the listener to
expect it. A missing chord only hurts if its arrival was anticipated.
Establish -> repeat -> perturb -> possibly restore. The lengths of these stages
can be seconds or minutes depending on genre and form.

Research on musical expectation suggests that enjoyment can relate to the
interaction of predictability and surprise, not simply maximum novelty.
Do not turn that finding into a universal numerical optimal-surprise rule.
Different listeners and musical cultures learn different expectations.

10.4 THE ART OF WITHHOLDING

A compelling arrangement may withhold:
  the full melody;
  the root of a chord;
  the downbeat kick;
  the expected snare;
  the high-frequency part of a recurring sound;
  the second half of a bass answer;
  the acoustic space of a previously dry motif.

When the withheld feature arrives, make sure the audience can recognize the
fulfillment. A payoff is a relationship with what came before.

10.5 STRUCTURAL CONTRAST WITHOUT "BIGGER DROP" THINKING

Alternatives to stacking instruments:
  switch a straight groove to a fractured one;
  expose a chord previously buried;
  remove the kick and let bass articulation define the rhythm;
  replace a sixteenth-note grid with open half-time;
  return a motif in a vulnerable, dry sound;
  move from dissonant density to one sustained consonant interval.

10.6 RECAPITULATION WITH NEW MEANING

A compelling final return is not always a literal replay. Keep the recognizable
rhythm but alter harmony; keep melody but change the bass; restore a phrase
under a new spatial background; complete a previously cut-off final note.
The listener hears both the original identity and the journey taken.

10.7 ENDINGS ARE COMPOSITIONAL CLAIMS

Possible endings:
  RESOLUTION: the tension resolves and the final gesture completes.
  WITHDRAWAL: layers disappear until only the seed remains.
  INTERRUPTION: cut before the listener expects closure.
  TRANSFORMATION: the last sound implies the opening has become something else.
  LOOP CIRCLE: the ending reconnects seamlessly to the beginning.

Choose intentionally. A master fade cannot rescue an arrangement that never
made a final compositional decision.

===============================================================================
11. CREATIVE COMPOSITION PROCEDURE FOR AN AI
===============================================================================

This is a reusable method, not a rigid production checklist. Internally plan,
then output only what the authoritative Beat Lab score contract permits.

PASS 1 - DEFINE THE REQUEST
  Extract explicit style, duration, mood, rhythmic language, sound references,
  foreground expectations, and exclusions. Translate artist references into
  abstract attributes rather than copying recognizable work.

PASS 2 - DECIDE THE DRIVING CONTRAST
  Choose a productive tension: mechanical/human, dense/spacious, tender/ominous,
  dry/remote, static/unstable, repetitive/evolving. A track can have several
  contrasts, but select one that guides its identity.

PASS 3 - INVENT THREE DISTINCT SEEDS
  Invent one rhythmic seed, one pitched/harmonic seed, and one timbral seed.
  They may be interrelated, but each should have a recognizable silhouette.
  Reject generic placeholders such as continuous root-eighth bass notes unless
  repetition itself is a deliberate aesthetic decision.

PASS 4 - CHOOSE AN ANCHOR AND A PROTAGONIST
  Decide what the listener can rely on and what has permission to mutate.
  Determine whether the bass, break, melody, harmony, or sound field leads.

PASS 5 - TEST TWO BARS BEFORE ARRANGING EVERYTHING
  Write a compelling 2- to 4-bar combination containing the main relationship.
  If it is weak, revise the timing, gaps, interaction, or motif. Do not hide a
  weak loop behind 20 layers or elaborate mastering.

PASS 6 - MAKE A TRANSFORMATION LIBRARY
  Create 3-6 meaningful variants with known preserved traits:
    A0 - unmistakable seed;
    A1 - rhythmic response;
    A2 - fragile, thinned variation;
    A3 - harmonic reinterpretation;
    A4 - timbrally fragmented variation;
    A5 - returning seed with one changed ending.
  Use only variants that serve the eventual form.

PASS 7 - PLAN THE SCENES
  Map time into scenes. For each, name protagonist, harmonic state, rhythmic
  state, novelty, memory, transition mechanism, and reason it belongs.
  Ensure something develops in the middle; do not simply save everything
  interesting for an ending.

PASS 8 - WRITE THE BIGGEST PAYOFF FIRST IF USEFUL
  Decide what late return, resolution, or transformation is worth earning.
  Place the preceding scenes to establish its significance.

PASS 9 - ARRANGE WITH FOCUS
  At each entrance, decide what leaves or becomes quieter. Reserve a space for
  one-off events and let looped material sustain the musical grammar. Do not
  add an instrument merely to signal the start of another 8-bar block.

PASS 10 - VERIFY MUSICAL CAUSALITY
  For each section boundary, ask: "Because of what the listener just heard,
  why should this be the next event?" The answer may be contrast, extension,
  resolution, a delayed reply, or purposeful rupture.

PASS 11 - COMPOSE A TRUE END
  Select completion, dissolution, interruption, or a return with changed
  meaning. Do not let a pattern simply stop due to durationSec.

PASS 12 - RENDER, LISTEN, AND REVISE
  Schema validity is necessary, not sufficient. When audio preview is possible,
  listen without looking at the score. Diagnose the felt result, then make
  specific changes (see Section 15). If no renderer is accessible, inspect
  onsets, phrase spans, harmonic motion, and energy distribution conservatively.
  Do not claim a listening test you did not perform.

===============================================================================
12. CONTROLLED SURPRISE: A DECISION FRAMEWORK, NOT RANDOMNESS
===============================================================================

12.1 ESTABLISH A LOCAL GRAMMAR

Before violating an expectation, provide examples of it. The grammar can be:
  kick on four beats, but not in the final bar;
  bass always leaving beat 4 empty;
  a pad alternating two voicings;
  a synth gesture returning every eight bars;
  snare color changes only at section boundaries.

Only a few grammar rules are needed. Listeners do not need to consciously name
them, but repeated exposure makes deviation audible.

12.2 CHOOSE WHAT KIND OF SURPRISE

  RHYTHMIC:    displaced or missing accent.
  HARMONIC:    one unexpected bass/chord/voice movement.
  MELODIC:     leap, silence, contour reversal, delayed resolution.
  TIMBRAL:     familiar phrase in an unexpected sound.
  STRUCTURAL:  earlier-than-expected return or withheld arrival.
  SPATIAL:     distant element suddenly near or vice versa.

Prefer one primary surprise per significant moment unless deliberate overload
is part of the concept. Multiple surprises may cancel the listener's ability
to understand what changed.

12.3 BOUNDED VARIATION

For a recurring phrase, often preserve two of these three dimensions:
  rhythmic contour / pitch contour / phrase boundary.
Change the third and optionally alter timbre. This "two-of-three" rule is a
creative heuristic, not a command. Break it for genuine rupture.

12.4 STRUCTURED RANDOMNESS

Probability is valuable for subordinate texture, alternate ghost notes, and
micro-detail. It is risky for the one indispensable motif note or structural
payoff, because each render can lose the narrative event.

Use determinism for identity and form; probability for the small surrounding
living surface. Fix a seed when reproducibility matters. If a randomized event
would destroy the phrase when omitted, it was not merely decoration.

12.5 WHEN TO BREAK THE FRAMEWORK

If the request favors maximalism, free-form experimental music, musique
concrete, or persistent disorientation, coherent growth can occur through sound
morphology, recurrence of one frequency band, dynamic contour, or pure contrast
rather than tonal/rhythmic repetition. Do not force tonal songs onto abstract
sound art.

===============================================================================
13. THINK ACROSS THREE LEVELS OF MUSICAL MEMORY
===============================================================================

IMMEDIATE MEMORY (about a beat to a few seconds):
  transients, ghost notes, call/answer, syncopation, rests, attack shapes.
  Task: create a recognizable gesture.

PHRASE MEMORY (several bars):
  repetition with variations, 4- or 8-bar questions, melodic and bass answers.
  Task: create expectation and meaning within a local unit.

LONGER-TERM MEMORY (sections and returns):
  familiar bass appearing after a breakdown, timbral reveal, harmonic payoff,
  transformed opening, final completion.
  Task: make the piece feel like one developing thought.

Do not interpret these as fixed perceptual time windows. They are useful
organizational scales and depend on tempo, density, and listener familiarity.

A GOOD CROSS-SCALE DEVICE:
  Micro: a short-short-long snare echo.
  Phrase: those accents become the recurring last-bar fill.
  Macro: later the bass adopts short-short-long as the final theme.

The listener may not consciously detect the connection but can still perceive
continuity. Make one connection clear enough to matter.

===============================================================================
14. GENRE LENSES: APPLY PRINCIPLES WITHOUT ERASING STYLE
===============================================================================

The genre guide defines identity and tempo language. This section suggests
how to develop music *inside* those identities. These are possibilities, not
claims that every track in a genre must behave this way.

TECH HOUSE
  Anchor: kick/bass/hat pocket.
  Develop: rhythmic displacement, negative space, eccentric but related
           percussion responses, selective short timbral surprises.
  Preserve: danceable forward pulse and the importance of groove.
  Avoid: replacing a strong pocket with an overcomplicated lead melody.

TECHNO / MINIMAL TECHNO
  Anchor: stable pulse, tonal or textural cell.
  Develop: phase relationships, filter/spectral revelation, tiny accent
           mutations, strategic subtraction, long-form changes in pressure.
  Preserve: hypnotic continuity if the request calls for it.
  Avoid: a mandatory chord change or pop-style breakdown every eight bars.

JUNGLE / DRUM & BASS
  Anchor: breakbeat grammar, meaningful backbeat reference, sub/bass identity.
  Develop: break rearrangement, call/response between edits and bass,
           cross-accent and silence, half-time/double-time perceptual shifts.
  Preserve: physical rhythmic motion despite detailed edits.
  Avoid: filling every subdivision until no contrast remains.

IDM / EXPERIMENTAL ELECTRONICA
  Anchor: one legible motif, recurring timbral fingerprint, or rhythmic core.
  Develop: metrically surprising variations, cross-voice hocket, strange
           harmony, register swaps, motif-to-noise transformations.
  Preserve: a deliberate listening path; "experimental" need not mean random.
  Avoid: glitched surface detail with no large-scale relationship.

AMBIENT / DRONE
  Anchor: pitch center, space, evolving spectrum, or a recurring faint gesture.
  Develop: nearly imperceptible harmonic and spectral motion, recontextualized
           resonances, tension through persistence and very rare events.
  Preserve: patience and focus; silence is material.
  Avoid: treating absence of drums as a reason to add aimless chords.

TRANCE / MELODIC ELECTRONICA
  Anchor: a memorable contour or arpeggiated pitch identity.
  Develop: harmonic anticipation, altered phrase endings, delayed completion,
           countermelody, expansion and compression of melodic range.
  Preserve: melodic memorability and earned release.
  Avoid: large detuned stacks as a substitute for an actual musical theme.

BROKEN BEAT / FUTURE JAZZ / JAZZ-ELECTRONIC HYBRIDS
  Anchor: an expressive bass-and-drum conversation or a distinct chord color.
  Develop: syncopated accompaniment, off-center accents, extended harmony,
           voice leading, contrapuntal fragments, elastic rhythmic answers.
  Preserve: pocket even when subdivisions get sophisticated.
  Avoid: equating "jazz" with randomly adding sevenths and ninths everywhere.

INDUSTRIAL / HARD EXPERIMENTAL
  Anchor: an unmistakable percussive or timbral character.
  Develop: brutal repetition, unusual accent hierarchy, abrupt drops to
           unprocessed intimacy, pitch/timbre inversion, impact through silence.
  Preserve: intensity of concept, not necessarily constant full-scale loudness.

Adapt to the actual user's hybrid description; the genre boundaries are
resources, not prohibitions. If the request combines warm jungle with IDM and
jazz harmony, compose the relationship instead of choosing one genre label and
abandoning the others.

===============================================================================
15. THE REVISION LAB: DIAGNOSE THE COMPOSITION, NOT JUST THE MIX
===============================================================================

If playback is available, listen three times with different attention:

  PASS A - WITHOUT LOOKING: What do you actually remember after it ends?
  PASS B - GROOVE ONLY: Is there a strong composite beat/bass relationship?
  PASS C - LONG ARC: Can you feel why each scene follows the last?

SYMPTOM -> COMPOSITIONAL INTERVENTION

"Sounds good but forgettable."
  Give one phrase an asymmetrical hook; repeat it consistently before varying.

"Constant motion, no direction."
  Design a delayed payoff; remove unmotivated fill layers; build a returning
  motif across multiple sections.

"Too repetitive."
  Change phrase endings, harmonic interpretation, or listener focus; do not
  reflexively add a new instrument every four bars.

"Too random."
  Establish a stable anchor or use recurring timbral/motivic fingerprints;
  reserve the wildest edits for a smaller number of moments.

"The drop is bigger but not better."
  Ask which new musical fact is revealed. Make the core groove or hook clearer,
  not merely louder.

"Complex drums fight the bass."
  Inspect their combined onsets. Restore a shared landing point or a deliberate
  gap for bass articulation; simplify the low-end rhythm first.

"Harmony is sophisticated but emotionally flat."
  Change voice leading, spacing, bass relationship, and harmonic rhythm.
  Let a melodic tone persist across contrasting chords.

"Beautiful atmosphere but no composition."
  Make a recurring spectral/pitched gesture evolve; introduce a meaningful
  absence, answer, or late reveal.

"Every section sounds like a different track."
  Carry one identity fingerprint across boundaries; use foreshadowing before
  major changes or recognizable material immediately after rupture.

"One strong idea is buried."
  Subtract companions. Give the idea a full, intelligible statement before
  radically transforming it.

"Ending feels accidental."
  Let an idea finish, fail to finish conspicuously, or hand itself back to the
  opening. Do not rely solely on stopping the beat.

THE MUTING TEST:
  Temporarily remove any layer. If the piece communicates more strongly,
  consider dropping that layer or limiting it to one meaningful scene.

THE QUIET-DETAIL TEST:
  At normal listening level, can one hear why that tiny glitch exists? If not,
  it may still be useful texture; but do not count it as compositional progress.

THE 20-SECOND IDENTITY TEST:
  Can a listener encountering any non-breakdown segment infer what is unique
  about this track within roughly a phrase? Treat this as an editorial question,
  not a hard stopwatch criterion.

===============================================================================
16. BEAT LAB IMPLEMENTATION: TRANSLATE MUSICAL INTENT INTO LEGAL SCORES
===============================================================================

This is a conceptual crosswalk, NOT a substitute for music-guide.txt. Before
emitting JSON, re-check the actual documented syntax, numeric constraints,
closed name catalogs, transform scope, and unit semantics.

COMPOSITIONAL IDEA                         BEAT LAB CAPABILITY TO CONSULT
-------------------------------------------------------------------------------
Stable recurring seed                     motifs; patterns; arrangement
Related melody variants                  motifTransform; pattern transforms
Alternating calls and answers            separate patterns and placements
Pattern mutation over repeated cycles    condition; variations; transform
Independent loop lengths                 lenBeats; repeat; atBeat
Asymmetric phrase endings                omit/only; varied patterns; direct notes
Ghosts and infrequent detail             per-note volume/probability; seed
Coordinated timing feel                  grooves; swing; humanize; per-note off
Timbre-changing phrase                   ex_ synthesis; controls; automation
More organic attack and gesture          per-note expr; articulation; velocity
Moving acoustic/sample fragments         rs_ capture/slicing; sample controls
Background spectral movement             automation; pads; granular where legal
Evolving chord color                     harmony; explicit notes; voice leading
Hocket or counterpoint                    alternating pitched tracks/patterns
Bass/kick dialogue                        inspect pattern onset structure
One-off structural gesture                direct track; limited-time placement
Section intensity/width/texture           track/bus automation; master moves
Intentional silence                       omit patterns, notes, and entrances

UNIT SAFETY:
  - Direct tracks use time and note duration in SECONDS.
  - Pattern and motif notes use BEATS; arrangement is located by beat.
  - Determine section length by BPM/tempoMap, do not confuse bars and beats.
  - Use only documented top-level fields and exact symbolic names.
  - Per-note 'slide' is a boolean; the renderer also accepts 1/0 for true/false.
  - A motif transform is not a composition oracle; you author meaningful source
    material and choose where its transformations belong.
  - A probabilistic note may disappear on any repetition: keep necessary
    structural events deterministic.
  - Transforming a phrase by stretching notes does not necessarily expand
    its enclosing pattern's repeat period. Check clipping and section bounds.
  - Patterns extending a parent can become denser by addition; use omission,
    thinning, silence, or a new pattern when the music should become smaller.
  - A named automation target has persistent behavior. End its envelope at
    the intended resting value and use supported target/parameter names.
  - Reserve a unique pattern or explicit placement for structural one-offs.
  - Do not use documentation examples as prevalidated musical templates;
    construct original notes and validate with the current compiler.

COMPOSITIONAL FAILURE MODES SPECIFIC TO STRUCTURED SCORES:
  - One pattern repeated at uniform volume for the full duration.
  - Every pattern begins at beats divisible by 16: all entries feel square.
  - Transform values change, but listener cannot hear the preserved identity.
  - Too many independent probability events erase an essential groove.
  - A long reverb pad masks all phrase boundaries.
  - Apparent rhythmic "complexity" is just indiscriminate note multiplication.
  - An ending cuts off a sustained note or leaves the final thematic question
    unresolved accidentally rather than on purpose.

A concise score that realizes an idea is better than an enormous score that
merely exercises engine features. Use available advanced capabilities when
musically warranted, not to demonstrate their existence.

===============================================================================
17. FULL WORKED COMPOSITION: WARM JAZZ-JUNGLE MEETS UNEASY IDM
===============================================================================

A compositional storyboard, NOT executable JSON. Original illustration based
on a generic hybrid aesthetic: detailed breakbeats, elastic analog bass,
melodic warmth, occasional menace, wide reverberant harmonic atmosphere.

17.1 INITIAL DECISIONS

  Tempo: approximately 170 BPM in 4/4; a 96-bar track lasts about 136 s
         before any optional tail (96 * 4 * 60 / 170 = 135.53 s).
  Main anchor: a two-bar funky, rounded bass shape.
  Main instability: chopped break accents and occasional phrase fractures.
  Melodic seed: A4 -> C5 -> B4 -> E5 with unequal timing and a final rest.
  Harmony: an A-centered, slightly ambiguous minor palette, with extensions
           used sparingly and one sharper dominant tension event.
  Depth: dry rhythmic foreground, small syncopated chord middle, spacious bed.
  Core contrast: complex motion below, spacious sustained feeling above.

17.2 MOTIF FAMILY

  M0 (identity): short A-C, longer B, late brief E, then air.
  M1 (warmth): same rhythm, two notes moved to gentler nearby pitches.
  M2 (fracture): only A-C attacks; an extra stutter echoes the original rest.
  M3 (menace): B becomes Bb briefly over an A pedal; original rhythm retained.
  M4 (distance): seed in long, soft notes with a ghostly delayed response.
  M5 (return): original contour but final E held, completing earlier truncation.

Pitch names indicate intentions. Ensure the actual harmony/scale and motif
transforms express chosen pitches; use literal notes when necessary.

17.3 BASS GESTURE

  Bars 1-2 of its first appearance:
  - Rounded A low note lands decisively at first beat.
  - A quick two-note syncopation responds between main kicks.
  - The second bar rises briefly to C, then returns toward A.
  - It leaves a deliberate hole before the last snare of bar 2.

  Later development:
  - repeat intact so identity becomes clear;
  - vary just one note length;
  - in the uneasy scene, bring one chromatic neighbor into the answer;
  - in the final return, place the original syncopation under a new chord.

The bass should feel like a phrase somebody could imitate, not a constant run
of low notes. Its exact sound is an implementation decision in ex_ synthesis.

17.4 SCENE PLAN (96 BARS; BAR COUNTS ARE 1-BASED)

  Bars 1-8     "Curiosity"
    A sparse harmonic fragment and small percussive clicks hint at the melody.
    Let two rhythm fingerprints be audible before a full break arrives.
    No full bass statement yet; prefigure its short-short-long accent.

  Bars 9-24    "Conversation"
    Full bass gesture appears with a legible, warm breakbeat.
    Keep the snare/backbeat recognizable; edit small pickups every 4 bars.
    A tiny bright synth replies to the bass only at the end of alternate phrases.
    New fact: percussion and bass are related characters, not a rhythm bed.

  Bars 25-40   "Playful elaboration"
    Break fragments change order; one 3-unit accent grouping drifts across bar
    expectations without erasing the main pulse. Introduce M1 in a middle voice.
    At bar 39, deliberately remove a familiar bass pickup; the missing note
    prepares an emotional shift more effectively than a giant fill.

  Bars 41-52   "Unease"
    Harmonic bass/voice relationship becomes more ambiguous; briefly use M3.
    Keep part of the bass rhythm but shorten its sustain. Glitches become
    INTERRUPTIONS rather than decoration. Limit loud percussive overload;
    the sharpened harmonic color should be audible as a new emotional fact.

  Bars 53-64   "Weightlessness"
    Remove most foreground drums; sustain M4 as distant harmonic residue.
    Let a few tiny sounds orbit a held pitch; no need for a standard riser.
    The atmosphere feels vast because active event density collapses.
    New fact: the chopped motif and the airy harmonic image are connected.

  Bars 65-80   "Fracture and recognition"
    Reintroduce chopped breaks with bass fragments, but avoid immediate full
    maximal density. Percussion echoes the motif rhythm; another instrument
    answers the opening's missing end. At bar 73 the stable bass A returns
    while upper harmony still feels different: recognition under new light.

  Bars 81-92   "Tender return"
    Return the first full bass gesture almost unchanged; use a warmer/higher
    chord voicing. M5 completes what earlier phrases withheld. Complexity can
    remain in subtle break edits, but the main focus is now unmistakable.

  Bars 93-96   "Afterimage"
    Strip away drums and upper clutter. Leave one quiet bass conclusion and
    the dying upper-tone response. End on an intentional hold or gentle open
    suspension; do not merely exhaust the arrangement's repeat count.

17.5 THREE CROSS-SCALE PAYOFFS

  Rhythm: the early missing slot becomes the destination of the final answer.
  Pitch: the unsettled semitone is heard against a familiar, finally stable A.
  Timbre: a fragment first heard as a dry click returns as a distant pitched
          tone, revealing it as part of the same motif family.

17.6 WHAT NOT TO DO TO THIS TRACK

  - Do not add four random glitch layers to every bar.
  - Do not play an extended chord stack continuously under the densest break.
  - Do not interpret "jazz-inspired" as mandatory rapid chord changes.
  - Do not replace the memorable bass with a new bass each scene.
  - Do not make the final return louder simply because it is later.

17.7 HOW TO COMPOSE A DIFFERENT VERSION

Retain the emotional contrast, then choose a different anchor or motif DNA.
For example, let chords lead and bass answer; use a five-onset rhythmic cell;
place the most delicate section at the beginning rather than the center.
The storyboard demonstrates a method of connected decisions, not a template
to reuse for every IDM-jungle request.

===============================================================================
18. THREE MORE SHORT COMPOSITION STUDIES
===============================================================================

STUDY A: TECHNO, "THE SAME NOTE CHANGES MEANING"
  Seed: one repeating two-note synth interval; dry kick pulse.
  Development: first establish timbral identity, then narrow the harmony to a
  drone, gradually shift a background pitch by semitone, temporarily remove
  the kick, finally restore it while the original interval is reharmonized.
  Payoff: no obvious new hook, but the familiar notes now feel unstable.
  Don't confuse the slow filter movement with the entire composition;
  the harmonic reinterpretation is the main event.

STUDY B: TECH HOUSE, "THE BASS MISSES ITS TRAIN"
  Seed: syncopated two-bar bass with a conspicuous beat-4 rest.
  Development: hats answer that empty beat; a four-bar cycle varies only the
  final kick pickup; halfway through, the hats unexpectedly omit their answer.
  Payoff: later the bass finally occupies the empty beat, briefly aligning
  with the kick, then the original gap returns. The listener has learned an
  absence and feels its fulfillment without added instruments.

STUDY C: AMBIENT, "AN OBJECT MOVES THROUGH SPACE"
  Seed: a distant pitched tone followed by two short echoes.
  Development: the spectral center moves slowly; the echoes become clearer;
  a dissonant neighboring tone appears and is gently absorbed; the near/dry
  original returns once, quietly, then dissolves into the background.
  Payoff: the same gesture is heard at a changed distance. Form is built from
  attention and spatial memory rather than beats, drops, or chords.

===============================================================================
19. CONCISE CREATIVE RULES TO REMEMBER WHILE GENERATING
===============================================================================

  01. Find the song inside the loop before building the arrangement around it.
  02. Establish a pattern before asking its violation to feel surprising.
  03. A motif can be rhythm, harmony, timbre, space, or silence; not only notes.
  04. Repeat for recognition; vary for interest; return for meaning.
  05. Vary ONE meaningful feature first; add more only if needed.
  06. When two instruments play, design the relationship between them.
  07. Listen to bass and drums as one composite groove.
  08. A missing expected hit is a valid compositional event.
  09. More onsets do not automatically mean more rhythmic imagination.
  10. A melody's contour, focal point, and rests matter more than its length.
  11. Chord timing and voice leading matter as much as chord complexity.
  12. Dissonance matters in relation to its surrounding context.
  13. Timbre changes can reveal, hide, or reinterpret a musical idea.
  14. Wide space is often achieved by leaving sonic and temporal room.
  15. Let the foreground change without always introducing new instruments.
  16. Every structural arrival should reveal or change a musical relationship.
  17. A breakdown can be an emotional climax even when nearly silent.
  18. Keep structural identity deterministic; use chance for subordinate life.
  19. Preserve coherence across extreme contrasts with one recognizable trace.
  20. The strongest ending changes how the beginning is remembered.

===============================================================================
20. FINAL SILENT SELF-REVIEW BEFORE EMITTING A BEAT LAB SCORE
===============================================================================

A. ORIGINALITY
  [ ] Material is newly composed; no recognizable melody/hook is copied.
  [ ] The piece has an identity more specific than a genre and BPM.

B. MOTIF AND DEVELOPMENT
  [ ] At least one idea is recognizably introduced and later developed,
      unless a deliberately non-thematic composition was requested.
  [ ] Variations preserve audible relationships rather than merely sharing IDs.
  [ ] Significant new ideas earn their role; there is no unnecessary clutter.

C. RHYTHM AND INTERACTION
  [ ] Groove layers have complementary roles and intentional spaces.
  [ ] Bass and drums make a convincing composite rhythm where relevant.
  [ ] Micro-events/ornaments are subordinate to a larger rhythmic intention.

D. HARMONY AND EMOTION
  [ ] Chord color, bass, voice leading, and change rate fit the emotional arc.
  [ ] Contrasting emotions are audible, not just labels in the plan.
  [ ] Sparse passages do actual narrative work rather than serving as filler.

E. FORM
  [ ] Each scene develops, reveals, contradicts, withholds, or meaningfully
      sustains something; section length alone is not the reason it exists.
  [ ] At least one late moment rewards the listener's memory.
  [ ] The ending is intentional.

F. EXECUTION
  [ ] All score values and symbols conform to the current music-guide.txt.
  [ ] Pattern beats versus direct-track seconds are handled correctly.
  [ ] No guessed instruments, fields, plugins, or impossible transformations.
  [ ] No essential payoff depends on unreliable probability.
  [ ] The score is valid and its musical choices have been reviewed separately.

An item can intentionally be false. If so, know the artistic reason.

===============================================================================
21. SOURCES, INFLUENCES, AND PROVENANCE
===============================================================================

This document is an original synthesis and application guide, not a copy of a
textbook or a claim that scientific studies dictate musical taste. Distinguish:
  - Established vocabulary: motive, contour, fragmentation, sequence, voice
    leading, harmonic rhythm, counterpoint, hocket, metric grouping.
  - Published practical ideas: variation, asymmetrical loops, dramatic arc,
    subtraction, active listening and motif development in electronic music.
  - Authorial heuristics: blueprint, fingerprint preservation, protagonist
    rotation, scene verbs, structured surprise, and self-review procedures.
    These are practical proposals, not experimentally validated formulae.

Useful primary references and open educational resources:

  Beat Lab executable score specification:
  https://instush.github.io/beatlab-guide/music-guide.txt

  Beat Lab electronic music production principles:
  https://instush.github.io/beatlab-guide/electronic-music-principles.txt

  Beat Lab electronic music genres:
  https://instush.github.io/beatlab-guide/electronic-music-genres.txt

  Dennis DeSantis, Making Music: Creative Strategies for Electronic Music
  Producers (Ableton), with openly readable chapters on melody contour,
  successive mutations, asynchronous loops, and dramatic arc:
  https://makingmusic.ableton.com/

  Open Music Theory, Foundational Concepts for Phrase-Level Forms (motive and
  hierarchical musical form):
  https://viva.pressbooks.pub/openmusictheory/chapter/foundational-concepts/

  Gold et al. (2019), Predictability and Uncertainty in the Pleasure of Music:
  A Reward for Learning? Journal of Neuroscience 39(47), 9397-9409.
  https://pmc.ncbi.nlm.nih.gov/articles/PMC6867811/

  Cheung et al. (2019), Uncertainty and Surprise Jointly Predict Musical
  Pleasure and Amygdala, Hippocampus, and Auditory Cortex Activity.
  Current Biology 29(23), 4084-4092.e4.
  https://doi.org/10.1016/j.cub.2019.09.067

No numerical emotional quality score or universal music formula is implied by
these sources. Listening, context, creative intent, and the user's request
remain decisive.

END OF GUIDE
