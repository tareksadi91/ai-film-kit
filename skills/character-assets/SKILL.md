---
name: character-assets
description: Build the reusable image assets a film runs on. Character sheets, environment plates, prop sheets, and the reference declaration block that tells a video model what each one is for. Use when the user is starting a film, needs a character to stay the same across shots, needs a location to stay the same across shots, or is deciding which references to attach to a generation.
---

# Character assets

A character is not one picture. It is a locked face, a set of identity markers, and a
library of angles that every downstream generation points back at.

Build in this order and do not skip forward. An outfit cannot go on a face that is not
locked. A sheet cannot be built before an approved single image exists.

```
style plate  ->  face lock  ->  outfit  ->  character sheet
             ->  environment plate
```

## 1. One style plate first

A single image carrying the treatment, and nothing else. Every later asset is generated
*from* it, which is what makes them agree with each other.

Generate this on whichever tool has the widest stylistic range. In 2026 that is still
MidJourney. The precision models render competent; they do not invent a direction.

Lock the settings tail and never change it for the life of the film. The subject clause
changes every shot. The tail does not.

## 2. Face lock, then outfit, then sheet

Feed the style plate alongside the character description. Ask for the sheet explicitly:

```
create a character sheet of the person in image 2, in the same style and grading as
image 1: front, three-quarter, profile, plus two seated poses and one closeup
```

Three panels is a sensible default: full body front, full body rear, and a tight
chest-up face lock. Six panels starves each face panel of resolution, so only go wider
when the extra angles are doing real work.

Precision editors are the right tool here. They are weak at art direction and strong at
obedience, which is exactly backwards from the style tool and exactly what this step
needs.

## The rule that surprises everyone: a plate carries no light

Two things sound like one thing and are not.

**Biological realism: fully on.** Real pore texture, peach fuzz, strand hair with
flyaways, fabric weave and drape, metal with surface detail, eyes with depth.

**Photographic capture behaviour: off.** No key direction, no shadow side, no cast
shadow, no contact shadow, no falloff on the background, no spill, no bokeh, no
vignette, no flare, no haze.

These are references, not finished frames. Any lighting baked into a plate is inherited
and amplified by every generation that reads it, and it fights whatever lighting the
actual scene wants. Writing "photographed on a real set by a real photographer" switches
on the second axis along with the first, and the second axis is what poisons a reference.

Flat neutral grey field. Shadowless. The scene prompt does all the lighting later.

## 3. Environment plates

Same style plate, same grading, one plate per location.

```
a painting of <the location>, using the same colour grading and image style as the
uploaded reference
```

Environmental consistency is the named hard part of this whole craft, and the plate is
what fixes it. An environment plate does the opposite job from a character sheet: it is
nothing but light and geography. Where the window is, how far the table sits from it,
what the room is made of. No character in it.

## Identity that has to hold

- **Permanent features are declared permanent.** "The blunt bangs are permanent and
  present in every frame."
- **Attributes that drift get an inline negation.** "BROWN eyes, never blue, never
  green."
- **State-conditional features carry their state and the reason.** "No horns in this
  scene, omit them entirely, horns are battle-state only." Without the reason the model
  splits the difference.
- **Negate invented detail explicitly.** Clean clear face, no beauty marks, no facial
  markings. The model invents facial detail otherwise.
- **Props carry scale relative to a body.** "A 20cm knife, noticeably shorter than his
  forearm, it reads short and not as a sword." Scale is the one that fails.
- **Wardrobe is restated every prompt, written economically.** One clause per garment:
  colour, fabric, cut, how it sits.

## 4. Declare every reference, with its job

This block goes first, above everything. The model is looking at a pile of images with
no idea which is a person, which is a room and which is a prop. A bare handle in the
middle of an action line asks it to infer that, and inference is where continuity goes.

```
@rei        - the main character, a courier. Character sheet: front / side / back.
@device     - a prop. Sheet: inactive and active states.
@shop-plate - ENVIRONMENT PLATE. Controls geography, materials and light direction only.
@shop-reel  - REFERENCE VIDEO. Room layout and light. Does not define the current
              moment, do not inherit its camera.
```

One line each: the handle, what kind of thing it is, and what job it does. **A reference
with no declared job is the one the model reinterprets.**

Scope a reference explicitly when it should only govern part of the frame. "Controls
geography, materials, atmosphere and light direction only" is a real instruction and the
model honours it.

**Handles come from filenames, so the filename is the interface.** Where a shot numbering
scheme fights a short handle, keep the shot number. It is load-bearing for the manifest
and the edit; the handle is typed once.

## 5. Declaring is free. Attaching is metered

Write the full declaration block every time. Words cost nothing. The upload is what the
platform bills, and on at least one platform video references are priced by duration: a
13 second reference reel added 380 credits to a 5 second generation, more than the
generation itself.

So:

- **An extend already carries what you would attach.** The source is video of the
  character, the room, the wardrobe and the light. Re-attaching the sheet on top pays
  twice for facts already in the seed.
- **Never attach two references carrying the same fact.** A frame cut from a reel and the
  reel itself are one piece of geometry billed twice. For a locked-off shot the still
  does everything the video would.
- **Pin what would actually drift.** Identity, canonical geometry, a prop's design. Mood
  plates do not drift. They did their job when the sheets were made from them and should
  rarely be attached to a shot again.
- **Generated footage outranks the original plate.** Once shots have established a room's
  geography, prefer them and stop feeding the original still back in.

## What to do when it ignores you

When the model ignores a written instruction, look for a conflicting visible cue before
adding more words. On one film a large glass pane behind a character read as the exit,
and the model kept promoting it into a sliding door. "Hinged door", "door to her right"
and "not a sliding door" all failed. The visible geometry outranked the prompt every
time.

The fix was a reference showing where the entrance actually is, and then a camera that
does not contain the pane. It was a spatial problem wearing a wording problem's clothes.
