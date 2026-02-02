# 🤖 AI Developer Assistant - Cloudflare Agents

A powerful AI-powered developer assistant built on Cloudflare's platform, featuring Llama 3.1 on Workers AI with custom developer utility tools.

## 🌟 Features

### Core Components
- **LLM**: Llama 3.1 8B running on Cloudflare Workers AI
- **Workflow/Coordination**: Durable Objects for state management + Workflows for task scheduling
- **User Interface**: Real-time chat interface built with React
- **Memory/State**: Persistent chat history using Durable Objects with SQLite

### Developer Tools
1. **Base64 Encoder/Decoder** - Encode or decode text to/from base64
2. **UUID Generator** - Generate random UUIDs (v4)
3. **Hash Generator** - Create SHA-256 or SHA-1 cryptographic hashes
4. **JSON Formatter** - Validate and format JSON strings
5. **Weather Lookup** - Get weather information (requires confirmation)
6. **Task Scheduler** - Schedule tasks with flexible timing (delayed, scheduled, cron)

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ installed
- Cloudflare account
- Wrangler CLI

### Local Development

1. **Clone the repository**
```bash
git clone <your-repo-url>
cd cloudflare
```

2. **Install dependencies**
```bash
npm install
```

3. **Start development server**
```bash
npm start
```

4. **Open in browser**
```
http://localhost:5173/
```

### Deployment

1. **Deploy to Cloudflare**
```bash
npm run deploy
```

2. **Access your deployed app**
The deployment will provide a URL like: `https://cloudflare.<your-subdomain>.workers.dev`

## 💡 Usage Examples

### Developer Tools

**Base64 Encoding**
```
You: Encode "hello world" to base64
AI: [Uses base64Tool] Base64 encoded: aGVsbG8gd29ybGQ=
```

**Generate UUID**
```
You: Generate a UUID
AI: [Uses generateUUID] Generated UUID: 550e8400-e29b-41d4-a716-446655440000
```

**Hash Generation**
```
You: Hash "password123" with SHA-256
AI: [Uses hashGenerator] SHA-256 hash: ef92b778bafe771e89245b89ecbc08a44a4e166c06659911881f383d4473e94f
```

**JSON Formatting**
```
You: Format this JSON: {"name":"test","values":[1,2,3]}
AI: [Uses jsonFormatter] Valid JSON (formatted):
```json
{
  "name": "test",
  "values": [
    1,
    2,
    3
  ]
}
```
```

### Task Scheduling

```
You: Schedule a reminder in 30 seconds to take a break
AI: [Uses scheduleTask] Task scheduled for type "delayed" : 30
```

### General Chat

```
You: What's 127 * 45?
AI: 5,715
```

## 🏗️ Architecture

```
┌─────────────────┐
│   React UI      │ ← User Interface (Pages)
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│  Durable Object │ ← State Management + Chat Logic
│   (Chat Agent)  │
└────────┬────────┘
         │
         ↓
┌─────────────────┐
│   Workers AI    │ ← LLM (Llama 3.1 8B)
│  (Llama 3.1)    │
└─────────────────┘
```

### Key Files

- `src/server.ts` - Chat agent logic, LLM integration
- `src/tools.ts` - Tool definitions (developer utilities)
- `src/app.tsx` - React chat UI
- `src/utils.ts` - Helper functions for tool processing
- `wrangler.jsonc` - Cloudflare Workers configuration

## 🛠️ Development

### Adding New Tools

1. Define tool in `src/tools.ts`:
```typescript
const myTool = tool({
  description: "Description of what the tool does",
  inputSchema: z.object({
    param: z.string().describe("Parameter description")
  }),
  execute: async ({ param }) => {
    // Tool logic here
    return "Result";
  }
});
```

2. Export in tools object:
```typescript
export const tools = {
  // ... existing tools
  myTool
} satisfies ToolSet;
```

3. Update system prompt in `src/server.ts` to inform the AI about the new tool.

### Running Tests

```bash
npm test
```

### Code Formatting

```bash
npm run format
npm run check
```

## 📦 Tech Stack

- **Runtime**: Cloudflare Workers
- **LLM**: Llama 3.1 8B (Workers AI)
- **Framework**: React 19
- **Build Tool**: Vite
- **State Management**: Durable Objects
- **Styling**: Tailwind CSS
- **Type Safety**: TypeScript
- **AI SDK**: Vercel AI SDK + Workers AI Provider

## 🎯 Assignment Requirements

✅ **LLM**: Llama 3.1 on Cloudflare Workers AI
✅ **Workflow/Coordination**: Durable Objects + Workflows
✅ **User Input**: React-based chat interface
✅ **Memory/State**: Durable Objects with SQLite storage
✅ **Custom Tools**: 4 developer utility tools
✅ **Documentation**: README.md with setup instructions
✅ **AI Prompts**: PROMPTS.md with all prompts used

## 📝 License

MIT

## 🔗 Links

- [Cloudflare Agents Documentation](https://developers.cloudflare.com/agents/)
- [Workers AI Documentation](https://developers.cloudflare.com/workers-ai/)
- [Durable Objects Documentation](https://developers.cloudflare.com/durable-objects/)
