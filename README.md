# Creative Automation for Scalable Social Ad Campaigns

A demo-ready local Python project that ingests campaign briefs, reuses or generates missing assets, overlays campaign messaging, and organizes outputs by product and aspect ratio. Includes an agentic monitor, diagrams, and documentation.

## Features
- **Pipeline**: Ingest brief (YAML/JSON), reuse local assets, generate missing creatives (OpenAI Image API or placeholder fallback), overlay campaign message, and save to `output/{product}/{aspect}/`.
- **Aspect Ratios**: 1:1, 9:16, 16:9.
- **Agent**: Monitors `input/briefs/`, triggers pipeline, tracks counts, flags <3 variants, drafts alert emails to console.
- **Docs**: Mermaid architecture and agentic diagrams, 1-slide roadmap, stakeholder email sample.
- **Config**: `.env` for keys, logging level, optional font path.

## Project Structure
```
creative-automation-project/
├── README.md
├── requirements.txt
├── main.py
├── .env.example
├── input/
│   ├── briefs/
│   │   └── sample_brief.yaml
│   └── assets/
├── output/
├── src/
│   ├── pipeline/
│   │   ├── asset_ingestion.py
│   │   ├── asset_generation.py
│   │   └── post_processor.py
│   └── utils/
│       └── logger.py
├── agent/
│   └── monitor.py
└── docs/
    ├── architecture_diagram.mmd
    ├── agentic_system_design.mmd
    ├── roadmap.md
    └── stakeholder_email.md
```

## Setup (Windows)
1. Install Python 3.10+.
2. Create venv and install deps:
```
py -3 -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```
3. Create `.env` from `.env.example` and set `OPENAI_API_KEY` if using OpenAI image generation.

## Run the Pipeline
```
python -m main --brief input/briefs/sample_brief.yaml
```
- Outputs to `output/{product}/{aspect}/`.
- If `OPENAI_API_KEY` is not set, placeholder images are generated locally with Pillow.

## Run the Agent Monitor
- Run once:
```
python -m agent.monitor --once
```
- Watch folder (polling every 10s):
```
python -m agent.monitor --watch --interval 10
```
- Agent triggers the pipeline for each new brief and logs a draft email if assets per product/aspect are <3.

## Environment
- `.env` keys:
  - `OPENAI_API_KEY` (optional)
  - `OPENAI_IMAGE_MODEL=gpt-image-1` (optional)
  - `LOG_LEVEL=INFO`
  - `FONT_PATH` (optional, path to a .ttf font)

## Diagrams
- Mermaid files in `docs/`.
- If your IDE cannot export diagrams, open `.mmd` files in https://mermaid.live or import to draw.io/Excalidraw to export PNG/SVG.

## Example Brief
See `input/briefs/sample_brief.yaml`.

## Limitations
- OpenAI image generation requires an API key and may incur costs.
- Non-square images are derived by resizing/cropping from a base image.
- Brand compliance checks are simplified (color usage and optional logo overlay).
- Text moderation is a simple keyword blocker for demo purposes.

## License
MIT (for take-home demo purposes).
