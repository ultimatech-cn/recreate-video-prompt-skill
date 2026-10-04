# Recreate Video Prompt Skill

A vendor-neutral multimodal agent skill for turning a reference video, identity images, and optional requirements into a stable AI video-generation prompt.

It is not tied to GPT, OpenAI, ComfyUI, or a specific video generator. Any agent can use it if the host can load instructions and the agent can inspect video and images, or receives a trustworthy upstream video analysis.

## What it does

- Separates identity control from motion and camera control.
- Finds the video's core hook and chronological action beats.
- Preserves contact mechanics, physics, object paths, reactions, and camera relationships.
- Supports character replacement and creative remakes.
- Produces either one copyable generation prompt or strict structured JSON.
- Excludes captions, editing, sound, compositing, and publishing unless requested.

## Repository structure

```text
recreate-video-prompt-skill/
├── SKILL.md
├── skill.json
├── prompts/
│   └── agent-system-prompt.md
├── schemas/
│   ├── input.schema.json
│   └── output.schema.json
└── examples/
    ├── request.json
    └── response.json
```
## Video Examples

### Example

 — Character Replacement

https://github.com/user-attachments/assets/39a3685b-7951-4c8d-b75a-260f127f8a96

**What the skill preserves**

- Core action and chronological motion
- Camera angle and framing
- Physical interaction and timing
- Realistic smartphone-recorded appearance

**What the skill changes**

- Character identity
- Clothing, props, or environment when requested
- Non-essential creative elements
## Integration options

### Native skill support

Copy the complete directory into the skill location configured by your agent framework. Use `SKILL.md` as the entrypoint and preserve all relative paths.

### System-prompt support

Load `prompts/agent-system-prompt.md` as the agent's system or developer instruction. Supply the video, identity images, and optional requirements as separately labeled inputs.

### Tool or API support

Use `schemas/input.schema.json` for requests and validate structured responses with `schemas/output.schema.json`. `skill.json` provides a simple vendor-neutral manifest; frameworks may ignore it and load `SKILL.md` directly.

## Example request

```text
Use the recreate-video-prompt skill.

Reference video: attached.
Image 1 — identity reference: attached.
Additional requirements: Preserve the core movement and camera timing, but change the location and wardrobe. Ultra-realistic smartphone footage. No text and no editing instructions.
Output mode: JSON.
```

## Input priority

1. Explicit user requirements.
2. Identity and appearance from identity images.
3. Action timing and camera behavior from the reference video.
4. Sensible agent defaults.

## Important limitation

This skill creates semantic direction; it does not transfer motion. For close replication, pass the original reference video or extracted pose, motion, depth, or camera controls directly to the target video generator when supported.

A text-only agent must not pretend it inspected media it cannot access. Give it an upstream analysis with chronological frames, timing, action beats, camera behavior, and contact mechanics.

## Publishing

Upload the entire folder to GitHub without flattening the directory structure. This package intentionally does not include a software license. Add the license you prefer before inviting third parties to reuse or redistribute it.
