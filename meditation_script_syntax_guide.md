# Meditation script syntax guide

This guide is the short reference for creating Go Lightly meditations with script mode. Use these tokens inside the `Meditation Script` section of a meditation markdown file. Plain text becomes spoken audio, and the tokens add silence, speed changes, or prerecorded sounds.

## Core syntax

### 1. Spoken text

- Any plain text is read aloud by text-to-speech.
- Use normal punctuation for natural phrasing.
- Do not include stage directions, notes, or bracketed asides unless they should be spoken.

Example:

```text
Let your attention settle on the feeling of breathing.
```

### 2. Pause

- Use `<break time="Ns" />` to insert silence.
- Replace `N` with a number of seconds.
- Decimals are allowed.
- The value must be greater than `0` and no more than `300`.
- Keep the `s` suffix, quotes, and self-closing `/>`.

Examples:

```text
<break time="2s" />
<break time="3.5s" />
<break time="90s" />
```

Avoid:

```text
<break time="3" />
<break time="3s">
<break time=3s />
```

### 3. Speed override

- Use `{speed=N}spoken text{/speed}` to change text-to-speech speed for a specific phrase or sentence.
- Replace `N` with a number from `0.7` to `1.3`.
- Use `1.0` for normal speed.
- Use slower values, such as `0.85` or `0.9`, for lines that should feel more spacious.
- Close every speed block with `{/speed}`.
- Do not nest speed blocks.

Examples:

```text
{speed=0.9}Take one slow breath in.{/speed}
{speed=1.0}Let the breath move at its own pace.{/speed}
```

Avoid:

```text
{speed=.9}Take one slow breath in.{/speed}
{speed=0.9}Take one slow breath in.
{/speed}Take one slow breath in.
{speed=0.9}{speed=0.8}Take one slow breath in.{/speed}{/speed}
```

### 4. Sound

- Use `[Sound Name]` to play a prerecorded sound.
- Use only the sound names listed in this guide.
- Put sounds on their own line.
- Follow a sound with a pause when the resonance or breath cue needs room.
- Use the canonical capitalization from the sound list.

Example:

```text
[Tibetan Singing Bowl]
<break time="4s" />
```

## Available sounds

### 1. Tibetan Singing Bowl

- Duration: 6 seconds
- Use for openings, closings, and simple section transitions.

### 2. Double Tibetan Singing Bowl

- Duration: 7 seconds
- Use for stronger endings, major transitions, or a more final closing signal.

### 3. Inhale

- Duration: 4 seconds
- Use as a breath cue when the listener should breathe in with the sound.

### 4. Exhale

- Duration: 6 seconds
- Use as a breath cue when the listener should breathe out with the sound.

## Timing guidance

### 1. Estimate total duration

- Spoken text time
- All `<break>` durations
- Sound durations from the available sounds list

### 2. Use rough spoken-text estimates

- 150 words per minute at normal speed
- Slightly longer for `{speed=0.9}`
- Slightly shorter for speeds above `1.0`

### 3. Prefer adjusting pause lengths

Adjust pause lengths instead of making the spoken text dense.

## Common patterns

### 1. Opening

```text
[Tibetan Singing Bowl]
<break time="4s" />

Take a moment to arrive.
<break time="3s" />
```

### 2. Guided breath

```text
[Inhale]
<break time="1s" />
[Exhale]
<break time="2s" />
```

### 3. Slower instruction

```text
{speed=0.9}Let the next breath be easy and unforced.{/speed}
<break time="5s" />
```

### 4. Closing

```text
[Double Tibetan Singing Bowl]
<break time="3s" />
```

## Final checks

### 1. Every `<break>` has

- `time=`
- quoted seconds
- an `s` suffix
- a self-closing `/>`

### 2. Every `{speed=N}` has

- a value between `0.7` and `1.3`
- an integer part before the decimal
- a matching `{/speed}`

### 3. Every `[Sound Name]`

- matches one of the available sounds
- appears on its own line
- is included in the duration estimate
