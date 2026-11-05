# Notes on LLM Agents

Short, self-contained notes on how LLM agents work, one concept per file. Each note has its own explanation, code and diagrams (Mermaid, which GitHub and VS Code render), and can be read on its own.

## Index

### Agent fundamentals

- [Tool calling](tool-calling.md): how a model asks your code to run a function, and how the result goes back.
- [The agent loop](agent-loop.md): tool calling in a loop, the message history as memory, and a worked maze example.

## Source

These notes come from my learning in Ed Donner's course "AI FDE: The Forward Deployed Engineer & Agentic AI Architect". They are written to stand alone, so you don't need the course to follow them.

## Adding a note

- One concept per file, named in lowercase kebab-case (`tool-calling.md`).
- Start with a one-paragraph summary, then explanation, diagrams, gotchas and a "Related" section.
- Add a line to the index above.
