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
