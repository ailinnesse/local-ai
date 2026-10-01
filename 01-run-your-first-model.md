# Run your first model

Companion to the video: [TITLE](VIDEO-LINK-HERE)

Install Ollama, pull a model that fits your machine, and see where it is
actually running. About twenty minutes, most of it downloading.

---

## 1. Check your hardware first

Before downloading anything, find out how much memory a model can live in.
That single number decides everything.

**Windows:** Ctrl + Shift + Esc → Performance → GPU → **Dedicated GPU
memory**. No separate GPU listed? Use the Memory figure instead.

**Mac:** Apple menu → About This Mac → **Memory**. One figure covers both.

[What fits on your machine](what-fits-on-your-machine.md) turns that number
into a model size.

## 2. Install Ollama

Download from [ollama.com](https://ollama.com) and run the installer. It
starts a service in the background and gives you a command line. Nothing to
configure.

**If your C: drive is tight,** set the `OLLAMA_MODELS` environment variable
to another drive before pulling anything. Models are several gigabytes each
and they all land there by default.

## 3. Pull a model — and mind the tag

```
ollama run <model>
```

Downloads it and starts a chat.

**Use the size tag.** A bare name gives you the model's default, which is
often far bigger than you want:

```
ollama run <model>:3b
ollama run <model>:8b
```

I ran a bare name on a 4 GB card and got a 9.5 GB model. It still worked —
it just spent most of its time on the processor. Check the model's page on
[ollama.com/library](https://ollama.com/library) for the tags it publishes,
because they vary between models.

## 4. Ask it something

You are at a `>>>` prompt. Type and press Enter.

For anything spanning several lines, type `"""` on its own line, paste, then
`"""` again. Otherwise Enter sends after the first line.

Useful while you are in there:

| | |
|---|---|
| `Ctrl + C` | stop an answer mid-flow |
| `/bye` | leave the chat |
| `/?` | list the commands |

## 5. See where it is actually running

This is the part most walkthroughs skip, and it explains everything else.

Open a **second** terminal — you cannot run this from inside the chat — and:

```
ollama ps
```

| Column | What it tells you |
|---|---|
| SIZE | how much memory the model is using right now |
| PROCESSOR | the split between GPU and CPU |
| UNTIL | when it will unload itself, about five minutes idle |

A model that fits your video memory shows **100% GPU** and answers quickly.
One that does not shows a split, and the larger the CPU share the slower it
goes. Nothing breaks either way.

An empty list means nothing is loaded. Downloading does not load a model;
running it does.

## 6. Prove it is local

Turn the wifi off and ask it something.

That is the whole argument in one gesture, and it is worth doing before you
believe any of the rest.

---

## Commands worth keeping

| | |
|---|---|
| `ollama run <model>` | download if needed, then chat |
| `ollama pull <model>` | download only |
| `ollama list` | what is on disk, and how big |
| `ollama ps` | what is loaded in memory now |
| `ollama stop <model>` | unload it |
| `ollama rm <model>` | delete it and get the space back |

---

## What a small model is good at

Worth knowing before you judge one. A 3B to 8B model on a laptop is
reliable at:

- summarising text you give it
- pulling structured fields out of messy text
- rewriting, shortening, changing tone
- tidying inconsistent lists and names

It is unreliable at:

- anything that happened after it was trained, which it will not tell you
- arithmetic
- long chains of reasoning
- specialist syntax, where it is confidently almost right

The last one is the trap. A wrong answer in a language you do not read
fluently looks exactly like a right one.
