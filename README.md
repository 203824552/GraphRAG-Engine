# 🧠 GraphRAG Studio

![Windows](https://img.shields.io/badge/Platform-Windows-blue?logo=windows)
![Local](https://img.shields.io/badge/Deployment-100%25_Local-brightgreen)
![Status](https://img.shields.io/badge/Status-Stable_v1.0-orange)

GraphRAG Studio is a fully localized, out-of-the-box desktop application for GraphRAG and multi-hop Question Answering (QA). No Python environment configuration is required. Just extract and run.

---

## ✨ Core Features

- 📦 **Zero-Configuration**: Built-in Deep Learning environment (PyTorch/Transformers). Simply double-click the `.exe` to launch the backend terminal and web interface simultaneously.
- 🔒 **100% Data Privacy**: Fully compatible with local LLMs (e.g., vLLM/Ollama via OpenAI API format). Dense vector indexing is performed locally. Your data never leaves your machine.
- 🧩 **Anti-Hallucination Retrieval**: Implements a 4-phase retrieval pipeline. Features Neff topology entropy checking and automatic `Text Fallback` dense retrieval when graph evidence is insufficient.
- 🛡️ **Robust Data Management**: 
  - **MD5 Hash Deduplication**: Accurately blocks redundant document chunks to save computing resources.
  - Automatic timestamped source archiving for 100% data traceability.

---

## 📥 Download

Due to the inclusion of complete AI dependencies and offline model weights, the package size is approximately **2.62 GB**. Please download the latest release via the official Hugging Face global link below:

- **[📦 Download GraphRAG Studio v1.0 (Windows)](https://huggingface.co/203824552xjc/GraphRAG-Studio-Release/resolve/main/GraphRAG_Studio_v1.0_Windows.zip?download=true)**

*(Note: This is a direct download link hosted on Hugging Face. If you experience slow download speeds in certain regions, using a download manager is recommended.)*

## 🚀 Quick Start Guide

### Step 1: Initialization
Extract the downloaded ZIP file to a directory containing **only English characters** (e.g., `D:\GraphRAG_Studio`). Double-click `GraphRAG_Engine.exe` to launch the application. A background terminal console will appear, and your default web browser will automatically open the UI at `http://127.0.0.1:8866` in a few seconds.

> **💡 Note on First Launch:** 
> The initial startup may take slightly longer. This is completely normal. The system is dynamically auto-generating its core directories in the same folder where the `.exe` is located:
> - 📁 **`workspace/`**: The local database where your knowledge graph JSON files, entity dictionaries, and Dense Vector (`.npy`) indexes are securely cached.
> - 📁 **`data_input/`**: The immutable archive directory. All your uploaded `.txt` files will be automatically timestamped and backed up here to guarantee data traceability.
> - 📁 **`models/`**: The offline cache for HuggingFace embedding/reranker models (if applicable).
> - 📄 **`config.json`**: The core parameter file. If accidentally deleted, the system will self-heal and regenerate a default one upon the next launch.

### Step 2: System Configuration

<img width="3018" height="954" alt="image" src="https://github.com/user-attachments/assets/fd98e726-27d5-48ba-b95f-40f1cfdd024c" />


Before building your knowledge graph, navigate to the **[⚙️ Configuration]** tab to set up your backend engine. The interface allows you to configure two main components:

- **1. LLM Settings (Local Deployment Supported):**
  The system natively supports both cloud APIs (e.g., OpenAI) and fully offline local models (e.g., vLLM, Ollama). 
  - Simply input your `Base URL` and `Model Name`. 
  - *Tip: If you are using a strictly local deployment, you can leave the `API Key` field entirely blank.*

- **2. Retrieval Parameters:**
  Fine-tune the RAG pipeline behavior directly from the UI:
  - **Top-N**: The maximum number of final evidence snippets fed to the LLM.
  - **Entity / Fallback K**: Controls the recall depth for graph traversal and dense text fallback.
  - **Neff Threshold**: A unique topological entropy checker to prevent graph hallucination (lower values enforce stricter evidence alignment).

**🔥 In-Memory Hot Update:** 
Once you click **[💾 Save]**, all parameters are updated in memory instantly. You do not need to restart the software to apply changes.

> **💡 Advanced Tuning:** The UI exposes the most frequently used parameters. For deeper system configurations, you can directly edit the auto-generated `config.json` file in the root directory.

### Step 3: Knowledge Base Construction

<img width="2970" height="1602" alt="image" src="https://github.com/user-attachments/assets/39e7a3b2-1f82-4092-b1a1-8ec89bc83f8e" />


Navigate to the **[📚 KG Construction]** tab to ingest your corpus and build the multi-modal knowledge index. The interface provides a highly robust data ingestion pipeline:

- **1. Flexible Project Management:**
  You can either type a new name to create a fresh project or select an existing project from the dropdown menu to manage your historical knowledge bases.

- **2. Smart Build Modes (The Core Engine):**
  - **Fresh Build (`全新构建`)**: Wipes the selected project's existing graph and vector indexes, allowing you to start with a clean slate. *(Note: The original `.txt` archives in the `data_input/` folder remain safely untouched).*
  - **Incremental Merging (`增量合并`)**: Safely appends new knowledge to an existing project. 
    - 🛡️ **Built-in Hash Deduplication**: When uploading new documents, the system employs an **MD5 Hash Fingerprinting** mechanism at the text-chunk level. It silently intercepts and ignores any redundant text blocks you may have accidentally re-uploaded, saving massive LLM API costs and keeping the vector database pristine.

- **3. Automated Pipeline & Visualization:**
  Upload `.txt` files or paste text directly, then click **[🚀 Start Building]**. The engine will autonomously handle text chunking, graph extraction, and Dense Vector indexing.
  - **Interactive Preview**: Upon completion, a physics-simulated 2D Knowledge Graph will render on the right panel. *(For browser performance optimization, it dynamically displays the Top 100 core nodes).*
  - **Standalone Vector Refresh**: If you've modified the underlying embedding model in `config.json`, simply click **[🔄 Refresh Vector Index]** to rebuild the dense vectors from your historical pure-text JSON cache instantly—no LLM re-extraction required!

### Step 4: Smart Multi-hop QA & Reasoning

Once your knowledge base is built, navigate to the **[💬 Multi-hop QA]** tab. This is where the core engine demonstrates its glass-box reasoning capabilities.

<img width="2886" height="1863" alt="image" src="https://github.com/user-attachments/assets/e3af39e0-5dc0-4ee8-a179-2cf8b28789f8" />


- **1. Query & Transparent Execution:**
  Select your project and input a complex, multi-hop question. The **Backend Terminal Log** will stream the real-time execution status of the 4-Phase pipeline.
- **2. Grounded Answer & Evidence Chain:**
  The LLM generates a concise, direct answer completely devoid of conversational chatter. Below the answer, a strict **Source Evidence Chain** is provided, indicating exactly whether the snippet was retrieved via Graph Alignment (`[KG]`) or Dense Vector Fallback (`[Text]`).
- **3. Reasoning Subgraph Activation:**
  The right panel dynamically renders the specific subgraph activated during the query. Core reasoning nodes and paths are highlighted in **Orange**, visually explaining *how* the engine arrived at the answer.

---

**🛠️ The Glass-Box Analysis Dashboard:**
Scroll down to view the real-time synchronization dashboard. This exposes the entire RAG pipeline's inner workings, making it highly suitable for academic analysis and debugging:

<img width="2841" height="1104" alt="image" src="https://github.com/user-attachments/assets/f1acea44-5bdc-4aad-abda-39c49630d444" />


- **Phase 1 (Logical Skeleton Decomposition):** Deconstructs the complex user query into atomic triples (Head -> Relation -> Tail).
- **Phase 2 (Graph Coarse Ranking & Neff Entropy):** Evaluates the sufficiency of the graph retrieval. It calculates the **Neff Topological Entropy** for each sub-query. If the entropy is too high or paths are missing (🔴 Insufficient), it autonomously triggers the text fallback.
- **Phase 3 (Evidence Re-ranking Top-K):** Displays the cross-modal recalled evidences with their exact **Cosine Similarity Scores**. You can click on any row in the dataframe to read the full original context snippet in the detail box on the right.

---

## ⚙️ System Mechanics & Operational Details

To ensure optimal performance and resource management, please note the following operational behaviors of the GraphRAG Studio engine:

- **The Terminal Console**: 
  When you launch the application, a terminal console opens alongside the web interface. This console acts as the core backend engine. While the web interface provides high-level summarized feedback, the terminal streams detailed execution logs, including text chunking status and precise model retrieval logs. Closing this terminal window will immediately terminate the entire application.

- **Initial Launch Dependencies**: 
  Upon the very first execution, the system automatically fetches necessary NLP dependencies (such as NLTK tokenizers) and the default dense embedding/reranking models into the local `models/` directory. This initial network dependency phase requires additional processing time. All subsequent application launches will bypass this step and load directly from local storage.

- **Memory Residency**: 
  To guarantee minimal latency during multi-hop QA inference, the deep learning models remain active in your system's memory once loaded. These resources are only released when the engine is formally shut down.

- **Graceful Termination**: 
  You do not need to manually close the background terminal. To safely release physical memory and ensure data integrity, navigate to the Configuration tab and click the **Stop Server** button. The system will halt all processes, and the background terminal window will automatically exit after a two-second delay.

- **Session Recovery**: 
  If you accidentally close your browser window, the backend engine continues running safely in the background. Do not restart the executable. Simply open your browser and navigate back to `http://127.0.0.1:8866` to resume your active session.

