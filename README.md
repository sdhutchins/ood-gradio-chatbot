# Gradio Chatbot for Cheaha

A minimal Open OnDemand app for launching a Gradio-based LLM chatbot on UAB's Cheaha HPC cluster.

## Table of Contents

- [Project Background](#project-background)
- [Install & Setup](#install--setup)
- [Usage](#usage)
- [Directory Structure](#directory-structure)
- [Contributing](#contributing)
- [License](#license)
- [Authors](#authors)

## Project Background

This project provides a simple, reproducible interface for deploying a local LLM chatbot using Gradio on Cheaha via Open OnDemand. It is designed for biologists and computational biologists who need interactive, on-demand access to language models for research and data exploration.

## Install & Setup

- **Python version:** 3.11+
- **Other software:** Gradio, llama-cpp-python, build tools (GCC)

### Instructions

1. **Create and activate a Python virtual environment:**
   ```sh
   module load Anaconda3
   module load GC
   python3 -m venv ${HOME}/env-chatbot
   . ${HOME}/env-chatbot/bin/activate
   ```
2. **Upgrade pip and install dependencies:**
   ```sh
   python3 -m pip install --upgrade pip setuptools wheel
   python3 -m pip install numpy gradio llama_cpp_python
   ```
3. **Download a pre-trained LLM model (GGUF format):**
   ```sh
   mkdir -p ${HOME}/llm
   wget https://huggingface.co/professorf/Meta-Llama-3-1-8B-Instruct-f16-gguf/resolve/main/llama-3-1-8b-instruct-f16.gguf -O ${HOME}/llm/llama-3-1-8b-instruct-f16.gguf
   ```

## Usage

1. Log in to [Open OnDemand](https://rc.uab.edu/).
2. Select "Gradio Chatbot" from the Interactive Apps menu.
3. Fill in the resource form (partition, CPUs, memory, etc.).
4. Submit the job and wait for the session to start.
5. Click the provided link to access the Gradio chatbot interface.

## Directory Structure

```sh
$ tree -a ood-gradio-chatbot/
ood-gradio-chatbot/
├── app.py                  # Gradio chatbot application
├── README.md               # This file
├── icon.png                # App icon
├── manifest.yml            # App metadata
├── form.yml.erb            # OOD form definition
├── submit.yml.erb          # OOD SLURM submission script
├── template/
│   ├── before.sh.erb       # Pre-launch environment setup
│   ├── script.sh.erb       # Launch script
│   └── after.sh.erb        # Post-launch script (optional)
├── view.html.erb           # OOD web interface button
└── ...                     # (other files as needed)
```

## Contributing

We welcome contributions! [See the docs for guidelines](./CONTRIBUTING.md).

## License

View the [LICENSE](LICENSE) for this project.

## Authors

- Shaurita Hutchins [email](mailto:sdhutchins@uab.edu) | Graduate Research Assistant | [sdhutchins](https://github.com/sdhutchins)
