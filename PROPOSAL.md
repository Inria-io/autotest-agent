# Final Project Proposal: AutoTest Agent

**Group:** Daurenuly Daulet (S23068962), Argynbek Magzhan (S23069465), Inria Altje Kalalo (S26078838)
**Section:** [section] | **Repository:** https://github.com/Inria-io/autotest-agent

## 1. Problem and user

Many Python developers, especially students and small teams, spend a lot of time writing unit tests by hand, or ship code with insufficient test coverage because writing tests is slow and tedious. Without tests, bugs go unnoticed and refactoring is risky.

**AutoTest Agent** is a command-line tool for a developer who owns a Python repository. An AI-powered agent analyzes the source code of a module, generates pytest tests, runs them, automatically repairs the tests that fail, and measures the improvement in code coverage. The user is a student or junior developer who wants a working test suite without writing every test by hand.

## 2. AI feature and how we will measure it

**AI feature:** an agent loop in which an LLM uses tools to complete the task: `read_file`, `run_pytest`, and `get_coverage`. For each target module the agent (1) reads the code, (2) generates pytest tests, (3) runs them in an isolated working folder, (4) reads the errors and the coverage report, and (5) repairs the tests, for a maximum of 3 rounds.

**Evaluation:** we will run the tool on a benchmark of 5 to 8 small open-source Python repositories (named in the README) and compare three setups:
- (a) a one-shot LLM with no loop (baseline),
- (b) the agent loop,
- (c) the agent loop with coverage-guided retry.

Metrics: coverage before and after, share of generated tests that pass, and mutation score (using mutmut) to check that the tests detect real bugs, not only execute lines. Each configuration is run 3 times and the results are averaged. If the agent does not beat the baseline, we report that honestly in REFLECTION.md.

## 3. Agentic tools

Claude Code and OpenAI Codex ([paid / free: confirm]). We will use more than one tool, and any switch will be recorded in DECISIONS.md.

To handle rate limits and cost, we will write PLAN.md before any code, use the strongest model for planning and a cheaper one for routine edits, and keep agent sessions short and focused.

## 4. MVP and stretch goals

**MVP (must work by Mon 16 Nov):** a CLI command `autotest ./repo --module <file.py>` that runs the full loop for one Python module and prints coverage before and after, the number of tests generated, and the number passing. Evidence at the checkpoint: runs on 2 small repositories, with results saved in `results/`.

**Definition of done:** the loop finishes without crashing on both repositories, and coverage increases on both.

**Stretch goals:**
1. Mutation testing on 5 repositories with the full three-way comparison.
2. JavaScript (Jest) support, or an HTML report.

## 5. Data and external APIs

- Open-source Python repositories for the benchmark (listed in the README), plus pytest, coverage.py, and mutmut.
- An LLM API for the tool itself: [provider]. Access: [confirmed / to be confirmed].
- API keys are stored in environment variables only and never committed. Generated code runs only in a sandboxed working folder.
- We collect no personal data.

## 6. Division of work

| Member | Responsibility |
|---|---|
| Daurenuly Daulet | [e.g. agent loop and tools] |
| Argynbek Magzhan | [e.g. CLI and reporting] |
| Inria Altje Kalalo | [e.g. benchmark, evaluation harness, tests] |

All members commit to the repository and contribute to PLAN.md, DECISIONS.md, and REFLECTION.md.
