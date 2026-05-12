# Local AI Agent using Ollama, n8n Cloud, and ngrok

## Project Overview

This project demonstrates a cloud-connected local AI agent built using:

- n8n Cloud
- Ollama
- ngrok
- Local Large Language Models (LLMs)

The workflow enables n8n Cloud to communicate with a locally hosted AI model running through Ollama using secure ngrok tunneling.

The AI agent processes user prompts in real time and generates responses using locally hosted models instead of relying on paid external AI APIs.

This project demonstrates:
- AI workflow orchestration
- Cloud-to-local networking
- Local LLM deployment
- Secure tunneling
- AI agent integration
- Execution monitoring
- Prompt routing
- Token usage tracking

---

# Workflow Architecture

![Workflow](./screenshots/workflow-architecture.png)

---

# AI Chat Interface

![Chat](./screenshots/ai-chat-interface.png)

---

# Execution Logs

![Logs](./screenshots/execution-logs.png)

---

# Ollama Response Output

![Output](./screenshots/ollama-response-output.png)

---

# Technologies Used

| Technology | Purpose |
|---|---|
| n8n Cloud | Workflow Automation |
| Ollama | Local LLM Hosting |
| ngrok | Secure Public Tunnel |
| Llama 3.2 | AI Language Model |
| AI Agent Node | Prompt Processing |
| Chat Trigger | User Interaction |

---

# Understanding the Deployment Challenge

Initially, the workflow was designed assuming Ollama could directly connect with n8n.

Later, it was identified that the workflow was running on **n8n Cloud**, while Ollama was running locally on the developer machine.

This created a networking limitation:

```text
n8n Cloud → Cannot directly access localhost services
```

Since Ollama runs locally on:

```text
http://localhost:11434
```

the cloud-hosted n8n instance could not communicate with the local Ollama server directly.

---

# Why ngrok Was Required

To solve this issue, ngrok was introduced as a tunneling service.

ngrok exposed the local Ollama server securely to the internet by creating a public HTTPS forwarding URL.

Architecture after introducing ngrok:

```text
n8n Cloud
     ↓
ngrok Public Tunnel
     ↓
Local Ollama Server
     ↓
Llama 3.2 Model
```

This allowed the cloud workflow to communicate with the locally hosted AI model.

---

# System Architecture

```text
┌──────────────────────────────┐
│         User Input           │
│   Chat Message / Prompt      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│     n8n Cloud Workflow       │
│                              │
│  • Chat Trigger Node         │
│  • AI Agent Node             │
│  • Prompt Orchestration      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      ngrok Secure Tunnel     │
│                              │
│  Public HTTPS Forwarding     │
│  Host Header Rewriting       │
│  External Request Routing    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Local Ollama Server     │
│                              │
│  Running on localhost:11434  │
│  Handles LLM API Requests    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Llama 3.2 Model         │
│                              │
│  Local AI Inference Engine   │
│  Prompt Processing           │
│  Response Generation         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      AI Response Output      │
│                              │
│  Response returned to n8n    │
│  Execution Logs Generated    │
│  Token Usage Calculated      │
└──────────────────────────────┘
```

---

# Communication Flow

```text
User Prompt
    ↓
n8n Cloud AI Agent
    ↓
ngrok Public Tunnel
    ↓
Local Ollama API
    ↓
Llama 3.2 Model
    ↓
Generated AI Response
    ↓
n8n Execution Logs
    ↓
Chat Interface Output
```

---

# Workflow Explanation

## 1. Chat Trigger Node

The workflow begins when a user sends a message through the chat interface.

The node captures:
- User query
- Session information
- Chat input

---

## 2. AI Agent Node

The AI Agent node:
- Receives user prompts
- Handles AI orchestration
- Manages workflow execution
- Routes prompts to the language model

Dynamic prompt mapping was configured using:

```javascript
{{ $json.chatInput }}
```

This allows real-time user messages to be passed directly into the AI pipeline.

---

## 3. Ollama Chat Model

The Ollama Chat Model node connects n8n Cloud with a locally hosted LLM.

Model used:

```text
llama3.2:latest
```

The model performs:
- prompt processing
- response generation
- local inference

without depending on external cloud AI providers.

---

# Challenges Faced During Development

This project involved multiple networking and deployment challenges while integrating cloud-hosted workflows with locally running AI models.

---

## 1. Cloud-to-Local Connectivity Issue

The first major issue was understanding that:
- n8n was running on cloud infrastructure
- Ollama was running locally

This prevented direct communication between both systems.

### Solution

ngrok was introduced to expose the local Ollama server publicly.

Command used:

```bash
ngrok http 11434
```

---

## 2. HTTP 403 Forbidden Error

After connecting ngrok, requests still failed with:

```text
403 Forbidden
```

### Cause

Ollama rejected externally forwarded requests due to host-header mismatches.

---

## 3. Host Header Rewrite Configuration

To solve the issue, ngrok had to rewrite incoming request headers.

Final working command:

```bash
ngrok http 11434 --host-header="localhost:11434"
```

This allowed Ollama to treat forwarded requests as localhost traffic.

---

## 4. External Origin Restriction

By default, Ollama restricts many external-origin requests.

Even after ngrok forwarding, requests from n8n Cloud were blocked.

### Solution

Ollama was started with external-origin access enabled:

```bash
set OLLAMA_ORIGINS=*
ollama serve
```

This allowed requests from:
- ngrok
- n8n Cloud
- external APIs

---

## 5. Port Conflict Error

While debugging, restarting Ollama repeatedly caused:

```text
Only one usage of each socket address is normally permitted
```

### Cause

Another Ollama process was already running on port 11434.

### Solution

The existing Ollama instance was terminated:

```bash
taskkill /F /IM ollama.exe
```

Then Ollama was restarted correctly.

---

## 6. Incorrect Credential Configuration

Several connection failures were caused by:
- adding `/api/chat`
- using invalid ngrok URLs
- adding trailing slashes

### Correct Base URL Format

```text
https://your-ngrok-url.ngrok-free.app
```

No extra endpoint paths were required.

---

## 7. Model Validation

The model name inside n8n had to exactly match the locally installed Ollama model.

Installed models were verified using:

```bash
ollama list
```

Final model used:

```text
llama3.2:latest
```

---

# Features

- Local AI inference
- Cloud-to-local AI orchestration
- Real-time AI responses
- Secure tunneling using ngrok
- Execution logging
- Dynamic prompt mapping
- Local LLM deployment
- Token usage monitoring
- AI workflow automation

---

# Sample User Prompt

```text
Explain workflow automation in simple terms.
```

---

# Sample AI Response

```text
Workflow automation refers to the use of software and technology to automate repetitive tasks and business processes without manual intervention.
```

---

# Token Usage Monitoring

The workflow tracks:
- Prompt tokens
- Completion tokens
- Total token usage

This helps optimize:
- model efficiency
- prompt engineering
- response generation

---

# Request Lifecycle

1. User sends a prompt through the n8n chat interface.
2. Chat Trigger node captures the input.
3. AI Agent node processes the request.
4. ngrok securely forwards the request.
5. Ollama receives the API call locally.
6. Llama 3.2 processes the prompt.
7. AI response is generated.
8. Response is returned back to n8n Cloud.
9. Execution logs and token statistics are generated.
10. Final response is displayed in the chat interface.

---

# Project Structure

```text
ollama-ai-agent-n8n/
│
├── workflow/
│   └── ollama-ai-agent-workflow.json
│
├── screenshots/
│   ├── workflow-architecture.png
│   ├── ai-chat-interface.png
│   ├── execution-logs.png
│   └── ollama-response-output.png
│
└── README.md
```

---

# Setup Instructions

## Step 1 — Install Ollama

Download Ollama from:

https://ollama.com/download/windows

---

## Step 2 — Pull Llama 3.2 Model

```bash
ollama pull llama3.2
```

---

## Step 3 — Start Ollama with External Access

```bash
set OLLAMA_ORIGINS=*
ollama serve
```

Keep this terminal running.

---

## Step 4 — Start ngrok Tunnel

```bash
ngrok http 11434 --host-header="localhost:11434"
```

Keep this terminal running.

---

## Step 5 — Configure Ollama Credential in n8n Cloud

Inside the Ollama Chat Model node:
- use the ngrok forwarding URL
- do not add `/api/chat`
- use model:

```text
llama3.2:latest
```

---

## Step 6 — Execute Workflow

Run the workflow and interact with the AI agent using the chat interface.

---

# Future Enhancements

- Multi-agent workflows
- AI memory integration
- Vector databases
- Retrieval-Augmented Generation (RAG)
- Document question answering
- Voice-enabled AI agents
- WhatsApp AI automation
- Autonomous AI task execution

---

# Key Learnings

This project helped in understanding:
- cloud vs local workflow execution
- secure tunneling
- API forwarding
- distributed AI systems
- AI workflow orchestration
- local LLM deployment
- debugging external connectivity issues

---

# Author

Charvi Gosala

---

# License

MIT License
