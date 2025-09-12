# miniflux-luma

Atom feed exporter for Miniflux starred items

## Features

- Export Miniflux starred items as an Atom feed
- Configurable limit for number of entries
- Lightweight and fast
- Available as a single binary or Docker container
- Multi-arch support (amd64, arm64)

## Installation

### Pre-built Binaries

Download the latest release from the [GitHub Releases](https://github.com/blacs30/miniflux-luma/releases) page.

### From Source

```bash
go install github.com/blacs30/miniflux-luma@latest
```

### Docker

```bash
docker run -p 8080:8080 \
  -e MINIFLUX_ENDPOINT=https://miniflux.example.com \
  -e MINIFLUX_API_TOKEN_FILE=api_token \
  ghcr.io/yourusername/miniflux-luma:latest
```

## Usage

### Configuration

| Flag              | Environment Variable      | Default                        | Description                         |
| ----------------- | ------------------------- | ------------------------------ | ----------------------------------- |
| `-endpoint`       | `MINIFLUX_ENDPOINT`       | `https://miniflux.example.org` | Miniflux server URL                 |
| `-api-token-file` | `MINIFLUX_API_TOKEN_FILE` | `api_token`                    | Path to file containing API token   |
| `-listen-addr`    | `LISTEN_ADDR`             | `127.0.0.1:8080`               | Address to listen on                |
| `-feed-title`     | `FEED_TITLE`              | `Starred entries`              | Title of the Atom feed              |
| `-limit`          | `LIMIT`                   | `100`                          | Maximum number of entries to return |
| `-tls-cert`       | `TLS_CERT`                | ``                             | Path to TLS certificate file        |
| `-tls-key`        | `TLS_KEY`                 | ``                             | Path to TLS key file                |

### Environment Variables

You can also configure the application using environment variables. These take precedence over command-line flags.

### Example

```bash
# Using command line arguments
miniflux-luma \
  -endpoint https://miniflux.example.com \
  -listen-addr :8080 \
  -limit 1000

# Using environment variables
export MINIFLUX_ENDPOINT=https://miniflux.example.com
export MINIFLUX_API_TOKEN_FILE=api_token
export LIMIT=1000
miniflux-luma
```

## Docker Compose

```yaml
version: "3.8"

services:
  miniflux-luma:
    image: ghcr.io/yourusername/miniflux-luma:latest
    restart: unless-stopped
    ports:
      - "8080:8080"
    environment:
      - MINIFLUX_ENDPOINT=https://rss.example.com
      - MINIFLUX_API_TOKEN_FILE=api_token
      - LISTEN_ADDR=:8080
      - LIMIT=1000
```

## Development

### Building from Source

```bash
git clone https://github.com/blacs30/miniflux-luma.git
cd miniflux-luma
go build
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
