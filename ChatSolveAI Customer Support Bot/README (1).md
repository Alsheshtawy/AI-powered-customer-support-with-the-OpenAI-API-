# ChatSolveAI Customer Support Bot

A customer support chatbot built with the OpenAI API as part of a DataCamp certification project.

## What it does
1. **Knowledge base to embeddings:** embeds every document with `text-embedding-3-small` in one batched call and saves them to `knowledge_embeddings.json`.
2. **Query matching:** embeds customer queries and finds the top 3 predefined responses by cosine similarity, with exponential-backoff retries for rate limits and confidence scores scaled 0-1 (`query_responses.json`).
3. **Chatbot:** returns the closest stored answer when similarity is at least 0.6, otherwise generates one with `gpt-4o-mini`. Each interaction is logged with query, response, timestamp and confidence (`sample_chatbot_responses.json`).

## Run it
```bash
pip install openai pandas numpy jupyter
export OPENAI_API_KEY="your-key-here"     # Windows PowerShell: $env:OPENAI_API_KEY="your-key-here"
jupyter notebook chatsolveai_support_bot.ipynb
```
Put the input files (`knowledge_base.csv`, `processed_queries.csv`, `predefined_responses.json`, `chatbot_responses.json`) next to the notebook.

## What I learned
- Inspect the data structure before writing code.
- Choose similarity thresholds from real scores (support-hours paraphrase: 0.68, uncovered refund question: 0.55).
- Batch embedding requests to save time and avoid rate limits.
