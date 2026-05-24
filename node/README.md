# Nano Banana Pro Node.js Example

This example submits a `nano-banana-pro` task from server-side Node.js code, stores the returned `data.task_id`, and polls until the task reaches `finished` or `failed`.

## Run

```bash
cp ../.env.example ../.env
# Set POYO_API_KEY in ../.env
npm start
```

The script exits before making a request if `POYO_API_KEY` is missing.

## Notes

- Keep API keys in server-side environment variables.
- Persist the task ID in your own database before polling.
- Use webhooks for long-running production queues.