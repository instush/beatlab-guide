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

One oscillator modulates another's pitch. Fast modulation creates **sidebands** —
new partials above and below the carrier.

- **Ratio** determines harmonicity. Integer ratios (1:1, 2:1) give pitched, musical
  tones; non-integer ratios give bells and metallic noise.
- **Index** determines how much spectrum is generated.
- **Envelope the index**, don't fix it: a falling index (peak ~5.9, decaying over
  70 ms, resting at 0.4) gives a bright attack settling into a purer sustain. This
  one trick is most of what makes FM basses, bells and electric pianos work.

---

## 7. Dynamics and compression {#compression}

### 7.1 What the controls actually do

- **Threshold** — the level above which reduction begins. Below it, nothing happens.
- **Ratio** — how hard it pulls down above the threshold. 4:1 is a general default;
  12:1 and above is ducking or effect territory.
- **Knee** — hard knee switches abruptly at the threshold; soft knee eases in.
- **Makeup gain** — restores the level compression removed.

### 7.2 Attack and release are the whole instrument

**Attack decides how much transient survives.** Sub-millisecond attack (0.3 ms)
catches the very first click, shrinking the transient — the drum becomes softer and
rounder. On drums, start between **10 and 30 ms** and deliberately let the transient
through, compressing what follows it.

**Release must resolve before the next hit.** A 700 ms release at 140 BPM never
recovers between hits and the groove stops breathing; ~110 ms (one sixteenth at that
tempo) tracks the groove. Release is a tempo value, not a taste value.

### 7.3 Always compare level-matched

Compression lowers peaks; makeup raises everything. Compared un-matched, compression
always sounds "better" because it is simply louder. Level-matched, the honest
description is: *same loudness, but the quiet detail steps forward.* Judge it that
way or you are not judging compression at all.

### 7.4 Compressor character

At identical settings and matched level, the topology still changes the sound:

| Type | Character | Typical use |
|---|---|---|
| VCA | clean, precise, transparent | the general-purpose workhorse |
| FET | fast, aggressive | drums, snare edge |
| Opto | smooth, slow, breathing release | vocals, bus glue |
| Vari-Mu | warm, glue | mix bus |

### 7.5 Two structural uses

- **Parallel compression** — duplicate, crush the copy (20:1, 0.5 ms attack), blend
  it ~35% under the dry. Keeps the transient *and* adds weight, which serial
  compression cannot do simultaneously.
- **Sidechain** — a compressor keyed from another track. Kick ducking a pad at 12:1
  with 200 ms release makes room rhythmically. See §3 for the bass case, and §9 for
  ducking reverb returns.

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
| Resonance ride | cutoff rising, resonance 20% → 85% peaking at bar 3 | peak in the middle, then back off |
| Noise riser | band-pass filter rising to 7.1 kHz **and** volume −7.8 → +24 dB | build-up (two lanes, not one) |
| Reverb throw | send normally 0%, spiked for one hit at beat 16, 4.5 s decay | fills a turnaround without washing the groove |
| EQ bell sweep | +14 dB, Q 5, centre 200 Hz → 6 kHz over 4 bars | reads as "leaving" |

Note the pattern: the *same* cutoff ramp is a groove element at one bar and a build
at four. Length is what assigns meaning, which is why automation should be written
against the arrangement, not against taste.

Autoduck as an alternative to sidechain compression: rather than a compressor, draw
the duck curve directly — 1/4 sync, −24 dB depth, dip shape. A drawn curve is
deterministic and shapeable in ways a detector's envelope is not.

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

−8 LUFS is a *club* target and deliberately louder than streaming normalization
(−14 LUFS). Choose the target for the destination; mastering a streaming release to
−8 LUFS buys nothing but distortion, since the platform will turn it down anyway.

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

AUTOMATE    (parameter, start, end, bars, curve)
            1 bar = groove; 4 bars = build

ARRANGE     16-bar intro, 32-bar drop, reset the ear every 16 bars

MIX         stage -10 dBFS; HP everything but kick/bass at 150 Hz 24 dB/oct
            pre-master -6 dBFS / -18 LUFS
            master -1 dBTP ceiling, -8 LUFS club
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
