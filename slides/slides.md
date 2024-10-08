---
theme: default
background: images/cover.png
class: 'text-center'
highlighter: shiki
lineNumbers: true
title: "A quick introduction to uv and ruff"
drawings:
  persist: false
transition: fade
css: unocss
---

# A quick introduction to 
# uv and Ruff

by [Martin Brochhaus](https://primal.net/p/npub1c80wmfpzc7dkghh93kxtrwpe5gdztynvnk2vy93ge68zmzwrm0yqq5h5s7)

<span class="text-xs text-gray-500">Midjourney prompt: "A package manager for the python programming language written in the rust programming language"</span>

---
src: ./pages/about-me.md
---

---
src: ./pages/about-pugs.md
---

---

# Note to self:

- `uv python uninstall --all`
- `rm -rf ~/.local/share/uv`
- `uv cache clean`

---

# Read The Docs!

- [https://docs.astral.sh/uv/getting-started/](https://docs.astral.sh/uv/getting-started/)

<img src="/images/uv.png" class="w-full mt-3" />

---

# Install uv

- `curl -LsSf https://astral.sh/uv/install.sh | sh`
- add `source $HOME/.cargo/env` to `~/.bash_profile` or `~/.zshrc`
- `uv self update`
- `echo 'eval "$(uv generate-shell-completion zsh)"' >> ~/.zshrc`

---

# Install Python

- `uv python install` <-- the latest version
- `uv python install 3.11` <-- a specific version
- `uv python pin 3.11` <-- make that version active
- `uv run python` <-- python interpreter should be 3.11 now
- `uv python list` <-- list all available versions
- `uv python pin 3.12` <-- pin to another version
- `uv run python` <-- python interpreter should be 3.12 now

---

# Create a project

```zsh
mkdir ~/Projects/
cd ~/Projects/
uv init uv-demo --lib
cd uv-demo
```

This creates the following files:

```
uv-demo
├── README.md
├── pyproject.toml
└── src
    └── uv_demo
        └── __init__.py
```

---

# Pin Python version

- `cd ~/Projects/uv-demo`
- `uv python pin 3.12`
- Also change `requires-python` in `pyproject.toml`
- This creates a `.python-version` file

---

# Add dependencies

- `uv add flask` <-- updates `pyproject.toml`
- `uv pip list` <-- list all installed packages
- `uv add --dev black` <-- adds a dev dependency
- `uv tree` <-- show dependency tree
- `rm -rf .venv` <-- remove virtual environment
- `uv sync` <-- re-create virtual environment (ultra fast!)

---

# Install global tools

- `uv tool install ruff --force`
- `uv tool update-shell`

---

# Run Python scripts

- `uv run ruff check .` <-- run global tool ruff 
- `uv run black .` <-- run venv local tool black
- Add this to `pyproject.toml`:
  ```toml
  [project.scripts]
  hello = "uv_demo:hello"
  ```
- `uv run hello` <-- run the hello script

---

# Everything is awesome now?

- try `uv add uwsgi`

---

# F$#&%K!!!!!

<img src="/images/meme.jpg" />

---

# Use sysconfigpatcher

- `uv tool install git+https://github.com/bluss/sysconfigpatcher --force`
- `uv python dir`
- `sysconfigpatcher ~/.local/share/uv/python/cpython-3.12.5-macos-aarch64-none`
- `uv add uwsgi`

---

# Let's talk about ruff

- Read the docs: [https://docs.astral.sh/ruff/](https://docs.astral.sh/ruff/)
- Install: `uv tool install ruff --force`
- Now you can run ruff manually via `uv run ruff check .` or `uv run ruff format .`
- Add this to `pyproject.toml`:
  ```toml
  [tool.ruff]
  line-length = 80
  ```

---

# Install VSCode extension

- Install [VSCode extension](https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff)
- In VSCode: `Ctrl+Shift+P` then `Open Workspace Settings (JSON)`
- Add:
  ```json
  {
    "editor.rulers": [
        80
    ],
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "charliermarsh.ruff",
    "ruff.lint.extendSelect": [
        "I"
    ]
  }
  ```

- That's it! Try to add some imports to `__init__.py` and see what happens...

---

# Join our Telegram group!

<img src="/images/telegram.jpeg" class="h-[400px] mt-3" />


---
layout: end
---
