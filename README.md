# PianoScript V2 🎹

**Author:** ghgltggamer  
**License:** MIT  

PianoScript V2 is a lightweight, browser-based music scripting language designed to generate piano melodies (or any sample-based instrument) using **absolute timeline scheduling**. It is optimized for AI-generated melodies, but also easy for humans to write and experiment with.

---

## Features

- Timeline-based music: each note has an absolute start time.
- Overlapping notes and natural polyphony without chord syntax.
- Supports rests, optional velocity, and flexible tempo/time units.
- Runs entirely in the browser — no Python packages, no backend required.
- Works with any sample: piano, strings, synths, or chords.
- Perfect for AI-powered melody generation.

---

## How to use ?
 - Clone this repository.
 - This repository comes with multiple files but you only need to care about `index.html` and `assets/piano.mp3`.
 - Open the `index.html` in a browser. (No need to start a web server)
 - Paste the *Piano Script V2* Code in the textbox
 - Click *Run*
 - The Music will play. Feel free to screen record it while playing

---

## Language Syntax

### 1. Headers (optional)

Headers define global settings for the piece. Place them at the top of the script.

| Header | Description | Default |
|--------|------------|---------|
| `@tempo <number>` | Tempo in beats per minute (BPM) | 120 |
| `@velocity <0-1>` | Default note velocity (volume) | 0.7 |
| `@time <seconds|beats>` | Unit for start time and duration | beats |

**Example:**
```

@tempo 90
@velocity 0.8
@time seconds

```

---

### 2. Notes

```

<NOTE> <START_TIME> <DURATION> [v<VELOCITY>]

```

- `<NOTE>`: Note name with optional accidental and octave (e.g., `C4`, `F#5`, `Bb3`)  
- `<START_TIME>`: Absolute start time in seconds or beats (depending on `@time`)  
- `<DURATION>`: Duration in seconds or beats  
- `[v<VELOCITY>]`: Optional velocity (0–1) for this note, overrides default  

**Example:**
```

C4 0.0 0.5
E4 0.25 0.25
G4 0.5 1.0 v0.9

```

Notes with the **same start time** automatically play together.

---

### 3. Rests

```

R <START_TIME> <DURATION>

```

- Represents silence in the timeline.  
- Optional but useful for readability.  

**Example:**
```

R 1.5 0.25

```

---

### 4. Multiple notes / polyphony

- Multiple notes starting at the same time naturally play together.  
- No `()` or chord grouping needed.  

**Example:**
```

C4 0.0 0.5
E4 0.0 0.5
G4 0.0 0.5

```

---

### 5. Comments

- Lines starting with `#` are ignored.  
- Use comments for readability.

**Example:**
```

# This is a simple melody

C4 0.0 0.5

```

---

## Example Script

```

@time seconds
@velocity 0.8

# Intro

C4 0.0 0.5
E4 0.0 0.5
G4 0.0 0.5

# Melody

D4 1.0 0.5
F4 1.0 0.5
A4 1.0 0.5

R 1.5 0.25

C5 2.0 1.0

```

---

## System Prompt for AI

If using an LLM to generate melodies, you can use this system prompt:

```

You are a music AI that ONLY outputs in PianoScript V2 format.
Follow these rules strictly:

1. Output ONLY valid PianoScript V2.
2. Do NOT write explanations, comments, or any text outside the language.
3. Use absolute start times, durations, and optional velocities.
4. Notes with the same start time can play together for chords.
5. Include headers @tempo, @velocity, @time only if necessary.
6. Ensure all numbers are finite and positive.

Example valid output:
@time seconds
@velocity 0.8
C4 0.0 0.5
E4 0.0 0.5
G4 0.0 0.5
D4 1.0 0.5
F4 1.0 0.5
A4 1.0 0.5

No need to play multiple notes together unless needed. Make sure to always output a unique melody.

User: make a 30 second long christmas song
```

---

## License

MIT License — free to use, modify, and distribute.

---

**Author:** ghgltggamer
```

---

This README covers everything:

* Language explanation for humans
* How polyphony works naturally
* Example scripts
* AI system prompt for generating valid PianoScript V2
