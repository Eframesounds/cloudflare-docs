---
_build:
  publishResources: false
  render: never
  list: never
---
`https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/workers-ai/`

When making requests to Workers AI, replace `https://api.cloudflare.com/client/v4/accounts/{account_id}/ai/run` in the URL you’re currently using with `https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/workers-ai`.

Then add the model you want to run at the end of the URL. You can see the list of [Workers AI models](https://developers.cloudflare.com/workers-ai/models/) and pick the ID.

You'll need to generate an [API token](/fundamentals/api/get-started/create-token/) with Workers AI read access and use it in your request.

```bash
---
header: Request to Workers AI llama model
---

curl https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/workers-ai/@cf/meta/llama-3-8b-instruct \
 --header 'Authorization: Bearer {cf_api_token}' \
 --header 'Content-Type: application/json' \
 --data '{"prompt": "What is Cloudflare?"}'
```

```bash
---
header: Request to Workers AI text classification model
---

curl https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/workers-ai/@cf/huggingface/distilbert-sst-2-int8 \
  --header 'Authorization: Bearer {cf_api_token}' \
  --header 'Content-Type: application/json' \
  --data '{ "text": "Cloudflare docs are amazing!" }'
```

## OpenAI compatible endpoints

{{<render file="_openai-compatibility.md" productFolder="workers-ai">}}
<br/>

```bash
---
header: Request to OpenAI compatible endpoint
---
curl https://gateway.ai.cloudflare.com/v1/{account_id}/{gateway_slug}/workers-ai/v1/chat/completions \
 --header 'Authorization: Bearer {cf_api_token}' \
 --header 'Content-Type: application/json' \
 --data '{
      "model": "@cf/meta/llama-3-8b-instruct",
      "messages": [
        {
          "role": "user",
          "content": "What is Cloudflare?"
        }
      ]
    }
'
```