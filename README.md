Edit agentVENV/lib/python3.12/site-packages/minisweagent/config/mini.yaml and add (remember the 2x and 4x indents!)
```
model:
  cost_tracking: "ignore_errors"
  [SNIP]
  model_name: "localModel"
  model_kwargs:
    custom_llm_provider: "openai"
    api_base: "http://127.0.0.1:9000/v1"
    api_key: "dummy"
    drop_params: true
```	