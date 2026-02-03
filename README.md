# AI-Powered Research Proposal Automation

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![LangChain](https://img.shields.io/badge/LangChain-0.3.21-green.svg)](https://langchain.com)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-0.6.3-orange.svg)](https://www.trychroma.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> An agentic AI system that automates NIH research proposal generation by ingesting funding announcements (NOFOs), performing semantic relevance scoring on research papers, and generating aligned proposal ideas.

**Developed as capstone project for Johns Hopkins University Generative AI Certificate Program**

---

## 🎯 Problem Statement

Organizations and researchers maintain large archives of publications. When responding to competitive grants—especially NIH NOFOs—it becomes extremely difficult to:

- Align past work with new funding calls
- Extract relevant expertise from unrelated projects  
- Ideate novel, fundable research proposals
- Generate compliant proposal text that satisfies review criteria

The manual effort to match research to funding criteria and write compelling proposals is labor-intensive and prone to missed opportunities.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        RESEARCH PROPOSAL AI SYSTEM                       │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐               │
│  │  NOFO Doc    │    │  Research    │    │   Vector     │               │
│  │  (PDF)       │───▶│  Papers      │───▶│   Store      │               │
│  │              │    │  (PDFs)      │    │  (ChromaDB)  │               │
│  └──────────────┘    └──────────────┘    └──────────────┘               │
│         │                   │                   │                        │
│         ▼                   ▼                   ▼                        │
│  ┌──────────────────────────────────────────────────────┐               │
│  │              TOPIC EXTRACTION MODULE                  │               │
│  │         LLM identifies funding priorities             │               │
│  └──────────────────────────────────────────────────────┘               │
│                            │                                             │
│                            ▼                                             │
│  ┌──────────────────────────────────────────────────────┐               │
│  │           RELEVANCE ASSESSMENT MODULE                 │               │
│  │    Hybrid Search: BM25 + Semantic Embeddings          │               │
│  │    Filters papers by alignment to NOFO topic          │               │
│  └──────────────────────────────────────────────────────┘               │
│                            │                                             │
│                            ▼                                             │
│  ┌──────────────────────────────────────────────────────┐               │
│  │            PROPOSAL IDEATION ENGINE                   │               │
│  │    Generates 5 research proposals with:               │               │
│  │    • Target condition & digital platform              │               │
│  │    • Intervention mechanism                           │               │
│  │    • Health equity focus                              │               │
│  │    • Source citations                                 │               │
│  └──────────────────────────────────────────────────────┘               │
│                            │                                             │
│                            ▼                                             │
│  ┌──────────────────────────────────────────────────────┐               │
│  │              RAG-ENHANCED DRAFTING                    │               │
│  │    Full proposal sections with retrieved context      │               │
│  └──────────────────────────────────────────────────────┘               │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Technical Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **LLM** | GPT-4o-mini | Topic extraction, relevance scoring, proposal generation |
| **Orchestration** | LangChain 0.3.21 | Prompt management, chain composition |
| **Vector Store** | ChromaDB 0.6.3 | Semantic search over research papers |
| **Embeddings** | Sentence Transformers | Document vectorization |
| **Retrieval** | Hybrid BM25 + Semantic | Best-of-both-worlds search |
| **Document Processing** | PyPDF, LangChain loaders | PDF ingestion and chunking |

---

## 📊 Key Features

### 1. Intelligent Topic Extraction
Automatically identifies funding priorities from complex NOFO documents, extracting actionable research themes.

### 2. Semantic Relevance Scoring
Uses hybrid retrieval (BM25 keyword matching + dense embeddings) to filter research papers by alignment to funding criteria.

### 3. Multi-Proposal Ideation
Generates 5 distinct research proposals, each including:
- Target mental health condition
- Digital platform strategy
- Intervention mechanism
- Health equity population focus
- Supporting citations

### 4. RAG-Enhanced Drafting
Retrieves relevant context from filtered papers to generate compliant proposal sections.

---

## 🚀 Results

| Metric | Outcome |
|--------|---------|
| Papers processed | 50+ research publications |
| Relevance filtering | Reduced candidate papers by 70% |
| Proposals generated | 5 NOFO-aligned research ideas |
| Time savings | ~80% vs manual proposal ideation |

---

## 📁 Repository Structure

```
├── README.md
├── notebooks/
│   ├── final_project_proposal_ai.ipynb    # Main capstone notebook
│   └── midterm_email_classifier.ipynb     # Email intelligence system
├── docs/
│   ├── architecture.md                     # System design details
│   └── sample_outputs/                     # Generated proposal examples
├── requirements.txt
└── LICENSE
```

---

## 🛠️ Installation

```bash
# Clone repository
git clone https://github.com/YOUR_USERNAME/research-proposal-ai.git
cd research-proposal-ai

# Install dependencies
pip install -r requirements.txt

# Configure API keys
cp config.example.json config.json
# Edit config.json with your OpenAI API key
```

---

## 📖 Usage

```python
# Load NOFO document
from langchain.document_loaders import PyPDFLoader
nofo = PyPDFLoader("path/to/NOFO.pdf").load()

# Extract funding topic
topic = llm.invoke(topic_extraction_prompt)

# Filter relevant research
relevant_papers = relevance_filter(papers, topic)

# Generate proposals
proposals = llm.invoke(ideation_prompt)
```

See `notebooks/final_project_proposal_ai.ipynb` for complete implementation.

---

## 👤 Author

**Thomas Hornacek**  
MBA, DePaul University | Generative AI Certificate, Johns Hopkins University

- 9+ years market research & analytics (Kantar, C+R Research, quantilope, Harris Poll)
- Specialization: AI-enhanced research operations, pricing analytics, brand tracking
- [LinkedIn](https://linkedin.com/in/thomashornacek)

---

## 📜 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- Johns Hopkins University Engineering for Professionals
- Dr. Ian McCulloh (course instructor)
- NIH/NIMH for public NOFO documentation
