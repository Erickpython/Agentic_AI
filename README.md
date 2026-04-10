## Learning Agentic AI

This is my personal Agentic AI project journal and setup guide. I started with a local model workflow using Ollama and built a Python development environment for connecting those models through LangChain.

### Ollama setup

1. Installed Ollama with the official install script:
   - `curl -fsSL https://ollama.com/install.sh | sh`

2. Pulled local models that I use in this project:
   - `ollama pull mistral`
   - `ollama pull llama3`

These models are now hosted locally by Ollama and can be queried in an offline-first or low-latency way.

### Workspace and Python environment

1. Created project folder:
   - `mkdir AGENTIC_AI && cd AGENTIC_AI`

2. Created virtualenv:
   - `python3 -m venv agenticvenv`
   - `source agenticvenv/bin/activate`

3. Installed dependencies:
   - `pip install ollama langchain langchain-ollama`

### Using LangChain with Ollama local models

I use LangChain as the orchestration layer in Python while Ollama serves the local LLMs.

Example workflow:

- Set up a LangChain Ollama client to point to local Ollama API endpoint (default `http://127.0.0.1:11434`).
- Select a model name from the pulled models, e.g. `mistral` or `llama3`.
- Run prompts through LangChain chains (LLMChain, ConversationChain, etc.) for higher-level agent execution and state management.

#### Sample connection code

```python
from langchain_ollama import Ollama
from langchain import LLMChain, PromptTemplate

ollama = Ollama(
    model="mistral",
    base_url="http://127.0.0.1:11434"
)

template = "Write a short summary of: {topic}"
prompt = PromptTemplate(template=template, input_variables=["topic"])
chain = LLMChain(llm=ollama, prompt=prompt)

result = chain.run({"topic": "Agentic AI learning workflow"})
print(result)
```

### What I learned

- Running local models with Ollama enables fast experimentation without cloud API dependency.
- LangChain provides modular agents, prompt templating, and memory abstractions on top of local LLMs.
- This combo is ideal for Agentic AI research where you do repeated prompt iterations and local model control.
