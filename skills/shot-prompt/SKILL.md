---
name: shot-prompt
description: Write a production prompt for an AI video model (Seedance 2 / 2.5, Kling, Veo, Gemini Omni) from a shot description. Use whenever the user wants a video prompt, wants a scene broken into shots, is extending or continuing an existing clip, or asks why a generation came back wrong. Covers the mode fork, the prompt spine, lens locks in degrees, the geometry map, and the rules that stop a shot drifting.
---

# Shot prompt

A prompt is a production document. Who is in frame, where they stand, what they do,
how it is filmed, and what must not change. If a word does not produce a visible pixel,
cut it.

## Step zero: settle the target before writing anything

Ask once, in one line, if the user has not said:

| | Seedance 2 | Seedance 2.5 | Gemini Omni | Kling 3 | Veo 3.1 |
|---|---|---|---|---|---|
| image references | 9 | 50 | few | none | 1 to 3, and never with a first frame |
| max runtime | 15s | 30s | short | 15s | 8s |
| multi-shot in one take | yes | yes | no | no | no |

A 2.5-shaped prompt fed to 2.0 loses references silently and truncates. A 2.0-shaped
prompt on 2.5 leaves half the identity budget unspent.

**More references is not automatically better.** Two references that teach the model
the same thing blend into an averaged face. Ship one.

## Then pick the mode. The two are mutually exclusive

| the shot is | mode | why |
|---|---|---|
| a continuation of a shot you keep | **first frame** | the frame already fixes cast, wardrobe, room, light and camera, more precisely than any sheet and for free |
| a cut to a new angle or place | **reference** | there is no frame to continue from, so identity and geometry come from sheets and plates |

In first-frame mode reference handles do not resolve. Write plain description and let
the image carry identity. Spend the words on action, camera and timing.

## The spine

Keep the order. It is the order the model reads.

```
REFS         one line per reference: the handle, what kind of thing it is, what job it does
SUBJECT      a noun inventory. who and what is on screen, wardrobe, hero objects. no verbs of motion
GEOMETRY     absolute lateral position, depth plane per subject, vertical relations
FIRST FRAME  what is already happening at frame one
CAMERA       shot size, lens lock in degrees, movement or the absence of it
LIGHT        direction, quality, temperature, named source
TIMING       beat by beat with timecodes, hard cuts called on the second
PRESERVE     what must hold
AVOID        every unwanted thing you have seen it add once
```

**Drop the action block.** Subject, action and timing narrate the same events three
times, and the timecodes are the part that demonstrably works. Asked for a 3.5 second
first shot, the model cut at 3.542 exactly. Let timing carry the narrative.

**Watch the ceiling.** Around 4,000 characters and the prompt is refused outright.
A three-shot ten-second prompt lands near 2,800 written this way and near 4,000 written
with everything restated.

## Lens locks go in degrees

The model treats a degree as a snap value and a millimetre as a suggestion. Write the
degree first, mm in parentheses, and never use an off-ladder value.

| FOV | mm | use for |
|---|---|---|
| 107° | 14 to 16mm | vast interior scale, epic establishing |
| 84° | 20 to 24mm | full-body blocking, immersive action |
| 63° | 28 to 35mm | observational, walking alongside |
| 47° | 40 to 50mm | universal medium, two-shot, waist-up |
| 34° | 60 to 70mm | compressed group, stacked depth planes |
| 29° | 75 to 85mm | isolated bust, detail on hands |
| 18° | 100 to 135mm | identity-hold close-up, held emotional beat |
| 12° | 180 to 200mm | hand insert, object close, texture |

Declare the lock per shot and repeat it at the top of every beat in a long take. An
unusual FOV gets averaged back toward normal unless you also say what it is not:
`strong telephoto compression, background pulled in close and thrown soft, no deep
focus, no full-room coverage`.

## The geometry map is what stops bodies drifting

State three things every time:

1. **Absolute lateral position.** LEFT, MIDDLE, RIGHT, and what sits off-frame in which
   direction.
2. **Depth plane per subject.** Foreground, mid-ground, background, and which planes
   are sharp.
3. **Vertical relations where they matter.** Above, below, suspended. These invert more
   readily than anything else.

Several figures in one frame go at **different depths, never in a row**. A line-up reads
as a posed group photo.

## First frame

One line. What is already happening at frame one. The model volunteers an empty
establishing frame, and on an eight-second clip that costs half a second of nothing.

```
FIRST FRAME: already mid-sentence, leaning in, mug already on the table.
No empty establishing frame, no static hold before the action starts.
```

## Promote the things it keeps dropping

Anything the model routinely softens or loses comes out of the prose into its own
ALL-CAPS block near the top: `THE GEOMETRY — CRITICAL:` then one exhaustive paragraph.

**Cap it at four.** Past four they compete and all of them dilute. The block is the
instruction, so downstream slots apply it and never restate it.

Useful blocks: the staging, the geometry, two distinct designs that must never merge,
nobody else is in the frame, everyone in the background is alive, the mouth stays
visible during dialogue.

## Five rules that decide whether it works

1. **Only what a camera could record.** "She turns toward the window and pauses" works.
   "Make it emotional" is nothing. Emotion is rendered in muscle: shoulders lift, jaw
   locks, exhales through the nose.
2. **Directions are frame-left and frame-right.** Her right is the frame's left. If you
   must use character-relative direction, label it as such in the same clause.
3. **Say each thing once.** The attached plate already describes the room. Restating it
   in subject, scene and preserve is three chances to contradict the image.
4. **A negative can summon what it forbids.** "Not a sliding door" puts a sliding door
   in the sentence. Prefer the positive: send the character the other way and never
   name the object.
5. **Never carve an exception into a negative block.** "No on-screen text, other than
   the shop sign" reopens the door and the captions come back. Real in-world text is
   described separately, as a physical object with shape, colour and placement.

## Measurables the model actually reads

Speed in km/h. Height in cm. Mass in kg. Distance in metres. Atmosphere as density plus
named depth planes. Contact rendered as deformation. Write `she stands 183cm to his
168cm`, never `she looks tall next to him`.

## Extending an existing clip

An extension is not written in this spine. The clip already is the scene, so
establishing blocks are the opposite of what you want. Two or three sentences of
continuous action, then one of constraint.

- **Extend** when the same physical moment continues and you want to inherit the last
  frame's camera and spatial state.
- **Reference video** when you want a new camera setup but need the model to remember
  the geography.
- **Both** for a hard continuity problem: latest clip as the extend source, a curated
  context reel as the reference video, each declared with its own job.

Extend anchors on the composition of the tail, not just the final frame, so whatever is
prominent at the end is inherited whether you name it or not. If the next shot needs a
part of the room the tail does not show, cut instead of extending.

After several chained extensions, re-seed from the original clip. Drift compounds along
a chain.

## Delivery

Title with runtime, the numbered reference list in attach order, then one fenced code
block holding the whole prompt. No preamble. Iterations ship as the revised full prompt,
never as "replace this line".

Two camera vantages on the same action are two prompts, whatever the runtime ceiling
allows. Runtime available is not runtime required.
