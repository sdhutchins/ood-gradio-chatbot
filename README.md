# Gradio Chatbot for Cheaha

A minimal Open OnDemand app for launching a Gradio-based LLM chatbot on UAB's Cheaha HPC cluster.

This was modified from and inspired by Wake Forest's HPC example of [OOD-GradioApps](https://github.com/WFU-HPC/OOD-GradioApps/tree/main).

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
- **Other software:** Gradio, llama-cpp-python, build tools (GCC, CMake, OpenBLAS, CUDA)

### Instructions

1. **Create and activate a Python virtual environment:**
   ```sh
   module load Anaconda3
   module load GCCcore/12.2.0
   module load GCC/12.2.0           # if this exists — otherwise skip
   module load CUDA/12.3.0
   module load CMake/3.24.3-GCCcore-12.2.0
   conda activate env-chatbot
   conda env create -f env-chatbot.yml
   conda activate env-chatbot

   # Set compiler environments
   export CC=$(which gcc)
   export CXX=$(which g++)
   export CUDAHOSTCXX=$CXX
   export CUDACXX=$(which nvcc)
   ```
2. **Upgrade pip and install dependencies:**
   ```sh
   CMAKE_ARGS="-DLLAMA_CUDA=on -DLLAMA_CUBLAS=on -DLLAMA_CUDA_FORCE_DMMV=on -DLLAMA_NATIVE=off" pip install llama-cpp-python==0.2.77 --no-binary :all:
   ```
3. **Download a pre-trained LLM model (GGUF format):**
   ```sh
   mkdir -p ${HOME}/llm
   # Download a smaller, more reliable model
   wget https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-gguf/resolve/main/Phi-3-mini-4k-instruct-q4.gguf -O ${HOME}/llm/Phi-3-mini-4k-instruct-q4.gguf
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
