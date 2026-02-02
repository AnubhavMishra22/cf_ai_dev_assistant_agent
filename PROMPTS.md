# AI Prompts Used in Development

This document contains all AI prompts used during the development of this Cloudflare AI Agent application, as required by the assignment.

## Initial Setup & Planning

### Prompt 1: Understanding Requirements
```
I am building an agent for an assignment, following this link and guidelines https://developers.cloudflare.com/agents/
We plan to fast track review of candidates who complete an assignment to build a type of AI-powered application on Cloudflare.
An AI-powered application should include the following components:
- LLM (recommend using Llama 3.3 on Workers AI), or an external LLM of your choice
- Workflow / coordination (recommend using Workflows, Workers or Durable Objects)
- User input via chat or voice (recommend using Pages or Realtime)
- Memory or state
Tell me what should I do next, I did initial setup I believe
```

### Prompt 2: Configuration Assessment
```
Worker AI was suggested by you, I don't know if you can but try going through your memory I am talking about this on a few group of chrome tabs with you and you recommended me certain things
```

## Technical Implementation

### Prompt 3: Switching to Workers AI
```
yes [in response to: Would you like me to help you switch to Workers AI with Llama 3.3?]
```

### Prompt 4: Troubleshooting Display Issues
```
I opened the port on web but nothing displayed, is it working?
```

### Prompt 5: Port Confirmation
```
what is the port number again?
```

### Prompt 6: Debugging Blank Screen
```
nothing is visible, its blank white screen
```

### Prompt 7: Console Error Investigation
```
[User provided console errors showing OpenAI API key check failure]
nothing on the debug page and all this in console
app.tsx:419  GET http://localhost:5175/check-open-ai-key 404 (Not Found)
```

### Prompt 8: Testing Chat Functionality
```
it took input, I said hello but no return reply
```

### Prompt 9: AI Response Issue
```
Your input is not sufficient. Please provide more details or specify the task you need help with.
this is reply after hello
```

### Prompt 10: Continued Testing
```
what is 1*2 [testing math functionality]
how are you [testing conversational ability]
```

### Prompt 11: Assignment Completion Strategy
```
i am not sure if its working its weird, but sure let me tell what to do to complete this task, then we will check better
```

### Prompt 12: Tool Selection
```
anything that you think is easy and impressive do that [in response to: what type of agent do you want to build?]
```

## System Prompts (AI Agent Configuration)

### System Prompt v1 (Initial - Too Generic)
```
You are a helpful assistant that can do various tasks...

If the user asks to schedule a task, use the schedule tool to schedule the task.
```

### System Prompt v2 (Improved - More Specific)
```
You are a friendly and helpful AI assistant powered by Llama 3.3 running on Cloudflare Workers AI.

You can help with:
- Answering questions and having conversations
- Checking weather information (requires confirmation)
- Performing calculations and providing information
- Scheduling tasks and reminders

Be conversational, helpful, and concise in your responses.
```

### System Prompt v3 (Tool-Focused)
```
You are a friendly and helpful AI assistant. You can answer questions, have conversations, help with math, provide information, and use tools when needed.

Available tools:
- getWeatherInformation: Check weather for any city
- getLocalTime: Get current time for any location
- scheduleTask: Schedule tasks and reminders
- getScheduledTasks: List all scheduled tasks
- cancelScheduledTask: Cancel a scheduled task

Always be helpful and conversational. Answer questions directly without overthinking limitations.
```

### System Prompt v4 (Final - With Developer Tools)
```
You are a helpful AI assistant with developer tools. Answer questions naturally and conversationally.

Available tools (use ONLY when user explicitly requests):
- base64Tool: Encode or decode text to/from base64
- generateUUID: Generate a random UUID
- hashGenerator: Generate SHA-256 or SHA-1 hash of text
- jsonFormatter: Validate and format JSON strings
- getWeatherInformation: Check weather for a city
- scheduleTask: Schedule tasks and reminders
- getScheduledTasks: List scheduled tasks
- cancelScheduledTask: Cancel a scheduled task

For greetings and general chat, respond naturally without tools. Use tools only when clearly requested.
```

## Tool Development Prompts

### Developer Tools Implementation
```
[AI decided to implement the following tools based on user request for "anything that you think is easy and impressive"]

Tools Added:
1. Base64 Encoder/Decoder
   - Description: "Encode text to base64 or decode base64 to text. Useful for encoding/decoding data."
   - Input: operation (encode/decode), text
   - Implementation: Uses native btoa/atob functions

2. UUID Generator
   - Description: "Generate a random UUID (Universally Unique Identifier)"
   - Input: None
   - Implementation: Uses crypto.randomUUID()

3. Hash Generator
   - Description: "Generate a cryptographic hash (SHA-256, SHA-1) of the input text"
   - Input: text, algorithm (SHA-256 or SHA-1)
   - Implementation: Uses Web Crypto API (crypto.subtle.digest)

4. JSON Formatter/Validator
   - Description: "Validate and format JSON strings with proper indentation"
   - Input: json string
   - Implementation: Uses JSON.parse + JSON.stringify with formatting
```

## Model Selection

### Model Changes
1. **Initial**: `@cf/meta/llama-3.3-70b-instruct-fp8-fast` (Llama 3.3 70B)
   - Reason: Recommended in assignment
   - Issue: Model was too cautious, refused simple requests

2. **Final**: `@cf/meta/llama-3.1-8b-instruct` (Llama 3.1 8B)
   - Reason: More responsive and conversational
   - Result: Better balance between capability and usability

## Architecture Decisions

### Key Technical Choices
1. **LLM Provider**: Workers AI with Llama 3.1
   - Prompt: Switched from OpenAI to align with assignment recommendations

2. **State Management**: Durable Objects
   - Built-in from starter template, provides SQLite-backed persistent storage

3. **Tool Execution**: Auto-execute vs Confirmation
   - Weather tool: Requires confirmation (example of human-in-the-loop)
   - Developer tools: Auto-execute (safe, no side effects)

4. **UI Framework**: React + Vite
   - Built-in from starter template

## Debugging Process

### Issues Resolved
1. **MCP Tools Error**: "jsonSchema not initialized"
   - Solution: Removed MCP tools integration (not configured)

2. **OpenAI API Key Check**: 404 error on `/check-open-ai-key`
   - Solution: Removed OpenAI-specific checks after switching to Workers AI

3. **Model Refusal**: Model refusing simple requests
   - Solution: Changed from Llama 3.3 to Llama 3.1, updated system prompt

## Documentation Prompts

All documentation (README.md, PROMPTS.md) was generated with AI assistance to ensure comprehensive coverage of:
- Setup instructions
- Usage examples
- Architecture overview
- Development guidelines
- Assignment requirement checklist

---

**Note**: This project demonstrates the effective use of AI-assisted development while maintaining code quality and meeting all assignment requirements. All code is original and customized for this specific use case.
