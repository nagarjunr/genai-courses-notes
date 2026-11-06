# Notes on LLM Agents

Short, self-contained notes on how LLM agents work, one concept per file. Each note has its own explanation, code and diagrams (Mermaid, which GitHub and VS Code render), and can be read on its own.

## Index

### Agent fundamentals

- [Tool calling](tool-calling.md): how a model asks your code to run a function, and how the result goes back.
- [The agent loop](agent-loop.md): tool calling in a loop, the message history as memory, and a worked maze example.

## Course roadmap

What the course covers, by week. Ticked items have notes.

### Week 1: AI Engineer

- [ ] The skills of an AI Architect and Forward Deployed Engineer (FDE), and the roadmap to get there
- [ ] Accelerating delivery with Claude Code and the Agentic Development Lifecycle (ADLC) while staying accountable
- [ ] Harness engineering: building agents with LangChain, Deep Agents and the Claude Agent SDK
  - [x] [Tool calling](tool-calling.md)
  - [x] [The agent loop](agent-loop.md)
- [ ] Choosing between frontier, open-source and local LLMs on intelligence, speed, token cost and privacy

### Week 2: AI Architect

- [ ] Evals and observability in Langfuse to drive architecture decisions and measure business outcomes
- [ ] Long-term memory for agents with agentic RAG over MCP, using vector datastores
- [ ] Production-grade agent workflows in LangGraph: durable state, crash recovery and human in the loop
- [ ] Scaling and optimizing with agent swarms, LLM as a judge and recursive self-improvement

### Week 3: AI FDE

- [ ] Leading AI initiatives with clients, from discovery and metrics to governance, responsible AI and handover
- [ ] Securing agents against prompt injection and the lethal trifecta, with guardrails, policies and AI gateways
- [ ] A data and integration architecture for agents: an enterprise context layer and an MCP gateway
- [ ] Deploying LangGraph agents to production with AWS Bedrock AgentCore Runtime, Gateway, Policy and Memory

## Source

These notes come from my learning in Ed Donner's course "AI FDE: The Forward Deployed Engineer & Agentic AI Architect". They are written to stand alone, so you don't need the course to follow them.

## Adding a note

- One concept per file, named in lowercase kebab-case (`tool-calling.md`).
- Start with a one-paragraph summary, then explanation, diagrams, gotchas and a "Related" section.
- Add a line to the index above.
