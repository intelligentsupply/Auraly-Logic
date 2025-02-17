# Myth Frame - An Autonomous AI by DEv

<div align="center">

  <img src="https://github.com/intelligentsupply/Nivue-Arch/blob/af03e12c8decb6b552b86ae88a5511ceb66ead8e/Nivue%20Arch%20(1).png" width="100%" />
</div>

## Table of Contents
- [Overview](#Overview)
- [Core Features](#core-features)
- [Extension Points](#extension-points)
- [Quick Start](#quick-start)
- [Using Echo.exe as a Module](#using-echoexe-as-a-module)

## Overview
ECHO.EXE is an autonomous AI agent engine built with TypeScript, Rust, and Go, emphasizing modular architecture and platform independence. It provides a flexible foundation for building AI-driven systems with:

- Plugin-based architecture with swappable components
- Multi-provider LLM support (GPT-4, Claude, and custom providers)
- Cross-platform agent management
- Extensible manager system for unique behaviors
- Vector-based semantic storage with pgvector

## Core Features

### Plugin Architecture
- **Manager System:** Extend functionality via custom managers:
  - **Echo Manager:** Captures and reflects interactions as memory patterns
  - **Personality Manager:** Adapts responses based on user interaction history
  - **Custom Managers:** Add specialized behaviors and processes

### State Management
- **Shared State System:** Centralized state management:
  - Cross-manager communication
  - Custom data injection
  - Persistent agent memory

### LLM Integration
- **Provider Abstraction:** Support multiple LLM providers:
  - Built-in support for GPT-4 and Claude
  - Extensible interfaces for custom LLMs
  - Configurable model selection with automatic fallback handling

### Platform Support
- **Platform Agnostic Core:**
  - CLI and API interfaces included
  - Extensible platform manager for custom integrations

### Storage Layer
- **Semantic Memory Layer:**
  - PostgreSQL with pgvector for vector-based semantic search
  - Customizable memory storage solutions
  - Vector embedding support

### Toolkit/Function System
- **Modular Toolkit Integration:**
  - Plug-and-play custom tools
  - Function calling and auto-response integration
  - Context-aware tool execution

## Extension Points
1. **LLM Providers:** Implement new AI providers with the LLM interface:
```go
 type Provider interface {
    GenerateCompletion(context.Context, CompletionRequest) (string, error)
    EmbedText(context.Context, string) ([]float32, error)
 }
```

2. **Managers:** Add new behaviors via the Manager interface:
```go
 type Manager interface {
    GetID() ManagerID
    Process(state *state.State) error
    Context(state *state.State) ([]state.StateData, error)
 }
```

## Quick Start
1. Clone the repository:
```bash
git clone https://github.com/mirroor-labs/echo-exe
```
2. Configure your environment:
```bash
cp .env.example .env
```
3. Install dependencies:
```bash
npm install
cargo build
go mod download
```
4. Launch the environment:
```bash
npm run dev
```

## Environment Variables
```env
DB_URL=postgresql://user:password@localhost:5432/echo
OPENAI_API_KEY=your_openai_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key
```

## Using Echo.exe as a Module
1. Install the ECHO.EXE module:
```bash
npm install @mirroor/echo-exe
```
2. Import and initialize in your code:
```typescript
import { Engine, LLMClient, MemoryManager } from '@mirroor/echo-exe';
const llmClient = new LLMClient({
  provider: 'gpt4',
  apiKey: process.env.OPENAI_API_KEY,
});
const engine = new Engine({ llm: llmClient });
const response = await engine.process("Hello, Echo");
```

## Contact
- Website: [mirroor.ai](https://mirroor.ai)
- Email: contact@mirroor.ai
- Twitter: [@mirroor_ai](https://x.com/mirroor_ai)

## License
Licensed under the MIT License.

