---
name: spotcam
description: Use when the user asks about their SpotCam cameras — which cameras they have, whether a camera is online, what a camera shows now, what happened earlier, or for a clip or time-lapse (e.g. "check my front door camera", "did anyone come by this afternoon?", "make a clip of the driveway at 8 am").
---

# SpotCam cameras

The `spotcam` MCP server gives access to the signed-in user's SpotCam cameras.

- `list_cameras` returns every camera the user owns or that was shared with them: serial number (`sn`), name, relation (owner/shared) and status (online, off, offline, sleeping).
- `get_camera_preview` takes an `sn` and returns the latest preview image the camera uploaded, with its capture time.
- For cameras the user owns: `search_events` (what happened over a period), `get_timeline_sheet` / `get_frame` / `get_frames_at` (look back through recordings), `export_video_clip` / `export_timelapse` (make a video; follow it with `get_export_progress` or `list_exports`).
- Plans: `list_subscriptions` (each camera's current plan). For choosing AI detection plans, use the `spotcam-ai-plans` skill.

How to use them:

1. Call `list_cameras` first and match the camera the user means by name. If several could match, ask which one.
2. Call `get_camera_preview` with that camera's `sn`, then describe what the image shows and mention how old it is (the preview is uploaded periodically, not a live stream).
3. If a camera is offline, off or sleeping, say so instead of guessing. Cameras shared with the user only return a preview while they are online.
4. If the tools are missing or report that sign-in is needed, tell the user to run `/mcp`, choose `spotcam` and select Authenticate.

Only report what the image actually shows. Do not identify people by name from an image.
