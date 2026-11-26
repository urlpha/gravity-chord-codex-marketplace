---
name: music-producer
description: Create finished songs, write lyrics, and produce background music with GravityChord. Use when the user asks for a song, lyrics, music, BGM, background track, short-video or Douyin backing music, instrumental, game music, podcast intro, or any audio creation task. Covers Chinese triggers 写歌、写歌词、做音乐、生成音乐、配乐、BGM、纯音乐、编曲、短视频配乐、国风、R&B、电子.
---

# GravityChord Music Producer

GravityChord turns a text description into a finished, playable song: it writes or takes
lyrics, renders audio with the ACE-Step engine, masters to broadcast loudness, and returns
a listen link plus a share page.

Use the `gravity-chord` MCP tools. Do **not** synthesize audio with ffmpeg, sox, or Python
audio libraries — those produce placeholder tones, not music.

## Tools

| Tool | Use it for | Key parameters |
|---|---|---|
| `list_styles` | 71 built-in style presets with BPM/key/duration | none |
| `list_timbres` | Available vocal timbres | none |
| `suggest_params` | Turn a loose description into concrete parameters | `caption` |
| `write_lyrics` | Lyrics only, no audio | `caption`, `structure`, `duration` |
| `check_lyrics` | Validate lyric structure | `lyrics` |
| `generate_music` | **Render audio (main entry)** | `caption`, `lyrics`, `duration`, `instrumental`, `bpm`, `keyscale`, `vocal_language` |
| `get_task` | Poll progress / fetch result | `task_id` |
| `list_works` | List the user's previous works | none |
| `remaster_task` | Re-master an existing work | `task_id`, `lufs` |
| `get_usage` | Remaining quota | none |

## Rules that matter

1. **`caption` must be English.** Translate the user's request into an English sonic
   description before calling the tool. Passing Chinese verbatim measurably lowers output
   quality. Example: 「夏天的离别」→ `melancholic summer pop, warm acoustic guitar, soft male vocal`.
2. **`generate_music` is a long job.** A 90-second track takes roughly 3-6 minutes; a
   600-second track about 18 minutes. It returns a `task_id` with status `queued` or
   `running` — then poll `get_task` every 20-30 seconds. **Never submit the same request
   twice while one is running.**
3. **Pure instrumental requires `instrumental: true`.** Otherwise the engine attempts vocals.
4. **Duration is 0-600 seconds**, default 90. "Short" means 30-60.
5. If the user gave no lyrics, call `write_lyrics` first, then pass the result into
   `generate_music(lyrics=...)`. Do not let the engine improvise lyrics for a vocal track.
6. Deliver with: listen link (`preview_url` or `audio_url`), quality score, and the share
   page link.
7. On HTTP 401, tell the user to re-authorize: `codex mcp login gravity-chord`.

## Prompting the engine well

- Describe instrumentation, mood, tempo feel, and vocal type — not genre names alone.
- Avoid competitor brand names in `caption` (Suno, Udio). Use descriptions instead:
  `commercial pop production, polished mix, wide stereo`.
- `caption` describes the arrangement; `lyrics` is the sung text. Never mix them.
- For consistency across several tracks, reuse the same `bpm` and `keyscale`.
