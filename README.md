<p align="center">
  <a href="https://www.huntapi.com"><img src="images/banner.png" alt="Media Metadata API by HuntAPI" width="100%"></a>
</p>

# Media Metadata API

[![Discord](https://img.shields.io/badge/Discord-Join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/CFj3ph8aHU) [![Get API key](https://img.shields.io/badge/HuntAPI-Get%20an%20API%20key-111827)](https://app.huntapi.com/register) [![API docs](https://img.shields.io/badge/Docs-API%20reference-0EA5E9)](https://docs.huntapi.com) [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

The **HuntAPI Media Metadata API** returns the metadata of a media URL — title, duration, thumbnail, channel, view and like counts — without downloading the file.

- **Media Metadata API** — Extract metadata from a media URL without downloading the file.

Use it to preview links, enrich content databases, check durations before downloading, or track public video stats.

| Endpoint | Request | Credits |
|---|---|---|
| [Media Metadata API](#media-metadata-api) | `GET /v1/media/metadata` | 1 |

## Table of contents

- [How it works](#how-it-works)
- [Media Metadata API](#media-metadata-api)
- [Code examples in other languages](#code-examples-in-other-languages)
- [Use cases](#use-cases)
- [Why HuntAPI?](#why-huntapi)
- [FAQ](#faq)
- [Official SDKs](#official-sdks)
- [Related repositories](#related-repositories)
- [Support](#support)

## How it works

1. **Create a HuntAPI account** and copy your API key from the [dashboard](https://app.huntapi.com/register).
2. **Call `https://api.huntapi.com`** with the header `x-api-key: YOUR_API_KEY`.
3. **Use the result** in your app — no infrastructure to run.

```bash
export HUNTAPI_API_KEY="your-api-key"
pip install requests        # Python
# TypeScript: Node.js 18+ (native fetch), run with `npx tsx file.ts`
```

## Media Metadata API

Extract metadata from a media URL without downloading the file.

`GET https://api.huntapi.com/v1/media/metadata` · **1 credit per request** · [API reference](https://app.huntapi.com/openapi)

### Request parameters

| Parameter | In | Type | Required | Description |
|---|---|---|---|---|
| `query` | query | string | ✅ | Media URL to inspect (YouTube, Instagram, TikTok, Vimeo, X, Facebook, Twitch, Reddit, etc.). |

### Python example

```python
import os

import requests

API_KEY = os.environ["HUNTAPI_API_KEY"]
HEADERS = {"x-api-key": API_KEY}

response = requests.get(
    "https://api.huntapi.com/v1/media/metadata",
    headers=HEADERS,
    params={
        "query": "https://www.youtube.com/watch?v=Z5YP8kznWZs",
    },
    timeout=120,
)
response.raise_for_status()

data = response.json()
print(data)
```

### TypeScript example

```typescript
type MediaMetadataApi = {
  metadata?: {
    id?: string;
    ext?: string;
    title?: string;
    width?: number;
    height?: number;
    channel?: string;
    is_live?: boolean;
    duration?: number;
    was_live?: boolean;
    extractor?: string;
    thumbnail?: string;
    like_count?: number;
    view_count?: number;
    channel_url?: string;
    description?: string;
    live_status?: string;
    upload_date?: number;
    webpage_url?: string;
    original_url?: string;
  };
};

const headers = { "x-api-key": process.env.HUNTAPI_API_KEY!, "Content-Type": "application/json" };

const params = new URLSearchParams({
  "query": "https://www.youtube.com/watch?v=Z5YP8kznWZs",
});

const response = await fetch(`https://api.huntapi.com/v1/media/metadata?${params}`, { headers });
if (!response.ok) throw new Error(`HTTP ${response.status}: ${await response.text()}`);

const data = (await response.json()) as MediaMetadataApi;
console.log(data);
```

### Output example

Example response from the API reference, abridged.

```json
{
  "metadata": {
    "id": "3g3Eow41B6I",
    "ext": "mp4",
    "title": "Faire une interview Multicam avec UNE SEULE caméra",
    "width": 640,
    "height": 360,
    "channel": "Alex Jackson",
    "is_live": false,
    "duration": 432,
    "was_live": false,
    "extractor": "Youtube",
    "thumbnail": "https://i.ytimg.com/vi/3g3Eow41B6I/maxresdefault.jpg",
    "like_count": 4060,
    "view_count": 93297,
    "channel_url": "https://www.youtube.com/channel/UCW0GdGxlRENND_ft84Cp5vg",
    "description": "🎁 Starter Pack DaVinci Resolve GRATUIT : https://formations.alexjackson.io/starter-pack-davinci-resolve",
    "live_status": "not_live",
    "upload_date": 1712188800,
    "webpage_url": "https://www.youtube.com/watch?v=3g3Eow41B6I",
    "original_url": "https://www.youtube.com/watch?v=3g3Eow41B6I"
  }
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `metadata` | object |  |
| `metadata.id` | string |  |
| `metadata.ext` | string |  |
| `metadata.title` | string |  |
| `metadata.width` | integer |  |
| `metadata.height` | integer |  |
| `metadata.channel` | string |  |
| `metadata.is_live` | boolean |  |
| `metadata.duration` | integer |  |
| `metadata.was_live` | boolean |  |
| `metadata.extractor` | string |  |
| `metadata.thumbnail` | string |  |
| `metadata.like_count` | integer |  |
| `metadata.view_count` | integer |  |
| `metadata.channel_url` | string |  |
| `metadata.description` | string |  |
| `metadata.live_status` | string |  |
| `metadata.upload_date` | integer |  |
| `metadata.webpage_url` | string |  |
| `metadata.original_url` | string |  |

## Code examples in other languages

Ready-to-run examples live in [`examples/`](examples); each reads your key from `HUNTAPI_API_KEY`.

| Language | `media-metadata` |
|---|---|
| cURL (Bash) | [media_metadata.sh](examples/curl/media_metadata.sh) |
| PHP | [media_metadata.php](examples/php/media_metadata.php) |
| C# | [MediaMetadata.cs](examples/csharp/MediaMetadata.cs) |
| Go | [media_metadata.go](examples/go/media_metadata.go) |
| Java | [MediaMetadataExample.java](examples/java/MediaMetadataExample.java) |
| Ruby | [media_metadata.rb](examples/ruby/media_metadata.rb) |
| Node.js | [media_metadata.mjs](examples/nodejs/media_metadata.mjs) |

## Use cases

- **Link previews** — Show title, thumbnail and duration for pasted media links.
- **Pre-download checks** — Check duration and availability before starting a download job.
- **Content databases** — Enrich catalogs with channel, views and upload date.

## Why HuntAPI?

- **Async by design** — submit a URL, get a `job_id`, follow `progress` (0–100) or receive a webhook.
- **Video & audio** — choose quality (up to `1080p` / `best`) and format (`mp4`, `webm`, `mkv`, `mp3`, `m4a`, `wav`).
- **Metadata in one call** — title, duration, thumbnail, channel and view counts without downloading the file.
- **One API key, one header** — `x-api-key` on every request, JSON everywhere.
- **Copy-paste examples** — Python and TypeScript in each README, 7 more languages in `examples/`.

## FAQ

### How do I authenticate?

Create an account on [HuntAPI](https://app.huntapi.com/register), copy your API key and send it in the `x-api-key` header of every request to `https://api.huntapi.com`.

### How much does a request cost?

Credits per call: `/v1/media/metadata` **1**. See [HuntAPI pricing](https://www.huntapi.com/pricing).

### Which platforms are supported?

YouTube, Instagram, TikTok, Vimeo, X, Facebook, Twitch, Reddit and more, as listed in the API reference.

### Which languages are supported?

Any language that can make an HTTP request. This README shows Python and TypeScript; the [`examples/`](examples) folder contains cURL, PHP, C#, Go, Java, Ruby and Node.js.

## Official SDKs

Use HuntAPI from your own language with a typed client:

| SDK | Package | Install |
| --- | --- | --- |
| Node.js | [`@huntapi/sdk`](https://www.npmjs.com/package/@huntapi/sdk) | `npm install @huntapi/sdk` |
| Python | [`huntapi`](https://pypi.org/project/huntapi/) | `pip install huntapi` |
| Go | [`huntapi-go`](https://pkg.go.dev/github.com/huntapi/huntapi-go) | `go get github.com/huntapi/huntapi-go` |
| .NET | [`HuntApi`](https://www.nuget.org/packages/HuntApi) | `dotnet add package HuntApi` |
| Ruby | [`huntapi`](https://rubygems.org/gems/huntapi) | `gem install huntapi` |
| PHP | [`huntapi/sdk`](https://packagist.org/packages/huntapi/sdk) | `composer require huntapi/sdk` |
| Java | [`huntapi-java`](https://github.com/huntapi/huntapi-java) | build from source, see its README |
| CLI | [`@huntapi/cli`](https://www.npmjs.com/package/@huntapi/cli) | `npm install -g @huntapi/cli` |
| MCP server | [`@huntapi/mcp`](https://www.npmjs.com/package/@huntapi/mcp) | `npx -y @huntapi/mcp` |

## Related repositories

- [Video Download API](https://github.com/huntapi/video-download-api)
- [Audio Download API](https://github.com/huntapi/audio-download-api)
- [YouTube Video Downloader API](https://github.com/huntapi/youtube-video-downloader-api)
- [YouTube to MP3 API](https://github.com/huntapi/youtube-to-mp3-api)
- [All HuntAPI repositories](https://github.com/huntapi)

## Support

- 💬 Join the [Discord](https://discord.gg/CFj3ph8aHU) to ask questions and share what you build.
- 📚 Read the [API reference](https://docs.huntapi.com).
- 🔑 [Get your API key](https://app.huntapi.com/register).

---

<p align="center">
  <a href="https://www.huntapi.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="images/logo-dark.svg">
      <img src="images/logo.svg" alt="HuntAPI" height="28">
    </picture>
  </a>
  <br>
  <sub>Built by <a href="https://www.huntapi.com">HuntAPI</a>. Examples are released under the MIT license.</sub>
</p>
