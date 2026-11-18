# SpotCam for AI assistants — User guide

SpotCam connects your AI assistant (Claude, ChatGPT, Gemini, GitHub Copilot
and others) to your SpotCam cameras. Ask in plain language which cameras you
have, what a camera shows, what happened while you were away, or for a video
of a moment.

- **Server URL:** `https://mcp.myspotcam.com/mcp`
- **Sign-in:** your SpotCam email and password, in your browser (OAuth). No API key.
- **Access:** the assistant cannot change camera settings, move cameras,
  delete recordings, or subscribe, change or pay for plans. It creates video
  exports in your My Film storage, and only when you ask.

## What you can ask

- "List my SpotCam cameras." / "Is the garage camera online?"
- "Show me what the front door camera sees right now."
- "Did anyone come to the front door this afternoon?"
- "Show me the living room at 3:15 pm yesterday."
- "Make a one-minute clip of the driveway from 8:00 this morning."
- "Make a time-lapse of the garden for today."
- "Wait two minutes and tell me if someone walks into the hallway."
- "Which plan is each of my cameras on?"

## Tools

| Tool | What it does |
|---|---|
| `list_cameras` | Your cameras and the cameras shared with you: serial number, name, owner/shared, status. |
| `get_camera_preview` | The latest image a camera uploaded (typically under a minute old; not a live stream). |
| `search_events` | Events a camera recorded over up to 7 days (people, motion, sound, pets, a baby, vehicles, …), with counts and times. |
| `get_timeline_sheet`, `get_frame`, `get_frames_at` | Look back through a camera's recordings: an overview sheet of a period, or the frames at given times. |
| `export_video_clip`, `export_timelapse` | Create a video clip or a time-lapse from the recordings, saved to your My Film storage. |
| `get_export_progress`, `list_exports`, `get_export_frames` | Follow an export, list your exports with links to play or download them, and look at frames of an exported video. |
| `wait_for_event` | Wait in the conversation for a camera to detect a person or motion (up to a few minutes in most apps). |
| `list_subscriptions` | The plan each camera you own is on and when it renews. |
| `submit_feedback` | Sends your bug report or suggestion to the SpotCam team. |

Recordings, events and exports are available for cameras you **own**;
shared cameras give their list entry and latest image only.

## Usage limits

Each camera has usage limits. Every camera is currently on the **Free** limits:

| Per camera | Free |
|---|---|
| Calls about the camera | 5 a minute, 100 a day |
| Images and video sent | 200 MB a month |
| Video clips | 2 a day, up to 3 minutes each |
| Time-lapses | 1 a month |
| Waiting for events | 1 wait at a time |

When a limit is reached, the assistant is told which limit, when it resets
(days are counted in Taipei time, UTC+8), and, for a camera you own, its
current plan and a link to that camera's page on the SpotCam website. Nothing
is charged and no plan changes unless you subscribe on the website yourself.
Each account counts separately, also for a camera shared with several people.

## Set up

### Claude (claude.ai, Claude Desktop, Claude mobile)

1. Open <https://claude.ai/customize/connectors> (web or Desktop; mobile cannot
   add connectors, but syncs them).
2. Select **Add custom connector**, enter name `SpotCam` and URL
   `https://mcp.myspotcam.com/mcp`.
3. Under advanced settings, keep **Use Claude's published identity**.
4. Select **Add**, then **Connect**, sign in to SpotCam and select **Allow**.

On Team and Enterprise plans an organization Owner adds the connector; each
member then selects **Connect**.

### Claude Code

```
/plugin marketplace add SpotCam-Cloud/spotcam-plugins
/plugin install spotcam@spotcam
```

Run `/reload-plugins`, open `/mcp`, choose the SpotCam server and select
**Authenticate**. Alternatively:
`claude mcp add --transport http --scope user spotcam https://mcp.myspotcam.com/mcp`.

### Other assistants

| Assistant | Command or link |
|---|---|
| VS Code + GitHub Copilot | `code --add-mcp '{"name":"spotcam","type":"http","url":"https://mcp.myspotcam.com/mcp"}'` |
| GitHub Copilot CLI | `copilot mcp add --transport http spotcam https://mcp.myspotcam.com/mcp` |
| OpenAI Codex CLI | `codex mcp add spotcam --url https://mcp.myspotcam.com/mcp` |
| Gemini CLI | `gemini extensions install https://github.com/SpotCam-Cloud/spotcam-plugins`, then `/mcp auth spotcam` |
| opencode | `opencode mcp add spotcam --url https://mcp.myspotcam.com/mcp` |

## Which cameras the assistant can see

- Cameras you own.
- Cameras another SpotCam user shared with you by invitation (your email is on
  the camera's share list). A shared camera returns a preview only while it is
  online.
- Not: public cameras you follow, or cameras whose owner blocked you.

## Manage or revoke access

- Open <https://mcp.myspotcam.com/oauth/account>, sign in, and select
  **Revoke** next to an app.
- Removing the connector in your assistant also stops it from being used.
- Access expires after 90 days; sign in again to continue. Deleting your
  SpotCam account or changing its email ends access immediately.

## Troubleshooting

| Problem | What to do |
|---|---|
| "Incorrect email or password" | Use the email and password you use for the SpotCam app. Accounts created only with Facebook sign-in need a password set first. |
| "Too many failed attempts" | Wait the time shown, then try again. |
| "Camera not found or you do not have access to it" | Ask the assistant to list your cameras and use one of those. |
| "No preview available: the camera is not online" | The camera is offline or asleep; previews of shared cameras need the camera online. |
| A recording or export tool says the time is outside the recordings | Ask for a time within the camera's recording days (see `list_subscriptions`). |
| "Limit reached" | The answer says which limit and when it resets; wait until then. |
| An export says My Film storage is full | Delete old videos in the SpotCam app, then try again. |
| The assistant says it needs sign-in | Reconnect: in Claude Code run `/mcp` and choose Authenticate; in claude.ai select Connect on the connector. |

## Support

Email info@myspotcam.com, or see <https://www.myspotcam.com/en/welcome/support/>.
Privacy: <https://mcp.myspotcam.com/privacy>.

## 繁體中文快速上手

1. 在 <https://claude.ai/customize/connectors> 新增自訂 connector，網址填 `https://mcp.myspotcam.com/mcp`。
2. 按 Connect，用 SpotCam 帳號登入並按允許。
3. 在對話中問「列出我的攝影機」「門口攝影機現在畫面如何」「今天下午有沒有人來過」「幫我把車道早上 8 點的一分鐘做成影片」或「等兩分鐘，走道有人就告訴我」。

AI 助理不能改攝影機設定、不能刪錄影，也不能訂閱、變更或付費購買方案；只有在你要求時才會建立匯出影片。每台攝影機目前都適用 Free 額度（每台每天 100 次呼叫、每月 200 MB、每天 2 段 3 分鐘內的影片、每月 1 支縮時、同時 1 個等待），用完時 AI 會說明何時重置。要撤銷授權，請到 <https://mcp.myspotcam.com/oauth/account>。
