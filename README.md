# Semantic Search with OpenAI Embeddings

A Jupyter notebook that does semantic search over AI Show video transcripts using Azure OpenAI embeddings. Type a query such as "What is Azure Machine Learning?" and get the most relevant videos, with links to the matching timestamp on YouTube.

## How it works

1. `transcripts_the_ai_show_index_enriched_lite_3m.json` holds the video segments, each with a precomputed embedding (`ada_v2` column).
2. Your query is embedded with Azure OpenAI.
3. Cosine similarity is computed between the query and every segment.
4. Segments scoring at least `0.75` are kept, and the top 5 are shown with title, summary, speakers, topics and a YouTube link.

## Prerequisites

- [uv](https://docs.astral.sh/uv/)
- An Azure OpenAI resource with a `text-embedding-ada-002` deployment

## Setup

```bash
uv sync
cp .env.example .env
```

Edit `.env` and fill in your values:

| Variable | Description |
| --- | --- |
| `AZURE_OPENAI_API_KEY` | Key from the resource's **Keys and Endpoint** page |
| `AZURE_OPENAI_ENDPOINT` | e.g. `https://<your-resource>.openai.azure.com/` |
| `AZURE_OPENAI_EMBEDDING_MODEL_DEPLOYMENT_NAME` | The **deployment name** of your embedding model (from **Model deployments**), not the model name |

`.env` is gitignored, so your key is not committed.

## Run

```bash
uv run jupyter lab main.ipynb
```

Run the cells in order. The last cell prompts for a query; type `exit` to stop.

## Notes

- The project uses the legacy `openai` 0.28 SDK (`openai.embeddings_utils`). Newer `openai` versions are not compatible with this notebook.
- Python 3.12 is required; the pinned dependencies do not have Python 3.13 builds.
