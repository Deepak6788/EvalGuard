# EvalGuard

[![Python](https://img.shields.io/badge/Python-3.12-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.13-red)](https://pytorch.org/)
[![Transformers](https://img.shields.io/badge/Transformers-HuggingFace-yellow)](https://huggingface.co/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
EvalGuard is a modular Python framework for evaluating AI-generated responses across multiple quality dimensions, including relevance, instruction compliance, completeness, groundedness, and hallucination risk.

The framework provides a structured and extensible approach for evaluating AI-generated responses by combining multiple complementary evaluation metrics into a unified assessment.

---

## Why EvalGuard?

Large Language Models are often evaluated using a single metric, which may overlook important aspects of response quality. EvalGuard combines multiple complementary evaluation techniques into a unified framework, making it easier to analyze AI-generated responses from different perspectives such as semantic relevance, instruction following, completeness, factual grounding, and hallucination risk.

---

## Features

- Evaluates semantic relevance between prompts and responses using transformer-based cross-encoders.
- Verifies adherence to prompt instructions such as sentence limits, word limits, JSON formatting, and list formatting.
- Measures response completeness for single-part and multi-part questions.
- Detects unsupported and contradictory claims using evidence retrieval and Natural Language Inference (NLI).
- Estimates hallucination risk based on claim-level analysis.
- Generates an overall evaluation score and verdict.
- Provides a command-line interface for interactive evaluation.
- Exports evaluation reports in JSON format.

---

## Key Highlights

- Modular evaluation pipeline
- Transformer-based semantic relevance scoring
- Hybrid completeness evaluation
- Evidence retrieval with claim verification
- Hallucination risk estimation
- Command-line interface
- JSON report export
- Comprehensive automated test suite

---

## Evaluation Pipeline

Prompt
        │
        ▼
Relevance Evaluation
        │
        ▼
Instruction Compliance
        │
        ▼
Completeness Evaluation
        │
        ▼
Groundedness Analysis
        │
        ▼
Hallucination Detection
        │
        ▼
Overall Score & Verdict

---

## Evaluation Metrics

### Relevance
Measures how well the response answers the user's prompt after removing formatting-related instructions.

Model:
- CrossEncoder (MS MARCO MiniLM)

---

### Instruction Compliance
Checks whether the response follows explicit prompt instructions, including:

- Sentence limits
- Word limits
- Bullet list requirements
- JSON output requirements

---

### Completeness
Determines whether every part of a prompt has been answered.

Supports:

- Multi-part questions
- Comparison questions
- "Why" questions
- "How" questions
- Person
- Time
- Location
- Method
- Reason detection

---

### Groundedness
Extracts claims from the response, retrieves the most relevant supporting evidence from the reference context, and validates each claim using Natural Language Inference.

Possible outcomes:

- Entailment
- Neutral
- Contradiction

---

### Hallucination Risk
Calculates hallucination risk from the groundedness analysis by identifying unsupported and contradictory claims.

---

## Project Structure

```
EvalGuard/
│
├── core/
│   ├── evaluation_engine.py
│   ├── evidence_retriever.py
│   └── models.py
│
├── evaluators/
│   ├── relevance.py
│   ├── instruction.py
│   ├── completeness.py
│   ├── groundedness.py
│   └── hallucination.py
│
├── utils/
│   ├── cli.py
│   ├── report_formatter.py
│   ├── report_exporter.py
│   └── text_processing.py
│
├── tests/
│   ├── test_relevance.py
│   ├── test_instruction.py
│   ├── test_completeness.py
│   ├── test_groundedness.py
│   ├── test_hallucination.py
│   ├── test_engine.py
│   └── test_cli.py
│
├── config.py
├── main.py
├── requirements.txt
└── README.md
```

---

## Models Used

| Evaluation Task | Model |
|-----------------|-------|
| Relevance | cross-encoder/ms-marco-MiniLM-L6-v2 |
| Embeddings | sentence-transformers/all-MiniLM-L6-v2 |
| Natural Language Inference | cross-encoder/nli-deberta-v3-base |

---

 ## Technologies Used

- Python 3.12
- PyTorch
- Transformers
- Sentence Transformers
- Natural Language Inference (NLI)
- Hugging Face Transformers

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Deepak6788/EvalGuard.git
cd EvalGuard
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

The required transformer models are downloaded automatically during the first execution.

---

## Usage

Run the application:

```bash
python main.py
```

Provide the following inputs when prompted:

- Prompt
- AI Response
- Reference Context

EvalGuard will generate:

- Relevance Score
- Instruction Score
- Completeness Score
- Groundedness Score
- Hallucination Risk
- Overall Evaluation Score
- Final Verdict

---

## Example

Prompt

```
Who created Nova and when was it released?
```

Response

```
Nova was created by Arin and released in 2023.
```

Reference Context

```
Nova was created by Arin.
The programming language was released in 2023.
```

Expected Output

```
Verdict              : EXCELLENT
Overall Score        : 1.0000

Relevance            : 1.0000
Instruction          : 1.0000
Completeness         : 1.0000
Groundedness         : 1.0000
Hallucination Risk   : 0.0000
```

---

## Testing

The project includes dedicated test modules for each evaluation component.

Run individual tests using:

```bash
python -m tests.test_relevance
python -m tests.test_instruction
python -m tests.test_completeness
python -m tests.test_groundedness
python -m tests.test_hallucination
python -m tests.test_engine
```

---

## Future Improvements

Potential enhancements include:

- Additional evaluation metrics and customizable scoring.
- Batch evaluation of multiple responses.
- Web-based interface.
- REST API integration.
- Evaluation history and analytics dashboard.
- Support for multiple evidence retrieval strategies.

---

## License

This project is licensed under the MIT License.