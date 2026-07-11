---
name: youtube-transcript-description
description: Extract a YouTube video description and timestamped transcript via Apify. Auto-selects cheapest working actor (johnvc/YoutubeTranscripts first, fallback to starvibe/youtube-video-transcript). Trigger when user shares a YouTube URL and wants description, transcript, captions, or subtitles with timestamps.
metadata:
  version: "1.3.0"
  category: data-extraction
  status: published
  confidence: 0.95
  source: learned
  owner: prithvi shergill
  created: "2026-07-11T20:43:00Z"
  updated: "2026-07-11T21:37:00Z"
---

# Youtube Transcript Description

Extract a YouTube video's description AND timestamped transcript via Apify actors. Prefer the cheapest reliable actor and fall back automatically.

## When to Use
- User pastes a YouTube link (youtu.be or youtube.com/watch) and asks for the video description, transcript/captions/subtitles with timestamps, or both.
- Do NOT use for thumbnails, video downloads, comments, or non-YouTube URLs.

## How It Works

### 0. Clean the URL (Always)
- Strip all tracking parameters (`?si=...`, `&t=...`, etc.).
- Normalize to `https://www.youtube.com/watch?v=VIDEO_ID`.
- Reason: Tracking params frequently cause actor failures or empty results.

### 1. Verify Schema (Mandatory)
- Always call `mcp__85e0a92d__fetch-actor-details` first for the chosen actor to confirm the current input schema and pricing.

### 2. Primary Actor — johnvc/YoutubeTranscripts (~$0.00001)
- Tool: `mcp__85e0a92d__call-actor`
- Input (must be a real nested object, never a string). Recommended minimal + reliable fields:
  ```json
  {
    "youtube_url": "https://www.youtube.com/watch?v=VIDEO_ID",
    "include_metadata": true,
    "languages": ["en"],
    "transcript_type": "any",
    "preserve_formatting": false,
    "list_only": false
  }
  ```
- Optionally include `waitSecs: 60`.
- Success criteria: Actor reaches SUCCEEDED status AND returns both a non-empty `description` and non-empty `timestamps[]`.
- If successful → go to Step 4.
- Any failure, empty description, or missing transcript → go to Step 3.

### 3. Fallback Actor — starvibe/youtube-video-transcript ($0.005)
- Tool: `mcp__85e0a92d__call-actor`
- Input (real object). Recommended:
  ```json
  {
    "youtube_url": "https://www.youtube.com/watch?v=VIDEO_ID",
    "max_videos": 1,
    "include_transcript_text": true
  }
  ```
- Use ONLY when the primary actor fails.

### 4. Retrieve & Format Output
- After the actor run reaches SUCCEEDED, wait 30–45 seconds for the dataset to fully propagate.
- Call `mcp__85e0a92d__get-dataset-items` with `clean: true`.
- Map fields:
  - Name ← title
  - Channel ← channelName
  - Link ← cleaned URL
  - Description ← description
  - Transcript:
    - johnvc: Aggregate `timestamps[]` items of shape `{t: seconds, w: word}` into readable sentence segments and render as `[MM:SS] text`
    - starvibe: Use `transcript[]` items of shape `{start, end, duration, text}` directly as `[MM:SS] text`

## Tools / Capabilities
- `mcp__85e0a92d__fetch-actor-details` — mandatory first step for schema check
- `mcp__85e0a92d__call-actor` — run the actors (critical: pass `input` as a real object, never stringify it)
- `mcp__85e0a92d__get-dataset-items` — retrieve results after the buffer wait
- `mcp__85e0a92d__get-actor-run` — optional for status polling

## Memory Usage
None. The actor priority order and URL-cleaning rules are hardcoded in the steps.

## Output Format
```
Youtube Video:
Name: [Title]
Channel: [Channel Name]
Link: [Clean URL]

Description:
[Full description text]

Transcript with timestamps:
[00:00] First sentence or segment...
[00:12] Next sentence...
```

## Examples
Input: `https://youtu.be/I9W6NhFkGAI?si=XdAhdniLxpgAsDS1`
→ Clean to `https://www.youtube.com/watch?v=I9W6NhFkGAI`
→ fetch-actor-details
→ call johnvc/YoutubeTranscripts with the recommended input object (include_metadata + languages etc.)
→ wait 30–45s after SUCCEEDED
→ get-dataset-items(clean: true)
→ render in the exact Output Format above.

## Testing the Skill
When testing this skill (especially in Agent mode), use this exact sample input:

**Test Input URL:**
`https://youtu.be/I9W6NhFkGAI?si=XdAhdniLxpgAsDS1`

**Expected Flow:**
1. Clean URL → `https://www.youtube.com/watch?v=I9W6NhFkGAI`
2. Call primary actor (johnvc) with the recommended full input object
3. On success → wait 30–45s → get-dataset-items
4. Render in the exact Output Format

**Alternative test URL** (from previous successful runs):
`https://www.youtube.com/watch?v=SlqjA04_dpk`

Always invent or use one of these real YouTube links when asked to test end-to-end. Do not ask the user for a URL during testing.

## Known Issues & Workarounds
- call-actor "/input: must be object" validation error: This is usually caused by accidentally stringifying the input. Always pass a real nested object. Re-fetch the schema with fetch-actor-details immediately before the call. Retry once if needed.
- Flag (do not silently swap) if either actor's price or schema changes, or if starvibe is down.
