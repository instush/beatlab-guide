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

Use this as a creative expansion of the score guide's B.5 workflow, not a second
checklist to complete. Revisit decisions when sound, phrase or form suggests a
better direction. All planning stays internal; the music response is JSON only.

1. INTENT AND CONTRAST
   Extract style, duration, mood, references and exclusions. Translate references
   into musical attributes. Choose a guiding relationship such as mechanical /
   human, tender / ominous or repetitive / evolving. Section 1's blueprint is an
   optional aid; fill only the slots that clarify the idea.

2. MATERIAL WITH ITS SOUND
   Invent a recognizable rhythmic, pitched, harmonic or timbral seed, or a few
   related seeds when needed. Decide what anchors the music and what can mutate.
   Try the main relationship in a short passage, often 2-4 bars for groove music.
   Revise timing, gaps, envelopes and interaction together. A drone may need a
   longer listening window; no universal loop length or number of seeds applies.

3. DEVELOPMENT AND PAYOFF
   Explore variants with audible preserved traits: an answering rhythm, thinned
   fragment, new harmony, timbral fracture or completed ending. Keep only useful
   variants. If a late payoff suggests itself first, compose it and work backward
   to what would make it meaningful; otherwise let the material suggest the form.

4. SCENES AND FOCUS
   Map the duration into scenes, identifying what remains recognizable and what
   changes. At an entrance, consider whether another voice should leave or recede.
   Ask why the next scene follows this one: extension, contrast, resolution,
   delayed reply, intentional hold or rupture. Choose an ending rather than
   letting the repeat count decide it. No fixed scene count or drop is required.

5. REALIZATION
   Translate the plan through the score guide's exact syntax. Use the conceptual
   crosswalk in Section 16; it does not authorize additional fields. Check that
   timing, sound and orchestration actually expose the intended relationships.

6. REVIEW AND REVISION
   Apply technical validation separately from musical evaluation (Section 20;
   score guide I.1). With playback, listen without looking and diagnose the felt
   result using Section 15. Without it, inspect onsets, phrase spans, harmonic
   motion and density conservatively. Fix a specific weakness, then re-check the
   affected passage and boundaries. Never claim a listening test you did not do.

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

18.1 EXECUTABLE MINIATURE: TEACH A GAP, THEN ANSWER IT

This 12-second study isolates Study B's gap-and-answer relationship. It is not a
complete tech-house production or a template for its section lengths. At 120 BPM,
each four-beat pattern lasts two seconds. Local beat 3 means the fourth beat.

  Beats 0-8:   A repeats twice; hats answer its empty fourth beat.
  Beats 8-12:  the bass repeats, but the hat answer disappears.
  Beats 12-16: FILLED preserves A and adds a bass note in the learned gap.
  Beats 16-20: the original bass gap and hat answer return.
  Beat 20:    one root and kick close the study; the remaining time lets them decay.

```json
{
  "bpm":120,"durationSec":12,"seed":23,
  "patterns":{
    "KICK":{"instrument":"drums","lenBeats":4,
      "notes":["0 e_kick 0.8","1 e_kick 0.8","2 e_kick 0.8","3 e_kick 0.8"]},
    "A":{"instrument":"moog_bass","lenBeats":4,
      "notes":["0 A1 0.5 0.8","0.75 C2 0.25 0.65","1.5 E2 0.5 0.75","2.5 A1 0.25 0.65"]},
    "ANSWER":{"instrument":"drums","lenBeats":4,
      "notes":["3 e_hat_closed 0.55","3.5 e_hat_closed 0.4"]},
    "FILLED":{"extends":"A","notes":["3 A1 0.5 0.8"]},
    "END":{"extends":"A","only":[0]},
    "LAST_KICK":{"extends":"KICK","only":[0]}
  },
  "arrangement":[
    {"pattern":"KICK","atBeat":0,"repeat":5},
    {"pattern":"A","atBeat":0,"repeat":3},
    {"pattern":"ANSWER","atBeat":0,"repeat":2},
    {"pattern":"FILLED","atBeat":12},
    {"pattern":"A","atBeat":16},
    {"pattern":"ANSWER","atBeat":16},
    {"pattern":"END","atBeat":20},
    {"pattern":"LAST_KICK","atBeat":20}
  ]
}
```

The new bass event is deterministic and placed once; adding it to A itself would
erase the earlier absence that gives it meaning. The return restores the gap
without adding another instrument. With playback, compare against a version
using A at beat 12 too: does the single changed note register as an answer?
If the relationship is weak, adjust the phrase, register or envelope before
adding effects. Write new material for the user's piece; reuse the method.

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

TECHNICAL VALIDATION — required independently of artistic intent:
  [ ] Fields, values, symbols and references conform to the current score guide.
  [ ] Pattern beats and direct-track seconds, repeats and duration are correct.
  [ ] Custom sounds, routing, effects and automation satisfy their contracts.
  [ ] The response is one valid JSON object, with no prose or invented features.

Use the score guide's I.1 for the full technical check. Its documented language
is authoritative; a schema or compiler is additional support when accessible.

MUSICAL EVALUATION — use the relevant questions for the intended style:

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

F. REALIZATION
  [ ] Sound, register, level and timing expose the relationships the plan describes.
  [ ] Essential payoffs are deterministic unless chance itself is the concept.
  [ ] Review is based on actual playback where available, with no invented
      listening or measurement claims when only the score can be inspected.

Musical heuristics may be set aside for an artistic reason. Technical validity
and the JSON-only response contract are never optional. Revise the most important
weakness and re-check the result rather than maximizing every checklist item.

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
