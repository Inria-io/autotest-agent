# AutoTest Agent

An agent that generates, runs, and repairs pytest unit tests for a Python repository and
reports the coverage gained.

## What it does
[2-3 sentences: reads a module, writes tests, runs them in an isolated folder, repairs
failures for up to 3 rounds, prints coverage before/after.]

## Setup (from a clean machine)
```bash
git clone [repo link]
cd [repo folder]
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env             # then put your own API key in .env
```

## Usage
```bash
python -m autotest ./path/to/repo --module file.py
```

## Evaluation
[How to run the evaluation, e.g. `python benchmark/evaluate.py`, and where results are saved.]
Summary of results: [table: one-shot vs agent loop vs coverage-guided retry].

## Benchmark repositories and third-party components
[List every open-source repo, dataset, and library you use, with links.]

## Agentic tools used
[Tool(s), free or paid, and any switch (also recorded in DECISIONS.md).]

## Team
[Member 1], [Member 2], [Member 3]
