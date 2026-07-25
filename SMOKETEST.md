Recommended smoketest for koboldcpp - first tell it to list folder contents

```
curl http://127.0.0.1:9000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "anything",
    "messages": [
      {
        "role": "user",
        "content": "List the current directory using the bash tool."
      }
    ],
    "tools": [
      {
        "type": "function",
        "function": {
          "name": "bash",
          "description": "Run a shell command",
          "parameters": {
            "type": "object",
            "properties": {
              "command": {
                "type": "string"
              }
            },
            "required": ["command"]
          }
        }
      }
    ]
  }'
```  

if it works, throw simulated results in:

```  
curl http://127.0.0.1:9000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "anything",
    "messages": [
      {
        "role": "user",
        "content": "List the current directory using the bash tool."
      },
      {
        "role": "assistant",
        "tool_calls": [{
          "id": "call_123",
          "type": "function",
          "function": {
            "name": "bash",
            "arguments": "{\"command\":\"ls -la\"}"
          }
        }]
      },
      {
        "role": "tool",
        "tool_call_id": "call_123",
        "content": "total 12\nfoo.txt"
      }
    ]
  }'
```  