# SpotCam MCP Server — Privacy Policy

> **DRAFT — to be approved by SpotCam's legal team before it is published or
> submitted to any app directory.** Items marked TODO need a legal decision.
> The technical statements describe the service as implemented on
> 2026-11-12.

- **Effective date:** TODO (date of publication)
- **Operator:** SpotCam Co., Ltd., 17F-8, No. 716, Zhongzheng Rd., Zhonghe Dist.,
  New Taipei City 235603, Taiwan (R.O.C.)
- **Contact:** info@myspotcam.com

This policy covers the SpotCam MCP server at `https://mcp.myspotcam.com/mcp`
(the "Service"), which lets AI assistants you choose access your SpotCam
cameras on your behalf. Your SpotCam account, cameras and recordings
themselves remain covered by the SpotCam Privacy Policy:
<https://www.myspotcam.com/en/welcome/privacy/>.

## 1. What the Service accesses and why

| Data | Source | Purpose | Stored by the Service? |
|---|---|---|---|
| Email address and password you type on the sign-in page | You | Verified with the SpotCam account service to confirm your identity | **Password: never stored or logged.** Email: stored with your authorization (see §3) |
| SpotCam account ID | SpotCam account service | Identify your account and your cameras | Stored with your authorization |
| Camera list: serial numbers, names, owner/shared relation, connection status | SpotCam database (read-only) | Answer the camera tools and check which cameras you may access | Not stored; read on each request (names are kept only as a one-way fingerprint for usage statistics) |
| Latest preview images, recorded frames and event lists of your cameras | The camera's SpotCam video server | Answer the preview, recording and event tools | **Not stored**; fetched on each request and passed to your AI assistant |
| Video exports (clips and time-lapses) you ask for | The camera's SpotCam video server | Create the video in your SpotCam My Film storage and let you play or download it | The video stays in your My Film storage. The Service keeps a record of the request (camera, time range, status) and streams the video through itself when you open a playback link; it does not keep a copy |
| Your camera plans and the plan catalog | SpotCam database (read-only) | Answer the plan tools | Not stored |
| Plan subscription requests you confirm | You, through your AI assistant | Pass your request to the SpotCam team | Stored (see §3). No payment is taken and no payment data is read |
| Feedback you send through your AI assistant | You | Fix problems and improve the Service | Stored (see §3) |
| Event triggers you set up, including the Claude Routine address and token you paste on the account page | You | Notify your Claude Routine when a camera detects the events you chose | Stored until you delete the trigger, it expires (at most 72 hours) or your authorization ends |
| Access and refresh tokens issued to your AI assistant | The Service | Keep your assistant signed in | Stored only as one-way hashes |
| Security log: account ID, assistant (client) identifier, tool used, camera serial number, IP address, time, success or failure | Your requests | Security, abuse prevention, troubleshooting | Stored (see §3) |
| Usage records: account ID, assistant identifier, tool used, camera serial number, outcome, timings and data sizes | Your requests | Capacity planning, traffic limits by plan, and deciding which features to build | Stored (see §3). No conversation content, email address, IP address or image is part of them |

The Service only accesses cameras you own or that another user shared with
you by invitation; recordings, exports, events and plans are available for
cameras you own only. It cannot change camera settings. The Service never
receives your conversation with your AI assistant, only the tool calls the
assistant makes.

## 2. Sharing with your AI assistant provider

When you ask your AI assistant about your cameras, the Service sends the
requested data (for example a camera list, an image or a link to a video) to
that assistant (for example Anthropic's Claude, OpenAI's ChatGPT or Codex,
Google's Gemini, or GitHub Copilot). The provider processes it under its own
terms and privacy policy, which you accepted when you chose to use it.
SpotCam does not control how the provider stores or uses that data.

When an event trigger fires, the Service sends the camera name, event type
and time to the Claude Routine you connected, at the address you provided.

SpotCam does not sell your data, does not use it for advertising, and does
not use your camera images or videos to train AI models.
TODO (legal: list processors — Google Cloud, Amazon Web Services).

## 3. Retention

| Data | Kept for |
|---|---|
| Authorization (account ID, email, assistant identifier, token hashes) | Until you revoke it or it expires (at most 90 days), then 7 days before deletion |
| Unfinished sign-in requests | 10 minutes |
| Security log and per-call usage records | 90 days |
| Daily usage totals (account ID, tool, number of calls, data size) | Kept without expiry for long-term statistics. TODO (legal: confirm or set a limit) |
| Video export records | 90 days |
| Feedback, plan subscription requests, and the plan features requested | 365 days |
| Event triggers | Until deleted or expired (at most 72 hours), or until your authorization ends |
| Server operational logs | Rotated automatically (at most about 50 MB) |
| Passwords, camera images, recorded frames | Not retained |

## 4. Your choices

- **Revoke access** at any time at
  <https://mcp.myspotcam.com/oauth/account>, or by removing the connector
  in your AI assistant. Revoking also ends your event triggers.
- Deleting your SpotCam account or changing its email address ends the
  Service's access immediately.
- To see, correct or delete personal data the Service keeps about you, write
  to info@myspotcam.com. TODO (legal: rights under the Taiwan Personal Data
  Protection Act and the GDPR, and response time).

## 5. Security

All connections use TLS. Tokens are random, stored only as hashes, bound to
this Service, and expire. Each request is checked against the camera
ownership and sharing rules of your SpotCam account. Playback links are
signed, bound to your authorization and expire. Sign-in attempts and tool
calls are rate-limited.

## 6. Where data is processed

The Service runs on Google Cloud in Taiwan (asia-east1); SpotCam account and
camera data is stored on Amazon Web Services in Singapore (ap-southeast-1),
and recordings on SpotCam's video servers in the region of each camera.
TODO (legal: confirm wording and cross-border transfer basis).

## 7. Children

The Service is for SpotCam account holders, who must be of legal age under
the SpotCam Terms of Service (<https://www.myspotcam.com/en/welcome/terms/>).

## 8. Changes

We will post changes to this policy here and update the effective date.
TODO (legal: notice period for material changes).

## 9. Contact

SpotCam Co., Ltd., 17F-8, No. 716, Zhongzheng Rd., Zhonghe Dist., New Taipei
City 235603, Taiwan (R.O.C.) — info@myspotcam.com
