# Failure modes

Defects are not the problem. Continuity is. Plan for these five and most of the
frustration goes away.

## 1. Continuity drifts, and it compounds

Extend when the same physical moment continues. Reference video when you cut to a new
angle but need the room remembered. Both together for a hard case.

After a few chained extensions, re-seed from the **original** clip rather than the last
extended segment. Drift compounds along a chain, and each link inherits the previous
link's mistakes as if they were canon.

Give every reference a clear role. Conflicting references reduce consistency, so drop
environment stills once generated footage has established its own geography.

## 2. Text loses to visible geometry, every time

When the model ignores an instruction, something in frame is contradicting it. More
words will not win. Change what the camera can see: move the camera, or supply a
reference that shows the truth.

## 3. Every clip eases out

The model settles the shot before it ends. Frame-to-frame motion energy in the final
eight frames falls to a third or a quarter of mid-clip.

So the last frames are both the stillest and the most similar to whatever comes next,
and cutting there produces a twitch rather than a cut. **Trim 8 to 12 frames off the
tail of every clip.** Past about 12 frames the curve flattens.

Diagnose it with PSNR across the join versus PSNR two frames apart inside the clip. If
across is greater than or equal to within, it is a jump cut and not bad footage. The fix
is a trim, not a regeneration.

## 4. The artistic tax

Texture degrades with runtime. On cheap tiers, measured brushwork was gone by two
seconds. A photoreal take survives its own length; a stylised one degrades while it runs.

So the more stylised the look, the more stills you need: shorter clips, more start
frames, and the style budget paid in images rather than in prompt words.

Prefer the shortest duration the platform allows, and judge the texture at the frame you
will actually cut on rather than at the end of the clip.

## 5. Budget the iteration, not the render

About seven generations to land one beat. Roughly $80 for a finished minute. Nearly all
of it is spent on takes you throw away, so optimise the cost of being wrong rather than
the cost of being right.

Generate at 720 and upres in post. Native 4K runs about a dollar a second and a good
upscaler closes most of the gap for a fraction of it.

## Two habits worth having

**Salvage, do not discard.** A generation that fails as a whole usually is not a total
loss. Cut the good seconds out as selects. A bad four-shot take routinely contains two
keepers.

**One shot per generation is not a rule.** It is a trade. A multi-shot take holds
wardrobe, light and geography across its own cut for nothing, which is consistency you
would otherwise have to engineer. But a take is atomic: one bad shot inside it and you
pay for all of them again, and no per-shot pass in post can reach inside a composite to
fix, grade or retime a single shot. Short and stable goes in together. Anything risky
gets its own generation.

## Change one thing at a time

Before the second attempt, name which criterion failed: texture, camera lock, subject
resolution, or pace. Then change exactly one thing. Two changes in one re-run buys no
finding and costs the same.

Before the third attempt on the same string, ask whether the **frame** is the problem
rather than the words. A model that renames its own output is telling you what it thinks
the shot is about.
