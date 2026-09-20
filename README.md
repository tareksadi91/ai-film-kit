# AI film kit

**Turn your agent into your assistant director.**

This is my working infrastructure for making film with AI, packaged so you can hand it
to an agent and have it run beside you. It knows how to build the assets, how to write
a shot prompt, and what usually goes wrong.

Nothing here is theory. All of it came out of trial and error: every rule was bought
with a failed generation, and most of them cost real credits. Where something came from
someone else's tutorial or someone else's skill file, it is in here only because it then
survived contact with an actual shoot.

## Install

**Claude Code:** copy the two folders in `skills/` into `~/.claude/skills/`.
**claude.ai:** upload each `skills/<name>/` folder as a skill.
**Anything else:** paste `SKILL.md` into the system prompt. They are plain markdown
and they do not depend on a runtime.

## Step 0, and it is not optional: give the agent a memory

Before any of this helps, make one file and tell the agent to read it at the start of
every session:

```
FINDINGS.md
```

One rule per failed generation. What you asked for, what came back, what the cause
turned out to be. That file is the whole product. An agent that forgets makes you pay
for the same lesson twice, and the lessons cost between 12 and 52 credits each.

Keep the working state somewhere you can look at it, not buried in a chat thread.
A single page you republish as it changes beats a folder of markdown nobody opens.

## The seven steps

1. **Set up the agent.** See above.
2. **Build the look.** One style plate. Lock the settings tail and never change it.
3. **Turn the look into assets.** Character sheets and environment plates, generated
   from that plate so they agree with each other. `skills/character-assets/`
4. **Map the scene.** Work through what happens with the agent, then draw the shots.
   Badly is fine. The drawing is what catches the angle you had not thought about.
5. **Pick the model per shot.** Reference ceilings and runtime ceilings differ, and
   they change the shape of the prompt, not just its trim.
6. **Write the prompt.** `skills/shot-prompt/`
7. **Expect the five failures.** `reference/failure-modes.md`

Steps 1 to 4 cost nothing. Nothing generates until step 5.

## What is measured and what is borrowed

Measured on my own footage, 2026: renderer behaviour, texture retention, the ease-out
at the end of every clip, the cost of a video reference, the way a visible object
outranks a written instruction.

Borrowed and then confirmed in use: the reference-locked chain (character sheet as
canon, environment plate for geography), the degree-based lens ladder, the geometry
map, the first-frame instruction.

Model rosters and prices move fast. Trust the tool's own UI over anything written here.
