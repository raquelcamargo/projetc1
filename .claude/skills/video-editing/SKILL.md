---
name: video-editing
description: Edit the user's videos end to end with an open-source toolchain (FFmpeg, Whisper, yt-dlp, HyperFrames, Three.js, motion graphics). Use whenever the user asks to edit, cut, caption, subtitle, resize, convert to Reels/Shorts/TikTok, download a video, transcribe, add animated text or 3D, or render a video from code.
---

# Video editing workflow

Goal: take a raw recording or a long video and deliver a finished vertical
clip (Reels, Shorts, TikTok) with the best takes, captions and motion
graphics, with as little manual work as possible.

User communication stays in Portuguese. Anything written to GitHub or to
files in this repository stays in English.

## Toolchain (source: "Claude x Video, 10 repos" carousel)

| # | Tool | Use it for | Status |
|---|------|-----------|--------|
| 01 | Ghost Editor | Raw talking-head recordings into Reels: best takes, captions, animations | Source URL not confirmed, ask the user |
| 02 | FFmpeg Skill | Cut, resize, crop to 9:16, adjust audio, burn subtitles, export | FFmpeg itself is the engine |
| 03 | Claude Shorts | Find the best moments of a long video and cut vertical clips with animated captions | Source URL not confirmed, ask the user |
| 04 | Not identified | Slide 5 of the carousel was not provided | Ask the user for slide 5 |
| 05 | Motion Skills | Animated charts, kinetic typography, explainer videos | Source URL not confirmed, ask the user |
| 06 | yt-dlp | Download video, audio, subtitles, thumbnails from YouTube and 1000+ sites | `pip install yt-dlp` |
| 07 | Whisper | Transcribe speech to text and SRT, edit by transcript | `pip install openai-whisper` |
| 08 | Awesome Claude Video Skills | Curated list of 180+ repos, use it to discover extra tools | Source URL not confirmed, ask the user |
| 09 | Three.js Skills | 3D scenes: animated objects, lighting, camera moves | Source URL not confirmed, ask the user |
| 10 | HyperFrames | Render video from HTML, CSS and GSAP animations | `npx skills add heygen-com/hyperframes` |

HyperFrames install: the full package also ships a `figma` skill that the
user does not want. Install selectively instead:
`npx skills add heygen-com/hyperframes -y -s hyperframes -s hyperframes-cli -s hyperframes-registry -s media-use -s remotion-to-hyperframes -s reverse-any-video -s slideshow -s style-sampling`
If `figma` appears anyway, run `npx skills remove -s figma -y`.

Rule: the carousel only shows names, not links. Never guess a repository URL
or install command. If a tool is marked "ask the user", request the link
before installing anything from it.

## Standard pipeline

1. **Check the environment first.** Run `command -v ffmpeg yt-dlp whisper node`.
   Report what is missing and install only after the user agrees.
2. **Get the source.** Local file: confirm path. URL: `yt-dlp -f "bv*+ba/b" -o "<dir>/%(title)s.%(ext)s" <url>`.
3. **Transcribe.** `whisper <file> --language pt --output_format srt` (use `--model small` or larger for accuracy). Keep the SRT and a plain-text copy.
4. **Pick the best moments.** Read the transcript, propose 3 to 5 candidate segments with timestamps and one line on why each works (hook, payoff, length 20 to 60 s). Wait for the user to choose unless told to decide.
5. **Cut and reframe with FFmpeg.**
   - Cut: `ffmpeg -ss <start> -to <end> -i in.mp4 -c copy cut.mp4` (re-encode if cuts are not frame accurate).
   - Vertical 9:16: `-vf "crop=ih*9/16:ih,scale=1080:1920"` (check the speaker stays in frame).
   - Captions: `-vf "subtitles=captions.srt:force_style='FontSize=18,Outline=2'"`.
   - Audio: `loudnorm` for consistent volume.
6. **Add motion graphics only if asked or clearly useful.** Titles, charts and explainer overlays via HyperFrames or Motion Skills, 3D via Three.js Skills. Render overlays with transparency or as separate clips, then composite with FFmpeg.
7. **Export** to H.264 MP4, 1080x1920, 30 fps, AAC audio, `-movflags +faststart`.
8. **Verify before reporting.** Run `ffprobe` on the output and confirm duration, resolution, audio stream and that captions are actually burned in. Extract a frame (`ffmpeg -ss 3 -i out.mp4 -frames:v 1 check.png`) and look at it. Say "medi" for what was measured and "acho" for opinions.

## Working rules

- Never overwrite the original file. Write outputs to a separate `output/` folder.
- Keep a short log of every FFmpeg command used so the edit can be reproduced.
- Ask before long renders or large downloads.
- Respect copyright: downloading with yt-dlp is for the user's own content or material they have rights to.
- Do not publish or send the finished video anywhere without an explicit "envia" or "pode enviar".

## Open items for the user

- Links for Ghost Editor, Claude Shorts, Motion Skills, Three.js Skills and Awesome Claude Video Skills.
- Slide 5 of the carousel (repo 04).
- Whether edits will run on the user's own machine (needs ffmpeg, yt-dlp, whisper installed locally) or in the cloud container (only ffmpeg is installed there today).
