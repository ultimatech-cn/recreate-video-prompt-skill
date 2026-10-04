---
name: recreate-video-prompt
description: Analyze a reference video, one or more identity images, and optional user requirements to create a stable prompt for AI video recreation or character replacement. Use for 视频复刻, 参考视频仿拍, character replacement, motion or camera imitation, creative remakes, and realistic smartphone footage. Produce video-generation instructions only; exclude editing, captions, audio production, compositing, and publishing unless explicitly requested.
---

# Recreate Video Prompt

## Goal

Turn a reference video, identity images, and optional requirements into one concise generation prompt that preserves the video's essential action and appeal while controlling identity, intentional changes, realism, and likely failure modes.

Treat each input as a separate control source:

- **Reference video:** timing, action sequence, interaction, object path, body mechanics, camera behavior, framing, and emotional rhythm.
- **Identity images:** face, hair, skin tone, body proportions, and stable appearance.
- **User requirements:** highest-priority creative changes, constraints, emphasis, and output preferences.
- **Generated prompt:** a director's instruction joining those sources. Do not make it carry motion data the target generator can receive directly.

If optional requirements are absent, continue with sensible defaults. Ask a question only when a missing required input prevents meaningful analysis.

## Workflow

### 1. Inspect actual inputs

Do not rely only on filenames, captions, or user summaries when media is accessible. Never claim to have inspected unavailable media.

For the reference video, identify:

1. Duration, aspect ratio, shot count, and whether it is continuous or edited.
2. The core hook: the single action, reveal, interaction, or visual surprise that makes the video recognizable.
3. A chronological beat sheet covering preparation, main action, reaction, and ending.
4. Contact mechanics and physics: what touches, grips, releases, bends, falls, splashes, transfers, or follows a trajectory.
5. Camera distance, angle, movement, pans, reframing, focus behavior, and handheld imperfections.
6. Setting, clothing, props, lighting, mood, and realism signature.
7. Existing text, logos, audio, or edits. Exclude them by default when the request is generation only.

For identity images, record only visible identity traits. Do not borrow the reference video's face, hair, body, or wardrobe when the supplied image replaces the person.

### 2. Separate preservation from change

Create two internal lists:

- **Must preserve:** core hook, action order, crucial gesture, contact, trajectory, reaction timing, framing relationship, and energy.
- **Change deliberately:** identity plus user-requested elements. For a creative remake, normally change at least two non-core elements such as location, wardrobe, decor, secondary props, or color palette.

Do not change the mechanism that creates the video's appeal. Treat any motion detail emphasized by the user as mandatory and preserve its exact order.

### 3. Resolve conflicts

Apply this authority order:

1. Explicit user requirements and emphasized details.
2. Identity and appearance from identity images.
3. Temporal action and camera behavior from the reference video.
4. Sensible defaults inferred by the agent.

Never let scene decoration override the core action. Never combine conflicting clothes, locations, camera styles, or body descriptions.

### 4. Write the generation prompt

Write in clear English unless another language is requested. Use chronological, physically explicit action sentences in this order:

1. Output format and realism target.
2. Identity source and stable appearance.
3. New setting, wardrobe, and deliberate changes.
4. Reference video's role.
5. Essential action sequence.
6. Expression, reaction, and ending.
7. Camera behavior and capture imperfections.
8. A short negative constraint list containing only likely failure modes.

Prefer precise verbs such as grips, squeezes, shakes, pauses, lifts, releases, turns, catches, and reacts. For crucial physical actions, describe the contact state before motion, the motion itself, and the resulting release or trajectory.

Keep the positive prompt normally between 180 and 350 words. Add detail only to disambiguate complex contact or choreography. Avoid poetic language, duplicated adjectives, long inventories, and exhaustive negative lists.

### 5. Preserve realism

For phone-shot realism, specify candid smartphone capture, ordinary exposure, slight handheld drift, mild sensor noise, natural motion blur, imperfect framing, practical lighting, realistic skin texture, believable body weight, fabric response, gravity, and object contact. Avoid cinematic polish unless requested.

If sexualized behavior is requested, identify depicted people as adults. Preserve the intended suggestive tone without inventing more explicit actions than requested.

## Output Modes

### Default

Return one complete, copyable video-generation prompt. Do not expose chain-of-thought or add editing instructions.

### Structured

Return valid JSON matching `schemas/output.schema.json`, with no Markdown fences or surrounding explanation.

Set `reference_video_required` to true when text alone is unlikely to reproduce exact motion, contact, timing, trajectory, or camera path.

## Integration

Use [prompts/agent-system-prompt.md](prompts/agent-system-prompt.md) when the host cannot load `SKILL.md` natively. Use the JSON schemas for tool-calling or API pipelines. Preserve the folder structure when installing the skill.
