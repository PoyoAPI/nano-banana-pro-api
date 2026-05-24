# Production Notes

Use this checklist before putting Nano Banana Pro image generation or editing into a user-facing product.

## API Key Safety

- Store `POYO_API_KEY` in server-side environment variables.
- Never send the key to browser code or mobile clients.
- Do not print `Authorization` headers in logs.

## Task State

- Persist `data.task_id` immediately after submit.
- Treat `finished` and `failed` as terminal states.
- Store the selected model, user ID, request time, and final status together.

## Polling

- Poll with a moderate interval, such as 5 to 10 seconds.
- Add a timeout in your application.
- Reconcile important webhook callbacks with the status endpoint.

## Webhooks

- Verify that the callback `task_id` belongs to a task your system submitted.
- Return 2xx quickly.
- Make duplicate callbacks safe.
- Replace demo in-memory state with your database.

## Files

- Download generated files before they expire.
- Copy production assets to your own storage.
- Avoid logging private media URLs when they contain customer content.