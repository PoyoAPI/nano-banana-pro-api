# Nano Banana Pro cURL Examples

Use these requests to submit a Nano Banana Pro task and poll for the result.

## Generate

```bash
export POYO_API_KEY="YOUR_POYO_API_KEY_HERE"
export POYO_BASE_URL="https://api.poyo.ai"

curl --fail-with-body --request POST \
  --url "$POYO_BASE_URL/api/generate/submit" \
  --header "Authorization: Bearer $POYO_API_KEY" \
  --header "Content-Type: application/json" \
  --data '{
    "model": "nano-banana-pro",
    "input": {
      "prompt": "A premium campaign visual for a modular desk lamp, warm interior scene, accurate product geometry, soft shadows, tasteful negative space for headline text",
      "size": "auto",
      "resolution": "2K",
      "output_format": "png",
      "enable_web_search": false,
      "n": 1
    }
  }'
```

Store the returned `data.task_id`, then poll:

```bash
curl --fail-with-body --request GET \
  --url "$POYO_BASE_URL/api/generate/status/task-unified-example" \
  --header "Authorization: Bearer $POYO_API_KEY"
```

## Image Edit Request

Use `nano-banana-pro-edit` when the request includes one or more source images.

```bash
curl --fail-with-body --request POST \
  --url "$POYO_BASE_URL/api/generate/submit" \
  --header "Authorization: Bearer $POYO_API_KEY" \
  --header "Content-Type: application/json" \
  --data '{
    "model": "nano-banana-pro-edit",
    "callback_url": "https://example.com/api/poyo/webhook",
    "input": {
      "prompt": "Preserve the source subject, improve the scene composition, and keep the result realistic and production-ready",
      "size": "auto",
      "resolution": "2K",
      "output_format": "png",
      "enable_web_search": false,
      "n": 1,
      "image_urls": [
        "https://example.com/source-product.png"
      ]
    }
  }'
```

## Expected Submit Response

```json
{
  "code": 200,
  "data": {
    "task_id": "task-unified-example",
    "status": "not_started",
    "created_time": "2026-05-23T08:00:00"
  }
}
```

## Expected Status Response

```json
{
  "code": 200,
  "data": {
    "task_id": "task-unified-example",
    "status": "finished",
    "progress": 100,
    "files": [
      {
        "file_url": "https://storage.poyo.ai/generated/image.png",
        "file_type": "image"
      }
    ],
    "error_message": null
  }
}
```
