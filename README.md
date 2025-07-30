
````markdown
# llamaware agent

modular C++ AI agent with offline + online LLM support, safe shell commands, web search, and memory.

## install

### dependencies

macOS:
```bash
brew install cpr nlohmann-json cmake
````

ubuntu/debian:

```bash
sudo apt update
sudo apt install libcpr-dev nlohmann-json3-dev cmake build-essential
```

required:

* c++17 compiler (gcc 7+, clang 5+, or msvc 2017+)
* cmake ≥ 3.14
* [cpr](https://github.com/libcpr/cpr)
* [nlohmann/json](https://github.com/nlohmann/json)
* [ollama](https://ollama.com/download) (for offline mode)
* together ai + serpapi keys (for online + search)

## build

```bash
git clone https://github.com/bniladridas/llamaware.git
cd llamaware
mkdir build && cd build
cmake ..
make
```

optional:

```bash
cp .env.example .env
# add your API keys
```

## run

### run the c++ agent

```bash
./build/bin/llamaware-agent
```

### run preflight checks

```bash
make preflight
```

### start the web ui (optional)

```bash
cd web
npm install
npm start
```

> 💡 fix any import errors before starting.

## usage

on startup:

```
choose mode [1=online / 2=offline]: 2
offline mode: llama3.2
agent initialized. type 'help' or 'exit'
```

available commands:

```
  search:<query>        → web search via serpapi
  cmd:<command>         → run safe shell command
  read:<file>           → read file contents
  write:<file> <text>   → write to file

  help                  → list commands
  exit / quit           → exit the agent
```

example session:

```
› search:latest ai news
[search results]

› cmd:ls -la
[executing]: ls -la
[command result]
total 48
...
```

## structure

```
src/
  main.cpp               → entry point
  core/agent.cpp         → main logic
  services/
    ai_service.cpp       → together + ollama api
    command_service.cpp  → shell exec
    file_service.cpp     → file ops
    web_service.cpp      → serpapi integration
  utils/
    ui.cpp               → terminal ui helpers
    config.cpp           → env setup
  data/memory_manager.cpp → context memory

include/                → headers
data/                   → runtime data
.env                    → config file
web/                    → react frontend
```

## customize

* change model: `agent.cpp`
* tweak ui: `ui.cpp` (ansi colors)
* memory file: `memory_manager.cpp`
* add features: chat, search, etc

## license

MIT — see `LICENSE`
(c) 2025 bniladridas