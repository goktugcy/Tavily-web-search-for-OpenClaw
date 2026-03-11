# Tavily Web Search Skill for OpenClaw

A lightweight Tavily web search skill for OpenClaw that works without `pip` or third-party Python packages.

This skill is designed for minimal Linux environments such as:

- Raspberry Pi
- Ubuntu Server
- small VPS setups
- systems where `pip` is unavailable or intentionally avoided

Instead of using the `tavily-python` SDK, this skill calls the Tavily REST API directly using Python's standard library.

## Features

- Tavily web search through direct REST API calls
- No `pip install` required
- No external Python dependencies
- Works well on Raspberry Pi and Ubuntu Server
- Supports general search and news search
- Supports answer summaries, images, and domain filtering
- Easy to integrate into OpenClaw skills

## Why this version exists

The official Tavily Python SDK is convenient, but some environments do not have a practical `pip` workflow.

This skill exists for setups where you want:

- a small footprint
- no package installation step
- predictable deployment
- compatibility with minimal server environments

## Folder Structure

```text
skills/tavily/
├── SKILL.md
├── .secrets/
│   └── tavily.key
└── scripts/
    └── tavily_search.py
```

## Secret Setup

Create the secret directory:

```bash
mkdir -p skills/tavily/.secrets
chmod 700 skills/tavily/.secrets
```

Create the key file:

```bash
nano skills/tavily/.secrets/tavily.key
```

The file must contain only your raw Tavily API key:

```
tvly-xxxxxxxxxxxxxxxx
```

Do **not** write:

```
TAVILY_API_KEY=tvly-xxxxxxxxxxxxxxxx
```

Set permissions:

```bash
chmod 600 skills/tavily/.secrets/tavily.key
```

## Usage

Basic search:

```bash
python3 skills/tavily/scripts/tavily_search.py --query "latest AI news"
```

News-focused search:

```bash
python3 skills/tavily/scripts/tavily_search.py --query "gold prices" --topic news
```

Advanced search:

```bash
python3 skills/tavily/scripts/tavily_search.py --query "raspberry pi ubuntu server optimization" --depth advanced
```

JSON output:

```bash
python3 skills/tavily/scripts/tavily_search.py --query "python asyncio" --json
```

## Supported Options

| Option              | Description                  |
| ------------------- | ---------------------------- |
| `--query`           | **required** search query    |
| `--topic`           | `general` or `news`          |
| `--depth`           | `basic` or `advanced`        |
| `--max-results`     | number of results            |
| `--no-answer`       | disable answer summary       |
| `--raw-content`     | include parsed raw content   |
| `--images`          | include image results        |
| `--include-domains` | restrict to selected domains |
| `--exclude-domains` | filter out selected domains  |
| `--json`            | output raw JSON              |

## OpenClaw Integration

This skill is meant to be used from OpenClaw through `SKILL.md`.

Typical usage flow:

1. User asks for web search or recent information
2. OpenClaw invokes the Tavily skill
3. The skill runs `scripts/tavily_search.py`
4. The script reads the API key from `.secrets/tavily.key`
5. Results are returned in a format suitable for summarization

## Security Notes

- The `.secrets` directory should never be committed
- Your API key should stay only on the target machine
- This repository should contain code and documentation only
- Add `.secrets/` to `.gitignore`

## Requirements

- Python 3
- Network access to Tavily API
- A valid Tavily API key
- No additional Python packages are required.

## Motivation

This project is especially useful for:

- Raspberry Pi home server setups
- Ubuntu Server deployments
- Offline-managed environments where dependencies are tightly controlled
- Users who want Tavily search without SDK installation

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.