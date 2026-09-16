# rv-preview — RenderingVideo Preview Skill

Draft or revise schema JSON and create a temporary preview without credentials. Requires Node.js 18+.

## Install

Clone this repository into your agent's skills directory using the short skill name:

```bash
git clone https://github.com/renderingvideo/renderingvideo-generator.git rv-preview
```

Then load `rv-preview/SKILL.md` using your agent's skill discovery workflow. The skill identifier is `rv-preview`. For an existing installation, pull the update and rename the old `renderingvideo-generator` directory to `rv-preview`. The GitHub repository URL remains unchanged.

## Usage

```bash
node scripts/gen-preview.cjs example.json
node scripts/gen-preview.cjs examples/enhanced-schema.json --json
```

The helper posts the full schema to `https://video.renderingvideo.com/api/preview`, without a `config` wrapper or API/agent keys. The enhanced example demonstrates grouped SVG assets, gradients, animations and keyframes without external media.

`--json` emits one response object with absolute URLs. Readable output prefers `viewerUrl`, then the actual returned preview/player URL. The helper reports `tempId` and `expiresIn`; previews normally expire after 7 days. It does not invent viewer paths or produce an MP4.

Use `RENDERINGVIDEO_VIDEO_ORIGIN` for a local/test video service. `RENDERINGVIDEO_TIMEOUT_MS` overrides the 90-second timeout. Invalid JSON, API failures, missing URLs and timeouts produce nonzero exit codes.

See [SKILL.md](SKILL.md), [schema reference](https://renderingvideo.com/docs/json-spec.md), and [API usage](https://renderingvideo.com/docs/api-and-usage.md). Permanent tasks, uploads and final renders use the authenticated API skill.

Run `node --test tests/*.test.cjs` for CLI response/timeout checks. Keep this repository aligned with the website's `.claude/skills/rv-preview` copy.
