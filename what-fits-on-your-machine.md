# What fits on your machine

A rough guide from memory to model size. The figures are for the 4-bit
versions, which is what you get by default, and they leave about a gigabyte
spare for the conversation itself.

---

## With a graphics card

Dedicated video memory. The model loads into it and runs fast.

| Video memory | Fits comfortably | Notes |
|---|---|---|
| 4 GB | up to 4B | 8B runs, partly on the processor |
| 6 GB | 7B to 8B | the usual sweet spot |
| 8 GB | 8B with room spare | 14B will split |
| 12 GB | 12B to 14B | |
| 16 GB | around 20B | |
| 24 GB+ | 27B to 32B | desktop card territory |

## Without one

No dedicated card. It runs on the processor and your system memory.
Everything works, it just answers more slowly.

| System memory | Fits | Notes |
|---|---|---|
| 8 GB | up to 3B | |
| 16 GB | 7B to 8B | a few words per second |
| 32 GB | 14B | with patience |

## Mac with Apple silicon

Memory is shared between processor and graphics, so use roughly two thirds
of the total. A 16 GB MacBook runs an 8B comfortably; a 32 GB one handles
14B to 20B.

---

## Where to find your numbers

**Windows:** Ctrl + Shift + Esc → Performance → GPU → Dedicated GPU memory.
Ignore "Shared GPU memory" — that is system RAM Windows lends the graphics
for display work, and it does not help here.

**Mac:** Apple menu → About This Mac → Memory.

**After the model loads:** `ollama ps` reports the actual split between GPU
and processor. That beats any table, including this one.

---

## Four things worth knowing

**These are 4-bit versions.** The full-precision ones are three to four times
larger. Model pages publish several quantisation levels and the naming
differs between them.

**Leave about a gigabyte spare.** A long conversation uses more memory than a
short one, and it grows as you go.

**Too big still runs.** What does not fit moves to the processor. Answers
come more slowly and nothing breaks.

**You lose speed, not ability.** A model answering slowly gives the same
answer as the same model answering quickly. Patience is a legitimate
substitute for hardware.
