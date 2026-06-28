# providers-record

Online provider registry for Radiumical.

This repository hosts a public list of LLM provider endpoints and a CSV source that can be converted to the JSONL registry format.

## Files

- `providers.jsonl` — Registry consumed by Radiumical clients (`https://radiumical.dev/providers.jsonl`).
- `providers.csv` — Human-editable source.

## Schema

Each JSONL line is a `ProviderSource`:

```json
{
  "provider": "openai",
  "name": "OpenAI",
  "api_type": "openai-chat",
  "api_base": "https://api.openai.com/v1",
  "key_env": "OPENAI_API_KEY",
  "models_endpoint": "/models",
  "auth_header": "Authorization",
  "version_header": null,
  "models": ["gpt-4o", "gpt-4o-mini"]
}
```

### `api_type` values

- `openai-chat` — OpenAI-compatible `/chat/completions` endpoint.
- `anthropic` — Anthropic Messages API.
- `ollama` — Local Ollama server (OpenAI-compatible).
- `unsupported` — Not yet implemented in Radiumical.

## Updating the registry

Edit `providers.csv`, then convert it with the `csv-to-jsonl` tool in the main Radiumical repo:

```bash
cargo run -p csv-to-jsonl -- -i providers.csv -o providers.jsonl
```

Then commit and push both files.

## License

MIT
