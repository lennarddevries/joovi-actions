# reusable docker build action

## Inputs

| Name | Required | Description |
| --- | --- | --- |
| `context` | no | Build context passed to `docker build` (default `.`). |
| `dockerfile` | no | Path to the Dockerfile (default `./Dockerfile`). |
| `target` | no | Named build stage to target. |
| `tags` | yes | Comma-separated tags applied to the image. |
| `platforms` | no | Target platforms (default `linux/amd64`). |
| `push` | no | Push image to registry (`false` by default). |
| `registry` | no | Registry hostname (default `ghcr.io`). |
| `cache-key-prefix` | no | Prefix for auto-generated cache key (default `docker`). |
| `cache-key` | no | Override cache key for layer caching when available. |
| `restore-cache-key` | no | Preferred restore key to try before the prefix fallback. |
| `build-args` | no | Additional build args (JSON string). |
| `registry-username` | no | Registry username (required when pushing). |
| `registry-token` | no | Registry token/password (required when pushing). |

The `cache-key` and `restore-cache-key` inputs let workflows supply change-detector outputs or other
precomputed values, avoiding costly rebuilds when dependency lockfiles remain unchanged.
