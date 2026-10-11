# Beatlab score language reference

> Generated file — do not edit directly. Edit `src/lib/beatlab/ext-score-schema.ts`, then run `node scripts/generate-music-reference.mjs`.

This is the deterministic half of the external-LLM music documentation: accepted locations, shapes, names, ranges, defaults, and compiler constraints. For composition strategy and musical judgment, use [`public/music-guide.md`](../public/music-guide.md).

The canonical machine-readable form is [`music-score.schema.json`](./music-score.schema.json), using JSON Schema 2020-12. The compiler remains authoritative for cross-reference and musical-semantic checks that JSON Schema cannot express.

## How to read this reference

- Beat-addressed fields are quarter-note beats. Plain `Track` note time/duration fields are seconds; `Pattern` and `Motif` fields are beats.
- `default` is documentation in JSON Schema. A generic validator does not insert it; the Beatlab compiler applies defaults.
- Closed objects reject unknown fields. The compiler exposes one current language, not versioned or compatibility dialects.
- Compact automation `fader` and `pan` are deliberately not public. Use exact params `track.fader` and `track.pan`.

## Reference index

[`Score`](#score) · [`TempoPoint`](#tempopoint) · [`Curve`](#curve) · [`Depth`](#depth) · [`Tone`](#tone) · [`NoteLine`](#noteline) · [`PitchToken`](#pitchtoken) · [`AbsolutePitch`](#absolutepitch) · [`ScaleDegreePitch`](#scaledegreepitch) · [`ChordVoicing`](#chordvoicing) · [`StretchMode`](#stretchmode) · [`BowDirection`](#bowdirection) · [`ReleaseMode`](#releasemode) · [`ResampleRegion`](#resampleregion) · [`Note`](#note) · [`ExpressionPoint`](#expressionpoint) · [`Expression`](#expression) · [`ArpOrder`](#arporder) · [`Arp`](#arp) · [`Pattern`](#pattern) · [`Placement`](#placement) · [`Trigger`](#trigger) · [`TriggerPlacement`](#triggerplacement) · [`Transform`](#transform) · [`Condition`](#condition) · [`RepeatParity`](#repeatparity) · [`Variation`](#variation) · [`Track`](#track) · [`Motif`](#motif) · [`MotifTransform`](#motiftransform) · [`Harmony`](#harmony) · [`ScaleName`](#scalename) · [`Chord`](#chord) · [`Groove`](#groove) · [`MeterDenominator`](#meterdenominator) · [`GrooveBinding`](#groovebinding) · [`Sweep`](#sweep) · [`SweepKnob`](#sweepknob) · [`FilterSweepKnob`](#filtersweepknob) · [`LfoSweepKnob`](#lfosweepknob) · [`BusSweep`](#bussweep) · [`BusSweepParam`](#bussweepparam) · [`Keyframe`](#keyframe) · [`AutomationCurve`](#automationcurve) · [`Lfo`](#lfo) · [`TrackParam`](#trackparam) · [`MasterMove`](#mastermove) · [`MasterMoveEffect`](#mastermoveeffect) · [`Bus`](#bus) · [`BusRole`](#busrole) · [`BusEffect`](#buseffect) · [`BusFilterMode`](#busfiltermode) · [`Send`](#send) · [`SendTarget`](#sendtarget) · [`BuiltInReturn`](#builtinreturn) · [`SendTap`](#sendtap) · [`Sidechain`](#sidechain) · [`SidechainSource`](#sidechainsource) · [`Resample`](#resample) · [`Granular`](#granular) · [`GranularWindow`](#granularwindow) · [`SynthControls`](#synthcontrols) · [`PumpSource`](#pumpsource) · [`SynthPatch`](#synthpatch) · [`CompactSynthPatch`](#compactsynthpatch) · [`CompactOscillatorType`](#compactoscillatortype) · [`SynthNoiseColor`](#synthnoisecolor) · [`CompactLfoShape`](#compactlfoshape) · [`DualSynthPatch`](#dualsynthpatch) · [`Oscillator`](#oscillator) · [`OscillatorPhase`](#oscillatorphase) · [`SynthLfoShape`](#synthlfoshape) · [`ModulationSource`](#modulationsource) · [`ModulationTarget`](#modulationtarget) · [`SynthFilterMode`](#synthfiltermode) · [`CustomDrumPatch`](#customdrumpatch) · [`KickDrumPatch`](#kickdrumpatch) · [`MembraneDrumPatch`](#membranedrumpatch) · [`ClapDrumPatch`](#clapdrumpatch) · [`NoiseDrumPatch`](#noisedrumpatch) · [`MetalDrumPatch`](#metaldrumpatch) · [`DrumChokeMode`](#drumchokemode) · [`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumNoiseColor`](#drumnoisecolor) · [`PitchedInstrumentName`](#pitchedinstrumentname) · [`FactoryDrumHitName`](#factorydrumhitname) · [`Automation`](#automation) · [`CenteredLfo`](#centeredlfo) · [`CompactLfo`](#compactlfo) · [`DrumHitName`](#drumhitname) · [`GranularCurve`](#granularcurve) · [`GranularCurvePoint`](#granularcurvepoint) · [`GrooveUse`](#grooveuse) · [`InstrumentName`](#instrumentname) · [`KnobKeyframe`](#knobkeyframe) · [`ModRoute`](#modroute) · [`PitchRange`](#pitchrange) · [`RegionRange`](#regionrange) · [`ResampleSlices`](#resampleslices) · [`ResampleSource`](#resamplesource) · [`SynthEnvelope`](#synthenvelope) · [`SynthLfo`](#synthlfo) · [`TrackBusName`](#trackbusname) · [`TrackControls`](#trackcontrols)

## Rejected forms

- Compact automation knobs fader and pan: use track.fader and track.pan exact params.
- Top-level era, Track era, and mix.glue: not language fields; use top-level glue.
- Synth patch version: not a language field; osc or osc1+osc2 identifies the architecture.
- Unknown compact-synth fields.
- Compiler-output fields fxAuto, automation on Track/Bus, and underscore-prefixed internal fields.

## Score

Complete public Beatlab composition program. It may use plain tracks, patterns plus arrangement, or both.

### Syntax

```text
{ "tracks": [Track, ...], [other Score properties] }
{ "patterns": { "<pattern key>": Pattern, ... }, "arrangement": [Placement, ...], [other Score properties] }
{ "tracks": [Track, ...], "patterns": { "<pattern key>": Pattern, ... }, "arrangement": [Placement, ...], [other Score properties] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `bpm` | `number` | no | `120` | ≥ 30; ≤ 300 — Constant tempo when tempoMap is absent. When tempoMap is present, this may be omitted; if supplied, it must match tempoMap[0].bpm. |
| `tempoMap` | `TempoPoint[]` | no |  | 1..128 items — Ordered tempo segments; first point starts at beat 0. |
| `seed` | `integer` | no | `1` | ≥ 0; ≤ 4294967295 — Unsigned 32-bit deterministic seed for authored and renderer variation. |
| `durationSec` | `number` | no | `40` | ≥ 0.5; ≤ 1800 — Rendered score duration in seconds. |
| `swing` | `number` | no | `0` | ≥ 0; ≤ 10 — Score-wide swing default. |
| `humanize` | `number` | no | `0` | ≥ 0; ≤ 10 — Score-wide timing/velocity humanization default. |
| `glue` | `number` | no | `0` | ≥ 0; ≤ 10 — Mix-bus compressor amount. |
| `groove` | `GrooveBinding` | no |  |  |
| `patterns` | `Dictionary<string, Pattern>` | with arrangement |  | 1..∞ entries — Pattern definitions. Each object key declares the Pattern's name and must use 1..48 letters, numbers, underscores, or hyphens. |
| `arrangement` | `Placement[]` | with patterns |  | 1..∞ items — Pattern placements. |
| `tracks` | `Track[]` | unless patterns + arrangement |  | 1..∞ items — Plain seconds-addressed tracks. |
| `triggers` | `Dictionary<string, Trigger>` | no |  | 0..64 entries — Named silent control patterns used by pump and custom-bus sidechains. |
| `motifs` | `Dictionary<string, Motif>` | no |  | 0..128 entries — Named reusable pitched phrases. Every declared entry is validated even when no Pattern references it. |
| `harmony` | `Harmony` | no |  |  |
| `grooves` | `Dictionary<string, Groove>` | no |  | 0..64 entries |
| `automation` | `Automation[]` | no |  | Track and custom-bus sweeps. |
| `master` | `MasterMove[]` | no |  | Master performance moves. |
| `synths` | `Dictionary<string, SynthPatch>` | no |  |  |
| `drumSynths` | `Dictionary<string, CustomDrumPatch>` | no |  |  |
| `buses` | `Dictionary<string, Bus>` | no |  | 0..16 entries |
| `resamples` | `Dictionary<string, Resample>` | no |  | 0..16 entries |

### Constraints

- A Score requires a non-empty tracks array, or both a non-empty patterns object and a non-empty arrangement array. Both forms may coexist.
- patterns and arrangement are a pair: supplying either one requires the other, even when tracks is also present.
- tempoMap begins at beat 0, is strictly increasing, and its first bpm matches top-level bpm when bpm is supplied.
- All names and references resolve; pattern inheritance, motif inheritance, and the routing graph are acyclic.
- Every Track.id is unique among top-level tracks.
- Unknown Score properties, wrong JSON types, and supplied numeric values outside their documented ranges are compiler errors; values are never coerced or clamped.
- JSON Schema default values are documentation annotations; the Beatlab compiler, not a generic validator, applies defaults.

### Examples

```json
{
  "bpm": 120,
  "seed": 7,
  "patterns": {
    "bass": {
      "instrument": "supersaw_lead",
      "lenBeats": 4,
      "notes": [
        "0 C2 0.5 0.8"
      ]
    }
  },
  "arrangement": [
    {
      "pattern": "bass",
      "atBeat": 0,
      "repeat": 4
    }
  ]
}
```

### Related

[`TempoPoint`](#tempopoint) · [`GrooveBinding`](#groovebinding) · [`Pattern`](#pattern) · [`Placement`](#placement) · [`Track`](#track) · [`Trigger`](#trigger) · [`Motif`](#motif) · [`Harmony`](#harmony) · [`Groove`](#groove) · [`Automation`](#automation) · [`MasterMove`](#mastermove) · [`SynthPatch`](#synthpatch) · [`CustomDrumPatch`](#customdrumpatch) · [`Bus`](#bus) · [`Resample`](#resample)

## TempoPoint

Beat-addressed step or linear BPM segment start.

### Syntax

```text
{ "atBeat": …, "bpm": …, ["curve": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `atBeat` | `number` | yes |  | ≥ 0 — Tempo-segment start on the global score timeline, in beats. |
| `bpm` | `number` | yes |  | ≥ 30; ≤ 300 — Tempo from this point, in quarter-note beats per minute. |
| `curve` | `Curve` | no | `"step"` | Interpolation from this point to the next. |

### Constraints

- curve belongs to this TempoPoint and controls the segment from this point to the next. The final point's curve has no effect.
- linear changes BPM linearly over beat position; step holds this point's BPM until the next point.

### Related

[`Curve`](#curve)

## Curve

String enum controlling interpolation from one point to the next.

### Syntax

```text
"step" | "linear"
```

### Values

`"step"` · `"linear"`

## Depth

String enum for front-to-back lane placement. Omission leaves the lane at neutral mid depth.

### Syntax

```text
"front" | "back"
```

### Values

`"front"` · `"back"`

### Value ranges

| Value / target | Range |
|---|---|
| `front` | closer: slightly louder with added presence |
| `back` | farther away: quieter, darker, and sent more strongly to the room |

## Tone

String enum for lane spectral character. Omission leaves the lane spectrally neutral.

### Syntax

```text
"dark" | "warm" | "bright"
```

### Values

`"dark"` · `"warm"` · `"bright"`

### Value ranges

| Value / target | Range |
|---|---|
| `dark` | reduces high frequencies |
| `warm` | adds low-mid body and gently reduces high frequencies |
| `bright` | adds high-frequency presence and reduces low-mid masking |

## NoteLine

Token-efficient positional note string. Time/duration are seconds on a plain Track and beats inside a Pattern or Motif.

### Syntax

```text
pitched lane: <time> <PitchToken> <duration> <volume> [pan] [pN] [@ms]
drums lane: <time> <DrumHitName> <volume> [pan] [pN] [@ms] [flam] [rollN]
```

### Constraints

- All fixed positional values are required. An optional pan number comes next, followed by zero to four tags.
- Time must be 0 or greater; pitched duration must be greater than 0; volume is 0.01..1; pan is -1..1.
- Tags are pN (N = 0..1), @ms (signed integer milliseconds), flam, and rollN (N = integer 1..16). Each tag kind may appear once; unknown and duplicate tags are errors. flam and rollN are mutually exclusive.
- Use a Note object for harmony events, expressions, sample options, controls, or granular settings.

### Examples

```json
"0 C4 0.5 0.8 -0.3 p0.6"
```

```json
"2 e_snare 0.7 roll4 @12"
```

### Related

[`PitchToken`](#pitchtoken) · [`DrumHitName`](#drumhitname)

## PitchToken

A pitched note: either one exact absolute pitch or a scale degree resolved through Score.harmony.

### Syntax

```text
AbsolutePitch | ScaleDegreePitch
```

### Constraints

- PitchToken is used by pitched instruments. Drum lanes use DrumHitName instead.

### Examples

```json
"C4"
```

```json
"Bb3"
```

```json
"^1"
```

```json
"^b7@4"
```

### Related

[`AbsolutePitch`](#absolutepitch) · [`ScaleDegreePitch`](#scaledegreepitch)

## AbsolutePitch

One exact pitch written as a note letter, optional accidental, and octave number.

### Syntax

```text
string matching ^([A-Ga-g])([b#]?)(-1|[0-9])$
```

### Constraints

- The letter is A through G. Uppercase is the canonical spelling; lowercase is accepted.
- The optional # raises the note by one semitone; the optional lowercase b lowers it by one semitone.
- The octave changes at C: C4 is middle C and A4 is 440 Hz.
- Unusual spellings such as Cb4, B#3, E#4, and Fb4 are valid musical notes.
- Pitch-token validity is separate from an instrument's playable or recorded range.

### Examples

```json
"C4"
```

```json
"Bb3"
```

```json
"F#2"
```

```json
"C-1"
```

## ScaleDegreePitch

A pitch resolved relative to Score.harmony.tonic and its scale or pitchSet.

### Syntax

```text
string matching ^\^(bb|##|b|#)?([1-9]|1[0-3])(?:@(-1|[0-8]))?$
```

### Constraints

- The leading ^ is required and the degree is an integer from 1 through 13.
- Degrees follow the declared scale: in a seven-note scale, ^8 repeats ^1 one octave higher and ^9 repeats ^2 one octave higher.
- The optional b or bb lowers the resolved degree by one or two semitones; # or ## raises it by one or two semitones.
- Mixed accidentals b# and #b are not accepted.
- The optional @octave fixes the register to -1 through 8. Without it, the enclosing note/placement register or harmony.octave applies.
- A top-level Score.harmony object is required whenever a scale-degree pitch is used.

### Examples

```json
"^1"
```

```json
"^b7"
```

```json
"^#4"
```

```json
"^9@3"
```

### Related

[`Harmony`](#harmony)

## ChordVoicing

Reusable name or explicit octave placement for every tone in a chord.

### Syntax

```text
one of the keys in Score.harmony.voicings Dictionary<string, integer[]> | integer[]
```

### Value ranges

| Value / target | Range |
|---|---|
| `string` | case-sensitive key from Score.harmony.voicings |
| `integer[]` | one -4..4 octave offset per chord tone, in Chord.tones order |

### Constraints

- An explicit array must contain exactly one offset for every tone in the chord.
- Each offset moves its corresponding tone by that many whole octaves; it does not add or remove tones.

### Examples

```json
"WIDE"
```

```json
[
  -1,
  0,
  1
]
```

### Related

[`Harmony`](#harmony) · [`Chord`](#chord)

## StretchMode

Fixed sampled-playback mode that fits a take to the note duration without changing pitch.

### Syntax

```text
"fit"
```

### Values

`"fit"`

## BowDirection

Explicit recorded bow direction for a sampled bank that declares directional takes.

### Syntax

```text
"down" | "up"
```

### Values

`"down"` · `"up"`

## ReleaseMode

Recorded sample note-off behavior.

### Syntax

```text
"natural" | "none"
```

### Values

`"natural"` · `"none"`

### Value ranges

| Value / target | Range |
|---|---|
| `natural` | play the recording's declared natural note-off when available |
| `none` | suppress the recording's declared note-off |

## ResampleRegion

Selects audio from the resample named by the enclosing Track or Pattern instrument: all plays the complete capture, a slices.regions key selects its declared beat range, and an integer selects a zero-based slice generated by gridBeats or transients.

### Syntax

```text
"all"
| one of the keys in Score.resamples.<current instrument>.slices.regions Dictionary<string, [number, number]>
| integer
```

### Constraints

- The current instrument is the rs_ instrument used by the Note's enclosing Track or Pattern.
- A region key or generated-slice index is local to that resample and must resolve there.
- An integer is valid only with gridBeats or transients; it is a slice index, not a beat position.

### Examples

```json
"all"
```

```json
"verse"
```

```json
2
```

### Related

[`Resample`](#resample) · [`ResampleSlices`](#resampleslices)

## Note

Full note form shared by tracks, patterns, and motifs. The enclosing collection determines time units.

### Syntax

```text
{ ["t": …], ["b": …], ["note": …], ["chord": …], ["octave": …], ["voicing": …], ["strumMs": …], ["arp": …], ["voiceLead": …], ["range": …], ["maxLeap": …], ["dur": …], ["durB": …], ["vol": …], ["volTo": …], ["expr": …], ["pan": …], ["p": …], ["off": …], ["flam": …], ["roll": …], ["slide": …], ["art": …], ["sampleStart": …], ["reverse": …], ["damp": …], ["stretch": …], ["bow": …], ["release": …], ["region": …], ["granular": …], ["c": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `t` | `number` | no |  | ≥ 0 — Local onset in seconds. Legal only inside a direct Track. |
| `b` | `number` | no |  | ≥ 0 — Pattern- or motif-local onset in beats. |
| `note` | `PitchToken \| DrumHitName` | one of note/chord, except that a lane whose instrument is one exact DrumHitName may omit both |  | Pitch, degree, or drum hit. Mutually exclusive with chord. |
| `chord` | `string` | one of note/chord on pitched lanes; never together with note |  | One of the keys in Score.harmony.chords Dictionary<string, Chord>. Mutually exclusive with note. |
| `octave` | `integer` | no | motif/placement register; otherwise harmony.octave (default 4) | ≥ -1; ≤ 8 — Register used for a degree or chord. |
| `voicing` | `ChordVoicing` | no | chord voicing; otherwise 0 for every tone |  |
| `strumMs` | `number` | no | `0` | ≥ -500; ≤ 500 — Chord strum distance in milliseconds; negative strums downward. |
| `arp` | `Arp` | no |  | Chord-only arpeggiation. Requires chord and is forbidden when note is used. |
| `voiceLead` | `boolean` | no | `false` | Connect this chord to the chronologically previous chord event by nearest motion. Equal onsets use original note-array order as the tie-breaker. |
| `range` | `PitchRange` | no | chord/transform range; otherwise unrestricted |  |
| `maxLeap` | `integer` | no | chord/transform maxLeap; otherwise unrestricted | ≥ 0; ≤ 48 — Chord-only maximum allowed voice movement in semitones. Requires voiceLead: true. |
| `dur` | `number` | no | pitched: 0.5 sec; drums/resamples: source duration | > 0 — Duration in seconds on a plain Track. |
| `durB` | `number` | no | pitched: 0.5 sec after placement; drums/resamples: source duration | > 0 — Duration in beats inside a Pattern or Motif. |
| `vol` | `number` | no | `0.7` | ≥ 0.01; ≤ 1 — Note gain. |
| `volTo` | `number` | no |  | ≥ 0; ≤ 1 — Gain target at the end of the note; 0 fades to silence. |
| `expr` | `Expression` | no |  |  |
| `pan` | `number` | no | enclosing Track/Pattern pan; otherwise 0 | ≥ -1; ≤ 1 — Per-note pan position. |
| `p` | `number` | no | `1` | ≥ 0; ≤ 1 — Seeded probability for this note. |
| `off` | `number` | no | `0` | Timing offset in milliseconds. |
| `flam` | `boolean` | no | `false` | Adds a grace hit before a drum onset. |
| `roll` | `integer` | no |  | ≥ 1; ≤ 16 — Number of hits in a buzz leading into the onset. |
| `slide` | `boolean` | no | `false` | Glides a synth from its previous note. |
| `art` | `string` | no |  | Articulation name. Generic names (legato, tenuto, staccato, accent, ghost, mute, breathy, bend) create expression contours on synthesized, drum, and sampled notes; sampled pitched banks may also declare recorded articulations. |
| `sampleStart` | `number` | no | `0` | ≥ 0; ≤ 600 — Seconds skipped into a sampled recording. |
| `reverse` | `boolean` | no | `false` | Play the selected sampled take backwards. |
| `damp` | `number` | no | `0` | ≥ 0; ≤ 10 — Sample high-frequency damping. |
| `stretch` | `StretchMode` | no |  | Time-fit a sampled take to explicit dur/durB without changing pitch. |
| `bow` | `BowDirection` | no | automatic alternation where available | Explicit recorded bow direction. |
| `release` | `ReleaseMode` | no | `"natural"` | Sample note-off behavior. |
| `region` | `ResampleRegion` | no | `"all"` | Audio region selected from the current rs_ instrument. |
| `granular` | `Granular` | no |  | Per-note grain-cloud settings for an rs_ instrument. Requires explicit dur/durB and overrides the enclosing Track or Pattern granular value. |
| `c` | `SynthControls` | no |  |  |

### Constraints

- note and chord are mutually exclusive. One is required except on a lane whose instrument is one exact DrumHitName; there, omission triggers the lane's hit at its recorded pitch, while an optional AbsolutePitch tunes that hit.
- chord is legal only on a pitched lane. A drums kit lane uses note with a DrumHitName.
- voicing, strumMs, arp, voiceLead, range, and maxLeap require chord and are forbidden when note is used.
- A Note.maxLeap override requires voiceLead: true. Chord.maxLeap is a reusable default that becomes active when a chord event enables voiceLead.
- When arp is present, strumMs is accepted but has no effect; arp supplies the generated timing.
- flam and roll are mutually exclusive; use one ornament per Note.
- Inside Pattern/Motif, only b and durB are legal; inside Track, only t and dur are legal.
- Instrument-specific fields are rejected or ignored when the selected instrument lacks that capability.

### Examples

```json
{
  "t": 0,
  "note": "C4",
  "dur": 0.5,
  "vol": 0.7
}
```

```json
{
  "b": 0,
  "note": "e_snare",
  "vol": 0.8
}
```

```json
{
  "b": 0,
  "chord": "HOME",
  "durB": 2,
  "vol": 0.7
}
```

### Related

[`PitchToken`](#pitchtoken) · [`DrumHitName`](#drumhitname) · [`ChordVoicing`](#chordvoicing) · [`Arp`](#arp) · [`PitchRange`](#pitchrange) · [`Expression`](#expression) · [`StretchMode`](#stretchmode) · [`BowDirection`](#bowdirection) · [`ReleaseMode`](#releasemode) · [`ResampleRegion`](#resampleregion) · [`Granular`](#granular) · [`SynthControls`](#synthcontrols)

## ExpressionPoint

One value at one normalized position within a note expression curve.

### Syntax

```text
[phase: number, value: number]
```

### Value ranges

| Value / target | Range |
|---|---|
| `phase` | 0..1 — 0 is the beginning of the note and 1 is the end |
| `value` | The containing Expression property determines the allowed range |

### Constraints

- An ExpressionPoint always contains exactly two numbers.

### Examples

```json
[
  0,
  0.4
]
```

```json
[
  1,
  1
]
```

## Expression

Normalized performance curves evaluated across one note.

### Syntax

```text
{ ["gain": …], ["pitchCents": …], ["pan": …], ["vibrato": …], ["timbre": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `gain` | `ExpressionPoint[]` | no |  | 2..32 items — Gain-multiplier curve. |
| `pitchCents` | `ExpressionPoint[]` | no |  | 2..32 items — Additive pitch-displacement curve in cents. |
| `pan` | `ExpressionPoint[]` | no |  | 2..32 items — Additive pan-offset curve. |
| `vibrato` | `ExpressionPoint[]` | no |  | 2..32 items — Vibrato-depth curve. |
| `timbre` | `ExpressionPoint[]` | no |  | 2..32 items — Spectral-color curve. |

### Value ranges

| Value / target | Range |
|---|---|
| `gain` | point value 0..2 — multiplier on the note's authored gain |
| `pitchCents` | point value -2400..2400 — additive pitch displacement in cents |
| `pan` | point value -1..1 — additive offset from the note's static pan |
| `vibrato` | point value 0..1 — depth mapped to 0..40 cents at 5.2 Hz |
| `timbre` | point value 0..1 — 0 dark, 0.5 neutral, 1 bright |

### Constraints

- Every curve begins at phase 0, ends at phase 1, and has strictly increasing phases.
- Each curve contains 2..32 ExpressionPoint values.

### Related

[`ExpressionPoint`](#expressionpoint)

## ArpOrder

Fixed order in which an arpeggio emits its generated chord notes.

### Syntax

```text
"up" | "down" | "upDown" | "asWritten" | "random"
```

### Values

`"up"` · `"down"` · `"upDown"` · `"asWritten"` · `"random"`

### Constraints

- random uses the Score seed and is deterministic for the same score.

## Arp

Deterministic arpeggiation of a named chord event. It may appear only on a Note that uses chord.

### Syntax

```text
{ ["order": …], ["stepBeats": …], ["octaves": …], ["gate": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `order` | `ArpOrder` | no | `"up"` |  |
| `stepBeats` | `number` | no | `0.25` | ≥ 0.0078125; ≤ 16 — Distance between generated notes in beats. |
| `octaves` | `integer` | no | `0` | ≥ 0; ≤ 3 — Additional octave copies. |
| `gate` | `number` | no | `0.85` | ≥ 0.05; ≤ 1 — Generated duration as a fraction of stepBeats. |

### Constraints

- Arp requires Note.chord and is forbidden with Note.note.

### Related

[`ArpOrder`](#arporder)

## Pattern

Reusable beat-addressed lane placed by arrangement entries.

### Syntax

```text
{ ["instrument": …], ["notes": …], ["controls": …], ["swing": …], ["humanize": …], ["groove": …], ["bus": …], ["depth": …], ["tone": …], ["pan": …], ["lateMs": …], ["flamMs": …], ["choke": …], ["granular": …], ["lenBeats": …], ["extends": …], ["motif": …], ["motifTransform": …], ["omit": …], ["only": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `instrument` | `InstrumentName` | at least one of instrument/extends |  | Exact public sound used by this lane. |
| `notes` | `(NoteLine \| Note)[]` | no |  | Beat-addressed notes for this lane. Note objects use b and durB; compact NoteLine time and duration are also beats. |
| `controls` | `TrackControls` | no | {} |  |
| `swing` | `number` | no | Score.swing (default 0) | ≥ 0; ≤ 10 — Lane swing override. |
| `humanize` | `number` | no | Score.humanize (default 0) | ≥ 0; ≤ 10 — Lane timing and velocity humanization override. |
| `groove` | `GrooveBinding` | no |  | Lane groove resolved after Score.groove; omission inherits Score.groove, or applies no groove when the Score also omits it. |
| `bus` | `TrackBusName` | no | automatic instrument role | Explicit mixer destination. Omission uses the instrument's automatic role: kit drums to kit, declared percussion to perc, factory bass roles to bass, transition roles to fx, and other material to bed. |
| `depth` | `Depth` | no | "mid" | Front/back placement; omission means mid. |
| `tone` | `Tone` | no | neutral | Spectral character; omission means neutral. |
| `pan` | `number` | no | `0` | ≥ -1; ≤ 1 — Static lane pan. A Note.pan value overrides it for that note. |
| `lateMs` | `number` | no | `0` | Timing offset applied to every note, in milliseconds. |
| `flamMs` | `number` | no | `25` | ≥ 5; ≤ 60 — Spacing between a drum note's flam grace hit and main hit, in milliseconds; has no effect without Note.flam. |
| `choke` | `boolean` | no | `true` | Whether later kit-bus hat/openhat onsets cut this lane's ringing open-hi-hat tails; relevant only to open-hi-hat material on the kit bus. |
| `granular` | `Granular` | no |  | Default granular voice for notes in an rs_ resample Pattern. |
| `lenBeats` | `number` | no | `4` | ≥ 0.5 — Pattern cycle length in quarter-note beats. |
| `extends` | `string` | at least one of instrument/extends |  | One of the keys in Score.patterns Dictionary<string, Pattern>. The parent is inherited before local fields and notes are applied. |
| `motif` | `string` | no |  | One of the keys in Score.motifs Dictionary<string, Motif>. Its pitched notes are prepended to local notes. |
| `motifTransform` | `MotifTransform` | no |  | Transforms all pitched material produced by this Pattern, including motif notes and local notes. |
| `omit` | `number[]` | no |  | Local onset beats to remove after inheritance and motif expansion. Applied after only when both are present. |
| `only` | `number[]` | no |  | Local onset beats to retain after inheritance and motif expansion; notes at every other onset are removed. |

### Constraints

- extends must resolve and must not form a cycle. It inherits the resolved parent instrument, lenBeats, notes, controls, swing, humanize, groove, bus, depth, tone, pan, lateMs, flamMs, choke, and granular. Local scalar values override, controls merge by key, and local notes are appended; child motif, motifTransform, omit, and only apply locally after inheritance.
- motif and motifTransform require a pitched instrument.
- Every Note object requires b >= 0 and may use durB; t and dur are not legal inside a Pattern. A compact NoteLine uses beats by context.

### Related

[`InstrumentName`](#instrumentname) · [`NoteLine`](#noteline) · [`Note`](#note) · [`TrackControls`](#trackcontrols) · [`GrooveBinding`](#groovebinding) · [`TrackBusName`](#trackbusname) · [`Depth`](#depth) · [`Tone`](#tone) · [`Granular`](#granular) · [`MotifTransform`](#motiftransform)

## Placement

Place and optionally develop one named Pattern on the global score timeline. Processing order is motifTransform, repetition selection, Variation merge, repeat-local Transform, note probability, volume/transpose, then groove and timing.

### Syntax

```text
{ "pattern": …, ["atBeat": …], ["repeat": …], ["vol": …], ["volFrom": …], ["volTo": …], ["transpose": …], ["motifTransform": …], ["transform": …], ["condition": …], ["variations": …], ["groove": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `pattern` | `string` | yes |  | One of the keys in Score.patterns Dictionary<string, Pattern>. |
| `atBeat` | `number` | no | `0` | ≥ 0 — Placement start on the global score timeline, in beats. |
| `repeat` | `integer` | no | `1` | ≥ 1; ≤ 256 — Number of pattern cycles. |
| `vol` | `number` | no | `1` | > 0 — Placement gain multiplier. |
| `volFrom` | `number` | no | Placement.vol | ≥ 0.01; ≤ 1 — Gain multiplier at the beginning of the complete declared placement timeline. |
| `volTo` | `number` | no | Placement.vol | ≥ 0; ≤ 1 — Gain multiplier at the end of the complete declared placement timeline; 0 fades to silence. |
| `transpose` | `integer` | no | `0` | ≥ -96; ≤ 96 — Placement-wide semitone transposition applied after the repeat-local Transform. |
| `motifTransform` | `MotifTransform` | no |  | Transforms the complete pitched Pattern before repetitions are selected; rhythm also scales repeat spacing. |
| `transform` | `Transform` | no |  | Base repeat-local Transform applied independently to every repetition that passes Condition. |
| `condition` | `Condition` | no |  | Selects which one-based repetitions emit notes. |
| `variations` | `Variation[]` | no |  | 1..16 items — Seeded mutually exclusive candidates. Exactly one is merged over transform for each active repetition. |
| `groove` | `GrooveBinding` | no |  | Placement-level groove override resolved after Pattern and Score groove settings. |

### Constraints

- pattern must resolve. volFrom and volTo use vol as an omitted endpoint; their ramp follows the declared placement timeline and is not compressed when Condition removes repetitions.
- Condition is evaluated before Variation selection. A selected Variation overrides only matching fields in transform.
- motifTransform pitch fields and Transform pitch fields require a pitched Pattern.

### Related

[`MotifTransform`](#motiftransform) · [`Transform`](#transform) · [`Condition`](#condition) · [`Variation`](#variation) · [`GrooveBinding`](#groovebinding)

## Trigger

Silent repeating control pattern for rhythmic pumping and bus sidechain ducking. It schedules detector events and never renders an instrument.

### Syntax

```text
{ "lenBeats": …, "hits": …, "placements": … }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `lenBeats` | `number` | yes |  | > 0; ≤ 256 — Length of one trigger cycle in beats. |
| `hits` | `number[]` | yes |  | 1..256 items — Unique local trigger positions, each less than lenBeats. |
| `placements` | `TriggerPlacement[]` | yes |  | 1..256 items — Global placements of this trigger pattern. |

### Constraints

- Every hit is finite, unique, at least 0, and strictly less than lenBeats.
- Trigger events outside score.durationSec are discarded; each declared Trigger must retain at least one event inside the score.
- hits and placements array order has no effect. Coincident events created by different placements collapse into one detector event.
- The complete Score may retain at most 100000 unique Trigger events after duration clipping and coincidence removal.
- Triggers generate no audio and do not require an instrument.

### Related

[`TriggerPlacement`](#triggerplacement)

## TriggerPlacement

Place and optionally repeat one silent Trigger pattern on the global beat timeline. Array order has no effect; every placement carries its own absolute atBeat.

### Syntax

```text
{ "atBeat": …, ["repeat": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `atBeat` | `number` | yes |  | ≥ 0 — Global placement start in beats. |
| `repeat` | `integer` | no | `1` | ≥ 1; ≤ 256 — Consecutive lenBeats cycles. |

## Transform

Repeat-local rhythmic, pitch, density, and accent development. Omitted fields make no change.

### Syntax

```text
{ ["reverse": …], ["rotate": …], ["stretch": …], ["gate": …], ["invert": …], ["diatonic": …], ["chromatic": …], ["octave": …], ["density": …], ["accent": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `reverse` | `boolean` | no | `false` | Reverse event groups over the existing onset positions; unlike MotifTransform.retrograde, the onset positions themselves stay fixed. |
| `rotate` | `number` | no | `0` | ≥ -4096; ≤ 4096 — Circular beat displacement wrapped inside the repetition's lenBeats. |
| `stretch` | `number` | no | `1` | ≥ 0.0625; ≤ 16 — Multiplier for local starts and explicit durations. Repeat spacing stays fixed; starts beyond lenBeats are removed. |
| `gate` | `number` | no | `1` | ≥ 0.05; ≤ 4 — Multiplier applied to explicit durations after stretch and density. |
| `invert` | `boolean` | no | `false` | Mirror the scale-degree contour around the earliest pitched note after timing transforms. Requires a pitched instrument and Score.harmony. |
| `diatonic` | `integer` | no | `0` | ≥ -64; ≤ 64 — Scale-step transposition. Requires a pitched instrument and Score.harmony. |
| `chromatic` | `integer` | no | `0` | ≥ -96; ≤ 96 — Semitone transposition. Requires a pitched instrument. |
| `octave` | `integer` | no | `0` | ≥ -8; ≤ 8 — Final octave displacement. Requires a pitched instrument. |
| `density` | `number` | no | `1` | ≥ 0; ≤ 4 — Seeded onset-group density: 0 removes all, below 1 thins, 1 is unchanged, and above 1 creates bounded retriggers. |
| `accent` | `number[]` | no |  | 1..128 items — One or more 0..2 velocity multipliers cycled over chronological onset groups; resulting note volume is clamped to 0..1. |

### Constraints

- Operations run in this fixed order: reverse, rotate, stretch, pitch, density, gate, accent, then repetition-boundary clipping.
- Final starts outside 0 <= beat < lenBeats are removed; explicit durations crossing lenBeats are shortened to the boundary.
- When merged from a Variation, only supplied fields override the Placement's base Transform.

## Condition

AND-combined selector for one-based Placement repetitions. An empty Condition selects every repetition.

### Syntax

```text
{ ["first": …], ["last": …], ["everyNth": …], ["alternate": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `first` | `boolean` | no |  | true selects only repeat 1; false excludes it. |
| `last` | `boolean` | no |  | true selects only the final repeat; false excludes it. |
| `everyNth` | `integer` | no |  | ≥ 1; ≤ 256 — Select repeats N, 2N, 3N, and so on. |
| `alternate` | `RepeatParity` | no |  | Select odd- or even-numbered repetitions. |

### Constraints

- All supplied selectors must match. Contradictory combinations are valid and select no repetitions.

### Related

[`RepeatParity`](#repeatparity)

## RepeatParity

String enum selecting odd- or even-numbered one-based Placement repetitions.

### Syntax

```text
"odd" | "even"
```

### Values

`"odd"` · `"even"`

## Variation

One relative-weight candidate in a seeded mutually exclusive group. Exactly one Variation is selected for every repetition that passes Condition.

### Syntax

```text
{ ["weight": …], ["transform": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `weight` | `number` | no | `1` | ≥ 0.000001; ≤ 1000 — Relative selection weight, not a percentage. |
| `transform` | `Transform` | no |  | Fields that override matching fields from Placement.transform. Omission keeps the base Transform unchanged, allowing a weighted no-additional-change candidate. |

### Related

[`Transform`](#transform)

## Track

Plain seconds-addressed lane. Every Note object requires t in seconds; a compact NoteLine's first value is also seconds. Use Pattern + Placement for beat-addressed repetition.

### Syntax

```text
{ "id": …, "instrument": …, ["notes": …], ["controls": …], ["swing": …], ["humanize": …], ["groove": …], ["bus": …], ["depth": …], ["tone": …], ["pan": …], ["lateMs": …], ["flamMs": …], ["choke": …], ["granular": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[A-Za-z0-9_-]{1,48}$` — Required identity for this Track. It must be unique among all objects in top-level tracks and is referenced by Sweep.track, resampling, and routing. |
| `instrument` | `InstrumentName` | yes |  | Exact public sound used by this lane. |
| `notes` | `(NoteLine \| Note)[]` | no | [] | Seconds-addressed notes for this lane. Every Note object requires t; every compact NoteLine starts with its time in seconds. |
| `controls` | `TrackControls` | no | {} |  |
| `swing` | `number` | no | Score.swing (default 0) | ≥ 0; ≤ 10 — Lane swing override. |
| `humanize` | `number` | no | Score.humanize (default 0) | ≥ 0; ≤ 10 — Lane timing and velocity humanization override. |
| `groove` | `GrooveBinding` | no |  | Lane groove resolved after Score.groove; omission inherits Score.groove, or applies no groove when the Score also omits it. |
| `bus` | `TrackBusName` | no | automatic instrument role | Explicit mixer destination. Omission uses the instrument's automatic role: kit drums to kit, declared percussion to perc, factory bass roles to bass, transition roles to fx, and other material to bed. |
| `depth` | `Depth` | no | "mid" | Front/back placement; omission means mid. |
| `tone` | `Tone` | no | neutral | Spectral character; omission means neutral. |
| `pan` | `number` | no | `0` | ≥ -1; ≤ 1 — Static lane pan. A Note.pan value overrides it for that note. |
| `lateMs` | `number` | no | `0` | Timing offset applied to every note, in milliseconds. |
| `flamMs` | `number` | no | `25` | ≥ 5; ≤ 60 — Spacing between a drum note's flam grace hit and main hit, in milliseconds; has no effect without Note.flam. |
| `choke` | `boolean` | no | `true` | Whether later kit-bus hat/openhat onsets cut this lane's ringing open-hi-hat tails; relevant only to open-hi-hat material on the kit bus. |
| `granular` | `Granular` | no |  | Lane-level default for notes on an rs_ resample instrument. A Note.granular value overrides it. |

### Constraints

- Track rejects unknown properties. Every Note object in notes requires a finite t >= 0 in seconds; b and durB are not legal inside a Track.
- TrackControls rejects unknown properties and requires numeric controls to be JSON numbers within their documented ranges.

### Related

[`InstrumentName`](#instrumentname) · [`NoteLine`](#noteline) · [`Note`](#note) · [`TrackControls`](#trackcontrols) · [`GrooveBinding`](#groovebinding) · [`TrackBusName`](#trackbusname) · [`Depth`](#depth) · [`Tone`](#tone) · [`Granular`](#granular)

## Motif

Reusable pitched phrase in beats, independent of an instrument.

### Syntax

```text
{ ["notes": …], ["lenBeats": …], ["extends": …], ["transform": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `notes` | `(NoteLine \| Note)[]` | at least one of notes/extends |  | 1..∞ items — Non-empty pitched phrase. Note objects use b and durB in beats; compact NoteLine time and duration are also beats. |
| `lenBeats` | `number` | no | parent Motif.lenBeats when extends is set; otherwise 4 | ≥ 0.0625 — Phrase boundary in quarter-note beats; it determines the inherited cycle length and the boundary used by retrograde. |
| `extends` | `string` | at least one of notes/extends |  | Exact key of another Motif in Score.motifs. The resolved parent notes come first, local notes are appended, and this Motif's transform is then applied to the merged phrase. |
| `transform` | `MotifTransform` | no |  | Applied after inheritance to the resolved parent notes followed by this Motif's local notes. |

### Constraints

- Every declared Motif is validated, including motifs that no Pattern uses. Unknown properties are rejected.
- Every Note object requires b >= 0 and may use durB; t and dur are not legal inside a Motif. A compact NoteLine uses beats by context.
- extends must resolve and remain acyclic. Parent notes are resolved first, local notes are appended, and the child transform is applied last.

### Related

[`NoteLine`](#noteline) · [`Note`](#note) · [`MotifTransform`](#motiftransform)

## MotifTransform

Transformation of a pitched note list. Operations run in a fixed order: resolve degrees and chords, retrograde, rhythm, inversion, diatonic movement, chromatic and octave movement, then voice-leading, range, and maximum-leap fitting.

### Syntax

```text
{ ["diatonic": …], ["chromatic": …], ["invert": …], ["retrograde": …], ["octave": …], ["rhythm": …], ["chord": …], ["voiceLead": …], ["register": …], ["range": …], ["maxLeap": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `diatonic` | `integer` | no | `0` | ≥ -64; ≤ 64 — Scale-step transposition. Requires top-level Score.harmony. |
| `chromatic` | `integer` | no | `0` | ≥ -96; ≤ 96 — Semitone transposition. |
| `invert` | `boolean` | no | `false` | Mirror the scale-degree contour around the earliest note by local onset. Requires top-level Score.harmony. |
| `retrograde` | `boolean` | no | `false` | Mirror each onset inside the unscaled phrase length while preserving its pitch and duration; this changes event times, not array order. |
| `octave` | `integer` | no | `0` | ≥ -8; ≤ 8 — Final octave displacement. |
| `rhythm` | `number` | no | `1` | ≥ 0.0625; ≤ 16 — Multiplier for local onsets, durations, and the resulting phrase/cycle length or Placement repeat spacing. |
| `chord` | `string` | no |  | One of the keys in Score.harmony.chords Dictionary<string, Chord>. Requires voiceLead: true. |
| `voiceLead` | `boolean` | no | `false` | When true, requires chord and snaps notes in chronological order to nearby pitch classes from that chord. |
| `register` | `integer` | no |  | ≥ -1; ≤ 8 — Fallback octave for scale-degree tokens without @octave and chord events without Note.octave. If omitted, uses Harmony.octave; explicit note octaves win. |
| `range` | `PitchRange` | no |  | Inclusive final pitch range. Without voiceLead, notes are moved only by whole octaves to fit; compilation fails when no matching octave fits. |
| `maxLeap` | `integer` | no |  | ≥ 0; ≤ 48 — Hard maximum between chronologically adjacent output notes, in semitones. The compiler chooses the nearest valid octave and fails when none satisfies the limit. |

### Constraints

- invert and nonzero diatonic require top-level Score.harmony; chord must resolve in Score.harmony.chords and may be supplied only with voiceLead: true.
- register affects only scale-degree tokens and chord events that do not carry their own octave. range and maxLeap also work on absolute pitches without harmony.
- At equal onset times, original array order is the deterministic tie-breaker for inversion and voice-leading.

### Related

[`PitchRange`](#pitchrange)

## Harmony

Tonality, reusable voicings, and named chords resolved before rendering.

### Syntax

```text
{ ["tonic": …], ["scale": …], ["pitchSet": …], ["octave": …], ["voicings": …], ["chords": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `tonic` | `string` | no | `"C"` | pattern `^[A-Ga-g][b#]?$` — Pitch class such as C, Bb, or F#. |
| `scale` | `ScaleName` | no | `"major"` | Built-in scale name. |
| `pitchSet` | `integer[]` | no |  | 1..12 items — Custom ascending unique semitone offsets; must include 0. |
| `octave` | `integer` | no | `4` | ≥ -1; ≤ 8 — Default register for degree tokens. |
| `voicings` | `Dictionary<string, integer[]>` | no | `{}` | Reusable named chord voicings. Each value contains one -4..4 octave offset per chord tone. |
| `chords` | `Dictionary<string, Chord>` | no | `{}` | Named chord definitions. Each dictionary key is a valid value for Note.chord. |

### Constraints

- An omitted Harmony property uses C as tonic, major as scale, octave 4, and empty voicings/chords dictionaries. The top-level Harmony object itself is required whenever a scale-degree token is used.
- pitchSet and scale are alternative scale definitions; pitchSet must be sorted, unique, and contain 0.
- When a Chord references a named voicing, that voicing's length must match the Chord.tones count.
- Every declared voicing and Chord is validated even when no Note references it. Unknown properties are rejected.

### Related

[`ScaleName`](#scalename) · [`Chord`](#chord)

## ScaleName

String enum selecting one built-in musical scale, generated from the compiler's scale table.

### Syntax

```text
"major"
| "ionian"
| "minor"
| "natural_minor"
| "aeolian"
| "harmonic_minor"
| "melodic_minor"
| "dorian"
| "phrygian"
| "lydian"
| "mixolydian"
| "locrian"
| "pentatonic_major"
| "pentatonic_minor"
| "blues"
| "chromatic"
```

### Values

`"major"` · `"ionian"` · `"minor"` · `"natural_minor"` · `"aeolian"` · `"harmonic_minor"` · `"melodic_minor"` · `"dorian"` · `"phrygian"` · `"lydian"` · `"mixolydian"` · `"locrian"` · `"pentatonic_major"` · `"pentatonic_minor"` · `"blues"` · `"chromatic"`

## Chord

One named harmony chord definition stored under a key in Score.harmony.chords. A Note.chord event expands its tones simultaneously unless strumMs or arp changes their timing.

### Syntax

```text
{ "tones": …, ["voicing": …], ["range": …], ["maxLeap": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `tones` | `PitchToken[]` | yes |  | 1..16 items — Scale degrees or absolute pitches expanded by a Note.chord event. |
| `voicing` | `ChordVoicing` | no | 0 for every tone | Named Harmony.voicings key or one octave offset per tone. |
| `range` | `PitchRange` | no | unrestricted MIDI range | Default inclusive pitch range for this chord. Tones move only by whole octaves to fit. |
| `maxLeap` | `integer` | no | unrestricted | ≥ 0; ≤ 48 — Default maximum movement per corresponding chord voice, used only when a Note.chord event sets voiceLead: true. |

### Related

[`PitchToken`](#pitchtoken) · [`ChordVoicing`](#chordvoicing) · [`PitchRange`](#pitchrange)

## Groove

One meter-length timing and velocity pocket map.

### Syntax

```text
{ ["meter": …], ["stepsPerBeat": …], ["timingMs": …], ["velocity": …], ["accent": …], ["phaseBeat": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `meter` | `[integer, MeterDenominator]` | no | `[4,4]` | 2..2 items — Time signature written as [numerator, denominator]. |
| `stepsPerBeat` | `integer` | no | `4` | ≥ 1; ≤ 16 — Grid steps per quarter-note beat. |
| `timingMs` | `number[]` | at least one of timingMs/velocity/accent | [0, …] | Signed timing offset per cycle step. |
| `velocity` | `number[]` | at least one of timingMs/velocity/accent | [1, …] | Velocity multiplier per cycle step. |
| `accent` | `number[]` | at least one of timingMs/velocity/accent | [0, …] | Emphasis mapped to a 0.5..1.5 velocity multiplier. |
| `phaseBeat` | `number` | no | `0` | ≥ -1000000; ≤ 1000000 — Global score beat at which step zero begins. |

### Constraints

- Every supplied array has meterNumerator * 4 / meterDenominator * stepsPerBeat entries.
- The computed cycle length must be 1..256 whole steps.
- Notes read the nearest subdivision step without quantizing their authored onset. The selected timing offset is clamped to 45% of the real local subdivision so adjacent grid events cannot cross.
- The target force at one step is velocity[step] * (1 + accent[step] * 0.5).
- Every declared Groove is validated even when no lane uses it. Unknown properties and non-numeric JSON values are rejected.

### Related

[`MeterDenominator`](#meterdenominator)

## MeterDenominator

Numeric enum selecting the beat unit used as a time-signature denominator.

### Syntax

```text
1 | 2 | 4 | 8 | 16
```

### Values

`1` · `2` · `4` · `8` · `16`

## GrooveBinding

A groove name, true to inherit, false to opt out, or a configured GrooveUse.

### Syntax

```text
one of the keys in Score.grooves Dictionary<string, Groove> | boolean | GrooveUse
```

### Constraints

- String/map names must resolve to a top-level grooves key.
- Bindings resolve from Score.groove to Track/Pattern.groove to Placement.groove. true preserves the inherited choice, false clears it, and a GrooveUse overrides only the fields it supplies.
- Score.groove is validated even when the score currently contains no lane that inherits it.

### Related

[`GrooveUse`](#grooveuse)

## Sweep

One compact knob or exact parameter on selected tracks, moved by keyframes or a finite LFO.

### Syntax

```text
{ ["track": …], ["pattern": …], ["instrument": …], ["knob": …], ["param": …], ["points": …], ["lfo": …], ["res": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `track` | `string` | exactly one of track/pattern/instrument |  | The id property of one direct Track in top-level tracks. The sweep applies only to that authored Track across its complete score timeline. |
| `pattern` | `string` | exactly one of track/pattern/instrument |  | One exact key from the top-level patterns object. The sweep applies to every arrangement placement of that Pattern, but not to Patterns that extend it. |
| `instrument` | `string` | exactly one of track/pattern/instrument |  | The instrument property of a Track or Pattern. The sweep applies globally to every direct Track and arranged Pattern using it, regardless of bus. |
| `knob` | `SweepKnob` | exactly one of knob/param |  | Compact 0..10 target. fader/pan are intentionally absent. |
| `param` | `TrackParam` | exactly one of knob/param |  |  |
| `points` | `Keyframe[]` | exactly one of points/lfo |  | 2..64 items — Strictly ascending beat-addressed keyframes. |
| `lfo` | `Lfo` | exactly one of points/lfo |  |  |
| `res` | `number` | no |  | ≥ 0; ≤ 10 — Optional resonance state change for a compact lowpass/highpass sweep. It begins at points[0][0] or lfo.atBeat and holds for this track + filter until a later sweep supplies res. |

### Constraints

- Exactly one of track/pattern/instrument is required.
- track resolves against the id property of one direct Track in top-level tracks.
- pattern resolves only against one exact top-level patterns key. All arrangement placements receive the sweep; Patterns that extend it do not.
- instrument resolves against the instrument property of direct Tracks and arranged Patterns. Every match receives the sweep, regardless of bus.
- Target names are case-sensitive. A target that resolves to nothing is an error.
- Exactly one of knob/param and exactly one of points/lfo are required.
- points contains 2..64 strictly ascending beat-addressed keyframes.
- A knob LFO is legal only for lowpass/highpass/pump and uses compact 0..10 units. A param LFO requires center and uses that param's native units.
- res is legal only with compact knob lowpass/highpass; it is an error on every other knob or exact param.
- Lowpass and highpass resonance are independent per track. Each starts at controls.res when present, otherwise 0. Omitting res retains that filter's current value.
- A res value takes effect at the sweep's first point and holds until a later sweep for the same track + filter supplies another value. Conflicting values at the same beat are errors; automation array order has no effect.
- Compact synth knobs, including cutoff/resonance/drive, are sampled at note onsets; their synth.* exact-param counterparts move continuously inside held notes.

### Examples

```json
{
  "track": "BASS_TRACK",
  "knob": "lowpass",
  "points": [
    [
      0,
      8
    ],
    [
      8,
      2
    ]
  ],
  "res": 5
}
```

```json
{
  "pattern": "BASS",
  "knob": "highpass",
  "points": [
    [
      16,
      0
    ],
    [
      24,
      8
    ]
  ],
  "res": 8
}
```

```json
{
  "instrument": "glass_lead",
  "param": "track.pan",
  "lfo": {
    "atBeat": 16,
    "beats": 8,
    "period": 2,
    "depth": 1,
    "center": 0
  }
}
```

### Related

[`SweepKnob`](#sweepknob) · [`TrackParam`](#trackparam) · [`Keyframe`](#keyframe) · [`Lfo`](#lfo) · [`FilterSweepKnob`](#filtersweepknob) · [`KnobKeyframe`](#knobkeyframe) · [`LfoSweepKnob`](#lfosweepknob) · [`CompactLfo`](#compactlfo) · [`AutomationCurve`](#automationcurve) · [`CenteredLfo`](#centeredlfo)

## SweepKnob

String enum selecting one compact 0..10 Sweep target.

### Syntax

```text
"lowpass"
| "highpass"
| "pump"
| "cutoff"
| "resonance"
| "envMod"
| "attack"
| "decay"
| "sustain"
| "release"
| "drive"
| "detune"
| "sub"
| "noise"
| "lfoRate"
| "wobble"
| "vibrato"
| "sweep"
| "pitchDrop"
| "vol"
```

### Values

`"lowpass"` · `"highpass"` · `"pump"` · `"cutoff"` · `"resonance"` · `"envMod"` · `"attack"` · `"decay"` · `"sustain"` · `"release"` · `"drive"` · `"detune"` · `"sub"` · `"noise"` · `"lfoRate"` · `"wobble"` · `"vibrato"` · `"sweep"` · `"pitchDrop"` · `"vol"`

### Constraints

- fader and pan are intentionally absent; use TrackParam track.fader or track.pan.

## FilterSweepKnob

String enum selecting a compact track filter whose resonance can be changed by Sweep.res.

### Syntax

```text
"lowpass" | "highpass"
```

### Values

`"lowpass"` · `"highpass"`

## LfoSweepKnob

String enum selecting a compact Sweep target that supports continuous LFO movement.

### Syntax

```text
"lowpass" | "highpass" | "pump"
```

### Values

`"lowpass"` · `"highpass"` · `"pump"`

## BusSweep

Native-unit automation of one declared custom bus, effect, or send property.

### Syntax

```text
{ "bus": "<Score.buses key>", "param": BusSweepParam, "points": [Keyframe, ...] }
{ "bus": "<Score.buses key>", "effect": "<Bus.effects id>", "param": BusSweepParam, "points": [Keyframe, ...] }
{ "bus": "<Score.buses key>", "send": "<Bus.sends id>", "param": "amount", "points": [Keyframe, ...] }
{ "bus": "<Score.buses key>", "param": BusSweepParam, "lfo": CenteredLfo }
{ "bus": "<Score.buses key>", "effect": "<Bus.effects id>", "param": BusSweepParam, "lfo": CenteredLfo }
{ "bus": "<Score.buses key>", "send": "<Bus.sends id>", "param": "amount", "lfo": CenteredLfo }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `bus` | `string` | yes |  | Case-sensitive exact key from Score.buses. This always selects the containing custom Bus. |
| `effect` | `string` | no |  | Case-sensitive id of one effect in the selected Bus. When present, param selects a property of this effect. |
| `send` | `string` | no |  | Case-sensitive id of one send in the selected Bus. When present, param must be amount. |
| `param` | `BusSweepParam` | yes |  |  |
| `points` | `Keyframe[]` | exactly one of points/lfo |  | 2..64 items — Strictly ascending beat-addressed keyframes whose values use the selected property's native units. |
| `lfo` | `CenteredLfo` | exactly one of points/lfo |  | Finite native-unit LFO. It starts and finishes at center, and its full excursion must fit the selected property's range. |

### Constraints

- The three target forms are: bus alone changes the Bus itself; bus + effect changes that effect; bus + send changes that send. effect and send must never appear together.
- bus must resolve to a declared custom Bus. effect and send ids resolve only inside that Bus. All references are case-sensitive; an unresolved reference is an error.
- Bus properties: fader 0..1; pan -1..1; sidechain.amount 0..10, only when that Bus declares sidechain.
- Send property: amount 0..1 is the only automatable send property.
- Effect properties: eq low/mid/high -12..12 dB and mix 0..1; drive/crush/tape amount 0..10 and mix 0..1; chorus/phaser rateHz 0.01..10, depth 0..1, feedback -0.9..0.9, and mix 0..1; delay timeBeats 0.0625..4, feedback 0..0.92, and mix 0..1; reverb size/damping/mix 0..1 and tone -1..1; filter cutoff 30..16000 Hz, resonance 0..0.9, and mix 0..1; width amount 0..2; tremolo rateHz 0.01..20 and depth/mix 0..1.
- Only an existing numeric property may move. Routing, ids, effect types, and filter mode remain static.
- Before the earliest keyframe, the selected property's configured value remains active. After the latest keyframe, its value holds.
- Several BusSweep entries for the same property merge into one time-sorted envelope. Values interpolate across a gap; to hold across it, begin the later entry at the held value.
- Conflicting points at the same beat are errors; automation array order has no effect.
- Point values and the complete LFO excursion must stay inside the selected property's native range; out-of-range values are errors.
- A CenteredLfo begins at center, returns to center at its ending beat, and then holds center until later automation changes the property.

### Examples

```json
{
  "bus": "music",
  "param": "fader",
  "points": [
    [
      0,
      1
    ],
    [
      8,
      0.5
    ]
  ]
}
```

```json
{
  "bus": "music",
  "effect": "echo",
  "param": "feedback",
  "points": [
    [
      0,
      0.2
    ],
    [
      8,
      0.7
    ]
  ]
}
```

```json
{
  "bus": "music",
  "send": "hall_send",
  "param": "amount",
  "points": [
    [
      0,
      0.1
    ],
    [
      8,
      0.8
    ]
  ]
}
```

### Related

[`BusSweepParam`](#bussweepparam) · [`Keyframe`](#keyframe) · [`CenteredLfo`](#centeredlfo)

## BusSweepParam

String enum selecting the numeric custom-Bus, effect, or send property moved by a BusSweep. The selected bus object determines which enum values are legal.

### Syntax

```text
"fader"
| "pan"
| "sidechain.amount"
| "amount"
| "low"
| "mid"
| "high"
| "mix"
| "rateHz"
| "depth"
| "feedback"
| "timeBeats"
| "size"
| "damping"
| "tone"
| "cutoff"
| "resonance"
```

### Values

`"fader"` · `"pan"` · `"sidechain.amount"` · `"amount"` · `"low"` · `"mid"` · `"high"` · `"mix"` · `"rateHz"` · `"depth"` · `"feedback"` · `"timeBeats"` · `"size"` · `"damping"` · `"tone"` · `"cutoff"` · `"resonance"`

### Value ranges

| Value / target | Range |
|---|---|
| `fader` | Bus property only; 0..1 |
| `pan` | Bus property only; -1..1 |
| `sidechain.amount` | Bus property only; 0..10; the selected Bus must declare sidechain |
| `amount` | Send 0..1; drive/crush/tape effect 0..10; width effect 0..2 |
| `low` | eq effect only; -12..12 dB |
| `mid` | eq effect only; -12..12 dB |
| `high` | eq effect only; -12..12 dB |
| `mix` | Any effect except width; 0..1 |
| `rateHz` | chorus/phaser 0.01..10 Hz; tremolo 0.01..20 Hz |
| `depth` | chorus/phaser/tremolo effect only; 0..1 |
| `feedback` | chorus/phaser -0.9..0.9; delay 0..0.92 |
| `timeBeats` | delay effect only; 0.0625..4 beats |
| `size` | reverb effect only; 0..1 |
| `damping` | reverb effect only; 0..1 |
| `tone` | reverb effect only; -1..1 |
| `cutoff` | filter effect only; 30..16000 Hz |
| `resonance` | filter effect only; 0..0.9 |

## Keyframe

Automation point [beat, value, curve?]. Curve shapes the segment into this point.

### Syntax

```text
[beat, value]
[beat, value, curve]
```

### Constraints

- The optional curve belongs to the destination keyframe: it shapes movement from the previous keyframe into this one. Omitting it means linear. A curve on the first keyframe has no effect.
- Within a segment, let f run from 0 at the previous keyframe to 1 at the destination. linear uses f; exp uses f^3; log uses 1-(1-f)^3; scurve uses f^2*(3-2*f).
- step holds the previous keyframe's value for the whole segment, then jumps to the destination value exactly at the destination beat.

### Examples

```json
[
  32,
  2
]
```

```json
[
  64,
  8,
  "exp"
]
```

### Related

[`AutomationCurve`](#automationcurve)

## AutomationCurve

String enum controlling interpolation into an automation keyframe.

### Syntax

```text
"linear" | "exp" | "log" | "scurve" | "step"
```

### Values

`"linear"` · `"exp"` · `"log"` · `"scurve"` · `"step"`

## Lfo

Tempo-synchronized sine automation over a finite beat window.

### Syntax

```text
{ "atBeat": …, "beats": …, "period": …, "depth": …, ["center": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `atBeat` | `number` | yes |  | ≥ 0 — LFO start on the global score timeline, in beats. |
| `beats` | `number` | yes |  | > 0 — LFO duration in beats. |
| `period` | `number` | yes |  | > 0 — Beats per sine cycle. |
| `depth` | `number` | yes |  | > 0 — Full swing width in target units. |
| `center` | `number` | no |  | Resting value; required for exact param automation. |

## TrackParam

Exact continuous target in native units. This is how fader and pan are automated.

### Syntax

```text
"track.fader" | "track.pan" | "synth.cutoff" | "synth.resonance" | "synth.drive" | "synth.blend" | "synth.sync" | "synth.ring" | "synth.shape" | "synth.pitch1" | "synth.pitch2"
```

### Values

`"track.fader"` · `"track.pan"` · `"synth.cutoff"` · `"synth.resonance"` · `"synth.drive"` · `"synth.blend"` · `"synth.sync"` · `"synth.ring"` · `"synth.shape"` · `"synth.pitch1"` · `"synth.pitch2"`

### Value ranges

| Value / target | Range |
|---|---|
| `track.fader` | 0..1 |
| `track.pan` | -1..1 |
| `synth.cutoff` | 30..16000 Hz |
| `synth.resonance` | 0..0.9 |
| `synth.drive` | 1..8 |
| `synth.blend` | 0..1 |
| `synth.sync` | 0..1 |
| `synth.ring` | 0..1 |
| `synth.shape` | 0..1 |
| `synth.pitch1` | -48..48 semitones |
| `synth.pitch2` | -48..48 semitones |

### Constraints

- synth.* targets require a synthesized instrument.
- blend/sync/ring/shape/pitch1/pitch2 require an ex_ dual-oscillator patch.

## MasterMove

A bounded master-bus performance move.

### Syntax

```text
{ "fx": …, "atBeat": …, "beats": …, ["unitBeats": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `fx` | `MasterMoveEffect` | yes |  |  |
| `atBeat` | `number` | yes |  | ≥ 0 — Move start on the global score timeline, in beats. |
| `beats` | `number` | yes |  | > 0 — Move duration in beats. |
| `unitBeats` | `number` | no | `0.25` | > 0 — Stutter slice length in beats. On another move it is still validated as positive, then has no audio effect. |

### Related

[`MasterMoveEffect`](#mastermoveeffect)

## MasterMoveEffect

String enum selecting one bounded master-bus performance effect.

### Syntax

```text
"killLow" | "killHigh" | "tapeStop" | "stutter" | "narrow" | "open"
```

### Values

`"killLow"` · `"killHigh"` · `"tapeStop"` · `"stutter"` · `"narrow"` · `"open"`

## Bus

Declared custom mixing bus. Its Score.buses object key is its routing identity. The completed Bus is mixed into the built-in role selected by role.

### Syntax

```text
{ ["role": …], ["effects": …], ["sends": …], ["sidechain": …], ["fader": …], ["pan": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `role` | `BusRole` | no | `"bed"` | Built-in role bus that receives this custom Bus's completed output. |
| `effects` | `BusEffect[]` | no | `[]` | 0..8 items — Insert chain processed in array order; changing the order can change the sound. |
| `sends` | `Send[]` | no | `[]` | 0..8 items — Parallel feeds processed in array order after this Bus's fader and pan; each Send.tap chooses pre or post audio. |
| `sidechain` | `Sidechain` | no |  |  |
| `fader` | `number` | no | `1` | ≥ 0; ≤ 1 — Static bus fader. |
| `pan` | `number` | no | `0` | ≥ -1; ≤ 1 — Static bus pan. |

### Constraints

- Every supplied numeric value must be a JSON number inside its documented range; values are never coerced or clamped.
- Effect ids are unique among this Bus's effects, and send ids are unique among this Bus's sends. The two id namespaces are separate.
- The complete custom-bus send and sidechain graph must be acyclic.
- A custom Bus can be a duckable effect return: send audio to it, use a reverb or delay with mix 1, and put sidechain on that return Bus. Built-in hall and plate returns are not sidechain targets.

### Related

[`BusRole`](#busrole) · [`BusEffect`](#buseffect) · [`Send`](#send) · [`Sidechain`](#sidechain)

## BusRole

String enum selecting the mixer behavior inherited by a custom Bus.

### Syntax

```text
"kit" | "perc" | "bass" | "bed" | "lead" | "fx"
```

### Values

`"kit"` · `"perc"` · `"bass"` · `"bed"` · `"lead"` · `"fx"`

## BusEffect

Strict discriminated bus insert. The type selects the legal parameter set.

### Syntax

```text
{ "id": …, "type": …, ["low": …], ["mid": …], ["high": …], ["mix": …] }
| { "id": …, "type": …, ["amount": …], ["mix": …] }
| { "id": …, "type": …, ["amount": …], ["mix": …] }
| { "id": …, "type": …, ["amount": …], ["mix": …] }
| { "id": …, "type": …, ["rateHz": …], ["depth": …], ["feedback": …], ["mix": …] }
| { "id": …, "type": …, ["rateHz": …], ["depth": …], ["feedback": …], ["mix": …] }
| { "id": …, "type": …, ["timeBeats": …], ["feedback": …], ["mix": …] }
| { "id": …, "type": …, ["size": …], ["damping": …], ["tone": …], ["mix": …] }
| { "id": …, "type": …, ["mode": …], ["cutoff": …], ["resonance": …], ["mix": …] }
| { "id": …, "type": …, ["amount": …] }
| { "id": …, "type": …, ["rateHz": …], ["depth": …], ["mix": …] }
```

### Alternatives

#### Eq bus effect

Three-band equalizer.

##### Syntax

```text
{ "id": …, "type": …, ["low": …], ["mid": …], ["high": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"eq"` | yes |  | Effect discriminator. |
| `low` | `number` | no | `0` | ≥ -12; ≤ 12 — Low-band gain in dB. |
| `mid` | `number` | no | `0` | ≥ -12; ≤ 12 — Mid-band gain in dB. |
| `high` | `number` | no | `0` | ≥ -12; ≤ 12 — High-band gain in dB. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Drive bus effect

Saturation.

##### Syntax

```text
{ "id": …, "type": …, ["amount": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"drive"` | yes |  | Effect discriminator. |
| `amount` | `number` | no | `0` | ≥ 0; ≤ 10 — Drive amount. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Crush bus effect

Bit/sample-rate color.

##### Syntax

```text
{ "id": …, "type": …, ["amount": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"crush"` | yes |  | Effect discriminator. |
| `amount` | `number` | no | `0` | ≥ 0; ≤ 10 — Crush amount. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Tape bus effect

Tape color.

##### Syntax

```text
{ "id": …, "type": …, ["amount": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"tape"` | yes |  | Effect discriminator. |
| `amount` | `number` | no | `0` | ≥ 0; ≤ 10 — Tape amount. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Chorus bus effect

Tempo-independent chorus.

##### Syntax

```text
{ "id": …, "type": …, ["rateHz": …], ["depth": …], ["feedback": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"chorus"` | yes |  | Effect discriminator. |
| `rateHz` | `number` | no | `0.6` | ≥ 0.01; ≤ 10 — Modulation rate in Hz. |
| `depth` | `number` | no | `0.5` | ≥ 0; ≤ 1 — Modulation depth. |
| `feedback` | `number` | no | `0` | ≥ -0.9; ≤ 0.9 — Signed feedback. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Phaser bus effect

Tempo-independent phaser.

##### Syntax

```text
{ "id": …, "type": …, ["rateHz": …], ["depth": …], ["feedback": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"phaser"` | yes |  | Effect discriminator. |
| `rateHz` | `number` | no | `0.4` | ≥ 0.01; ≤ 10 — Modulation rate in Hz. |
| `depth` | `number` | no | `0.5` | ≥ 0; ≤ 1 — Modulation depth. |
| `feedback` | `number` | no | `0` | ≥ -0.9; ≤ 0.9 — Signed feedback. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Delay bus effect

Beat-synchronized delay.

##### Syntax

```text
{ "id": …, "type": …, ["timeBeats": …], ["feedback": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"delay"` | yes |  | Effect discriminator. |
| `timeBeats` | `number` | no | `0.75` | ≥ 0.0625; ≤ 4 — Delay time in beats. |
| `feedback` | `number` | no | `0.32` | ≥ 0; ≤ 0.92 — Feedback. |
| `mix` | `number` | no | `0.25` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Reverb bus effect

Algorithmic reverb.

##### Syntax

```text
{ "id": …, "type": …, ["size": …], ["damping": …], ["tone": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"reverb"` | yes |  | Effect discriminator. |
| `size` | `number` | no | `0.7` | ≥ 0; ≤ 1 — Room size. |
| `damping` | `number` | no | `0.35` | ≥ 0; ≤ 1 — High-frequency damping. |
| `tone` | `number` | no | `0` | ≥ -1; ≤ 1 — Dark to bright tone. |
| `mix` | `number` | no | `0.2` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Filter bus effect

Static low-pass or high-pass filter.

##### Syntax

```text
{ "id": …, "type": …, ["mode": …], ["cutoff": …], ["resonance": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"filter"` | yes |  | Effect discriminator. |
| `mode` | `BusFilterMode` | no | `"lowpass"` |  |
| `cutoff` | `number` | no | `3000` | ≥ 30; ≤ 16000 — Cutoff in Hz. |
| `resonance` | `number` | no | `0.1` | ≥ 0; ≤ 0.9 — Filter resonance. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

#### Width bus effect

Stereo width processor.

##### Syntax

```text
{ "id": …, "type": …, ["amount": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"width"` | yes |  | Effect discriminator. |
| `amount` | `number` | no | `1` | ≥ 0; ≤ 2 — 0 mono, 1 unchanged, 2 extra-wide. |

#### Tremolo bus effect

Tempo-independent amplitude modulation.

##### Syntax

```text
{ "id": …, "type": …, ["rateHz": …], ["depth": …], ["mix": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique effect id inside this bus. |
| `type` | `"tremolo"` | yes |  | Effect discriminator. |
| `rateHz` | `number` | no | `2` | ≥ 0.01; ≤ 20 — Modulation rate in Hz. |
| `depth` | `number` | no | `0.5` | ≥ 0; ≤ 1 — Modulation depth. |
| `mix` | `number` | no | `1` | ≥ 0; ≤ 1 — Dry/wet mix. |

### Constraints

- id and type are required. The selected type permits only its documented properties.
- Every supplied numeric value must be a JSON number inside its documented range; values are never coerced or clamped.
- Effect ids are unique within one bus; maximum eight effects per bus.

### Related

[`BusFilterMode`](#busfiltermode)

## BusFilterMode

String enum selecting a custom-Bus filter direction.

### Syntax

```text
"lowpass" | "highpass"
```

### Values

`"lowpass"` · `"highpass"`

## Send

Copy part of one custom Bus into hall, plate, or another custom Bus as a parallel signal path.

### Syntax

```text
{ "id": …, "to": …, ["amount": …], ["tap": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `id` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Unique send id inside this bus. |
| `to` | `SendTarget` | yes |  | Built-in return or declared custom bus. |
| `amount` | `number` | no | `0.25` | ≥ 0; ≤ 1 — Send level. |
| `tap` | `SendTap` | no | `"post"` |  |

### Constraints

- Every supplied numeric value must be a JSON number inside its documented range; values are never coerced or clamped.

### Related

[`SendTarget`](#sendtarget) · [`SendTap`](#sendtap)

## SendTarget

A built-in shared return or the exact key of one declared custom Bus.

### Syntax

```text
BuiltInReturn | one of the keys in Score.buses Dictionary<string, Bus>
```

### Constraints

- A custom Bus key must resolve in the same Score.

### Related

[`BuiltInReturn`](#builtinreturn)

## BuiltInReturn

String enum selecting one built-in shared effect return.

### Syntax

```text
"hall" | "plate"
```

### Values

`"hall"` · `"plate"`

## SendTap

String enum selecting where a Send copies its source Bus audio.

### Syntax

```text
"pre" | "post"
```

### Values

`"pre"` · `"post"`

### Value ranges

| Value / target | Range |
|---|---|
| `pre` | copy the Bus input before its effects, sidechain ducking, fader, and pan |
| `post` | copy the completed Bus output after its effects, sidechain ducking, fader, and pan |

## Sidechain

Duck one custom Bus after its insert effects and before its fader/pan, driven by one or more exact sources.

### Syntax

```text
{ "from": …, ["amount": …], ["attackMs": …], ["releaseMs": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `from` | `SidechainSource[]` | yes |  | 1..16 items — Exact detector sources. Their strongest level wins at each sample; array order has no effect. |
| `amount` | `number` | no | `4` | ≥ 0; ≤ 10 — Ducking amount. |
| `attackMs` | `number` | no | `10` | ≥ 1; ≤ 200 — Attack in milliseconds. |
| `releaseMs` | `number` | no | `250` | ≥ 10; ≤ 2000 — Release in milliseconds. |

### Constraints

- Every supplied numeric value must be a JSON number inside its documented range; values are never coerced or clamped.
- Every source symbol must resolve; duplicate sources are errors and custom-bus routing/sidechains must remain acyclic.
- A drumHit or trigger source uses a fixed 20 ms control pulse at each event; attackMs and releaseMs determine the audible duck shape.

### Related

[`SidechainSource`](#sidechainsource) · [`Trigger`](#trigger)

## SidechainSource

One exact detector source for a custom Bus sidechain. Track, Pattern, and instrument selectors follow their completed post-fader audio; drumHit and trigger selectors create fixed control pulses; bus selects one declared custom Bus's post-fader output.

### Syntax

```text
{ "track": … }
| { "pattern": … }
| { "instrument": … }
| { "drumHit": … }
| { "trigger": … }
| { "bus": … }
```

### Alternatives

#### Track sidechain source

Follow exactly one top-level Track.

##### Syntax

```text
{ "track": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `track` | `string` | yes |  | Exact Track.id. |

#### Pattern sidechain source

Follow every placement of exactly one Pattern.

##### Syntax

```text
{ "pattern": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `pattern` | `string` | yes |  | Exact key in Score.patterns. |

#### Instrument sidechain source

Follow every lane globally using one public instrument.

##### Syntax

```text
{ "instrument": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `instrument` | `InstrumentName` | yes |  |  |

#### Drum-hit sidechain source

Create a control pulse at every occurrence of one public drum hit.

##### Syntax

```text
{ "drumHit": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `drumHit` | `DrumHitName` | yes |  |  |

#### Silent Trigger sidechain source

Create a control pulse at every event in one silent Trigger.

##### Syntax

```text
{ "trigger": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `trigger` | `string` | yes |  | Exact key in Score.triggers. |

#### Custom Bus sidechain source

Follow one declared custom Bus's completed post-fader audio.

##### Syntax

```text
{ "bus": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `bus` | `string` | yes |  | pattern `^[a-z][a-z0-9_]{0,31}$` — Exact key in Score.buses; built-in role buses are not valid detector sources. |

### Constraints

- Exactly one selector property is required in each SidechainSource object.
- All sources must resolve and duplicates are errors.
- Several sources are combined by their strongest detector level at each sample; array order has no effect and source audio cannot phase-cancel another source.

### Related

[`InstrumentName`](#instrumentname) · [`DrumHitName`](#drumhitname) · [`PumpSource`](#pumpsource) · [`Trigger`](#trigger) · [`Bus`](#bus)

## Resample

Bounded pre-render capture exposed as a temporary rs_ instrument.

### Syntax

```text
{ "source": …, "fromBeat": …, "beats": …, ["slices": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `source` | `ResampleSource` | yes |  |  |
| `fromBeat` | `number` | yes |  | ≥ 0 — Capture start on the global score timeline, in beats. |
| `beats` | `number` | yes |  | ≥ 0.015625; ≤ 512 — Capture length in beats. |
| `slices` | `ResampleSlices` | no |  |  |

### Constraints

- Maximum 16 captures, 32 seconds per capture, and 120 seconds across all captures after tempo conversion.
- Maximum 128 generated regions and 120 seconds of overlapping explicit-region material per capture.
- Captures may not depend on rs_ instruments.

### Related

[`ResampleSource`](#resamplesource) · [`ResampleSlices`](#resampleslices)

## Granular

Deterministic grain-cloud playback for an rs_ instrument.

### Syntax

```text
{ ["grainMs": …], ["density": …], ["overlap": …], ["scan": …], ["freeze": …], ["positionJitter": …], ["pitchJitterCents": …], ["window": …], ["stereoScatter": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `grainMs` | `number` | no | `80` | ≥ 10; ≤ 500 — Maximum source fragment length in milliseconds. |
| `density` | `GranularCurve` | no | `18` | Grains per second as a constant or phase curve. |
| `overlap` | `number` | no | `0.65` | ≥ 0; ≤ 0.95 — Maximum adjacent-grain overlap. |
| `scan` | `GranularCurve` | no | `[[0,0],[1,1]]` | Source position as a constant or 0..1 phase curve. |
| `freeze` | `number` | no | scan | ≥ 0; ≤ 1 — Fixed source position replacing scan. |
| `positionJitter` | `number` | no | `0` | ≥ 0; ≤ 1 — Random source-position displacement as a region fraction. |
| `pitchJitterCents` | `number` | no | `0` | ≥ 0; ≤ 1200 — Per-grain seeded pitch spread. |
| `window` | `GranularWindow` | no | `"hann"` | Amplitude shape applied to each grain. |
| `stereoScatter` | `number` | no | `0` | ≥ 0; ≤ 1 — Per-grain pan spread. |

### Constraints

- density values are 1..200; scan values are 0..1; every curve begins at phase 0, ends at 1, and has strictly increasing phases.
- Maximum granular note length is 120 seconds; score-wide estimate is limited to 250,000 grains.

### Related

[`GranularWindow`](#granularwindow) · [`GranularCurve`](#granularcurve)

## GranularWindow

String enum selecting the amplitude shape applied to every grain.

### Syntax

```text
"hann" | "triangle" | "tukey"
```

### Values

`"hann"` · `"triangle"` · `"tukey"`

## SynthControls

The 16 public 0..10 front-panel controls for pitched synth instruments. This is the only control map accepted by per-note c. An omitted control makes no override, so the enclosing layer or selected synth patch remains.

### Syntax

```text
{ "cutoff": 6, "resonance": 4, ... }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `cutoff` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth filter cutoff. Omission preserves the selected patch value. |
| `resonance` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth filter resonance; distinct from the track filter control res. Omission preserves the selected patch value. |
| `envMod` | `number` | no |  | ≥ 0; ≤ 10 — Amount the pitched synth's filter envelope moves its cutoff per note. Omission preserves the selected patch value. |
| `attack` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude-envelope attack time. Omission preserves the selected patch value. |
| `decay` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude and filter-envelope decay time. Omission preserves the selected patch value. |
| `sustain` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth held amplitude after decay. Omission preserves the selected patch value. |
| `release` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude-envelope release time. Omission preserves the selected patch value. |
| `drive` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth voice saturation. Omission preserves the selected patch value. |
| `detune` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth unison spread. Omission preserves the selected patch value. |
| `sub` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth sub-oscillator level. Omission preserves the selected patch value. |
| `noise` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth noise level. Omission preserves the selected patch value. |
| `lfoRate` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO rate. Omission preserves the selected patch value. |
| `wobble` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO-to-filter depth. Omission preserves the selected patch value. |
| `vibrato` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO-to-pitch depth. Omission preserves the selected patch value. |
| `sweep` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth cutoff movement across each note. Omission preserves the selected patch value. |
| `pitchDrop` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth attack pitch displacement that converges to the written pitch. Omission preserves the selected patch value. |

## PumpSource

One exact public source for track pump. Select a top-level Track, an arranged Pattern, every lane using an instrument, one drum-hit name, or a silent Trigger; the selector is a string reference, not the referenced object.

### Syntax

```text
{ "track": … }
| { "pattern": … }
| { "instrument": … }
| { "drumHit": … }
| { "trigger": … }
```

### Alternatives

#### Track pump source

Trigger from notes produced by exactly one top-level Track.

##### Syntax

```text
{ "track": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `track` | `string` | yes |  | Exact id property of one object in top-level Score.tracks. |

#### Pattern pump source

Trigger from every placement of exactly one Pattern.

##### Syntax

```text
{ "pattern": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `pattern` | `string` | yes |  | Exact key in the top-level Score.patterns Dictionary<string, Pattern>. |

#### Instrument pump source

Trigger from every Track or arranged Pattern globally using exactly one public instrument.

##### Syntax

```text
{ "instrument": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `instrument` | `InstrumentName` | yes |  | Exact instrument property used by a Track or Pattern in this Score. |

#### Drum-hit pump source

Trigger from every occurrence of exactly one public drum hit, including hits inside drums lanes and single-drum lanes.

##### Syntax

```text
{ "drumHit": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `drumHit` | `DrumHitName` | yes |  | Exact factory drum hit or key declared in Score.drumSynths. |

#### Silent trigger pump source

Trigger from every compiled event in one silent Trigger timeline.

##### Syntax

```text
{ "trigger": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `trigger` | `string` | yes |  | Exact key in the top-level Score.triggers Dictionary<string, Trigger>. |

### Constraints

- Exactly one selector property is required in each PumpSource object.
- Every referenced source must produce at least one rendered note or compiled Trigger event; unresolved or unused sources are compiler errors.
- Several PumpSource values are combined into one time-sorted onset stream; duplicate sources are errors and array order has no effect.
- Public instrument and drum-hit identities are preserved through compilation; internal renderer voice groups never participate in matching.

### Related

[`InstrumentName`](#instrumentname) · [`DrumHitName`](#drumhitname) · [`Track`](#track) · [`Pattern`](#pattern) · [`Trigger`](#trigger)

## SynthPatch

A compact single-oscillator or expanded dual-oscillator ex_ patch.

### Syntax

```text
CompactSynthPatch
| DualSynthPatch
```

### Related

[`CompactSynthPatch`](#compactsynthpatch) · [`DualSynthPatch`](#dualsynthpatch)

## CompactSynthPatch

Single-oscillator subtractive/FM patch. osc identifies this architecture; there is no version field.

### Syntax

```text
{ "osc": …, ["cutoff": …], ["attack": …], ["decay": …], ["sustain": …], ["release": …], ["noiseColor": …], ["lfoShape": …], ["unison": …], ["detuneCents": …], ["fmRatio": …], ["fmIndex": …], ["fmDecay": …], ["sub": …], ["noise": …], ["cutoffEnv": …], ["filterDecay": …], ["res": …], ["cutoffRise": …], ["lfoRate": …], ["lfoCutoff": …], ["lfoPitch": …], ["drive": …], ["gain": …], ["pitchDropSemis": …], ["pitchDropSec": …], ["pitchRiseSemis": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `osc` | `CompactOscillatorType` | yes |  |  |
| `cutoff` | `number` | no | `2000` | ≥ 30; ≤ 16000 — Filter cutoff in Hz. |
| `attack` | `number` | no | `0.005` | ≥ 0.001; ≤ 3 — Amp attack in seconds. |
| `decay` | `number` | no | `0.3` | ≥ 0.01; ≤ 4 — Amp decay in seconds. |
| `sustain` | `number` | no | `0.7` | ≥ 0; ≤ 1 — Amp sustain. |
| `release` | `number` | no | `0.2` | ≥ 0.01; ≤ 4 — Amp release in seconds. |
| `noiseColor` | `SynthNoiseColor` | no | `"white"` | Noise oscillator color. |
| `lfoShape` | `CompactLfoShape` | no | `"sine"` | LFO waveform. |
| `unison` | `integer` | no | `1` | ≥ 1; ≤ 8 — Stacked oscillator copies. |
| `detuneCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Total unison spread in cents. |
| `fmRatio` | `number` | no | `2` | ≥ 0.25; ≤ 12 — FM modulator ratio. |
| `fmIndex` | `number` | no | `4` | ≥ 0; ≤ 12 — FM index. |
| `fmDecay` | `number` | no | `0.5` | ≥ 0.02; ≤ 5 — FM-index decay in seconds. |
| `sub` | `number` | no | `0` | ≥ 0; ≤ 1 — Sub-oscillator level. |
| `noise` | `number` | no | `0` | ≥ 0; ≤ 1 — Pre-filter noise level. |
| `cutoffEnv` | `number` | no | `0` | ≥ 0; ≤ 8000 — Filter-envelope depth in Hz. |
| `filterDecay` | `number` | no | `0.3` | ≥ 0.02; ≤ 3 — Filter-envelope decay in seconds. |
| `res` | `number` | no | `0` | ≥ 0; ≤ 0.9 — Filter resonance. |
| `cutoffRise` | `number` | no | `0` | ≥ -12000; ≤ 12000 — Whole-note cutoff travel in Hz. |
| `lfoRate` | `number` | no | `0` | ≥ 0; ≤ 20 — LFO rate in Hz. |
| `lfoCutoff` | `number` | no | `0` | ≥ 0; ≤ 6000 — LFO cutoff depth in Hz. |
| `lfoPitch` | `number` | no | `0` | ≥ 0; ≤ 1200 — LFO pitch depth in cents. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Voice saturation; 1 is clean. |
| `gain` | `number` | no | `0.8` | ≥ 0; ≤ 1 — Patch output gain. |
| `pitchDropSemis` | `number` | no | `0` | ≥ -48; ≤ 48 — Attack pitch displacement in semitones. |
| `pitchDropSec` | `number` | no | `0.08` | ≥ 0.01; ≤ 0.5 — Attack pitch convergence time in seconds. |
| `pitchRiseSemis` | `number` | no | `0` | ≥ -48; ≤ 48 — Whole-note pitch travel in semitones. |

### Constraints

- noiseColor applies only to osc noise; fmRatio/fmIndex/fmDecay apply only to osc fm.
- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- Unknown fields are errors.

### Related

[`CompactOscillatorType`](#compactoscillatortype) · [`SynthNoiseColor`](#synthnoisecolor) · [`CompactLfoShape`](#compactlfoshape)

## CompactOscillatorType

String enum selecting the oscillator architecture of a CompactSynthPatch.

### Syntax

```text
"saw" | "square" | "sine" | "fm" | "noise"
```

### Values

`"saw"` · `"square"` · `"sine"` · `"fm"` · `"noise"`

## SynthNoiseColor

String enum selecting the spectral character of synthesized noise.

### Syntax

```text
"white" | "pink" | "crackle"
```

### Values

`"white"` · `"pink"` · `"crackle"`

## CompactLfoShape

String enum selecting the LFO waveform available to a CompactSynthPatch.

### Syntax

```text
"sine" | "sh"
```

### Values

`"sine"` · `"sh"`

## DualSynthPatch

Expanded dual-oscillator synth. Presence of osc1 and osc2 identifies this architecture; there is no version field.

### Syntax

```text
{ "osc1": …, "osc2": …, ["blend": …], ["sync": …], ["ring": …], ["shape": …], ["sub": …], ["noise": …], ["unison": …], ["detuneCents": …], ["stereo": …], ["filter": …], ["amp": …], ["env2": …], ["lfo1": …], ["lfo2": …], ["mod": …], ["macros": …], ["drive": …], ["gain": …], ["cutoffRise": …], ["pitchDropSemis": …], ["pitchDropSec": …], ["pitchRiseSemis": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `osc1` | `Oscillator` | yes |  |  |
| `osc2` | `Oscillator` | yes |  |  |
| `blend` | `number` | no | `0.5` | ≥ 0; ≤ 1 — Oscillator crossfade. |
| `sync` | `number` | no | `0` | ≥ 0; ≤ 1 — Hard sync amount. |
| `ring` | `number` | no | `0` | ≥ 0; ≤ 1 — Ring modulation amount. |
| `shape` | `number` | no | `0` | ≥ 0; ≤ 1 — Nonlinear wave shaping. |
| `sub` | `number` | no | `0` | ≥ 0; ≤ 1 — Sub-oscillator level. |
| `noise` | `number` | no | `0` | ≥ 0; ≤ 1 — Additional noise level. |
| `unison` | `integer` | no | `1` | ≥ 1; ≤ 6 — Voices per oscillator. |
| `detuneCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Unison spread. |
| `stereo` | `number` | no | `0.8` | ≥ 0; ≤ 1 — Unison stereo spread. |
| `filter` | `object` | no | `{"mode":"lowpass","cutoff":3000,"res":0.1,"keytrack":0}` | Dual-patch multimode filter. |
| `amp` | `SynthEnvelope` | no | `{"attack":0.005,"decay":0.3,"sustain":0.7,"release":0.2}` | Amplitude envelope. |
| `env2` | `SynthEnvelope` | no | `{"attack":0.005,"decay":0.3,"sustain":0,"release":0.2}` | Modulation envelope. |
| `lfo1` | `SynthLfo` | no | `{"shape":"sine","rateHz":0.5,"phase":0}` |  |
| `lfo2` | `SynthLfo` | no | `{"shape":"triangle","rateHz":0.13,"phase":0.25}` |  |
| `mod` | `ModRoute[]` | no | `[]` | 0..8 items — Ordered modulation routes. |
| `macros` | `object` | no | `{"motion":0,"roughness":0,"inharmonicity":0,"air":0,"body":0}` | Perceptual macro amounts. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Voice saturation; 1 is clean. |
| `gain` | `number` | no | `0.75` | ≥ 0; ≤ 1 — Patch output gain. |
| `cutoffRise` | `number` | no | `0` | ≥ -12000; ≤ 12000 — Whole-note cutoff travel in Hz. |
| `pitchDropSemis` | `number` | no | `0` | ≥ -48; ≤ 48 — Attack pitch displacement. |
| `pitchDropSec` | `number` | no | `0.08` | ≥ 0.01; ≤ 0.5 — Pitch convergence time in seconds. |
| `pitchRiseSemis` | `number` | no | `0` | ≥ -48; ≤ 48 — Whole-note pitch travel. |

### filter

Dual-patch multimode filter.

#### Syntax

```text
{ ["mode": …], ["cutoff": …], ["res": …], ["keytrack": …] }
```

#### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `mode` | `SynthFilterMode` | no | `"lowpass"` |  |
| `cutoff` | `number` | no | `3000` | ≥ 30; ≤ 16000 — Cutoff in Hz. |
| `res` | `number` | no | `0.1` | ≥ 0; ≤ 0.9 — Resonance. |
| `keytrack` | `number` | no | `0` | ≥ 0; ≤ 1 — Keyboard tracking. |

### macros

Perceptual macro amounts.

#### Syntax

```text
{ ["motion": …], ["roughness": …], ["inharmonicity": …], ["air": …], ["body": …] }
```

#### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `motion` | `number` | no | `0` | ≥ 0; ≤ 1 — Slow filter/pitch and blend/pan movement. |
| `roughness` | `number` | no | `0` | ≥ 0; ≤ 1 — Coordinated waveshaping, ring modulation, and a small noise edge. |
| `inharmonicity` | `number` | no | `0` | ≥ 0; ≤ 1 — Offsets oscillator 2 by up to 6.93 semitones and adds ring texture. |
| `air` | `number` | no | `0` | ≥ 0; ≤ 1 — Opens the filter by up to 3000 Hz and adds quiet high-passed stereo air. |
| `body` | `number` | no | `0` | ≥ 0; ≤ 1 — Adds up to 0.35 of a centered sub fundamental. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- sync and sync modulation require two pitched oscillators.
- Pitch envelopes require at least one pitched oscillator; inharmonicity requires pitched osc2.

### Related

[`Oscillator`](#oscillator) · [`SynthFilterMode`](#synthfiltermode) · [`SynthEnvelope`](#synthenvelope) · [`SynthLfo`](#synthlfo) · [`ModRoute`](#modroute)

## Oscillator

Strict wave-discriminated oscillator for a dual-oscillator patch.

### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
| { "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
| { "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …], ["pulseWidth": …] }
| { "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
| { "wave": …, ["level": …], ["noiseColor": …] }
| { "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …], "table": … }
```

### Alternatives

#### sine oscillator

sine dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"sine"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `octave` | `integer` | no | `0` | ≥ -4; ≤ 4 — Octave offset. |
| `semitones` | `number` | no | `0` | ≥ -24; ≤ 24 — Semitone offset. |
| `fineCents` | `number` | no | `0` | ≥ -100; ≤ 100 — Fine tuning in cents. |
| `phase` | `OscillatorPhase` | no | `"reset"` |  |
| `phaseOffset` | `number` | no | `0` | ≥ 0; ≤ 1 — Initial cycle phase. |

#### saw oscillator

saw dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"saw"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `octave` | `integer` | no | `0` | ≥ -4; ≤ 4 — Octave offset. |
| `semitones` | `number` | no | `0` | ≥ -24; ≤ 24 — Semitone offset. |
| `fineCents` | `number` | no | `0` | ≥ -100; ≤ 100 — Fine tuning in cents. |
| `phase` | `OscillatorPhase` | no | `"reset"` |  |
| `phaseOffset` | `number` | no | `0` | ≥ 0; ≤ 1 — Initial cycle phase. |

#### square oscillator

square dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …], ["pulseWidth": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"square"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `octave` | `integer` | no | `0` | ≥ -4; ≤ 4 — Octave offset. |
| `semitones` | `number` | no | `0` | ≥ -24; ≤ 24 — Semitone offset. |
| `fineCents` | `number` | no | `0` | ≥ -100; ≤ 100 — Fine tuning in cents. |
| `phase` | `OscillatorPhase` | no | `"reset"` |  |
| `phaseOffset` | `number` | no | `0` | ≥ 0; ≤ 1 — Initial cycle phase. |
| `pulseWidth` | `number` | no | `0.5` | ≥ 0.05; ≤ 0.95 — Pulse duty cycle. |

#### triangle oscillator

triangle dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"triangle"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `octave` | `integer` | no | `0` | ≥ -4; ≤ 4 — Octave offset. |
| `semitones` | `number` | no | `0` | ≥ -24; ≤ 24 — Semitone offset. |
| `fineCents` | `number` | no | `0` | ≥ -100; ≤ 100 — Fine tuning in cents. |
| `phase` | `OscillatorPhase` | no | `"reset"` |  |
| `phaseOffset` | `number` | no | `0` | ≥ 0; ≤ 1 — Initial cycle phase. |

#### noise oscillator

noise dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["noiseColor": …] }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"noise"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `noiseColor` | `SynthNoiseColor` | no | `"white"` |  |

#### wavetable oscillator

wavetable dual-patch oscillator.

##### Syntax

```text
{ "wave": …, ["level": …], ["octave": …], ["semitones": …], ["fineCents": …], ["phase": …], ["phaseOffset": …], "table": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `wave` | `"wavetable"` | yes |  |  |
| `level` | `number` | no | `1` | ≥ 0; ≤ 1 — Oscillator level. |
| `octave` | `integer` | no | `0` | ≥ -4; ≤ 4 — Octave offset. |
| `semitones` | `number` | no | `0` | ≥ -24; ≤ 24 — Semitone offset. |
| `fineCents` | `number` | no | `0` | ≥ -100; ≤ 100 — Fine tuning in cents. |
| `phase` | `OscillatorPhase` | no | `"reset"` |  |
| `phaseOffset` | `number` | no | `0` | ≥ 0; ≤ 1 — Initial cycle phase. |
| `table` | `number[]` | yes |  | 8..64 items — One waveform cycle; compiler removes DC and peak-normalizes it. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- Wavetable samples must not all be identical.

### Related

[`OscillatorPhase`](#oscillatorphase) · [`SynthNoiseColor`](#synthnoisecolor)

## OscillatorPhase

String enum selecting how a dual-patch oscillator chooses its phase at note onset.

### Syntax

```text
"reset" | "random"
```

### Values

`"reset"` · `"random"`

## SynthLfoShape

String enum selecting the waveform of a dual-patch SynthLfo.

### Syntax

```text
"sine" | "triangle" | "square" | "sh"
```

### Values

`"sine"` · `"triangle"` · `"square"` · `"sh"`

## ModulationSource

String enum selecting the signal that drives a dual-patch modulation route.

### Syntax

```text
"env2" | "lfo1" | "lfo2"
```

### Values

`"env2"` · `"lfo1"` · `"lfo2"`

## ModulationTarget

String enum selecting the parameter moved by a dual-patch modulation route.

### Syntax

```text
"pitch1" | "pitch2" | "blend" | "sync" | "ring" | "shape" | "cutoff" | "resonance" | "pan"
```

### Values

`"pitch1"` · `"pitch2"` · `"blend"` · `"sync"` · `"ring"` · `"shape"` · `"cutoff"` · `"resonance"` · `"pan"`

## SynthFilterMode

String enum selecting the filter response of a DualSynthPatch.

### Syntax

```text
"lowpass" | "bandpass" | "highpass" | "notch"
```

### Values

`"lowpass"` · `"bandpass"` · `"highpass"` · `"notch"`

## CustomDrumPatch

A model-discriminated exd_ electronic drum patch. Model-inapplicable fields are errors.

### Syntax

```text
KickDrumPatch
| MembraneDrumPatch
| ClapDrumPatch
| NoiseDrumPatch
| MetalDrumPatch
```

### Constraints

- model is the required discriminator; every other field is optional and receives the selected model's documented default.
- The patch must remain audible: gain must be greater than 0 and at least one source level used by that model must be greater than 0.

### Related

[`KickDrumPatch`](#kickdrumpatch) · [`MembraneDrumPatch`](#membranedrumpatch) · [`ClapDrumPatch`](#clapdrumpatch) · [`NoiseDrumPatch`](#noisedrumpatch) · [`MetalDrumPatch`](#metaldrumpatch)

## KickDrumPatch

Bounded deterministic kick drum voice.

### Syntax

```text
{ "model": …, ["bus": …], ["duration": …], ["gain": …], ["drive": …], ["highpassHz": …], ["lowpassHz": …], ["decayVar": …], ["toneVar": …], ["pitchVarCents": …], ["tuneHz": …], ["pitchStartHz": …], ["pitchDecay": …], ["body": …], ["bodyDecay": …], ["click": …], ["clickHz": …], ["noise": …], ["noiseColor": …], ["noiseDecay": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `model` | `"kick"` | yes |  | Model discriminator. Must be "kick" for KickDrumPatch. |
| `bus` | `DrumBus` | no | `"kit"` | Default mixer role for the generated drum. Track.bus or Pattern.bus overrides it. |
| `duration` | `number` | no | `0.35` | ≥ 0.01; ≤ 4 — Default hard generated-audio length in seconds when Note.dur or Note.durB is omitted. A note duration replaces it up to the custom hit's 4-second limit; synthesis extending beyond the selected length is truncated. |
| `gain` | `number` | no | `0.8` | > 0; ≤ 1 — Patch output gain. It must be greater than 0 so the patch is audible. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Tanh drive; 1 is clean. |
| `highpassHz` | `number` | no | `0` | ≥ 0; ≤ 12000 — High-pass cutoff in Hz. |
| `lowpassHz` | `number` | no | `18000` | ≥ 100; ≤ 18000 — Low-pass cutoff in Hz. |
| `decayVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Seeded per-hit multiplier applied to body and noise decays, uniformly selected from 1-decayVar through 1+decayVar. |
| `toneVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Chooses one seeded per-hit tone factor uniformly from 1-toneVar through 1+toneVar. The factor multiplies filter and click frequencies, shifts dark/bright noise filtering, and moves each metal partial away from or toward ratio 1 using 1 + (ratio - 1) * factor. |
| `pitchVarCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Seeded per-hit body-pitch displacement selected uniformly from -pitchVarCents through +pitchVarCents. |
| `tuneHz` | `number` | no | `48` | ≥ 20; ≤ 300 — Body frequency in Hz. |
| `pitchStartHz` | `number` | no | `150` | ≥ 20; ≤ 3000 — Initial body frequency; it may be above or below tuneHz. |
| `pitchDecay` | `number` | no | `0.035` | ≥ 0.001; ≤ 1 — Exponential pitch-sweep time constant in seconds. After this time, 36.8% of the initial distance from tuneHz remains. |
| `body` | `number` | no | `1` | ≥ 0; ≤ 1 — Tonal body level. |
| `bodyDecay` | `number` | no | `0.22` | ≥ 0.003; ≤ 4 — Body decay in seconds. |
| `click` | `number` | no | `0.25` | ≥ 0; ≤ 1 — Transient click level. |
| `clickHz` | `number` | no | `3500` | ≥ 100; ≤ 16000 — Click frequency. |
| `noise` | `number` | no | `0.08` | ≥ 0; ≤ 1 — Noise level. |
| `noiseColor` | `DrumNoiseColor` | no | `"bright"` |  |
| `noiseDecay` | `number` | no | `0.015` | ≥ 0.003; ≤ 4 — Noise decay in seconds. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- highpassHz must be lower than lowpassHz.
- duration is the default hard generated-audio length. Note.dur or Note.durB replaces it up to the custom hit's 4-second limit; synthesis beyond the selected length is truncated.
- bus is the default route. An explicit Track.bus or Pattern.bus overrides it.
- The patch must contain an audible source and gain must be greater than 0.

### Related

[`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumNoiseColor`](#drumnoisecolor)

## MembraneDrumPatch

Bounded deterministic membrane drum voice.

### Syntax

```text
{ "model": …, ["bus": …], ["duration": …], ["gain": …], ["drive": …], ["highpassHz": …], ["lowpassHz": …], ["decayVar": …], ["toneVar": …], ["pitchVarCents": …], ["tuneHz": …], ["pitchStartHz": …], ["pitchDecay": …], ["body": …], ["bodyDecay": …], ["damping": …], ["click": …], ["clickHz": …], ["noise": …], ["noiseColor": …], ["noiseDecay": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `model` | `"membrane"` | yes |  | Model discriminator. Must be "membrane" for MembraneDrumPatch. |
| `bus` | `DrumBus` | no | `"kit"` | Default mixer role for the generated drum. Track.bus or Pattern.bus overrides it. |
| `duration` | `number` | no | `0.45` | ≥ 0.01; ≤ 4 — Default hard generated-audio length in seconds when Note.dur or Note.durB is omitted. A note duration replaces it up to the custom hit's 4-second limit; synthesis extending beyond the selected length is truncated. |
| `gain` | `number` | no | `0.8` | > 0; ≤ 1 — Patch output gain. It must be greater than 0 so the patch is audible. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Tanh drive; 1 is clean. |
| `highpassHz` | `number` | no | `0` | ≥ 0; ≤ 12000 — High-pass cutoff in Hz. |
| `lowpassHz` | `number` | no | `18000` | ≥ 100; ≤ 18000 — Low-pass cutoff in Hz. |
| `decayVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Seeded per-hit multiplier applied to body and noise decays, uniformly selected from 1-decayVar through 1+decayVar. |
| `toneVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Chooses one seeded per-hit tone factor uniformly from 1-toneVar through 1+toneVar. The factor multiplies filter and click frequencies, shifts dark/bright noise filtering, and moves each metal partial away from or toward ratio 1 using 1 + (ratio - 1) * factor. |
| `pitchVarCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Seeded per-hit body-pitch displacement selected uniformly from -pitchVarCents through +pitchVarCents. |
| `tuneHz` | `number` | no | `110` | ≥ 20; ≤ 2000 — Body frequency in Hz. |
| `pitchStartHz` | `number` | no | `145` | ≥ 20; ≤ 4000 — Initial body frequency; it may be above or below tuneHz. |
| `pitchDecay` | `number` | no | `0.06` | ≥ 0.001; ≤ 1 — Exponential pitch-sweep time constant in seconds. After this time, 36.8% of the initial distance from tuneHz remains. |
| `body` | `number` | no | `0.9` | ≥ 0; ≤ 1 — Tonal body level. |
| `bodyDecay` | `number` | no | `0.35` | ≥ 0.003; ≤ 4 — Body decay in seconds. |
| `damping` | `number` | no | `0.35` | ≥ 0; ≤ 1 — Suppresses and shortens the membrane's two higher modes; 0 preserves them most and 1 damps them most. |
| `click` | `number` | no | `0.08` | ≥ 0; ≤ 1 — Transient click level. |
| `clickHz` | `number` | no | `1800` | ≥ 100; ≤ 16000 — Click frequency. |
| `noise` | `number` | no | `0.2` | ≥ 0; ≤ 1 — Noise level. |
| `noiseColor` | `DrumNoiseColor` | no | `"white"` |  |
| `noiseDecay` | `number` | no | `0.08` | ≥ 0.003; ≤ 4 — Noise decay in seconds. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- highpassHz must be lower than lowpassHz.
- duration is the default hard generated-audio length. Note.dur or Note.durB replaces it up to the custom hit's 4-second limit; synthesis beyond the selected length is truncated.
- bus is the default route. An explicit Track.bus or Pattern.bus overrides it.
- The patch must contain an audible source and gain must be greater than 0.

### Related

[`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumNoiseColor`](#drumnoisecolor)

## ClapDrumPatch

Bounded deterministic clap drum voice.

### Syntax

```text
{ "model": …, ["bus": …], ["duration": …], ["gain": …], ["drive": …], ["highpassHz": …], ["lowpassHz": …], ["decayVar": …], ["toneVar": …], ["pitchVarCents": …], ["bursts": …], ["spacingMs": …], ["spread": …], ["noise": …], ["noiseColor": …], ["noiseDecay": …], ["body": …], ["tuneHz": …], ["bodyDecay": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `model` | `"clap"` | yes |  | Model discriminator. Must be "clap" for ClapDrumPatch. |
| `bus` | `DrumBus` | no | `"kit"` | Default mixer role for the generated drum. Track.bus or Pattern.bus overrides it. |
| `duration` | `number` | no | `0.22` | ≥ 0.01; ≤ 4 — Default hard generated-audio length in seconds when Note.dur or Note.durB is omitted. A note duration replaces it up to the custom hit's 4-second limit; synthesis extending beyond the selected length is truncated. |
| `gain` | `number` | no | `0.8` | > 0; ≤ 1 — Patch output gain. It must be greater than 0 so the patch is audible. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Tanh drive; 1 is clean. |
| `highpassHz` | `number` | no | `0` | ≥ 0; ≤ 12000 — High-pass cutoff in Hz. |
| `lowpassHz` | `number` | no | `18000` | ≥ 100; ≤ 18000 — Low-pass cutoff in Hz. |
| `decayVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Seeded per-hit multiplier applied to body and noise decays, uniformly selected from 1-decayVar through 1+decayVar. |
| `toneVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Chooses one seeded per-hit tone factor uniformly from 1-toneVar through 1+toneVar. The factor multiplies filter and click frequencies, shifts dark/bright noise filtering, and moves each metal partial away from or toward ratio 1 using 1 + (ratio - 1) * factor. |
| `pitchVarCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Seeded per-hit pitch displacement of the optional tonal body, selected uniformly from -pitchVarCents through +pitchVarCents. |
| `bursts` | `integer` | no | `3` | ≥ 1; ≤ 8 — Number of transient bursts. |
| `spacingMs` | `number` | no | `12` | ≥ 1; ≤ 40 — Burst separation in milliseconds. |
| `spread` | `number` | no | `0.15` | ≥ 0; ≤ 1 — Seeded looseness after the first burst: timing may move by up to 45% of spacingMs * spread and level by up to 30% * spread. This does not create stereo width. |
| `noise` | `number` | no | `1` | ≥ 0; ≤ 1 — Noise level. |
| `noiseColor` | `DrumNoiseColor` | no | `"bright"` |  |
| `noiseDecay` | `number` | no | `0.045` | ≥ 0.003; ≤ 1 — Noise decay in seconds. |
| `body` | `number` | no | `0.08` | ≥ 0; ≤ 1 — Tonal body level. |
| `tuneHz` | `number` | no | `180` | ≥ 20; ≤ 2000 — Body frequency. |
| `bodyDecay` | `number` | no | `0.08` | ≥ 0.003; ≤ 1 — Body decay in seconds. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- highpassHz must be lower than lowpassHz.
- duration is the default hard generated-audio length. Note.dur or Note.durB replaces it up to the custom hit's 4-second limit; synthesis beyond the selected length is truncated.
- bus is the default route. An explicit Track.bus or Pattern.bus overrides it.
- The patch must contain an audible source and gain must be greater than 0.

### Related

[`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumNoiseColor`](#drumnoisecolor)

## NoiseDrumPatch

Bounded deterministic noise drum voice.

### Syntax

```text
{ "model": …, ["bus": …], ["duration": …], ["gain": …], ["drive": …], ["highpassHz": …], ["lowpassHz": …], ["decayVar": …], ["toneVar": …], ["choke": …], ["noise": …], ["noiseColor": …], ["noiseDecay": …], ["density": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `model` | `"noise"` | yes |  | Model discriminator. Must be "noise" for NoiseDrumPatch. |
| `bus` | `DrumBus` | no | `"kit"` | Default mixer role for the generated drum. Track.bus or Pattern.bus overrides it. |
| `duration` | `number` | no | `0.16` | ≥ 0.01; ≤ 4 — Default hard generated-audio length in seconds when Note.dur or Note.durB is omitted. A note duration replaces it up to the custom hit's 4-second limit; synthesis extending beyond the selected length is truncated. |
| `gain` | `number` | no | `0.8` | > 0; ≤ 1 — Patch output gain. It must be greater than 0 so the patch is audible. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Tanh drive; 1 is clean. |
| `highpassHz` | `number` | no | `0` | ≥ 0; ≤ 12000 — High-pass cutoff in Hz. |
| `lowpassHz` | `number` | no | `18000` | ≥ 100; ≤ 18000 — Low-pass cutoff in Hz. |
| `decayVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Seeded per-hit multiplier applied to body and noise decays, uniformly selected from 1-decayVar through 1+decayVar. |
| `toneVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Chooses one seeded per-hit tone factor uniformly from 1-toneVar through 1+toneVar. The factor multiplies filter and click frequencies, shifts dark/bright noise filtering, and moves each metal partial away from or toward ratio 1 using 1 + (ratio - 1) * factor. |
| `choke` | `DrumChokeMode` | no | `"none"` | Hi-hat choke role. closed/open has physical choke behavior only when the final route is the kit bus. |
| `noise` | `number` | no | `1` | ≥ 0; ≤ 1 — Noise level. |
| `noiseColor` | `DrumNoiseColor` | no | `"bright"` |  |
| `noiseDecay` | `number` | no | `0.12` | ≥ 0.003; ≤ 4 — Noise decay in seconds. |
| `density` | `number` | no | `55` | ≥ 1; ≤ 300 — Expected number of seeded short-noise grain triggers per second. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- highpassHz must be lower than lowpassHz.
- duration is the default hard generated-audio length. Note.dur or Note.durB replaces it up to the custom hit's 4-second limit; synthesis beyond the selected length is truncated.
- bus is the default route. An explicit Track.bus or Pattern.bus overrides it.
- The patch must contain an audible source and gain must be greater than 0.
- pitchVarCents is not a NoiseDrumPatch field because this model has no pitched component.

### Related

[`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumChokeMode`](#drumchokemode) · [`DrumNoiseColor`](#drumnoisecolor)

## MetalDrumPatch

Bounded deterministic metal drum voice.

### Syntax

```text
{ "model": …, ["bus": …], ["duration": …], ["gain": …], ["drive": …], ["highpassHz": …], ["lowpassHz": …], ["decayVar": …], ["toneVar": …], ["pitchVarCents": …], ["tuneHz": …], ["partials": …], ["body": …], ["bodyDecay": …], ["damping": …], ["click": …], ["clickHz": …], ["noise": …], ["noiseColor": …], ["noiseDecay": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `model` | `"metal"` | yes |  | Model discriminator. Must be "metal" for MetalDrumPatch. |
| `bus` | `DrumBus` | no | `"kit"` | Default mixer role for the generated drum. Track.bus or Pattern.bus overrides it. |
| `duration` | `number` | no | `0.6` | ≥ 0.01; ≤ 4 — Default hard generated-audio length in seconds when Note.dur or Note.durB is omitted. A note duration replaces it up to the custom hit's 4-second limit; synthesis extending beyond the selected length is truncated. |
| `gain` | `number` | no | `0.8` | > 0; ≤ 1 — Patch output gain. It must be greater than 0 so the patch is audible. |
| `drive` | `number` | no | `1` | ≥ 1; ≤ 8 — Tanh drive; 1 is clean. |
| `highpassHz` | `number` | no | `0` | ≥ 0; ≤ 12000 — High-pass cutoff in Hz. |
| `lowpassHz` | `number` | no | `18000` | ≥ 100; ≤ 18000 — Low-pass cutoff in Hz. |
| `decayVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Seeded per-hit multiplier applied to body and noise decays, uniformly selected from 1-decayVar through 1+decayVar. |
| `toneVar` | `number` | no | `0` | ≥ 0; ≤ 0.5 — Chooses one seeded per-hit tone factor uniformly from 1-toneVar through 1+toneVar. The factor multiplies filter and click frequencies, shifts dark/bright noise filtering, and moves each metal partial away from or toward ratio 1 using 1 + (ratio - 1) * factor. |
| `pitchVarCents` | `number` | no | `0` | ≥ 0; ≤ 100 — Seeded per-hit displacement of the metallic partial bank, selected uniformly from -pitchVarCents through +pitchVarCents. |
| `tuneHz` | `number` | no | `320` | ≥ 20; ≤ 4000 — Reference frequency multiplied by every value in partials. |
| `partials` | `number[]` | no | `[1,1.43,1.91,2.47,3.16,4.11]` | 2..8 items — Strictly ascending frequency multipliers of tuneHz. Earlier, lower partials are rendered louder and longer. |
| `body` | `number` | no | `1` | ≥ 0; ≤ 1 — Metallic body level. |
| `bodyDecay` | `number` | no | `0.45` | ≥ 0.003; ≤ 4 — Body decay in seconds. |
| `damping` | `number` | no | `0.35` | ≥ 0; ≤ 1 — Increasingly suppresses and shortens later partials in array order; 0 preserves them most and 1 damps them most. |
| `click` | `number` | no | `0.08` | ≥ 0; ≤ 1 — Transient click level. |
| `clickHz` | `number` | no | `4800` | ≥ 100; ≤ 16000 — Click frequency. |
| `noise` | `number` | no | `0.08` | ≥ 0; ≤ 1 — Noise level. |
| `noiseColor` | `DrumNoiseColor` | no | `"bright"` |  |
| `noiseDecay` | `number` | no | `0.03` | ≥ 0.003; ≤ 4 — Noise decay in seconds. |

### Constraints

- All supplied numbers must remain inside their documented ranges; out-of-range values are compile errors and are never clamped.
- highpassHz must be lower than lowpassHz.
- duration is the default hard generated-audio length. Note.dur or Note.durB replaces it up to the custom hit's 4-second limit; synthesis beyond the selected length is truncated.
- bus is the default route. An explicit Track.bus or Pattern.bus overrides it.
- The patch must contain an audible source and gain must be greater than 0.
- partials must contain 2..8 strictly ascending ratios; array order defines the renderer's partial damping order.

### Related

[`DrumModel`](#drummodel) · [`DrumBus`](#drumbus) · [`DrumNoiseColor`](#drumnoisecolor)

## DrumChokeMode

String enum selecting the hi-hat choke role of a synthesized noise drum.

### Syntax

```text
"none" | "closed" | "open"
```

### Values

`"none"` · `"closed"` · `"open"`

### Value ranges

| Value / target | Range |
|---|---|
| `none` | ordinary noise percussion; does not join the physical hi-hat choke group |
| `closed` | closed-hi-hat role; cuts ringing open-role hits when the final route is the kit bus |
| `open` | open-hi-hat role; may be cut by later closed-role hits when the final route is the kit bus |

## DrumModel

String enum selecting the custom drum synthesis algorithm and its allowed model-specific fields.

### Syntax

```text
"kick" | "membrane" | "clap" | "noise" | "metal"
```

### Values

`"kick"` · `"membrane"` · `"clap"` · `"noise"` · `"metal"`

### Value ranges

| Value / target | Range |
|---|---|
| `kick` | pitched body sweeping from pitchStartHz toward tuneHz |
| `membrane` | drum-head body with damping and attack noise |
| `clap` | several short noise bursts with seeded timing/level looseness and an optional tonal body |
| `noise` | noise percussion such as a hi-hat or shaker |
| `metal` | inharmonic metallic partials with optional click and noise |

## DrumBus

String enum selecting the generated drum's mixer role.

### Syntax

```text
"kit" | "perc"
```

### Values

`"kit"` · `"perc"`

### Value ranges

| Value / target | Range |
|---|---|
| `kit` | main drum-kit bus, including kick-keyed glue processing |
| `perc` | percussion bus, outside the main kit glue processing |

## DrumNoiseColor

String enum selecting the spectral balance of a custom drum's noise component.

### Syntax

```text
"dark" | "white" | "bright"
```

### Values

`"dark"` · `"white"` · `"bright"`

### Value ranges

| Value / target | Range |
|---|---|
| `dark` | reduced high-frequency noise |
| `white` | neutral white-noise balance |
| `bright` | emphasized high-frequency noise |

## PitchedInstrumentName

Closed factory pitched-instrument symbol table, generated from the engine registry.

### Syntax

```text
one exact name from the generated factory catalog
```

### Values

`"supersaw_lead"` · `"analog_pad"` · `"synth_pluck"` · `"acid_bass"` · `"fm_bell"` · `"synth_brass"` · `"sub_808"` · `"sub_pure"` · `"saw_bass"` · `"reese_bass"` · `"growl_bass"` · `"wobble_bass"` · `"donk_bass"` · `"fm_bass"` · `"pluck_bass"` · `"mid_bass"` · `"knock_bass"` · `"moog_bass"` · `"rubber_bass"` · `"acid_deep"` · `"acid_screamer"` · `"hoover_bass"` · `"saw_bass_clean"` · `"saw_bass_short"` · `"saw_bass_rolling"` · `"saw_bass_offbeat"` · `"saw_bass_wide"` · `"saw_bass_driven"` · `"saw_bass_hollow"` · `"saw_bass_psy"` · `"saw_bass_trance"` · `"saw_bass_techno"` · `"liquid_reese"` · `"neuro_reese"` · `"pwm_bass"` · `"sync_bass"` · `"wavetable_bass"` · `"ringmod_bass"` · `"metallic_fm_bass"` · `"round_analog_bass"` · `"poly_saw"` · `"square_lead"` · `"chip_lead"` · `"chip_arp"` · `"fm_lead"` · `"whistle_lead"` · `"hoover_lead"` · `"noise_lead"` · `"trance_pluck"` · `"dream_pluck"` · `"laser_lead"` · `"glass_lead"` · `"soft_lead"` · `"screech_lead"` · `"sync_lead"` · `"pwm_lead"` · `"wavetable_lead"` · `"shaped_digital_lead"` · `"vocal_wavetable_lead"` · `"poly_hybrid_lead"` · `"glass_pad"` · `"dark_pad"` · `"air_pad"` · `"ice_pad"` · `"choir_pad"` · `"strings_pad"` · `"shimmer_pad"` · `"space_pad"` · `"evolving_pad"` · `"nostalgia_pad"` · `"dark_drone"` · `"warm_poly_pad"` · `"pwm_pad"` · `"wavetable_motion_pad"` · `"swarm_pad"` · `"spectral_pad"` · `"tension_pad"` · `"textural_machine"` · `"synth_keys"` · `"saw_chords"` · `"rave_stab"` · `"house_stab"` · `"ep_keys"` · `"organ_keys"` · `"clav_keys"` · `"music_box"` · `"pizz_synth"` · `"stab_brass"` · `"space_keys"` · `"space_keys_glass"` · `"space_keys_dark"` · `"space_keys_air"` · `"space_keys_shimmer"` · `"space_keys_tape"` · `"space_keys_orbit"` · `"space_keys_hologram"` · `"space_keys_alien"` · `"space_keys_frozen"` · `"warm_poly_keys"` · `"pwm_keys"` · `"phase_keys"` · `"morphed_keys"` · `"tape_keys"` · `"bell_keys"` · `"dub_chord"` · `"detroit_chord"` · `"rhythmic_filter_keys"` · `"signal_pulse"` · `"cloud_pulse"` · `"metallic_pulse"` · `"random_pan_keys"` · `"rhythmic_organ"` · `"wooden_pluck"` · `"metallic_pluck"` · `"rubber_pluck"` · `"resonant_ping"` · `"pitch_env_hit"` · `"laser_zap"` · `"sub_drop"` · `"pitch_riser"` · `"siren"` · `"white_noise"` · `"pink_wash"` · `"noise_riser"` · `"noise_fall"` · `"vinyl_crackle"` · `"sub_drone"` · `"metallic_drone"` · `"swarm_drone"` · `"pitched_ambience"` · `"circuit_bent_texture"` · `"balafon"` · `"kalimba"` · `"mbira"` · `"dan_tranh"` · `"hand_chimes"` · `"didgeridoo_drone"` · `"didgeridoo_phrase"` · `"ocean_drum"` · `"recorder"` · `"harpsichord"` · `"bowed_psaltery"` · `"wine_glass"` · `"glockenspiel"` · `"timpani"` · `"strumstick"` · `"folk_harp"` · `"saxello"` · `"saxello_staccato"` · `"saxello_vibrato"` · `"accordion"` · `"classical_guitar"` · `"ukulele"` · `"jazz_guitar"` · `"distortion_guitar"` · `"overdriven_guitar"` · `"honky_tonk_piano"` · `"tagelharpa"` · `"tuba"` · `"tuba_staccato"` · `"baritone_sax"` · `"baritone_sax_staccato"` · `"bass_finger"` · `"bass_pluck"` · `"bass_mute"` · `"bass_ghost"` · `"funk_guitar"` · `"funk_guitar_stac"` · `"funk_guitar_hammer"` · `"twang_guitar"` · `"twang_guitar_stac"` · `"prepared_guitar"` · `"upright_pizz"` · `"upright_arco"` · `"piano"` · `"electric_piano"` · `"organ"` · `"organ_8ft"` · `"organ_4ft"` · `"harmonica"` · `"harmonica_soft"` · `"harmonica_vibrato"` · `"ocarina"` · `"ocarina_vibrato"` · `"tenor_sax"` · `"tenor_sax_staccato"` · `"tenor_sax_vibrato"` · `"harp"` · `"marimba"` · `"tubular_bells"` · `"vibraphone"` · `"vibraphone_bowed"` · `"xylophone"` · `"french_horn"` · `"trombone"` · `"trumpet"` · `"bassoon"` · `"clarinet"` · `"flute"` · `"oboe"` · `"piccolo"` · `"violin"` · `"violin_section"` · `"viola_section"` · `"cello_section"` · `"cello"` · `"cello_staccato"` · `"cello_pizzicato"` · `"bagpipe"` · `"bagpipe_short"` · `"clean_electric_guitar"`

## FactoryDrumHitName

Closed factory drum symbol table, generated from the engine registry.

### Syntax

```text
string enum (one exact value listed below)
```

### Values

`"kick"` · `"snare"` · `"snare_soft"` · `"hat_closed"` · `"hat_open"` · `"crash"` · `"tom"` · `"e_kick"` · `"e_kick_deep"` · `"e_snare"` · `"e_clap"` · `"e_hat_closed"` · `"e_hat_open"` · `"e_tick"` · `"hand_clap"` · `"finger_clap"` · `"finger_snap"` · `"stomp"` · `"chest_thump"` · `"hat_pedal"` · `"hat_half_open"` · `"hat_three_quarter"` · `"hat_splash"` · `"ride"` · `"ride_bell"` · `"snare_rimshot"` · `"snare_cross_stick"` · `"snare_flam"` · `"snare_buzz"` · `"snare_muted"` · `"timbale_hi"` · `"timbale_lo"` · `"cuica_muted"` · `"cuica_open"` · `"snare_tight"` · `"snare_dry_muted"` · `"snare_prepared"` · `"snare_spring"` · `"snare_brush"` · `"snare_stir_long"` · `"snare_stir_long_light"` · `"snare_stir_short"` · `"snare_stir_short_light"` · `"china_cymbal"` · `"cymbal_stack"` · `"cymbal_stack_edge"` · `"sizzle_ride"` · `"sizzle_ride_edge"` · `"sizzle_ride_bell"` · `"bongo_hi"` · `"bongo_lo"` · `"conga"` · `"conga_slap"` · `"darbuka"` · `"darbuka_tek"` · `"frame_drum"` · `"cajon"` · `"agogo_hi"` · `"agogo_lo"` · `"cabasa"` · `"claves"` · `"cowbell"` · `"guiro"` · `"shaker"` · `"tambourine"` · `"tambourine_shake"` · `"triangle"` · `"triangle_mute"` · `"woodblock"` · `"gong"` · `"sleigh_bells"` · `"log_drum_hi"` · `"log_drum_lo"` · `"didgeridoo_bark"` · `"didgeridoo_short"` · `"didgeridoo_tap"` · `"suspended_cymbal_hit"` · `"suspended_cymbal_bell"` · `"suspended_cymbal_stick"` · `"suspended_cymbal_bowed"` · `"cymbal_swell_1_5s"` · `"cymbal_swell_2s"` · `"cymbal_swell_4s"` · `"cymbal_swell_7_5s"` · `"suspended_cymbal_scrape"` · `"mark_tree_up"` · `"mark_tree_down"` · `"mark_tree_fast_up"` · `"mark_tree_slow_up"` · `"mark_tree_slow_down"` · `"mark_tree_random"` · `"bell_tree"` · `"vibraslap"` · `"anvil"` · `"brake_drum"` · `"brake_drum_bowed"` · `"finger_cymbals"` · `"flexatone"` · `"flexatone_fast"` · `"flexatone_long"` · `"flexatone_extra_long"` · `"flexatone_slap"` · `"ratchet_crank"` · `"ratchet_fast"` · `"ratchet_slow"` · `"slapstick"` · `"ukulele_body_tap"` · `"ukulele_chuck"` · `"castanets"` · `"maracas_forward"` · `"maracas_backward"`

## Automation

A Sweep or BusSweep. track.fader/track.pan replace the removed compact fader/pan knobs.

### Syntax

```text
Sweep
| BusSweep
```

### Related

[`Sweep`](#sweep) · [`BusSweep`](#bussweep)

## CenteredLfo

Tempo-synchronized sine automation for a native-unit param target.

### Syntax

```text
{ "atBeat": …, "beats": …, "period": …, "depth": …, "center": … }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `atBeat` | `number` | yes |  | ≥ 0 — LFO start on the global score timeline, in beats. |
| `beats` | `number` | yes |  | > 0 — LFO duration in beats. |
| `period` | `number` | yes |  | > 0 — Beats per sine cycle. |
| `depth` | `number` | yes |  | > 0 — Full swing width in target units. |
| `center` | `number` | yes |  | Resting value in target-native units. |

## CompactLfo

Tempo-synchronized sine automation in the compact 0..10 knob scale.

### Syntax

```text
{ "atBeat": …, "beats": …, "period": …, "depth": …, ["center": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `atBeat` | `number` | yes |  | ≥ 0 — LFO start on the global score timeline, in beats. |
| `beats` | `number` | yes |  | > 0 — LFO duration in beats. |
| `period` | `number` | yes |  | > 0 — Beats per sine cycle. |
| `depth` | `number` | yes |  | > 0; ≤ 10 — Full swing width in knob units. |
| `center` | `number` | no | `5` | ≥ 0; ≤ 10 — Optional resting value. |

## DrumHitName

A factory drum or declared exd_ custom drum used inside a drums lane.

### Syntax

```text
FactoryDrumHitName | one of the keys in Score.drumSynths Dictionary<string, CustomDrumPatch>
```

### Constraints

- For a custom drum, write the drumSynths dictionary key, not the CustomDrumPatch object.
- An exd_ value must exactly match a key declared in the same Score's drumSynths dictionary.

### Related

[`FactoryDrumHitName`](#factorydrumhitname)

## GranularCurve

A constant number or a normalized phase curve.

### Syntax

```text
number | GranularCurvePoint[]
```

### Constraints

- The array form contains 2..32 points, begins at phase 0, ends at phase 1, and uses strictly increasing phases.
- The property using the curve sets the value range: Granular.density uses 1..200; Granular.scan uses 0..1.

### Related

[`GranularCurvePoint`](#granularcurvepoint)

## GranularCurvePoint

Two-number point [phase, value]. Phase is 0..1 from the beginning to the end of the note; value is 1..200 grains/second for density and source position 0..1 for scan.

### Syntax

```text
[number, number]
```

### Constraints

- A GranularCurvePoint always contains exactly two numbers.

## GrooveUse

A named groove with independent timing/velocity strength and optional phase override.

### Syntax

```text
{ ["map": …], ["amount": …], ["timing": …], ["velocity": …], ["phaseBeat": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `map` | `string` | no |  | Exact key from Score.grooves. |
| `amount` | `number` | no | inherited GrooveUse.amount; otherwise 1 | ≥ 0; ≤ 1 — Master timing and velocity blend. |
| `timing` | `number` | no | inherited GrooveUse.timing; otherwise 1 | ≥ 0; ≤ 1 — Additional timing-only blend. |
| `velocity` | `number` | no | inherited GrooveUse.velocity; otherwise 1 | ≥ 0; ≤ 1 — Additional velocity/accent-only blend. |
| `phaseBeat` | `number` | no | inherited GrooveUse.phaseBeat; otherwise Groove.phaseBeat | ≥ -1000000; ≤ 1000000 — Override the map's global phase anchor. |

### Constraints

- map must resolve when supplied; without map, this object needs an inherited groove map.
- amount blends both timing and force, timing multiplies only the timing blend, and velocity multiplies only the velocity/accent blend.
- A GrooveUse overrides only the fields it supplies, including when it supplies a new map. A string GrooveBinding selects a map and resets amount/timing/velocity to 1 and phaseBeat to that Groove's phaseBeat.

## InstrumentName

A factory instrument, drums lane, declared custom synth/drum, or declared resample.

### Syntax

```text
PitchedInstrumentName
| FactoryDrumHitName
| "drums"
| one of the keys in Score.synths Dictionary<string, SynthPatch>
| one of the keys in Score.drumSynths Dictionary<string, CustomDrumPatch>
| one of the keys in Score.resamples Dictionary<string, Resample>
```

### Constraints

- Every non-factory name must resolve to a matching top-level declaration.

### Related

[`PitchedInstrumentName`](#pitchedinstrumentname) · [`FactoryDrumHitName`](#factorydrumhitname)

## KnobKeyframe

Compact automation point with a public 0..10 knob value.

### Syntax

```text
[beat, knobValue]
[beat, knobValue, curve]
```

### Constraints

- The optional curve belongs to the destination keyframe: it shapes movement from the previous keyframe into this one. Omitting it means linear. A curve on the first keyframe has no effect.
- Within a segment, let f run from 0 at the previous keyframe to 1 at the destination. linear uses f; exp uses f^3; log uses 1-(1-f)^3; scurve uses f^2*(3-2*f).
- step holds the previous keyframe's value for the whole segment, then jumps to the destination value exactly at the destination beat.

### Related

[`AutomationCurve`](#automationcurve)

## ModRoute

One bounded dual-patch modulation route.

### Syntax

```text
{ "source": …, "target": …, "amount": … }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `source` | `ModulationSource` | yes |  |  |
| `target` | `ModulationTarget` | yes |  |  |
| `amount` | `number` | yes |  | Signed depth in target-native units. |

### Value ranges

| Value / target | Range |
|---|---|
| `pitch1` | -48..48 semitones |
| `pitch2` | -48..48 semitones |
| `cutoff` | -12000..12000 Hz |
| `resonance` | -0.9..0.9 |
| `blend` | -1..1 |
| `sync` | -1..1 |
| `ring` | -1..1 |
| `shape` | -1..1 |
| `pan` | -1..1 |

### Constraints

- amount must remain inside the selected target's documented range; out-of-range values are compile errors and are never clamped.
- Pitch targets require a pitched target oscillator; sync requires two pitched oscillators.

### Related

[`ModulationSource`](#modulationsource) · [`ModulationTarget`](#modulationtarget)

## PitchRange

Ascending absolute-pitch range written as [lowest pitch, highest pitch]. Both endpoints are inclusive.

### Syntax

```text
[AbsolutePitch, AbsolutePitch]
```

### Constraints

- The first pitch must not be above the second.

### Examples

```json
[
  "C3",
  "C5"
]
```

### Related

[`AbsolutePitch`](#absolutepitch)

## RegionRange

[startBeat, endBeat], both relative to the beginning of the capture.

### Syntax

```text
[number, number]
```

### Constraints

- end must be greater than start and no later than the capture length.

## ResampleSlices

Optional single method for exposing named or numbered regions.

### Syntax

```text
{ "gridBeats": … }
| { "regions": … }
| { "transients": … }
```

### Alternatives

#### Grid slices

Equal beat-length slices named 0, 1, 2, ...

##### Syntax

```text
{ "gridBeats": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `gridBeats` | `number` | yes |  | ≥ 0.015625 — Length of every generated slice in capture-relative beats. |

#### Explicit regions

Named capture-relative beat ranges.

##### Syntax

```text
{ "regions": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `regions` | `Dictionary<string, [number, number]>` | yes |  | 1..128 entries |

#### Transient slices

Renderer-detected transient regions.

##### Syntax

```text
{ "transients": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `transients` | `object` | yes |  | Onset detector settings. |

##### transients

Onset detector settings.

###### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `threshold` | `number` | no | `0.22` | ≥ 0.01; ≤ 1 — Relative onset threshold. |
| `minGapMs` | `number` | no | `60` | ≥ 10; ≤ 2000 — Minimum onset separation in milliseconds. |
| `max` | `integer` | no | `32` | ≥ 1; ≤ 128 — Maximum regions. |

### Related

[`RegionRange`](#regionrange)

## ResampleSource

Exactly one authored track or capturable bus.

### Syntax

```text
{ "track": … }
| { "bus": … }
```

### Alternatives

#### Track capture source

Capture one rendered lane by an exact direct Track id or top-level Pattern key.

##### Syntax

```text
{ "track": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `track` | `string` | yes |  | Exact id property of one top-level Track, or exact key from Score.patterns. |

#### Bus capture source

Capture a built-in musical or declared custom bus.

##### Syntax

```text
{ "bus": … }
```

##### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `bus` | `TrackBusName` | yes |  |  |

### Constraints

- The symbol must resolve; hall, plate, and master are not capturable buses.

### Related

[`TrackBusName`](#trackbusname)

## SynthEnvelope

ADSR envelope in seconds plus normalized sustain. It has no universal defaults: DualSynthPatch.amp and DualSynthPatch.env2 each document the defaults inherited by omitted fields.

### Syntax

```text
{ ["attack": …], ["decay": …], ["sustain": …], ["release": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `attack` | `number` | no |  | ≥ 0.001; ≤ 4 — Attack in seconds. |
| `decay` | `number` | no |  | ≥ 0.005; ≤ 8 — Decay in seconds. |
| `sustain` | `number` | no |  | ≥ 0; ≤ 1 — Sustain. |
| `release` | `number` | no |  | ≥ 0.005; ≤ 8 — Release in seconds. |

## SynthLfo

Free-running patch LFO. It has no universal defaults: DualSynthPatch.lfo1 and DualSynthPatch.lfo2 each document the defaults inherited by omitted fields.

### Syntax

```text
{ ["shape": …], ["rateHz": …], ["phase": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `shape` | `SynthLfoShape` | no |  |  |
| `rateHz` | `number` | no |  | ≥ 0.01; ≤ 40 — Rate in Hz. |
| `phase` | `number` | no |  | ≥ 0; ≤ 1 — Initial cycle phase, where 0 is the beginning and 1 is one complete cycle. |

### Related

[`SynthLfoShape`](#synthlfoshape)

## TrackBusName

Built-in musical role or declared custom-bus name.

### Syntax

```text
BusRole | one of the keys in Score.buses Dictionary<string, Bus>
```

### Related

[`BusRole`](#busrole)

## TrackControls

Combined static lane controls: pitched-synth front panel plus lane effects. Every numeric control must be a JSON number in its documented range; omission preserves the stated default or selected synth patch value.

### Syntax

```text
{ ["echo": …], ["pump": …], ["crush": …], ["chorus": …], ["flanger": …], ["phaser": …], ["tremolo": …], ["wah": …], ["reverb": …], ["lowpass": …], ["highpass": …], ["res": …], ["tape": …], ["punch": …], ["smooth": …], ["squash": …], ["plate": …], ["vinyl": …], ["drive": …], ["pumpRelease": …], ["pumpHold": …], ["pumpShape": …], ["wet": …], ["eqLow": …], ["eqMid": …], ["eqHigh": …], ["pumpFrom": …], ["cutoff": …], ["resonance": …], ["envMod": …], ["attack": …], ["decay": …], ["sustain": …], ["release": …], ["detune": …], ["sub": …], ["noise": …], ["lfoRate": …], ["wobble": …], ["vibrato": …], ["sweep": …], ["pitchDrop": …] }
```

### Properties

| Property | Type | Required | Default | Range / meaning |
|---|---|---:|---|---|
| `echo` | `number` | no | `0` | ≥ 0; ≤ 10 — Tempo-synchronized dotted-eighth feedback delay amount. |
| `pump` | `number` | no | `0` | ≥ 0; ≤ 10 — Onset-triggered ducking depth; 0 is off and 10 ducks by up to 85%. |
| `crush` | `number` | no | `0` | ≥ 0; ≤ 10 — Bit-depth and sample-rate reduction amount. |
| `chorus` | `number` | no | `0` | ≥ 0; ≤ 10 — Short modulated-delay widening amount. |
| `flanger` | `number` | no | `0` | ≥ 0; ≤ 10 — Short feedback-delay sweep amount. |
| `phaser` | `number` | no | `0` | ≥ 0; ≤ 10 — Swept phase-notch amount. |
| `tremolo` | `number` | no | `0` | ≥ 0; ≤ 10 — Tempo-synchronized amplitude-modulation amount. |
| `wah` | `number` | no | `0` | ≥ 0; ≤ 10 — Envelope-following filter amount. |
| `reverb` | `number` | no | `0` | ≥ 0; ≤ 10 — Send level to the shared hall; not affected by wet. |
| `lowpass` | `number` | no | `0` | ≥ 0; ≤ 10 — Track low-pass filter: 0 is open/bypassed and 10 closes toward low frequencies. |
| `highpass` | `number` | no | `0` | ≥ 0; ≤ 10 — Track high-pass filter: 0 is open/bypassed and 10 removes frequencies up to about 2.4 kHz. |
| `res` | `number` | no | `0` | ≥ 0; ≤ 10 — Static resonance baseline shared by the track's lowpass and highpass. A sweep's res overrides only its named filter from that sweep's first beat onward. |
| `tape` | `number` | no | `0` | ≥ 0; ≤ 10 — Tape-style saturation, softening, and wobble amount. |
| `punch` | `number` | no | `0` | ≥ 0; ≤ 10 — Transient attack enhancement amount. |
| `smooth` | `number` | no | `0` | ≥ 0; ≤ 10 — Slow program-dependent leveling amount. |
| `squash` | `number` | no | `0` | ≥ 0; ≤ 10 — Fast aggressive compression amount. |
| `plate` | `number` | no | `0` | ≥ 0; ≤ 10 — Send level to the shared bright plate; not affected by wet. |
| `vinyl` | `number` | no | `0` | ≥ 0; ≤ 10 — Record-player bandwidth, wobble, and deterministic crackle amount. |
| `drive` | `number` | no | selected synth patch value on pitched synths; 0 on recorded sounds and drums | ≥ 0; ≤ 10 — Pitched-synth voice saturation on a pitched synth; track distortion on a recorded sound or drum. |
| `pumpRelease` | `number` | no | 0.6 beats | ≥ 0; ≤ 10 — Pump recovery duration control: 0 is 0.15 beats and 10 is 1.5 beats. |
| `pumpHold` | `number` | no | `0` | ≥ 0; ≤ 10 — Fully ducked hold before recovery: 0 is none and 10 is 120 ms. |
| `pumpShape` | `number` | no | recovery exponent 1.5 | ≥ 0; ≤ 10 — Pump recovery-curve shape: higher values recover later. |
| `wet` | `number` | no | `10` | ≥ 0; ≤ 10 — Wet share of the color chain (EQ, wah, drive, crush, modulation, tremolo, echo, tape, dynamics, and vinyl). Filters, pump, hall, and plate are outside this blend. |
| `eqLow` | `number` | no | `0` | ≥ -12; ≤ 12 — Low-shelf gain in dB. |
| `eqMid` | `number` | no | `0` | ≥ -12; ≤ 12 — Mid-band gain in dB. |
| `eqHigh` | `number` | no | `0` | ≥ -12; ≤ 12 — High-shelf gain in dB. |
| `pumpFrom` | `PumpSource[]` | no |  | 1..16 items — One or more exact public sources whose note onsets trigger pump. Array order has no effect. |
| `cutoff` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth filter cutoff. Omission preserves the selected patch value. |
| `resonance` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth filter resonance; distinct from the track filter control res. Omission preserves the selected patch value. |
| `envMod` | `number` | no |  | ≥ 0; ≤ 10 — Amount the pitched synth's filter envelope moves its cutoff per note. Omission preserves the selected patch value. |
| `attack` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude-envelope attack time. Omission preserves the selected patch value. |
| `decay` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude and filter-envelope decay time. Omission preserves the selected patch value. |
| `sustain` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth held amplitude after decay. Omission preserves the selected patch value. |
| `release` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth amplitude-envelope release time. Omission preserves the selected patch value. |
| `detune` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth unison spread. Omission preserves the selected patch value. |
| `sub` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth sub-oscillator level. Omission preserves the selected patch value. |
| `noise` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth noise level. Omission preserves the selected patch value. |
| `lfoRate` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO rate. Omission preserves the selected patch value. |
| `wobble` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO-to-filter depth. Omission preserves the selected patch value. |
| `vibrato` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth LFO-to-pitch depth. Omission preserves the selected patch value. |
| `sweep` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth cutoff movement across each note. Omission preserves the selected patch value. |
| `pitchDrop` | `number` | no |  | ≥ 0; ≤ 10 — Pitched-synth attack pitch displacement that converges to the written pitch. Omission preserves the selected patch value. |

### Constraints

- Synth controls affect pitched synth instruments only; they do not control recorded instruments or synthesized/recorded drums. Track effects work on every instrument.
- Unknown fields and invalid numeric control values are compiler errors; numeric controls require finite JSON numbers within their documented ranges.
- pumpFrom is required when static pump is greater than 0 or a pump Sweep targets the lane. Its value is PumpSource[], never a string.
- eqLow/eqMid/eqHigh use dB rather than 0..10.

### Related

[`PumpSource`](#pumpsource)

