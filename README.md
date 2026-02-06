# Advanced RAG Assignment: Code Q&A and Multi-Source Retrieval

This assignment builds on the concepts from the Basic RAG Lab. You will implement two advanced RAG systems that introduce routing, tool use, and multi-source retrieval - key concepts that bridge basic RAG to agentic RAG patterns.

## Learning Objectives

- Build RAG systems that work with code and multiple file types
- Implement query routing to select appropriate retrieval strategies
- Combine keyword search (grep/BM25) with semantic search
- Handle structured and unstructured data sources
- Introduce tool-use patterns (without full agent frameworks)

## Prerequisites

- Completed the Basic RAG Lab
- Understanding of chunking, indexing, and retrieval strategies
- Familiarity with vector stores and embeddings
- Python 3.10+
- API keys (Groq is FREE)

## Assignment Overview

This assignment has two parts:

### Part 1: Code Q&A System (50 points)

Build a RAG system that can answer questions about a real open-source codebase.

**Challenges:**
- Multiple file types (.py, .md, .json, .yaml, .toml, etc.)
- Code-aware chunking (functions, classes, not just text blocks)
- Large scale - working with 100+ files
- Combining vector search with keyword search (grep-like patterns)

**What you'll implement:**
- Document loaders for different file types
- Code-specific text splitters
- Hybrid retrieval (semantic + keyword)
- Query routing: should I search code? docs? configs?

**Example questions your system should handle:**
- "How does authentication work in this codebase?"
- "What configuration options are available?"
- "Where is the main entry point?"
- "What dependencies does this project use?"

### Part 2: Multi-Source RAG with Routing (50 points)

Build a RAG system that intelligently routes queries to different data sources.

**Data Sources:**
- Text documents (markdown, text files)
- Structured data (CSV, JSON)
- Configuration files
- API documentation

**What you'll implement:**
- Query router that decides which source(s) to query
- Source-specific retrieval strategies
- Result combination from multiple sources
- Query rewriting for different source types

**Example questions:**
- "What is the default timeout setting?" -> Config files
- "How do I use the authentication module?" -> Documentation
- "List all available endpoints" -> Could need multiple sources

## Getting API Keys

| Provider | Link | Notes |
|----------|------|-------|
| **Groq** (Recommended) | https://console.groq.com/ | FREE tier, no credit card |
| OpenAI | https://platform.openai.com/ | Paid |
| Anthropic | https://console.anthropic.com/ | Paid |
| Cohere | https://dashboard.cohere.com/ | FREE tier (for re-ranking) |

## Environment Setup

### Step 1: Install uv (Python Package Manager)

```bash
# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# Restart your shell or run:
source $HOME/.local/bin/env
```

### Step 2: Create Virtual Environment and Install Dependencies

```bash
# Navigate to the assignment directory
cd <your-repo-path>

# Create virtual environment and install all dependencies
uv sync

# Activate the virtual environment
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### Step 3: Register the Kernel for Jupyter

```bash
# Register the kernel (run this with venv activated)
uv run python -m ipykernel install --user --name=advanced-rag --display-name="Advanced RAG"
```

### Step 4: Configure Your API Keys

```bash
# Copy the example environment file
cp .env.example .env

# Edit .env and add your API key(s)
```

## Project Structure

```
advanced-rag/
├── data/
│   ├── codebase/          # Sample codebase for Part 1
│   ├── docs/              # Documentation files
│   ├── configs/           # Configuration files
│   └── structured/        # CSV/JSON data files
├── notebooks/
│   ├── part1_code_qa.ipynb
│   └── part2_multi_source.ipynb
├── src/                   # Your implementation
├── tests/                 # Test cases
├── .env.example
├── pyproject.toml
└── README.md
```

## Key Concepts

### Query Routing

Instead of always using the same retrieval strategy, a router decides:
- Which data source(s) to query
- Which retrieval method to use (semantic, keyword, hybrid)
- Whether to rewrite the query for specific sources

```
User Query -> Router -> [Source A, Source B] -> Combine Results -> Generate Answer
```

### Code-Aware Chunking

Standard text splitters don't understand code structure. For code:
- Split by functions/classes, not arbitrary character counts
- Preserve imports and context
- Handle different languages/file types appropriately

### Hybrid Retrieval

Combine multiple retrieval strategies:
- **Semantic Search**: Good for conceptual questions ("How does X work?")
- **Keyword Search**: Good for specific terms, function names, error messages
- **Ensemble**: Weight and combine results from both

## Deliverables

### Part 1: Code Q&A (50 points)
- [ ] Implement document loaders for multiple file types
- [ ] Implement code-aware chunking
- [ ] Build hybrid retrieval (semantic + keyword)
- [ ] Answer test questions correctly
- [ ] Save results to `part1_results.txt`

### Part 2: Multi-Source RAG (50 points)
- [ ] Implement query router
- [ ] Handle at least 3 different source types
- [ ] Implement source-specific retrieval
- [ ] Combine results from multiple sources
- [ ] Save results to `part2_results.txt`

## Grading Criteria

| Criteria | Points |
|----------|--------|
| Part 1: Document loading and chunking | 15 |
| Part 1: Hybrid retrieval implementation | 15 |
| Part 1: Answer quality on test questions | 20 |
| Part 2: Query router implementation | 15 |
| Part 2: Multi-source handling | 15 |
| Part 2: Answer quality on test questions | 20 |
| **Total** | **100** |

## Tips

1. **Start with the lab code** - Reuse patterns from basic-rag
2. **Test incrementally** - Get one file type working before adding more
3. **Use logging** - Debug retrieval issues by logging what's being retrieved
4. **Experiment with chunk sizes** - Code may need different chunk sizes than prose

## Resources

- [LangChain Code Splitters](https://python.langchain.com/docs/how_to/code_splitter/)
- [LangChain Routing](https://python.langchain.com/docs/how_to/routing/)
- [Ensemble Retriever](https://python.langchain.com/docs/how_to/ensemble_retriever/)
- [BM25 Retriever](https://python.langchain.com/docs/integrations/retrievers/bm25/)

## Submission

Commit and push all required files:
- Completed notebooks
- `part1_results.txt`
- `part2_results.txt`
- Any source code in `src/`
