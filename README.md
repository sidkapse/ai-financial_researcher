# ai-financial_researcher

An AI-powered financial research agent built with [CrewAI](https://www.crewai.com/) that produces comprehensive company research reports. The system uses a two-agent crew to gather real-time information from the web and synthesize it into professional, actionable reports.

## What It Does

**My Financial Researcher** runs a two-stage sequential research pipeline:

1. **Research** — A senior financial researcher agent uses web search (Serper) to collect information about the company: current status, historical performance, challenges, opportunities, recent news, and future outlook.
2. **Analysis** — A market analyst agent takes the research findings and produces a polished report with an executive summary, structured analysis, and market outlook.

The final report is saved as `report.md`, ready for review or further use.

## Capabilities

| Capability | Description |
|------------|-------------|
| **Custom companies** | Research any publicly traded company by changing the `company` input (e.g., Tesla, Apple, Nvidia). |
| **Live web search** | Uses SerperDevTool to fetch current news, financial data, and market information. |
| **Sequential process** | Tasks run in order: research → analysis, with the analyst receiving full research context. |
| **Configurable agents** | Agents (researcher, analyst) are defined in YAML with customizable roles, goals, and backstories. |
| **Structured output** | Reports follow a consistent format: executive summary, financial health, historical performance, challenges & opportunities, recent news, market outlook. |
| **Professional reports** | Output is formatted in Markdown with clear headings and disclaimers (e.g., not for trading decisions). |
| **Verbose mode** | Full reasoning and step-by-step output are visible during execution. |

## Project Structure

```
my_financial_researcher/
├── src/my_financial_researcher/
│   ├── config/
│   │   ├── agents.yaml    # Researcher & analyst agent definitions
│   │   └── tasks.yaml     # Research and analysis task definitions
│   ├── crew.py            # CrewAI crew definition
│   └── main.py            # Entry point (run)
├── report.md              # Generated research report (output)
├── .env                   # API keys (OPENAI_API_KEY, SERPER_API_KEY)
├── pyproject.toml
└── README.md
```

## Requirements

- Python 3.10–3.13
- [OpenAI API key](https://platform.openai.com/api-keys) — for the LLM
- [Serper API key](https://serper.dev/) — for web search (free tier available)

## Setup

1. **Clone** the repository and navigate to `3_crew/my_financial_researcher`.

2. **Create a virtual environment** and install dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   pip install -e .
   ```

3. **Configure environment variables** in `.env`:

   ```env
   OPENAI_API_KEY=your-openai-api-key
   SERPER_API_KEY=your-serper-api-key
   MODEL=gpt-4.1-mini-2025-04-14
   ```

## Usage

### Run a research report

Default company: **Tesla**

```bash
run_crew
```

### Customize the company

Edit the `inputs` dict in `main.py`:

```python
inputs = {
    'company': 'Apple'  # or Nvidia, Microsoft, etc.
}
```

## Example Output

For the company **Tesla**, the report includes:

- **Executive summary** — High-level overview of Tesla’s position in EVs and energy
- **Financial health** — Revenue, profitability, margins, balance sheet strength
- **Historical performance** — Stock evolution, production, market leadership
- **Challenges & opportunities** — Demand trends, competition, new products, energy storage
- **Recent news** — Latest developments, product launches, market shifts
- **Market outlook** — Analyst views, future plans, risks and catalysts
- **Disclaimer** — Report is for informational use, not for trading decisions

Output is saved in `report.md`.

## Built With

- [CrewAI](https://github.com/joaomdmoura/crewAI) — Framework for orchestrating AI agents
- [CrewAI Tools](https://github.com/joaomdmoura/crewAI-tools) — SerperDevTool for web search
- [OpenAI GPT-4.1-mini](https://platform.openai.com/docs/models) — Model used by the agents
- [Serper](https://serper.dev/) — Google Search API for real-time data

## License

MIT
