# Hailuo AI / MiniMax (hailuo-ai)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Hailuo AI is MiniMax's generative video and audio platform. MiniMax is a foundation-model company whose developer platform (`platform.minimax.io` / `api.minimax.io`, and `intl.minimaxi.com` for international users, `api.minimaxi.chat` for mainland China) exposes documented HTTP APIs for **AI video generation** (the Hailuo text-to-video and image-to-video models), large language model chat completions, text-to-speech, music generation, and voice cloning.

The flagship surface for this entry is **video generation**. Hailuo video is produced by an asynchronous, three-step flow: create a task, poll its status, then retrieve the finished MP4 by a temporary download URL. All APIs authenticate with a **Bearer API key**.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/hailuo-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/hailuo-ai/refs/heads/main/apis.yml)

## Access Model

- Public, self-service developer platform — sign up at [platform.minimax.io](https://platform.minimax.io/login).
- Both **pay-as-you-go API keys** and **subscription keys** are issued from the console.
- Video generation is metered in **video points per clip** (varies by model, resolution, and duration); chat and text-to-speech are metered per token / per character. Failed or security-blocked generations are not charged.
- The consumer web app at `hailuoai.video` is a separate, subscription-based product; the entry here documents the **developer API**.
- Endpoints, HTTP methods, model names, and the async workflow are grounded in MiniMax's live documentation. Detailed request/response JSON schemas are honestly **modeled** to reflect documented fields, and the `music_generation` endpoint payload is flagged as modeled — reconcile against the official reference before production use.

## Tags

- Video Generation
- AI Video
- Generative AI
- Text-to-Video
- Image-to-Video
- Text to Speech
- LLM
- Foundation Models

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Hailuo Video Generation API

Asynchronous AI video generation powered by the Hailuo models (MiniMax-Hailuo-2.3, MiniMax-Hailuo-02, Video-01, T2V-01, I2V-01, S2V-01). Supports text-to-video, image-to-video, first-and-last-frame video, and subject-reference video (face-consistent characters), with configurable duration and resolution up to 1080P.

Three-step flow:

1. `POST /v1/video_generation` → returns a `task_id`
2. `GET /v1/query/video_generation?task_id=...` → poll until status is `Success`, returns a `file_id`
3. `GET /v1/files/retrieve?file_id=...` → returns a temporary `download_url` (video URLs valid ~9 hours)

- **Human URL:** [https://platform.minimax.io/docs/guides/video-generation](https://platform.minimax.io/docs/guides/video-generation)
- **Base URL:** `https://api.minimax.io/v1`

#### Tags

- Video Generation
- AI Video
- Text-to-Video
- Image-to-Video
- Generative AI

#### Properties

- [Documentation](https://platform.minimax.io/docs/guides/video-generation)
- [API Reference](https://www.minimax.io/news/video-generation-api)
- [OpenAPI](openapi/hailuo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hailuo-ai.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/hailuo-ai.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MiniMax Text-to-Speech (T2A) API

Speech synthesis (T2A v2) across the speech-2.8, speech-2.6, speech-02, and speech-01 HD/turbo models, with 100+ voices, emotion and language control, and per-request voice/audio settings. Available both as a synchronous HTTP endpoint (`POST /v1/t2a_v2`) and as a documented **real-time WebSocket API** (`wss://api.minimax.io/ws/v1/t2a_v2`) that streams audio chunks as they are generated.

- **Human URL:** [https://platform.minimax.io/docs/api-reference/speech-t2a-http](https://platform.minimax.io/docs/api-reference/speech-t2a-http)
- **Base URL:** `https://api.minimax.io/v1`

#### Tags

- Text to Speech
- Audio
- Voice
- WebSocket

#### Properties

- [Documentation](https://platform.minimax.io/docs/api-reference/speech-t2a-http)
- [OpenAPI](openapi/hailuo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [AsyncAPI](asyncapi/hailuo-ai-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/v2.6.0)
- [Postman Collection](collections/hailuo-ai.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### MiniMax Chat Completions API

OpenAI-compatible chat completions (`POST /v1/chat/completions`) served by MiniMax's large language models (the MiniMax-M / abab family), with streaming, tool/function calling, and long-context support.

- **Human URL:** [https://platform.minimax.io/docs/api-reference/text-generation](https://platform.minimax.io/docs/api-reference/text-generation)
- **Base URL:** `https://api.minimax.io/v1`

#### Tags

- LLM
- Chat
- Completions
- Foundation Models

#### Properties

- [Documentation](https://platform.minimax.io/docs/api-reference/text-generation)
- [OpenAPI](openapi/hailuo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/hailuo-ai.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### MiniMax Music Generation API

Generates a vocal song from a music-style description (prompt) plus lyrics via `POST /v1/music_generation`. Endpoint path and payload are **modeled** from MiniMax's published music API; confirm exact fields against the live reference during reconciliation.

- **Human URL:** [https://platform.minimax.io/docs/api-reference/music-generation](https://platform.minimax.io/docs/api-reference/music-generation)
- **Base URL:** `https://api.minimax.io/v1`

#### Tags

- Music Generation
- Audio
- Generative AI

#### Properties

- [Documentation](https://platform.minimax.io/docs/api-reference/music-generation)
- [OpenAPI](openapi/hailuo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### MiniMax Files API

Retrieves generated assets by `file_id` (`GET /v1/files/retrieve`), returning a temporary download URL — video URLs are valid for roughly 9 hours (32,400 seconds). Used to fetch the finished MP4 after a video task completes.

- **Human URL:** [https://platform.minimax.io/docs/api-reference](https://platform.minimax.io/docs/api-reference)
- **Base URL:** `https://api.minimax.io/v1`

#### Tags

- Files
- Storage
- Downloads

#### Properties

- [Documentation](https://platform.minimax.io/docs/guides/video-generation)
- [OpenAPI](openapi/hailuo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [Authentication](authentication/hailuo-ai-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/minimax-ai)
- [Website](https://www.minimax.io/)
- [Documentation](https://platform.minimax.io/docs)
- [Plans](plans/hailuo-ai-plans-pricing.yml)
- [Rate Limits](rate-limits/hailuo-ai-rate-limits.yml)
- [Fin Ops](finops/hailuo-ai-finops.yml)
- [Sign Up](https://platform.minimax.io/login)
- [Blog](https://www.minimax.io/news)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
